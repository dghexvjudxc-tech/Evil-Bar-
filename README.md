<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>☕ كافيه مصطفى</title>
    <style>
        :root {
            --gold: #d4a853;
            --gold-light: #f0d78c;
            --gold-dark: #b8922e;
            --bg: #0a0a0a;
            --bg2: #141414;
            --bg3: #1e1e1e;
            --text: #f0e6d2;
            --text2: #a89070;
            --border: #2a2a2a;
            --red: #ff4757;
            --green: #2ed573;
            --purple: #a55eea;
            --radius: 16px;
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* ============ جسيمات ============ */
        #particlesCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        /* ============ صفحة المصادقة ============ */
        #authPage {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.96);
            backdrop-filter: blur(25px);
            z-index: 9999;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        #authPage.hidden {
            display: none;
        }
        .auth-box {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: 25px;
            padding: 40px 35px;
            width: 92%;
            max-width: 480px;
            box-shadow: 0 0 100px rgba(212, 168, 83, 0.2);
            animation: popIn 0.5s ease-out;
            position: relative;
        }
        @keyframes popIn {
            from {
                transform: scale(0.5) translateY(50px);
                opacity: 0;
            }
            to {
                transform: scale(1) translateY(0);
                opacity: 1;
            }
        }
        .auth-box .auth-logo {
            text-align: center;
            font-size: 4em;
            animation: floatLogo 3s ease-in-out infinite;
        }
        @keyframes floatLogo {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-12px);
            }
        }
        .auth-box h2 {
            text-align: center;
            font-size: 2em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin: 10px 0;
        }
        .auth-box .subtitle {
            text-align: center;
            color: var(--text2);
            margin-bottom: 22px;
            font-size: 0.9em;
        }
        .auth-tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 22px;
        }
        .auth-tab {
            flex: 1;
            padding: 12px;
            background: transparent;
            border: 2px solid rgba(212, 168, 83, 0.3);
            color: var(--gold);
            border-radius: 10px;
            cursor: pointer;
            font-weight: 900;
            transition: var(--transition);
            text-align: center;
        }
        .auth-tab.active {
            background: var(--gold);
            color: #1a1a1a;
            border-color: var(--gold);
        }
        .form-group {
            margin-bottom: 14px;
        }
        .form-group label {
            display: block;
            color: var(--gold);
            margin-bottom: 5px;
            font-weight: bold;
            font-size: 0.9em;
        }
        .form-group input {
            width: 100%;
            padding: 13px 16px;
            background: var(--bg3);
            border: 2px solid #2a2a2a;
            border-radius: 10px;
            color: var(--text);
            font-size: 1em;
            font-family: inherit;
            transition: var(--transition);
        }
        .form-group input:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 15px rgba(212, 168, 83, 0.15);
        }
        .btn-auth {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            border-radius: 10px;
            font-size: 1.15em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .btn-auth:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 28px rgba(212, 168, 83, 0.35);
        }
        .error-msg {
            color: var(--red);
            text-align: center;
            margin-top: 8px;
            display: none;
            font-weight: bold;
            font-size: 0.88em;
        }
        .success-msg {
            color: var(--green);
            text-align: center;
            margin-top: 8px;
            display: none;
            font-weight: bold;
            font-size: 0.88em;
        }

        /* ============ التطبيق الرئيسي ============ */
        #mainApp {
            display: none;
        }
        #mainApp.visible {
            display: block;
            animation: fadeIn 0.5s;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ============ النافبار ============ */
        .navbar {
            background: rgba(10, 10, 10, 0.9);
            backdrop-filter: blur(30px);
            border-bottom: 1px solid rgba(212, 168, 83, 0.3);
            padding: 12px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 5px 30px rgba(0, 0, 0, 0.6);
            flex-wrap: wrap;
            gap: 8px;
        }
        .logo-wrap {
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
        }
        .logo-icon {
            font-size: 2em;
            animation: floatLogo 3s infinite;
        }
        .logo-text {
            font-size: 1.4em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .nav-actions {
            display: flex;
            gap: 8px;
            align-items: center;
            flex-wrap: wrap;
        }
        .nav-btn {
            background: transparent;
            border: 1px solid rgba(212, 168, 83, 0.35);
            color: var(--gold);
            padding: 9px 16px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.85em;
            transition: var(--transition);
        }
        .nav-btn:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-2px);
        }
        .cart-btn {
            background: var(--gold);
            color: #1a1a1a;
            border: none;
            padding: 11px 22px;
            border-radius: 50px;
            font-weight: 900;
            cursor: pointer;
            position: relative;
            transition: var(--transition);
        }
        .cart-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(212, 168, 83, 0.4);
        }
        .cart-badge {
            position: absolute;
            top: -8px;
            right: -8px;
            background: var(--red);
            color: #fff;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.7em;
            font-weight: 900;
            display: none;
        }
        .user-tag {
            background: rgba(165, 94, 234, 0.15);
            border: 1px solid var(--purple);
            color: var(--purple);
            padding: 9px 16px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 0.85em;
        }
        .logout-btn {
            background: transparent;
            border: 1px solid var(--red);
            color: var(--red);
            padding: 9px 14px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.85em;
            transition: var(--transition);
        }
        .logout-btn:hover {
            background: var(--red);
            color: #fff;
        }

        /* ============ المحتوى ============ */
        .container {
            max-width: 1300px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }
        .hero {
            text-align: center;
            padding: 40px 20px 25px;
        }
        .hero h1 {
            font-size: clamp(2em, 5vw, 3.2em);
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), #fff, var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 8px;
        }
        .hero p {
            color: var(--text2);
            font-size: 1em;
        }
        .section-title {
            text-align: center;
            font-size: 1.8em;
            font-weight: 900;
            color: var(--gold);
            margin: 45px 0 15px;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 55px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
            margin: 8px auto;
            border-radius: 10px;
        }
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            padding: 8px;
        }
        .product-card {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border-radius: var(--radius);
            overflow: hidden;
            border: 1px solid var(--border);
            transition: var(--transition);
            position: relative;
            cursor: pointer;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
        }
        .product-card:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
            box-shadow: 0 18px 45px rgba(212, 168, 83, 0.2);
        }
        .product-card .badge {
            position: absolute;
            top: 12px;
            left: 12px;
            background: var(--red);
            color: #fff;
            padding: 5px 14px;
            border-radius: 20px;
            font-size: 0.75em;
            font-weight: 900;
            z-index: 2;
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(255, 71, 87, 0.5);
            }
            50% {
                box-shadow: 0 0 0 14px rgba(255, 71, 87, 0);
            }
        }
        .img-wrap {
            width: 100%;
            height: 210px;
            overflow: hidden;
        }
        .img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.6s;
        }
        .product-card:hover .img-wrap img {
            transform: scale(1.1);
        }
        .img-fb {
            width: 100%;
            height: 210px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 5em;
            background: linear-gradient(135deg, #1a0e05, #2a1a0e);
        }
        .info {
            padding: 16px;
        }
        .info h3 {
            font-size: 1.1em;
            margin-bottom: 4px;
        }
        .info .desc {
            color: #7a6a55;
            font-size: 0.82em;
            margin-bottom: 12px;
        }
        .price-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .old-p {
            font-size: 0.8em;
            color: #555;
            text-decoration: line-through;
            margin-left: 5px;
        }
        .cur-p {
            font-size: 1.3em;
            font-weight: 900;
            color: var(--gold);
        }
        .add-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 10px 18px;
            border-radius: 10px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .add-btn:hover {
            transform: scale(1.05);
        }
        .qty-row {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .qty-b {
            background: var(--bg3);
            border: 2px solid var(--gold);
            color: var(--gold);
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1em;
            transition: var(--transition);
        }
        .qty-b:hover {
            background: var(--gold);
            color: #1a1a1a;
        }
        .qty-v {
            font-weight: 900;
            min-width: 24px;
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
            backdrop-filter: blur(10px);
            z-index: 5000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .modal-overlay.active {
            display: flex;
            animation: fadeIn 0.3s;
        }
        .modal-box {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: 22px;
            padding: 28px;
            width: 92%;
            max-width: 600px;
            max-height: 85vh;
            overflow-y: auto;
            position: relative;
            animation: popIn 0.4s ease-out;
        }
        .modal-close {
            position: absolute;
            top: 14px;
            left: 18px;
            background: none;
            border: none;
            color: var(--gold);
            font-size: 1.8em;
            cursor: pointer;
        }
        .modal-close:hover {
            color: var(--red);
            transform: rotate(90deg);
        }
        .modal-box h2 {
            text-align: center;
            color: var(--gold);
            margin-bottom: 18px;
        }
        .cart-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px;
            border-bottom: 1px solid #222;
        }
        .cart-item-info {
            flex: 1;
        }
        .cart-item-name {
            font-weight: bold;
        }
        .cart-item-price {
            color: var(--gold);
            font-size: 0.85em;
        }
        .cart-remove {
            background: var(--red);
            color: #fff;
            border: none;
            padding: 7px 12px;
            border-radius: 8px;
            cursor: pointer;
        }
        .cart-total {
            text-align: center;
            font-size: 1.5em;
            font-weight: 900;
            color: var(--gold);
            margin: 18px 0;
        }
        .pay-opts {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin: 14px 0;
        }
        .pay-opt {
            background: var(--bg3);
            border: 2px solid transparent;
            padding: 14px;
            border-radius: 12px;
            cursor: pointer;
            text-align: center;
            font-size: 1.6em;
            transition: var(--transition);
            flex: 1;
            min-width: 80px;
        }
        .pay-opt.selected {
            border-color: var(--gold);
            background: #1a1008;
            box-shadow: 0 0 20px rgba(212, 168, 83, 0.25);
        }
        .pay-opt span {
            display: block;
            font-size: 0.3em;
        }
        .checkout-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #2ed573, #1dd1a1);
            color: #000;
            border: none;
            border-radius: 12px;
            font-size: 1.15em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .checkout-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(46, 213, 115, 0.4);
        }

        /* ============ لوحة الأدمن ============ */
        .admin-panel {
            display: none;
            background: linear-gradient(160deg, #0d0d0d, #181818);
            border: 2px solid var(--purple);
            border-radius: 20px;
            padding: 25px;
            margin: 30px 0;
        }
        .admin-panel.active {
            display: block;
        }
        .admin-panel h2 {
            color: var(--purple);
            text-align: center;
            margin-bottom: 18px;
        }
        .admin-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 16px;
        }
        .admin-card {
            background: #141414;
            border: 1px solid #222;
            border-radius: 14px;
            padding: 16px;
        }
        .admin-card h3 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 10px;
        }
        .admin-card input,
        .admin-card select {
            width: 100%;
            padding: 9px;
            margin-bottom: 7px;
            background: #0a0a0a;
            border: 1px solid #222;
            border-radius: 7px;
            color: var(--text);
            font-family: inherit;
            font-size: 0.88em;
        }
        .admin-card button {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 7px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 3px;
        }
        .btn-add {
            background: var(--green);
            color: #000;
        }
        .btn-del {
            background: var(--red);
            color: #fff;
            width: auto;
            padding: 5px 10px;
            font-size: 0.75em;
        }
        .btn-reset {
            background: #ffa502;
            color: #000;
        }
        .btn-export {
            background: var(--purple);
            color: #fff;
        }
        .admin-list {
            max-height: 320px;
            overflow-y: auto;
        }
        .admin-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 7px;
            border-bottom: 1px solid #1a1a1a;
            font-size: 0.82em;
        }

        /* ============ أزرار عائمة ============ */
        .floats {
            position: fixed;
            bottom: 25px;
            left: 25px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 100;
        }
        .fbtn {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            border: none;
            cursor: pointer;
            font-size: 1.3em;
            transition: var(--transition);
            box-shadow: 0 6px 22px rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .fbtn:hover {
            transform: scale(1.14);
        }
        .fbtn-wa {
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
                box-shadow: 0 0 0 18px rgba(37, 211, 102, 0);
            }
        }
        .fbtn-admin {
            background: linear-gradient(135deg, #6c5ce7, #a55eea);
            color: #fff;
            font-weight: 900;
        }
        .fbtn-cart {
            background: var(--gold);
            color: #1a1a1a;
            display: none;
        }
        .fbtn-cart.show {
            display: flex;
            animation: bounceIn 0.5s;
        }
        @keyframes bounceIn {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.2);
            }
            100% {
                transform: scale(1);
            }
        }

        /* ============ توست ============ */
        .toast-cont {
            position: fixed;
            top: 80px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 6px;
            pointer-events: none;
        }
        .toast {
            background: #1a1a1a;
            border: 1px solid var(--gold);
            padding: 12px 26px;
            border-radius: 50px;
            font-weight: bold;
            animation: tIn 0.4s, tOut 0.4s 2.4s forwards;
            pointer-events: auto;
        }
        @keyframes tIn {
            from {
                transform: translateY(-40px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        @keyframes tOut {
            from {
                opacity: 1;
            }
            to {
                opacity: 0;
                transform: translateY(-30px);
            }
        }

        /* ============ فوتر ============ */
        .footer {
            text-align: center;
            padding: 35px 20px;
            background: #050505;
            border-top: 1px solid rgba(212, 168, 83, 0.1);
            margin-top: 50px;
            position: relative;
            z-index: 1;
        }
        .footer h3 {
            color: var(--gold);
            font-size: 1.6em;
        }
        .footer .phone {
            color: var(--gold);
            font-size: 1.1em;
            margin: 6px 0;
            direction: ltr;
            display: inline-block;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .navbar {
                justify-content: center;
                padding: 8px;
            }
            .nav-btn {
                padding: 7px 11px;
                font-size: 0.72em;
            }
            .products-grid {
                grid-template-columns: 1fr 1fr;
                gap: 12px;
            }
            .img-wrap,
            .img-fb {
                height: 145px;
            }
            .img-fb {
                font-size: 3.5em;
            }
            .auth-box {
                padding: 28px 18px;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>

    <canvas id="particlesCanvas"></canvas>

    <!-- صفحة المصادقة -->
    <div id="authPage">
        <div class="auth-box">
            <div class="auth-logo">☕</div>
            <h2>كافيه مصطفى</h2>
            <p class="subtitle">سجل دخولك أو أنشئ حساباً للمتابعة</p>
            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchTab('login')">🚪 دخول</button>
                <button class="auth-tab" onclick="switchTab('register')">📝 حساب جديد</button>
            </div>
            <div id="loginForm">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="loginUser" placeholder="اسم المستخدم"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="loginPass" placeholder="كلمة المرور"></div>
                <div class="error-msg" id="loginErr"></div>
                <button class="btn-auth" onclick="doLogin()">🚪 دخول</button>
            </div>
            <div id="registerForm" style="display:none;">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="regUser" placeholder="اختر اسماً"></div>
                <div class="form-group"><label>📧 البريد الإلكتروني</label><input type="email" id="regEmail" placeholder="بريدك"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="regPass" placeholder="6 أحرف على الأقل"></div>
                <div class="form-group"><label>🔒 تأكيد كلمة المرور</label><input type="password" id="regPass2" placeholder="أعد كتابتها"></div>
                <div class="error-msg" id="regErr"></div>
                <div class="success-msg" id="regOk"></div>
                <button class="btn-auth" onclick="doRegister()">📝 إنشاء حساب</button>
            </div>
        </div>
    </div>

    <!-- التطبيق الرئيسي -->
    <div id="mainApp">
        <nav class="navbar">
            <div class="logo-wrap" onclick="scrollToTop()"><span class="logo-icon">☕</span><span class="logo-text">كافيه مصطفى</span></div>
            <div class="nav-actions">
                <button class="nav-btn" onclick="scrollToS('drinks')">🥤 مشروبات</button>
                <button class="nav-btn" onclick="scrollToS('food')">🍽️ مأكولات</button>
                <button class="nav-btn" onclick="scrollToS('special')">🍷 خاصة</button>
                <span class="user-tag" id="userTag">👤</span>
                <button class="logout-btn" onclick="logout()">🚪 خروج</button>
                <button class="cart-btn" onclick="openCart()">🛒 السلة <span class="cart-badge" id="cartBadge">0</span></button>
            </div>
        </nav>
        <div class="container">
            <div class="hero"><h1>☕ كافيه مصطفى</h1><p>أجود المشروبات والمأكولات - اطلب أونلاين</p></div>
            <div id="drinks"><h2 class="section-title">🥤 المشروبات</h2><div class="products-grid" id="drinksGrid"></div></div>
            <div id="food"><h2 class="section-title">🍽️ المأكولات</h2><div class="products-grid" id="foodGrid"></div></div>
            <div id="special"><h2 class="section-title">🍷 مشروبات خاصة</h2><div class="products-grid" id="specialGrid"></div></div>
            <div id="payment"><h2 class="section-title">💳 الدفع</h2>
                <div style="display:flex;flex-wrap:wrap;gap:14px;justify-content:center;padding:20px;">
                    <div style="background:#1a1a1a;border:2px solid var(--gold);border-radius:16px;padding:25px;text-align:center;font-size:2.5em;flex:1;min-width:130px;">💵<br><span style="font-size:0.25em;">نقداً</span></div>
                    <div style="background:#1a1a1a;border:2px solid var(--gold);border-radius:16px;padding:25px;text-align:center;font-size:2.5em;flex:1;min-width:130px;">📱<br><span style="font-size:0.25em;">فودافون كاش<br><span dir="ltr" style="color:var(--gold);font-size:1.2em;">01026966717</span></span></div>
                </div>
            </div>
            <div class="admin-panel" id="adminPanel">
                <h2>👑 لوحة الأدمن</h2>
                <div class="admin-grid">
                    <div class="admin-card">
                        <h3>➕ إضافة منتج</h3>
                        <select id="adminCat"><option value="drinks">🥤 مشروبات</option><option value="food">🍽️ مأكولات</option><option value="special">🍷 خاصة</option></select>
                        <input type="text" id="adminName" placeholder="الاسم">
                        <input type="text" id="adminDesc" placeholder="الوصف">
                        <input type="number" id="adminPrice" placeholder="السعر">
                        <input type="number" id="adminOld" placeholder="سعر قبل الخصم">
                        <input type="text" id="adminEmoji" placeholder="إيموجي">
                        <input type="text" id="adminImg" placeholder="رابط الصورة">
                        <button class="btn-add" onclick="adminAdd()">✅ إضافة</button>
                    </div>
                    <div class="admin-card"><h3>📋 المنتجات</h3><div class="admin-list" id="adminList"></div></div>
                    <div class="admin-card"><h3>⚙️ أدوات</h3><p style="color:var(--gold);">🥤 <b id="s1">0</b> | 🍽️ <b id="s2">0</b> | 🍷 <b id="s3">0</b></p><button class="btn-reset" onclick="adminReset()">🔄 إعادة ضبط</button><button class="btn-export" onclick="adminExport()">📤 تصدير</button></div>
                </div>
            </div>
        </div>
        <div class="footer"><h3>☕ كافيه مصطفى</h3><p style="color:var(--text2);">📍 شارع النخيل، مدينة القهوة</p><p class="phone">📞 01026966717</p><p style="color:#555;">© 2026 - Developed by Mustafa 👑</p></div>
    </div>

    <!-- مودال السلة -->
    <div class="modal-overlay" id="cartModal">
        <div class="modal-box">
            <button class="modal-close" onclick="closeCart()">✕</button>
            <h2>🛒 السلة</h2>
            <div id="cartItems"></div>
            <div class="cart-total" id="cartTotal">الإجمالي: 0 ج.م</div>
            <div class="pay-opts" id="payOpts">
                <div class="pay-opt selected" onclick="selPay('cash',this)">💵<span>نقداً</span></div>
                <div class="pay-opt" onclick="selPay('vodafone',this)">📱<span>فودافون كاش</span></div>
            </div>
            <button class="checkout-btn" onclick="checkout()">✅ تأكيد واتساب</button>
        </div>
    </div>

    <!-- أزرار عائمة -->
    <div class="floats">
        <button class="fbtn fbtn-wa" onclick="openWa()">💬</button>
        <button class="fbtn fbtn-admin" id="fAdmin" onclick="togAdmin()">👑</button>
        <button class="fbtn fbtn-cart" id="fCart" onclick="openCart()">🛒</button>
    </div>
    <div class="toast-cont" id="toastCont"></div>

    <script>
        const ADMIN_USER = 'Mustafa';
        const ADMIN_PASS = '123456';
        const WA_NUM = '201026966717';
        const PHONE = '01026966717';

        function defData() {
            return {
                drinks: [
                    { id: 1, name: 'قهوة تركية', desc: 'قهوة تركية أصلية', price: 25, oldPrice: 0, emoji: '☕',
                        img: 'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400&h=300&fit=crop' },
                    { id: 2, name: 'لاتيه', desc: 'لاتيه كريمي بحليب طازج', price: 35, oldPrice: 42, emoji: '🥛',
                        img: 'https://images.unsplash.com/photo-1570968915860-54d5c301fa9f?w=400&h=300&fit=crop' },
                    { id: 3, name: 'كابتشينو', desc: 'كابتشينو إيطالي', price: 30, oldPrice: 0, emoji: '☕',
                        img: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400&h=300&fit=crop' },
                    { id: 4, name: 'شاي كرك', desc: 'شاي كرك هندي', price: 20, oldPrice: 25, emoji: '🍵',
                        img: 'https://images.unsplash.com/photo-1564890369478-c89ca6d9cde9?w=400&h=300&fit=crop' },
                    { id: 5, name: 'موكا مثلجة', desc: 'موكا باردة', price: 40, oldPrice: 0, emoji: '🧊',
                        img: 'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400&h=300&fit=crop' },
                    { id: 6, name: 'عصير مانجو', desc: 'مانجو طبيعي', price: 30, oldPrice: 0, emoji: '🥭',
                        img: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=400&h=300&fit=crop' },
                ],
                food: [
                    { id: 101, name: 'كرواسون', desc: 'كرواسون فرنسي', price: 30, oldPrice: 0, emoji: '🥐',
                        img: 'https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=400&h=300&fit=crop' },
                    { id: 102, name: 'تشيز كيك', desc: 'تشيز كيك بالتوت', price: 45, oldPrice: 55, emoji: '🍰',
                        img: 'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400&h=300&fit=crop' },
                    { id: 103, name: 'وافل', desc: 'وافل شوكولاتة', price: 40, oldPrice: 0, emoji: '🧇',
                        img: 'https://images.unsplash.com/photo-1558584724-0e4d32ca55a6?w=400&h=300&fit=crop' },
                    { id: 104, name: 'بان كيك', desc: 'بان كيك بالعسل', price: 35, oldPrice: 0, emoji: '🥞',
                        img: 'https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=400&h=300&fit=crop' },
                ],
                special: [
                    { id: 201, name: 'مشروب خاص 1', desc: 'مشروب مميز', price: 50, oldPrice: 0, emoji: '🍷',
                        img: 'https://images.unsplash.com/photo-1474722883777-792e7990302f?w=400&h=300&fit=crop' },
                    { id: 202, name: 'مشروب خاص 2', desc: 'مشروب فاخر', price: 65, oldPrice: 80, emoji: '🥂',
                        img: 'https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?w=400&h=300&fit=crop' },
                ],
            };
        }

        function ld() { const s = localStorage.getItem('MFC_D');
            if (s) try { return JSON.parse(s); } catch (e) {} return defData(); }

        function sd() { localStorage.setItem('MFC_D', JSON.stringify(data)); }
        let data = ld();
        let cart = JSON.parse(localStorage.getItem('MFC_C') || '[]');
        let selPayM = 'cash';
        let isAdmin = false;
        let user = null;

        // جسيمات
        const pc = document.getElementById('particlesCanvas');
        const pctx = pc.getContext('2d');
        pc.width = innerWidth;
        pc.height = innerHeight;
        const pa = [];
        class P {
            constructor() { this.r();
                this.y = Math.random() * pc.height; }
            r() { this.x = Math.random() * pc.width;
                this.y = -10;
                this.s = Math.random() * 3 + 1;
                this.sy = Math.random() * 1.5 + 0.3;
                this.sx = (Math.random() - 0.5) * 0.4;
                this.o = Math.random() * 0.6 + 0.2;
                this.c = ['#d4a853', '#f0d78c', '#b8922e'][Math.floor(Math.random() * 3)]; }
            u() { this.y += this.sy;
                this.x += this.sx; if (this.y > pc.height + 10) this.r(); }
            d() { pctx.beginPath();
                pctx.arc(this.x, this.y, this.s, 0, Math.PI * 2);
                pctx.fillStyle = this.c;
                pctx.globalAlpha = this.o;
                pctx.fill();
                pctx.globalAlpha = 1; }
        }
        for (let i = 0; i < 45; i++) pa.push(new P());

        function ap() { pctx.clearRect(0, 0, pc.width, pc.height);
            pa.forEach(p => { p.u();
                p.d(); });
            requestAnimationFrame(ap); }
        ap();
        addEventListener('resize', () => { pc.width = innerWidth;
            pc.height = innerHeight; });

        // توست
        function toast(m, e) { const c = document.getElementById('toastCont');
            const t = document.createElement('div');
            t.className = 'toast';
            t.style.borderColor = e ? 'var(--red)' : 'var(--gold)';
            t.textContent = m;
            c.appendChild(t);
            setTimeout(() => t.remove(), 2800); }

        // المصادقة
        function switchTab(t) {
            document.querySelectorAll('.auth-tab').forEach(x => x.classList.remove('active'));
            if (t === 'login') { document.querySelector('.auth-tab:nth-child(1)').classList.add('active');
                document.getElementById('loginForm').style.display = 'block';
                document.getElementById('registerForm').style.display = 'none'; } else { document.querySelector(
                    '.auth-tab:nth-child(2)').classList.add('active');
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('registerForm').style.display = 'block'; }
            document.getElementById('loginErr').style.display = 'none';
            document.getElementById('regErr').style.display = 'none';
            document.getElementById('regOk').style.display = 'none';
        }

        function doLogin() {
            const u = document.getElementById('loginUser').value.trim();
            const p = document.getElementById('loginPass').value.trim();
            const e = document.getElementById('loginErr');
            if (!u || !p) { e.textContent = '⚠️ املأ الحقول';
                e.style.display = 'block'; return; }
            const users = JSON.parse(localStorage.getItem('MFC_U') || '[]');
            const f = users.find(x => x.username.toLowerCase() === u.toLowerCase() && x.password === p);
            if (f) { user = f;
                isAdmin = f.isAdmin;
                localStorage.setItem('MFC_CU', JSON.stringify(f));
                showApp();
                toast('✅ مرحباً ' + f.username); } else { e.textContent = '❌ بيانات خاطئة';
                e.style.display = 'block'; }
        }

        function doRegister() {
            const u = document.getElementById('regUser').value.trim();
            const em = document.getElementById('regEmail').value.trim();
            const p = document.getElementById('regPass').value.trim();
            const p2 = document.getElementById('regPass2').value.trim();
            const err = document.getElementById('regErr');
            const ok = document.getElementById('regOk');
            err.style.display = 'none';
            ok.style.display = 'none';
            if (!u || !em || !p || !p2) { err.textContent = '⚠️ املأ الحقول';
                err.style.display = 'block'; return; }
            if (p !== p2) { err.textContent = '❌ كلمتا المرور غير متطابقتين';
                err.style.display = 'block'; return; }
            if (p.length < 6) { err.textContent = '❌ 6 أحرف على الأقل';
                err.style.display = 'block'; return; }
            if (!em.includes('@')) { err.textContent = '❌ بريد غير صالح';
                err.style.display = 'block'; return; }
            if (u.toLowerCase() === ADMIN_USER.toLowerCase()) { err.textContent = '❌ الاسم محجوز للأدمن';
                err.style.display = 'block'; return; }
            const users = JSON.parse(localStorage.getItem('MFC_U') || '[]');
            if (users.find(x => x.username.toLowerCase() === u.toLowerCase())) { err.textContent = '❌ الاسم موجود';
                err.style.display = 'block'; return; }
            const isA = (u.toLowerCase() === ADMIN_USER.toLowerCase());
            users.push({ username: u, email: em, password: p, isAdmin: isA, createdAt: new Date().toISOString() });
            localStorage.setItem('MFC_U', JSON.stringify(users));
            ok.textContent = '✅ تم الإنشاء! سجل دخولك';
            ok.style.display = 'block';
            document.getElementById('regUser').value = '';
            document.getElementById('regEmail').value = '';
            document.getElementById('regPass').value = '';
            document.getElementById('regPass2').value = '';
            setTimeout(() => switchTab('login'), 1400);
        }

        function showApp() { document.getElementById('authPage').classList.add('hidden');
            document.getElementById('mainApp').classList.add('visible');
            document.getElementById('userTag').textContent = '👑 ' + user.username;
            document.getElementById('fAdmin').style.background = isAdmin ?
                'linear-gradient(135deg,#2ed573,#1dd1a1)' : 'linear-gradient(135deg,#6c5ce7,#a55eea)';
            renderAll();
            updateCartBadge(); if (isAdmin) { document.getElementById('adminPanel').classList.add('active');
                renAdminList(); } }

        function logout() { user = null;
            isAdmin = false;
            localStorage.removeItem('MFC_CU');
            document.getElementById('mainApp').classList.remove('visible');
            document.getElementById('authPage').classList.remove('hidden');
            document.getElementById('adminPanel').classList.remove('active');
            toast('👋 تم الخروج'); }

        // عرض المنتجات
        function card(p) { const ci = cart.find(i => i.id === p.id);
            const q = ci ? ci.quantity : 0;
            const d = p.oldPrice > 0 && p.oldPrice > p.price;
            const dp = d ? Math.round((1 - p.price / p.oldPrice) * 100) : 0;
            const im = p.img ?
                `<img src="${p.img}" alt="${p.name}" loading="lazy" onerror="this.style.display='none';this.parentElement.querySelector('.fb').style.display='flex';">` :
                '';
            return `
        <div class="product-card">
          ${d?`<div class="badge">🔥 -${dp}%</div>`:''}
          <div class="img-wrap">${im}<div class="img-fb fb" style="${p.img?'display:none;':''}">${p.emoji||'🍽️'}</div></div>
          <div class="info"><h3>${p.emoji||''} ${p.name}</h3><p class="desc">${p.desc}</p>
            <div class="price-row"><div>${d?`<span class="old-p">${p.oldPrice} ج.م</span>`:''}<span class="cur-p">${p.price} ج.م</span></div>
            ${q>0?`<div class="qty-row"><button class="qty-b" onclick="chq(${p.id},'${p.name.replace(/'/g,"\\'")}',${p.price},-1,event)">➖</button><span class="qty-v">${q}</span><button class="qty-b" onclick="chq(${p.id},'${p.name.replace(/'/g,"\\'")}',${p.price},1,event)">➕</button></div>`:`<button class="add-btn" onclick="chq(${p.id},'${p.name.replace(/'/g,"\\'")}',${p.price},1,event)">🛒 أضف</button>`}
            </div></div></div>`; }

        function renderAll() { document.getElementById('drinksGrid').innerHTML = data.drinks.map(card).join('');
            document.getElementById('foodGrid').innerHTML = data.food.map(card).join('');
            document.getElementById('specialGrid').innerHTML = data.special.map(card).join('');
            document.getElementById('s1').textContent = data.drinks.length;
            document.getElementById('s2').textContent = data.food.length;
            document.getElementById('s3').textContent = data.special.length; }

        function chq(id, n, p, d, e) { if (e) e.stopPropagation();
            const ex = cart.find(i => i.id === id); if (ex) { ex.quantity += d; if (ex.quantity <= 0) cart = cart.filter(i =>
                    i.id !== id); } else if (d > 0) { cart.push({ id, name: n, price: p, quantity: d }); }
            sc();
            renderAll(); if (d > 0) toast('✅ ' + n); }

        function sc() { localStorage.setItem('MFC_C', JSON.stringify(cart));
            updateCartBadge(); }

        function updateCartBadge() { const c = cart.reduce((s, i) => s + i.quantity, 0);
            const b = document.getElementById('cartBadge');
            const f = document.getElementById('fCart');
            b.textContent = c;
            b.style.display = c > 0 ? 'flex' : 'none'; if (c > 0) f.classList.add('show');
            else f.classList.remove('show'); }

        function openCart() { document.getElementById('cartModal').classList.add('active');
            renCart(); }

        function closeCart() { document.getElementById('cartModal').classList.remove('active'); }

        function renCart() { const c = document.getElementById('cartItems');
            const t = document.getElementById('cartTotal'); if (cart.length === 0) { c.innerHTML =
                    '<div style="text-align:center;padding:35px;color:#555;"><div style="font-size:3.5em;">🛒</div><p>فارغة</p></div>';
                    t.textContent = 'الإجمالي: 0 ج.م'; return; } let total = 0;
            c.innerHTML = cart.map(i => { const it = i.price * i.quantity;
                total += it; return `<div class="cart-item"><div class="cart-item-info"><span class="cart-item-name">${i.name} ×${i.quantity}</span><br><span class="cart-item-price">${it} ج.م</span></div><button class="cart-remove" onclick="remCart(${i.id})">🗑️</button></div>`; })
                .join('');
            t.textContent = 'الإجمالي: ' + total + ' ج.م'; }

        function remCart(id) { cart = cart.filter(i => i.id !== id);
            sc();
            renderAll();
            renCart(); }

        function selPay(m, el) { selPayM = m;
            document.querySelectorAll('#payOpts .pay-opt').forEach(o => o.classList.remove('selected'));
            el.classList.add('selected'); }

        function checkout() { if (cart.length === 0) { toast('⚠️ فارغة!', true); return; } const total = cart.reduce((s, i) =>
                s + (i.price * i.quantity), 0);
            const pn = { cash: 'نقداً', vodafone: 'فودافون كاش' };
            const sum = cart.map(i => `• ${i.name} ×${i.quantity} = ${i.price*i.quantity} ج.م`).join('\n');
            const msg =
                `🛒 *طلب - كافيه مصطفى*\n━━━━\n${sum}\n━━━━\n💰 *الإجمالي:* ${total} ج.م\n💳 *الدفع:* ${pn[selPayM]}\n📞 ${PHONE}\n━━━━\n🙏 شكراً! ☕`;
            const url = `https://wa.me/${WA_NUM}?text=${encodeURIComponent(msg)}`;
            toast('🎉 جاري الواتساب...');
            cart = [];
            sc();
            renderAll();
            closeCart();
            setTimeout(() => open(url, '_blank'), 600); }

        function openWa() { open(`https://wa.me/${WA_NUM}?text=مرحباً كافيه مصطفى`, '_blank'); }

        // الأدمن
        function togAdmin() { if (isAdmin) { const p = document.getElementById('adminPanel');
                p.classList.toggle('active'); if (p.classList.contains('active')) { renAdminList();
                    p.scrollIntoView({ behavior: 'smooth' }); } } else toast('❌ للأدمن فقط!', true); }

        function adminAdd() { if (!isAdmin) return;
            const c = document.getElementById('adminCat').value;
            const n = document.getElementById('adminName').value.trim();
            const d = document.getElementById('adminDesc').value.trim();
            const p = parseFloat(document.getElementById('adminPrice').value);
            const o = parseFloat(document.getElementById('adminOld').value) || 0;
            const e = document.getElementById('adminEmoji').value.trim();
            const i = document.getElementById('adminImg').value.trim(); if (!n || !d || isNaN(p) || p <= 0) { toast(
                '⚠️ بيانات ناقصة', true); return; } const ids = [...data.drinks, ...data.food, ...data.special].map(x => x
                .id);
            const nid = ids.length > 0 ? Math.max(...ids) + 1 : 1;
            data[c].push({ id: nid, name: n, desc: d, price: p, oldPrice: o, emoji: e || '🍽️', img: i });
            sd();
            renderAll();
            renAdminList();
            ['adminName', 'adminDesc', 'adminPrice', 'adminOld', 'adminEmoji', 'adminImg'].forEach(x => document
                .getElementById(x).value = '');
            toast('✅ تمت الإضافة'); }

        function adminDel(c, id) { if (!isAdmin) return;
            const p = data[c].find(x => x.id === id); if (!confirm('حذف "' + p?.name + '"؟')) return;
            data[c] = data[c].filter(x => x.id !== id);
            sd();
            renderAll();
            renAdminList();
            toast('🗑️ تم الحذف'); }

        function renAdminList() { const c = document.getElementById('adminList');
            const all = [...data.drinks.map(p => ({ ...p, cat: 'drinks', ic: '🥤' })), ...data.food.map(p => ({ ...p,
                cat: 'food', ic: '🍽️' })), ...data.special.map(p => ({ ...p, cat: 'special', ic: '🍷' })), ];
            c.innerHTML = all.map(p =>
                `<div class="admin-item"><span>${p.ic} ${p.emoji||''} ${p.name} - <b style="color:var(--gold)">${p.price}ج.م</b></span><button class="btn-del" onclick="adminDel('${p.cat}',${p.id})">🗑️</button></div>`
                ).join(''); }

        function adminReset() { if (!isAdmin) return; if (!confirm('⚠️ إعادة ضبط؟')) return;
            localStorage.removeItem('MFC_D');
            data = defData();
            sd();
            renderAll();
            renAdminList();
            toast('🔄 تم الضبط'); }

        function adminExport() { if (!isAdmin) return;
            const b = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const a = document.createElement('a');
            a.href = URL.createObjectURL(b);
            a.download = 'mustafa_backup.json';
            a.click();
            toast('📤 تم التصدير'); }

        function scrollToS(id) { document.getElementById(id).scrollIntoView({ behavior: 'smooth' }); }

        function scrollToTop() { scrollTo({ top: 0, behavior: 'smooth' }); }
        document.getElementById('cartModal').addEventListener('click', function(e) { if (e.target === this) closeCart
        (); });

        // بدء التشغيل
        function init() { if (!localStorage.getItem('MFC_D')) sd();
            const users = JSON.parse(localStorage.getItem('MFC_U') || '[]'); if (!users.find(u => u.username
                    .toLowerCase() === ADMIN_USER.toLowerCase())) { users.push(
