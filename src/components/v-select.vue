<template>
  <div class="v-select">
    <p
        class="selected-block"
        @click="areRoleAreVisible = !areRoleAreVisible"
        >
      {{selected}}</p>
    <div
        v-if="areRoleAreVisible"
        class="options">
        <p class="role-name--container"
          v-for="option in options"
          :key="option.value"
          @click="selectRole(option)"
        >
          <span class="role-name--title">{{ option.roleName }}</span><br>
          <span class="role-name--text">{{ option.roleText }}</span>
        </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-select",
  props: {
    options: {
      type: Array,
      default() {
        return []
      }
    },
    selected: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      areRoleAreVisible: false
    }
  },
  methods: {
    selectRole(option){
      this.$emit('select', option)
      this.areRoleAreVisible = false;
    },
    hideSelect(){
      this.areRoleAreVisible = false;
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelect, true)
  },
  beforeUnmount() {
    document.removeEventListener('click', this.hideSelect)
  }
}
</script>

<style>
.v-select {
  cursor: pointer;

}
.options {
  position: absolute;
  width: 318px;
  height: 188px;
  background-color: #FFF8EF;
  box-shadow: 4px 4px 24px rgb(0 0 0 / 16%);
  border-radius: 6px;
  right: 21px;
  top: 14px;
  z-index: 1;
}
.selected-block {
  position: absolute;
  right: 3px;
  top: -8px;
  color: #3C1F1D;
}
.selected-block:after {
  content: "";
  background-image: url("../assets/dropdownBtn.png");
  background-size: contain;
  width: 10px;
  height: 10px;
  padding-right: 11px;
  margin-right: 13px;
  background-repeat: no-repeat;
  background-position: center;
  margin-left: 5px;
}
.selected-block:after:active {
  transform: rotate(-90deg);
}
.role-name--title {
  color: #3C1F1D;
  font-size: 16px;
  line-height: 20px;
  font-weight: 600;
}
.role-name--text{
  font-size: 12px;
  line-height: 16px;
  color: #876A68;
  text-align: left;
}
.role-name--container {
  background: #FFF8EF;
  padding: 15px 16px 16px 40px;
  border-radius: 6px;
}
.role-name--container:hover {
  background: #F6EFE6;
}

.role-name--container:hover:before {
  content: "";
  background-image: url("../assets/acceptIconImage.png");
  background-size: contain;
  width: 13px;
  height: 13px;
  padding-right: 11px;
  margin-right: 13px;
  background-repeat: no-repeat;
  background-position: center;
  margin-left: -24px;
}
</style>