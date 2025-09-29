# SIH
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Defence Cyber Incident & Safety Portal</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-color: #00d4aa;
            --secondary-color: #1a1a2e;
            --accent-color: #16213e;
            --danger-color: #ff4757;
            --warning-color: #ffa502;
            --success-color: #2ed573;
            --dark-bg: #0f0f23;
            --card-bg: rgba(255, 255, 255, 0.05);
            --text-primary: #ffffff;
            --text-secondary: rgba(255, 255, 255, 0.8);
        }

        body {
            font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, var(--dark-bg) 0%, var(--secondary-color) 50%, var(--accent-color) 100%);
            color: var(--text-primary);
            min-height: 100vh;
            line-height: 1.6;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header Styles */
        header {
            background: rgba(0, 0, 0, 0.4);
            backdrop-filter: blur(20px);
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 2px solid var(--primary-color);
            transition: all 0.3s ease;
        }

        header.scrolled {
            background: rgba(0, 0, 0, 0.8);
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo i {
            font-size: 2.2rem;
            color: var(--primary-color);
            filter: drop-shadow(0 0 10px rgba(0, 212, 170, 0.5));
        }

        .logo h1 {
            font-size: 1.6rem;
            font-weight: 700;
            background: linear-gradient(45deg, var(--primary-color), #ffffff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2.5rem;
        }

        .nav-links a {
            color: var(--text-primary);
            text-decoration: none;
            transition: all 0.3s ease;
            font-weight: 500;
            position: relative;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary-color);
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after,
        .nav-links a.active::after {
            width: 100%;
        }

        .auth-buttons {
            display: flex;
            gap: 1rem;
        }

        .btn {
            padding: 0.8rem 1.8rem;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s ease;
            font-size: 0.95rem;
        }

        .btn-primary {
            background: linear-gradient(45deg, var(--primary-color), #00b894);
            color: var(--secondary-color);
            box-shadow: 0 4px 15px rgba(0, 212, 170, 0.3);
        }

        .btn-secondary {
            background: transparent;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 212, 170, 0.4);
        }

        /* Main Content */
        main {
            margin-top: 100px;
            padding: 2rem 0;
        }

        .page {
            display: none;
            animation: fadeInUp 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .page.active {
            display: block;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Hero Section */
        .hero {
            text-align: center;
            padding: 5rem 0;
            background: radial-gradient(circle at 50% 50%, rgba(0, 212, 170, 0.1) 0%, transparent 70%);
            border-radius: 25px;
            margin-bottom: 4rem;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: conic-gradient(from 0deg, transparent, rgba(0, 212, 170, 0.05), transparent);
            animation: rotate 25s linear infinite;
        }

        @keyframes rotate {
            to { transform: rotate(360deg); }
        }

        .hero-content {
            position: relative;
            z-index: 2;
        }

        .hero h2 {
            font-size: clamp(2.5rem, 5vw, 4rem);
            margin-bottom: 1.5rem;
            background: linear-gradient(45deg, var(--primary-color), #ffffff, var(--primary-color));
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: shimmer 3s linear infinite;
        }

        @keyframes shimmer {
            to { background-position: 200% center; }
        }

        .hero p {
            font-size: 1.3rem;
            margin-bottom: 2.5rem;
            color: var(--text-secondary);
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            line-height: 1.8;
        }

        .hero-stats {
            display: flex;
            justify-content: center;
            gap: 3rem;
            margin-top: 3rem;
        }

        .hero-stat {
            text-align: center;
        }

        .hero-stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--primary-color);
        }

        .hero-stat-label {
            font-size: 0.9rem;
            color: var(--text-secondary);
            margin-top: 0.5rem;
        }

        /* Features Grid */
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 2.5rem;
            margin: 4rem 0;
        }

        .feature-card {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            padding: 2.5rem;
            border-radius: 20px;
            border: 1px solid rgba(0, 212, 170, 0.2);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }

        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--primary-color), transparent);
            transform: translateX(-100%);
            transition: transform 0.8s ease;
        }

        .feature-card:hover::before {
            transform: translateX(100%);
        }

        .feature-card:hover {
            transform: translateY(-15px);
            box-shadow: 0 25px 50px rgba(0, 212, 170, 0.3);
            border-color: var(--primary-color);
        }

        .feature-card i {
            font-size: 3.5rem;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
            display: block;
        }

        .feature-card h3 {
            font-size: 1.6rem;
            margin-bottom: 1rem;
            color: var(--text-primary);
        }

        .feature-card p {
            color: var(--text-secondary);
            line-height: 1.7;
        }

        /* Incident Report Form */
        .report-section {
            max-width: 900px;
            margin: 0 auto;
        }

        .report-form {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            padding: 3rem;
            border-radius: 20px;
            border: 1px solid rgba(0, 212, 170, 0.2);
            margin: 2rem 0;
        }

        .form-group {
            margin-bottom: 2rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.8rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 1rem;
            border: 2px solid rgba(0, 212, 170, 0.2);
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.05);
            color: var(--text-primary);
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(0, 212, 170, 0.1);
        }

        .file-upload-area {
            border: 3px dashed rgba(0, 212, 170, 0.4);
            padding: 3rem;
            text-align: center;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(0, 212, 170, 0.02);
        }

        .file-upload-area:hover {
            border-color: var(--primary-color);
            background: rgba(0, 212, 170, 0.05);
        }

        .file-upload-area.drag-over {
            border-color: var(--primary-color);
            background: rgba(0, 212, 170, 0.1);
        }

        /* Dashboard Styles */
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 3rem;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .dashboard-title {
            font-size: 2.5rem;
            font-weight: 700;
            background: linear-gradient(45deg, var(--primary-color), #ffffff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .dashboard-controls {
            display: flex;
            gap: 1rem;
            align-items: center;
        }

        .filter-select {
            padding: 0.8rem 1.2rem;
            background: var(--card-bg);
            color: var(--text-primary);
            border: 1px solid rgba(0, 212, 170, 0.3);
            border-radius: 8px;
            backdrop-filter: blur(10px);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            margin-bottom: 3rem;
        }

        .stat-card {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            padding: 2rem;
            border-radius: 15px;
            border: 1px solid rgba(0, 212, 170, 0.2);
            position: relative;
            overflow: hidden;
            transition: transform 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(45deg, var(--primary-color), var(--success-color), var(--warning-color), var(--danger-color));
            background-size: 400% 400%;
            animation: gradientShift 3s ease infinite;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .stat-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .stat-icon {
            font-size: 2rem;
            color: var(--primary-color);
        }

        .stat-trend {
            font-size: 0.9rem;
            padding: 0.3rem 0.8rem;
            border-radius: 15px;
            font-weight: 600;
        }

        .trend-up {
            background: rgba(255, 71, 87, 0.2);
            color: var(--danger-color);
        }

        .trend-down {
            background: rgba(46, 213, 115, 0.2);
            color: var(--success-color);
        }

        .stat-number {
            font-size: 3rem;
            font-weight: 700;
            color: var(--text-primary);
            margin-bottom: 0.5rem;
        }

        .stat-label {
            color: var(--text-secondary);
            font-size: 1rem;
        }

        /* Charts */
        .chart-grid {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 2rem;
            margin-bottom: 3rem;
        }

        .chart-container {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            padding: 2rem;
            border-radius: 15px;
            border: 1px solid rgba(0, 212, 170, 0.2);
        }

        .chart-title {
            font-size: 1.4rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            color: var(--text-primary);
        }

        /* Incidents Table */
        .incidents-section {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            border-radius: 15px;
            border: 1px solid rgba(0, 212, 170, 0.2);
            overflow: hidden;
        }

        .section-header {
            background: rgba(0, 212, 170, 0.1);
            padding: 1.5rem 2rem;
            border-bottom: 1px solid rgba(0, 212, 170, 0.2);
        }

        .section-title {
            font-size: 1.4rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .table-container {
            overflow-x: auto;
        }

        .incidents-table {
            width: 100%;
            border-collapse: collapse;
        }

        .table-header {
            background: rgba(0, 212, 170, 0.05);
        }

        .table-header th {
            padding: 1.2rem;
            text-align: left;
            font-weight: 600;
            color: var(--text-primary);
            border-bottom: 1px solid rgba(0, 212, 170, 0.2);
        }

        .table-row td {
            padding: 1.2rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            color: var(--text-secondary);
        }

        .table-row:hover {
            background: rgba(0, 212, 170, 0.02);
        }

        .priority-critical { color: var(--danger-color); font-weight: 600; }
        .priority-high { color: #ff6348; font-weight: 600; }
        .priority-medium { color: var(--warning-color); font-weight: 600; }
        .priority-low { color: var(--success-color); font-weight: 600; }

        .status-badge {
            padding: 0.4rem 1rem;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            text-align: center;
            min-width: 80px;
            display: inline-block;
        }

        .status-new { background: rgba(0, 212, 170, 0.2); color: var(--primary-color); }
        .status-investigating { background: rgba(255, 165, 2, 0.2); color: var(--warning-color); }
        .status-resolved { background: rgba(46, 213, 115, 0.2); color: var(--success-color); }
        .status-closed { background: rgba(113, 128, 150, 0.2); color: #718096; }

        .action-buttons {
            display: flex;
            gap: 0.5rem;
        }

        .btn-sm {
            padding: 0.4rem 0.8rem;
            font-size: 0.8rem;
            border-radius: 5px;
        }

        /* Alerts */
        .alert {
            padding: 1.2rem;
            border-radius: 10px;
            margin-bottom: 1.5rem;
            border-left: 4px solid;
            backdrop-filter: blur(10px);
        }

        .alert-success {
            background: rgba(46, 213, 115, 0.1);
            border-color: var(--success-color);
            color: var(--success-color);
        }

        .alert-warning {
            background: rgba(255, 165, 2, 0.1);
            border-color: var(--warning-color);
            color: var(--warning-color);
        }

        .alert-danger {
            background: rgba(255, 71, 87, 0.1);
            border-color: var(--danger-color);
            color: var(--danger-color);
        }

        .alert-info {
            background: rgba(0, 212, 170, 0.1);
            border-color: var(--primary-color);
            color: var(--primary-color);
        }

        /* Loading Animation */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: var(--primary-color);
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Real-time Updates */
        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            .hero-stats {
                flex-direction: column;
                gap: 1.5rem;
            }
            
            .chart-grid {
                grid-template-columns: 1fr;
            }
            
            .dashboard-header {
                flex-direction: column;
                align-items: stretch;
            }
            
            .dashboard-controls {
                justify-content: center;
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .features {
                grid-template-columns: 1fr;
            }
            
            .table-container {
                font-size: 0.9rem;
            }
        }

        /* Mobile Menu */
        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: var(--text-primary);
            font-size: 1.5rem;
            cursor: pointer;
        }

        @media (max-width: 768px) {
            .mobile-menu-btn {
                display: block;
            }
            
            .nav-links {
                position: absolute;
                top: 100%;
                left: 0;
                right: 0;
                background: rgba(0, 0, 0, 0.95);
                backdrop-filter: blur(20px);
                flex-direction: column;
                padding: 2rem;
                transform: translateY(-100%);
                opacity: 0;
                visibility: hidden;
                transition: all 0.3s ease;
            }
            
            .nav-links.active {
                transform: translateY(0);
                opacity: 1;
                visibility: visible;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav class="container">
            <div class="logo">
                <i class="fas fa-shield-alt"></i>
                <h1>DefCyber Portal</h1>
            </div>
            <ul class="nav-links">
                <li><a href="#" onclick="showPage('home')" class="nav-link">Home</a></li>
                <li><a href="#" onclick="showPage('report')" class="nav-link">Report Incident</a></li>
                <li><a href="#" onclick="showPage('dashboard')" class="nav-link">Dashboard</a></li>
                <li><a href="#" onclick="showPage('analytics')" class="nav-link">Analytics</a></li>
                <li><a href="#" onclick="showPage('resources')" class="nav-link">Resources</a></li>
            </ul>
            <div class="auth-buttons">
                <a href="#" class="btn btn-secondary">
                    <i class="fas fa-sign-in-alt"></i>
                    Login
                </a>
                <a href="#" class="btn btn-primary">
                    <i class="fas fa-id-card"></i>
                    CAC/PIV Login
                </a>
            </div>
            <button class="mobile-menu-btn" onclick="toggleMobileMenu()">
                <i class="fas fa-bars"></i>
            </button>
        </nav>
    </header>

    <main class="container">
        <!-- Home Page -->
        <div id="home" class="page active">
            <section class="hero">
                <div class="hero-content">
                    <h2>Defence Cyber Incident & Safety Portal</h2>
                    <p>Advanced AI-powered cybersecurity protection for defence personnel, families, and veterans. Report incidents, receive real-time threat analysis, and access immediate mitigation guidance through our secure platform.</p>
                    <div>
                        <a href="#" class="btn btn-primary" onclick="showPage('report')">
                            <i class="fas fa-exclamation-triangle"></i>
                            Report Incident Now
                        </a>
                        <a href="#" class="btn btn-secondary" onclick="showPage('dashboard')">
                            <i class="fas fa-chart-line"></i>
                            View Dashboard
                        </a>
                    </div>
                    <div class="hero-stats">
                        <div class="hero-stat">
                            <div class="hero-stat-number">2,847</div>
                            <div class="hero-stat-label">Incidents Resolved</div>
                        </div>
                        <div class="hero-stat">
                            <div class="hero-stat-number">99.2%</div>
                            <div class="hero-stat-label">Threat Detection Rate</div>
                        </div>
                        <div class="hero-stat">
                            <div class="hero-stat-number">< 2min</div>
                            <div class="hero-stat-label">Average Response Time</div>
                        </div>
                    </div>
                </div>
            </section>

            <section class="features">
                <div class="feature-card">
                    <i class="fas fa-brain"></i>
                    <h3>Advanced AI Analysis</h3>
                    <p>State-of-the-art machine learning algorithms analyze threats in real-time, identifying sophisticated attack patterns, espionage indicators, and targeted campaigns with 99%+ accuracy.</p>
                </div>
                
                <div class="feature-card">
                    <i class="fas fa-file-medical-alt"></i>
                    <h3>Multi-Format Evidence Processing</h3>
                    <p>Upload and analyze suspicious content in any format - text messages, URLs, images, audio files, videos, and documents. Our system processes all formats comprehensively.</p>
                </div>
                
                <div class="feature-card">
                    <i class="fas fa-bolt"></i>
                    <h3>Instant Alert System</h3>
                    <p>Receive immediate notifications when malicious content is detected, along with automated mitigation steps, security recommendations, and escalation procedures.</p>
                </div>
                
                <div class="feature-card">
                    <i class="fas fa-network-wired"></i>
                    <h3>CERT-Army Integration</h3>
                    <p>Seamless integration with CERT-Army workflows ensures priority handling of defence-related incidents with structured response protocols and chain of command.</p>
                </div>
                
                <div class="feature-card">
                    <i class="fas fa-mobile-alt"></i>
                    <h3>Cross-Platform Access</h3>
                    <p>Access the portal from anywhere with secure web and mobile applications, specifically designed for field conditions and operational requirements.</p>
                </div>
                
                <div class="feature-card">
                    <i class="fas fa-lock"></i>
                    <h3>Military-Grade Security</h3>
                    <p>End-to-end encryption, zero-trust architecture, role-based access controls, and full compliance with defence data security standards and regulations.</p>
                </div>
            </section>

            <div class="alert alert-info">
                <strong><i class="fas fa-info-circle"></i> Security Notice:</strong> This portal is exclusively for serving defence personnel, their families, and veterans. All communications are encrypted and monitored for security compliance.
            </div>
        </div>

        <!-- Report Incident Page -->
        <div id="report" class="page">
            <div class="report-section">
                <h2 style="text-align: center; margin-bottom: 2rem; font-size: 2.5rem;">Report Cyber Security Incident</h2>
                
                <div class="alert alert-warning">
                    <strong><i class="fas fa-shield-alt"></i> Secure Reporting:</strong> All submitted information is encrypted and processed by AI for immediate threat assessment. CERT-Army will be automatically notified for high-priority incidents.
                </div>

                <form class="report-form" id="incidentForm">
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 2rem;">
                        <div class="form-group">
                            <label for="incidentType">
                                <i class="fas fa-exclamation-triangle"></i> Incident Type
                            </label>
                            <select id="incidentType" name="incidentType" required>
                                <option value="">Select Incident Type</option>
                                <option value="phishing">Phishing/Social Engineering</option>
                                <option value="malware">Malware/Suspicious Files</option>
                                <option value="fraud">Financial Fraud</option>
                                <option value="espionage">Suspected Espionage</option>
                                <option value="honeytrap">Honeytrap/Romance Scam</option>
                                <option value="identity">Identity Theft</option>
                                <option value="opsec">OPSEC Violation</option>
                                <option value="data-breach">Data Breach</option>
                                <option value="other">Other Security Incident</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label for="priority">
                                <i class="fas fa-flag"></i> Priority Level
                            </label>
                            <select id="priority" name="priority" required>
                                <option value="">Select Priority</option>
                                <option value="low">Low - Suspicious but no immediate threat</option>
                                <option value="medium">Medium - Potential security risk</option>
                                <option value="high">High - Active threat detected</option>
                                <option value="critical">Critical - National security concern</option>
                            </select>
                        </div>
                    </div>

                    <div class="form-group">
                        <label
