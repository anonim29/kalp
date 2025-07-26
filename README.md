# kalp
6.py
import webbrowser
import os
from pathlib import Path


def create_matrix_html():
    """Matrix efektli Sisi animasyonu HTML dosyasını oluşturur"""

    html_content = """<!DOCTYPE html> 
<html lang="tr"> 
<head> 
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    <title>Matrix Sisi - Enhanced</title> 
    <style> 
        * { 
            margin: 0; 
            padding: 0; 
            box-sizing: border-box; 
        } 
 
        html, body { 
            background: black; 
            overflow: hidden; 
            height: 100vh; 
            font-family: 'Courier New', monospace; 
        } 
 
        #matrix { 
            position: fixed; 
            top: 0; 
            left: 0; 
            z-index: 0; 
        } 
 
        .welcome-btn { 
            position: fixed; 
            top: 50%; 
            left: 50%; 
            transform: translate(-50%, -50%); 
            background: #00ff00; 
            color: black; 
            border: none; 
            padding: 15px 25px; 
            font-size: 20px; 
            font-family: 'Courier New', monospace; 
            cursor: pointer; 
            z-index: 100; 
            border-radius: 5px; 
            transition: background-color 0.3s ease; 
        } 
 
        .welcome-btn:hover { 
            background: #00cc00; 
        } 
 
        .sisi-text { 
            position: absolute; 
            color: white; 
            font-size: 16px; 
            font-family: 'Courier New', monospace; 
            white-space: pre-line; 
            z-index: 10; 
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.9); 
            animation: sisiMove 5s linear forwards; 
            font-weight: bold; 
            opacity: 1; 
            display: inline-block; 
            text-align: center; 
        } 
 
        .heart { 
            position: absolute; 
            font-size: 30px; 
            z-index: 10; 
            animation: heartMove 2.5s linear forwards; 
            text-shadow: 0 0 10px rgba(255, 0, 0, 0.8); 
        } 
 
        @keyframes sisiMove { 
            0% { 
                transform: translateY(100vh) scale(0.8); 
                opacity: 1; 
            } 
            100% { 
                transform: translateY(-100vh) scale(1.5); 
                opacity: 0; 
            } 
        } 
 
        @keyframes heartMove { 
            0% { 
                transform: translateY(100vh) scale(1) rotate(0deg); 
                opacity: 0; 
            } 
            20% { 
                opacity: 1; 
            } 
            50% { 
                transform: translateY(50vh) scale(1.3) rotate(180deg); 
            } 
            80% { 
                opacity: 1; 
            } 
            100% { 
                transform: translateY(-50px) scale(0.8) rotate(360deg); 
                opacity: 0; 
            } 
        } 
    </style> 
</head> 
<body> 
    <canvas id="matrix"></canvas> 
    <button class="welcome-btn" onclick="startAnimation()">Hoşgeldin Sisi ❤️</button> 
 
    <script> 
        class MatrixAnimation { 
            constructor() { 
                this.animationStarted = false; 
                this.matrixInterval = null; 
                this.heartInterval = null; 
                this.sisiInterval = null; 
 
                this.canvas = document.getElementById('matrix'); 
                this.ctx = this.canvas.getContext('2d'); 
 
                this.characters = "アァイィウヴエェオカガキギクグケゲコゴサザシジスズセゼソゾタチッツヅテデトドナニヌネノハバパヒビピフブプヘベペホボポマミムメモヤユヨラリルレロワヲンABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@#$%^&*()"; 
                this.matrix = this.characters.split(""); 
 
                this.fontSize = 14; 
                this.drops = []; 
 
                this.initCanvas(); 
                this.setupEventListeners(); 
            } 
 
            initCanvas() { 
                this.canvas.width = window.innerWidth; 
                this.canvas.height = window.innerHeight; 
                this.columns = Math.floor(this.canvas.width / this.fontSize); 
 
                // Initialize drops 
                for (let x = 0; x < this.columns; x++) { 
                    this.drops[x] = Math.floor(Math.random() * 100); 
                } 
            } 
 
            setupEventListeners() { 
                window.addEventListener('resize', () => { 
                    this.initCanvas(); 
                }); 
            } 
 
            drawMatrix() { 
                this.ctx.fillStyle = "rgba(0, 0, 0, 0.04)"; 
                this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height); 
 
                this.ctx.fillStyle = "#0F0";  // Matrix yazıları yeşil renk olacak 
                this.ctx.font = this.fontSize + "px monospace"; 
 
                for (let i = 0; i < this.drops.length; i++) { 
                    const text = this.matrix[Math.floor(Math.random() * this.matrix.length)]; 
                    const x = i * this.fontSize; 
                    const y = this.drops[i] * this.fontSize; 
 
                    this.ctx.fillText(text, x, y); 
 
                    if (y > this.canvas.height && Math.random() > 0.975) { 
                        this.drops[i] = 0; 
                    } 
                    this.drops[i]++; 
                } 
            } 
 
            createSisi() { 
                const sisi = document.createElement('div'); 
                sisi.className = 'sisi-text'; 
 
                // Kalp şeklinde bir yazı düzeni oluşturuldu 
                const sisiText = ` 
                  SİSİSİ SİSİSİ 
                SİSİSİSİ SİSİSİSİ   
               SİSİSİSİSİSİSİSİSİS 
              SİSİSİSİSİSİSİSİSİSİS 
             SİSİSİSİSİSİSİSİSİSİSİ 
              SİSİSİSİSİSİSİSİSİSİS 
               SİSİSİSİSİSİSİSİSİS 
                SİSİSİSİSİSİSİSİS 
                 SİSİSİSİSİSİSİ 
                  SİSİSİSİSİSİ 
                   SİSİSİSİSİS 
                    SİSİSİSİS 
                     SİSİSİSİ 
                      SİSİSİS 
                       SİSİSİ 
                        SİSİS 
                         SİSİ 
                          Sİ 
                           S`; 
 
                sisi.innerHTML = sisiText; 
 
                sisi.style.left = Math.random() * (window.innerWidth - 300) + 'px'; 
                sisi.style.top = window.innerHeight + 'px'; 
                sisi.style.fontSize = "16px";  // Yazı boyutunu biraz büyüttük 
                sisi.style.whiteSpace = "pre-line";  // Satır başı boşluklarını ve yeni satırları göstermek için 
                sisi.style.animationDuration = (4 + Math.random() * 3) + 's';  // Animasyon süresi rastgele değişecek 
                sisi.style.display = 'block';  // Yazıyı görünür yap 
                document.body.appendChild(sisi); 
 
                setTimeout(() => { 
                    if (sisi.parentNode) { 
                        sisi.remove(); 
                    } 
                }, 5000);  // Yazıyı 5 saniye sonra kaldırma 
            } 
 
            createHeart() { 
                const heart = document.createElement('div'); 
                heart.className = 'heart'; 
 
                const hearts = ['❤️', '💖', '💕', '💗', '💝', '💘', '💞']; 
                heart.textContent = hearts[Math.floor(Math.random() * hearts.length)]; 
 
                heart.style.left = Math.random() * (window.innerWidth - 50) + 'px'; 
                heart.style.top = window.innerHeight + 'px'; 
 
                document.body.appendChild(heart); 
 
                setTimeout(() => { 
                    if (heart.parentNode) { 
                        heart.remove(); 
                    } 
                }, 2500);  // Kalp 2.5 saniye sonra kaybolur 
            } 
 
            start() { 
                if (this.animationStarted) return; 
                this.animationStarted = true; 
 
                // Hide button 
                document.querySelector('.welcome-btn').style.display = 'none'; 
 
                // Fill canvas with black 
                this.ctx.fillStyle = "black"; 
                this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height); 
 
                // Start animations 
                this.matrixInterval = setInterval(() => this.drawMatrix(), 50); 
                this.heartInterval = setInterval(() => this.createHeart(), 150); 
                this.sisiInterval = setInterval(() => this.createSisi(), 600); 
            } 
 
            stop() { 
                if (this.matrixInterval) clearInterval(this.matrixInterval); 
                if (this.heartInterval) clearInterval(this.heartInterval); 
                if (this.sisiInterval) clearInterval(this.sisiInterval); 
            } 
        } 
 
        // Initialize the animation 
        const matrixApp = new MatrixAnimation(); 
 
        // Global function for button onclick 
        function startAnimation() { 
            matrixApp.start(); 
        } 
    </script> 
</body> 
</html>"""

    return html_content


def save_and_open_html(filename="matrix_sisi_enhanced.html"):
    """HTML dosyasını kaydet ve tarayıcıda aç"""
    try:
        # HTML içeriğini oluştur
        html_content = create_matrix_html()

        # Dosyayı kaydet
        file_path = Path(filename)
        with open(file_path, "w", encoding="utf-8") as f:
            f.write(html_content)

        print(f"✅ HTML dosyası oluşturuldu: {file_path.absolute()}")

        # Tarayıcıda aç
        webbrowser.open(file_path.absolute().as_uri())
        print("🌐 Tarayıcıda açılıyor...")

        return str(file_path.absolute())

    except Exception as e:
        print(f"❌ Hata oluştu: {e}")
        return None


if __name__ == "__main__":
    # Ana fonksiyonu çalıştır
    save_and_open_html()
