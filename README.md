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
            /* Warna gelap transisi ke pink gelap */
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

        /* ================= MAIN LOBBY ================= */
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
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.8s ease;
            overflow: hidden;
        }

        .lobby.active {
            opacity: 1;
            visibility: visible;
        }

        /* Efek bintang */
        .star {
            position: absolute;
            background: #ff6b9e; /* Bintang warna pink */
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

        /* Konten Lobby */
        .content {
            text-align: center;
            z-index: 10;
            animation: fadeInUp 0.8s ease;
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .logo-icon {
            font-size: 100px;
            margin-bottom: 20px;
            color: #ff1e78;
            filter: drop-shadow(0 0 30px rgba(255,30,120,0.5));
            animation: logoGlow 3s infinite alternate;
        }

        @keyframes logoGlow {
            0% { filter: drop-shadow(0 0 20px rgba(255,30,120,0.3)); }
            100% { filter: drop-shadow(0 0 50px rgba(255,30,120,0.8)); }
        }

        h1 {
            font-size: 3.5rem;
            background: linear-gradient(135deg, #fff, #ffb3d1, #ff1e78);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 10px;
            letter-spacing: 2px;
        }

        .subtitle {
            color: #f8e1e9;
            font-size: 1rem;
            margin-bottom: 50px;
            letter-spacing: 3px;
        }

        /* Tombol ENJOY */
        .enjoy-btn {
            background: linear-gradient(135deg, #ff1e78, #d4145a);
            border: none;
            padding: 18px 50px;
            font-size: 1.5rem;
            font-weight: 700;
            color: white;
            border-radius: 60px;
            cursor: pointer;
            font-family: 'Inter', sans-serif;
            letter-spacing: 2px;
            box-shadow: 0 0 20px rgba(255,30,120,0.5);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            gap: 15px;
            margin: 0 auto;
        }

        .enjoy-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.5s ease;
        }

        .enjoy-btn:hover::before { left: 100%; }

        .enjoy-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 40px rgba(255,30,120,0.8);
        }

        .enjoy-btn i {
            font-size: 1.5rem;
            transition: transform 0.3s ease;
        }

        .enjoy-btn:hover i {
            transform: translateX(8px);
        }

        /* Footer */
        .footer {
            position: absolute;
            bottom: 30px;
            color: #d4145a;
            font-size: 12px;
            z-index: 10;
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

        @media (max-width: 600px) {
            h1 { font-size: 2.2rem; }
            .logo-icon { font-size: 70px; }
            .enjoy-btn { padding: 15px 35px; font-size: 1.2rem; }
            .subtitle { font-size: 0.8rem; margin-bottom: 30px; }
            .progress-container { width: 250px; }
        }
    </style>
</head>
<body>

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

<!-- MAIN LOBBY -->
<div class="lobby" id="lobby">
    <canvas id="particleCanvas"></canvas>
    <div class="nebula nebula-1"></div>
    <div class="nebula nebula-2"></div>
    
    <div class="content">
        <div class="logo-icon">
            <i class="fas fa-moon"></i>
        </div>
        <h1>MOMOI HUB</h1>
        <div class="subtitle">✦ SAIBA MOMOI'S CLOUD ✦</div>
        <button class="enjoy-btn" id="enjoyBtn">
            AYO MASUK! <i class="fas fa-arrow-right"></i>
        </button>
    </div>
    
    <div class="footer">
        <i class="fas fa-star"></i> Selamat Datang Di Momoi Cloud <i class="fas fa-star"></i>
    </div>
</div>

<script>
    // ============ LOADING 7 DETIK ============
    let progress = 0;
    const progressBar = document.getElementById('progressBar');
    const loadingPercent = document.getElementById('loadingPercent');
    const loadingScreen = document.getElementById('loadingScreen');
    const lobby = document.getElementById('lobby');
    
    const loadingInterval = setInterval(() => {
        progress += 1;
        progressBar.style.width = progress + '%';
        loadingPercent.innerText = progress + '%';
        
        if (progress >= 100) {
            clearInterval(loadingInterval);
            // Selesai loading, tampilkan lobby
            loadingScreen.style.opacity = '0';
            setTimeout(() => {
                loadingScreen.style.display = 'none';
                lobby.classList.add('active');
                startParticles();
                createStars();
            }, 800);
        }
    }, 70); // 100% dalam 7 detik
    
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
    let particleAnimation = null;
    
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
                // Partikel warna pink
                ctx.fillStyle = `rgba(255, 30, 120, ${p.alpha})`;
                ctx.fill();
                
                p.x += p.speedX;
                p.y += p.speedY;
                
                if (p.x < 0) p.x = canvas.width;
                if (p.x > canvas.width) p.x = 0;
                if (p.y < 0) p.y = canvas.height;
                if (p.y > canvas.height) p.y = 0;
            }
            
            particleAnimation = requestAnimationFrame(drawParticles);
        }
        
        drawParticles();
    }
    
    // ============ TOMBOL ENJOY - REDIRECT KE playwithmomoi.html ============
    const enjoyBtn = document.getElementById('enjoyBtn');
    
    const newBtn = enjoyBtn.cloneNode(true);
    enjoyBtn.parentNode.replaceChild(newBtn, enjoyBtn);
    
    newBtn.addEventListener('click', function(e) {
        e.preventDefault();
        e.stopPropagation();
        
        this.style.transform = 'scale(0.95)';
        setTimeout(() => {
            this.style.transform = 'scale(1)';
        }, 150);
        
        // Redirect ke playwithmomoi.html
        console.log('Redirecting to playwithmomoi.html...');
        window.location.href = 'playwithmomoi.html';
    });
    
    document.addEventListener('keydown', function(e) {
        if (e.key === 'Enter' && lobby.classList.contains('active')) {
            window.location.href = 'playwithmomoi.html';
        }
    });
    
    newBtn.addEventListener('mouseenter', () => { newBtn.style.transform = 'scale(1.05)'; });
    newBtn.addEventListener('mouseleave', () => { newBtn.style.transform = 'scale(1)'; });
</script>
</body>
</html>
