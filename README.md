<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evil Bar - إيفل بار</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.rtl.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <style>
        :root {
            --bg: #0a0a0a;
            --bg2: #1a1a1a;
            --gold: #D4AF37;
            --gold2: #FFD700;
            --brown: #4E342E;
            --white: #fff;
            --gray: #999;
            --red: #dc3545;
            --green: #28a745;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background: var(--bg);
            color: var(--white);
            font-family: 'Segoe UI', Tahoma, sans-serif;
            min-height: 100vh;
        }

        /* ========== AUTH PAGE ========== */
        .auth-container {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 50%, #0a0a0a 100%);
            padding: 20px;
        }

        .auth-box {
            background: rgba(30, 30, 30, 0.95);
            border: 1px solid rgba(212, 175, 55, 0.3);
            border-radius: 20px;
            padding: 40px;
            width: 100%;
            max-width: 450px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 30px rgba(212,175,55,0.1);
        }

        .auth-logo {
            text-align: center;
            margin-bottom: 30px;
        }

        .auth-logo h1 {
            color: var(--gold);
            font-size: 36px;
            font-weight: 900;
            letter-spacing: 5px;
            text-shadow: 0 0 20px rgba(212,175,55,0.5);
        }

        .auth-logo p {
            color: var(--gray);
            margin-top: 5px;
        }

        .auth-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            padding-bottom: 15px;
        }

        .auth-tab {
            flex: 1;
            padding: 12px;
            text-align: center;
            background: transparent;
            border: 1px solid rgba(255,255,255,0.2);
            color: var(--white);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
        }

        .auth-tab.active {
            background: var(--gold);
            color: #000;
            border-color: var(--gold);
            font-weight: bold;
        }

        .auth-tab:hover {
            border-color: var(--gold);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--gray);
            font-size: 14px;
        }

        .form-control {
            width: 100%;
            padding: 14px 18px;
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 12px;
            color: var(--white);
            font-size: 16px;
            transition: all 0.3s;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 15px rgba(212,175,55,0.2);
            background: rgba(255,255,255,0.08);
        }

        .form-control::placeholder {
            color: rgba(255,255,255,0.3);
        }

        .btn {
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .btn-gold {
            background: linear-gradient(135deg, #B8960C, var(--gold), #FFD700);
            color: #000;
        }

        .btn-gold:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(212,175,55,0.4);
        }

        .btn-outline {
            background: transparent;
            border: 2px solid rgba(255,255,255,0.3);
            color: var(--white);
        }

        .btn-outline:hover {
            border-color: var(--gold);
            color: var(--gold);
        }

        .btn-google {
            background: #fff;
            color: #333;
        }

        .btn-google:hover {
            background: #f5f5f5;
        }

        .btn-danger {
            background: var(--red);
            color: #fff;
        }

        .divider {
            text-align: center;
            margin: 20px 0;
            position: relative;
        }

        .divider::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 0;
            right: 0;
            height: 1px;
            background: rgba(255,255,255,0.2);
        }

        .divider span {
            background: rgba(30,30,30,0.95);
            padding: 0 15px;
            position: relative;
            color: var(--gray);
        }

        .otp-section {
            display: none;
            animation: fadeIn 0.3s;
        }

        .otp-section.show {
            display: block;
        }

        .timer {
            text-align: center;
            color: var(--gold);
            margin: 10px 0;
            font-weight: bold;
        }

        .error-msg {
            color: var(--red);
            font-size: 13px;
            margin-top: 5px;
            display: none;
        }

        .success-msg {
            color: var(--green);
            text-align: center;
            margin: 10px 0;
            display: none;
        }

        /* ========== MAIN APP ========== */
        .main-app {
            display: none;
        }

        .main-app.show {
            display: block;
        }

        /* Navbar */
        .navbar {
            background: rgba(10,10,10,0.95) !important;
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(212,175,55,0.2);
            padding: 12px 0;
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .brand {
            color: var(--gold) !important;
            font-size: 24px;
            font-weight: 900;
            letter-spacing: 3px;
            text-decoration: none;
            text-shadow: 0 0 15px rgba(212,175,55,0.4);
        }

        .nav-link {
            color: var(--white) !important;
            margin: 0 8px;
            transition: 0.3s;
            cursor: pointer;
        }

        .nav-link:hover, .nav-link.active {
            color: var(--gold) !important;
        }

        /* Hero */
        .hero {
            height: 90vh;
            background: linear-gradient(rgba(0,0,0,0.75), rgba(0,0,0,0.9)), url('https://images.unsplash.com/photo-1470337458703-46ad1756a187?w=1920&q=80');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .hero h1 {
            font-size: 72px;
            font-weight: 900;
            color: var(--gold);
            letter-spacing: 8px;
            text-shadow: 0 0 40px rgba(212,175,55,0.6);
            animation: glow 2s infinite;
        }

        @keyframes glow {
            0%,100% { text-shadow: 0 0 20px rgba(212,175,55,0.4); }
            50% { text-shadow: 0 0 40px rgba(212,175,55,0.8), 0 0 60px rgba(212,175,55,0.4); }
        }

        .hero p {
            font-size: 22px;
            color: var(--gray);
            margin: 20px 0 30px;
        }

        /* Section */
        .section {
            padding: 80px 0;
        }

        .section-title {
            text-align: center;
            font-size: 36px;
            font-weight: bold;
            margin-bottom: 50px;
        }

        .gold-text {
            color: var(--gold);
        }

        /* Product Card */
        .product-card {
            background: rgba(30,30,30,0.9);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 16px;
            overflow: hidden;
            transition: all 0.3s;
            height: 100%;
        }

        .product-card:hover {
            transform: translateY(-8px);
            border-color: rgba(212,175,55,0.4);
            box-shadow: 0 15px 40px rgba(0,0,0,0.4);
        }

        .product-img {
            height: 220px;
            overflow: hidden;
            position: relative;
        }

        .product-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: 0.5s;
        }

        .product-card:hover .product-img img {
            transform: scale(1.1);
        }

        .product-badge {
            position: absolute;
            top: 10px;
            left: 10px;
            background: var(--red);
            color: #fff;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
        }

        .product-info {
            padding: 20px;
        }

        .product-info h5 {
            font-size: 18px;
            margin-bottom: 5px;
        }

        .product-info .desc {
            color: var(--gray);
            font-size: 13px;
            margin-bottom: 10px;
        }

        .product-price {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
        }

        .price-old {
            text-decoration: line-through;
            color: var(--gray);
            font-size: 14px;
        }

        .price-new {
            color: var(--gold);
            font-size: 22px;
            font-weight: bold;
        }

        .stars {
            color: var(--gold);
            margin-bottom: 12px;
        }

        .btn-sm {
            padding: 10px 20px;
            font-size: 14px;
            width: auto;
            display: inline-flex;
        }

        /* Category nav */
        .cat-nav {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 40px;
        }

        .cat-btn {
            padding: 12px 24px;
            background: transparent;
            border: 1px solid rgba(255,255,255,0.2);
            color: var(--white);
            border-radius: 50px;
            cursor: pointer;
            transition: 0.3s;
            font-size: 15px;
        }

        .cat-btn:hover, .cat-btn.active {
            background: var(--gold);
            color: #000;
            border-color: var(--gold);
            font-weight: bold;
        }

        /* Cart sidebar */
        .cart-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 2000;
            display: none;
        }

        .cart-overlay.open {
            display: block;
        }

        .cart-sidebar {
            position: fixed;
            top: 0;
            right: -420px;
            width: 400px;
            height: 100%;
            background: #1a1a1a;
            border-left: 1px solid rgba(212,175,55,0.3);
            z-index: 2001;
            transition: right 0.3s;
            padding: 20px;
            overflow-y: auto;
        }

        .cart-sidebar.open {
            right: 0;
        }

        /* Footer */
        footer {
            background: #111;
            border-top: 1px solid rgba(212,175,55,0.2);
            padding: 40px 0 20px;
            text-align: center;
        }

        footer a {
            color: var(--gray);
            text-decoration: none;
            margin: 0 10px;
        }

        footer a:hover {
            color: var(--gold);
        }

        /* Toast */
        .toast-msg {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--gold);
            color: #000;
            padding: 15px 25px;
            border-radius: 10px;
            font-weight: bold;
            z-index: 9999;
            transform: translateX(120%);
            transition: 0.3s;
        }

        .toast-msg.show {
            transform: translateX(0);
        }

        .toast-msg.error {
            background: var(--red);
            color: #fff;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @media (max-width: 768px) {
            .hero h1 { font-size: 36px; letter-spacing: 4px; }
            .hero p { font-size: 16px; }
            .section-title { font-size: 24px; }
            .cart-sidebar { width: 100%; right: -100%; }
            .auth-box { padding: 25px; }
        }
    </style>
</head>
<body>

    <!-- ==================== AUTH PAGE ==================== -->
    <div id="authPage" class="auth-container">
        <div class="auth-box">
            <div class="auth-logo">
                <h1>EVIL BAR</h1>
                <p>أفخم كافيه وبار في المدينة</p>
            </div>

            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchAuthTab('email')">
                    <i class="fas fa-envelope"></i> البريد الإلكتروني
                </button>
                <button class="auth-tab" onclick="switchAuthTab('phone')">
                    <i class="fas fa-phone"></i> رقم الهاتف
                </button>
            </div>

            <!-- Email Login -->
            <div id="emailLogin">
                <div class="form-group">
                    <label>البريد الإلكتروني</label>
                    <input type="email" class="form-control" id="loginEmail" placeholder="example@email.com">
                </div>
                <div class="form-group">
                    <label>كلمة المرور</label>
                    <input type="password" class="form-control" id="loginPassword" placeholder="••••••••">
                </div>
                <div class="form-group" style="display:flex;align-items:center;gap:10px;">
                    <input type="checkbox" id="rememberMe" style="width:auto;">
                    <label style="margin:0;">تذكرني</label>
                </div>
                <button class="btn btn-gold" onclick="loginWithEmail()">
                    <i class="fas fa-sign-in-alt"></i> تسجيل الدخول
                </button>
                <button class="btn btn-google mt-3" onclick="loginWithGoogle()">
                    <i class="fab fa-google"></i> تسجيل الدخول بـ Google
                </button>
            </div>

            <!-- Phone Login -->
            <div id="phoneLogin" style="display:none;">
                <div class="form-group">
                    <label>رقم الهاتف</label>
                    <input type="tel" class="form-control" id="phoneNumber" placeholder="+20 1xx xxxx xxx">
                    <small style="color:var(--gray);">سيتم إرسال رمز تحقق إلى هاتفك</small>
                </div>
                <button class="btn btn-gold" id="sendOtpBtn" onclick="sendOTP()">
                    <i class="fas fa-paper-plane"></i> إرسال رمز التحقق
                </button>
                <div class="otp-section" id="otpSection">
                    <div class="form-group mt-3">
                        <label>رمز التحقق</label>
                        <input type="text" class="form-control" id="otpCode" placeholder="******" maxlength="6">
                        <div class="error-msg" id="otpError">الرمز غير صحيح</div>
                    </div>
                    <div class="timer" id="otpTimer">60 ثانية</div>
                    <button class="btn btn-gold" id="verifyOtpBtn" onclick="verifyOTP()">
                        <i class="fas fa-check"></i> تأكيد الرمز
                    </button>
                    <button class="btn btn-outline mt-2" id="resendOtpBtn" onclick="sendOTP()" disabled>
                        <i class="fas fa-redo"></i> إعادة إرسال
                    </button>
                </div>
            </div>

            <div class="divider mt-4"><span>أو</span></div>

            <p style="text-align:center;margin-top:15px;">
                ليس لديك حساب؟ 
                <a href="#" style="color:var(--gold);" onclick="showRegister()">إنشاء حساب جديد</a>
            </p>

            <!-- Register -->
            <div id="registerSection" style="display:none;">
                <div class="form-group">
                    <label>الاسم الكامل</label>
                    <input type="text" class="form-control" id="regName" placeholder="الاسم الكامل">
                </div>
                <div class="form-group">
                    <label>البريد الإلكتروني</label>
                    <input type="email" class="form-control" id="regEmail" placeholder="example@email.com">
                </div>
                <div class="form-group">
                    <label>رقم الهاتف (اختياري)</label>
                    <input type="tel" class="form-control" id="regPhone" placeholder="+20 1xx xxxx xxx">
                </div>
                <div class="form-group">
                    <label>كلمة المرور</label>
                    <input type="password" class="form-control" id="regPassword" placeholder="••••••••">
                </div>
                <button class="btn btn-gold" onclick="registerUser()">
                    <i class="fas fa-user-plus"></i> إنشاء حساب
                </button>
                <button class="btn btn-outline mt-2" onclick="hideRegister()">
                    العودة لتسجيل الدخول
                </button>
            </div>
        </div>
    </div>

    <!-- ==================== MAIN APP ==================== -->
    <div id="mainApp" class="main-app">
        <!-- Navbar -->
        <nav class="navbar navbar-expand-lg">
            <div class="container">
                <a class="brand" href="#" onclick="showPage('home')">EVIL BAR</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu" style="border-color:var(--gold);">
                    <span class="navbar-toggler-icon" style="filter:invert(1);"></span>
                </button>
                <div class="collapse navbar-collapse" id="navMenu">
                    <ul class="navbar-nav me-auto">
                        <li class="nav-item"><a class="nav-link active" href="#" onclick="showPage('home')">الرئيسية</a></li>
                        <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('menu')">المنيو</a></li>
                        <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('drinks')">المشروبات</a></li>
                        <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('food')">المأكولات</a></li>
                        <li class="nav-item"><a class="nav-link" href="#" onclick="showPage('reservation')">حجز طاولة</a></li>
                    </ul>
                    <div class="d-flex align-items-center gap-2">
                        <button class="btn btn-sm btn-gold position-relative" onclick="toggleCart()">
                            <i class="fas fa-shopping-cart"></i> <span id="cartCountBadge">0</span>
                        </button>
                        <span style="color:var(--gold);cursor:pointer;" onclick="logout()" title="تسجيل الخروج">
                            <i class="fas fa-user"></i> <span id="userNameDisplay"></span>
                        </span>
                    </div>
                </div>
            </div>
        </nav>

        <!-- Page Content -->
        <div id="pageContent"></div>

        <!-- Footer -->
        <footer>
            <div class="container">
                <h5 class="gold-text">EVIL BAR</h5>
                <p>أفخم كافيه وبار في المدينة</p>
                <div class="mt-2">
                    <a href="#" onclick="showPage('home')">الرئيسية</a>
                    <a href="#" onclick="showPage('menu')">المنيو</a>
                    <a href="#">اتصل بنا</a>
                    <a href="#">سياسة الخصوصية</a>
                </div>
                <p class="mt-3" style="color:var(--gray);">&copy; 2024 Evil Bar. جميع الحقوق محفوظة.</p>
            </div>
        </footer>
    </div>

    <!-- Cart Sidebar -->
    <div class="cart-overlay" id="cartOverlay" onclick="toggleCart()"></div>
    <div class="cart-sidebar" id="cartSidebar">
        <div class="d-flex justify-content-between align-items-center mb-3">
            <h5 class="gold-text"><i class="fas fa-shopping-cart"></i> السلة</h5>
            <button class="btn-close btn-close-white" onclick="toggleCart()"></button>
        </div>
        <div id="cartItemsList"></div>
        <hr style="border-color:rgba(255,255,255,0.2);">
        <h5>الإجمالي: <span class="gold-text" id="cartTotal">0</span> ج.م</h5>
        <button class="btn btn-gold mt-3" onclick="checkout()">إتمام الشراء</button>
        <button class="btn btn-outline mt-2" onclick="clearCart()">تفريغ السلة</button>
    </div>

    <!-- Toast -->
    <div class="toast-msg" id="toastMsg"></div>

    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script>
        // ==================== DATA ====================
        const menuData = [
            // Hot Drinks
            { id:1, name:'إسبرسو', cat:'hot-drinks', catName:'مشروبات ساخنة', price:35, discPrice:null, rating:4.8, img:'https://images.unsplash.com/photo-1510707577719-ae7c14805e3a?w=400&q=80', desc:'إسبرسو إيطالي أصيل غني وقوي' },
            { id:2, name:'كابتشينو', cat:'hot-drinks', catName:'مشروبات ساخنة', price:45, discPrice:null, rating:4.9, img:'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400&q=80', desc:'كابتشينو برغوة كثيفة' },
            { id:3, name:'لاتيه', cat:'hot-drinks', catName:'مشروبات ساخنة', price:45, discPrice:38, rating:4.7, img:'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400&q=80', desc:'لاتيه كريمي ناعم' },
            { id:4, name:'موكا', cat:'hot-drinks', catName:'مشروبات ساخنة', price:50, discPrice:null, rating:4.8, img:'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400&q=80', desc:'موكا بالشوكولاتة البلجيكية' },
            { id:5, name:'أمريكانو', cat:'hot-drinks', catName:'مشروبات ساخنة', price:40, discPrice:35, rating:4.6, img:'https://images.unsplash.com/photo-1551030173-122aabc4489c?w=400&q=80', desc:'أمريكانو كلاسيكي' },
            { id:6, name:'قهوة تركي', cat:'hot-drinks', catName:'مشروبات ساخنة', price:30, discPrice:null, rating:4.9, img:'https://images.unsplash.com/photo-1509042239860-f550ce710b93?w=400&q=80', desc:'قهوة تركية تقليدية' },

            // Cold Drinks
            { id:7, name:'آيس لاتيه', cat:'cold-drinks', catName:'مشروبات باردة', price:50, discPrice:null, rating:4.6, img:'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400&q=80', desc:'آيس لاتيه منعش' },
            { id:8, name:'ليمون نعناع', cat:'cold-drinks', catName:'مشروبات باردة', price:35, discPrice:30, rating:4.8, img:'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=400&q=80', desc:'ليمونادة طازجة بالنعناع' },
            { id:9, name:'عصير برتقال', cat:'cold-drinks', catName:'مشروبات باردة', price:30, discPrice:null, rating:4.5, img:'https://images.unsplash.com/photo-1621506289937-a8e4df240d0b?w=400&q=80', desc:'عصير برتقال طبيعي 100%' },
            { id:10, name:'مانجو', cat:'cold-drinks', catName:'مشروبات باردة', price:40, discPrice:null, rating:4.9, img:'https://images.unsplash.com/photo-1546173159-315724a31696?w=400&q=80', desc:'عصير مانجو طازج' },
            { id:11, name:'سموذي فراولة', cat:'cold-drinks', catName:'مشروبات باردة', price:45, discPrice:null, rating:4.7, img:'https://images.unsplash.com/photo-1553530666-ba11a7da3888?w=400&q=80', desc:'سموذي فراولة طبيعي' },

            // Food
            { id:12, name:'تشيز كيك', cat:'food', catName:'حلويات', price:60, discPrice:50, rating:4.9, img:'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400&q=80', desc:'تشيز كيك نيويورك' },
            { id:13, name:'براوني', cat:'food', catName:'حلويات', price:45, discPrice:null, rating:4.8, img:'https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=400&q=80', desc:'براوني شوكولاتة بلجيكية' },
            { id:14, name:'كرواسون', cat:'food', catName:'مخبوزات', price:35, discPrice:null, rating:4.7, img:'https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=400&q=80', desc:'كرواسون فرنسي طازج' },
            { id:15, name:'كيك شوكولاتة', cat:'food', catName:'حلويات', price:70, discPrice:60, rating:4.9, img:'https://images.unsplash.com/photo-1578985545062-69928b1d9587?w=400&q=80', desc:'كيك شوكولاتة ثلاثي' },
            { id:16, name:'تيراميسو', cat:'food', catName:'حلويات', price:65, discPrice:null, rating:4.9, img:'https://images.unsplash.com/photo-1571877227200-a0d98ea607e9?w=400&q=80', desc:'تيراميسو إيطالي أصيل' },

            // Alcoholic
            { id:17, name:'هاينكن', cat:'alcohol', catName:'مشروبات كحولية', price:70, discPrice:null, rating:4.6, img:'https://images.unsplash.com/photo-1618885472179-5e474019f2a9?w=400&q=80', desc:'بيرة هاينكن الهولندية' },
            { id:18, name:'ويسكي', cat:'alcohol', catName:'مشروبات كحولية', price:120, discPrice:100, rating:4.8, img:'https://images.unsplash.com/photo-1527281400683-1aae777175f0?w=400&q=80', desc:'ويسكي سكوتش 12 سنة' },
            { id:19, name:'موهيتو', cat:'alcohol', catName:'مشروبات كحولية', price:75, discPrice:null, rating:4.9, img:'https://images.unsplash.com/photo-1551538827-9c037cb4f32a?w=400&q=80', desc:'موهيتو كوبي منعش' },
            { id:20, name:'مارتيني', cat:'alcohol', catName:'مشروبات كحولية', price:85, discPrice:null, rating:4.8, img:'https://images.unsplash.com/photo-1575023782549-62ca0d244b39?w=400&q=80', desc:'مارتيني جاف كلاسيكي' },
            { id:21, name:'مارغريتا', cat:'alcohol', catName:'مشروبات كحولية', price:80, discPrice:null, rating:4.7, img:'https://images.unsplash.com/photo-1556855810-ac404d3c2eba?w=400&q=80', desc:'مارغريتا كلاسيكية' },
        ];

        // ==================== STATE ====================
        let cart = JSON.parse(localStorage.getItem('evilCart')) || [];
        let user = JSON.parse(localStorage.getItem('evilUser')) || null;
        let currentPage = 'home';
        let otpInterval = null;

        // ==================== INIT ====================
        window.onload = function() {
            if (user) {
                showMainApp();
            }
            AOS.init({ duration: 800, once: true });
        };

        // ==================== AUTH ====================
        function switchAuthTab(tab) {
            document.querySelectorAll('.auth-tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');
            document.getElementById('emailLogin').style.display = tab === 'email' ? 'block' : 'none';
            document.getElementById('phoneLogin').style.display = tab === 'phone' ? 'block' : 'none';
        }

        function loginWithEmail() {
            const email = document.getElementById('loginEmail').value.trim();
            const password = document.getElementById('loginPassword').value.trim();
            
            if (!email || !password) {
                showToast('يرجى إدخال البريد الإلكتروني وكلمة المرور', 'error');
                return;
            }

            const users = JSON.parse(localStorage.getItem('evilUsers')) || [];
            const found = users.find(u => u.email === email && u.password === password);
            
            if (found) {
                loginSuccess(found);
            } else {
                // Demo login
                if (email === 'demo@evilbar.com' && password === '123456') {
                    loginSuccess({ name: 'زائر', email: 'demo@evilbar.com', phone: '' });
                } else {
                    showToast('بيانات الدخول غير صحيحة', 'error');
                }
            }
        }

        function loginWithGoogle() {
            // Simulate Google login
            loginSuccess({ name: 'مستخدم Google', email: 'google@evilbar.com', phone: '' });
        }

        function sendOTP() {
            const phone = document.getElementById('phoneNumber').value.trim();
            if (!phone) {
                showToast('يرجى إدخال رقم الهاتف', 'error');
                return;
            }

            document.getElementById('otpSection').classList.add('show');
            document.getElementById('sendOtpBtn').style.display = 'none';
            
            // Store OTP (demo: 123456)
            localStorage.setItem('evilOTP', '123456');
            localStorage.setItem('evilPhone', phone);
            
            // Timer
            let seconds = 60;
            document.getElementById('otpTimer').textContent = seconds + ' ثانية';
            document.getElementById('resendOtpBtn').disabled = true;
            
            if (otpInterval) clearInterval(otpInterval);
            otpInterval = setInterval(() => {
                seconds--;
                document.getElementById('otpTimer').textContent = seconds + ' ثانية';
                if (seconds <= 0) {
                    clearInterval(otpInterval);
                    document.getElementById('resendOtpBtn').disabled = false;
                    document.getElementById('otpTimer').textContent = 'انتهت الصلاحية';
                }
            }, 1000);

            showToast('تم إرسال رمز التحقق (تجريبي: 123456)');
            document.getElementById('otpCode').focus();
        }

        function verifyOTP() {
            const otp = document.getElementById('otpCode').value.trim();
            const correctOTP = localStorage.getItem('evilOTP');
            const phone = localStorage.getItem('evilPhone');
            
            if (otp === correctOTP) {
                loginSuccess({ name: 'مستخدم', email: '', phone: phone });
                clearInterval(otpInterval);
            } else {
                document.getElementById('otpError').style.display = 'block';
            }
        }

        function loginSuccess(userData) {
            user = userData;
            localStorage.setItem('evilUser', JSON.stringify(user));
            showMainApp();
            showToast('مرحباً ' + user.name + '! 👋');
        }

        function showRegister() {
            document.getElementById('registerSection').style.display = 'block';
            document.getElementById('emailLogin').style.display = 'none';
            document.getElementById('phoneLogin').style.display = 'none';
            document.querySelector('.divider').style.display = 'none';
        }

        function hideRegister() {
            document.getElementById('registerSection').style.display = 'none';
            document.getElementById('emailLogin').style.display = 'block';
            document.querySelector('.divider').style.display = 'block';
        }

        function registerUser() {
            const name = document.getElementById('regName').value.trim();
            const email = document.getElementById('regEmail').value.trim();
            const phone = document.getElementById('regPhone').value.trim();
            const password = document.getElementById('regPassword').value.trim();
            
            if (!name || !email || !password) {
                showToast('يرجى ملء جميع الحقول المطلوبة', 'error');
                return;
            }

            const users = JSON.parse(localStorage.getItem('evilUsers')) || [];
            if (users.find(u => u.email === email)) {
                showToast('البريد الإلكتروني مستخدم مسبقاً', 'error');
                return;
            }

            users.push({ name, email, phone, password });
            localStorage.setItem('evilUsers', JSON.stringify(users));
            loginSuccess({ name, email, phone });
        }

        function logout() {
            user = null;
            localStorage.removeItem('evilUser');
            document.getElementById('mainApp').classList.remove('show');
            document.getElementById('authPage').style.display = 'flex';
            showToast('تم تسجيل الخروج');
        }

        // ==================== MAIN APP ====================
        function showMainApp() {
            document.getElementById('authPage').style.display = 'none';
            document.getElementById('mainApp').classList.add('show');
            document.getElementById('userNameDisplay').textContent = user.name;
            updateCartUI();
            showPage('home');
        }

        function showPage(page) {
            currentPage = page;
            const content = document.getElementById('pageContent');
            
            switch(page) {
                case 'home':
                    content.innerHTML = renderHome();
                    break;
                case 'menu':
                    content.innerHTML = renderMenuPage('all');
                    break;
                case 'drinks':
                    content.innerHTML = renderMenuPage('drinks');
                    break;
                case 'food':
                    content.innerHTML = renderMenuPage('food');
                    break;
                case 'reservation':
                    content.innerHTML = renderReservation();
                    break;
            }
            
            // Update active nav
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            const links = document.querySelectorAll('.nav-link');
            const index = ['home','menu','drinks','food','reservation'].indexOf(page);
            if (links[index]) links[index].classList.add('active');
            
            window.scrollTo({ top: 0, behavior: 'smooth' });
            AOS.refresh();
        }

        function renderHome() {
            const featured = menuData.filter(p => [1,3,8,10,12,14,17,19].includes(p.id));
            return `
                <div class="hero">
                    <div>
                        <h1>EVIL BAR</h1>
                        <p>أفخم تجربة قهوة وبار في المدينة</p>
                        <button class="btn btn-gold" style="width:auto;display:inline-flex;margin:5px;" onclick="showPage('menu')">📋 تصفح المنيو</button>
                        <button class="btn btn-outline" style="width:auto;display:inline-flex;margin:5px;border-color:var(--gold);color:var(--gold);" onclick="showPage('reservation')">🍽 احجز طاولة</button>
                    </div>
                </div>
                <div class="section">
                    <div class="container">
                        <h2 class="section-title"><span class="gold-text">منتجاتنا</span> المميزة</h2>
                        <div class="row">
                            ${featured.map(p => productCard(p)).join('')}
                        </div>
                    </div>
                </div>
                <div class="section" style="background:#111;">
                    <div class="container text-center">
                        <h2 class="section-title">احجز <span class="gold-text">طاولتك</span> الآن</h2>
                        <p style="color:var(--gray);margin-bottom:30px;">استمتع بأجواء راقية وخدمة ممتازة</p>
                        <button class="btn btn-gold" style="width:auto;display:inline-flex;" onclick="showPage('reservation')">احجز الآن</button>
                    </div>
                </div>
            `;
        }

        function renderMenuPage(filter) {
            let items = menuData;
            if (filter === 'drinks') items = menuData.filter(p => p.cat === 'hot-drinks' || p.cat === 'cold-drinks' || p.cat === 'alcohol');
            if (filter === 'food') items = menuData.filter(p => p.cat === 'food');
            
            const cats = [
                { id:'all', name:'الكل' },
                { id:'hot-drinks', name:'مشروبات ساخنة' },
                { id:'cold-drinks', name:'مشروبات باردة' },
                { id:'food', name:'حلويات ومخبوزات' },
                { id:'alcohol', name:'مشروبات كحولية' },
            ];
            
            return `
                <div class="section">
                    <div class="container">
                        <h1 class="section-title"><span class="gold-text">المنيو</span> 🍽️</h1>
                        <div class="cat-nav">
                            ${cats.map(c => `
                                <button class="cat-btn ${filter === c.id ? 'active' : ''}" onclick="filterMenu('${c.id}')">${c.name}</button>
                            `).join('')}
                        </div>
                        <div class="row" id="menuItems">
                            ${items.map(p => productCard(p)).join('')}
                        </div>
                    </div>
                </div>
            `;
        }

        function filterMenu(cat) {
            let items = cat === 'all' ? menuData : menuData.filter(p => p.cat === cat);
            document.getElementById('menuItems').innerHTML = items.map(p => productCard(p)).join('');
            document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
            event.target.classList.add('active');
        }

        function productCard(p) {
            const price = p.discPrice || p.price;
            return `
                <div class="col-lg-3 col-md-4 col-sm-6 mb-4" data-aos="fade-up">
                    <div class="product-card">
                        <div class="product-img">
                            <img src="${p.img}" alt="${p.name}" onerror="this.src='https://via.placeholder.com/400x220/1a1a1a/d4af37?text=${p.name}'">
                            ${p.discPrice ? '<span class="product-badge">خصم</span>' : ''}
                        </div>
                        <div class="product-info">
                            <h5>${p.name}</h5>
                            <p class="desc">${p.desc}</p>
                            <div class="product-price">
                                ${p.discPrice ? `<span class="price-old">${p.price} ج.م</span>` : ''}
                                <span class="price-new">${price} ج.م</span>
                            </div>
                            <div class="stars">
                                ${'★'.repeat(Math.floor(p.rating))}${p.rating % 1 >= 0.5 ? '½' : ''}
                                <small style="color:var(--gray);">${p.rating}</small>
                            </div>
                            <button class="btn btn-gold btn-sm" onclick="addToCart(${p.id})">
                                <i class="fas fa-cart-plus"></i> أضف للسلة
                            </button>
                        </div>
                    </div>
                </div>
            `;
        }

        function renderReservation() {
            return `
                <div class="section">
                    <div class="container">
                        <div class="auth-box" style="margin:0 auto;">
                            <h2 class="gold-text text-center mb-4">🍽 حجز طاولة</h2>
                            <div class="form-group">
                                <label>عدد الضيوف</label>
                                <select class="form-control" id="guests">
                                    <option>1 شخص</option><option>2 أشخاص</option><option>3 أشخاص</option>
                                    <option>4 أشخاص</option><option>5 أشخاص</option><option>6+ أشخاص</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>التاريخ</label>
                                <input type="date" class="form-control" id="resDate">
                            </div>
                            <div class="form-group">
                                <label>الوقت</label>
                                <input type="time" class="form-control" id="resTime">
                            </div>
                            <div class="form-group">
                                <label>ملاحظات</label>
                                <textarea class="form-control" id="resNotes" rows="3" placeholder="أي طلبات خاصة؟"></textarea>
                            </div>
                            <button class="btn btn-gold" onclick="submitReservation()">تأكيد الحجز</button>
                        </div>
                    </div>
                </div>
            `;
        }

        function submitReservation() {
            showToast('✅ تم تأكيد الحجز! سنتواصل معك قريباً');
        }

        // ==================== CART ====================
        function addToCart(productId) {
            const product = menuData.find(p => p.id === productId);
            if (!product) return;
            
            const existing = cart.find(i => i.productId === productId);
            if (existing) {
                existing.qty++;
            } else {
                cart.push({ productId, qty: 1, price: product.discPrice || product.price, name: product.name, img: product.img });
            }
            saveCart();
            updateCartUI();
            showToast('✅ تمت الإضافة إلى السلة');
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            saveCart();
            updateCartUI();
        }

        function clearCart() {
            cart = [];
            saveCart();
            updateCartUI();
            showToast('🗑 تم تفريغ السلة');
        }

        function saveCart() {
            localStorage.setItem('evilCart', JSON.stringify(cart));
        }

        function updateCartUI() {
            const count = cart.reduce((s, i) => s + i.qty, 0);
            const total = cart.reduce((s, i) => s + (i.price * i.qty), 0);
            
            document.getElementById('cartCountBadge').textContent = count;
            document.getElementById('cartTotal').textContent = total;
            
            const list = document.getElementById('cartItemsList');
            if (cart.length === 0) {
                list.innerHTML = '<p style="color:var(--gray);text-align:center;">السلة فارغة</p>';
            } else {
                list.innerHTML = cart.map((item, i) => `
                    <div style="display:flex;align-items:center;gap:10px;margin-bottom:10px;padding:10px;background:rgba(255,255,255,0.05);border-radius:10px;">
                        <img src="${item.img}" width="45" height="45" style="border-radius:8px;object-fit:cover;">
                        <div style="flex:1;">
                            <small style="font-weight:bold;">${item.name}</small><br>
                            <small style="color:var(--gold);">${item.price} ج.م × ${item.qty}</small>
                        </div>
                        <button class="btn btn-sm btn-danger" onclick="removeFromCart(${i})" style="width:auto;">🗑</button>
                    </div>
                `).join('');
            }
        }

        function toggleCart() {
            document.getElementById('cartSidebar').classList.toggle('open');
            document.getElementById('cartOverlay').classList.toggle('open');
        }

        function checkout() {
            if (cart.length === 0) {
                showToast('السلة فارغة', 'error');
                return;
            }
            const total = cart.reduce((s, i) => s + (i.price * i.qty), 0);
            cart = [];
            saveCart();
            updateCartUI();
            toggleCart();
            showToast('🎉 تم الطلب بنجاح! الإجمالي: ' + total + ' ج.م');
        }

        // ==================== TOAST ====================
        function showToast(msg, type = '') {
            const toast = document.getElementById('toastMsg');
            toast.textContent = msg;
            toast.className = 'toast-msg show ' + type;
            setTimeout(() => toast.classList.remove('show'), 3000);
        }
    </script>
</body>
</html>
