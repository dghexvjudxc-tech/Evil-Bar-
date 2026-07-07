<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>☕ كافيه مصطفى - المنصة المتكاملة</title>
    <style>
        :root {
            --gold: #d4a853;
            --gold-light: #f0d78c;
            --gold-dark: #b8922e;
            --bg-primary: #0a0a0a;
            --bg-secondary: #111111;
            --bg-card: #1a1a1a;
            --bg-input: #1e1e1e;
            --text-primary: #f0e6d2;
            --text-secondary: #a89070;
            --text-muted: #6b5b4a;
            --border: #2a2a2a;
            --border-gold: rgba(212, 168, 83, 0.3);
            --red: #ff4757;
            --green: #2ed573;
            --blue: #5352ed;
            --purple: #a55eea;
            --orange: #ffa502;
            --pink: #ff6b81;
            --shadow-sm: 0 4px 15px rgba(0, 0, 0, 0.3);
            --shadow-md: 0 8px 30px rgba(0, 0, 0, 0.5);
            --shadow-lg: 0 15px 50px rgba(0, 0, 0, 0.6);
            --shadow-gold: 0 10px 40px rgba(212, 168, 83, 0.2);
            --radius-sm: 10px;
            --radius: 20px;
            --radius-lg: 28px;
            --transition: all 0.35s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            overflow-x: hidden;
            scroll-behavior: smooth;
            -webkit-tap-highlight-color: transparent;
            cursor: default;
        }

        /* ============ مؤشر مخصص ============ */
        .custom-cursor {
            width: 32px;
            height: 32px;
            border: 2px solid var(--gold);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 99999;
            transition: all 0.12s ease-out;
            mix-blend-mode: difference;
        }
        .cursor-inner {
            width: 7px;
            height: 7px;
            background: var(--gold-light);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 99999;
            transition: all 0.04s ease-out;
        }
        .custom-cursor.hover {
            width: 55px;
            height: 55px;
            border-color: var(--gold-light);
            background: rgba(212, 168, 83, 0.1);
        }
        .custom-cursor.click {
            transform: scale(0.7);
        }

        /* ============ جسيمات الخلفية ============ */
        #particlesCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        /* ============ شاشة التحميل الأولية ============ */
        #initialLoader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 100000;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: all 0.8s cubic-bezier(0.77, 0, 0.175, 1);
        }
        #initialLoader.hidden {
            opacity: 0;
            pointer-events: none;
            transform: scale(1.3);
        }
        #initialLoader .loader-coffee {
            font-size: 6em;
            animation: loaderBounce 0.8s ease-in-out infinite alternate;
        }
        @keyframes loaderBounce {
            from {
                transform: translateY(0) rotate(-5deg);
            }
            to {
                transform: translateY(-30px) rotate(5deg);
            }
        }
        #initialLoader .loader-title {
            font-size: 2.8em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), #fff, var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-top: 20px;
            letter-spacing: 6px;
            animation: loaderGlow 1.5s ease-in-out infinite;
        }
        @keyframes loaderGlow {
            0%,
            100% {
                filter: brightness(1);
            }
            50% {
                filter: brightness(1.6);
            }
        }
        #initialLoader .loader-bar {
            width: 280px;
            height: 5px;
            background: #1a1a1a;
            border-radius: 10px;
            margin-top: 40px;
            overflow: hidden;
        }
        #initialLoader .loader-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--gold-dark), var(--gold), var(--gold-light));
            border-radius: 10px;
            animation: loaderFill 2.2s ease-in-out;
        }
        @keyframes loaderFill {
            0% {
                width: 0;
            }
            100% {
                width: 100%;
            }
        }
        #initialLoader .loader-dots {
            display: flex;
            gap: 12px;
            margin-top: 25px;
        }
        #initialLoader .loader-dot {
            width: 14px;
            height: 14px;
            background: var(--gold);
            border-radius: 50%;
            animation: dotJump 0.7s ease-in-out infinite alternate;
        }
        #initialLoader .loader-dot:nth-child(2) {
            animation-delay: 0.2s;
        }
        #initialLoader .loader-dot:nth-child(3) {
            animation-delay: 0.4s;
        }
        @keyframes dotJump {
            to {
                transform: translateY(-25px);
                opacity: 0.3;
            }
        }

        /* ============ صفحة المصادقة (تظهر بعد التحميل) ============ */
        #authPage {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.97);
            backdrop-filter: blur(30px);
            z-index: 90000;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.6s cubic-bezier(0.77, 0, 0.175, 1);
        }
        #authPage.hidden {
            opacity: 0;
            pointer-events: none;
            transform: scale(1.1);
        }
        #authPage .auth-container {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: var(--radius-lg);
            padding: 45px 40px;
            width: 92%;
            max-width: 520px;
            box-shadow: 0 0 120px rgba(212, 168, 83, 0.25), 0 0 300px rgba(0, 0, 0, 0.8);
            animation: authBoxIn 0.7s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }
        @keyframes authBoxIn {
            from {
                transform: scale(0.3) translateY(80px);
                opacity: 0;
            }
            to {
                transform: scale(1) translateY(0);
                opacity: 1;
            }
        }
        #authPage .auth-container::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: conic-gradient(from 0deg, transparent, rgba(212, 168, 83, 0.03), transparent, rgba(212, 168, 83, 0.03),
                    transparent);
            animation: authSpin 20s linear infinite;
            pointer-events: none;
        }
        @keyframes authSpin {
            to {
                transform: rotate(360deg);
            }
        }
        #authPage .auth-inner {
            position: relative;
            z-index: 1;
        }
        #authPage .auth-logo {
            text-align: center;
            font-size: 4em;
            animation: authLogoFloat 3s ease-in-out infinite;
            filter: drop-shadow(0 0 25px rgba(212, 168, 83, 0.6));
        }
        @keyframes authLogoFloat {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-15px);
            }
        }
        #authPage h2 {
            text-align: center;
            font-size: 2.2em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin: 15px 0 5px;
        }
        #authPage .auth-subtitle {
            text-align: center;
            color: var(--text-secondary);
            margin-bottom: 25px;
            font-size: 0.95em;
        }
        #authPage .auth-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
        }
        #authPage .auth-tab {
            flex: 1;
            padding: 13px;
            background: transparent;
            border: 2px solid rgba(212, 168, 83, 0.3);
            color: var(--gold);
            border-radius: var(--radius-sm);
            cursor: pointer;
            font-weight: 900;
            font-size: 1em;
            transition: var(--transition);
            text-align: center;
        }
        #authPage .auth-tab.active {
            background: var(--gold);
            color: #1a1a1a;
            border-color: var(--gold);
            box-shadow: 0 5px 25px rgba(212, 168, 83, 0.3);
        }
        #authPage .auth-tab:hover:not(.active) {
            border-color: var(--gold-light);
            background: rgba(212, 168, 83, 0.05);
        }
        #authPage .form-group {
            margin-bottom: 16px;
            position: relative;
        }
        #authPage .form-group label {
            display: block;
            color: var(--gold);
            margin-bottom: 6px;
            font-weight: bold;
            font-size: 0.9em;
        }
        #authPage .form-group .input-icon {
            position: absolute;
            right: 14px;
            top: 42px;
            font-size: 1.2em;
            pointer-events: none;
        }
        #authPage .form-group input {
            width: 100%;
            padding: 14px 45px 14px 18px;
            background: var(--bg-input);
            border: 2px solid #2a2a2a;
            border-radius: var(--radius-sm);
            color: var(--text-primary);
            font-size: 1em;
            font-family: inherit;
            transition: var(--transition);
        }
        #authPage .form-group input:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 20px rgba(212, 168, 83, 0.2);
            background: #1a1a1a;
        }
        #authPage .form-group input::placeholder {
            color: #555;
        }
        #authPage .btn-auth {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, var(--gold-dark), var(--gold), var(--gold-light));
            color: #1a1a1a;
            border: none;
            border-radius: var(--radius-sm);
            font-size: 1.2em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }
        #authPage .btn-auth:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 35px rgba(212, 168, 83, 0.4);
        }
        #authPage .btn-auth:active {
            transform: scale(0.95);
        }
        #authPage .btn-auth::after {
            content: '';
            position: absolute;
            top: -100%;
            left: -100%;
            width: 300%;
            height: 300%;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            transition: all 0.5s;
        }
        #authPage .btn-auth:hover::after {
            top: 100%;
            left: 100%;
        }
        #authPage .error-msg {
            color: var(--red);
            text-align: center;
            margin-top: 10px;
            display: none;
            font-weight: bold;
            font-size: 0.9em;
            animation: shake 0.5s;
        }
        @keyframes shake {
            0%,
            100% {
                transform: translateX(0);
            }
            25% {
                transform: translateX(-8px);
            }
            75% {
                transform: translateX(8px);
            }
        }
        #authPage .success-msg {
            color: var(--green);
            text-align: center;
            margin-top: 10px;
            display: none;
            font-weight: bold;
            font-size: 0.9em;
        }
        #authPage .auth-footer-text {
            text-align: center;
            margin-top: 20px;
            color: var(--text-muted);
            font-size: 0.85em;
        }
        #authPage .auth-footer-text span {
            color: var(--gold);
            cursor: pointer;
            text-decoration: underline;
            font-weight: bold;
        }

        /* ============ الصفحة الرئيسية (مخفية حتى تسجيل الدخول) ============ */
        #mainApp {
            display: none;
        }
        #mainApp.visible {
            display: block;
            animation: mainAppIn 0.6s ease-out;
        }
        @keyframes mainAppIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ============ النافبار ============ */
        .navbar {
            background: rgba(10, 10, 10, 0.88);
            backdrop-filter: blur(35px) saturate(180%);
            -webkit-backdrop-filter: blur(35px) saturate(180%);
            border-bottom: 1px solid var(--border-gold);
            padding: 12px 28px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 5px 35px rgba(0, 0, 0, 0.7);
            animation: navbarSlide 0.7s ease-out;
        }
        @keyframes navbarSlide {
            from {
                transform: translateY(-120%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        .logo-wrap {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            transition: var(--transition);
        }
        .logo-wrap:hover {
            transform: scale(1.06);
        }
        .logo-icon {
            font-size: 2.4em;
            animation: logoFloat 3.5s ease-in-out infinite;
            filter: drop-shadow(0 0 18px rgba(212, 168, 83, 0.7));
        }
        @keyframes logoFloat {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
        }
        .logo-text {
            font-size: 1.7em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: 3px;
        }
        .nav-actions {
            display: flex;
            gap: 10px;
            align-items: center;
            flex-wrap: wrap;
        }
        .nav-link {
            background: transparent;
            border: 1px solid rgba(212, 168, 83, 0.35);
            color: var(--gold);
            padding: 10px 18px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.88em;
            transition: var(--transition);
            white-space: nowrap;
            position: relative;
            overflow: hidden;
        }
        .nav-link:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-4px);
            box-shadow: 0 8px 28px rgba(212, 168, 83, 0.35);
        }
        .nav-cart-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 13px 26px;
            border-radius: 50px;
            font-weight: 900;
            cursor: pointer;
            position: relative;
            transition: var(--transition);
            font-size: 1em;
            box-shadow: 0 5px 22px rgba(212, 168, 83, 0.35);
        }
        .nav-cart-btn:hover {
            transform: translateY(-4px);
            box-shadow: 0 12px 35px rgba(212, 168, 83, 0.55);
        }
        .cart-badge {
            position: absolute;
            top: -10px;
            right: -10px;
            background: var(--red);
            color: #fff;
            border-radius: 50%;
            width: 28px;
            height: 28px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75em;
            font-weight: 900;
            display: none;
            animation: badgePop 0.5s ease-out;
        }
        @keyframes badgePop {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.4);
            }
            100% {
                transform: scale(1);
            }
        }
        .nav-user-info {
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(165, 94, 234, 0.1);
            border: 1px solid var(--purple);
            color: var(--purple);
            padding: 10px 18px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 0.9em;
            cursor: pointer;
            transition: var(--transition);
        }
        .nav-user-info:hover {
            background: rgba(165, 94, 234, 0.2);
        }
        .nav-logout-btn {
            background: transparent;
            border: 1px solid var(--red);
            color: var(--red);
            padding: 10px 16px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.85em;
            transition: var(--transition);
        }
        .nav-logout-btn:hover {
            background: var(--red);
            color: #fff;
            transform: translateY(-3px);
        }

        /* ============ المحتوى ============ */
        .main-container {
            max-width: 1350px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        /* ============ الهيرو ============ */
        .hero-section {
            text-align: center;
            padding: 50px 20px 30px;
        }
        .hero-section h1 {
            font-size: clamp(2.2em, 5.5vw, 4em);
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), #fff, var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
            animation: heroGlow 2.5s ease-in-out infinite;
            line-height: 1.2;
        }
        @keyframes heroGlow {
            0%,
            100% {
                filter: brightness(1) drop-shadow(0 0 10px rgba(212, 168, 83, 0.2));
            }
            50% {
                filter: brightness(1.5) drop-shadow(0 0 35px rgba(212, 168, 83, 0.7));
            }
        }
        .hero-section .hero-desc {
            color: var(--text-secondary);
            font-size: 1.15em;
            max-width: 650px;
            margin: 0 auto 25px;
            line-height: 1.7;
        }
        .hero-search-box {
            display: flex;
            max-width: 480px;
            margin: 0 auto 25px;
            gap: 8px;
        }
        .hero-search-box input {
            flex: 1;
            padding: 15px 22px;
            background: var(--bg-input);
            border: 2px solid #2a2a2a;
            border-radius: 50px;
            color: var(--text-primary);
            font-size: 1em;
            font-family: inherit;
            transition: var(--transition);
        }
        .hero-search-box input:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 25px rgba(212, 168, 83, 0.2);
        }
        .hero-search-box button {
            padding: 15px 22px;
            background: var(--gold);
            color: #1a1a1a;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 900;
            font-size: 1.2em;
            transition: var(--transition);
        }
        .hero-search-box button:hover {
            background: var(--gold-light);
            transform: scale(1.06);
        }
        .hero-stats {
            display: flex;
            justify-content: center;
            gap: 22px;
            flex-wrap: wrap;
        }
        .hero-stat {
            background: rgba(17, 17, 17, 0.8);
            border: 1px solid var(--border-gold);
            border-radius: var(--radius);
            padding: 22px 32px;
            text-align: center;
            backdrop-filter: blur(20px);
            transition: var(--transition);
            cursor: default;
        }
        .hero-stat:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
            box-shadow: var(--shadow-gold);
        }
        .hero-stat .stat-number {
            font-size: 2.5em;
            font-weight: 900;
            color: var(--gold);
            display: block;
        }
        .hero-stat .stat-label {
            color: var(--text-secondary);
            font-size: 0.9em;
            margin-top: 4px;
        }

        /* ============ عناوين الأقسام ============ */
        .section-header {
            text-align: center;
            font-size: 2em;
            font-weight: 900;
            color: var(--gold);
            margin: 50px 0 18px;
            position: relative;
        }
        .section-header::after {
            content: '';
            display: block;
            width: 65px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold), var(--gold-light), var(--gold), transparent);
            margin: 10px auto;
            border-radius: 10px;
        }
        .section-subtitle {
            text-align: center;
            color: var(--text-secondary);
            margin-bottom: 28px;
            font-size: 0.95em;
        }

        /* ============ شبكة المنتجات ============ */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 24px;
            padding: 8px;
        }
        .product-card {
            background: linear-gradient(160deg, #1a1a1a, #0e0e0e);
            border-radius: var(--radius);
            overflow: hidden;
            border: 1px solid var(--border);
            transition: var(--transition);
            position: relative;
            cursor: pointer;
            box-shadow: 0 8px 28px rgba(0, 0, 0, 0.4);
            animation: cardFadeIn 0.5s ease-out;
        }
        @keyframes cardFadeIn {
            from {
                opacity: 0;
                transform: translateY(25px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .product-card:hover {
            transform: translateY(-14px);
            border-color: var(--gold);
            box-shadow: 0 22px 55px rgba(212, 168, 83, 0.25), 0 0 45px rgba(212, 168, 83, 0.08);
        }
        .product-card .discount-tag {
            position: absolute;
            top: 14px;
            left: 14px;
            background: var(--red);
            color: #fff;
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 0.78em;
            font-weight: 900;
            z-index: 2;
            animation: tagPulse 1.5s infinite;
        }
        @keyframes tagPulse {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(255, 71, 87, 0.5);
            }
            50% {
                box-shadow: 0 0 0 16px rgba(255, 71, 87, 0);
            }
        }
        .product-card .fav-btn {
            position: absolute;
            top: 14px;
            right: 14px;
            background: rgba(0, 0, 0, 0.7);
            border: none;
            color: #fff;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 2;
            font-size: 1.2em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(10px);
        }
        .product-card .fav-btn.liked {
            background: var(--pink);
            animation: heartBeat 0.6s;
        }
        @keyframes heartBeat {
            0%,
            100% {
                transform: scale(1);
            }
            30% {
                transform: scale(1.4);
            }
            60% {
                transform: scale(0.85);
            }
        }
        .product-img-wrap {
            width: 100%;
            height: 240px;
            position: relative;
            overflow: hidden;
        }
        .product-img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.7s;
        }
        .product-card:hover .product-img-wrap img {
            transform: scale(1.14) rotate(2deg);
        }
        .product-img-fallback {
            width: 100%;
            height: 240px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 6.5em;
            background: linear-gradient(135deg, #1a0e05, #2a1a0e, #0a0300);
        }
        .product-info {
            padding: 20px;
        }
        .product-info h3 {
            font-size: 1.15em;
            font-weight: 900;
            margin-bottom: 5px;
        }
        .product-info .product-desc {
            color: #7a6a55;
            font-size: 0.84em;
            margin-bottom: 14px;
            line-height: 1.4;
        }
        .product-bottom-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .old-price-tag {
            font-size: 0.8em;
            color: #555;
            text-decoration: line-through;
            margin-left: 6px;
        }
        .current-price-tag {
            font-size: 1.45em;
            font-weight: 900;
            color: var(--gold);
        }
        .btn-add-cart {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 11px 22px;
            border-radius: var(--radius-sm);
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9em;
        }
        .btn-add-cart:hover {
            transform: scale(1.07);
            box-shadow: 0 7px 22px rgba(212, 168, 83, 0.45);
        }
        .btn-add-cart:active {
            transform: scale(0.93);
        }
        .qty-control-row {
            display: flex;
            align-items: center;
            gap: 11px;
        }
        .qty-control-btn {
            background: var(--bg-input);
            border: 2px solid var(--gold);
            color: var(--gold);
            width: 34px;
            height: 34px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.1em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .qty-control-btn:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: scale(1.15);
        }
        .qty-display {
            font-size: 1.2em;
            font-weight: 900;
            min-width: 28px;
            text-align: center;
        }

        /* ============ مودال السلة ============ */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(12px);
            z-index: 5000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .modal-overlay.active {
            display: flex;
            animation: fadeIn 0.3s;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
        .modal-dialog {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: var(--radius-lg);
            padding: 32px;
            width: 92%;
            max-width: 680px;
            max-height: 86vh;
            overflow-y: auto;
            position: relative;
            animation: modalPopIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 0 100px rgba(212, 168, 83, 0.2);
        }
        @keyframes modalPopIn {
            from {
                transform: scale(0.4) translateY(60px);
                opacity: 0;
            }
            to {
                transform: scale(1) translateY(0);
                opacity: 1;
            }
        }
        .modal-close-btn {
            position: absolute;
            top: 16px;
            left: 20px;
            background: none;
            border: none;
            color: var(--gold);
            font-size: 2em;
            cursor: pointer;
            transition: var(--transition);
        }
        .modal-close-btn:hover {
            color: var(--red);
            transform: rotate(90deg) scale(1.2);
        }
        .modal-dialog h2 {
            text-align: center;
            color: var(--gold);
            font-size: 1.9em;
            margin-bottom: 22px;
        }
        .cart-item-row {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 14px;
            border-bottom: 1px solid #222;
            animation: fadeInUp 0.4s;
        }
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(18px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .cart-item-details {
            flex: 1;
        }
        .cart-item-name {
            font-weight: 900;
        }
        .cart-item-sub {
            color: var(--gold);
            font-size: 0.85em;
        }
        .cart-remove-btn {
            background: var(--red);
            color: #fff;
            border: none;
            padding: 8px 16px;
            border-radius: 8px;
            cursor: pointer;
            transition: var(--transition);
        }
        .cart-remove-btn:hover {
            background: #d63031;
            transform: scale(1.1);
        }
        .cart-total-display {
            text-align: center;
            font-size: 1.7em;
            font-weight: 900;
            color: var(--gold);
            margin: 20px 0;
            text-shadow: 0 0 30px rgba(212, 168, 83, 0.5);
        }
        .payment-options-row {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
            margin: 16px 0;
        }
        .payment-option-btn {
            background: var(--bg-input);
            border: 2px solid transparent;
            padding: 14px 16px;
            border-radius: var(--radius-sm);
            cursor: pointer;
            text-align: center;
            font-size: 1.8em;
            transition: var(--transition);
            flex: 1;
            min-width: 90px;
        }
        .payment-option-btn.selected {
            border-color: var(--gold);
            background: #1a1008;
            box-shadow: 0 0 25px rgba(212, 168, 83, 0.3);
        }
        .payment-option-btn span {
            display: block;
            font-size: 0.28em;
            margin-top: 4px;
            color: var(--text-primary);
        }
        .btn-checkout {
            width: 100%;
            padding: 17px;
            background: linear-gradient(135deg, #2ed573, #1dd1a1);
            color: #000;
            border: none;
            border-radius: var(--radius-sm);
            font-size: 1.25em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            letter-spacing: 2px;
        }
        .btn-checkout:hover {
            transform: translateY(-4px);
            box-shadow: 0 14px 40px rgba(46, 213, 115, 0.4);
        }

        /* ============ لوحة الأدمن ============ */
        .admin-dashboard {
            display: none;
            background: linear-gradient(160deg, #0d0d0d, #181818);
            border: 2px solid var(--purple);
            border-radius: 22px;
            padding: 28px;
            margin: 30px 0;
            animation: fadeIn 0.5s;
        }
        .admin-dashboard.active {
            display: block;
        }
        .admin-dashboard h2 {
            color: var(--purple);
            text-align: center;
            font-size: 1.7em;
            margin-bottom: 22px;
        }
        .admin-grid-layout {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(330px, 1fr));
            gap: 18px;
        }
        .admin-card {
            background: #141414;
            border: 1px solid #222;
            border-radius: 16px;
            padding: 18px;
        }
        .admin-card h3 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 12px;
        }
        .admin-card input,
        .admin-card select,
        .admin-card textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 8px;
            background: #0a0a0a;
            border: 1px solid #222;
            border-radius: 8px;
            color: var(--text-primary);
            font-family: inherit;
            font-size: 0.9em;
            transition: var(--transition);
        }
        .admin-card input:focus,
        .admin-card select:focus {
            outline: none;
            border-color: var(--purple);
        }
        .admin-card button {
            width: 100%;
            padding: 11px;
            border: none;
            border-radius: 8px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 4px;
        }
        .btn-add-product {
            background: var(--green);
            color: #000;
        }
        .btn-delete-product {
            background: var(--red);
            color: #fff;
            width: auto;
            padding: 6px 12px;
            font-size: 0.78em;
        }
        .btn-reset-all {
            background: var(--orange);
            color: #000;
        }
        .btn-export-data {
            background: var(--purple);
            color: #fff;
        }
        .btn-import-data {
            background: var(--blue);
            color: #fff;
        }
        .admin-product-list {
            max-height: 370px;
            overflow-y: auto;
        }
        .admin-product-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 9px;
            border-bottom: 1px solid #1a1a1a;
            font-size: 0.85em;
        }
        .admin-product-item button {
            width: auto;
            padding: 5px 10px;
            font-size: 0.78em;
        }
        #importFileInput {
            display: none;
        }

        /* ============ أزرار عائمة ============ */
        .floating-buttons {
            position: fixed;
            bottom: 28px;
            left: 28px;
            display: flex;
            flex-direction: column;
            gap: 11px;
            z-index: 100;
        }
        .float-btn {
            width: 52px;
            height: 52px;
            border-radius: 50%;
            border: none;
            cursor: pointer;
            font-size: 1.4em;
            transition: var(--transition);
            box-shadow: 0 8px 28px rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .float-btn:hover {
            transform: scale(1.16);
        }
        .float-whatsapp {
            background: #25D366;
            color: #fff;
            animation: waPulse 2s infinite;
        }
        @keyframes waPulse {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(37, 211, 102, 0.5);
            }
            50% {
                box-shadow: 0 0 0 20px rgba(37, 211, 102, 0);
            }
        }
        .float-admin-btn {
            background: linear-gradient(135deg, #6c5ce7, #a55eea);
            color: #fff;
            font-weight: 900;
        }
        .float-cart-btn {
            background: var(--gold);
            color: #1a1a1a;
            display: none;
        }
        .float-cart-btn.visible {
            display: flex;
            animation: bounceIn 0.5s;
        }
        @keyframes bounceIn {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.25);
            }
            100% {
                transform: scale(1);
            }
        }
        .float-scroll-top {
            background: #333;
            color: #fff;
            font-size: 1.2em;
            display: none;
        }
        .float-scroll-top.visible {
            display: flex;
            animation: fadeIn 0.3s;
        }

        /* ============ توست ============ */
        .toast-container {
            position: fixed;
            top: 90px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 8px;
            align-items: center;
            pointer-events: none;
        }
        .toast {
            background: #1a1a1a;
            border: 1px solid var(--gold);
            color: var(--text-primary);
            padding: 14px 32px;
            border-radius: 50px;
            font-weight: 900;
            animation: toastSlideIn 0.4s, toastSlideOut 0.4s 2.6s forwards;
            white-space: nowrap;
            box-shadow: var(--shadow-md);
            pointer-events: auto;
        }
        @keyframes toastSlideIn {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        @keyframes toastSlideOut {
            from {
                opacity: 1;
            }
            to {
                opacity: 0;
                transform: translateY(-35px);
            }
        }

        /* ============ فوتر ============ */
        .site-footer {
            text-align: center;
            padding: 45px 20px;
            background: #050505;
            border-top: 1px solid rgba(212, 168, 83, 0.12);
            margin-top: 60px;
            position: relative;
            z-index: 1;
        }
        .site-footer h3 {
            color: var(--gold);
            font-size: 1.9em;
            margin-bottom: 8px;
        }
        .site-footer .phone-number {
            color: var(--gold);
            font-size: 1.3em;
            margin: 8px 0;
            direction: ltr;
            display: inline-block;
            font-weight: 900;
        }
        .site-footer .social-icons {
            display: flex;
            justify-content: center;
            gap: 14px;
            margin: 22px 0;
        }
        .site-footer .social-icon {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            cursor: pointer;
            transition: var(--transition);
        }
        .site-footer .social-icon:hover {
            border-color: var(--gold);
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-6px);
            box-shadow: var(--shadow-gold);
        }

        /* ============ Responsive ============ */
        @media (max-width: 768px) {
            .navbar {
                flex-wrap: wrap;
                gap: 6px;
                justify-content: center;
                padding: 8px;
            }
            .nav-link {
                padding: 7px 12px;
                font-size: 0.74em;
            }
            .hero-section h1 {
                font-size: 1.7em;
            }
            .products-grid {
                grid-template-columns: 1fr 1fr;
                gap: 12px;
            }
            .product-img-wrap,
            .product-img-fallback {
                height: 155px;
            }
            .product-img-fallback {
                font-size: 4em;
            }
            .section-header {
                font-size: 1.4em;
            }
            .auth-container {
                padding: 28px 20px;
            }
            #authPage h2 {
                font-size: 1.6em;
            }
            .modal-dialog {
                padding: 20px;
            }
            .admin-grid-layout {
                grid-template-columns: 1fr;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>

    <!-- مؤشر مخصص -->
    <div class="custom-cursor" id="customCursor"></div>
    <div class="cursor-inner" id="cursorDot"></div>

    <!-- جسيمات -->
    <canvas id="particlesCanvas"></canvas>

    <!-- شاشة التحميل الأولية -->
    <div id="initialLoader">
        <div class="loader-coffee">☕</div>
        <div class="loader-title">كافيه مصطفى</div>
        <div class="loader-bar"><div class="loader-fill"></div></div>
        <div class="loader-dots">
            <div class="loader-dot"></div><div class="loader-dot"></div><div class="loader-dot"></div>
        </div>
    </div>

    <!-- صفحة المصادقة -->
    <div id="authPage">
        <div class="auth-container">
            <div class="auth-inner">
                <div class="auth-logo">☕</div>
                <h2>كافيه مصطفى</h2>
                <p class="auth-subtitle">سجل دخولك أو أنشئ حساباً جديداً للمتابعة</p>
                <div class="auth-tabs">
                    <button class="auth-tab active" onclick="switchAuthTab('login')">🚪 تسجيل الدخول</button>
                    <button class="auth-tab" onclick="switchAuthTab('register')">📝 إنشاء حساب</button>
                </div>
                <div id="loginFormBlock">
                    <div class="form-group">
                        <label>👤 اسم المستخدم</label>
                        <span class="input-icon">👤</span>
                        <input type="text" id="loginUsername" placeholder="أدخل اسم المستخدم">
                    </div>
                    <div class="form-group">
                        <label>🔒 كلمة المرور</label>
                        <span class="input-icon">🔒</span>
                        <input type="password" id="loginPassword" placeholder="أدخل كلمة المرور">
                    </div>
                    <div class="error-msg" id="loginError"></div>
                    <button class="btn-auth" onclick="handleLogin()">🚪 دخول إلى الموقع</button>
                </div>
                <div id="registerFormBlock" style="display:none;">
                    <div class="form-group">
                        <label>👤 اسم المستخدم</label>
                        <span class="input-icon">👤</span>
                        <input type="text" id="regUsername" placeholder="اختر اسم مستخدم">
                    </div>
                    <div class="form-group">
                        <label>📧 البريد الإلكتروني</label>
                        <span class="input-icon">📧</span>
                        <input type="email" id="regEmail" placeholder="أدخل بريدك الإلكتروني">
                    </div>
                    <div class="form-group">
                        <label>🔒 كلمة المرور</label>
                        <span class="input-icon">🔒</span>
                        <input type="password" id="regPassword" placeholder="كلمة مرور قوية (6 أحرف على الأقل)">
                    </div>
                    <div class="form-group">
                        <label>🔒 تأكيد كلمة المرور</label>
                        <span class="input-icon">🔒</span>
                        <input type="password" id="regPasswordConfirm" placeholder="أعد كتابة كلمة المرور">
                    </div>
                    <div class="error-msg" id="regError"></div>
                    <div class="success-msg" id="regSuccess"></div>
                    <button class="btn-auth" onclick="handleRegister()">📝 إنشاء حساب جديد</button>
                </div>
                <p class="auth-footer-text">كافيه مصطفى © 2026 - جميع الحقوق محفوظة</p>
            </div>
        </div>
    </div>

    <!-- التطبيق الرئيسي -->
    <div id="mainApp">
        <!-- النافبار -->
        <nav class="navbar">
            <div class="logo-wrap" onclick="scrollToTop()">
                <span class="logo-icon">☕</span>
                <span class="logo-text">كافيه مصطفى</span>
            </div>
            <div class="nav-actions">
                <button class="nav-link" onclick="scrollToSection('drinksSection')">🥤 مشروبات</button>
                <button class="nav-link" onclick="scrollToSection('foodSection')">🍽️ مأكولات</button>
                <button class="nav-link" onclick="scrollToSection('specialSection')">🍷 مشروبات خاصة</button>
                <button class="nav-link" onclick="scrollToSection('paymentSection')">💳 الدفع</button>
                <div class="nav-user-info" id="navUserInfo">👤 مستخدم</div>
                <button class="nav-logout-btn" onclick="handleLogout()">🚪 خروج</button>
                <button class="nav-cart-btn" onclick="openCartModal()">
                    🛒 السلة <span class="cart-badge" id="cartBadge">0</span>
                </button>
            </div>
        </nav>

        <!-- المحتوى -->
        <div class="main-container">
            <!-- هيرو -->
            <div class="hero-section">
                <h1>☕ كافيه مصطفى</h1>
                <p class="hero-desc">أجود المشروبات والمأكولات الطازجة - اطلب أونلاين واستمتع بأفضل تجربة مع خدمة توصيل سريعة</p>
                <div class="hero-search-box">
                    <input type="text" id="searchInput" placeholder="🔍 ابحث عن منتجك المفضل...">
                    <button onclick="searchProducts()">🔍</button>
                </div>
                <div class="hero-stats">
                    <div class="hero-stat"><span class="stat-number" id="totalProductsStat">0</span><span class="stat-label">منتج</span></div>
                    <div class="hero-stat"><span class="stat-number">2</span><span class="stat-label">طرق دفع</span></div>
                    <div class="hero-stat"><span class="stat-number">24/7</span><span class="stat-label">خدمة</span></div>
                    <div class="hero-stat"><span class="stat-number">⭐4.9</span><span class="stat-label">تقييم</span></div>
                </div>
            </div>

            <!-- المشروبات -->
            <div id="drinksSection">
                <h2 class="section-header">🥤 المشروبات الساخنة والباردة</h2>
                <p class="section-subtitle">مشروبات محضرة بأيدي أمهر الباريستا</p>
                <div class="products-grid" id="drinksGrid"></div>
            </div>

            <!-- المأكولات -->
            <div id="foodSection">
                <h2 class="section-header">🍽️ المأكولات والحلويات</h2>
                <p class="section-subtitle">مأكولات طازجة يومياً بأفضل المكونات</p>
                <div class="products-grid" id="foodGrid"></div>
            </div>

            <!-- مشروبات خاصة -->
            <div id="specialSection">
                <h2 class="section-header">🍷 مشروبات خاصة</h2>
                <p class="section-subtitle">مشروبات مميزة للمناسبات الخاصة</p>
                <div class="products-grid" id="specialGrid"></div>
            </div>

            <!-- طرق الدفع -->
            <div id="paymentSection">
                <h2 class="section-header">💳 طرق الدفع الآمنة</h2>
                <p class="section-subtitle">نقداً عند الاستلام أو عن طريق فودافون كاش</p>
                <div style="display:flex;flex-wrap:wrap;gap:16px;justify-content:center;padding:22px;">
                    <div style="background:#1a1a1a;border:2px solid
