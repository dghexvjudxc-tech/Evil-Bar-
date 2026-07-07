<!DOCTYPE html>
<html lang="ar" dir="rtl" data-bs-theme="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evil Bar - إيفل بار | Luxury Cafe & Bar</title>
    <meta name="description" content="Evil Bar - أفخم كافيه وبار في المدينة. قهوة، مشروبات، حلويات، وأجواء راقية">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.rtl.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0a0a;
            --bg-secondary: #111111;
            --gold: #D4AF37;
            --gold-light: #F4D03F;
            --gold-dark: #B8960C;
            --brown: #4E342E;
            --white: #FFFFFF;
            --text-primary: #FFFFFF;
            --text-secondary: #B0B0B0;
            --glass-bg: rgba(20, 20, 20, 0.7);
            --glass-border: rgba(212, 175, 55, 0.3);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background-color: var(--bg-primary);
            color: var(--text-primary);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow-x: hidden;
            transition: all 0.3s ease;
        }

        body.light-mode {
            --bg-primary: #f5f5f5;
            --bg-secondary: #ffffff;
            --text-primary: #1a1a1a;
            --text-secondary: #666666;
            --glass-bg: rgba(255, 255, 255, 0.7);
        }

        /* Preloader */
        #preloader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--bg-primary); z-index: 9999;
            display: flex; align-items: center; justify-content: center;
        }
        .loader { text-align: center; }
        .loader-circle {
            width: 80px; height: 80px; border: 3px solid transparent;
            border-top-color: var(--gold); border-radius: 50%;
            animation: spin 1s linear infinite; margin: 0 auto 20px;
        }
        .loader-text { color: var(--gold); font-size: 24px; font-weight: bold; letter-spacing: 5px; }
        @keyframes spin { to { transform: rotate(360deg); } }

        /* Glass Effects */
        .glass-card {
            background: var(--glass-bg); backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border); border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4); transition: all 0.3s ease;
        }
        .glass-card:hover { transform: translateY(-5px); box-shadow: 0 12px 40px rgba(212, 175, 55, 0.2); }
        
        .glass-navbar {
            background: rgba(10, 10, 10, 0.85) !important; backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(212, 175, 55, 0.2); padding: 10px 0;
        }
        
        .glass-footer {
            background: rgba(10, 10, 10, 0.9); backdrop-filter: blur(20px);
            border-top: 1px solid rgba(212, 175, 55, 0.2); padding: 40px 0 20px;
        }

        /* Buttons */
        .btn-gold {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold), var(--gold-light));
            color: #000; border: none; font-weight: bold; padding: 12px 30px;
            border-radius: 50px; transition: all 0.3s ease; letter-spacing: 1px;
        }
        .btn-gold:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(212, 175, 55, 0.4); color: #000; }
        
        .btn-outline-gold {
            border: 2px solid var(--gold); color: var(--gold); background: transparent;
            padding: 10px 25px; border-radius: 50px; transition: all 0.3s ease;
        }
        .btn-outline-gold:hover { background: var(--gold); color: #000; }

        /* Brand */
        .brand-text {
            color: var(--gold); font-size: 28px; font-weight: 900;
            letter-spacing: 3px; text-shadow: 0 0 20px rgba(212, 175, 55, 0.5);
            text-decoration: none;
        }
        .brand-text:hover { color: var(--gold-light); }

        /* Nav */
        .nav-link { color: var(--text-primary) !important; transition: all 0.3s; margin: 0 5px; }
        .nav-link:hover { color: var(--gold) !important; }
        .navbar-toggler { border-color: var(--gold); }
        .navbar-toggler-icon { filter: invert(1); }

        /* Hero */
        .hero-section {
            height: 100vh; background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.9)), url('https://images.unsplash.com/photo-1470337458703-46ad1756a187?w=1920');
            background-size: cover; background-position: center; background-attachment: fixed;
            display: flex; align-items: center; justify-content: center; position: relative;
        }
        .hero-title {
            font-size: 80px; font-weight: 900; color: var(--gold);
            letter-spacing: 10px; text-shadow: 0 0 40px rgba(212, 175, 55, 0.6);
            animation: glitch 3s infinite;
        }
        .hero-subtitle { font-size: 24px; color: var(--text-secondary); margin: 20px 0 30px; }
        
        @keyframes glitch {
            0%, 100% { transform: none; }
            20% { transform: skew(0.5deg); }
            40% { transform: skew(-0.5deg); }
            60% { transform: skew(0.3deg); }
            80% { transform: skew(-0.3deg); }
        }

        /* Scroll indicator */
        .scroll-indicator { position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%); }
        .scroll-indicator span {
            display: block; width: 8px; height: 8px; border-radius: 50%;
            background: var(--gold); margin: 5px 0; animation: bounce 1.5s infinite;
        }
        .scroll-indicator span:nth-child(2) { animation-delay: 0.2s; }
        .scroll-indicator span:nth-child(3) { animation-delay: 0.4s; }
        @keyframes bounce {
            0%, 100% { opacity: 0.3; transform: translateY(0); }
            50% { opacity: 1; transform: translateY(-5px); }
        }

        /* Section titles */
        .section-title { font-size: 40px; font-weight: bold; margin-bottom: 40px; }
        .gold-text { color: var(--gold) !important; }

        /* Product Card */
        .product-card { overflow: hidden; border-radius: 20px; }
        .product-img {
            height: 250px; overflow: hidden; position: relative;
        }
        .product-img img {
            width: 100%; height: 100%; object-fit: cover;
            transition: transform 0.5s ease;
        }
        .product-card:hover .product-img img { transform: scale(1.1); }
        
        .product-actions {
            position: absolute; top: 10px; right: 10px; display: flex;
            flex-direction: column; gap: 8px; opacity: 0;
            transform: translateX(20px); transition: all 0.3s ease;
        }
        .product-card:hover .product-actions { opacity: 1; transform: translateX(0); }
        
        .btn-fav, .btn-cart {
            width: 35px; height: 35px; border-radius: 50%; border: none;
            background: rgba(0,0,0,0.6); color: var(--gold); cursor: pointer;
            transition: all 0.3s; display: flex; align-items: center; justify-content: center;
        }
        .btn-fav:hover, .btn-cart:hover { background: var(--gold); color: #000; }
        .btn-fav.active { background: var(--gold); color: #000; }
        
        .discount-badge {
            position: absolute; top: 10px; left: 10px;
            background: var(--gold); color: #000; padding: 5px 10px;
            border-radius: 20px; font-size: 12px; font-weight: bold;
        }
        .old-price { text-decoration: line-through; color: var(--text-secondary); font-size: 14px; }
        .current-price { font-size: 20px; font-weight: bold; color: var(--gold); }

        /* Category Card */
        .category-card {
            display: block; padding: 40px 20px; text-decoration: none;
            color: var(--text-primary); transition: all 0.3s; text-align: center;
            border-radius: 20px;
        }
        .category-card:hover { background: rgba(212, 175, 55, 0.1); color: var(--gold); }
        .category-icon { font-size: 45px; color: var(--gold); margin-bottom: 15px; }

        /* CTA */
        .cta-section {
            background: linear-gradient(rgba(0,0,0,0.85), rgba(0,0,0,0.85)), url('https://images.unsplash.com/photo-1572116469696-31de0f17cc34?w=1920');
            background-size: cover; background-position: center; background-attachment: fixed;
            padding: 80px 0;
        }

        /* Auth Modal */
        .modal-content {
            background: rgba(20,20,20,0.95); backdrop-filter: blur(20px);
            border: 1px solid rgba(212,175,55,0.3); border-radius: 20px;
        }
        .modal-header { border-bottom: 1px solid rgba(212,175,55,0.2); }
        .modal-footer { border-top: 1px solid rgba(212,175,55,0.2); }

        /* Footer */
        .footer a { color: var(--text-secondary); text-decoration: none; transition: all 0.3s; }
        .footer a:hover { color: var(--gold); }
        .social-icon {
            width: 40px; height: 40px; line-height: 40px; text-align: center;
            border: 1px solid rgba(212,175,55,0.3); border-radius: 50%;
            display: inline-block; margin: 0 5px; transition: all 0.3s;
        }
        .social-icon:hover { background: var(--gold); color: #000; border-color: var(--gold); }

        /* Toast */
        .toast-custom {
            position: fixed; bottom: 20px; right: 20px; z-index: 9999;
            padding: 15px 25px; border-radius: 10px; color: #000;
            font-weight: bold; transform: translateX(120%); transition: transform 0.3s ease;
        }
        .toast-custom.show { transform: translateX(0); }
        .toast-success { background: var(--gold); }
        .toast-error { background: #ff4444; color: #fff; }

        /* Cart Badge */
        .cart-badge {
            position: absolute; top: -8px; right: -8px;
            background: var(--gold); color: #000; border-radius: 50%;
            width: 20px; height: 20px; font-size: 11px;
            display: flex; align-items: center; justify-content: center; font-weight: bold;
        }

        /* Search */
        .search-box {
            background: var(--glass-bg); border: 1px solid rgba(212,175,55,0.3);
            border-radius: 50px; padding: 10px 20px; color: var(--text-primary);
            width: 250px; transition: all 0.3s;
        }
        .search-box:focus { outline: none; border-color: var(--gold); box-shadow: 0 0 15px rgba(212,175,55,0.3); }

        /* Page content */
        .page-content { padding: 100px 0; min-height: 100vh; }

        /* Animations */
        .fade-in { animation: fadeIn 1s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        
        .neon-text { text-shadow: 0 0 10px rgba(212,175,55,0.5), 0 0 20px rgba(212,175,55,0.3); }

        /* Cart Sidebar */
        .cart-sidebar {
            position: fixed; top: 0; right: -400px; width: 400px; height: 100%;
            background: rgba(10,10,10,0.98); backdrop-filter: blur(20px);
            border-left: 1px solid rgba(212,175,55,0.3); z-index: 9998;
            transition: right 0.3s ease; padding: 20px; overflow-y: auto;
        }
        .cart-sidebar.open { right: 0; }
        .cart-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.7); z-index: 9997; display: none;
        }
        .cart-overlay.open { display: block; }

        /* Rating Stars */
        .stars { color: var(--gold); }
        .stars .far { color: var(--text-secondary); }

        /* Responsive */
        @media (max-width: 768px) {
            .hero-title { font-size: 40px; letter-spacing: 5px; }
            .hero-subtitle { font-size: 16px; }
            .section-title { font-size: 28px; }
            .cart-sidebar { width: 100%; right: -100%; }
        }
    </style>
</head>
<body>

    <!-- Preloader -->
    <div id="preloader">
        <div class="loader">
            <div class="loader-circle"></div>
            <div class="loader-text">EVIL BAR</div>
        </div>
    </div>

    <!-- Navigation -->
    <nav class="navbar navbar-expand-lg fixed-top glass-navbar">
        <div class="container">
            <a class="brand-text" href="#" onclick="navigateTo('home')">EVIL BAR</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('home')">الرئيسية</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('menu')">القائمة</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('reservation')">حجز طاولة</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('gallery')">المعرض</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('blog')">المدونة</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('about')">من نحن</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('contact')">اتصل بنا</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="navigateTo('faq')">الأسئلة الشائعة</a></li>
                </ul>
                <div class="d-flex align-items-center gap-2 flex-wrap">
                    <input type="text" class="search-box" placeholder="🔍 بحث..." id="searchInput" onkeyup="handleSearch(event)">
                    <button class="btn btn-outline-gold position-relative" onclick="toggleCart()">
                        <i class="fas fa-shopping-cart"></i>
                        <span class="cart-badge" id="cartCount">0</span>
                    </button>
                    <button class="btn btn-outline-gold" onclick="navigateTo('favorites')">
                        <i class="fas fa-heart"></i>
                    </button>
                    <button class="btn btn-outline-gold" onclick="openAuthModal()" id="authBtn">
                        <i class="fas fa-user"></i> دخول
                    </button>
                    <button class="btn btn-outline-gold" onclick="toggleTheme()" id="themeBtn">
                        <i class="fas fa-moon"></i>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main id="mainContent"></main>

    <!-- Cart Sidebar -->
    <div class="cart-overlay" id="cartOverlay" onclick="toggleCart()"></div>
    <div class="cart-sidebar" id="cartSidebar">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h4 class="gold-text">🛒 سلة المشتريات</h4>
            <button class="btn-close btn-close-white" onclick="toggleCart()"></button>
        </div>
        <div id="cartItems"></div>
        <div class="mt-4 pt-3 border-top border-gold">
            <h5>الإجمالي: <span class="gold-text" id="cartTotal">0</span> ج.م</h5>
            <button class="btn btn-gold w-100 mt-3" onclick="checkout()">إتمام الشراء 💳</button>
            <button class="btn btn-outline-gold w-100 mt-2" onclick="clearCart()">تفريغ السلة</button>
        </div>
    </div>

    <!-- Auth Modal -->
    <div class="modal fade" id="authModal" tabindex="-1">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title gold-text">تسجيل الدخول</h5>
                    <button class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div id="authTabs">
                        <ul class="nav nav-tabs mb-3" id="authTabNav">
                            <li class="nav-item"><a class="nav-link active" onclick="switchAuthTab('email')">البريد الإلكتروني</a></li>
                            <li class="nav-item"><a class="nav-link" onclick="switchAuthTab('phone')">رقم الهاتف</a></li>
                        </ul>
                        <div id="emailAuth">
                            <input type="email" class="form-control mb-3 bg-dark text-white" placeholder="البريد الإلكتروني" id="loginEmail">
                            <input type="password" class="form-control mb-3 bg-dark text-white" placeholder="كلمة المرور" id="loginPassword">
                            <div class="form-check mb-3">
                                <input type="checkbox" class="form-check-input" id="rememberMe">
                                <label class="form-check-label">تذكرني</label>
                            </div>
                            <button class="btn btn-gold w-100 mb-2" onclick="login()">تسجيل الدخول</button>
                            <button class="btn btn-outline-light w-100 mb-2" onclick="googleLogin()">
                                <i class="fab fa-google"></i> Google
                            </button>
                        </div>
                        <div id="phoneAuth" style="display:none;">
                            <input type="tel" class="form-control mb-3 bg-dark text-white" placeholder="رقم الهاتف" id="loginPhone">
                            <button class="btn btn-gold w-100 mb-2" onclick="sendOTP()">إرسال رمز التحقق</button>
                            <input type="text" class="form-control mb-3 bg-dark text-white" placeholder="رمز التحقق" id="otpInput" style="display:none;">
                            <button class="btn btn-gold w-100 mb-2" id="verifyOtpBtn" style="display:none;" onclick="verifyOTP()">تحقق</button>
                            <button class="btn btn-outline-gold w-100 mb-2" id="resendOtpBtn" style="display:none;" onclick="sendOTP()">إعادة إرسال (<span id="otpTimer">60</span>)</button>
                        </div>
                    </div>
                    <hr>
                    <p class="text-center mb-2">ليس لديك حساب؟</p>
                    <button class="btn btn-outline-gold w-100" onclick="switchToRegister()">إنشاء حساب جديد</button>
                    <div id="registerForm" style="display:none;">
                        <input type="text" class="form-control mb-2 bg-dark text-white" placeholder="الاسم الأول" id="regFirstName">
                        <input type="text" class="form-control mb-2 bg-dark text-white" placeholder="الاسم الأخير" id="regLastName">
                        <input type="email" class="form-control mb-2 bg-dark text-white" placeholder="البريد الإلكتروني" id="regEmail">
                        <input type="password" class="form-control mb-2 bg-dark text-white" placeholder="كلمة المرور" id="regPassword">
                        <button class="btn btn-gold w-100" onclick="register()">إنشاء حساب</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="glass-footer text-center text-md-start" id="footer">
        <div class="container">
            <div class="row">
                <div class="col-md-4 mb-3">
                    <h4 class="gold-text">EVIL BAR</h4>
                    <p>أفخم كافيه وبار في المدينة، نقدم أجود المشروبات وألذ المأكولات في أجواء راقية.</p>
                </div>
                <div class="col-md-4 mb-3">
                    <h5 class="gold-text">روابط سريعة</h5>
                    <a href="#" onclick="navigateTo('about')">من نحن</a><br>
                    <a href="#" onclick="navigateTo('menu')">القائمة</a><br>
                    <a href="#" onclick="navigateTo('faq')">الأسئلة الشائعة</a><br>
                    <a href="#" onclick="navigateTo('privacy')">سياسة الخصوصية</a><br>
                    <a href="#" onclick="navigateTo('terms')">الشروط والأحكام</a>
                </div>
                <div class="col-md-4 mb-3">
                    <h5 class="gold-text">تواصل معنا</h5>
                    <p><i class="fas fa-phone gold-text"></i> +20 123 456 789</p>
                    <p><i class="fas fa-envelope gold-text"></i> info@evilbar.com</p>
                    <p><i class="fas fa-map-marker-alt gold-text"></i> القاهرة، مصر</p>
                    <div>
                        <a href="#" class="social-icon"><i class="fab fa-facebook"></i></a>
                        <a href="#" class="social-icon"><i class="fab fa-instagram"></i></a>
                        <a href="#" class="social-icon"><i class="fab fa-twitter"></i></a>
                        <a href="#" class="social-icon"><i class="fab fa-tiktok"></i></a>
                    </div>
                </div>
            </div>
            <hr style="border-color: rgba(212,175,55,0.2);">
            <p class="text-center mb-0">&copy; 2024 Evil Bar. All rights reserved. Made with ❤️</p>
        </div>
    </footer>

    <!-- Toast -->
    <div class="toast-custom" id="toast"></div>

    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>

    <script>
        // ==================== DATA ====================
        const products = [
            // Hot Drinks
            { id:1, name:'إسبرسو', nameEn:'Espresso', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:35, discountPrice:null, rating:4.8, orders:1250, stock:100, image:'https://images.unsplash.com/photo-1510707577719-ae7c14805e3a?w=400', desc:'إسبرسو إيطالي أصيل، غني وقوي', featured:true, alcoholic:false },
            { id:2, name:'أمريكانو', nameEn:'Americano', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:40, discountPrice:35, rating:4.6, orders:980, stock:100, image:'https://images.unsplash.com/photo-1551030173-122aabc4489c?w=400', desc:'أمريكانو كلاسيكي منعش', featured:true, alcoholic:false },
            { id:3, name:'كابتشينو', nameEn:'Cappuccino', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:45, discountPrice:null, rating:4.9, orders:1580, stock:100, image:'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400', desc:'كابتشينو إيطالي برغوة كثيفة', featured:true, alcoholic:false },
            { id:4, name:'لاتيه', nameEn:'Latte', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:45, discountPrice:40, rating:4.7, orders:1320, stock:100, image:'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400', desc:'لاتيه كريمي ناعم', featured:false, alcoholic:false },
            { id:5, name:'موكا', nameEn:'Mocha', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:50, discountPrice:null, rating:4.8, orders:1100, stock:100, image:'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400', desc:'موكا بالشوكولاتة البلجيكية', featured:false, alcoholic:false },
            { id:6, name:'فلات وايت', nameEn:'Flat White', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:45, discountPrice:null, rating:4.5, orders:850, stock:100, image:'https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=400', desc:'فلات وايت أسترالي أصيل', featured:false, alcoholic:false },
            { id:7, name:'قهوة تركي', nameEn:'Turkish Coffee', category:'hot-drinks', categoryName:'مشروبات ساخنة', price:30, discountPrice:null, rating:4.9, orders:2000, stock:100, image:'https://images.unsplash.com/photo-1509042239860-f550ce710b93?w=400', desc:'قهوة تركية تقليدية', featured:true, alcoholic:false },
            
            // Cold Drinks
            { id:8, name:'آيس لاتيه', nameEn:'Iced Latte', category:'cold-drinks', categoryName:'مشروبات باردة', price:50, discountPrice:null, rating:4.6, orders:900, stock:100, image:'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400', desc:'آيس لاتيه منعش', featured:false, alcoholic:false },
            { id:9, name:'آيس موكا', nameEn:'Iced Mocha', category:'cold-drinks', categoryName:'مشروبات باردة', price:55, discountPrice:48, rating:4.7, orders:780, stock:100, image:'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400', desc:'آيس موكا بالشوكولاتة', featured:false, alcoholic:false },
            { id:10, name:'ليمون نعناع', nameEn:'Lemon Mint', category:'cold-drinks', categoryName:'مشروبات باردة', price:35, discountPrice:null, rating:4.8, orders:1500, stock:100, image:'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=400', desc:'ليمونادة طازجة بالنعناع', featured:true, alcoholic:false },
            { id:11, name:'عصير برتقال', nameEn:'Orange Juice', category:'cold-drinks', categoryName:'مشروبات باردة', price:30, discountPrice:null, rating:4.5, orders:1100, stock:100, image:'https://images.unsplash.com/photo-1621506289937-a8e4df240d0b?w=400', desc:'عصير برتقال طبيعي 100%', featured:false, alcoholic:false },
            { id:12, name:'مانجو', nameEn:'Mango Juice', category:'cold-drinks', categoryName:'مشروبات باردة', price:40, discountPrice:null, rating:4.9, orders:1800, stock:100, image:'https://images.unsplash.com/photo-1546173159-315724a31696?w=400', desc:'عصير مانجو طازج', featured:true, alcoholic:false },
            { id:13, name:'سموذي فراولة', nameEn:'Strawberry Smoothie', category:'cold-drinks', categoryName:'مشروبات باردة', price:45, discountPrice:null, rating:4.7, orders:950, stock:100, image:'https://images.unsplash.com/photo-1553530666-ba11a7da3888?w=400', desc:'سموذي فراولة طبيعي', featured:false, alcoholic:false },
            { id:14, name:'مياه معدنية', nameEn:'Mineral Water', category:'cold-drinks', categoryName:'مشروبات باردة', price:10, discountPrice:null, rating:4.0, orders:3000, stock:500, image:'https://images.unsplash.com/photo-1616118132534-381148898bb4?w=400', desc:'مياه معدنية نقية', featured:false, alcoholic:false },
            { id:15, name:'مشروبات غازية', nameEn:'Soft Drinks', category:'cold-drinks', categoryName:'مشروبات باردة', price:15, discountPrice:null, rating:4.2, orders:2500, stock:300, image:'https://images.unsplash.com/photo-1527960471264-932f39eb5846?w=400', desc:'مشروبات غازية متنوعة', featured:false, alcoholic:false },
            
            // Desserts
            { id:16, name:'تشيز كيك', nameEn:'Cheesecake', category:'desserts', categoryName:'حلويات', price:60, discountPrice:null, rating:4.9, orders:1600, stock:50, image:'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400', desc:'تشيز كيك نيويورك الأصلية', featured:true, alcoholic:false },
            { id:17, name:'براوني', nameEn:'Brownie', category:'desserts', categoryName:'حلويات', price:45, discountPrice:38, rating:4.8, orders:1400, stock:60, image:'https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=400', desc:'براوني شوكولاتة بلجيكية', featured:true, alcoholic:false },
            { id:18, name:'تيراميسو', nameEn:'Tiramisu', category:'desserts', categoryName:'حلويات', price:65, discountPrice:null, rating:4.9, orders:1200, stock:40, image:'https://images.unsplash.com/photo-1571877227200-a0d98ea607e9?w=400', desc:'تيراميسو إيطالي أصيل', featured:false, alcoholic:false },
            { id:19, name:'كوكيز', nameEn:'Cookies', category:'desserts', categoryName:'حلويات', price:25, discountPrice:null, rating:4.6, orders:2000, stock:100, image:'https://images.unsplash.com/photo-1499636136210-6f4ee915583e?w=400', desc:'كوكيز طازج يومياً', featured:false, alcoholic:false },
            { id:20, name:'كرواسون', nameEn:'Croissant', category:'desserts', categoryName:'حلويات', price:35, discountPrice:null, rating:4.7, orders:1700, stock:80, image:'https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=400', desc:'كرواسون فرنسي طازج', featured:false, alcoholic:false },
            { id:21, name:'كيك شوكولاتة', nameEn:'Chocolate Cake', category:'desserts', categoryName:'حلويات', price:70, discountPrice:60, rating:4.9, orders:1900, stock:30, image:'https://images.unsplash.com/photo-1578985545062-69928b1d9587?w=400', desc:'كيك شوكولاتة ثلاثي', featured:true, alcoholic:false },
            
            // Alcoholic Drinks
            { id:22, name:'ستيلا', nameEn:'Stella', category:'alcoholic', categoryName:'مشروبات كحولية', price:60, discountPrice:null, rating:4.5, orders:800, stock:200, image:'https://images.unsplash.com/photo-1566633806327-68e152aaf26d?w=400', desc:'بيرة ستيلا المحلية', featured:false, alcoholic:true },
            { id:23, name:'هاينكن', nameEn:'Heineken', category:'alcoholic', categoryName:'مشروبات كحولية', price:70, discountPrice:null, rating:4.6, orders:950, stock:150, image:'https://images.unsplash.com/photo-1618885472179-5e474019f2a9?w=400', desc:'بيرة هاينكن الهولندية', featured:true, alcoholic:true },
            { id:24, name:'كورونا', nameEn:'Corona', category:'alcoholic', categoryName:'مشروبات كحولية', price:65, discountPrice:null, rating:4.4, orders:700, stock:180, image:'https://images.unsplash.com/photo-1559526324-593bc073d938?w=400', desc:'بيرة كورونا المكسيكية', featured:false, alcoholic:true },
            { id:25, name:'فودكا', nameEn:'Vodka', category:'alcoholic', categoryName:'مشروبات كحولية', price:80, discountPrice:null, rating:4.7, orders:600, stock:100, image:'https://images.unsplash.com/photo-1569529465841-dfecdab7503b?w=400', desc:'فودكا نقية ممتازة', featured:true, alcoholic:true },
            { id:26, name:'ويسكي', nameEn:'Whiskey', category:'alcoholic', categoryName:'مشروبات كحولية', price:120, discountPrice:100, rating:4.8, orders:550, stock:80, image:'https://images.unsplash.com/photo-1527281400683-1aae777175f0?w=400', desc:'ويسكي سكوتش 12 سنة', featured:true, alcoholic:true },
            { id:27, name:'جاك دانيلز', nameEn:'Jack Daniels', category:'alcoholic', categoryName:'مشروبات كحولية', price:110, discountPrice:null, rating:4.8, orders:500, stock:70, image:'https://images.unsplash.com/photo-1580189094344-0b8b452b1e56?w=400', desc:'جاك دانيلز تينيسي', featured:false, alcoholic:true },
            { id:28, name:'موهيتو', nameEn:'Mojito', category:'alcoholic', categoryName:'مشروبات كحولية', price:75, discountPrice:null, rating:4.9, orders:1300, stock:100, image:'https://images.unsplash.com/photo-1551538827-9c037cb4f32a?w=400', desc:'موهيتو كوبي منعش', featured:true, alcoholic:true },
            { id:29, name:'مارغريتا', nameEn:'Margarita', category:'alcoholic', categoryName:'مشروبات كحولية', price:80, discountPrice:null, rating:4.7, orders:900, stock:100, image:'https://images.unsplash.com/photo-1556855810-ac404d3c2eba?w=400', desc:'مارغريتا كلاسيكية', featured:false, alcoholic:true },
            { id:30, name:'مارتيني', nameEn:'Martini', category:'alcoholic', categoryName:'مشروبات كحولية', price:85, discountPrice:null, rating:4.8, orders:750, stock:90, image:'https://images.unsplash.com/photo-1575023782549-62ca0d244b39?w=400', desc:'مارتيني جاف كلاسيكي', featured:true, alcoholic:true },
        ];

        const categories = [
            { id:'hot-drinks', name:'مشروبات ساخنة', icon:'fas fa-mug-hot', image:'https://images.unsplash.com/photo-1509042239860-f550ce710b93?w=600' },
            { id:'cold-drinks', name:'مشروبات باردة', icon:'fas fa-glass-whiskey', image:'https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?w=600' },
            { id:'desserts', name:'حلويات', icon:'fas fa-cake', image:'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=600' },
            { id:'alcoholic', name:'مشروبات كحولية', icon:'fas fa-wine-bottle', image:'https://images.unsplash.com/photo-1470337458703-46ad1756a187?w=600' },
        ];

        const blogPosts = [
            { title:'تاريخ القهوة العربية', slug:'arabic-coffee-history', image:'https://images.unsplash.com/photo-1509042239860-f550ce710b93?w=600', date:'2024-01-15', excerpt:'اكتشف تاريخ القهوة العربية الأصيلة...' },
            { title:'فن تحضير الإسبرسو', slug:'espresso-art', image:'https://images.unsplash.com/photo-1510707577719-ae7c14805e3a?w=600', date:'2024-02-20', excerpt:'أسرار تحضير الإسبرسو المثالي...' },
            { title:'أفضل كوكتيلات الصيف', slug:'summer-cocktails', image:'https://images.unsplash.com/photo-1551538827-9c037cb4f32a?w=600', date:'2024-03-10', excerpt:'كوكتيلات منعشة لفصل الصيف...' },
        ];

        const galleryImages = [
            'https://images.unsplash.com/photo-1470337458703-46ad1756a187?w=600',
            'https://images.unsplash.com/photo-1559925393-8be0ec4767c8?w=600',
            'https://images.unsplash.com/photo-1572116469696-31de0f17cc34?w=600',
            'https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=600',
            'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?w=600',
            'https://images.unsplash.com/photo-1552566626-52f8b828add9?w=600',
        ];

        // ==================== STATE ====================
        let cart = JSON.parse(localStorage.getItem('evilBarCart')) || [];
        let favorites = JSON.parse(localStorage.getItem('evilBarFavorites')) || [];
        let currentUser = JSON.parse(localStorage.getItem('evilBarUser')) || null;
        let currentPage = 'home';
        let isDarkMode = localStorage.getItem('evilBarTheme') !== 'light';
        let otpTimerInterval = null;

        // ==================== INITIALIZATION ====================
        document.addEventListener('DOMContentLoaded', function() {
            // Preloader
            setTimeout(() => {
                const preloader = document.getElementById('preloader');
                preloader.style.opacity = '0';
                preloader.style.transition = 'opacity 0.5s';
                setTimeout(() => preloader.remove(), 500);
            }, 1500);

            // Theme
            if (!isDarkMode) {
                document.body.classList.add('light-mode');
                document.getElementById('themeBtn').innerHTML = '<i class="fas fa-sun"></i>';
            }

            // User
            updateAuthUI();
            
            // Navigate
            navigateTo('home');
            
            // AOS
            AOS.init({ duration: 800, once: true, offset: 100 });
            
            // Update cart
            updateCartUI();
        });

        // ==================== NAVIGATION ====================
        function navigateTo(page, data = null) {
            currentPage = page;
            const content = document.getElementById('mainContent');
            
            switch(page) {
                case 'home': content.innerHTML = renderHome(); break;
                case 'menu': content.innerHTML = renderMenu(data); break;
                case 'reservation': content.innerHTML = renderReservation(); break;
                case 'gallery': content.innerHTML = renderGallery(); break;
                case 'blog': content.innerHTML = renderBlog(); break;
                case 'about': content.innerHTML = renderAbout(); break;
                case 'contact': content.innerHTML = renderContact(); break;
                case 'faq': content.innerHTML = renderFAQ(); break;
                case 'privacy': content.innerHTML = renderPrivacy(); break;
                case 'terms': content.innerHTML = renderTerms(); break;
                case 'favorites': content.innerHTML = renderFavorites(); break;
                case 'profile': content.innerHTML = renderProfile(); break;
                case 'orderHistory': content.innerHTML = renderOrderHistory(); break;
                default: content.innerHTML = render404();
            }
            
            window.scrollTo({ top: 0, behavior: 'smooth' });
            AOS.refresh();
            
            // GSAP animations
            gsap.from('.animate-in', { duration: 0.6, y: 30, opacity: 0, stagger: 0.1, ease: 'power2.out' });
        }

        // ==================== RENDER FUNCTIONS ====================
        function renderHome() {
            const featured = products.filter(p => p.featured).slice(0, 8);
            let html = `
                <section class="hero-section">
                    <div class="text-center" style="position:relative;z-index:1;">
                        <h1 class="hero-title neon-text animate-in">EVIL BAR</h1>
                        <p class="hero-subtitle animate-in">أفخم تجربة قهوة وبار في المدينة</p>
                        <div class="animate-in">
                            <a href="#" onclick="navigateTo('menu')" class="btn btn-gold btn-lg me-2">📋 تصفح القائمة</a>
                            <a href="#" onclick="navigateTo('reservation')" class="btn btn-outline-gold btn-lg">🍽 احجز طاولة</a>
                        </div>
                    </div>
                    <div class="scroll-indicator"><span></span><span></span><span></span></div>
                </section>

                <section class="py-5">
                    <div class="container">
                        <h2 class="section-title text-center animate-in"><span class="gold-text">منتجاتنا</span> المميزة</h2>
                        <div class="row">
                            ${featured.map((p, i) => `
                                <div class="col-lg-3 col-md-6 mb-4 animate-in" style="animation-delay:${i*0.1}s">
                                    ${productCard(p)}
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </section>

                <section class="py-5" style="background:var(--bg-secondary);">
                    <div class="container">
                        <h2 class="section-title text-center animate-in"><span class="gold-text">أقسام</span> القائمة</h2>
                        <div class="row">
                            ${categories.map((c, i) => `
                                <div class="col-md-3 col-sm-6 mb-4 animate-in" style="animation-delay:${i*0.1}s">
                                    <a href="#" onclick="navigateTo('menu', '${c.id}')" class="glass-card category-card">
                                        <div class="category-icon"><i class="${c.icon}"></i></div>
                                        <h5>${c.name}</h5>
                                    </a>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </section>

                <section class="cta-section text-center">
                    <h2 class="text-white mb-3 animate-in">احجز طاولتك الآن</h2>
                    <p class="text-white mb-4 animate-in">استمتع بأجواء راقية وخدمة ممتازة في Evil Bar</p>
                    <a href="#" onclick="navigateTo('reservation')" class="btn btn-gold btn-lg animate-in">احجز الآن</a>
                </section>
            `;
            return html;
        }

        function renderMenu(categoryFilter = null) {
            let filtered = products;
            if (categoryFilter) {
                filtered = products.filter(p => p.category === categoryFilter);
            }
            
            let html = `
                <section class="page-content">
                    <div class="container">
                        <h1 class="gold-text text-center mb-4 animate-in">📋 القائمة</h1>
                        <div class="text-center mb-4 animate-in">
                            <button class="btn btn-outline-gold m-1" onclick="navigateTo('menu')">الكل</button>
                            ${categories.map(c => `
                                <button class="btn btn-outline-gold m-1" onclick="navigateTo('menu', '${c.id}')">
                                    <i class="${c.icon}"></i> ${c.name}
                                </button>
                            `).join('')}
                        </div>
                        <div class="row">
                            ${filtered.map((p, i) => `
                                <div class="col-lg-3 col-md-4 col-sm-6 mb-4 animate-in" style="animation-delay:${i*0.05}s">
                                    ${productCard(p)}
                                </div>
                            `).join('')}
                        </div>
                        ${filtered.length === 0 ? '<p class="text-center">لا توجد منتجات في هذا القسم</p>' : ''}
                    </div>
                </section>
            `;
            return html;
        }

        function productCard(p) {
            const isFav = favorites.includes(p.id);
            return `
                <div class="product-card glass-card">
                    <div class="product-img">
                        <img src="${p.image}" alt="${p.name}" onerror="this.src='https://via.placeholder.com/400x250/111/333?text=Evil+Bar'">
                        ${p.discountPrice ? `<span class="discount-badge">-${Math.round((1-p.discountPrice/p.price)*100)}%</span>` : ''}
                        <div class="product-actions">
                            <button class="btn-fav ${isFav ? 'active' : ''}" onclick="event.stopPropagation();toggleFavorite(${p.id})">
                                <i class="${isFav ? 'fas' : 'far'} fa-heart"></i>
                            </button>
                            <button class="btn-cart" onclick="event.stopPropagation();addToCart(${p.id})">
                                <i class="fas fa-shopping-cart"></i>
                            </button>
                        </div>
                    </div>
                    <div class="p-3">
                        <h5 class="mb-1">${p.name}</h5>
                        <p class="text-muted small mb-2">${p.desc}</p>
                        <div class="mb-2">
                            ${p.discountPrice ? `
                                <span class="old-price">${p.price} ج.م</span>
                                <span class="current-price">${p.discountPrice} ج.م</span>
                            ` : `
                                <span class="current-price">${p.price} ج.م</span>
                            `}
                        </div>
                        <div class="stars mb-2">
                            ${renderStars(p.rating)}
                            <small class="text-muted">(${p.ordersCount || p.orders})</small>
                        </div>
                        <button class="btn btn-gold btn-sm w-100" onclick="addToCart(${p.id})">
                            <i class="fas fa-cart-plus"></i> أضف للسلة
                        </button>
                    </div>
                </div>
            `;
        }

        function renderStars(rating) {
            let html = '';
            for (let i = 1; i <= 5; i++) {
                if (i <= Math.floor(rating)) html += '<i class="fas fa-star"></i>';
                else if (i - 0.5 <= rating) html += '<i class="fas fa-star-half-alt"></i>';
                else html += '<i class="far fa-star"></i>';
            }
            html += ` <span class="gold-text">${rating}</span>`;
            return html;
        }

        function renderReservation() {
            return `
                <section class="page-content">
                    <div class="container">
                        <div class="glass-card p-5 animate-in" style="max-width:600px;margin:0 auto;">
                            <h1 class="gold-text text-center mb-4">🍽 حجز طاولة</h1>
                            <form onsubmit="submitReservation(event)">
                                <div class="mb-3">
                                    <label class="form-label">عدد الضيوف</label>
                                    <select class="form-select bg-dark text-white" id="guests">
                                        <option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><option>6+</option>
                                    </select>
                                </div>
                                <div class="mb-3">
                                    <label class="form-label">التاريخ</label>
                                    <input type="date" class="form-control bg-dark text-white" id="resDate" required>
                                </div>
                                <div class="mb-3">
                                    <label class="form-label">الوقت</label>
                                    <input type="time" class="form-control bg-dark text-white" id="resTime" required>
                                </div>
                                <div class="mb-3">
                                    <label class="form-label">طلبات خاصة</label>
                                    <textarea class="form-control bg-dark text-white" id="resRequests" rows="3"></textarea>
                                </div>
                                <button type="submit" class="btn btn-gold w-100">تأكيد الحجز ✅</button>
                            </form>
                        </div>
                    </div>
                </section>
            `;
        }

        function renderGallery() {
            return `
                <section class="page-content">
                    <div class="container">
                        <h1 class="gold-text text-center mb-4 animate-in">🖼 معرض الصور</h1>
                        <div class="row">
                            ${galleryImages.map((img, i) => `
                                <div class="col-md-4 mb-4 animate-in" style="animation-delay:${i*0.1}s">
                                    <div class="glass-card overflow-hidden">
                                        <img src="${img}" class="w-100" style="height:300px;object-fit:cover;transition:0.3s;" 
                                             onmouseover="this.style.transform='scale(1.05)'" onmouseout="this.style.transform='scale(1)'">
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </section>
            `;
        }

        function renderBlog() {
            return `
                <section class="page-content">
                    <div class="container">
                        <h1 class="gold-text text-center mb-4 animate-in">📰 المدونة</h1>
                        <div class="row">
                            ${blogPosts.map((post, i) => `
                                <div class="col-md-4 mb-4 animate-in" style="animation-delay:${i*0.1}s">
                                    <div class="glass-card overflow-hidden">
                                        <img src="${post.image}" class="w-100" style="height:200px;object-fit:cover;">
                                        <div class="p-3">
                                            <h5>${post.title}</h5>
                                            <p class="text-muted small">${post.date}</p>
                                            <p>${post.excerpt}</p>
                                            <button class="btn btn-outline-gold btn-sm">اقرأ المزيد →</button>
                                        </div>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </section>
            `;
        }

        function renderAbout() {
            return `
                <section class="page-content">
                    <div class="container">
                        <div class="glass-card p-5 animate-in">
                            <h1 class="gold-text">ℹ️ من نحن</h1>
                            <p class="lead">Evil Bar هو أفخم كافيه وبار في المدينة، تأسس عام 2020.</p>
                            <p>نقدم أجود أنواع القهوة المحضرة على أيدي أمهر الباريستا، وألذ الحلويات الطازجة يومياً، وأفضل المشروبات في أجواء راقية وفاخرة.</p>
                            <h5 class="gold-text mt-4">🎯 رؤيتنا</h5>
                            <p>أن نكون الوجهة الأولى لعشاق القهوة والمشروبات الفاخرة في المنطقة.</p>
                            <h5 class="gold-text">💎 قيمنا</h5>
                            <ul>
                                <li>الجودة العالية في كل كوب</li>
                                <li>الخدمة الممتازة</li>
                                <li>الأجواء الراقية</li>
                                <li>الابتكار المستمر</li>
                            </ul>
                        </div>
                    </div>
                </section>
            `;
        }

        function renderContact() {
            return `
                <section class="page-content">
                    <div class="container">
                        <div class="glass-card p-5 animate-in" style="max-width:600px;margin:0 auto;">
                            <h1 class="gold-text text-center mb-4">📞 اتصل بنا</h1>
                            <form onsubmit="submitContact(event)">
                                <input type="text" class="form-control mb-3 bg-dark text-white" placeholder="الاسم" id="contactName" required>
                                <input type="email" class="form-control mb-3 bg-dark text-white" placeholder="البريد الإلكتروني" id="contactEmail" required>
                                <input type="text" class="form-control mb-3 bg-dark text-white" placeholder="الموضوع" id="contactSubject" required>
                                <textarea class="form-control mb-3 bg-dark text-white" rows="5" placeholder="الرسالة" id="contactMessage" required></textarea>
                                <button type="submit" class="btn btn-gold w-100">إرسال ✉️</button>
                            </form>
                        </div>
    
