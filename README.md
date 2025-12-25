<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PFTH | The Archive</title>
    <style>
        * {
            box-sizing: border-box;
        }
        
        body { 
            margin: 0; 
            background-color: #000; 
            color: #fff; 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; 
            height: 100vh; 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            justify-content: center; 
            text-align: center;
            overflow: hidden;
            position: relative;
        }
        
        /* Animated background */
        .background-grid {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                linear-gradient(rgba(10, 10, 10, 0.9) 1px, transparent 1px),
                linear-gradient(90deg, rgba(10, 10, 10, 0.9) 1px, transparent 1px);
            background-size: 20px 20px;
            opacity: 0.15;
            z-index: -1;
        }
        
        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            z-index: -1;
        }
        
        /* THE BLACK SUIT CONCIERGE */
        .concierge-frame { 
            width: 280px; 
            height: 380px; 
            border: 1px solid #1a1a1a; 
            background: #050505; 
            margin-bottom: 2.5rem; 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            justify-content: center;
            position: relative;
            overflow: hidden;
            transition: all 0.4s ease;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.7);
        }
        
        .concierge-frame::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 1px;
            background: linear-gradient(90deg, transparent, #fff, transparent);
            animation: scanline 6s infinite linear;
            animation-delay: 2s;
        }
        
        @keyframes scanline {
            0% { left: -100%; }
            100% { left: 100%; }
        }
        
        .concierge-frame:hover {
            border-color: #333;
            transform: translateY(-5px);
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.9);
        }
        
        .concierge-label { 
            font-size: 9px; 
            letter-spacing: 3px; 
            color: #666; 
            text-transform: uppercase; 
            line-height: 2;
            transition: color 0.3s;
            position: relative;
            z-index: 2;
        }
        
        .concierge-frame:hover .concierge-label {
            color: #aaa;
        }
        
        /* Animated concierge interior */
        .concierge-interior {
            position: absolute;
            width: 100%;
            height: 100%;
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            grid-template-rows: repeat(15, 1fr);
            opacity: 0.05;
            z-index: 1;
        }
        
        .interior-cell {
            border-right: 1px solid rgba(50, 50, 50, 0.2);
            border-bottom: 1px solid rgba(50, 50, 50, 0.2);
        }
        
        /* BRANDING */
        h1 { 
            font-weight: 200; 
            letter-spacing: 18px; 
            margin: 0; 
            text-transform: uppercase; 
            font-size: 2.2rem;
            position: relative;
            padding-bottom: 15px;
            transition: letter-spacing 0.5s;
        }
        
        h1:hover {
            letter-spacing: 22px;
        }
        
        h1::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, #fff, transparent);
            transition: width 0.5s;
        }
        
        h1:hover::after {
            width: 150px;
        }
        
        .tagline { 
            font-size: 10px; 
            letter-spacing: 5px; 
            color: #666; 
            margin-top: 15px; 
            text-transform: uppercase;
            transition: color 0.4s;
        }
        
        .tagline:hover {
            color: #999;
        }
        
        .asset-count {
            font-size: 9px;
            letter-spacing: 3px;
            color: #444;
            margin-top: 5px;
            text-transform: uppercase;
            animation: pulse 4s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 1; }
        }
        
        /* THE GATEWAY */
        .gate-btn { 
            margin-top: 50px; 
            padding: 18px 50px; 
            background: transparent; 
            border: 1px solid #fff; 
            color: #fff; 
            text-transform: uppercase; 
            letter-spacing: 6px; 
            font-size: 10px; 
            cursor: pointer; 
            transition: all 0.3s; 
            position: relative;
            overflow: hidden;
        }
        
        .gate-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transition: left 0.7s;
        }
        
        .gate-btn:hover { 
            background: #fff; 
            color: #000; 
            letter-spacing: 8px;
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.3);
        }
        
        .gate-btn:hover::before {
            left: 100%;
        }
        
        .gate-btn:active {
            transform: scale(0.98);
        }
        
        .loading-dots {
            display: none;
            letter-spacing: 2px;
            margin-top: 10px;
            font-size: 12px;
            color: #666;
        }
        
        .loading-dots span {
            animation: blink 1.4s infinite both;
        }
        
        .loading-dots span:nth-child(2) {
            animation-delay: 0.2s;
        }
        
        .loading-dots span:nth-child(3) {
            animation-delay: 0.4s;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }
        
        /* Status indicator */
        .status-indicator {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 25px;
            font-size: 8px;
            letter-spacing: 3px;
            color: #333;
            text-transform: uppercase;
        }
        
        .status-light {
            width: 8px;
            height: 8px;
            background-color: #0a0;
            border-radius: 50%;
            margin-right: 8px;
            animation: status-pulse 2s infinite;
            box-shadow: 0 0 8px #0a0;
        }
        
        @keyframes status-pulse {
            0%, 100% { opacity: 0.7; }
            50% { opacity: 1; }
        }
        
        .launch-footer { 
            position: fixed; 
            bottom: 30px; 
            font-size: 8px; 
            color: #222; 
            letter-spacing: 2px;
            transition: color 0.4s;
        }
        
        .launch-footer:hover {
            color: #444;
        }
        
        /* Access Panel (hidden by default) */
        .access-panel {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 100;
            opacity: 0;
            transition: opacity 0.5s;
        }
        
        .access-header {
            font-size: 12px;
            letter-spacing: 8px;
            color: #666;
            margin-bottom: 40px;
            text-transform: uppercase;
        }
        
        .access-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            max-width: 800px;
            padding: 30px;
        }
        
        .asset-card {
            background: rgba(20, 20, 20, 0.8);
            border: 1px solid #222;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .asset-card:hover {
            border-color: #666;
            transform: translateY(-5px);
            background: rgba(30, 30, 30, 0.9);
        }
        
        .asset-type {
            font-size: 8px;
            letter-spacing: 3px;
            color: #666;
            text-transform: uppercase;
            margin-bottom: 10px;
        }
        
        .close-panel {
            position: absolute;
            top: 40px;
            right: 40px;
            background: transparent;
            border: 1px solid #333;
            color: #666;
            width: 40px;
            height: 40px;
            cursor: pointer;
            font-size: 20px;
            transition: all 0.3s;
        }
        
        .close-panel:hover {
            color: #fff;
            border-color: #fff;
        }
        
        /* Responsive adjustments */
        @media (max-width: 768px) {
            h1 {
                font-size: 1.5rem;
                letter-spacing: 10px;
            }
            
            .concierge-frame {
                width: 250px;
                height: 350px;
            }
            
            .gate-btn {
                padding: 15px 40px;
            }
            
            .access-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 15px;
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="background-grid"></div>
    
    <!-- Animated particles -->
    <div class="particles-container"></div>
    
    <!-- Concierge Frame -->
    <div class="concierge-frame">
        <div class="concierge-interior" id="conciergeGrid"></div>
        <div class="concierge-label">AI Concierge Active<br>Attire: Black Suit<br>Status: Ready</div>
    </div>
    
    <!-- Branding -->
    <h1>Pfth</h1>
    <div class="tagline">The Archive // 2,000+ Assets</div>
    <div class="asset-count" id="assetCounter">Loading Assets: <span id="count">0</span>/2000+</div>
    
    <!-- Gateway Button -->
    <button class="gate-btn" id="gatewayBtn">Enter Archive</button>
    
    <!-- Loading Indicator -->
    <div class="loading-dots" id="loadingIndicator">
        <span>.</span><span>.</span><span>.</span>
    </div>
    
    <!-- Status Indicator -->
    <div class="status-indicator">
        <div class="status-light"></div>
        <div class="status-text">System Online</div>
    </div>
    
    <!-- Launch Footer -->
    <div class="launch-footer">LAUNCHED DEC 23, 2025</div>
    
    <!-- Access Panel -->
    <div class="access-panel" id="accessPanel">
        <button class="close-panel" id="closePanel">×</button>
        <div class="access-header">Pfth Archive - Secure Access</div>
        <div class="access-grid" id="assetGrid">
            <!-- Asset cards will be generated here -->
        </div>
    </div>

    <script>
        // Initialize particles
        function initParticles() {
            const container = document.querySelector('.particles-container');
            const particleCount = 50;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                
                // Random position
                particle.style.left = `${Math.random() * 100}%`;
                particle.style.top = `${Math.random() * 100}%`;
                
                // Random animation
                const duration = 3 + Math.random() * 5;
                const delay = Math.random() * 5;
                
                particle.style.animation = `float ${duration}s infinite ${delay}s`;
                
                // Create custom float animation
                const style = document.createElement('style');
                style.textContent = `
                    @keyframes float {
                        0%, 100% { transform: translate(0, 0) scale(1); opacity: 0.2; }
                        33% { transform: translate(${Math.random() * 40 - 20}px, ${Math.random() * 40 - 20}px) scale(${0.5 + Math.random()}); opacity: 0.7; }
                        66% { transform: translate(${Math.random() * 40 - 20}px, ${Math.random() * 40 - 20}px) scale(${0.5 + Math.random()}); opacity: 0.3; }
                    }
                `;
                document.head.appendChild(style);
                
                container.appendChild(particle);
            }
        }
        
        // Initialize concierge grid
        function initConciergeGrid() {
            const grid = document.getElementById('conciergeGrid');
            const rows = 15;
            const cols = 10;
            
            for (let i = 0; i < rows * cols; i++) {
                const cell = document.createElement('div');
                cell.className = 'interior-cell';
                
                // Randomly add active cells
                if (Math.random() > 0.7) {
                    cell.style.backgroundColor = 'rgba(80, 80, 80, 0.1)';
                }
                
                grid.appendChild(cell);
            }
        }
        
        // Animate asset counter
        function animateAssetCounter() {
            const counter = document.getElementById('count');
            const target = 2000;
            let current = 0;
            const increment = target / 100;
            const interval = setInterval(() => {
                current += increment;
                counter.textContent = Math.floor(current);
                
                if (current >= target) {
                    clearInterval(interval);
                    counter.textContent = target + '+';
                }
            }, 30);
        }
        
        // Simulate archive access
        function accessArchive() {
            const btn = document.getElementById('gatewayBtn');
            const loading = document.getElementById('loadingIndicator');
            const panel = document.getElementById('accessPanel');
            
            // Show loading
            btn.style.display = 'none';
            loading.style.display = 'block';
            
            // Simulate loading time
            setTimeout(() => {
                loading.style.display = 'none';
                
                // Show access panel
                panel.style.display = 'flex';
                setTimeout(() => {
                    panel.style.opacity = '1';
                }, 10);
                
                // Generate asset cards
                generateAssetCards();
            }, 2000);
        }
        
        // Generate sample asset cards
        function generateAssetCards() {
            const grid = document.getElementById('assetGrid');
            const assetTypes = [
                'Visual Media', 'Audio Files', 'Documents', 'Code Repositories',
                '3D Models', 'Archival Footage', 'Research Data', 'Design Assets'
            ];
            
            // Clear any existing cards
            grid.innerHTML = '';
            
            // Create 8 asset cards
            for (let i = 0; i < 8; i++) {
                const card = document.createElement('div');
                card.className = 'asset-card';
                
                const type = assetTypes[i];
                const count = Math.floor(Math.random() * 300) + 100;
                
                card.innerHTML = `
                    <div class="asset-type">${type}</div>
                    <div style="font-size: 24px; margin: 10px 0;">${count}</div>
                    <div style="font-size: 9px; color: #666; letter-spacing: 2px;">ARCHIVED FILES</div>
                `;
                
                // Add click event
                card.addEventListener('click', () => {
                    alert(`Accessing ${type} archive...\n${count} files available.`);
                });
                
                grid.appendChild(card);
            }
        }
        
        // Close access panel
        function closeAccessPanel() {
            const panel = document.getElementById('accessPanel');
            const btn = document.getElementById('gatewayBtn');
            
            panel.style.opacity = '0';
            setTimeout(() => {
                panel.style.display = 'none';
                btn.style.display = 'block';
            }, 500);
        }
        
        // Initialize when page loads
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize visual elements
            initParticles();
            initConciergeGrid();
            animateAssetCounter();
            
            // Set up event listeners
            document.getElementById('gatewayBtn').addEventListener('click', accessArchive);
            document.getElementById('closePanel').addEventListener('click', closeAccessPanel);
            
            // Add click sound effect to gate button
            const gateBtn = document.getElementById('gatewayBtn');
            gateBtn.addEventListener('click', () => {
                // Create a subtle click sound using Web Audio API
                try {
                    const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    const oscillator = audioContext.createOscillator();
                    const gainNode = audioContext.createGain();
                    
                    oscillator.connect(gainNode);
                    gainNode.connect(audioContext.destination);
                    
                    oscillator.frequency.value = 800;
                    oscillator.type = 'sine';
                    
                    gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.1);
                    
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + 0.1);
                } catch (e) {
                    // Audio context not supported, continue silently
                }
            });
            
            // Add keyboard shortcut (Ctrl+Enter or Cmd+Enter) to access archive
            document.addEventListener('keydown', (e) => {
                if ((e.ctrlKey || e.metaKey) && e.key === 'Enter') {
                    accessArchive();
                }
                
                // Escape key closes panel
                if (e.key === 'Escape') {
                    closeAccessPanel();
                }
            });
        });
    </script>
</body>
</html>