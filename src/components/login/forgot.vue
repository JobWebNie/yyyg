<template>
  <div class="exportforgot" id="exportforgot">
    <!-- 顶部标题 -->
    <div class="tc box rel flex js_between al_center top_title">
        <span class="back"  v-on:click="back()">
           <img :src="baseImgUrl+'left_21_37.png'" style="width:.42rem;height:.74rem;" alt="">
        </span>
       <span>找回密码</span>
      <span class="exit"></span>
    </div>
    <div class="userins">
        <div class="pass_inner">
            <span class="pass_label">手机号：</span>
            <p class="user_tel">
                <img :src="baseImgUrl+'login_tel_80_80.png'" style="width:1.6rem;height:1.6rem;" alt="phone-icon">
                <input type="number" value="" placeholder="请输入手机号" maxlength="11">
            </p>
        </div>
        <div class="pass_inner">
            <span class="pass_label">验证码：</span>
            <p class="user_tel">
                <img :src="baseImgUrl+'login_pass_80_80.png'" style="width:1.6rem;height:1.6rem;" alt="valid-icon">
                <input type="number" value=""  maxlength="11">
            </p>
            <span class="btn_validefy" v-if="notvalided" @click="createdCode()">获取验证码</span>
            <span class="btn_validefy" v-else> {{timercount}}s</span>
        </div>
        <div class="pass_inner">
            <span class="pass_label">新密码：</span>
            <p class="user_tel">
                <img :src="baseImgUrl+'login_pass_80_80.png'" style="width:1.6rem;height:1.6rem;" alt="valid-icon">
                <input type="number" value=""  maxlength="11">
            </p>
        </div>
    </div>
    <p class="login_button" >下一步</p>
  </div>
</template>
<script>
export default {
  name: "exportforgot",
  data() {
    return {
      baseImgUrl: this.$store.state.baseImgUrl,
      notvalided:true,
      timercount:'',
      timer:null,
      code:''
    };
  },
  created: function() {},
  computed: {},
  methods: {
    back: function() {
      this.$router.back()
    },
    // 生成随机码
    createdCode(){
    const TIME_COUNT = 60
    if(!this.timer){
      this.timercount = TIME_COUNT;
      this.timer = setInterval(()=>{
         if (this.timercount > 0 && this.timercount <= TIME_COUNT) {
         this.timercount--;
        } else {
         this.notvalided = true;
         clearInterval(this.timer);
         this.timer = null;
        }
       }, 1000)
    }
    this.notvalided = false;
    const parten = ['0','1','2','3','4','5','6','7','8','9'];
    const code='';
    this.code = code;
    for(let i = 0;i<4;i++){
      let ran = parseInt(Math.random()*parten.length);
      this.code += parten[ran];
    }
  }
  }

};
</script>

 

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "forgot.css";
</style>
