<template>
  <div class="home">
      <p class="number">{{counter}}秒 / 94608000秒</p>
  </div>
</template>

<script>
// @ is an alias to /src
import firebase from "firebase";
const config = {
  apiKey: "AIzaSyBZqj5mk6EZDtOQHClJGBb3l9Nw0FAqdpA",
  authDomain: "firabasefire.firebaseapp.com",
  databaseURL: "https://firabasefire.firebaseio.com",
  projectId: "firabasefire",
  storageBucket: "firabasefire.appspot.com",
  messagingSenderId: "616673046185"
};
firebase.initializeApp(config);
const database = firebase.database();

export default {
  name: "home",
  data() {
    return {
      counter: 0
    };
  },
  methods: {
    getCounter(val) {
      this.counter = val;
    }
  },
  mounted() {
    const starCountRef = firebase.database().ref("stone");
    starCountRef.on("value", snapshot => {
      // console.log(snapshot.val());
      this.getCounter(snapshot.val());
    });
  }
};
</script>

<style lang="scss">
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
}

.number {
    font-size: 64px;
}
</style>
