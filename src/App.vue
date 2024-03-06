<script setup>


// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// import { getAnalytics } from "firebase/analytics";
import { getMessaging, getToken, onMessage} from 'firebase/messaging';
import { ref } from 'vue';
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyDHUQjhL3ZTGRABKBg2O4saS1Ve4StvY_g",
  authDomain: "fyppush-f9a64.firebaseapp.com",
  projectId: "fyppush-f9a64",
  storageBucket: "fyppush-f9a64.appspot.com",
  messagingSenderId: "647988498605",
  appId: "1:647988498605:web:78856978d24976a14b3624",
  measurementId: "G-ZTF7LZETFH"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
// const analytics = getAnalytics(app);
const messaging = getMessaging(app);
const token = ref(null)
onMessage(messaging, (payload) => {
    console.log('Message received. ', payload);
    // ...
  });

// Get registration token. Initially this makes a network call, once retrieved
// subsequent calls to getToken will return from cache.
// const messaging = getMessaging();
getToken(messaging, { vapidKey: 'BIB3GyustUsKi1cb9qe_MV-n5a1zFezDpuHMLHnJfYnO5Ki2AHXcJItLA82lQSQCatD6Bko8IGzfKsUNN3qp5tk' }).then((currentToken) => {
  if (currentToken) {
    // Send the token to your server and update the UI if necessary
    // ...
    console.log(currentToken)
    // getMessaging().subscribeToTopic(currentToken, 'notifications').then((reponse) => {
    //   console.log("successfully subscribed")
    // })
    // fetch(`http://127.0.0.1:8000/dashboard/subscribe/${currentToken}`).then((response) => {
    //   console.log(response.json())
    // })
    token.value = currentToken
  } else {
    // Show permission request UI
    console.log('No registration token available. Request permission to generate one.');
    // ...
  }
}).catch((err) => {
  console.log('An error occurred while retrieving token. ', err);
  // ...
});
</script>

<template>
  HELLO WORLD
  User Token: {{ token }}
</template>

<style scoped>
*{
  color: white;
}
</style>
