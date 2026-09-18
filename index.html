<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    body { font-family:'Kanit',sans-serif; background:#f4f4f9; display:flex; flex-direction:column;
           align-items:center; min-height:100vh; margin:0; padding:20px; text-align:center; box-sizing:border-box; }
    h1 { color:#333; margin-bottom:20px; font-size:20px; }
    #reader { width:100%; max-width:400px; border-radius:10px; overflow:hidden;
              box-shadow:0 4px 8px rgba(0,0,0,0.1); background:#000; min-height:200px; }
    video { width:100%; display:block; }
    .btn { padding:12px 24px; font-size:16px; border:none; border-radius:50px; color:#fff;
           margin:10px 6px; cursor:pointer; }
    .btn-start { background-color:#007bff; }
    .btn-stop { background-color:#dc3545; }
    #outputMessage { margin-top:20px; padding:15px; border-radius:10px; font-weight:bold;
                      width:100%; max-width:400px; min-height:24px; box-sizing:border-box; }
    .success { background-color:#d4edda; color:#155724; border:1px solid #c3e6cb; }
    .error   { background-color:#f8d7da; color:#721c24; border:1px solid #f5c6cb; }
    .warning { background-color:#fff3cd; color:#856404; border:1px solid #ffeeba; }
    .loading { color:#666; font-size:14px; }
  </style>
  <script src="https://cdn.jsdelivr.net/npm/jsqr@1.4.0/dist/jsQR.js"></script>
</head>
<body>
  <h1>ระบบเช็คอิน (Event Check-In)</h1>

  <!-- EDIT THIS -->
  <script>
    const WEB_APP_URL = "https://script.google.com/macros/s/AKfycby8NWodaoO76eNTVIQThfp21tV5jq1QfgznNqh4TUH-aX2C1jmpbwp5WEMnXSw8JwAv4g/exec"; // your Apps Script /exec URL
  </script>

  <div>
    <button id="startBtn" class="btn btn-start" onclick="startScan()">เปิดกล้อง / Start</button>
    <button id="stopBtn" class="btn btn-stop" onclick="stopScan()" style="display:none;">ปิดกล้อง / Stop</button>
  </div>

  <div id="reader">
    <video id="video" playsinline></video>
    <canvas id="canvas" style="display:none;"></canvas>
  </div>

  <div id="outputMessage"></div>

  <script>
    const video = document.getElementById('video');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    let stream = null;
    let scanning = false;
    let lastScannedId = null;
    let lastScanTime = 0;
    const COOLDOWN_MS = 4000;

    function setMessage(text, cls) {
      const el = document.getElementById('outputMessage');
      el.textContent = text;
      el.className = cls || '';
    }

    async function startScan() {
      setMessage('กำลังขอสิทธิ์เข้าถึงกล้อง...', 'loading');
      try {
        stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "environment" } });
        video.srcObject = stream;
        video.setAttribute('playsinline', true);
        await video.play();
        document.getElementById('startBtn').style.display = 'none';
        document.getElementById('stopBtn').style.display = 'inline-block';
        scanning = true;
        setMessage('กำลังสแกน... ถือ QR Code ให้อยู่ในกรอบ', 'loading');
        requestAnimationFrame(tick);
      } catch (err) {
        setMessage('ไม่สามารถเปิดกล้องได้: ' + err.name, 'error');
      }
    }

    function stopScan() {
      scanning = false;
      if (stream) stream.getTracks().forEach(t => t.stop());
      document.getElementById('startBtn').style.display = 'inline-block';
      document.getElementById('stopBtn').style.display = 'none';
      setMessage('', '');
    }

    function tick() {
      if (!scanning) return;
      if (video.readyState === video.HAVE_ENOUGH_DATA) {
        canvas.height = video.videoHeight;
        canvas.width = video.videoWidth;
        ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
        const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
        const code = jsQR(imageData.data, imageData.width, imageData.height);

        if (code && code.data) {
          const now = Date.now();
          if (code.data !== lastScannedId || now - lastScanTime > COOLDOWN_MS) {
            lastScannedId = code.data;
            lastScanTime = now;
            handleScan(code.data);
          }
        }
      }
      requestAnimationFrame(tick);
    }

    async function handleScan(regId) {
      setMessage('กำลังตรวจสอบ...', 'loading');
      try {
        const url = `${WEB_APP_URL}?action=checkin&regId=${encodeURIComponent(regId)}`;
        const response = await fetch(url);
        const result = await response.json();
        setMessage(result.message, result.status);
      } catch (err) {
        setMessage('เกิดข้อผิดพลาด: ' + err.message, 'error');
      }
    }
  </script>
</body>
</html>
