<template>
  <transition name="fade">
    <div class="vue-modal" v-show="open">
      <transition name="drop-in">
        <div class="vue-modal-inner" v-show="open">
          <div class="vue-modal-content">
            <slot/>
            <h3 class="invite-others--header" id="inviteOthersHeader">Invite others</h3>
            <button
                type="button"
                class="close-button"
                @click="close"
            >
              <span aria-hidden="true">&times;</span>
            </button>


            <div class="input-email--container" id="inputEmailContainer">
              <div class="invite-input-field--container">
                <input
                    v-model="emailValue"
                    v-on:keydown.enter="addedEmail"
                    class="input-email-field"
                    id="inputEmailField"
                    type="email"
                    placeholder="Enter people E-mails"
                >
                <button
                    @click="addedEmail"
                    type="submit"
                    :disabled="!validated"
                    class="input-email-field--submit-btn"
                    id="inputEmailFieldSubmitBtn"
                >
                  Add
                </button>
              </div>
              <div class="adress-book-container" id="adressBookContainer">
                <p>or add from</p>
                <a href="https://ua.mail.yahoo.com" class="invite-yahoo-btn invite-social--buttons"
                   id="inviteYahooBtn"></a>
                <a href="https://gmail.com/" class="invite-gmail-btn invite-social--buttons" id="inviteGmailBtn"> </a>
                <a href="https://ua.mail.yahoo.com" class="invite-aol-btn invite-social--buttons"
                   id="inviteAolBtn"> </a>
                <a href="https://icloud.com" class="invite-icloud-btn invite-social--buttons" id="inviteIcloudBtn"> </a>
              </div>
            </div>
            <hr class="first-block--line">

            <div class="guest-list--container">
              <div
                  v-for="guests in guestList"
                  :key="guests.emailOfGuest"
                  class="guest-list-items"
              >

                <div class="guests-block">
                  <p class="email-guest--people">{{ guests.emailOfGuest }}</p>
                  <div class="role-of-guest--people--container">

                    <v-select
                        :options="options"
                        @select="optionSelect(guests, $event)"
                        :selected="guests.selectedRole"
                    />

                  </div>
                </div>
                <button
                    @click="deleteGuest(guests)"
                    class="delete-guest-button"
                ></button>
              </div>


            </div>
            <div class="bottom-invite--container">
              <input type="text" class="bottom-invite--text-field" placeholder="Personal message (optional)">
            </div>
            <div class="footer-invites--container">
              <p>{{ guestList.length }} recipients</p>
              <button
                  @click="close"
                  type="submit"
                  class="footer-invites--send-button"
              >
                Send
              </button>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
import {onMounted, onUnmounted} from "vue";
import vSelect from "./v-select.vue";

export default {
  components: {
    vSelect
  },
  data() {
    return {
      emailValue: "",
      guestList: [],
      options: [
        {
          value: 1,
          roleName: "Guest",
          roleText: "Default access level, can leave tributes, share media and stories"
        },
        {
          value: 2,
          roleName: "Administrator",
          roleText: "Can control all aspects of the website, including moderating content posted by others and changing website settings"
        }
      ]
    }
  },
  props: {
    open: {
      type: Boolean,
      required: true
    }
  },
  setup(_, {emit}) {
    const close = () => {
      emit("close")
    };
    const handleKeyup = (event) => {
      if (event.keyCode === 27) {
        close();
      }
    };
    onMounted(() => document.addEventListener("keyup", handleKeyup));
    onUnmounted(() => document.removeEventListener("keydown", handleKeyup));
    return {
      close
    };
  },

  created() {
    const emailsData = localStorage.getItem("emails-list");
    if (emailsData) {
      this.guestList = JSON.parse(emailsData);
    }
  },
  methods: {
    optionSelect(guest, roleParams) {
      guest.selectedRole = roleParams.roleName;
      localStorage.setItem('emails-list', JSON.stringify(this.guestList));
    },
    addedEmail() {
      const newEmail = {
        emailOfGuest: this.emailValue,
        selectedRole: this.options[0].roleName,
      };

      this.guestList.push(newEmail);
      this.emailValue = "";
      localStorage.setItem('emails-list', JSON.stringify(this.guestList));
    },
    deleteGuest(deleteToGuest) {
      this.guestList = this.guestList.filter(guests => guests !== deleteToGuest);
    },
    validateEmail(email) {
      const va = /^([a-z0-9_-]+\.)*[a-z0-9_-]+@[a-z0-9_-]+(\.[a-z0-9_-]+)*\.[a-z]{2,6}$/;
      return va.test(email);
    }
  },
  computed: {
    validated(){
      return this.validateEmail(this.emailValue)
    }
  }

}
</script>

<style>

body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.close-button {
  background: none;
  position: absolute;
  right: 0.63em;
  top: 0.6em;
  border: none;
  cursor: pointer;
  font-size: 2.1em;
}

.vue-modal {
  position: fixed;
  margin: auto auto;
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  background-color: rgba(100, 100, 100, 0.5);
  z-index: 1;
}

.vue-modal-inner {
  max-width: 600px;
  height: 776px;
  margin: 2em auto;
  background: #FFF8EF;
  background-clip: padding-box;
  border-radius: 6px;
}

.vue-modal-content {
  position: relative;
  padding: 1em 1em 2em 1.5em;
  max-height: 743px;
}

.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-leave-to {
  opacity: 0;
}

.drop-in-enter-from,
.drop-in-leave-to {
  opacity: 0;
  transform: translateY(-70px);
}

.drop-in-enter-active,
.drop-in-leave-active {
  transition: all 0.4s ease-out;
}

.invite-input-field--container {
  display: inline-flex;
  margin-top: 32px;
}

.input-email--container {
  width: 34.5em;
  height: 9.5em;
}

.input-email--container ::after {
  border: 1px solid #000;
}

.input-email-field {
  margin-right: 12px;
  padding: 8px 16px;
  width: 425px;
  height: 29px;
  background: #FFFFFF;
  border: 1px solid rgba(51, 51, 51, 0.16);
  border-radius: 6px;
  font-size: 16px;
  color: #ACAAAD;
}

.input-email-field label {
  font-family: 'Open Sans';
  font-style: normal;
  color: #ACAAAD;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
}

.input-email-field--submit-btn {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 12px 24px;
  width: 79px;
  height: 48px;
  opacity: 0.56;
  border: 1px solid #D1CAC1;
  border-radius: 6px;
  font-weight: 600;
  cursor: pointer;
}

.adress-book-container {
  width: 298px;
  height: 49px;
  display: inline-flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 12px;
  color: #3C1F1D;
}

.invite-social--buttons {
  width: 40px;
  height: 40px;
  border: none;
  background-color: transparent;
  background-position: center;
  background-repeat: no-repeat;
  background-size: contain;
  padding: 0;
  box-sizing: border-box;
}

.invite-yahoo-btn {
  background-image: url("../assets/yahooIconImage.png");
}

.invite-gmail-btn {
  background-image: url("../assets/gmailIconImage.png");
}

.invite-aol-btn {
  background-image: url("../assets/aolIconImage.png");
}

.invite-icloud-btn {
  background-image: url("../assets/icloudIconImage.png");
}

.first-block--line {
  margin-left: -25px;
  width: 599px;
  color: #DFD8CF;
}

.guest-list--container {
  width: 100%;
  height: 390px;
  overflow: auto;
}

.delete-guest-button {
  background-image: url("../assets/deleteIconImage.png");
  background-repeat: no-repeat;
  background-size: contain;
  width: 20px;
  height: 27px;
  border: none;
  background-color: transparent;
  margin-left: 9px;
}
.delete-guest-button:hover {
  cursor: pointer;
}

.guest-list-items {
  display: inline-flex;
  width: 100%;
  align-items: center;
  margin-top: 6px;
}

.guests-block {
  width: 93%;
  height: 50px;
  background: #F6EFE6;
  border-radius: 6px;
  display: inline-flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 6px;
  position: relative;
  /*z-index: 0;*/
}

.email-guest--people {
  padding: 10px;
  color: #3C1F1D;
}

.bottom-invite--container {
  width: 100%;
  height: 96px;
}

.bottom-invite--text-field {
  padding: 12px 16px;
  width: 517px;
  height: 24px;
  background: #FFFFFF;
  border: 1px solid rgba(51, 51, 51, 0.16);
  border-radius: 6px;
  flex-grow: 1;
  margin-top: 23px;
}

.bottom-invite--text-field::placeholder {
  font-size: 16px;
  color: #ACAAAD;
}

.footer-invites--container {
  width: 98%;
  height: 50px;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 20px;
  color: #876A68;
  display: inline-flex;
  align-items: center;
  align-content: end;
  justify-content: flex-end;
}

.footer-invites--send-button {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 12px 24px;
  width: 160px;
  height: 48px;
  background: linear-gradient(90deg, #64362D 0%, #82544B 100%);
  border: 1px solid #3E1007;
  border-radius: 6px;
  margin-left: 25px;
  color: #fff;
  font-size: 18px;
  font-weight: 400;
}

.role-of-guest--people--container {
  /*position: relative;*/
  /*margin-top: 230px;*/
  /*margin-right: 21px;*/
  /*z-index: 1;*/
  position: absolute;
  right: 0;
}
</style>