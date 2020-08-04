<template>
  <div :style="backgroundStyle" class="componentWrapper">
    <h3 :style="titleStyle">{{title}}</h3>
    <input type="email" placeholder="Email" v-model="email" />
    <textarea name id rows="4" placeholder="Message" v-model="message"></textarea>
    <button :style="buttonStyle" id="sendButton" @click="post">{{buttonText}}</button>
  </div>
</template>

<script>
export default {
  name: "vubak",
  props: {
    url: {
      type: String,
      default: "",
    },
    title: { type: String, default: "Send some feedback!" },
    buttonText: { type: String, default: "Send" },
    backgroundStyle: { type: String, default: "background-color: black;" },
    buttonStyle: { type: String, default: "background-color: #25c12b;" },
    titleStyle: { type: String, default: "" },
  },
  data() {
    return {
      email: "",
      message: "",
    };
  },
  methods: {
    post() {
      //Checks if provided email is valid
      let emailCheck = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if (emailCheck.test(this.email) && this.message !== "") {
        let payload = {
          text: `User: ${this.email}\nMessage: ${this.message}`,
        };
        fetch(this.url, {
          method: "post",
          body: JSON.stringify(payload),
        }).then(() => {
          this.email = "";
          this.message = "";
        });
      }
    },
  },
};
</script>

<style scoped>
* {
  font-family: sans-serif;
}
.componentWrapper {
  padding: 16px;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 400px;
}
.componentWrapper h3 {
  color: white;
  margin-top: 0;
}
.componentWrapper span {
  color: white;
}
input {
  border-radius: 8px;
  border: none;
  margin: 4px 0 4px 0;
  padding: 4px;
}
textarea {
  resize: none;
  border: none;
  border-radius: 8px;
  margin: 4px 0 4px 0;
  padding: 4px;
}
#sendButton {
  margin: auto;
  margin-top: 4px;
  color: white;
  background-color: #25c12b;
  width: fit-content;
  padding: 12px 32px 12px 32px;
  border: none;
  border-radius: 10em;
  font-weight: bold;
  cursor: pointer;
}
</style>