<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Momoi Lobby | Loading...</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            font-family: 'Inter', system-ui, sans-serif;
            min-height: 100vh;
            overflow: hidden;
            position: relative;
            background: #12050b; 
        }

        /* ================= LOADING SCREEN ================= */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, #2a0010, #12050b);
            z-index: 1000;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            transition: opacity 0.8s ease;
        }

        .loading-logo {
            font-size: 80px;
            margin-bottom: 30px;
            color: #ff1e78;
            animation: floatLogo 2s infinite ease-in-out;
            filter: drop-shadow(0 0 20px rgba(255, 30, 120, 0.4));
        }

        @keyframes floatLogo {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }

        .loading-text {
            color: #ff1e78;
            font-size: 24px;
            font-weight: 600;
            letter-spacing: 5px;
            margin-bottom: 30px;
            text-shadow: 0 0 20px rgba(255, 30, 120, 0.5);
        }

        .progress-container {
            width: 300px;
            height: 6px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 15px;
        }

        .progress-bar {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, #d4145a, #ff1e78);
            border-radius: 10px;
            transition: width 0.1s linear;
            box-shadow: 0 0 10px #ff1e78;
        }

        .loading-percent {
            color: #f8e1e9;
            font-size: 14px;
            font-family: monospace;
        }

        .loading-tips {
            position: absolute;
            bottom: 50px;
            color: #d4145a;
            font-size: 12px;
            text-align: center;
        }

        /* ================= MAIN LOBBY (Background pas loading) ================= */
        .lobby {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #12050b 0%, #2a0010 50%, #12050b 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        /* Efek bintang */
        .star {
            position: absolute;
            background: #ff6b9e; 
            border-radius: 50%;
            pointer-events: none;
            animation: twinkle 2s infinite alternate;
        }

        @keyframes twinkle {
            0% { opacity: 0.2; transform: scale(1); }
            100% { opacity: 1; transform: scale(1.2); }
        }

        /* Efek nebula */
        .nebula {
            position: absolute;
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(255,30,120,0.15), transparent);
            border-radius: 50%;
            pointer-events: none;
            animation: nebulaMove 20s infinite alternate;
        }

        .nebula-1 { top: -200px; right: -200px; }
        .nebula-2 { bottom: -200px; left: -200px; animation-delay: -5s; }

        @keyframes nebulaMove {
            0% { transform: translate(0, 0) scale(1); opacity: 0.3; }
            100% { transform: translate(50px, 50px) scale(1.2); opacity: 0.6; }
        }

        /* Particle canvas */
        #particleCanvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 5;
        }
    </style>
</head>
<body>

<!-- BACKGROUND LOBBY (Bintang & Partikel) -->
<div class="lobby" id="lobby">
    <canvas id="particleCanvas"></canvas>
    <div class="nebula nebula-1"></div>
    <div class="nebula nebula-2"></div>
</div>

<!-- LOADING SCREEN -->
<div class="loading-screen" id="loadingScreen">
    <div class="loading-logo">
        <i class="fas fa-moon-stars"></i>
    </div>
    <div class="loading-text">LOADING</div>
    <div class="progress-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>
    <div class="loading-percent" id="loadingPercent">0%</div>
    <div class="loading-tips">
        <i class="fas fa-sparkles"></i> Mempersiapkan Lobby Untuk Ke playwithmomoi.html... <i class="fas fa-sparkles"></i>
    </div>
</div>

<script>
    // ============ LOADING 3 DETIK ============
    let progress = 0;
    const progressBar = document.getElementById('progressBar');
    const loadingPercent = document.getElementById('loadingPercent');
    const loadingScreen = document.getElementById('loadingScreen');
    
    // Mulai animasi partikel & bintang di background dari awal
    startParticles();
    createStars();

    // 3000ms / 100% = 30ms per 1%
    const loadingInterval = setInterval(() => {
        progress += 1;
        progressBar.style.width = progress + '%';
        loadingPercent.innerText = progress + '%';
        
        if (progress >= 100) {
            clearInterval(loadingInterval);
            // Selesai loading, layar menghitam (fade out)
            loadingScreen.style.opacity = '0';
            
            // Tunggu 0.8 detik sampai fade out selesai, lalu pindah halaman
            setTimeout(() => {
                window.location.href = 'playwithmomoi.html';
            }, 800);
        }
    }, 30); // 100 * 30ms = 3000ms (3 detik)
    
    // ============ EFEK BINTANG STATIS ============
    function createStars() {
        const starCount = 150;
        for (let i = 0; i < starCount; i++) {
            const star = document.createElement('div');
            star.classList.add('star');
            const size = Math.random() * 3 + 1;
            star.style.width = size + 'px';
            star.style.height = size + 'px';
            star.style.left = Math.random() * 100 + '%';
            star.style.top = Math.random() * 100 + '%';
            star.style.animationDelay = Math.random() * 2 + 's';
            star.style.animationDuration = Math.random() * 3 + 1 + 's';
            document.body.appendChild(star);
        }
    }
    
    // ============ PARTICLE ANIMATION ============
    function startParticles() {
        const canvas = document.getElementById('particleCanvas');
        const ctx = canvas.getContext('2d');
        
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        let particles = [];
        const particleCount = 80;
        
        for (let i = 0; i < particleCount; i++) {
            particles.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                radius: Math.random() * 3 + 1,
                alpha: Math.random() * 0.5 + 0.2,
                speedX: (Math.random() - 0.5) * 0.5,
                speedY: (Math.random() - 0.5) * 0.5
            });
        }
        
        function drawParticles() {
            if (!ctx) return;
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            for (let p of particles) {
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                ctx.fillStyle = `rgba(255, 30, 120, ${p.alpha})`;
                ctx.fill();
                
                p.x += p.speedX;
                p.y += p.speedY;
                
                if (p.x < 0) p.x = canvas.width;
                if (p.x > canvas.width) p.x = 0;
                if (p.y < 0) p.y = canvas.height;
                if (p.y > canvas.height) p.y = 0;
            }
            
            requestAnimationFrame(drawParticles);
        }
        
        drawParticles();
    }
</script>
</body>
</html>
