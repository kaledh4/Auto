<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auto Knowledge Base | Dashboard</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0a0f;
            --bg-secondary: #12121a;
            --bg-card: rgba(18, 18, 26, 0.8);
            --bg-glass: rgba(255, 255, 255, 0.03);
            --border-subtle: rgba(255, 255, 255, 0.06);
            --border-accent: rgba(139, 92, 246, 0.3);
            --text-primary: #f0f0f5;
            --text-secondary: #8b8b9a;
            --text-muted: #5a5a6e;
            --accent-primary: #8b5cf6;
            --accent-secondary: #a78bfa;
            --accent-glow: rgba(139, 92, 246, 0.4);
            --success: #10b981;
            --warning: #f59e0b;
            --error: #ef4444;
            --info: #3b82f6;
            --gradient-hero: linear-gradient(135deg, #8b5cf6 0%, #6366f1 50%, #3b82f6 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            line-height: 1.6;
            overflow-x: hidden;
        }

        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .bg-animation::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: 
                radial-gradient(ellipse at 20% 20%, rgba(139, 92, 246, 0.08) 0%, transparent 50%),
                radial-gradient(ellipse at 80% 80%, rgba(99, 102, 241, 0.06) 0%, transparent 50%),
                radial-gradient(ellipse at 50% 50%, rgba(59, 130, 246, 0.04) 0%, transparent 60%);
            animation: bgPulse 15s ease-in-out infinite;
        }

        @keyframes bgPulse {
            0%, 100% { transform: translate(0, 0) scale(1); }
            50% { transform: translate(-5%, -5%) scale(1.1); }
        }

        .floating-orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(80px);
            animation: float 20s ease-in-out infinite;
        }

        .orb-1 {
            width: 400px;
            height: 400px;
            background: rgba(139, 92, 246, 0.1);
            top: 10%;
            right: -100px;
        }

        .orb-2 {
            width: 300px;
            height: 300px;
            background: rgba(99, 102, 241, 0.08);
            bottom: 20%;
            left: -50px;
            animation-delay: -7s;
        }

        @keyframes float {
            0%, 100% { transform: translate(0, 0) rotate(0deg); }
            33% { transform: translate(30px, -30px) rotate(5deg); }
            66% { transform: translate(-20px, 20px) rotate(-5deg); }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        .header {
            text-align: center;
            padding: 40px 0 30px;
            position: relative;
        }

        .header::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--accent-primary), transparent);
        }

        .logo {
            display: inline-flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 8px;
        }

        .logo-icon {
            width: 48px;
            height: 48px;
            background: var(--gradient-hero);
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            box-shadow: 0 8px 32px var(--accent-glow);
            animation: logoGlow 3s ease-in-out infinite;
        }

        @keyframes logoGlow {
            0%, 100% { box-shadow: 0 8px 32px var(--accent-glow); }
            50% { box-shadow: 0 8px 48px var(--accent-glow), 0 0 60px var(--accent-glow); }
        }

        .logo h1 {
            font-size: 1.8rem;
            font-weight: 700;
            background: var(--gradient-hero);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            color: var(--text-secondary);
            font-size: 0.95rem;
            font-weight: 400;
        }

        .nav-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 12px;
            margin: 30px 0;
        }

        .nav-card {
            background: var(--bg-card);
            border: 1px solid var(--border-subtle);
            border-radius: 16px;
            padding: 20px 16px;
            text-align: center;
            text-decoration: none;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            backdrop-filter: blur(10px);
            position: relative;
            overflow: hidden;
            display: block;
        }

        .nav-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 2px;
            background: var(--gradient-hero);
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .nav-card:hover {
            transform: translateY(-4px);
            border-color: var(--border-accent);
            box-shadow: 0 12px 40px rgba(139, 92, 246, 0.15);
        }

        .nav-card:hover::before {
            transform: scaleX(1);
        }

        .nav-icon {
            font-size: 28px;
            margin-bottom: 8px;
            display: block;
        }

        .nav-label {
            font-size: 0.85rem;
            font-weight: 500;
            color: var(--text-primary);
        }

        .section {
            margin: 30px 0;
        }

        .section-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .section-title::before {
            content: '';
            width: 4px;
            height: 20px;
            background: var(--gradient-hero);
            border-radius: 2px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 16px;
        }

        .stat-card {
            background: var(--bg-card);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 24px;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::after {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(139, 92, 246, 0.1) 0%, transparent 70%);
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .stat-card:hover::after {
            opacity: 1;
        }

        .stat-card:hover {
            transform: translateY(-2px);
            border-color: var(--border-accent);
        }

        .stat-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 16px;
        }

        .stat-title {
            font-size: 0.85rem;
            color: var(--text-secondary);
            font-weight: 500;
        }

        .stat-indicator {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        .stat-indicator.online {
            background: var(--success);
            box-shadow: 0 0 12px var(--success);
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.6; transform: scale(1.2); }
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--text-primary);
            font-family: 'JetBrains Mono', monospace;
        }

        .stat-meta {
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-top: 8px;
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 12px;
        }

        .service-card {
            background: var(--bg-glass);
            border: 1px solid var(--border-subtle);
            border-radius: 14px;
            padding: 18px;
            display: flex;
            align-items: center;
            gap: 14px;
            transition: all 0.3s ease;
        }

        .service-card:hover {
            border-color: var(--border-accent);
            background: rgba(139, 92, 246, 0.05);
        }

        .service-icon {
            width: 42px;
            height: 42px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            flex-shrink: 0;
            background: rgba(16, 185, 129, 0.15);
            color: var(--success);
        }

        .service-info {
            flex: 1;
            min-width: 0;
        }

        .service-name {
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .service-status {
            font-size: 0.75rem;
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .service-status::before {
            content: '';
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: var(--success);
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--text-muted);
        }

        .empty-icon {
            font-size: 48px;
            margin-bottom: 12px;
            opacity: 0.5;
        }

        .footer {
            text-align: center;
            padding: 40px 20px;
            margin-top: 40px;
            border-top: 1px solid var(--border-subtle);
        }

        .footer-text {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        @media (max-width: 640px) {
            .container {
                padding: 16px;
            }

            .header {
                padding: 30px 0 20px;
            }

            .logo h1 {
                font-size: 1.4rem;
            }

            .logo-icon {
                width: 40px;
                height: 40px;
                font-size: 20px;
            }

            .nav-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 10px;
            }

            .nav-card {
                padding: 16px 12px;
            }

            .stat-card {
                padding: 20px;
            }

            .services-grid {
                grid-template-columns: 1fr;
            }
        }

        .fade-in {
            animation: fadeIn 0.5s ease forwards;
            opacity: 0;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .stagger-1 { animation-delay: 0.1s; }
        .stagger-2 { animation-delay: 0.2s; }
        .stagger-3 { animation-delay: 0.3s; }
    </style>
</head>
<body>
    <div class="bg-animation">
        <div class="floating-orb orb-1"></div>
        <div class="floating-orb orb-2"></div>
    </div>

    <div class="container">
        <header class="header fade-in">
            <div class="logo">
                <div class="logo-icon">🧠</div>
                <h1>Auto Knowledge Base</h1>
            </div>
            <p class="subtitle">Real-time monitoring & documentation system</p>
        </header>

        <nav class="nav-grid fade-in stagger-1">
            <a href="./admin/config.html" class="nav-card">
                <span class="nav-icon">⚙️</span>
                <span class="nav-label">Admin Settings</span>
            </a>
            <a href="./admin/status.html" class="nav-card">
                <span class="nav-icon">📈</span>
                <span class="nav-label">System Status</span>
            </a>
            <a href="./kb/research_gaps.html" class="nav-card">
                <span class="nav-icon">🔍</span>
                <span class="nav-label">Research Gaps</span>
            </a>
        </nav>

        <section class="section fade-in stagger-2">
            <h2 class="section-title">Services</h2>
            <div class="services-grid">
                <div class="service-card">
                    <div class="service-icon">📥</div>
                    <div class="service-info">
                        <div class="service-name">Data Aggregator</div>
                        <div class="service-status">Online</div>
                    </div>
                </div>
                <div class="service-card">
                    <div class="service-icon">📝</div>
                    <div class="service-info">
                        <div class="service-name">Report Generator</div>
                        <div class="service-status">Online</div>
                    </div>
                </div>
                <div class="service-card">
                    <div class="service-icon">🔄</div>
                    <div class="service-info">
                        <div class="service-name">GitHub Sync</div>
                        <div class="service-status">Online</div>
                    </div>
                </div>
            </div>
        </section>

        <section class="section fade-in stagger-3">
            <h2 class="section-title">Recent Activity</h2>
            <div class="stat-card">
                <div class="empty-state">
                    <div class="empty-icon">📭</div>
                    <p>No activity logged yet</p>
                </div>
            </div>
        </section>

        <footer class="footer fade-in">
            <p class="footer-text">Auto Knowledge Base • Backend runs independently on VPS</p>
            <p class="footer-text" style="margin-top: 8px;">Designed for mobile-first experience</p>
        </footer>
    </div>
</body>
</html>
