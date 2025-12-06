<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CareerMatch Pro - Tư Vấn Chọn Ngành & Trường Đại Học</title>
    <!-- Tải Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Tải Chart.js cho biểu đồ -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.1/dist/chart.min.js"></script>
    
    <!-- FIX: Tải thư viện Lucide Icons dưới dạng script thường và sử dụng biến toàn cục -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <script>
        // Hàm này sẽ được gọi khi nội dung DOM đã sẵn sàng hoặc khi nội dung động được chèn
        window.createLucideIcons = () => {
            // Kiểm tra xem đối tượng lucide đã được định nghĩa chưa
            if (typeof lucide !== 'undefined' && lucide.createIcons) {
                lucide.createIcons();
            }
        };
        // Gọi hàm tạo icon khi trang đã tải xong
        window.addEventListener('load', window.createLucideIcons);
    </script>
    <style>
        /* Cấu hình Tailwind CSS */
        :root {
            --color-primary: #2E7DFF; /* Xanh chủ đạo */
            --color-secondary: #0D1A2D; /* Text */
            --color-background-light: #EEF4FF; /* Background nhẹ */
        }
        
        /* Font Poppins làm font chính */
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            color: var(--color-secondary);
            background-color: #fff;
        }

        /* Custom scrollbar cho các trình duyệt WebKit */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: var(--color-background-light);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--color-primary);
            border-radius: 4px;
        }
        
        /* Hiệu ứng chuyển động mượt */
        .transition-all {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        /* Button Primary */
        .btn-primary {
            background-color: var(--color-primary);
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 0.75rem; /* rounded-xl */
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(46, 125, 255, 0.4);
            transition: all 0.3s ease;
        }
        .btn-primary:hover {
            background-color: #1a64f7;
            box-shadow: 0 6px 20px rgba(46, 125, 255, 0.6);
            transform: translateY(-2px);
        }

        /* Modal Backdrop */
        .modal-backdrop {
            background-color: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(5px);
        }

        /* Ẩn các trang (views) và chỉ hiển thị trang hiện tại */
        .view {
            display: none;
        }
        .view.active {
            display: block;
        }
    </style>
</head>
<body>

<!-- MÔ PHỎNG HỆ THỐNG AUTHENTICATION VÀ STATE MANAGEMENT -->
<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { getFirestore, doc, setDoc, getDoc, onSnapshot, collection, query, updateDoc, arrayUnion } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
    import { setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
    
    // Bắt buộc phải sử dụng các biến global có sẵn
    const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-careermatch-id';
    const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : null;
    const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

    let app, db, auth;
    let userId = 'guest_user'; // Mặc định là khách

    window.authState = {
        isReady: false,
        isAuthenticated: false,
        userId: userId,
        userData: {
            name: "Học Sinh Khách",
            tests: [], // Lịch sử bài test
            favorites: [] // Ngành/trường yêu thích
        }
    };

    // Hàm chuyển đổi Base64 sang ArrayBuffer
    function base64ToArrayBuffer(base64) {
        const binaryString = atob(base64);
        const len = binaryString.length;
        const bytes = new Uint8Array(len);
        for (let i = 0; i < len; i++) {
            bytes[i] = binaryString.charCodeAt(i);
        }
        return bytes.buffer;
    }

    // Khởi tạo Firebase và đăng nhập
    async function initializeFirebase() {
        if (!firebaseConfig) {
            console.error("Firebase config is missing.");
            window.authState.isReady = true;
            updateUIState();
            return;
        }

        // Đặt mức log
        setLogLevel('debug');

        app = initializeApp(firebaseConfig);
        auth = getAuth(app);
        db = getFirestore(app);

        // Đăng nhập với Custom Token hoặc Ẩn danh
        try {
            if (initialAuthToken) {
                await signInWithCustomToken(auth, initialAuthToken);
            } else {
                await signInAnonymously(auth);
            }
        } catch (error) {
            console.error("Firebase Auth failed:", error);
            // Vẫn tiếp tục với trạng thái chưa xác thực nếu auth thất bại
            window.authState.isReady = true;
            updateUIState();
            return;
        }

        // Lắng nghe trạng thái đăng nhập
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                window.authState.isAuthenticated = !user.isAnonymous;
                window.authState.userId = user.uid;
                userId = user.uid;
                
                // Lắng nghe dữ liệu người dùng
                const userDocRef = doc(db, "artifacts", appId, "users", userId, "profile", "data");
                onSnapshot(userDocRef, (docSnap) => {
                    if (docSnap.exists()) {
                        window.authState.userData = { ...window.authState.userData, ...docSnap.data() };
                        console.log("User data updated:", window.authState.userData);
                        updateUIState();
                    } else {
                        // Tạo hồ sơ người dùng mới
                        const defaultProfile = {
                            name: `User ${user.uid.substring(0, 4)}`,
                            tests: [],
                            favorites: [],
                            createdAt: new Date().toISOString()
                        };
                        setDoc(userDocRef, defaultProfile).catch(e => console.error("Error setting initial profile:", e));
                        window.authState.userData = defaultProfile;
                        updateUIState();
                    }
                }, (error) => {
                    console.error("Error listening to user data:", error);
                });

            } else {
                // User signed out or anonymous
                window.authState.isAuthenticated = false;
                window.authState.userId = 'guest_user';
                userId = 'guest_user';
                window.authState.userData = {
                    name: "Học Sinh Khách",
                    tests: [],
                    favorites: []
                };
            }
            window.authState.isReady = true;
            updateUIState();
        });
    }

    // Hàm cập nhật trạng thái UI
    function updateUIState() {
        const authStatusElement = document.getElementById('auth-status');
        if (authStatusElement) {
            authStatusElement.textContent = window.authState.userData.name;
        }
        // Có thể gọi hàm render lại các phần phụ thuộc vào dữ liệu người dùng tại đây
    }
    
    // Hàm lưu kết quả test vào Firestore
    window.saveTestResult = async (testType, resultData) => {
        if (!window.authState.isReady || !db || window.authState.userId === 'guest_user') {
            displayMessage("Vui lòng Đăng nhập/Đăng ký để lưu kết quả.", "warning");
            return;
        }
        try {
            const userDocRef = doc(db, "artifacts", appId, "users", userId, "profile", "data");
            const newTestResult = {
                type: testType,
                date: new Date().toISOString(),
                result: resultData
            };
            
            await updateDoc(userDocRef, {
                tests: arrayUnion(newTestResult)
            });
            displayMessage("Kết quả đã được lưu vào Lịch sử bài test của bạn!", "success");
        } catch (error) {
            console.error("Error saving test result:", error);
            displayMessage("Lỗi khi lưu kết quả. Vui lòng thử lại.", "error");
        }
    };

    // Khởi tạo Firebase khi DOM sẵn sàng
    document.addEventListener('DOMContentLoaded', initializeFirebase);
    
</script>

<!-- KHUNG CHỨA TOÀN BỘ NỘI DUNG -->
<div id="app-container" class="min-h-screen flex flex-col">

    <!-- HEADER (Menu & Auth) -->
    <header class="sticky top-0 z-40 bg-white shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex justify-between items-center">
            <!-- Logo -->
            <a href="#" class="flex items-center space-x-2" onclick="changeView('home')">
                <div class="text-xl font-extrabold text-white bg-blue-500 p-2 rounded-lg">CM</div>
                <span class="text-xl font-bold text-gray-800">CareerMatch Pro</span>
            </a>

            <!-- Menu (Desktop) -->
            <nav class="hidden md:flex space-x-8 text-gray-600 font-medium">
                <a href="#" class="hover:text-blue-600 transition-colors" onclick="changeView('home')">Trang Chủ</a>
                <a href="#test" class="hover:text-blue-600 transition-colors" onclick="changeView('test-selection')">Làm Test</a>
                <a href="#report" class="hover:text-blue-600 transition-colors" onclick="changeView('report')">Phân Tích</a>
                <a href="#blog" class="hover:text-blue-600 transition-colors">Thư Viện</a>
                <a href="#contact" class="hover:text-blue-600 transition-colors">Liên Hệ</a>
            </nav>

            <!-- Đăng nhập/Đăng ký (Desktop) -->
            <div class="hidden md:flex items-center space-x-4">
                <span id="auth-status" class="text-sm font-semibold text-gray-600">Loading...</span>
                <button class="btn-primary" onclick="showModal('auth-modal')">
                    Đăng Nhập
                </button>
            </div>

            <!-- Mobile Menu Button -->
            <button class="md:hidden p-2 rounded-lg text-gray-600 hover:bg-gray-100" onclick="toggleMobileMenu()">
                <i data-lucide="menu" class="w-6 h-6"></i>
            </button>
        </div>

        <!-- Mobile Menu (Ẩn/Hiện) -->
        <div id="mobile-menu" class="md:hidden absolute w-full bg-white shadow-lg py-2 transition-all duration-300 transform -translate-y-full opacity-0">
            <nav class="flex flex-col space-y-2 px-4 pb-2 text-gray-700 font-medium">
                <a href="#" class="py-2 hover:bg-gray-50 rounded-lg" onclick="changeView('home'); toggleMobileMenu()">Trang Chủ</a>
                <a href="#test" class="py-2 hover:bg-gray-50 rounded-lg" onclick="changeView('test-selection'); toggleMobileMenu()">Làm Test</a>
                <a href="#report" class="py-2 hover:bg-gray-50 rounded-lg" onclick="changeView('report'); toggleMobileMenu()">Phân Tích</a>
                <a href="#blog" class="py-2 hover:bg-gray-50 rounded-lg">Thư Viện</a>
                <a href="#contact" class="py-2 hover:bg-gray-50 rounded-lg">Liên Hệ</a>
                <hr class="my-2">
                <div class="flex items-center justify-between py-2">
                    <span id="auth-status-mobile" class="text-sm font-semibold text-gray-600">Loading...</span>
                    <button class="btn-primary text-sm" onclick="showModal('auth-modal'); toggleMobileMenu()">
                        Đăng Nhập
                    </button>
                </div>
            </nav>
        </div>
    </header>

    <!-- CONTENT AREA (Các View) -->
    <main class="flex-grow">
        
        <!-- MESSAGE BOX (Cho thông báo lỗi/thành công) -->
        <div id="message-box" class="fixed top-20 right-5 z-50 transition-transform duration-500 transform translate-x-full">
            <!-- Messages will be inserted here -->
        </div>

        <!-- 1. HOME VIEW -->
        <section id="home-view" class="view active">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                
                <!-- Banner Hero -->
                <div class="bg-gradient-to-r from-indigo-500 to-blue-500 rounded-3xl p-8 lg:p-16 mt-8 flex flex-col lg:flex-row items-center justify-between shadow-xl">
                    <div class="lg:w-1/2 text-white">
                        <h1 class="text-4xl lg:text-5xl font-extrabold leading-tight mb-4">
                            Khám Phá CareerMatch Pro: Tương Lai Nghề Nghiệp Trong Tầm Tay
                        </h1>
                        <p class="text-lg lg:text-xl font-light opacity-90 mb-8">
                            Phân tích **Sở thích, Năng lực & Tính cách** của bạn để tìm ra ngành nghề và trường đại học phù hợp nhất tại Việt Nam.
                        </p>
                        <button class="btn-primary bg-white text-blue-600 hover:bg-gray-100 shadow-none hover:shadow-lg" onclick="changeView('test-selection')">
                            <i data-lucide="compass" class="inline w-5 h-5 mr-2"></i> Bắt đầu tư vấn ngành nghề
                        </button>
                    </div>
                    <div class="lg:w-1/3 mt-8 lg:mt-0">
                        <!-- Hình minh họa 3D/Gradient -->
                        <div class="w-full aspect-square bg-white bg-opacity-10 rounded-full flex items-center justify-center p-4">
                             
                        </div>
                    </div>
                </div>

                <!-- Thống kê -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 py-16 text-center">
                    <div class="p-6 bg-white rounded-2xl shadow-lg border-t-4 border-blue-500">
                        <p class="text-5xl font-extrabold text-blue-600">120+</p>
                        <p class="text-gray-500 mt-2 font-medium">Ngành Nghề Phân Tích</p>
                    </div>
                    <div class="p-6 bg-white rounded-2xl shadow-lg border-t-4 border-indigo-500">
                        <p class="text-5xl font-extrabold text-indigo-600">300+</p>
                        <p class="text-gray-500 mt-2 font-medium">Trường Đại Học Việt Nam</p>
                    </div>
                    <div class="p-6 bg-white rounded-2xl shadow-lg border-t-4 border-sky-500">
                        <p class="text-5xl font-extrabold text-sky-600">50K+</p>
                        <p class="text-gray-500 mt-2 font-medium">Học Sinh Đã Tư Vấn</p>
                    </div>
                </div>

                <!-- Quy trình 3 bước -->
                <div class="py-16">
                    <h2 class="text-3xl font-bold text-center mb-12">Quy Trình Khám Phá Tương Lai Của Bạn</h2>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                        <!-- Bước 1 -->
                        <div class="text-center p-6 bg-white rounded-xl shadow-md hover:shadow-xl transition-all border border-gray-100">
                            <div class="w-16 h-16 mx-auto mb-4 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center font-bold text-2xl border-4 border-blue-300">1</div>
                            <h3 class="text-xl font-semibold mb-2">Làm Bài Trắc Nghiệm</h3>
                            <p class="text-gray-500">Hoàn thành các bài Test Holland, MBTI, Năng lực học tập để phân tích sâu sắc bản thân.</p>
                        </div>
                        <!-- Bước 2 -->
                        <div class="text-center p-6 bg-white rounded-xl shadow-md hover:shadow-xl transition-all border border-gray-100">
                            <div class="w-16 h-16 mx-auto mb-4 bg-indigo-100 text-indigo-600 rounded-full flex items-center justify-center font-bold text-2xl border-4 border-indigo-300">2</div>
                            <h3 class="text-xl font-semibold mb-2">Nhận Báo Cáo Phân Tích</h3>
                            <p class="text-gray-500">Thuật toán AI tổng hợp dữ liệu, tạo báo cáo tính cách, sở thích và điểm mạnh cá nhân.</p>
                        </div>
                        <!-- Bước 3 -->
                        <div class="text-center p-6 bg-white rounded-xl shadow-md hover:shadow-xl transition-all border border-gray-100">
                            <div class="w-16 h-16 mx-auto mb-4 bg-sky-100 text-sky-600 rounded-full flex items-center justify-center font-bold text-2xl border-4 border-sky-300">3</div>
                            <h3 class="text-xl font-semibold mb-2">Xem Gợi Ý Ngành & Trường</h3>
                            <p class="text-gray-500">Danh sách các Ngành nghề và Trường đại học (có Điểm chuẩn, Học phí) phù hợp với bạn.</p>
                        </div>
                    </div>
                </div>

                <!-- Testimonials -->
                <div class="py-16 bg-gray-50 rounded-2xl p-8 mb-8">
                    <h2 class="text-3xl font-bold text-center mb-12">Học Sinh Đã Nói Gì?</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                        <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-blue-500">
                            <i data-lucide="quote" class="w-8 h-8 text-blue-500 mb-3"></i>
                            <p class="text-gray-600 italic mb-4">"Nhờ CareerMatch Pro, em đã hiểu rõ mình thuộc nhóm tính cách nào và tự tin đăng ký ngành Công nghệ Thông tin!"</p>
                            <p class="font-semibold text-gray-800">- Nguyễn Văn A, THPT Chuyên Lê Quý Đôn</p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-indigo-500">
                            <i data-lucide="quote" class="w-8 h-8 text-indigo-500 mb-3"></i>
                            <p class="text-gray-600 italic mb-4">"Biểu đồ Holland rất trực quan, giúp em dễ dàng so sánh điểm mạnh yếu. Báo cáo gợi ý trường rất chi tiết."</p>
                            <p class="font-semibold text-gray-800">- Trần Thị B, THPT Trần Đại Nghĩa</p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-sky-500">
                            <i data-lucide="quote" class="w-8 h-8 text-sky-500 mb-3"></i>
                            <p class="text-gray-600 italic mb-4">"Chatbot AI trả lời cực kỳ nhanh và chuẩn xác. Em đã tìm được câu trả lời cho băn khoăn về học phí trường Y."</p>
                            <p class="font-semibold text-gray-800">- Lê Hoàng C, THPT Amsterdam</p>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- 2. TEST SELECTION VIEW -->
        <section id="test-selection-view" class="view">
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
                <h2 class="text-4xl font-extrabold text-center mb-4">Làm Bài Trắc Nghiệm Hướng Nghiệp</h2>
                <p class="text-center text-gray-600 mb-10">Hoàn thành ít nhất 2 bài test để nhận báo cáo phân tích toàn diện nhất!</p>
                
                <div class="space-y-6">
                    <!-- Test Holland -->
                    <div class="p-6 bg-white rounded-xl shadow-lg border-l-8 border-blue-500 flex justify-between items-center">
                        <div>
                            <h3 class="text-2xl font-bold text-gray-800 mb-1 flex items-center"><i data-lucide="heart" class="w-6 h-6 mr-2 text-blue-500"></i> Test Sở Thích (Holland - RIASEC)</h3>
                            <p class="text-gray-500">Phân tích 6 nhóm sở thích nghề nghiệp (60 câu hỏi).</p>
                        </div>
                        <button class="btn-primary" onclick="changeView('holland-test')">
                            Bắt Đầu
                        </button>
                    </div>

                    <!-- Test MBTI -->
                    <div class="p-6 bg-white rounded-xl shadow-lg border-l-8 border-indigo-500 flex justify-between items-center">
                        <div>
                            <h3 class="text-2xl font-bold text-gray-800 mb-1 flex items-center"><i data-lucide="user-check" class="w-6 h-6 mr-2 text-indigo-500"></i> Test Tính Cách (MBTI)</h3>
                            <p class="text-gray-500">Phân tích 16 nhóm tính cách (25 câu hỏi).</p>
                        </div>
                        <button class="btn-primary" onclick="changeView('mbti-test')">
                            Bắt Đầu
                        </button>
                    </div>

                    <!-- Test Năng Lực Học Tập -->
                    <div class="p-6 bg-white rounded-xl shadow-lg border-l-8 border-green-500 flex justify-between items-center">
                        <div>
                            <h3 class="text-2xl font-bold text-gray-800 mb-1 flex items-center"><i data-lucide="brain" class="w-6 h-6 mr-2 text-green-500"></i> Test Năng Lực Học Tập</h3>
                            <p class="text-gray-500">Đánh giá Tư duy Logic, Ngôn ngữ, Toán học, Ghi nhớ (4 phần).</p>
                        </div>
                        <button class="btn-primary opacity-50 cursor-not-allowed">
                            Sắp Ra Mắt
                        </button>
                    </div>
                </div>

            </div>
        </section>
        
        <!-- 3. HOLLAND TEST VIEW -->
        <section id="holland-test-view" class="view">
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
                <h2 class="text-3xl font-bold text-center mb-4">Trắc Nghiệm Sở Thích Nghề Nghiệp Holland</h2>
                <p class="text-center text-gray-600 mb-8">Hãy chọn mức độ bạn **thích** hoặc **không thích** thực hiện các hoạt động sau. (Tổng 60 câu)</p>
                
                <div id="holland-questions" class="bg-white p-6 rounded-xl shadow-lg">
                    <!-- Questions will be dynamically inserted here -->
                </div>

                <div class="flex justify-between items-center mt-6">
                    <button id="holland-prev-btn" class="btn-primary bg-gray-400 hover:bg-gray-500" disabled>
                        <i data-lucide="arrow-left" class="inline w-5 h-5 mr-1"></i> Quay lại
                    </button>
                    <div id="holland-progress" class="text-sm font-medium text-gray-600">Câu 1/60</div>
                    <button id="holland-next-btn" class="btn-primary" onclick="nextHollandQuestion()">
                        Tiếp theo <i data-lucide="arrow-right" class="inline w-5 h-5 ml-1"></i>
                    </button>
                    <button id="holland-submit-btn" class="btn-primary hidden bg-green-500 hover:bg-green-600" onclick="calculateHollandResult()">
                        Xem Kết Quả <i data-lucide="send" class="inline w-5 h-5 ml-1"></i>
                    </button>
                </div>

            </div>
        </section>
        
        <!-- 3.5. MBTI TEST VIEW (New View) -->
        <section id="mbti-test-view" class="view">
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
                <h2 class="text-3xl font-bold text-center mb-4">Trắc Nghiệm Tính Cách MBTI</h2>
                <p class="text-center text-gray-600 mb-8">Bạn sẽ trả lời 25 câu hỏi để xác định nhóm tính cách 16 loại của mình. (Mô phỏng 1 câu)</p>
                
                <div id="mbti-questions" class="bg-white p-6 rounded-xl shadow-lg space-y-6">
                    <!-- Sample MBTI Question 1/25 -->
                    <div class="border-b pb-4">
                        <p class="text-xl font-semibold mb-3 text-gray-800">Câu 1/25: Khi bạn cảm thấy tràn đầy năng lượng nhất, bạn thường là người hướng ngoại (E) hay hướng nội (I)?</p>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                            <label class="p-3 border-2 rounded-xl bg-blue-50 text-blue-800 hover:bg-blue-200 cursor-pointer transition-colors flex items-center">
                                <input type="radio" name="mbti-q1" value="E" class="mr-2 h-5 w-5 accent-blue-600"> Hướng Ngoại (E) - Dành thời gian với người khác
                            </label>
                            <label class="p-3 border-2 rounded-xl bg-green-50 text-green-800 hover:bg-green-200 cursor-pointer transition-colors flex items-center">
                                <input type="radio" name="mbti-q1" value="I" class="mr-2 h-5 w-5 accent-green-600"> Hướng Nội (I) - Dành thời gian một mình
                            </label>
                        </div>
                    </div>
                    
                    <p class="text-center text-gray-500 italic">Vui lòng hoàn thành bài test đầy đủ 25 câu để nhận kết quả chi tiết.</p>
                </div>

                <div class="flex justify-center mt-6">
                    <button class="btn-primary bg-green-500 hover:bg-green-600" onclick="changeView('report')">
                        Hoàn Thành & Xem Kết Quả (Mô phỏng)
                    </button>
                </div>
                <div class="text-center mt-4">
                    <button class="text-blue-500 hover:text-blue-700 text-sm" onclick="changeView('test-selection')">Quay lại trang chọn Test</button>
                </div>
            </div>
        </section>

        
        <!-- 4. HOLLAND RESULT / REPORT VIEW -->
        <section id="report-view" class="view">
            <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
                <h2 class="text-4xl font-extrabold text-center mb-4 text-blue-700">Báo Cáo Phân Tích Hướng Nghiệp Cá Nhân</h2>
                <p class="text-center text-gray-600 mb-10">Tổng hợp từ các bài trắc nghiệm (Holland, MBTI) và năng lực học tập của bạn.</p>

                <!-- Holland Result Section -->
                <div id="holland-result-section" class="bg-white p-8 rounded-2xl shadow-xl mb-10 border-t-8 border-blue-500">
                    <h3 class="text-3xl font-bold mb-6 flex items-center text-blue-600">
                        <i data-lucide="bar-chart-3" class="w-7 h-7 mr-3"></i> Kết Quả Trắc Nghiệm Sở Thích Holland (RIASEC)
                    </h3>
                    <div class="flex flex-col lg:flex-row gap-8">
                        <div class="lg:w-1/2">
                            <canvas id="holland-chart"></canvas>
                            <!-- Chú thích RIASEC -->
                            <div class="mt-6 space-y-2 text-sm text-gray-700">
                                <p><span class="font-bold text-red-500">R (Realistic):</span> Hiện thực, Kỹ thuật</p>
                                <p><span class="font-bold text-indigo-500">I (Investigative):</span> Nghiên cứu, Khoa học</p>
                                <p><span class="font-bold text-green-500">A (Artistic):</span> Nghệ thuật, Sáng tạo</p>
                                <p><span class="font-bold text-yellow-600">S (Social):</span> Xã hội, Phục vụ</p>
                                <p><span class="font-bold text-blue-500">E (Enterprising):</span> Quản lý, Lãnh đạo</p>
                                <p><span class="font-bold text-purple-500">C (Conventional):</span> Nghiệp vụ, Tổ chức</p>
                            </div>
                        </div>
                        <div class="lg:w-1/2">
                            <h4 class="text-2xl font-semibold mb-3">Mã Holland Của Bạn: <span id="holland-code" class="text-blue-600 font-extrabold text-3xl">???</span></h4>
                            <p id="holland-summary" class="text-gray-700 leading-relaxed mb-4">
                                Dựa trên kết quả, nhóm sở thích nổi trội của bạn là ...
                            </p>
                            <h4 class="text-xl font-semibold mt-6 mb-3">Ngành Nghề Gợi Ý Loại 1 (Phù Hợp Nhất)</h4>
                            <ul id="holland-career-suggestions" class="list-disc list-inside space-y-2 pl-4 text-gray-700">
                                <!-- Suggestions here -->
                                <li>Loading...</li>
                            </ul>
                        </div>
                    </div>
                </div>
                
                <!-- MBTI Result Section (Mô phỏng) -->
                <div class="bg-white p-8 rounded-2xl shadow-xl mb-10 border-t-8 border-indigo-500">
                    <h3 class="text-3xl font-bold mb-6 flex items-center text-indigo-600">
                        <i data-lucide="aperture" class="w-7 h-7 mr-3"></i> Kết Quả Trắc Nghiệm Tính Cách MBTI
                    </h3>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                        <div>
                            <p class="text-xl font-bold mb-2">Nhóm Tính Cách Chính:</p>
                            <div id="mbti-type" class="text-5xl font-extrabold text-indigo-600 mb-4">INFJ</div>
                            <p id="mbti-description" class="text-gray-700 italic">"Người bảo vệ" - Luôn nhìn nhận mọi thứ qua lăng kính ý nghĩa sâu sắc và giá trị cá nhân. Tính cách hiếm có và giàu lòng trắc ẩn.</p>
                            <ul class="mt-4 space-y-2 text-gray-700">
                                <li><span class="font-semibold">I (Introversion):</span> 75%</li>
                                <li><span class="font-semibold">N (Intuition):</span> 80%</li>
                                <li><span class="font-semibold">F (Feeling):</span> 65%</li>
                                <li><span class="font-semibold">J (Judging):</span> 90%</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-xl font-semibold mt-2 mb-3">Ngành Nghề Phù Hợp Với INFJ</h4>
                            <ul class="list-disc list-inside space-y-2 pl-4 text-gray-700">
                                <li>Nhà tư vấn tâm lý</li>
                                <li>Giáo viên/Giảng viên</li>
                                <li>Tác giả, Nhà văn</li>
                                <li>Thiết kế đồ họa, Sáng tạo nội dung</li>
                            </ul>
                            <a href="#" class="inline-block mt-4 text-indigo-600 font-semibold hover:underline">Xem chi tiết về INFJ...</a>
                        </div>
                    </div>
                </div>

                <!-- AI/Thuật toán Gợi ý Tổng hợp -->
                <div class="bg-gradient-to-br from-blue-50 to-blue-100 p-8 rounded-2xl shadow-xl border-4 border-blue-400">
                    <h3 class="text-3xl font-bold mb-6 flex items-center text-blue-700">
                        <i data-lucide="zap" class="w-7 h-7 mr-3"></i> AI Gợi Ý Ngành Học Tổng Hợp
                    </h3>
                    
                    <p class="text-lg font-medium text-gray-700 mb-4">Kết hợp Holland (IAS) + MBTI (INFJ) + Năng lực (Logic 85):</p>

                    <!-- Ngành Gợi Ý Loại 1 -->
                    <div class="mb-6 p-4 border-l-4 border-green-500 bg-green-50 rounded-lg">
                        <h4 class="text-xl font-bold text-green-700 mb-2 flex items-center"><i data-lucide="check-circle" class="w-5 h-5 mr-2"></i> Ngành Gợi Ý Loại 1 (Phù Hợp Nhất)</h4>
                        <ul class="space-y-1 text-gray-800">
                            <li><span class="font-semibold">Khoa học Dữ liệu & AI:</span> Kết hợp Logic cao + Nghiên cứu (I)</li>
                            <li><span class="font-semibold">Tâm lý học:</span> Phù hợp tuyệt đối với Tính cách INFJ + Yếu tố Xã hội (S)</li>
                        </ul>
                    </div>

                    <!-- Ngành Gợi Ý Loại 2 -->
                    <div class="mb-6 p-4 border-l-4 border-yellow-500 bg-yellow-50 rounded-lg">
                        <h4 class="text-xl font-bold text-yellow-700 mb-2 flex items-center"><i data-lucide="alert-triangle" class="w-5 h-5 mr-2"></i> Ngành Gợi Ý Loại 2 (Nên Cân Nhắc)</h4>
                        <ul class="space-y-1 text-gray-800">
                            <li><span class="font-semibold">Kỹ thuật Phần mềm:</span> Phù hợp Logic, nhưng cần phát triển thêm yếu tố Hiện thực (R)</li>
                            <li><span class="font-semibold">Truyền thông Đa phương tiện:</span> Phù hợp Sáng tạo (A), nhưng cần phát triển yếu tố Lãnh đạo (E)</li>
                        </ul>
                    </div>
                    
                    <button class="btn-primary mt-4 w-full lg:w-auto" onclick="showModal('detail-report-modal')">
                        Xem Báo Cáo Chi Tiết PDF <i data-lucide="file-text" class="inline w-5 h-5 ml-1"></i>
                    </button>
                    <button class="btn-primary mt-4 bg-gray-600 hover:bg-gray-700 w-full lg:w-auto ml-0 lg:ml-4" onclick="showChatbot()">
                        Hỏi Chatbot AI <i data-lucide="message-circle" class="inline w-5 h-5 ml-1"></i>
                    </button>
                </div>

                <!-- Gợi Ý Trường Đại Học Dựa Trên Ngành Đã Chọn -->
                <div class="mt-10 p-8 bg-gray-50 rounded-2xl shadow-inner">
                    <h3 class="text-3xl font-bold mb-6 flex items-center text-gray-800">
                        <i data-lucide="graduation-cap" class="w-7 h-7 mr-3"></i> Gợi Ý Trường Đại Học
                    </h3>
                    <p class="mb-4 text-gray-600">Dựa trên Ngành gợi ý: Khoa học Dữ liệu & Tâm lý học.</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Trường Gợi Ý 1 -->
                        <div class="p-4 bg-white rounded-xl shadow-md hover:shadow-lg transition-shadow border-l-4 border-red-500">
                            <h4 class="text-xl font-semibold mb-1">Đại Học Khoa học Tự nhiên (ĐHQG HCM)</h4>
                            <p class="text-sm text-gray-500 mb-2">Khu vực: TP.HCM | Ngành: Khoa học Dữ liệu</p>
                            <ul class="text-sm space-y-1">
                                <li><span class="font-medium text-red-600">Điểm chuẩn (2024):</span> 27.0 (A00, A01)</li>
                                <li><span class="font-medium">Học phí:</span> ~12 triệu/năm (Đại trà)</li>
                                <li><span class="font-medium">Tỉ lệ việc làm:</span> 95%</li>
                            </ul>
                            <div class="mt-3 flex justify-between items-center">
                                <a href="#" class="text-blue-600 hover:underline text-sm">Xem chi tiết Trường</a>
                                <button class="text-red-500 hover:text-red-700" title="Lưu lại">
                                    <i data-lucide="bookmark" class="w-5 h-5"></i>
                                </button>
                            </div>
                        </div>
                         <!-- Trường Gợi Ý 2 -->
                        <div class="p-4 bg-white rounded-xl shadow-md hover:shadow-lg transition-shadow border-l-4 border-purple-500">
                            <h4 class="text-xl font-semibold mb-1">Trường Đại Học Khoa học Xã hội và Nhân văn (ĐHQG HN)</h4>
                            <p class="text-sm text-gray-500 mb-2">Khu vực: Hà Nội | Ngành: Tâm lý học</p>
                            <ul class="text-sm space-y-1">
                                <li><span class="font-medium text-purple-600">Điểm chuẩn (2024):</span> 26.5 (C00, D01)</li>
                                <li><span class="font-medium">Học phí:</span> ~10 triệu/năm (Đại trà)</li>
                                <li><span class="font-medium">Tỉ lệ việc làm:</span> 90%</li>
                            </ul>
                            <div class="mt-3 flex justify-between items-center">
                                <a href="#" class="text-blue-600 hover:underline text-sm">Xem chi tiết Trường</a>
                                <button class="text-red-500 hover:text-red-700" title="Lưu lại">
                                    <i data-lucide="bookmark" class="w-5 h-5"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                    
                    <button class="btn-primary mt-6 bg-gray-600 hover:bg-gray-700 w-full" onclick="changeView('comparison-tool')">
                        Công Cụ So Sánh Trường <i data-lucide="columns-3" class="inline w-5 h-5 ml-1"></i>
                    </button>
                </div>
                
            </div>
        </section>

        <!-- 5. COMPARISON TOOL VIEW (Mô phỏng) -->
        <section id="comparison-tool-view" class="view">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
                <h2 class="text-4xl font-extrabold text-center mb-8">Công Cụ So Sánh Ngành & Trường Đại Học</h2>

                <div class="bg-white p-8 rounded-2xl shadow-xl">
                    <h3 class="text-3xl font-bold mb-6 text-blue-600 border-b pb-3">So Sánh Trường Đại Học</h3>
                    <p class="text-center text-gray-500 mb-4">Chọn 2 trường để so sánh chi tiết các tiêu chí.</p>
                    
                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tiêu Chí</th>
                                    <th class="px-6 py-3 text-left text-lg font-bold text-blue-700 uppercase tracking-wider">Trường 1 (KHTN)</th>
                                    <th class="px-6 py-3 text-left text-lg font-bold text-indigo-700 uppercase tracking-wider">Trường 2 (KHXHNV)</th>
                                </tr>
                            </thead>
                            <tbody class="bg-white divide-y divide-gray-200">
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Ngành Học Chính</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Khoa học Dữ liệu</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Tâm lý học</td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Khu Vực</td>
                                    <td class="px-6 py-4 whitespace-nowrap">TP. Hồ Chí Minh</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Hà Nội</td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Điểm Chuẩn (2024)</td>
                                    <td class="px-6 py-4 whitespace-nowrap text-red-600 font-bold">27.0</td>
                                    <td class="px-6 py-4 whitespace-nowrap text-red-600 font-bold">26.5</td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Học Phí (Đại trà)</td>
                                    <td class="px-6 py-4 whitespace-nowrap">~12 triệu/năm</td>
                                    <td class="px-6 py-4 whitespace-nowrap">~10 triệu/năm</td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Tỉ lệ Việc Làm</td>
                                    <td class="px-6 py-4 whitespace-nowrap text-green-600 font-medium">95%</td>
                                    <td class="px-6 py-4 whitespace-nowrap text-green-600 font-medium">90%</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- So Sánh Ngành -->
                <div class="bg-white p-8 rounded-2xl shadow-xl mt-10">
                    <h3 class="text-3xl font-bold mb-6 text-indigo-600 border-b pb-3">So Sánh Ngành Nghề</h3>
                    <p class="text-center text-gray-500 mb-4">So sánh 2 ngành: Kỹ thuật Phần mềm và Thiết kế Đồ họa.</p>
                    
                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tiêu Chí</th>
                                    <th class="px-6 py-3 text-left text-lg font-bold text-gray-800 uppercase tracking-wider">Kỹ Thuật Phần Mềm</th>
                                    <th class="px-6 py-3 text-left text-lg font-bold text-gray-800 uppercase tracking-wider">Thiết Kế Đồ Họa</th>
                                </tr>
                            </thead>
                            <tbody class="bg-white divide-y divide-gray-200">
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Mức Độ Phù Hợp (Holland)</td>
                                    <td class="px-6 py-4 whitespace-nowrap"><span class="bg-yellow-100 text-yellow-800 px-3 py-1 rounded-full text-xs font-medium">Trung Bình (R, I)</span></td>
                                    <td class="px-6 py-4 whitespace-nowrap"><span class="bg-green-100 text-green-800 px-3 py-1 rounded-full text-xs font-medium">Cao (A)</span></td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Cơ Hội Nghề Nghiệp</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Rất cao, nhu cầu lớn</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Cao, phụ thuộc vào năng khiếu</td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Mức Lương Trung Bình</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Cao (12-25 triệu/tháng)</td>
                                    <td class="px-6 py-4 whitespace-nowrap">Trung bình - Cao (8-20 triệu/tháng)</td>
                                </tr>
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap font-medium text-gray-900">Tố Chất Cần Có</td>
                                    <td class="px-6 py-4 whitespace-wrap">Tư duy logic, Giải quyết vấn đề</td>
                                    <td class="px-6 py-4 whitespace-wrap">Sáng tạo, Cảm quan màu sắc</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <div class="text-center mt-10">
                    <button class="btn-primary bg-blue-600 hover:bg-blue-700" onclick="changeView('report')">
                        <i data-lucide="eye" class="inline w-5 h-5 mr-1"></i> Trở về Báo Cáo Tổng Hợp
                    </button>
                </div>
            </div>
        </section>

    </main>
    
    <!-- FOOTER -->
    <footer class="bg-gray-800 text-white mt-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
                <!-- Về CareerMatch Pro -->
                <div>
                    <h5 class="font-bold text-lg mb-4 text-blue-400">CareerMatch Pro</h5>
                    <p class="text-sm text-gray-400">Nền tảng tư vấn hướng nghiệp 4.0, giúp học sinh THPT tự tin chọn ngành, chọn trường.</p>
                </div>
                <!-- Dịch vụ -->
                <div>
                    <h5 class="font-bold text-lg mb-4 text-blue-400">Dịch Vụ</h5>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="#" class="hover:text-white transition-colors" onclick="changeView('test-selection')">Làm Bài Test</a></li>
                        <li><a href="#" class="hover:text-white transition-colors" onclick="changeView('report')">Xem Báo Cáo</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">So Sánh Ngành/Trường</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">Chatbot AI</a></li>
                    </ul>
                </div>
                <!-- Liên kết nhanh -->
                <div>
                    <h5 class="font-bold text-lg mb-4 text-blue-400">Liên Kết</h5>
                    <ul class="space-y-2 text-sm text-gray-400">
                        <li><a href="#" class="hover:text-white transition-colors">Thư Viện Kiến Thức</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">FAQs</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">Điều Khoản Sử Dụng</a></li>
                        <li><a href="#" class="hover:text-white transition-colors">Chính Sách Bảo Mật</a></li>
                    </ul>
                </div>
                <!-- Liên hệ & Social -->
                <div>
                    <h5 class="font-bold text-lg mb-4 text-blue-400">Liên Hệ</h5>
                    <p class="text-sm text-gray-400 mb-2">Email: support@careermatchpro.vn</p>
                    <p class="text-sm text-gray-400 mb-4">Hotline: 1900 6868</p>
                    <div class="flex space-x-3">
                        <a href="#" class="text-gray-400 hover:text-blue-500 transition-colors"><i data-lucide="facebook" class="w-6 h-6"></i></a>
                        <a href="#" class="text-gray-400 hover:text-blue-500 transition-colors"><i data-lucide="instagram" class="w-6 h-6"></i></a>
                        <a href="#" class="text-gray-400 hover:text-blue-500 transition-colors"><i data-lucide="linkedin" class="w-6 h-6"></i></a>
                    </div>
                </div>
            </div>
            <div class="mt-8 pt-6 border-t border-gray-700 text-center text-sm text-gray-500">
                &copy; 2025 CareerMatch Pro. All rights reserved.
            </div>
        </div>
    </footer>

</div>

<!-- MODALS (Hidden by default) -->

<!-- Auth Modal (Đăng nhập/Đăng ký) -->
<div id="auth-modal" class="fixed inset-0 z-50 hidden items-center justify-center modal-backdrop">
    <div class="bg-white rounded-2xl shadow-2xl p-8 w-full max-w-md m-4 transform transition-all">
        <div class="flex justify-between items-center mb-6 border-b pb-3">
            <h3 class="text-2xl font-bold text-gray-800">Đăng Nhập / Đăng Ký</h3>
            <button class="text-gray-400 hover:text-gray-600" onclick="closeModal('auth-modal')">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>
        </div>
        
        <button class="w-full flex items-center justify-center space-x-2 bg-red-500 hover:bg-red-600 text-white font-semibold py-3 rounded-xl mb-3 transition-colors">
            <i data-lucide="mail" class="w-5 h-5"></i>
            <span>Tiếp tục với Email</span>
        </button>
        
        <button class="w-full flex items-center justify-center space-x-2 bg-blue-500 hover:bg-blue-600 text-white font-semibold py-3 rounded-xl mb-6 transition-colors">
            <i data-lucide="figma" class="w-5 h-5"></i> <!-- Dùng tạm figma icon làm placeholder cho Google -->
            <span>Tiếp tục với Google</span>
        </button>

        <p class="text-center text-sm text-gray-500">
            Kết quả của bạn sẽ được lưu lại khi đăng ký.
        </p>
    </div>
</div>

<!-- Detailed Report Modal (Mô phỏng) -->
<div id="detail-report-modal" class="fixed inset-0 z-50 hidden items-center justify-center modal-backdrop overflow-y-auto">
    <div class="bg-white rounded-2xl shadow-2xl p-8 w-full max-w-3xl m-4 transform transition-all">
        <div class="flex justify-between items-center mb-6 border-b pb-3">
            <h3 class="text-2xl font-bold text-gray-800">Báo Cáo Phân Tích Chi Tiết (PDF Preview)</h3>
            <button class="text-gray-400 hover:text-gray-600" onclick="closeModal('detail-report-modal')">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>
        </div>
        
        <div class="h-96 border-4 border-dashed border-gray-300 rounded-xl p-4 flex items-center justify-center bg-gray-50 mb-6">
            <p class="text-gray-600 text-center">
                [Mô phỏng nội dung Báo cáo PDF chi tiết]<br>
                Bao gồm: Mã Holland, Nhóm MBTI, Điểm năng lực, Gợi ý Ngành Loại 1 & 2, Giới thiệu cơ hội nghề nghiệp và mức lương trung bình.
            </p>
        </div>

        <button class="btn-primary w-full bg-blue-600 hover:bg-blue-700">
            Tải về Báo Cáo PDF <i data-lucide="download" class="inline w-5 h-5 ml-1"></i>
        </button>
    </div>
</div>

<!-- AI Chatbot Modal (Mô phỏng) -->
<div id="chatbot-modal" class="fixed inset-0 z-50 hidden items-center justify-center modal-backdrop">
    <div class="bg-white rounded-2xl shadow-2xl flex flex-col w-full max-w-xl h-full max-h-[80vh] m-4 transform transition-all">
        <div class="flex justify-between items-center p-5 border-b">
            <h3 class="text-2xl font-bold text-blue-600 flex items-center"><i data-lucide="bot" class="w-6 h-6 mr-2"></i> Chatbot Tư Vấn AI</h3>
            <button class="text-gray-400 hover:text-gray-600" onclick="closeModal('chatbot-modal')">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>
        </div>
        
        <div id="chat-window" class="flex-grow p-4 overflow-y-auto space-y-4 bg-gray-50">
            <!-- Initial Message -->
            <div class="flex justify-start">
                <div class="bg-blue-100 text-blue-800 p-3 rounded-r-xl rounded-tl-xl max-w-xs lg:max-w-md">
                    Chào bạn! Tôi là Career AI. Hãy hỏi tôi bất cứ điều gì về ngành học, trường đại học hoặc hướng nghiệp nhé! Ví dụ: "Em thích Toán + vẽ + lương cao thì nên học gì?"
                </div>
            </div>
        </div>

        <div class="p-4 border-t bg-white">
            <div class="flex space-x-3">
                <input type="text" id="chat-input" placeholder="Gõ câu hỏi của bạn..." class="flex-grow border border-gray-300 p-3 rounded-xl focus:ring-blue-500 focus:border-blue-500">
                <button class="btn-primary flex-shrink-0" onclick="sendChatMessage()">
                    <i data-lucide="send" class="w-5 h-5"></i>
                </button>
            </div>
        </div>
    </div>
</div>


<script>
    // --- GLOBAL STATE AND HELPER FUNCTIONS ---
    let currentView = 'home';

    // Holland Test Data (60 câu hỏi, 10 câu cho mỗi nhóm)
    const HollandQuestions = [
        // R (Realistic) - 10 questions
        { text: "Làm việc với máy móc, công cụ và vật liệu thô.", category: 'R' },
        { text: "Thiết kế và xây dựng các cấu trúc kỹ thuật.", category: 'R' },
        { text: "Sửa chữa đồ điện tử hoặc ô tô.", category: 'R' },
        { text: "Lái xe tải hoặc máy móc hạng nặng.", category: 'R' },
        { text: "Làm đầu bếp hoặc thợ làm bánh chuyên nghiệp.", category: 'R' },
        { text: "Chế tạo đồ gỗ hoặc kim loại.", category: 'R' },
        { text: "Lắp đặt và bảo trì hệ thống dây điện.", category: 'R' },
        { text: "Làm việc ngoài trời (nông nghiệp, lâm nghiệp).", category: 'R' },
        { text: "Làm nghề thợ hàn hoặc thợ sửa ống nước.", category: 'R' },
        { text: "Sử dụng các công cụ đo lường chính xác.", category: 'R' },
        
        // I (Investigative) - 10 questions
        { text: "Nghiên cứu các hiện tượng tự nhiên (vật lý, hóa học, sinh học).", category: 'I' },
        { text: "Thực hiện các thí nghiệm khoa học.", category: 'I' },
        { text: "Phân tích dữ liệu và tìm ra quy luật.", category: 'I' },
        { text: "Nghiên cứu về lịch sử hoặc ngôn ngữ học.", category: 'I' },
        { text: "Thiết kế phần mềm hoặc ứng dụng di động.", category: 'I' },
        { text: "Giải các bài toán logic hoặc mật mã phức tạp.", category: 'I' },
        { text: "Đọc và phân tích các báo cáo khoa học.", category: 'I' },
        { text: "Tìm hiểu cách hoạt động của cơ thể con người.", category: 'I' },
        { text: "Làm việc độc lập để giải quyết một vấn đề học thuật.", category: 'I' },
        { text: "Phát triển lý thuyết mới trong khoa học xã hội.", category: 'I' },
        
        // A (Artistic) - 10 questions
        { text: "Vẽ tranh, điêu khắc hoặc thiết kế thời trang.", category: 'A' },
        { text: "Viết truyện, làm thơ hoặc sáng tác nhạc.", category: 'A' },
        { text: "Biểu diễn trên sân khấu (hát, nhảy, kịch).", category: 'A' },
        { text: "Chụp ảnh nghệ thuật hoặc quay phim.", category: 'A' },
        { text: "Tạo ra các chiến dịch quảng cáo sáng tạo.", category: 'A' },
        { text: "Thiết kế nội thất hoặc cảnh quan.", category: 'A' },
        { text: "Chơi một loại nhạc cụ.", category: 'A' },
        { text: "Làm việc với màu sắc và hình khối.", category: 'A' },
        { text: "Viết kịch bản hoặc chỉnh sửa video.", category: 'A' },
        { text: "Tham gia các lớp học về hội họa, thủ công.", category: 'A' },
        
        // S (Social) - 10 questions
        { text: "Giúp đỡ, tư vấn hoặc chăm sóc người khác.", category: 'S' },
        { text: "Dạy học hoặc huấn luyện người khác.", category: 'S' },
        { text: "Làm việc trong các hoạt động cộng đồng, xã hội.", category: 'S' },
        { text: "Làm tình nguyện viên ở các tổ chức phi lợi nhuận.", category: 'S' },
        { text: "Tổ chức các sự kiện cho bạn bè hoặc cộng đồng.", category: 'S' },
        { text: "Đóng vai trò hòa giải khi có mâu thuẫn.", category: 'S' },
        { text: "Làm việc trong ngành dịch vụ khách hàng.", category: 'S' },
        { text: "Tư vấn tài chính hoặc pháp lý cho người khác.", category: 'S' },
        { text: "Làm việc trong lĩnh vực trị liệu vật lý.", category: 'S' },
        { text: "Làm y tá hoặc nhân viên xã hội.", category: 'S' },

        // E (Enterprising) - 10 questions
        { text: "Quản lý một dự án hoặc một nhóm người.", category: 'E' },
        { text: "Bán hàng hoặc tiếp thị sản phẩm.", category: 'E' },
        { text: "Khởi nghiệp kinh doanh riêng.", category: 'E' },
        { text: "Tham gia tranh luận, đàm phán hợp đồng.", category: 'E' },
        { text: "Thuyết phục người khác đồng ý với ý kiến của mình.", category: 'E' },
        { text: "Đứng lên phát biểu trước đám đông.", category: 'E' },
        { text: "Đặt mục tiêu lớn và cố gắng đạt được chúng.", category: 'E' },
        { text: "Phân tích thị trường và tìm kiếm cơ hội đầu tư.", category: 'E' },
        { text: "Tổ chức và điều hành một cuộc họp.", category: 'E' },
        { text: "Làm công việc có tính cạnh tranh cao.", category: 'E' },

        // C (Conventional) - 10 questions
        { text: "Lập bảng tính, sắp xếp hồ sơ, nhập dữ liệu.", category: 'C' },
        { text: "Theo dõi ngân sách, kế toán.", category: 'C' },
        { text: "Thực hiện các công việc văn phòng có tổ chức.", category: 'C' },
        { text: "Kiểm tra chất lượng và độ chính xác của tài liệu.", category: 'C' },
        { text: "Sử dụng phần mềm chuyên dụng để quản lý thông tin.", category: 'C' },
        { text: "Tuân thủ nghiêm ngặt các quy tắc và thủ tục.", category: 'C' },
        { text: "Lưu trữ và phục hồi hồ sơ một cách có hệ thống.", category: 'C' },
        { text: "Xử lý các giao dịch tài chính (ngân hàng, thanh toán).", category: 'C' },
        { text: "Sắp xếp lịch trình và quản lý thời gian hiệu quả.", category: 'C' },
        { text: "Viết báo cáo hoặc thư từ chính thức.", category: 'C' }
    ];
    
    let hollandAnswers = new Array(HollandQuestions.length).fill(null);
    let currentQuestionIndex = 0;
    const TOTAL_QUESTIONS = HollandQuestions.length;

    // --- VIEW MANAGEMENT ---

    function changeView(viewId) {
        document.querySelectorAll('.view').forEach(view => {
            view.classList.remove('active');
        });
        const nextView = document.getElementById(viewId + '-view');
        if (nextView) {
            nextView.classList.add('active');
            currentView = viewId;
            window.scrollTo({ top: 0, behavior: 'smooth' });
            // Sau khi chuyển view, render lại Lucide Icons
            if (window.createLucideIcons) {
                window.createLucideIcons();
            }
        }
        
        // Logic khởi tạo đặc biệt cho các view
        if (viewId === 'holland-test') {
            currentQuestionIndex = 0;
            hollandAnswers.fill(null);
            renderHollandQuestion();
        } else if (viewId === 'report') {
            // Kiểm tra và hiển thị kết quả Holland (mô phỏng)
            if (hollandAnswers.some(a => a !== null)) {
                // Giả sử có kết quả đã được tính trước đó
                displayHollandResult({
                    R: 20, I: 45, A: 60, S: 50, E: 30, C: 25 
                });
            } else {
                // Load kết quả mặc định hoặc từ data
                displayHollandResult({
                    R: 35, I: 55, A: 65, S: 40, E: 50, C: 30 
                });
            }
        }
    }

    // --- MODAL MANAGEMENT ---

    function showModal(modalId) {
        document.getElementById(modalId).classList.remove('hidden');
        document.getElementById(modalId).classList.add('flex');
        if (window.createLucideIcons) {
            window.createLucideIcons();
        }
    }

    function closeModal(modalId) {
        document.getElementById(modalId).classList.add('hidden');
        document.getElementById(modalId).classList.remove('flex');
    }
    
    function showChatbot() {
        showModal('chatbot-modal');
    }

    // --- UI/UX HELPER ---

    function toggleMobileMenu() {
        const menu = document.getElementById('mobile-menu');
        if (menu.classList.contains('-translate-y-full')) {
            menu.classList.remove('-translate-y-full', 'opacity-0');
            menu.classList.add('translate-y-0', 'opacity-100');
        } else {
            menu.classList.remove('translate-y-0', 'opacity-100');
            menu.classList.add('-translate-y-full', 'opacity-0');
        }
    }
    
    function displayMessage(message, type = 'info') {
        const box = document.getElementById('message-box');
        const colors = {
            success: 'bg-green-500',
            warning: 'bg-yellow-500',
            error: 'bg-red-500',
            info: 'bg-blue-500'
        };
        const icons = {
            success: 'check-circle',
            warning: 'alert-triangle',
            error: 'x-circle',
            info: 'info'
        };
        
        const messageHtml = `
            <div class="${colors[type]} text-white p-4 rounded-xl shadow-lg flex items-center space-x-3">
                <i data-lucide="${icons[type]}" class="w-6 h-6"></i>
                <p class="font-medium">${message}</p>
            </div>
        `;

        const tempDiv = document.createElement('div');
        tempDiv.innerHTML = messageHtml;
        box.appendChild(tempDiv.firstChild);

        if (window.createLucideIcons) {
            window.createLucideIcons();
        }

        // Hiện thông báo
        box.classList.remove('translate-x-full');
        box.classList.add('translate-x-0');

        // Tự động ẩn sau 4 giây
        setTimeout(() => {
            box.classList.remove('translate-x-0');
            box.classList.add('translate-x-full');
            // Xóa phần tử sau khi ẩn
            setTimeout(() => {
                box.innerHTML = '';
            }, 500); 
        }, 4000);
    }
    
    // --- HOLLAND TEST LOGIC ---

    function renderHollandQuestion() {
        const container = document.getElementById('holland-questions');
        const progress = document.getElementById('holland-progress');
        const prevBtn = document.getElementById('holland-prev-btn');
        const nextBtn = document.getElementById('holland-next-btn');
        const submitBtn = document.getElementById('holland-submit-btn');

        if (currentQuestionIndex >= TOTAL_QUESTIONS) {
            // Should not happen if logic is correct
            return;
        }

        const q = HollandQuestions[currentQuestionIndex];
        const currentAnswer = hollandAnswers[currentQuestionIndex];

        container.innerHTML = `
            <div class="mb-6">
                <p class="text-xl font-semibold mb-4 text-gray-800">
                    Câu ${currentQuestionIndex + 1}: ${q.text}
                </p>
                <div class="flex flex-col sm:flex-row justify-between space-y-3 sm:space-y-0 sm:space-x-4">
                    ${['Rất Không Thích', 'Không Thích', 'Bình Thường', 'Thích', 'Rất Thích'].map((label, value) => `
                        <label class="flex-1 text-center cursor-pointer p-3 border-2 rounded-xl transition-all ${currentAnswer === (value + 1) ? 'bg-blue-500 border-blue-600 text-white shadow-lg' : 'bg-gray-50 border-gray-200 text-gray-700 hover:bg-blue-100 hover:border-blue-400'}">
                            <input type="radio" name="holland-q${currentQuestionIndex}" value="${value + 1}" class="hidden" 
                                onchange="recordHollandAnswer(${currentQuestionIndex}, ${value + 1})" 
                                ${currentAnswer === (value + 1) ? 'checked' : ''}>
                            ${label}
                        </label>
                    `).join('')}
                </div>
            </div>
        `;
        
        progress.textContent = `Câu ${currentQuestionIndex + 1}/${TOTAL_QUESTIONS}`;

        // Cập nhật nút điều hướng
        prevBtn.disabled = currentQuestionIndex === 0;
        
        if (currentQuestionIndex === TOTAL_QUESTIONS - 1) {
            nextBtn.classList.add('hidden');
            submitBtn.classList.remove('hidden');
            submitBtn.disabled = currentAnswer === null;
        } else {
            nextBtn.classList.remove('hidden');
            submitBtn.classList.add('hidden');
            nextBtn.disabled = currentAnswer === null;
        }
        
        if (window.createLucideIcons) {
            window.createLucideIcons();
        }
    }

    function recordHollandAnswer(index, value) {
        hollandAnswers[index] = value;
        
        const nextBtn = document.getElementById('holland-next-btn');
        const submitBtn = document.getElementById('holland-submit-btn');

        if (index < TOTAL_QUESTIONS - 1) {
            nextBtn.disabled = false;
        } else if (index === TOTAL_QUESTIONS - 1) {
            submitBtn.disabled = false;
        }
        
        // Cập nhật giao diện câu trả lời ngay lập tức
        renderHollandQuestion();
    }
    
    function nextHollandQuestion() {
        if (currentQuestionIndex < TOTAL_QUESTIONS - 1) {
            currentQuestionIndex++;
            renderHollandQuestion();
        }
    }
    
    function prevHollandQuestion() {
        if (currentQuestionIndex > 0) {
            currentQuestionIndex--;
            renderHollandQuestion();
        }
    }

    function calculateHollandResult() {
        // Kiểm tra xem đã trả lời hết chưa
        if (hollandAnswers.some(a => a === null)) {
            displayMessage("Vui lòng hoàn thành tất cả các câu hỏi trước khi xem kết quả.", "error");
            return;
        }

        const scores = { R: 0, I: 0, A: 0, S: 0, E: 0, C: 0 };

        HollandQuestions.forEach((q, index) => {
            if (hollandAnswers[index] !== null) {
                // Điểm từ 1 (Rất Không Thích) đến 5 (Rất Thích)
                scores[q.category] += hollandAnswers[index];
            }
        });

        // Tìm mã Holland 3 chữ cái (ví dụ: AES)
        const sortedCategories = Object.keys(scores).sort((a, b) => scores[b] - scores[a]);
        const hollandCode = sortedCategories.slice(0, 3).join('');
        
        // Lưu kết quả vào Firebase (chức năng mô phỏng)
        window.saveTestResult('Holland-RIASEC', {
            scores: scores,
            code: hollandCode
        });

        // Hiển thị kết quả và chuyển sang trang báo cáo
        displayHollandResult(scores, hollandCode);
        changeView('report');
    }
    
    let hollandRadarChart;
    
    function displayHollandResult(scores, code) {
        const ctx = document.getElementById('holland-chart').getContext('2d');
        const categories = Object.keys(scores);
        const dataValues = Object.values(scores);
        const maxScore = Math.max(...dataValues, 10); 

        // Hủy biểu đồ cũ nếu có
        if (hollandRadarChart) {
            hollandRadarChart.destroy();
        }

        hollandRadarChart = new Chart(ctx, {
            type: 'radar',
            data: {
                labels: ['Hiện thực (R)', 'Nghiên cứu (I)', 'Nghệ thuật (A)', 'Xã hội (S)', 'Quản lý (E)', 'Nghiệp vụ (C)'],
                datasets: [{
                    label: 'Mức độ Sở thích',
                    data: dataValues,
                    backgroundColor: 'rgba(46, 125, 255, 0.2)',
                    borderColor: 'var(--color-primary)',
                    pointBackgroundColor: 'var(--color-primary)',
                    pointBorderColor: '#fff',
                    pointHoverBackgroundColor: '#fff',
                    pointHoverBorderColor: 'var(--color-primary)'
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: true,
                scales: {
                    r: {
                        angleLines: { display: true },
                        grid: { color: 'rgba(0, 0, 0, 0.1)' },
                        suggestedMin: 0,
                        suggestedMax: maxScore,
                        pointLabels: { font: { size: 14, weight: 'bold' } },
                        ticks: { display: false }
                    }
                },
                plugins: {
                    legend: { display: false },
                    tooltip: {
                        callbacks: {
                            label: (context) => `${context.label}: ${context.parsed.r}`
                        }
                    }
                }
            }
        });
        
        const sortedCategories = Object.keys(scores).sort((a, b) => scores[b] - scores[a]);
        const finalCode = code || sortedCategories.slice(0, 3).join('');

        // Cập nhật UI kết quả
        document.getElementById('holland-code').textContent = finalCode;
        document.getElementById('holland-summary').textContent = generateHollandSummary(finalCode);
        document.getElementById('holland-career-suggestions').innerHTML = generateCareerSuggestions(finalCode);
        
        // Chạy lại Lucide Icons sau khi nội dung thay đổi
        if (window.createLucideIcons) {
            window.createLucideIcons();
        }
    }
    
    function generateHollandSummary(code) {
        const descriptions = {
            R: 'Hiện thực (Thực tế, kỹ thuật, làm việc ngoài trời).',
            I: 'Nghiên cứu (Phân tích, điều tra, khoa học).',
            A: 'Nghệ thuật (Sáng tạo, biểu cảm, không có cấu trúc rõ ràng).',
            S: 'Xã hội (Giúp đỡ, giáo dục, làm việc với con người).',
            E: 'Quản lý (Thuyết phục, lãnh đạo, kinh doanh).',
            C: 'Nghiệp vụ (Tổ chức, dữ liệu, làm việc chi tiết, văn phòng).'
        };
        
        const summary = `Dựa trên kết quả, nhóm sở thích nổi trội của bạn là **${code}**. Điều này cho thấy bạn có xu hướng kết hợp: 
            <span class="font-bold text-blue-600">${descriptions[code[0]]}</span>, 
            <span class="font-bold text-blue-600">${descriptions[code[1]]}</span> và 
            <span class="font-bold text-blue-600">${descriptions[code[2]]}</span>.
            `;
        return summary;
    }
    
    function generateCareerSuggestions(code) {
        let suggestions = [];

        if (code.includes('R')) suggestions.push('Kỹ thuật Cơ khí, Kỹ thuật Điện, Xây dựng');
        if (code.includes('I')) suggestions.push('Khoa học Máy tính, Phân tích Dữ liệu, Công nghệ Sinh học');
        if (code.includes('A')) suggestions.push('Thiết kế Đồ họa/Nội thất, Kiến trúc, Truyền thông');
        if (code.includes('S')) suggestions.push('Tâm lý học, Sư phạm, Quan hệ Công chúng');
        if (code.includes('E')) suggestions.push('Quản trị Kinh doanh, Marketing, Luật');
        if (code.includes('C')) suggestions.push('Kế toán, Kiểm toán, Quản lý Hành chính');
        
        if (suggestions.length < 3) suggestions = ['Công nghệ Thông tin', 'Kinh tế', 'Truyền thông Đa phương tiện']; // Fallback

        return suggestions.map(s => `<li>${s}</li>`).join('');
    }

    // --- CHATBOT LOGIC (Mô phỏng API Call) ---
    
    const CHATBOT_API_URL = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent";
    const CHATBOT_API_KEY = ""; // Sẽ được tự động cung cấp trong môi trường Canvas
    
    async function fetchGeminiResponse(prompt) {
        const systemPrompt = "Bạn là Career AI, một chuyên gia tư vấn hướng nghiệp thân thiện, nhiệt tình. Bạn luôn phân tích câu hỏi dựa trên sở thích, năng lực và xu hướng thị trường Việt Nam. Trả lời bằng tiếng Việt.";
        const userQuery = prompt;
        
        const payload = {
            contents: [{ parts: [{ text: userQuery }] }],
            tools: [{ "google_search": {} }], // Bật Google Search để lấy thông tin mới
            systemInstruction: {
                parts: [{ text: systemPrompt }]
            },
        };

        let response = null;
        let retries = 0;
        const maxRetries = 3;

        while (retries < maxRetries) {
            try {
                const fetchResponse = await fetch(`${CHATBOT_API_URL}?key=${CHATBOT_API_KEY}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                
                if (fetchResponse.ok) {
                    response = await fetchResponse.json();
                    break; // Thành công, thoát vòng lặp
                } else {
                    // Xử lý lỗi HTTP khác (ví dụ 429 - Rate limit)
                    throw new Error(`HTTP error! status: ${fetchResponse.status}`);
                }
            } catch (error) {
                retries++;
                const delay = Math.pow(2, retries) * 1000; // Exponential backoff (1s, 2s, 4s)
                if (retries < maxRetries) {
                    await new Promise(resolve => setTimeout(resolve, delay));
                } else {
                    console.error("Gemini API call failed after multiple retries:", error);
                    return "Xin lỗi, tôi đang gặp vấn đề kết nối. Vui lòng thử lại sau.";
                }
            }
        }

        const candidate = response?.candidates?.[0];
        if (candidate && candidate.content?.parts?.[0]?.text) {
            return candidate.content.parts[0].text;
        } else {
            return "Xin lỗi, tôi không thể tạo ra câu trả lời vào lúc này. Vui lòng thử lại với câu hỏi khác.";
        }
    }
    
    async function sendChatMessage() {
        const input = document.getElementById('chat-input');
        const chatWindow = document.getElementById('chat-window');
        const userMessage = input.value.trim();

        if (!userMessage) return;

        // 1. Hiển thị tin nhắn người dùng
        appendMessage(userMessage, 'user');
        input.value = '';

        // 2. Hiển thị loading
        const loadingId = appendMessage('...', 'ai', true);
        
        // 3. Gọi API Gemini
        const aiResponseText = await fetchGeminiResponse(userMessage);

        // 4. Cập nhật tin nhắn AI
        updateMessage(loadingId, aiResponseText);
        
        // 5. Scroll xuống cuối
        chatWindow.scrollTop = chatWindow.scrollHeight;
    }

    function appendMessage(text, sender, isLoading = false) {
        const chatWindow = document.getElementById('chat-window');
        const messageDiv = document.createElement('div');
        const messageId = `msg-${Date.now()}`;
        
        if (sender === 'user') {
            messageDiv.className = 'flex justify-end';
            messageDiv.innerHTML = `
                <div class="bg-blue-500 text-white p-3 rounded-l-xl rounded-tr-xl max-w-xs lg:max-w-md shadow-md">
                    ${text}
                </div>
            `;
        } else { // sender === 'ai'
            messageDiv.className = 'flex justify-start';
            messageDiv.id = messageId;
            messageDiv.innerHTML = `
                <div class="bg-gray-200 text-gray-800 p-3 rounded-r-xl rounded-tl-xl max-w-xs lg:max-w-md shadow-md">
                    ${isLoading ? `<i data-lucide="loader-circle" class="w-5 h-5 animate-spin"></i> Đang phân tích...` : text.replace(/\n/g, '<br>')}
                </div>
            `;
        }

        chatWindow.appendChild(messageDiv);
        chatWindow.scrollTop = chatWindow.scrollHeight;
        
        if (window.createLucideIcons) {
            window.createLucideIcons();
        }
        
        return messageId;
    }

    function updateMessage(id, newText) {
        const messageDiv = document.getElementById(id);
        if (messageDiv) {
            messageDiv.querySelector('div').innerHTML = newText.replace(/\n/g, '<br>');
            messageDiv.querySelector('div').classList.replace('bg-gray-200', 'bg-white');
            messageDiv.querySelector('div').classList.add('border', 'border-gray-200');
        }
    }


    // --- INITIALIZATION ---

    document.addEventListener('DOMContentLoaded', () => {
        // Khởi tạo view
        changeView('home'); 
        
        // Khởi tạo Holland Test (chỉ tạo cấu trúc, chưa render câu hỏi)
        if (TOTAL_QUESTIONS > 0) {
            renderHollandQuestion();
        } else {
            console.error("Holland questions data is empty.");
        }
    });

    // Cần chạy lại Lucide Icons sau khi DOM tải xong
    window.onload = function() {
        if (window.createLucideIcons) {
            window.createLucideIcons();
        }
    };

</script>

</body>
</html>