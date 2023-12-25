<script>
//意見回饋頁面
export default {
  data() {
    return {
      name: "",
      phone: "",
      email: "",
      address: "",
      feedback: "",
    };
  },
  methods: {
    sendFeedback() {
      //電話號碼&電子郵件防呆
      const phoneRegex = /^09\d{8}$/;
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!phoneRegex.test(this.phone)) {
        alert("請輸入有效的電話號碼!");
        return;
      }
      if (!emailRegex.test(this.email)) {
        alert("請輸入有效的電子郵件!");
        return;
      }
      alert("發送成功，感謝您寶貴的意見!");
      // 暫存到localStorage
      localStorage.setItem("feedback_name", this.name);
      localStorage.setItem("feedback_phone", this.phone);
      localStorage.setItem("feedback_email", this.email);
      localStorage.setItem("feedback_address", this.address);
      localStorage.setItem("feedback_text", this.feedback);
      // 清空输入框的内容
      this.name = "";
      this.phone = "";
      this.email = "";
      this.address = "";
      this.feedback = "";
    },
  },
  computed: {
  },
};
</script>

<template>
  <div class="contactPosition">
    <div class="contact page">
      <div class="secondtitle1">
        <h2>CONTACT-聯絡我們</h2>
      </div>
      <div class="secondtitle2">
        <h3></h3>
        <!-- <h6>
          <RouterLink class="btn" to="/"> Home</RouterLink> >
          <a href="">聯絡我們</a>
        </h6> -->
      </div>
      <br />
      <div class="secondContent">
        <b>● 姓名</b>
        <br />
        <input type="text" class="textinput" v-model="name" />
        <br />
        <b>● 聯絡電話</b>
        <br />
        <input type="text" class="textinput" v-model="phone" maxlength="10" />
        <br />
        <b>● E-mail</b>
        <br />
        <input type="text" class="textinput" v-model="email" />
        <br />
        <b>● 意見與回饋</b>
        <br />
        <textarea
          cols="30"
          rows="10"
          class="textinput"
          v-model="feedback"
        ></textarea>
        <br />
        <br />
        <button class="ContactButton" @click="sendFeedback">SEND</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.contactPosition {
  .contact {
    display: flex;

    margin: 30px;
    flex-direction: column;
    border: 0px solid rgb(255, 0, 0);

    .secondtitle1 {
      justify-content: center;
      display: flex;
    }
    .secondtitle2 {
      justify-content: space-between;
      display: flex;
      a {
        border-radius: 10px;
        padding: 5px;
        transition: all 0.5s ease;
        text-decoration: none;
        color: black;
        &:hover {
          color: red;
          background-color: rgba(118, 118, 117, 0.5);
        }
      }
    }
    .secondContent {
      position: relative;
      left: 20%;
      border: 0px solid black;
      height: 100vh;
      width: 60vw;
      .textinput {
        width: 59vw;
      }
      .ContactButton {
        border: 0px solid black;
        transition: 0.5s;
        background-color: black;
        color: white;
        width: 10vw;
        height: 5vh;
        position: relative;
        left: 39%;
        &:hover {
          background-color: red;
        }
      }
    }
  }
}
</style>
