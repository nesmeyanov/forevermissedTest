<template>
  <div class="v-select">
    <p
        class="selected-block"
        @click="areRoleAreVisible = !areRoleAreVisible"
        >
      Selected role</p>
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
    }
  },
  data() {
    return {
      areRoleAreVisible: false
    }
  },
  methods: {
    selectRole(){

    }
  }
}
</script>

<style>
.v-select {
  cursor: pointer;
  position: relative;
  width: 300px;
  height: 140px;
  z-index: 999;
}
.options {
  width: 318px;
  height: 188px;
  background-color: #FFF8EF;
  box-shadow: 4px 4px 24px rgb(0 0 0 / 16%);
  border-radius: 6px;
  z-index: 111;
}
.selected-block {
  position: absolute;
  top: -53px;
  right: 3px;
  width: 108px;
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
.role-name--title {
  color: #3C1F1D;
  font-size: 16px;
  line-height: 20px;
  font-weight: 600;
  padding-bottom: 10px;
  color: #3C1F1D;
}
/*.role-name--title:after {*/
/*  content: "";*/
/*  background-image: url("../assets/dropdownBtn.png");*/
/*  background-size: contain;*/
/*  width: 10px;*/
/*  height: 10px;*/
/*  padding-right: 11px;*/
/*  margin-right: 13px;*/
/*  background-repeat: no-repeat;*/
/*  background-position: center;*/
/*  margin-left: 5px;*/
/*  text-align: left;*/
/*}*/
.role-name--text{
  font-size: 12px;
  line-height: 16px;
  color: #876A68;
  /*padding: 3px 16px 12px 48px;*/
  text-align: left;
  padding-bottom: 10px;
}
.role-name--container {
  background: #FFF8EF;
}
.role-name--container:hover {
  background: #F6EFE6;
}
.role-name--container {
    padding: 12px 16px 12px 40px;
}
</style>