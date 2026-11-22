<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Loading... - Momoi Cloud Hub</title>
<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  body {
    background-color: #12050b; /* Hitam kemerahan */
    color: #fff;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    background-image: radial-gradient(circle at center, #2a0010 0%, #12050b 100%);
  }

  /* Animasi Spinner ala Blue Archive / Anime */
  .loader-container {
    position: relative;
    width: 100px;
    height: 100px;
    margin-bottom: 30px;
  }

  .spinner {
    position: absolute;
    width: 100%;
    height: 100%;
    border: 4px solid rgba(255, 30, 120, 0.2);
    border-top: 4px solid #ff1e78;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    box-shadow: 0 0 20px rgba(255, 30, 120, 0.4);
  }

  /* Ikon Halo di tengah */
  .loader-icon {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 2.5rem;
    animation: pulse 1.5s ease-in-out infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  @keyframes pulse {
    0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 1; }
    50% { transform: translate(-50%, -50%) scale(1.1); opacity: 0.8; }
  }

  /* Teks Loading */
  .loading-text {
    font-size: 1.2rem;
    font-weight: bold;
    color: #ff1e78;
    letter-spacing: 2px;
    text-shadow: 0 0 10px rgba(255, 30, 120, 0.5);
    margin-bottom: 10px;
    text-align: center;
  }

  .loading-subtext {
    font-size: 0.9rem;
    color: #aaa;
    text-align: center;
    animation: blink 1.5s infinite;
  }

  @keyframes blink {
    0%, 100% { opacity: 0.5; }
    50% { opacity: 1; }
  }

  /* Progress Bar */
  .progress-bar-container {
    width: 80%;
    max-width: 300px;
    height: 6px;
    background: #333;
    border-radius: 10px;
    margin-top: 20px;
    overflow: hidden;
  }

  .progress-bar {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, #ff1e78, #ff6b9e);
    border-radius: 10px;
    animation: loadProgress 2.5s ease-in-out forwards;
    box-shadow: 0 0 10px #ff1e78;
  }

  @keyframes loadProgress {
    0% { width: 0%; }
    50% { width: 60%; }
    100% { width: 100%; }
  }

  .momoi-gif {
    width: 150px;
    margin-bottom: 20px;
    filter: drop-shadow(0 0 10px #ff1e78);
    animation: float 3s ease-in-out infinite;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
  }

</style>
</head>
<body>

  <!-- Ganti src dengan gambar Momoi kalau ada, atau biarin emoji -->
  <div class="momoi-gif">📱</div>

  <div class="loader-container">
    <div class="spinner"></div>
    <div class="loader-icon">🎀</div>
  </div>

  <div class="loading-text">LOADING MOMOI CLOUD...</div>
  <div class="loading-subtext">Menyiapkan server cloud dan playlist musik...</div>

  <div class="progress-bar-container">
    <div class="progress-bar"></div>
  </div>

<script>
  // GANTI "index.html" DENGAN NAMA FILE WEB UTAMA KAMU
  const targetUrl = "index.html"; 

  // Waktu loading (dalam milidetik). 2500 = 2.5 detik
  const loadingTime = 2500; 

  setTimeout(() => {
    // Efek fade out sebelum pindah
    document.body.style.transition = "opacity 0.5s ease";
    document.body.style.opacity = "0";
    
    setTimeout(() => {
      window.location.href = targetUrl;
    }, 500); // Tunggu 0.5 detik sampai layar gelap, baru pindah
  }, loadingTime);
</script>
</body>
</html>
