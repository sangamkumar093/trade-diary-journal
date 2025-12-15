<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TradeLog Pro - Advanced Trading Journal</title>
    
    <!-- 3D Icons Library -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Chart.js for Analytics -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <!-- Calendar CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">
    <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>
    
    <style>
        /* ===== MODERN CSS VARIABLES ===== */
        :root {
            --primary: #2563eb;
            --primary-dark: #1d4ed8;
            --primary-light: #60a5fa;
            --secondary: #1e293b;
            --dark: #0f172a;
            --light: #f8fafc;
            --gray: #64748b;
            --gray-light: #cbd5e1;
            --success: #10b981;
            --danger: #ef4444;
            --warning: #f59e0b;
            --purple: #8b5cf6;
            --teal: #14b8a6;
            
            /* 3D Effects */
            --shadow-soft: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            --shadow-medium: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
            --shadow-hard: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
            --shadow-3d: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            --gradient-primary: linear-gradient(135deg, var(--primary), var(--purple));
            --gradient-success: linear-gradient(135deg, var(--success), var(--teal));
            --gradient-warning: linear-gradient(135deg, var(--warning), #f97316);
            
            /* 3D Icon Colors */
            --icon-3d-blue: linear-gradient(145deg, #3b82f6, #1d4ed8);
            --icon-3d-green: linear-gradient(145deg, #10b981, #059669);
            --icon-3d-purple: linear-gradient(145deg, #8b5cf6, #7c3aed);
            --icon-3d-orange: linear-gradient(145deg, #f59e0b, #d97706);
            
            /* Border Radius */
            --radius-sm: 8px;
            --radius-md: 12px;
            --radius-lg: 16px;
            --radius-xl: 24px;
            --radius-full: 9999px;
        }

        /* ===== RESET & BASE STYLES ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
            color: var(--dark);
            line-height: 1.6;
            min-height: 100vh;
        }

        /* ===== 3D ICON STYLES ===== */
        .icon-3d {
            position: relative;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border-radius: var(--radius-md);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            transform-style: preserve-3d;
        }

        .icon-3d::before {
            content: '';
            position: absolute;
            inset: -1px;
            border-radius: inherit;
            background: inherit;
            filter: blur(8px);
            opacity: 0.5;
            z-index: -1;
            transition: all 0.3s ease;
        }

        .icon-3d:hover {
            transform: translateY(-4px) rotateX(5deg);
        }

        .icon-3d:hover::before {
            transform: scale(1.1);
            opacity: 0.8;
        }

        .icon-3d.blue {
            background: var(--icon-3d-blue);
            color: white;
            box-shadow: var(--shadow-medium), inset 0 -2px 4px rgba(0, 0, 0, 0.1);
        }

        .icon-3d.green {
            background: var(--icon-3d-green);
            color: white;
            box-shadow: var(--shadow-medium), inset 0 -2px 4px rgba(0, 0, 0, 0.1);
        }

        .icon-3d.purple {
            background: var(--icon-3d-purple);
            color: white;
            box-shadow: var(--shadow-medium), inset 0 -2px 4px rgba(0, 0, 0, 0.1);
        }

        .icon-3d.orange {
            background: var(--icon-3d-orange);
            color: white;
            box-shadow: var(--shadow-medium), inset 0 -2px 4px rgba(0, 0, 0, 0.1);
        }

        .icon-3d.large {
            width: 80px;
            height: 80px;
            font-size: 2rem;
        }

        .icon-3d.medium {
            width: 60px;
            height: 60px;
            font-size: 1.5rem;
        }

        .icon-3d.small {
            width: 40px;
            height: 40px;
            font-size: 1rem;
        }

        /* ===== NAVBAR ===== */
        .navbar {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 1rem 2rem;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: var(--shadow-soft);
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--dark);
            text-decoration: none;
        }

        .logo-icon {
            width: 40px;
            height: 40px;
            background: var(--gradient-primary);
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.2rem;
            box-shadow: var(--shadow-medium);
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            align-items: center;
        }

        .nav-link {
            color: var(--gray);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
            position: relative;
            padding: 0.5rem 0;
        }

        .nav-link:hover {
            color: var(--primary);
        }

        .nav-link.active {
            color: var(--primary);
        }

        .nav-link.active::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--gradient-primary);
            border-radius: var(--radius-full);
        }

        /* ===== BUTTONS ===== */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            padding: 0.75rem 1.5rem;
            border-radius: var(--radius-md);
            font-weight: 600;
            font-size: 0.95rem;
            text-decoration: none;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            outline: none;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }

        .btn:hover::before {
            width: 300px;
            height: 300px;
        }

        .btn-primary {
            background: var(--gradient-primary);
            color: white;
            box-shadow: var(--shadow-medium);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-hard);
        }

        .btn-secondary {
            background: white;
            color: var(--primary);
            border: 2px solid var(--primary);
        }

        .btn-secondary:hover {
            background: var(--primary);
            color: white;
            transform: translateY(-2px);
        }

        .btn-outline {
            background: transparent;
            color: var(--dark);
            border: 2px solid var(--gray-light);
        }

        .btn-outline:hover {
            border-color: var(--primary);
            color: var(--primary);
            transform: translateY(-2px);
        }

        .btn-success {
            background: var(--gradient-success);
            color: white;
            box-shadow: var(--shadow-medium);
        }

        .btn-danger {
            background: var(--danger);
            color: white;
            box-shadow: var(--shadow-medium);
        }

        /* ===== HERO SECTION ===== */
        .hero {
            max-width: 1400px;
            margin: 6rem auto 4rem;
            padding: 2rem;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
            min-height: calc(100vh - 80px);
        }

        .hero-content {
            animation: fadeInUp 0.8s ease-out;
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

        .hero-title {
            font-size: 3.5rem;
            font-weight: 800;
            line-height: 1.1;
            margin-bottom: 1.5rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero-subtitle {
            font-size: 1.25rem;
            color: var(--gray);
            margin-bottom: 2rem;
            line-height: 1.7;
        }

        .hero-stats {
            display: flex;
            gap: 2rem;
            margin: 2.5rem 0;
        }

        .stat-item {
            text-align: center;
            flex: 1;
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
            margin-top: 0.5rem;
            font-weight: 500;
        }

        .hero-actions {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        /* ===== 3D CHART VISUALIZATION ===== */
        .chart-visualization {
            background: white;
            border-radius: var(--radius-xl);
            padding: 2rem;
            box-shadow: var(--shadow-3d);
            animation: fadeIn 0.8s ease-out 0.3s both;
            position: relative;
            overflow: hidden;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.95);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .chart-visualization::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--gradient-primary);
        }

        .chart-title {
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            color: var(--dark);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .chart-container {
            height: 300px;
            position: relative;
            margin: 1rem 0;
        }

        .chart-patterns {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
            flex-wrap: wrap;
        }

        .pattern-card {
            flex: 1;
            min-width: 200px;
            background: white;
            border-radius: var(--radius-lg);
            padding: 1.5rem;
            border: 2px solid transparent;
            transition: all 0.3s ease;
            cursor: pointer;
            text-align: center;
        }

        .pattern-card:hover {
            transform: translateY(-5px);
            border-color: var(--primary-light);
            box-shadow: var(--shadow-hard);
        }

        .pattern-card.active {
            border-color: var(--primary);
            background: linear-gradient(135deg, #f0f9ff, #e0f2fe);
        }

        .pattern-icon {
            margin-bottom: 1rem;
        }

        /* ===== CALENDAR SECTION ===== */
        .calendar-section {
            max-width: 1400px;
            margin: 4rem auto;
            padding: 2rem;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 3rem;
            color: var(--dark);
            position: relative;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 4px;
            background: var(--gradient-primary);
            border-radius: var(--radius-full);
        }

        .calendar-container {
            background: white;
            border-radius: var(--radius-xl);
            padding: 2.5rem;
            box-shadow: var(--shadow-hard);
        }

        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1.5rem;
            border-bottom: 2px solid var(--gray-light);
        }

        .calendar-nav {
            display: flex;
            gap: 0.5rem;
        }

        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
            margin-bottom: 2rem;
        }

        .calendar-day-header {
            padding: 1rem;
            text-align: center;
            font-weight: 600;
            color: var(--gray);
            text-transform: uppercase;
            font-size: 0.85rem;
            letter-spacing: 1px;
        }

        .calendar-day {
            padding: 1rem;
            text-align: center;
            border-radius: var(--radius-md);
            background: white;
            border: 2px solid transparent;
            transition: all 0.2s ease;
            cursor: pointer;
            position: relative;
            font-weight: 500;
        }

        .calendar-day:hover {
            background: #f0f9ff;
            border-color: var(--primary-light);
            transform: translateY(-2px);
        }

        .calendar-day.active {
            background: var(--gradient-primary);
            color: white;
            border-color: var(--primary);
            box-shadow: var(--shadow-medium);
        }

        .calendar-day.has-trade::after {
            content: '';
            position: absolute;
            bottom: 5px;
            left: 50%;
            transform: translateX(-50%);
            width: 6px;
            height: 6px;
            background: var(--success);
            border-radius: 50%;
        }

        .calendar-day.today {
            border: 2px solid var(--primary);
            background: #eff6ff;
        }

        .calendar-events {
            background: #f8fafc;
            border-radius: var(--radius-lg);
            padding: 1.5rem;
            margin-top: 2rem;
        }

        .event-item {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 1rem;
            background: white;
            border-radius: var(--radius-md);
            margin-bottom: 0.5rem;
            border-left: 4px solid var(--primary);
        }

        .event-time {
            font-weight: 600;
            color: var(--primary);
            min-width: 100px;
        }

        /* ===== FEATURES SECTION ===== */
        .features-section {
            max-width: 1400px;
            margin: 4rem auto;
            padding: 2rem;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .feature-card {
            background: white;
            border-radius: var(--radius-lg);
            padding: 2rem;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            position: relative;
            overflow: hidden;
        }

        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--gradient-primary);
            transform: scaleX(0);
            transition: transform 0.3s ease;
            transform-origin: left;
        }

        .feature-card:hover {
            transform: translateY(-8px);
            box-shadow: var(--shadow-hard);
        }

        .feature-card:hover::before {
            transform: scaleX(1);
        }

        .feature-icon {
            margin-bottom: 1.5rem;
        }

        .feature-title {
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--dark);
        }

        .feature-description {
            color: var(--gray);
            line-height: 1.7;
        }

        /* ===== AUTH MODAL ===== */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(5px);
            z-index: 2000;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .modal-content {
            background: white;
            border-radius: var(--radius-xl);
            width: 100%;
            max-width: 500px;
            animation: modalSlideIn 0.3s ease;
            box-shadow: var(--shadow-3d);
            overflow: hidden;
        }

        @keyframes modalSlideIn {
            from {
                opacity: 0;
                transform: translateY(-50px) scale(0.95);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }

        .modal-header {
            padding: 2rem 2rem 1rem;
            text-align: center;
        }

        .modal-title {
            font-size: 1.75rem;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 0.5rem;
        }

        .modal-subtitle {
            color: var(--gray);
            font-size: 0.95rem;
        }

        .close-modal {
            position: absolute;
            top: 1.5rem;
            right: 1.5rem;
            background: none;
            border: none;
            font-size: 1.5rem;
            color: var(--gray);
            cursor: pointer;
            transition: color 0.3s;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .close-modal:hover {
            color: var(--danger);
            background: #fef2f2;
        }

        .form-tabs {
            display: flex;
            border-bottom: 2px solid var(--gray-light);
        }

        .tab-btn {
            flex: 1;
            padding: 1.2rem;
            background: none;
            border: none;
            font-size: 1rem;
            font-weight: 600;
            color: var(--gray);
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
        }

        .tab-btn:hover {
            color: var(--primary);
            background: #f8fafc;
        }

        .tab-btn.active {
            color: var(--primary);
        }

        .tab-btn.active::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--gradient-primary);
        }

        .tab-content {
            padding: 2rem;
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--dark);
        }

        .form-input {
            width: 100%;
            padding: 0.875rem 1rem;
            border: 2px solid var(--gray-light);
            border-radius: var(--radius-md);
            font-size: 1rem;
            transition: all 0.3s;
            background: white;
        }

        .form-input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        .form-checkbox {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .demo-credentials {
            background: linear-gradient(135deg, #eff6ff, #dbeafe);
            border-radius: var(--radius-md);
            padding: 1.5rem;
            margin-bottom: 2rem;
            border-left: 4px solid var(--primary);
        }

        .demo-title {
            font-weight: 600;
            color: var(--dark);
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* ===== DASHBOARD ===== */
        .dashboard {
            max-width: 1400px;
            margin: 5rem auto 2rem;
            padding: 1rem;
            display: none;
        }

        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1.5rem;
            border-bottom: 2px solid var(--gray-light);
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .user-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--gradient-primary);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.25rem;
            font-weight: 600;
            box-shadow: var(--shadow-medium);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: white;
            border-radius: var(--radius-lg);
            padding: 1.5rem;
            display: flex;
            align-items: center;
            gap: 1rem;
            box-shadow: var(--shadow-medium);
            transition: all 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow-hard);
        }

        .stat-icon {
            flex-shrink: 0;
        }

        .stat-content {
            flex: 1;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--dark);
            line-height: 1;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
            margin-top: 0.25rem;
        }

        .dashboard-chart {
            background: white;
            border-radius: var(--radius-lg);
            padding: 2rem;
            margin-bottom: 2rem;
            box-shadow: var(--shadow-medium);
        }

        .trade-form-container {
            background: white;
            border-radius: var(--radius-lg);
            padding: 2rem;
            margin-bottom: 2rem;
            box-shadow: var(--shadow-medium);
            display: none;
        }

        .trades-table-container {
            background: white;
            border-radius: var(--radius-lg);
            padding: 2rem;
            box-shadow: var(--shadow-medium);
        }

        .table-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .table {
            width: 100%;
            border-collapse: collapse;
        }

        .table th {
            text-align: left;
            padding: 1rem;
            font-weight: 600;
            color: var(--gray);
            border-bottom: 2px solid var(--gray-light);
        }

        .table td {
            padding: 1rem;
            border-bottom: 1px solid var(--gray-light);
            vertical-align: middle;
        }

        .table tr:hover {
            background: #f8fafc;
        }

        .profit-positive {
            color: var(--success);
            font-weight: 600;
        }

        .profit-negative {
            color: var(--danger);
            font-weight: 600;
        }

        .badge {
            padding: 0.25rem 0.75rem;
            border-radius: var(--radius-full);
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .badge-success {
            background: #d1fae5;
            color: var(--success);
        }

        .badge-danger {
            background: #fee2e2;
            color: var(--danger);
        }

        .badge-primary {
            background: #dbeafe;
            color: var(--primary);
        }

        .action-buttons {
            display: flex;
            gap: 0.5rem;
        }

        /* ===== RESPONSIVE DESIGN ===== */
        @media (max-width: 1200px) {
            .hero {
                grid-template-columns: 1fr;
                gap: 3rem;
                text-align: center;
            }
            
            .hero-stats {
                justify-content: center;
            }
        }

        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            .hero-title {
                font-size: 2.5rem;
            }
            
            .hero-stats {
                flex-direction: column;
                gap: 1.5rem;
            }
            
            .calendar-grid {
                gap: 5px;
            }
            
            .calendar-day {
                padding: 0.75rem 0.5rem;
                font-size: 0.9rem;
            }
            
            .features-grid {
                grid-template-columns: 1fr;
            }
            
            .modal-content {
                margin: 1rem;
            }
        }

        /* ===== UTILITY CLASSES ===== */
        .text-center {
            text-align: center;
        }

        .mb-1 { margin-bottom: 0.5rem; }
        .mb-2 { margin-bottom: 1rem; }
        .mb-3 { margin-bottom: 1.5rem; }
        .mb-4 { margin-bottom: 2rem; }
        .mt-1 { margin-top: 0.5rem; }
        .mt-2 { margin-top: 1rem; }
        .mt-3 { margin-top: 1.5rem; }
        .mt-4 { margin-top: 2rem; }

        .grid {
            display: grid;
            gap: 1rem;
        }

        .grid-2 {
            grid-template-columns: repeat(2, 1fr);
        }

        .grid-3 {
            grid-template-columns: repeat(3, 1fr);
        }

        .flex {
            display: flex;
        }

        .items-center {
            align-items: center;
        }

        .justify-between {
            justify-content: space-between;
        }

        .gap-1 { gap: 0.5rem; }
        .gap-2 { gap: 1rem; }
        .gap-3 { gap: 1.5rem; }
        .gap-4 { gap: 2rem; }
    </style>
</head>
<body>
    <!-- ===== NAVBAR ===== -->
    <nav class="navbar">
        <div class="nav-container">
            <a href="#" class="logo">
                <div class="logo-icon">
                    <i class="fas fa-chart-line"></i>
                </div>
                <span>TradeLog Pro</span>
            </a>
            
            <div class="nav-links">
                <a href="#features" class="nav-link">Features</a>
                <a href="#calendar" class="nav-link">Calendar</a>
                <a href="#patterns" class="nav-link">Chart Patterns</a>
                <a href="#pricing" class="nav-link">Pricing</a>
                <button class="btn btn-primary" onclick="showAuthModal('login')">
                    <i class="fas fa-sign-in-alt"></i> Login
                </button>
            </div>
        </div>
    </nav>

    <!-- ===== HERO SECTION ===== -->
    <section class="hero">
        <div class="hero-content">
            <h1 class="hero-title">Master Your Trading with Professional Insights</h1>
            <p class="hero-subtitle">
                India's most advanced AI-powered trading journal. Track, analyze, and optimize your 
                trading performance with cutting-edge technology and actionable insights.
            </p>
            
            <div class="hero-stats">
                <div class="stat-item">
                    <div class="stat-number" id="liveTrades">15,842</div>
                    <div class="stat-label">Live Trades Tracked</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number">87.5%</div>
                    <div class="stat-label">Average Accuracy</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number">₹4.2M</div>
                    <div class="stat-label">Profits Analyzed</div>
                </div>
            </div>
            
            <div class="hero-actions">
                <button class="btn btn-primary" onclick="showAuthModal('signup')">
                    <i class="fas fa-rocket"></i> Start Free Trial
                </button>
                <button class="btn btn-outline" onclick="scrollToFeatures()">
                    <i class="fas fa-play-circle"></i> Watch Demo
                </button>
                <button class="btn btn-secondary" onclick="scrollToCalendar()">
                    <i class="fas fa-calendar-alt"></i> View Calendar
                </button>
            </div>
        </div>
        
        <div class="chart-visualization">
            <div class="chart-title">
                <div class="icon-3d blue medium">
                    <i class="fas fa-chart-bar"></i>
                </div>
                Live Chart Patterns
            </div>
            
            <div class="chart-container">
                <canvas id="mainChart"></canvas>
            </div>
            
            <div class="chart-patterns">
                <div class="pattern-card active" onclick="changeChartPattern('head_shoulders')">
                    <div class="pattern-icon icon-3d purple small">
                        <i class="fas fa-mountain"></i>
                    </div>
                    <div class="font-weight-600">Head & Shoulders</div>
                    <div class="text-small text-gray">Reversal Pattern</div>
                </div>
                
                <div class="pattern-card" onclick="changeChartPattern('double_top')">
                    <div class="pattern-icon icon-3d orange small">
                        <i class="fas fa-chart-area"></i>
                    </div>
                    <div class="font-weight-600">Double Top</div>
                    <div class="text-small text-gray">Bearish Reversal</div>
                </div>
                
                <div class="pattern-card" onclick="changeChartPattern('triangle')">
                    <div class="pattern-icon icon-3d green small">
                        <i class="fas fa-expand-alt"></i>
                    </div>
                    <div class="font-weight-600">Triangle</div>
                    <div class="text-small text-gray">Continuation</div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== CALENDAR SECTION ===== -->
    <section id="calendar" class="calendar-section">
        <h2 class="section-title">Trading Calendar</h2>
        
        <div class="calendar-container">
            <div class="calendar-header">
                <h3 id="currentMonth">October 2023</h3>
                <div class="calendar-nav">
                    <button class="btn btn-outline btn-small" onclick="changeMonth(-1)">
                        <i class="fas fa-chevron-left"></i>
                    </button>
                    <button class="btn btn-primary btn-small" onclick="goToToday()">
                        Today
                    </button>
                    <button class="btn btn-outline btn-small" onclick="changeMonth(1)">
                        <i class="fas fa-chevron-right"></i>
                    </button>
                </div>
            </div>
            
            <div class="calendar-grid">
                <div class="calendar-day-header">Sun</div>
                <div class="calendar-day-header">Mon</div>
                <div class="calendar-day-header">Tue</div>
                <div class="calendar-day-header">Wed</div>
                <div class="calendar-day-header">Thu</div>
                <div class="calendar-day-header">Fri</div>
                <div class="calendar-day-header">Sat</div>
                
                <div id="calendarDays">
                    <!-- Calendar days will be populated here -->
                </div>
            </div>
            
            <div class="calendar-events">
                <h4 class="mb-3">
                    <div class="icon-3d green small">
                        <i class="fas fa-bell"></i>
                    </div>
                    Today's Market Events
                </h4>
                
                <div class="event-item">
                    <div class="event-time">9:15 AM</div>
                    <div class="event-details">
                        <div class="font-weight-600">NSE/BSE Market Open</div>
                        <div class="text-small text-gray">Indian Stock Markets</div>
                    </div>
                </div>
                
                <div class="event-item">
                    <div class="event-time">10:30 AM</div>
                    <div class="event-details">
                        <div class="font-weight-600">Reliance Industries Results</div>
                        <div class="text-small text-gray">Q2 2023 Earnings Report</div>
                    </div>
                </div>
                
                <div class="event-item">
                    <div class="event-time">3:30 PM</div>
                    <div class="event-details">
                        <div class="font-weight-600">NSE/BSE Market Close</div>
                        <div class="text-small text-gray">Indian Stock Markets</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== FEATURES SECTION ===== -->
    <section id="features" class="features-section">
        <h2 class="section-title">Powerful Features</h2>
        
        <div class="features-grid">
            <div class="feature-card">
                <div class="feature-icon icon-3d blue large">
                    <i class="fas fa-brain"></i>
                </div>
                <h3 class="feature-title">AI Pattern Recognition</h3>
                <p class="feature-description">
                    Advanced AI algorithms identify chart patterns and predict market movements 
                    with 85% accuracy rate.
                </p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon icon-3d green large">
                    <i class="fas fa-calendar-alt"></i>
                </div>
                <h3 class="feature-title">Smart Trading Calendar</h3>
                <p class="feature-description">
                    Never miss important trading events, earnings reports, or economic 
                    announcements with our smart calendar.
                </p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon icon-3d purple large">
                    <i class="fas fa-chart-network"></i>
                </div>
                <h3 class="feature-title">3D Chart Visualization</h3>
                <p class="feature-description">
                    Visualize complex chart patterns in 3D for better understanding and 
                    improved decision making.
                </p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon icon-3d orange large">
                    <i class="fas fa-robot"></i>
                </div>
                <h3 class="feature-title">Automated Journaling</h3>
                <p class="feature-description">
                    Auto-log trades from your broker and get instant AI-powered performance 
                    analysis and insights.
                </p>
            </div>
        </div>
    </section>

    <!-- ===== DASHBOARD ===== -->
    <div id="dashboard" class="dashboard">
        <div class="dashboard-header">
            <div>
                <h1 style="font-size: 2rem; font-weight: 700; color: var(--dark);">
                    <div class="icon-3d blue medium">
                        <i class="fas fa-tachometer-alt"></i>
                    </div>
                    Trading Dashboard
                </h1>
                <p id="dashboardDate" style="color: var(--gray); margin-top: 0.5rem;">
                    <i class="fas fa-calendar"></i> <span id="currentDate"></span>
                </p>
            </div>
            
            <div class="user-info">
                <div class="user-avatar" id="userAvatar">
                    <i class="fas fa-user"></i>
                </div>
                <div>
                    <div id="welcomeUser" style="font-weight: 600;">Welcome, Trader</div>
                    <button class="btn btn-outline btn-small" onclick="logout()">
                        <i class="fas fa-sign-out-alt"></i> Logout
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Stats Cards -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-icon icon-3d blue medium">
                    <i class="fas fa-exchange-alt"></i>
                </div>
                <div class="stat-content">
                    <div class="stat-value" id="totalTrades">0</div>
                    <div class="stat-label">Total Trades</div>
                </div>
            </div>
            
            <div class="stat-card">
                <div class="stat-icon icon-3d green medium">
                    <i class="fas fa-trophy"></i>
                </div>
                <div class="stat-content">
                    <div class="stat-value" id="winRate">0%</div>
                    <div class="stat-label">Win Rate</div>
                </div>
            </div>
            
            <div class="stat-card">
                <div class="stat-icon icon-3d orange medium">
                    <i class="fas fa-rupee-sign"></i>
                </div>
                <div class="stat-content">
                    <div class="stat-value" id="totalProfit">₹0</div>
                    <div class="stat-label">Total Profit</div>
                </div>
            </div>
            
            <div class="stat-card">
                <div class="stat-icon icon-3d purple medium">
                    <i class="fas fa-chart-line"></i>
                </div>
                <div class="stat-content">
                    <div class="stat-value" id="avgProfit">₹0</div>
                    <div class="stat-label">Avg. Profit/Trade</div>
                </div>
            </div>
        </div>
        
        <!-- Chart -->
        <div class="dashboard-chart">
            <h3 style="margin-bottom: 1.5rem; color: var(--dark);">
                <i class="fas fa-chart-bar"></i> Performance Analytics
            </h3>
            <canvas id="performanceChart" height="100"></canvas>
        </div>
        
        <!-- Trade Form -->
        <div class="trade-form-container" id="tradeForm">
            <h3 style="margin-bottom: 1.5rem; color: var(--dark);">
                <i class="fas fa-plus-circle"></i> Log New Trade
            </h3>
            
            <form id="tradeFormElement">
                <div class="grid grid-2 gap-3 mb-3">
                    <div class="form-group">
                        <label class="form-label">Symbol/Asset</label>
                        <input type="text" class="form-input" id="tradeSymbol" placeholder="RELIANCE, BTCUSD..." required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Trade Type</label>
                        <select class="form-input" id="tradeType" required>
                            <option value="BUY">Buy/Long</option>
                            <option value="SELL">Sell/Short</option>
                        </select>
                    </div>
                </div>
                
                <div class="grid grid-2 gap-3 mb-3">
                    <div class="form-group">
                        <label class="form-label">Entry Price (₹)</label>
                        <input type="number" class="form-input" id="entryPrice" step="0.01" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Exit Price (₹)</label>
                        <input type="number" class="form-input" id="exitPrice" step="0.01" required>
                    </div>
                </div>
                
                <div class="grid grid-2 gap-3 mb-3">
                    <div class="form-group">
                        <label class="form-label">Quantity</label>
                        <input type="number" class="form-input" id="quantity" step="0.01" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Strategy</label>
                        <select class="form-input" id="strategy">
                            <option value="Breakout">Breakout Trading</option>
                            <option value="Pullback">Pullback Trading</option>
                            <option value="Trend">Trend Following</option>
                            <option value="Scalping">Scalping</option>
                        </select>
                    </div>
                </div>
                
                <div class="form-group mb-3">
                    <label class="form-label">Trade Notes</label>
                    <textarea class="form-input" id="tradeNotes" rows="3" placeholder="What was your reasoning? Key learning points..."></textarea>
                </div>
                
                <div class="flex gap-2">
                    <button type="submit" class="btn btn-success">
                        <i class="fas fa-save"></i> Save Trade
                    </button>
                    <button type="button" class="btn btn-outline" onclick="hideTradeForm()">
                        <i class="fas fa-times"></i> Cancel
                    </button>
                </div>
            </form>
        </div>
        
        <!-- Trades Table -->
        <div class="trades-table-container">
            <div class="table-header">
                <h3 style="color: var(--dark);">
                    <i class="fas fa-history"></i> Trade History
                </h3>
                
                <div class="flex gap-2">
                    <button class="btn btn-primary" onclick="showTradeForm()">
                        <i class="fas fa-plus"></i> Add Trade
                    </button>
                    <button class="btn btn-outline" onclick="exportTrades()">
                        <i class="fas fa-download"></i> Export
                    </button>
                </div>
            </div>
            
            <table class="table">
                <thead>
                    <tr>
                        <th>Date</th>
                        <th>Symbol</th>
                        <th>Type</th>
                        <th>Entry</th>
                        <th>Exit</th>
                        <th>Quantity</th>
                        <th>P&L</th>
                        <th>Strategy</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="tradesList">
                    <!-- Trades will be populated here -->
                </tbody>
            </table>
        </div>
    </div>

    <!-- ===== AUTH MODAL ===== -->
    <div id="authModal" class="modal">
        <div class="modal-content">
            <button class="close-modal" onclick="hideAuthModal()">
                <i class="fas fa-times"></i>
            </button>
            
            <div class="modal-header">
                <h2 class="modal-title">Welcome to TradeLog Pro</h2>
                <p class="modal-subtitle">Sign in to access your trading dashboard</p>
            </div>
            
            <div class="form-tabs">
                <button class="tab-btn active" onclick="switchTab('login')">
                    <i class="fas fa-sign-in-alt"></i> Login
                </button>
                <button class="tab-btn" onclick="switchTab('signup')">
                    <i class="fas fa-user-plus"></i> Sign Up
                </button>
            </div>
            
            <!-- Login Form -->
            <div id="loginTab" class="tab-content active">
                <div class="demo-credentials">
                    <div class="demo-title">
                        <i class="fas fa-key"></i> Demo Account
                    </div>
                    <p><strong>Email:</strong> demo@trader.com</p>
                    <p><strong>Password:</strong> demo123</p>
                </div>
                
                <form id="loginForm">
                    <div class="form-group">
                        <label class="form-label">Email Address</label>
                        <input type="email" class="form-input" id="loginEmail" placeholder="Enter your email" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Password</label>
                        <input type="password" class="form-input" id="loginPassword" placeholder="Enter your password" required>
                    </div>
                    
                    <button type="submit" class="btn btn-primary" style="width: 100%;">
                        <i class="fas fa-sign-in-alt"></i> Login to Dashboard
                    </button>
                </form>
                
                <p class="text-center mt-3" style="color: var(--gray);">
                    Don't have an account? 
                    <a href="javascript:void(0)" onclick="switchTab('signup')" style="color: var(--primary); text-decoration: none;">
                        Sign up here
                    </a>
                </p>
            </div>
            
            <!-- Signup Form -->
            <div id="signupTab" class="tab-content">
                <form id="signupForm">
                    <div class="form-group">
                        <label class="form-label">Full Name</label>
                        <input type="text" class="form-input" id="signupName" placeholder="Enter your full name" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Email Address</label>
                        <input type="email" class="form-input" id="signupEmail" placeholder="Enter your email" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Password</label>
                        <input type="password" class="form-input" id="signupPassword" placeholder="Create a password" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Confirm Password</label>
                        <input type="password" class="form-input" id="signupConfirmPassword" placeholder="Confirm your password" required>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Trading Experience</label>
                        <select class="form-input" id="tradingExperience">
                            <option value="beginner">Beginner (0-1 year)</option>
                            <option value="intermediate">Intermediate (1-3 years)</option>
                            <option value="advanced">Advanced (3+ years)</option>
                            <option value="professional">Professional</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-checkbox">
                            <input type="checkbox" id="terms" required>
                            <span>I agree to the Terms & Conditions and Privacy Policy</span>
                        </label>
                    </div>
                    
                    <button type="submit" class="btn btn-primary" style="width: 100%;">
                        <i class="fas fa-user-plus"></i> Create Free Account
                    </button>
                </form>
                
                <p class="text-center mt-3" style="color: var(--gray);">
                    Already have an account? 
                    <a href="javascript:void(0)" onclick="switchTab('login')" style="color: var(--primary); text-decoration: none;">
                        Login here
                    </a>
                </p>
            </div>
        </div>
    </div>

    <!-- ===== JAVASCRIPT ===== -->
    <script>
        // ===== GLOBAL STATE =====
        let currentUser = null;
        let trades = [];
        let editingTradeId = null;
        let currentMonth = new Date().getMonth();
        let currentYear = new Date().getFullYear();
        let mainChart = null;
        let performanceChart = null;

        // ===== DATABASE SIMULATION =====
        class Database {
            constructor() {
                // Initialize with demo data
                if (!localStorage.getItem('trades')) {
                    const demoData = [
                        {
                            id: 1,
                            symbol: 'RELIANCE',
                            tradeType: 'BUY',
                            entryPrice: 2450,
                            exitPrice: 2500,
                            quantity: 10,
                            strategy: 'Breakout',
                            notes: 'Breakout above resistance with strong volume',
                            createdAt: '2023-10-15T10:30:00Z',
                            userId: 'demo'
                        },
                        {
                            id: 2,
                            symbol: 'TCS',
                            tradeType: 'SELL',
                            entryPrice: 3550,
                            exitPrice: 3500,
                            quantity: 5,
                            strategy: 'Pullback',
                            notes: 'Pullback to resistance level',
                            createdAt: '2023-10-14T14:20:00Z',
                            userId: 'demo'
                        },
                        {
                            id: 3,
                            symbol: 'BTCUSD',
                            tradeType: 'BUY',
                            entryPrice: 28000,
                            exitPrice: 28500,
                            quantity: 0.5,
                            strategy: 'Trend Following',
                            notes: 'Trend continuation pattern identified',
                            createdAt: '2023-10-13T09:15:00Z',
                            userId: 'demo'
                        }
                    ];
                    localStorage.setItem('trades', JSON.stringify(demoData));
                }
                
                if (!localStorage.getItem('users')) {
                    const users = [
                        {
                            id: 'demo',
                            email: 'demo@trader.com',
                            password: 'demo123',
                            name: 'Demo Trader',
                            experience: 'advanced',
                            joinDate: '2023-01-15'
                        }
                    ];
                    localStorage.setItem('users', JSON.stringify(users));
                }
            }

            findUser(email, password) {
                const users = JSON.parse(localStorage.getItem('users') || '[]');
                return users.find(user => user.email === email && user.password === password);
            }

            addUser(user) {
                const users = JSON.parse(localStorage.getItem('users') || '[]');
                user.id = 'user_' + Date.now();
                user.joinDate = new Date().toISOString();
                users.push(user);
                localStorage.setItem('users', JSON.stringify(users));
                return user;
            }

            getTrades(userId) {
                const allTrades = JSON.parse(localStorage.getItem('trades') || '[]');
                return allTrades.filter(trade => trade.userId === userId);
            }

            saveTrade(trade) {
                const trades = JSON.parse(localStorage.getItem('trades') || '[]');
                if (trade.id) {
                    const index = trades.findIndex(t => t.id === trade.id);
                    if (index !== -1) {
                        trades[index] = trade;
                    }
                } else {
                    trade.id = Date.now();
                    trade.createdAt = new Date().toISOString();
                    trade.userId = currentUser.id;
                    trades.unshift(trade);
                }
                localStorage.setItem('trades', JSON.stringify(trades));
                return trade;
            }

            deleteTrade(tradeId) {
                const trades = JSON.parse(localStorage.getItem('trades') || '[]');
                const filteredTrades = trades.filter(trade => trade.id !== tradeId);
                localStorage.setItem('trades', JSON.stringify(filteredTrades));
                return true;
            }
        }

        const db = new Database();

        // ===== CHART INITIALIZATION =====
        function initializeCharts() {
            // Main Chart
            const ctx1 = document.getElementById('mainChart').getContext('2d');
            mainChart = new Chart(ctx1, {
                type: 'line',
                data: {
                    labels: ['Day 1', 'Day 2', 'Day 3', 'Day 4', 'Day 5', 'Day 6', 'Day 7'],
                    datasets: [{
                        label: 'Stock Price',
                        data: [2450, 2500, 2475, 2550, 2525, 2600, 2575],
                        borderColor: '#3b82f6',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: false,
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        },
                        x: {
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        }
                    }
                }
            });

            // Performance Chart
            const ctx2 = document.getElementById('performanceChart').getContext('2d');
            performanceChart = new Chart(ctx2, {
                type: 'bar',
                data: {
                    labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
                    datasets: [{
                        label: 'Profit/Loss',
                        data: [1200, 1800, -800, 2500, 1500, 2200, 1900],
                        backgroundColor: [
                            '#10b981', '#10b981', '#ef4444', '#10b981', 
                            '#10b981', '#10b981', '#10b981'
                        ],
                        borderColor: 'white',
                        borderWidth: 2,
                        borderRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        },
                        x: {
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        }
                    }
                }
            });
        }

        function changeChartPattern(pattern) {
            // Update active pattern card
            document.querySelectorAll('.pattern-card').forEach(card => {
                card.classList.remove('active');
            });
            event.currentTarget.classList.add('active');

            // Update chart data based on pattern
            const patterns = {
                head_shoulders: [2450, 2600, 2450, 2550, 2450],
                double_top: [2400, 2550, 2450, 2550, 2400],
                triangle: [2450, 2500, 2475, 2525, 2500]
            };

            if (patterns[pattern]) {
                mainChart.data.datasets[0].data = patterns[pattern];
                mainChart.update();
            }
        }

        // ===== CALENDAR FUNCTIONS =====
        function generateCalendar(month, year) {
            const monthNames = [
                'January', 'February', 'March', 'April', 'May', 'June',
                'July', 'August', 'September', 'October', 'November', 'December'
            ];
            
            document.getElementById('currentMonth').textContent = 
                `${monthNames[month]} ${year}`;
            
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            const daysInMonth = lastDay.getDate();
            const startingDay = firstDay.getDay();
            
            const calendarGrid = document.getElementById('calendarDays');
            calendarGrid.innerHTML = '';
            
            // Add empty cells for days before the first day of the month
            for (let i = 0; i < startingDay; i++) {
                const emptyCell = document.createElement('div');
                emptyCell.className = 'calendar-day';
                emptyCell.style.opacity = '0.3';
                calendarGrid.appendChild(emptyCell);
            }
            
            // Add days of the month
            const today = new Date();
            for (let day = 1; day <= daysInMonth; day++) {
                const dayElement = document.createElement('div');
                dayElement.className = 'calendar-day';
                dayElement.textContent = day;
                
                // Check if today
                if (day === today.getDate() && 
                    month === today.getMonth() && 
                    year === today.getFullYear()) {
                    dayElement.classList.add('today');
                }
                
                // Add random trades for demo
                if (Math.random() > 0.7) {
                    dayElement.classList.add('has-trade');
                }
                
                // Add click event
                dayElement.onclick = () => selectDay(day, month, year);
                
                calendarGrid.appendChild(dayElement);
            }
        }

        function changeMonth(direction) {
            if (direction === 0) {
                currentMonth = new Date().getMonth();
                currentYear = new Date().getFullYear();
            } else {
                currentMonth += direction;
                if (currentMonth < 0) {
                    currentMonth = 11;
                    currentYear--;
                } else if (currentMonth > 11) {
                    currentMonth = 0;
                    currentYear++;
                }
            }
            generateCalendar(currentMonth, currentYear);
        }

        function goToToday() {
            changeMonth(0);
        }

        function selectDay(day, month, year) {
            const date = new Date(year, month, day);
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            alert(`Selected: ${date.toLocaleDateString('en-US', options)}`);
        }

        function scrollToCalendar() {
            document.getElementById('calendar').scrollIntoView({ 
                behavior: 'smooth',
                block: 'start'
            });
        }

        function scrollToFeatures() {
            document.getElementById('features').scrollIntoView({ 
                behavior: 'smooth',
                block: 'start'
            });
        }

        // ===== AUTHENTICATION =====
        function showAuthModal(tab = 'login') {
            document.getElementById('authModal').style.display = 'flex';
            switchTab(tab);
        }

        function hideAuthModal() {
            document.getElementById('authModal').style.display = 'none';
        }

        function switchTab(tab) {
            // Update tab buttons
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show/hide tab content
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            if (tab === 'login') {
                document.querySelector('.tab-btn[onclick*="login"]').classList.add('active');
                document.getElementById('loginTab').classList.add('active');
            } else {
                document.querySelector('.tab-btn[onclick*="signup"]').classList.add('active');
                document.getElementById('signupTab').classList.add('active');
            }
        }

        // ===== DASHBOARD FUNCTIONS =====
        function showDashboard() {
            document.getElementById('dashboard').style.display = 'block';
            document.querySelector('.hero').style.display = 'none';
            document.querySelector('.calendar-section').style.display = 'none';
            document.querySelector('.features-section').style.display = 'none';
            loadDashboard();
        }

        function hideDashboard() {
            document.getElementById('dashboard').style.display = 'none';
            document.querySelector('.hero').style.display = 'grid';
            document.querySelector('.calendar-section').style.display = 'block';
            document.querySelector('.features-section').style.display = 'block';
        }

        function showTradeForm() {
            document.getElementById('tradeForm').style.display = 'block';
            editingTradeId = null;
            document.getElementById('tradeFormElement').reset();
            document.getElementById('tradeSymbol').focus();
        }

        function hideTradeForm() {
            document.getElementById('tradeForm').style.display = 'none';
            editingTradeId = null;
            document.getElementById('tradeFormElement').reset();
        }

        function calculateProfit(trade) {
            const entry = parseFloat(trade.entryPrice);
            const exit = parseFloat(trade.exitPrice);
            const quantity = parseFloat(trade.quantity);
            
            if (trade.tradeType === 'BUY') {
                return (exit - entry) * quantity;
            } else {
                return (entry - exit) * quantity;
            }
        }

        function loadDashboard() {
            if (!currentUser) return;
            
            // Load user trades
            trades = db.getTrades(currentUser.id);
            
            // Update user info
            document.getElementById('welcomeUser').textContent = 
                `Welcome, ${currentUser.name || currentUser.email}`;
            
            // Update avatar
            const avatar = document.getElementById('userAvatar');
            const initials = currentUser.name ? currentUser.name.charAt(0).toUpperCase() : 'T';
            avatar.innerHTML = initials;
            
            // Update date
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            document.getElementById('currentDate').textContent = 
                now.toLocaleDateString('en-US', options);
            
            // Update stats
            updateDashboardStats();
            
            // Render trades
            renderTrades();
        }

        function updateDashboardStats() {
            const totalTrades = trades.length;
            const winningTrades = trades.filter(t => calculateProfit(t) > 0).length;
            const winRate = totalTrades > 0 ? (winningTrades / totalTrades * 100).toFixed(1) : 0;
            const totalProfit = trades.reduce((sum, t) => sum + calculateProfit(t), 0);
            const avgProfit = totalTrades > 0 ? (totalProfit / totalTrades).toFixed(2) : 0;
            
            document.getElementById('totalTrades').textContent = totalTrades;
            document.getElementById('winRate').textContent = `${winRate}%`;
            document.getElementById('totalProfit').textContent = `₹${totalProfit.toFixed(2)}`;
            document.getElementById('avgProfit').textContent = `₹${avgProfit}`;
            
            // Update live trades count
            document.getElementById('liveTrades').textContent = 
                (parseInt(totalTrades) + 15842).toLocaleString();
        }

        function renderTrades() {
            const tradesList = document.getElementById('tradesList');
            if (!tradesList) return;
            
            tradesList.innerHTML = '';
            
            trades.forEach(trade => {
                const profit = calculateProfit(trade);
                const profitClass = profit >= 0 ? 'profit-positive' : 'profit-negative';
                const profitText = profit >= 0 ? 
                    `+₹${profit.toFixed(2)}` : 
                    `-₹${Math.abs(profit).toFixed(2)}`;
                
                const date = new Date(trade.createdAt);
                const formattedDate = `${date.getDate().toString().padStart(2, '0')}/${(date.getMonth() + 1).toString().padStart(2, '0')}`;
                
                const typeBadge = trade.tradeType === 'BUY' ? 
                    '<span class="badge badge-success">BUY</span>' : 
                    '<span class="badge badge-danger">SELL</span>';
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${formattedDate}</td>
                    <td><strong>${trade.symbol || 'N/A'}</strong></td>
                    <td>${typeBadge}</td>
                    <td>₹${trade.entryPrice || '0'}</td>
                    <td>₹${trade.exitPrice || '0'}</td>
                    <td>${trade.quantity || '0'}</td>
                    <td class="${profitClass}">${profitText}</td>
                    <td><span class="badge badge-primary">${trade.strategy || 'N/A'}</span></td>
                    <td>
                        <div class="action-buttons">
                            <button class="btn btn-outline btn-small" onclick="editTrade(${trade.id})">
                                <i class="fas fa-edit"></i>
                            </button>
                            <button class="btn btn-outline btn-small" onclick="deleteTrade(${trade.id})">
                                <i class="fas fa-trash"></i>
                            </button>
                        </div>
                    </td>
                `;
                tradesList.appendChild(row);
            });
        }

        function editTrade(tradeId) {
            const trade = trades.find(t => t.id === tradeId);
            if (trade) {
                editingTradeId = tradeId;
                
                document.getElementById('tradeSymbol').value = trade.symbol || '';
                document.getElementById('tradeType').value = trade.tradeType || 'BUY';
                document.getElementById('entryPrice').value = trade.entryPrice || '';
                document.getElementById('exitPrice').value = trade.exitPrice || '';
                document.getElementById('quantity').value = trade.quantity || '';
                document.getElementById('strategy').value = trade.strategy || 'Breakout';
                document.getElementById('tradeNotes').value = trade.notes || '';
                
                showTradeForm();
            }
        }

        function deleteTrade(tradeId) {
            if (!confirm('Are you sure you want to delete this trade?')) return;
            
            if (db.deleteTrade(tradeId)) {
                trades = trades.filter(t => t.id !== tradeId);
                renderTrades();
                updateDashboardStats();
            }
        }

        function exportTrades() {
            const csvContent = "data:text/csv;charset=utf-8," +
                ["Date,Symbol,Type,Entry,Exit,Quantity,Profit,Strategy"].concat(
                    trades.map(trade => {
                        const profit = calculateProfit(trade);
                        const date = new Date(trade.createdAt).toLocaleDateString();
                        return `${date},${trade.symbol},${trade.tradeType},${trade.entryPrice},${trade.exitPrice},${trade.quantity},${profit},${trade.strategy}`;
                    })
                ).join("\n");
            
            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "trades_export.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function logout() {
            currentUser = null;
            trades = [];
            editingTradeId = null;
            hideDashboard();
            hideTradeForm();
            localStorage.removeItem('currentUser');
            switchTab('login');
        }

        // ===== EVENT LISTENERS =====
        document.addEventListener('DOMContentLoaded', function() {
            // Initialize charts
            initializeCharts();
            
            // Initialize calendar
            generateCalendar(currentMonth, currentYear);
            
            // Check saved user
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                showDashboard();
            }
            
            // Login form
            document.getElementById('loginForm').addEventListener('submit', function(e) {
                e.preventDefault();
                
                const email = document.getElementById('loginEmail').value;
                const password = document.getElementById('loginPassword').value;
                
                const user = db.findUser(email, password);
                
                if (user) {
                    currentUser = user;
                    localStorage.setItem('currentUser', JSON.stringify(user));
                    hideAuthModal();
                    showDashboard();
                } else {
                    alert('Invalid credentials. Use demo@trader.com / demo123');
                }
            });
            
            // Signup form
            document.getElementById('signupForm').addEventListener('submit', function(e) {
                e.preventDefault();
                
                const name = document.getElementById('signupName').value;
                const email = document.getElementById('signupEmail').value;
                const password = document.getElementById('signupPassword').value;
                const confirmPassword = document.getElementById('signupConfirmPassword').value;
                const experience = document.getElementById('tradingExperience').value;
                
                if (password !== confirmPassword) {
                    alert('Passwords do not match!');
                    return;
                }
                
                const user = {
                    name,
                    email,
                    password,
                    experience
                };
                
                const newUser = db.addUser(user);
                currentUser = newUser;
                localStorage.setItem('currentUser', JSON.stringify(newUser));
                
                alert('Account created successfully! Welcome to TradeLog Pro.');
                hideAuthModal();
                showDashboard();
            });
            
            // Trade form
            document.getElementById('tradeFormElement').addEventListener('submit', function(e) {
                e.preventDefault();
                
                const tradeData = {
                    id: editingTradeId,
                    symbol: document.getElementById('tradeSymbol').value,
                    tradeType: document.getElementById('tradeType').value,
                    entryPrice: parseFloat(document.getElementById('entryPrice').value),
                    exitPrice: parseFloat(document.getElementById('exitPrice').value),
                    quantity: parseFloat(document.getElementById('quantity').value),
                    strategy: document.getElementById('strategy').value,
                    notes: document.getElementById('tradeNotes').value
                };
                
                const savedTrade = db.saveTrade(tradeData);
                
                if (savedTrade) {
                    hideTradeForm();
                    loadDashboard();
                }
            });
            
            // Close modal on outside click
            window.addEventListener('click', function(event) {
                const modal = document.getElementById('authModal');
                if (event.target === modal) {
                    hideAuthModal();
                }
            });
        });

        // Auto-update live trades counter
        setInterval(() => {
            const current = parseInt(document.getElementById('liveTrades').textContent.replace(',', ''));
            const increment = Math.floor(Math.random() * 5) + 1;
            document.getElementById('liveTrades').textContent = (current + increment).toLocaleString();
        }, 3000);

        // Add smooth scrolling for navigation
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>
