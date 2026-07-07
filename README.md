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
            --orange: #ffa502;
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
            scroll-behavior: smooth;
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
            gap: 10px;
            margin-bottom: 22px;
        }
        .auth-tab {
            flex: 1;
            padding: 13px;
            background: transparent;
            border: 2px solid rgba(212, 168, 83, 0.3);
            color: var(--gold);
            border-radius: 12px;
            cursor: pointer;
            font-weight: 900;
            font-size: 1em;
            transition: var(--transition);
            text-align: center;
        }
        .auth-tab.active {
            background: var(--gold);
            color: #1a1a1a;
            border-color: var(--gold);
            box-shadow: 0 5px 25px rgba(212, 168, 83, 0.3);
        }
        .auth-tab:hover:not(.active) {
            border-color: var(--gold-light);
            background: rgba(212, 168, 83, 0.05);
        }
        .form-block {
            display: none;
        }
        .form-block.active {
            display: block;
            animation: fadeInUp 0.4s ease-out;
        }
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(15px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
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
            border-radius: 12px;
            font-size: 1.15em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            letter-spacing: 1px;
        }
        .btn-auth:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(212, 168, 83, 0.4);
        }
        .btn-auth:active {
            transform: scale(0.95);
        }
        .error-msg {
            color: var(--red);
            text-align: center;
            margin: 10px 0;
            display: none;
            font-weight: bold;
            font-size: 0.88em;
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
        .success-msg {
            color: var(--green);
            text-align: center;
            margin: 10px 0;
            display: none;
            font-weight: bold;
            font-size: 0.88em;
        }
        .auth-footer {
            text-align: center;
            margin-top: 18px;
            color: #555;
            font-size: 0.82em;
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
            gap: 10px;
        }
        .logo-wrap {
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            transition: var(--transition);
        }
        .logo-wrap:hover {
            transform: scale(1.05);
        }
        .logo-icon {
            font-size: 2em;
            animation: floatLogo 3s ease-in-out infinite;
        }
        .logo-text {
            font-size: 1.4em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 1px;
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
            padding: 10px 18px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.85em;
            transition: var(--transition);
            white-space: nowrap;
        }
        .nav-btn:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(212, 168, 83, 0.3);
        }
        .cart-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 11px 22px;
            border-radius: 50px;
            font-weight: 900;
            cursor: pointer;
            position: relative;
            transition: var(--transition);
            font-size: 0.95em;
        }
        .cart-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(212, 168, 83, 0.45);
        }
        .cart-badge {
            position: absolute;
            top: -10px;
            right: -10px;
            background: var(--red);
            color: #fff;
            border-radius: 50%;
            width: 26px;
            height: 26px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.72em;
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
        .user-tag {
            background: rgba(165, 94, 234, 0.15);
            border: 1px solid var(--purple);
            color: var(--purple);
            padding: 10px 18px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 0.85em;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        .logout-btn {
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
        .logout-btn:hover {
            background: var(--red);
            color: #fff;
            transform: translateY(-2px);
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
            max-width: 500px;
            margin: 0 auto;
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
            background: linear-gradient(90deg, transparent, var(--gold), var(--gold-light), var(--gold), transparent);
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
            box-shadow: 0 18px 45px rgba(212, 168, 83, 0.25);
        }
        .product-card .badge {
            position: absolute;
            top: 12px;
            left: 12px;
            background: var(--red);
            color: #fff;
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 0.75em;
            font-weight: 900;
            z-index: 2;
            animation: pulseBadge 1.5s infinite;
        }
        @keyframes pulseBadge {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(255, 71, 87, 0.5);
            }
            50% {
                box-shadow: 0 0 0 15px rgba(255, 71, 87, 0);
            }
        }
        .img-wrap {
            width: 100%;
            height: 210px;
            overflow: hidden;
            position: relative;
        }
        .img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.6s;
        }
        .product-card:hover .img-wrap img {
            transform: scale(1.12);
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
            padding: 18px;
        }
        .info h3 {
            font-size: 1.1em;
            font-weight: 900;
            margin-bottom: 4px;
        }
        .info .desc {
            color: #7a6a55;
            font-size: 0.82em;
            margin-bottom: 12px;
            line-height: 1.4;
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
            margin-left: 6px;
        }
        .cur-p {
            font-size: 1.35em;
            font-weight: 900;
            color: var(--gold);
        }
        .add-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 10px 20px;
            border-radius: 10px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9em;
        }
        .add-btn:hover {
            transform: scale(1.06);
            box-shadow: 0 6px 20px rgba(212, 168, 83, 0.4);
        }
        .add-btn:active {
            transform: scale(0.94);
        }
        .qty-row {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .qty-b {
            background: var(--bg3);
            border: 2px solid var(--gold);
            color: var(--gold);
            width: 32px;
            height: 32px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.1em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .qty-b:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: scale(1.1);
        }
        .qty-v {
            font-size: 1.1em;
            font-weight: 900;
            min-width: 26px;
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
            padding: 30px;
            width: 92%;
            max-width: 620px;
            max-height: 85vh;
            overflow-y: auto;
            position: relative;
            animation: popIn 0.4s ease-out;
            box-shadow: 0 0 80px rgba(212, 168, 83, 0.2);
        }
        .modal-close {
            position: absolute;
            top: 14px;
            left: 18px;
            background: none;
            border: none;
            color: var(--gold);
            font-size: 2em;
            cursor: pointer;
            transition: var(--transition);
        }
        .modal-close:hover {
            color: var(--red);
            transform: rotate(90deg) scale(1.2);
        }
        .modal-box h2 {
            text-align: center;
            color: var(--gold);
            font-size: 1.8em;
            margin-bottom: 20px;
        }
        .cart-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 13px;
            border-bottom: 1px solid #222;
        }
        .cart-item-info {
            flex: 1;
        }
        .cart-item-name {
            font-weight: 900;
            color: var(--text);
        }
        .cart-item-price {
            color: var(--gold);
            font-size: 0.85em;
        }
        .cart-remove {
            background: var(--red);
            color: #fff;
            border: none;
            padding: 8px 14px;
            border-radius: 8px;
            cursor: pointer;
            transition: var(--transition);
        }
        .cart-remove:hover {
            background: #d63031;
            transform: scale(1.08);
        }
        .cart-total {
            text-align: center;
            font-size: 1.5em;
            font-weight: 900;
            color: var(--gold);
            margin: 18px 0;
            text-shadow: 0 0 25px rgba(212, 168, 83, 0.4);
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
            padding: 15px;
            border-radius: 12px;
            cursor: pointer;
            text-align: center;
            font-size: 1.8em;
            transition: var(--transition);
            flex: 1;
            min-width: 90px;
        }
        .pay-opt.selected {
            border-color: var(--gold);
            background: #1a1008;
            box-shadow: 0 0 25px rgba(212, 168, 83, 0.3);
        }
        .pay-opt span {
            display: block;
            font-size: 0.28em;
            margin-top: 4px;
            color: var(--text);
        }
        .checkout-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #2ed573, #1dd1a1);
            color: #000;
            border: none;
            border-radius: 12px;
            font-size: 1.2em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            letter-spacing: 1px;
        }
        .checkout-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 35px rgba(46, 213, 115, 0.4);
        }

        /* ============ لوحة الأدمن ============ */
        .admin-panel {
            display: none;
            background: linear-gradient(160deg, #0d0d0d, #181818);
            border: 2px solid var(--purple);
            border-radius: 22px;
            padding: 28px;
            margin: 30px 0;
            animation: fadeIn 0.5s;
        }
        .admin-panel.active {
            display: block;
        }
        .admin-panel h2 {
            color: var(--purple);
            text-align: center;
            font-size: 1.7em;
            margin-bottom: 20px;
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
            padding: 18px;
        }
        .admin-card h3 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 12px;
            font-size: 1.1em;
        }
        .admin-card input,
        .admin-card select {
            width: 100%;
            padding: 10px;
            margin-bottom: 8px;
            background: #0a0a0a;
            border: 1px solid #222;
            border-radius: 8px;
            color: var(--text);
            font-family: inherit;
            font-size: 0.88em;
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
            font-size: 0.9em;
        }
        .btn-add {
            background: var(--green);
            color: #000;
        }
        .btn-add:hover {
            box-shadow: 0 6px 20px rgba(46, 213, 115, 0.3);
        }
        .btn-del {
            background: var(--red);
            color: #fff;
            width: auto;
            padding: 6px 12px;
            font-size: 0.75em;
        }
        .btn-del:hover {
            background: #d63031;
        }
        .btn-reset {
            background: var(--orange);
            color: #000;
        }
        .btn-export {
            background: var(--purple);
            color: #fff;
        }
        .admin-list {
            max-height: 330px;
            overflow-y: auto;
        }
        .admin-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px;
            border-bottom: 1px solid #1a1a1a;
            font-size: 0.82em;
        }
        .admin-item span {
            color: var(--text);
        }
        .admin-item b {
            color: var(--gold);
        }

        /* ============ أزرار عائمة ============ */
        .floats {
            position: fixed;
            bottom: 28px;
            left: 28px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 100;
        }
        .fbtn {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: none;
            cursor: pointer;
            font-size: 1.3em;
            transition: var(--transition);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .fbtn:hover {
            transform: scale(1.15);
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
                box-shadow: 0 0 0 20px rgba(37, 211, 102, 0);
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
                transform: scale(1.25);
            }
            100% {
                transform: scale(1);
            }
        }

        /* ============ توست ============ */
        .toast-cont {
            position: fixed;
            top: 85px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 7px;
            align-items: center;
            pointer-events: none;
        }
        .toast {
            background: #1a1a1a;
            border: 1px solid var(--gold);
            color: var(--text);
            padding: 13px 28px;
            border-radius: 50px;
            font-weight: 900;
            animation: tIn 0.4s, tOut 0.4s 2.5s forwards;
            pointer-events: auto;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5);
        }
        @keyframes tIn {
            from {
                transform: translateY(-45px);
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
            padding: 40px 20px;
            background: #050505;
            border-top: 1px solid rgba(212, 168, 83, 0.1);
            margin-top: 50px;
            position: relative;
            z-index: 1;
        }
        .footer h3 {
            color: var(--gold);
            font-size: 1.7em;
            margin-bottom: 6px;
        }
        .footer .phone {
            color: var(--gold);
            font-size: 1.15em;
            margin: 6px 0;
            direction: ltr;
            display: inline-block;
            font-weight: 900;
        }
        .footer .social {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin: 16px 0;
        }
        .footer .social-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1em;
            cursor: pointer;
            transition: var(--transition);
        }
        .footer .social-icon:hover {
            border-color: var(--gold);
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-5px);
        }

        /* ============ Responsive ============ */
        @media (max-width: 768px) {
            .navbar {
                justify-content: center;
                padding: 8px;
            }
            .nav-btn {
                padding: 7px 12px;
                font-size: 0.74em;
            }
            .products-grid {
                grid-template-columns: 1fr 1fr;
                gap: 12px;
            }
            .img-wrap,
            .img-fb {
                height: 150px;
            }
            .img-fb {
                font-size: 3.5em;
            }
            .section-title {
                font-size: 1.4em;
            }
            .hero h1 {
                font-size: 1.8em;
            }
            .auth-box {
                padding: 25px 18px;
            }
            .admin-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>

    <!-- جسيمات -->
    <canvas id="particlesCanvas"></canvas>

    <!-- ============ صفحة المصادقة ============ -->
    <div id="authPage">
        <div class="auth-box">
            <div class="auth-logo">☕</div>
            <h2>كافيه مصطفى</h2>
            <p class="subtitle">سجل دخولك أو أنشئ حساباً جديداً للمتابعة</p>
            <div class="auth-tabs">
                <button class="auth-tab active" id="tabLogin" onclick="switchTab('login')">🚪 تسجيل الدخول</button>
                <button class="auth-tab" id="tabRegister" onclick="switchTab('register')">📝 إنشاء حساب</button>
            </div>

            <!-- فورم تسجيل الدخول -->
            <div class="form-block active" id="loginFormBlock">
                <div class="form-group">
                    <label>👤 اسم المستخدم</label>
                    <input type="text" id="loginUser" placeholder="أدخل اسم المستخدم">
                </div>
                <div class="form-group">
                    <label>🔒 كلمة المرور</label>
                    <input type="password" id="loginPass" placeholder="أدخل كلمة المرور">
                </div>
                <div class="error-msg" id="loginErr"></div>
                <button class="btn-auth" onclick="doLogin()">🚪 دخول إلى الموقع</button>
            </div>

            <!-- فورم إنشاء حساب -->
            <div class="form-block" id="registerFormBlock">
                <div class="form-group">
                    <label>👤 اسم المستخدم</label>
                    <input type="text" id="regUser" placeholder="اختر اسم مستخدم">
                </div>
                <div class="form-group">
                    <label>📧 البريد الإلكتروني</label>
                    <input type="email" id="regEmail" placeholder="أدخل بريدك الإلكتروني">
                </div>
                <div class="form-group">
                    <label>🔒 كلمة المرور</label>
                    <input type="password" id="regPass" placeholder="كلمة مرور قوية (6 أحرف على الأقل)">
                </div>
                <div class="form-group">
                    <label>🔒 تأكيد كلمة المرور</label>
                    <input type="password" id="regPass2" placeholder="أعد كتابة كلمة المرور">
                </div>
                <div class="error-msg" id="regErr"></div>
                <div class="success-msg" id="regOk"></div>
                <button class="btn-auth" onclick="doRegister()">📝 إنشاء حساب جديد</button>
            </div>
            <p class="auth-footer">كافيه مصطفى © 2026 - جميع الحقوق محفوظة</p>
        </div>
    </div>

    <!-- ============ التطبيق الرئيسي ============ -->
    <div id="mainApp">
        <nav class="navbar">
            <div class="logo-wrap" onclick="scrollToTop()">
                <span class="logo-icon">☕</span>
                <span class="logo-text">كافيه مصطفى</span>
            </div>
            <div class="nav-actions">
                <button class="nav-btn" onclick="scrollToSection('drinksSection')">🥤 مشروبات</button>
                <button class="nav-btn" onclick="scrollToSection('foodSection')">🍽️ مأكولات</button>
                <button class="nav-btn" onclick="scrollToSection('specialSection')">🍷 مشروبات خاصة</button>
                <button class="nav-btn" onclick="scrollToSection('paymentSection')">💳 الدفع</button>
                <span class="user-tag" id="userTag">👤 مستخدم</span>
                <button class="logout-btn" onclick="doLogout()">🚪 خروج</button>
                <button class="cart-btn" onclick="openCartModal()">
                    🛒 السلة <span class="cart-badge" id="cartBadge">0</span>
                </button>
            </div>
        </nav>

        <div class="container">
            <div class="hero">
                <h1>☕ كافيه مصطفى</h1>
                <p>أجود المشروبات والمأكولات - اطلب أونلاين واستمتع</p>
            </div>

            <div id="drinksSection">
                <h2 class="section-title">🥤 المشروبات الساخنة والباردة</h2>
                <div class="products-grid" id="drinksGrid"></div>
            </div>

            <div id="foodSection">
                <h2 class="section-title">🍽️ المأكولات والحلويات</h2>
                <div class="products-grid" id="foodGrid"></div>
            </div>

            <div id="specialSection">
                <h2 class="section-title">🍷 مشروبات خاصة</h2>
                <div class="products-grid" id="specialGrid"></div>
            </div>

            <div id="paymentSection">
                <h2 class="section-title">💳 طرق الدفع</h2>
                <div style="display:flex;flex-wrap:wrap;gap:14px;justify-content:center;padding:20px;">
                    <div style="background:#1a1a1a;border:2px solid var(--gold);border-radius:16px;padding:28px;text-align:center;font-size:2.8em;flex:1;min-width:140px;">💵<br><span style="font-size:0.26em;color:var(--text);">نقداً عند الاستلام</span></div>
                    <div style="background:#1a1a1a;border:2px solid var(--gold);border-radius:16px;padding:28px;text-align:center;font-size:2.8em;flex:1;min-width:140px;">📱<br><span style="font-size:0.26em;color:var(--text);">فودافون كاش<br><span dir="ltr" style="color:var(--gold);font-size:1.2em;">01026966717</span></span></div>
                </div>
            </div>

            <!-- لوحة الأدمن -->
            <div class="admin-panel" id="adminPanel">
                <h2>👑 لوحة تحكم الأدمن - Mustafa</h2>
                <div class="admin-grid">
                    <div class="admin-card">
                        <h3>➕ إضافة منتج جديد</h3>
                        <select id="adminCat">
                            <option value="drinks">🥤 مشروبات</option>
                            <option value="food">🍽️ مأكولات</option>
                            <option value="special">🍷 مشروبات خاصة</option>
                        </select>
                        <input type="text" id="adminName" placeholder="اسم المنتج">
                        <input type="text" id="adminDesc" placeholder="وصف المنتج">
                        <input type="number" id="adminPrice" placeholder="السعر (ج.م)">
                        <input type="number" id="adminOld" placeholder="السعر قبل الخصم (اختياري)">
                        <input type="text" id="adminEmoji" placeholder="إيموجي (☕ 🍰 🍷)">
                        <input type="text" id="adminImg" placeholder="رابط الصورة">
                        <button class="btn-add" onclick="adminAddProduct()">✅ إضافة المنتج</button>
                    </div>
                    <div class="admin-card">
                        <h3>📋 جميع المنتجات</h3>
                        <div class="admin-list" id="adminList"></div>
                    </div>
                    <div class="admin-card">
                        <h3>⚙️ إحصائيات وأدوات</h3>
                        <p style="color:var(--gold);margin-bottom:6px;">🥤 مشروبات: <b id="stat1">0</b></p>
                        <p style="color:var(--gold);margin-bottom:6px;">🍽️ مأكولات: <b id="stat2">0</b></p>
                        <p style="color:var(--gold);margin-bottom:12px;">🍷 خاصة: <b id="stat3">0</b></p>
                        <button class="btn-reset" onclick="adminResetAll()">🔄 إعادة ضبط البيانات</button>
                        <button class="btn-export" onclick="adminExportData()">📤 تصدير البيانات</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="footer">
            <h3>☕ كافيه مصطفى</h3>
            <p style="color:var(--text2);">📍 شارع النخيل، مدينة القهوة</p>
            <p class="phone">📞 01026966717</p>
            <div class="social">
                <div class="social-icon">📘</div><div class="social-icon">📷</div><div class="social-icon">🐦</div>
            </div>
            <p style="color:#555;margin-top:14px;">© 2026 كافيه مصطفى - Developed by Mustafa 👑</p>
        </div>
    </div>

    <!-- مودال السلة -->
    <div class="modal-overlay" id="cartModal">
        <div class="modal-box">
            <button class="modal-close" onclick="closeCartModal()">✕</button>
            <h2>🛒 سلة المشتريات</h2>
            <div id="cartItems"></div>
            <div class="cart-total" id="cartTotal">الإجمالي: 0 ج.م</div>
            <p style="text-align:center;color:var(--gold);margin:10px 0;">اختر طريقة الدفع:</p>
            <div class="pay-opts" id="payOpts">
                <div class="pay-opt selected" onclick="selectPayment('cash', this)">💵<span>نقداً عند الاستلام</span></div>
                <div class="pay-opt" onclick="selectPayment('vodafone', this)">📱<span>فودافون كاش</span></div>
            </div>
            <button class="checkout-btn" onclick="doCheckout()">✅ تأكيد الطلب وإرسال واتساب</button>
        </div>
    </div>

    <!-- أزرار عائمة -->
    <div class="floats">
        <button class="fbtn fbtn-wa" onclick="openWhatsApp()" title="واتساب">💬</button>
        <button class="fbtn fbtn-admin" id="fbtnAdmin" onclick="toggleAdmin()" title="لوحة الأدمن">👑</button>
        <button class="fbtn fbtn-cart" id="fbtnCart" onclick="openCartModal()" title="السلة">🛒</button>
    </div>

    <!-- توست -->
    <div class="toast-cont" id="toastCont"></div>

    <script>
        // ==================== الثوابت ====================
        const ADMIN_USERNAME = 'Mustafa';
        const ADMIN_PASSWORD = '123456';
        const WHATSAPP_NUMBER = '201026966717';
        const PHONE_DISPLAY = '01026966717';

        // ==================== البيانات ====================
        function getDefaultData() {
            return {
                drinks: [
                    { id: 1, name: 'قهوة تركية', desc: 'قهوة تركية أصلية على الرمل', price: 25, oldPrice: 0, emoji: '☕',
                        img: 'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400&h=300&fit=crop' },
                    { id: 2, name: 'لاتيه كريمي', desc: 'لاتيه بحليب طازج وفن اللاتيه', price: 35, oldPrice: 42, emoji: '🥛',
                        img: 'https://images.unsplash.com/photo-1570968915860-54d5c301fa9f?w=400&h=300&fit=crop' },
                    { id: 3, name: 'كابتشينو إيطالي', desc: 'كابتشينو برغوة حليب كثيفة', price: 30, oldPrice: 0, emoji: '☕',
                        img: 'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400&h=300&fit=crop' },
                    { id: 4, name: 'شاي كرك', desc: 'شاي كرك هندي أصلي', price: 20, oldPrice: 25, emoji: '🍵',
                        img: 'https://images.unsplash.com/photo-1564890369478-c89ca6d9cde9?w=400&h=300&fit=crop' },
                    { id: 5, name: 'موكا مثلجة', desc: 'موكا باردة بصوص الشوكولاتة', price: 40, oldPrice: 0, emoji: '🧊',
                        img: 'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400&h=300&fit=crop' },
                    { id: 6, name: 'عصير مانجو', desc: 'مانجو طبيعي 100%', price: 30, oldPrice: 0, emoji: '🥭',
                        img: 'https://images.unsplash.com/photo-1546173159-315724a31696?w=400&h=300&fit=crop' },
                ],
                food: [
                    { id: 101, name: 'كرواسون زبدة', desc: 'كرواسون فرنسي طازج', price: 30, oldPrice: 0, emoji: '🥐',
                        img: 'https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=400&h=300&fit=crop' },
                    { id: 102, name: 'تشيز كيك التوت', desc: 'تشيز كيك بالتوت الطازج', price: 45, oldPrice: 55, emoji: '🍰',
                        img: 'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400&h=300&fit=crop' },
                    { id: 103, name: 'وافل شوكولاتة', desc: 'وافل بلجيكي بصوص الشوكولاتة', price: 40, oldPrice: 0, emoji: '🧇',
                        img: 'https://images.unsplash.com/photo-1558584724-0e4d32ca55a6?w=400&h=300&fit=crop' },
                    { id: 104, name: 'بان كيك بالعسل', desc: 'بان كيك أمريكي هش', price: 35, oldPrice: 0, emoji: '🥞',
                        img: 'https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=400&h=300&fit=crop' },
                ],
                special: [
                    { id: 201, name: 'مشروب خاص 1', desc: 'مشروب مميز بنكهة فاخرة', price: 50, oldPrice: 0, emoji: '🍷',
                        img: 'https://images.unsplash.com/photo-1474722883777-792e7990302f?w=400&h=300&fit=crop' },
                    { id: 202, name: 'مشروب خاص 2', desc: 'مشروب فاخر للمناسبات', price: 65, oldPrice: 80, emoji: '🥂',
                        img: 'https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?w=400&h=300&fit=crop' },
                ],
            };
        }

        function loadData() {
            const saved = localStorage.getItem('MFC_DATA_FINAL');
            if (saved) { try { return JSON.parse(saved); } catch (e) {} }
            return getDefaultData();
        }

        function saveData() { localStorage.setItem('MFC_DATA_FINAL', JSON.stringify(cafeData)); }

        let cafeData = loadData();
        let cart = JSON.parse(localStorage.getItem('MFC_CART_FINAL') || '[]');
        let selectedPaymentMethod = 'cash';
        let isAdminLoggedIn = false;
        let currentUser = null;

        // ==================== جسيمات ====================
        const pCanvas = document.getElementById('particlesCanvas');
        const pCtx = pCanvas.getContext('2d');
        pCanvas.width = innerWidth;
        pCanvas.height = innerHeight;
        const particlesArr = [];
        class Particle {
            constructor() { this.reset();
                this.y = Math.random() * pCanvas.height; }
            reset() { this.x = Math.random() * pCanvas.width;
                this.y = -10;
                this.size = Math.random() * 3 + 1;
                this.speedY = Math.random() * 1.5 + 0.3;
                this.speedX = (Math.random() - 0.5) * 0.4;
                this.opacity = Math.random() * 0.6 + 0.2;
                this.color = ['#d4a853', '#f0d78c', '#b8922e'][Math.floor(Math.random() * 3)]; }
            update() { this.y += this.speedY;
                this.x += this.speedX; if (this.y > pCanvas.height + 10) this.reset(); }
            draw() { pCtx.beginPath();
                pCtx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                pCtx.fillStyle = this.color;
                pCtx.globalAlpha = this.opacity;
                pCtx.fill();
                pCtx.globalAlpha = 1; }
        }
        for (let i = 0; i < 45; i++) particlesArr.push(new Particle());

        function animateParticles() { pCtx.clearRect(0, 0, pCanvas.width, pCanvas.height);
            particlesArr.forEach(p => { p.update();
                p.draw(); });
            requestAnimationFrame(animateParticles); }
        animateParticles();
        addEventListener('resize', () => { pCanvas.width = innerWidth;
            pCanvas.height = innerHeight; });

        // ==================== توست ====================
        function showToast(msg, isError = false) {
            const container = document.getElementById('toastCont');
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.style.borderColor = isError ? 'var(--red)' : 'var(--gold)';
            toast.textContent = msg;
            container.appendChild(toast);
            setTimeout(() => toast.remove(), 2900);
        }

        // ==================== المصادقة ====================
        function switchTab(tab) {
            const tabLogin = document.getElementById('tabLogin');
            const tabRegister = document.getElementById('tabRegister');
            const loginForm = document.getElementById('loginFormBlock');
            const registerForm = document.getElementById('registerFormBlock');

            // إخفاء الرسائل
            document.getElementById('loginErr').style.display = 'none';
            document.getElementById('regErr').style.display = 'none';
            document.getElementById('regOk').style.display = 'none';

            if (tab === 'login') {
                tabLogin.classList.add('active');
                tabRegister.classList.remove('active');
                loginForm.classList.add('active');
                registerForm.classList.remove('active');
            } else {
                tabRegister.classList.add('active');
                tabLogin.classList.remove('active');
                registerForm.classList.add('active');
                loginForm.classList.remove('active');
            }
        }

        function doLogin() {
            const username = document.getElementById('loginUser').value.trim();
            const password = document.getElementById('loginPass').value.trim();
            const errorEl = document.getElementById('loginErr');

            if (!username || !password) {
                errorEl.textContent = '⚠️ الرجاء ملء جميع الحقول';
                errorEl.style.display = 'block';
                return;
            }

            const users = JSON.parse(localStorage.getItem('MFC_USERS_FINAL') || '[]');
            const user = users.find(u => u.username.toLowerCase() === username.toLowerCase() && u.password === password);

            if (user) {
                currentUser = user;
                isAdminLoggedIn = user.isAdmin || false;
                localStorage.setItem('MFC_CURRENT_USER_FINAL', JSON.stringify(user));
                showMainApp();
                showToast('✅ مرحباً ' + user.username + '!');
            } else {
                errorEl.textContent = '❌ اسم المستخدم أو كلمة المرور غير صحيحة';
                errorEl.style.display = 'block';
            }
        }

        function doRegister() {
            const username = document.getElementById('regUser').value.trim();
            const email = document.getElementById('regEmail').value.trim();
            const password = document.getElementById('regPass').value.trim();
            const password2 = document.getElementById('regPass2').value.trim();
            const errorEl = document.getElementById('regErr');
            const successEl = document.getElementById('regOk');

            errorEl.style.display = 'none';
            successEl.style.display = 'none';

            if (!username || !email || !password || !password2) {
                errorEl.textContent = '⚠️ الرجاء ملء جميع الحقول';
                errorEl.style.display = 'block';
                return;
            }
            if (password !== password2) {
                errorEl.textContent = '❌ كلمتا المرور غير متطابقتين';
                errorEl.style.display = 'block';
                return;
            }
            if (password.length < 6) {
                errorEl.textContent = '❌ كلمة المرور يجب أن تكون 6 أحرف على الأقل';
                errorEl.style.display = 'block';
                return;
            }
            if (!email.includes('@') || !email.includes('.')) {
                errorEl.textContent = '❌ بريد إلكتروني غير صالح';
                errorEl.style.display = 'block';
                return;
            }
            if (username.toLowerCase() === ADMIN_USERNAME.toLowerCase()) {
                errorEl.textContent = '❌ هذا الاسم محجوز للأدمن فقط';
                errorEl.style.display = 'block';
                return;
            }

            const users = JSON.parse(localStorage.getItem('MFC_USERS_FINAL') || '[]');
            if (users.find(u => u.username.toLowerCase() === username.toLowerCase())) {
                errorEl.textContent = '❌ اسم المستخدم موجود مسبقاً';
                errorEl.style.display = 'block';
                return;
            }
            if (users.find(u => u.email.toLowerCase() === email.toLowerCase())) {
                errorEl.textContent = '❌ البريد الإلكتروني مستخدم مسبقاً';
                errorEl.style.display = 'block';
                return;
            }

            const isAdmin = (username.toLowerCase() === ADMIN_USERNAME.toLowerCase());
            const newUser = { username, email, password, isAdmin, createdAt: new Date().toISOString() };
            users.push(newUser);
            localStorage.setItem('MFC_USERS_FINAL', JSON.stringify(users));

            successEl.textContent = '✅ تم إنشاء الحساب بنجاح! يمكنك الآن تسجيل الدخول';
            successEl.style.display = 'block';
            document.getElementById('regUser').value = '';
            document.getElementById('regEmail').value = '';
            document.getElementById('regPass').value = '';
            document.getElementById('regPass2').value = '';

            setTimeout(() => switchTab('login'), 1600);
        }

        function showMainApp() {
            document.getElementById('authPage').classList.add('hidden');
            document.getElementById('mainApp').classList.add('visible');
            document.getElementById('userTag').t
