<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PoseAlert AI - Premium Dashboard</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@teachablemachine/pose@0.8/dist/teachablemachine-pose.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #6366f1;
            --danger: #ff4757;
            --success: #2ed573;
            --dark: #2f3542;
            --glass: rgba(255, 255, 255, 0.95);
        }

        body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: var(--dark);
        }

        .main-container {
            width: 95%;
            max-width: 1100px;
            background: var(--glass);
            backdrop-filter: blur(10px);
            border-radius: 24px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            display: grid;
            grid-template-columns: 1.2fr 0.8fr;
            gap: 30px;
        }

        @media (max-width: 850px) { .main-container { grid-template-columns: 1fr; } }

        .header { grid-column: 1 / -1; text-align: center; margin-bottom: 10px; }
        .header h1 { margin: 0; color: var(--primary); letter-spacing: -1px; }

        .video-box {
            position: relative;
            background: #000;
            border-radius: 18px;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            line-height: 0;
        }

        canvas { width: 100% !important; height: auto !important; transform: scaleX(-1); }

        .status-card {
            padding: 20px;
            border-radius: 18px;
            background: #f1f2f6;
            text-align: center;
            transition: all 0.3s ease;
        }

        .alert-active {
            background: #ffeaa7;
            border: 2px solid var(--danger);
            animation: shake 0.5s infinite;
        }

        @keyframes shake {
            0% { transform: translate(1px, 1px); }
            20% { transform: translate(-1px, -2px); }
            100% { transform: translate(1px, -1px); }
        }

        .timer-badge {
            font-size: 3rem;
            font-weight: 800;
            color: var(--primary);
            margin: 10px 0;
        }

        .btn-start {
            background: var(--primary);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s;
            width: 100%;
        }

        .btn-start:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(99, 102, 241, 0.4); }

        #label-container { font-weight: 600; font-size: 1.2rem; color: var(--danger); }
    </style>
</head>
<body>

<div class="main-container">
    <div class="header">
        <h1>POSE ALERT AI 🧘‍♂️</h1>
        <p>Hệ thống giám sát tư thế học tập thông minh</p>
    </div>

    <div class="left-col">
        <div class="video-box">
            <canvas id="canvas"></canvas>
        </div>
        <div style="margin-top: 15px;">
            <button class="btn-start" onclick="init()">⚡ BẮT ĐẦU GIÁM SÁT</button>
        </div>
    </div>

    <div class="right-col">
        <div class="status-card" id="main-status">
            <div id="status-text" style="font-size: 1.1rem; font-weight: 600;">Sẵn sàng khởi động</div>
            <div class="timer-badge" id="timer">00s</div>
            <div id="label-container">Đang chờ camera...</div>
        </div>

        <div class="status-card" style="margin-top: 20px;">
            <canvas id="myChart"></canvas>
            <p style="font-size: 0.9rem; margin-top: 15px; color: #57606f;">
                💡 <b>Ghi chú:</b> Hệ thống sẽ nhắc bằng giọng nói sau 30s ngồi sai liên tục.
            </p>
        </div>
    </div>
</div>

<script>
    // LINK MÔ HÌNH CỦA BẠN
    const URL = "https://teachablemachine.withgoogle.com/models/a8QICad-j/";

    let model, webcam, ctx, labelContainer, maxPredictions;
    let startTime = null;
    let stats = { good: 1, bad: 0 }; // Khởi tạo 1 để biểu đồ không lỗi
    let chart;

    const synth = window.speechSynthesis;

    async function init() {
        document.getElementById("status-text").innerText = "Đang tải mô hình AI...";
        
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        try {
            model = await tmPose.load(modelURL, metadataURL);
            maxPredictions = model.getTotalClasses();

            const size = 400;
            const flip = true;
            webcam = new tmPose.Webcam(size, size, flip);
            await webcam.setup();
            await webcam.play();
            window.requestAnimationFrame(loop);

            const canvas = document.getElementById("canvas");
            canvas.width = size; canvas.height = size;
            ctx = canvas.getContext("2d");
            
            initChart();
            document.getElementById("status-text").innerText = "Hệ thống đang chạy";
        } catch (e) {
            alert("Không thể mở camera. Vui lòng kiểm tra quyền truy cập!");
        }
    }

    async function loop() {
        webcam.update();
        await predict();
        window.requestAnimationFrame(loop);
    }

    async function predict() {
        const { pose, posenetOutput } = await model.estimatePose(webcam.canvas);
        const prediction = await model.predict(posenetOutput);

        let bestScene = "";
        let bestProb = 0;

        for (let i = 0; i < maxPredictions; i++) {
            if (prediction[i].probability > bestProb) {
                bestProb = prediction[i].probability;
                bestScene = prediction[i].className;
            }
        }

        updateUI(bestScene, bestProb);
        drawPose(pose);
    }

    function updateUI(poseName, prob) {
        const statusBox = document.getElementById("main-status");
        const timerText = document.getElementById("timer");
        const labelBox = document.getElementById("label-container");

        // Logic phân loại: Nếu không phải "ngồi đúng" (hoặc nếu độ tin cậy thấp)
        // Lưu ý: Sửa tên class "ngồi đúng" nếu bạn đặt tên khác trong TM
        const isBad = (poseName === "cúi đầu" || poseName === "vẹo lưng" || poseName === "mắt gần");

        if (!isBad) {
            statusBox.classList.remove("alert-active");
            document.getElementById("status-text").innerText = "Tư thế: TỐT ✅";
            document.getElementById("status-text").style.color = "var(--success)";
            labelBox.innerText = "Giữ vững phong độ!";
            startTime = null;
            timerText.innerText = "00s";
            stats.good++;
        } else {
            statusBox.classList.add("alert-active");
            document.getElementById("status-text").innerText = "Tư thế: XẤU ⚠️";
            document.getElementById("status-text").style.color = "var(--danger)";
            labelBox.innerText = "Bạn đang: " + poseName;
            
            if (!startTime) startTime = Date.now();
            let seconds = Math.floor((Date.now() - startTime) / 1000);
            timerText.innerText = (seconds < 10 ? "0" : "") + seconds + "s";

            if (seconds >= 30) {
                speakNotification(poseName);
                startTime = Date.now(); // Reset để nhắc lại sau 30s nữa
            }
            stats.bad++;
        }
        updateChart();
    }

    function speakNotification(pose) {
        const text = `Bạn ơi, bạn đang ${pose}. Hãy ngồi thẳng lưng lên để bảo vệ cột sống nhé!`;
        const utter = new SpeechSynthesisUtterance(text);
        utter.lang = 'vi-VN';
        utter.rate = 0.9;
        synth.speak(utter);
    }

    function initChart() {
        const ctxChart = document.getElementById('myChart').getContext('2d');
        chart = new Chart(ctxChart, {
            type: 'doughnut',
            data: {
                labels: ['Đúng', 'Sai'],
                datasets: [{
                    data: [1, 0],
                    backgroundColor: ['#2ed573', '#ff4757'],
                    borderWidth: 0
                }]
            },
            options: { cutout: '70%', plugins: { legend: { position: 'bottom' } } }
        });
    }

    function updateChart() {
        if (chart) {
            chart.data.datasets[0].data = [stats.good, stats.bad];
            chart.update('none');
        }
    }

    function drawPose(pose) {
        if (webcam.canvas) {
            ctx.drawImage(webcam.canvas, 0, 0);
            if (pose) {
                tmPose.drawKeypoints(pose.keypoints, 0.6, ctx);
                tmPose.drawSkeleton(pose.keypoints, 0.6, ctx);
            }
        }
    }
</script>

</body>
</html>