<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Realtime Chat Firebase</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    #messages { border: 1px solid #ccc; padding: 10px; height: 300px; overflow-y: auto; margin-bottom: 10px; }
    .msg { margin: 5px 0; padding: 5px; border-radius: 4px; background: #f1f1f1; }
  </style>
  <!-- Firebase Compat SDK -->
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database-compat.js"></script>
</head>
<body>
  <h2>Realtime Chat</h2>
  <div id="messages"></div>
  <input type="text" id="msgInput" placeholder="Tulis pesan..." />
  <button onclick="sendMessage()">Kirim</button>

  <script>
    // Konfigurasi Firebase kamu
    const firebaseConfig = {
      apiKey:"AIzaSyDKjZuHMc7OFWxJNI3ghSK0hupD2bXtYDg",
      authDomain:"pantek-fdfda.firebaseapp.com",
      databaseURL:"https://pantek-fdfda-default-rtdb.asia-southeast1.firebasedatabase.app",
      projectId:"pantek-fdfda",
      storageBucket:"pantek-fdfda.appspot.com",
      messagingSenderId:"250749381924",
      appId: "1:250749381924:web:ad5e5210626d1c271fd7b1",
      measurementId:"G-5VBKNGTDX6"
    };

    // Inisialisasi Firebase
    firebase.initializeApp(firebaseConfig);
    const db = firebase.database();

    // Referensi ke "messages"
    const messagesRef = db.ref("messages");

    // Kirim pesan
    function sendMessage() {
      const msg = document.getElementById("msgInput").value;
      if (msg.trim() !== "") {
        messagesRef.push({ text: msg });
        document.getElementById("msgInput").value = "";
      }
    }

    // Tampilkan pesan realtime
    messagesRef.on("child_added", (snapshot) => {
      const msg = snapshot.val().text;
      const msgEl = document.createElement("div");
      msgEl.className ="msg";
      msgEl.innerText =msg;
      document.getElementById("messages").appendChild(msgEl);
      document.getElementById("messages").scrollTop = document.getElementById("messages").scrollHeight;
    });
  </script>
</body>
</html>
