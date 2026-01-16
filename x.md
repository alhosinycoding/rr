<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أكاديمية الشهد التعليمية</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <style>
        body { font-family: 'Cairo', sans-serif; background: #0f172a; color: #f1f5f9; scroll-behavior: smooth; }
        .glass { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.05); }
        .sidebar { transition: transform 0.3s ease; z-index: 1000; }
        .tab-content { display: none; animation: fadeIn 0.4s ease-out; }
        .tab-content.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .loader { width: 40px; height: 40px; border: 4px solid #f97316; border-bottom-color: transparent; border-radius: 50%; display: inline-block; animation: rotation 1s linear infinite; }
        @keyframes rotation { 0% { transform: rotate(0deg) } 100% { transform: rotate(360deg) } }
    </style>
</head>
<body class="flex min-h-screen">

    <div id="loaderOverlay" class="fixed inset-0 bg-slate-900/90 z-[9999] hidden flex flex-col items-center justify-center">
        <span class="loader"></span>
        <p class="mt-4 text-orange-500 font-bold">جاري الاتصال بالسحابة...</p>
    </div>

    <aside id="sidebar" class="sidebar fixed inset-y-0 right-0 w-64 glass border-l border-white/5 p-6 flex flex-col -translate-x-full md:translate-x-0 transition-transform">
        <div class="flex items-center gap-3 mb-10 px-2">
            <div class="w-10 h-10 bg-orange-500 rounded-xl flex items-center justify-center shadow-lg shadow-orange-500/20">
                <i class="fa-solid fa-graduation-cap text-white text-xl"></i>
            </div>
            <h1 class="text-xl font-black text-orange-500 italic">الشهد</h1>
        </div>

        <nav id="navLinks" class="flex-1 space-y-2">
            </nav>

        <div class="pt-6 border-t border-white/10">
            <button onclick="logout()" class="flex items-center gap-3 w-full p-4 rounded-2xl text-red-400 hover:bg-red-500/10 transition">
                <i class="fa-solid fa-power-off"></i> تسجيل الخروج
            </button>
        </div>
    </aside>

    <main class="flex-1 md:mr-64 flex flex-col min-w-0">
        <header id="topBar" class="h-20 glass border-b border-white/5 px-8 flex items-center justify-between sticky top-0 z-50 hidden">
            <button onclick="toggleSidebar()" class="md:hidden text-2xl text-orange-500"><i class="fa-solid fa-bars"></i></button>
            <div class="flex items-center gap-4">
                <div class="text-left">
                    <p id="userNameDisplay" class="font-bold text-sm text-orange-500"></p>
                    <p id="userRankDisplay" class="text-[10px] text-slate-400 text-left"></p>
                </div>
                <div class="w-10 h-10 rounded-full bg-slate-800 border border-orange-500/30 flex items-center justify-center font-bold text-orange-500" id="avatarCircle"></div>
            </div>
        </header>

        <div class="p-6 md:p-10">
            <section id="loginPage" class="max-w-md mx-auto py-20 active tab-content">
                <div class="glass p-10 rounded-[3rem] shadow-2xl">
                    <h2 class="text-3xl font-black mb-2 text-center text-orange-500">مرحباً بك</h2>
                    <p class="text-center text-slate-400 text-sm mb-10">سجل دخولك للوصول إلى محتواك التعليمي</p>
                    <div class="space-y-4">
                        <input type="text" id="loginUser" placeholder="اسم المستخدم" class="w-full bg-slate-800/50 p-4 rounded-2xl outline-none border border-white/5 focus:border-orange-500 transition">
                        <input type="password" id="loginPass" placeholder="كلمة المرور" class="w-full bg-slate-800/50 p-4 rounded-2xl outline-none border border-white/5 focus:border-orange-500 transition">
                        <button onclick="handleLogin()" class="w-full bg-orange-600 hover:bg-orange-500 py-4 rounded-2xl font-black text-lg transition transform active:scale-95 shadow-lg shadow-orange-600/20">دخول</button>
                    </div>
                </div>
            </section>

            <section id="lessonsPage" class="tab-content">
                <div class="flex items-center justify-between mb-8">
                    <h2 class="text-2xl font-black border-r-4 border-orange-500 pr-4">حصص الأكاديمية</h2>
                </div>
                <div id="videoContainer" class="hidden mb-10 glass p-4 rounded-[2.5rem]">
                    <div class="flex justify-between items-center mb-4 px-2">
                        <h3 id="currentVideoTitle" class="font-bold text-orange-500 italic"></h3>
                        <button onclick="closeVideo()" class="bg-red-500/10 text-red-500 px-4 py-2 rounded-xl text-sm font-bold">إغلاق المشغل</button>
                    </div>
                    <div class="aspect-video w-full" id="playerWrapper"></div>
                </div>
                <div id="lessonsGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
            </section>

            <section id="examsPage" class="tab-content">
                <h2 class="text-2xl font-black border-r-4 border-purple-500 pr-4 mb-8">الاختبارات الدورية</h2>
                <div id="examsGrid" class="grid grid-cols-1 md:grid-cols-2 gap-6"></div>
            </section>

            <section id="adminPage" class="tab-content">
                <h2 class="text-2xl font-black border-r-4 border-blue-500 pr-4 mb-8">إدارة المنصة</h2>
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <div class="glass p-8 rounded-3xl">
                        <h3 class="font-bold mb-6 flex items-center gap-2"><i class="fa-solid fa-user-plus text-orange-500"></i> إضافة طالب جديد</h3>
                        <div class="space-y-3">
                            <input type="text" id="addStdName" placeholder="الاسم بالكامل" class="w-full bg-slate-800 p-3 rounded-xl outline-none">
                            <input type="text" id="addStdUser" placeholder="اسم المستخدم" class="w-full bg-slate-800 p-3 rounded-xl outline-none">
                            <input type="text" id="addStdPass" placeholder="كلمة المرور" class="w-full bg-slate-800 p-3 rounded-xl outline-none">
                            <input type="text" id="addStdGroup" placeholder="المجموعة (مثلاً: ثانية ثانوي)" class="w-full bg-slate-800 p-3 rounded-xl outline-none">
                            <button onclick="apiAction('addStudent')" class="w-full bg-orange-600 p-3 rounded-xl font-bold">إضافة الطالب</button>
                        </div>
                    </div>
                    <div class="glass p-8 rounded-3xl">
                        <h3 class="font-bold mb-6 flex items-center gap-2"><i class="fa-solid fa-film text-blue-500"></i> إضافة حصة جديدة</h3>
                        <div class="space-y-3">
                            <input type="text" id="addLesTitle" placeholder="عنوان الحصة" class="w-full bg-slate-800 p-3 rounded-xl outline-none">
                            <input type="text" id="addLesUrl" placeholder="رابط يوتيوب" class="w-full bg-slate-800 p-3 rounded-xl outline-none">
                            <button onclick="apiAction('addLesson')" class="w-full bg-blue-600 p-3 rounded-xl font-bold">نشر الحصة</button>
                        </div>
                    </div>
                </div>
            </section>
        </div>
    </main>

    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbxwguM2z9Vwwk7rzC3TCeAlV061eiHyuNwMvOF7nNbXqOiYrbVT62flrubhmr81AoEk/exec";
        let currentUser = JSON.parse(localStorage.getItem('shahd_user')) || null;

        // عند تشغيل الصفحة
        window.onload = () => {
            if (currentUser) {
                initApp();
            }
        };

        // دالة تسجيل الدخول
        async function handleLogin() {
            const u = document.getElementById('loginUser').value.trim();
            const p = document.getElementById('loginPass').value.trim();
            if (!u || !p) return alert("يرجى إدخال البيانات");

            showLoader(true);
            try {
                const response = await fetch(SCRIPT_URL, {
                    method: 'POST',
                    body: JSON.stringify({ action: 'login', u, p })
                });
                const data = await response.json();
                
                if (data.success) {
                    currentUser = data;
                    localStorage.setItem('shahd_user', JSON.stringify(data));
                    initApp();
                } else {
                    if (data.message === "blocked") alert("حسابك موقوف، تواصل مع الإدارة");
                    else alert("بيانات الدخول غير صحيحة");
                }
            } catch (err) { alert("فشل الاتصال بالسيرفر"); }
            showLoader(false);
        }

        // إعداد الواجهة بعد الدخول
        function initApp() {
            document.getElementById('loginPage').classList.remove('active');
            document.getElementById('topBar').classList.remove('hidden');
            document.getElementById('userNameDisplay').innerText = currentUser.name;
            document.getElementById('userRankDisplay').innerText = `المجموعة: ${currentUser.group} | الترتيب: ${currentUser.rank}`;
            document.getElementById('avatarCircle').innerText = currentUser.name[0];

            let navHtml = `
                <button onclick="switchTab('lessonsPage')" class="nav-btn w-full flex items-center gap-3 p-4 rounded-2xl hover:bg-orange-500/10 transition active-nav">
                    <i class="fa-solid fa-play"></i> الحصص التعليمية
                </button>
                <button onclick="switchTab('examsPage')" class="nav-btn w-full flex items-center gap-3 p-4 rounded-2xl hover:bg-purple-500/10 transition">
                    <i class="fa-solid fa-file-signature"></i> الاختبارات
                </button>
            `;

            if (currentUser.role === 'admin') {
                navHtml += `
                <button onclick="switchTab('adminPage')" class="nav-btn w-full flex items-center gap-3 p-4 rounded-2xl hover:bg-blue-500/10 transition text-blue-400">
                    <i class="fa-solid fa-user-shield"></i> لوحة التحكم
                </button>`;
            }
            document.getElementById('navLinks').innerHTML = navHtml;
            switchTab('lessonsPage');
            refreshData();
        }

        // جلب البيانات وتحديث الجريد
        async function refreshData() {
            try {
                // جلب الحصص
                const resLes = await fetch(`${SCRIPT_URL}?action=getData&type=LESSON`); // التعديل: getData الآن تجلب الكل حسب هيكلة السكربت
                const data = await (await fetch(`${SCRIPT_URL}?action=getData`)).json();
                
                // رندر الحصص
                const lessonsGrid = document.getElementById('lessonsGrid');
                lessonsGrid.innerHTML = data.filter(r => r.name && r.val1 && !r.val2.includes(':')).map(l => `
                    <div class="glass p-5 rounded-[2.5rem] group cursor-pointer hover:border-orange-500/50 transition" onclick="watchVideo('${l.val1}', '${l.name}')">
                        <div class="relative rounded-3xl overflow-hidden mb-4 aspect-video bg-slate-800 flex items-center justify-center">
                            <i class="fa-solid fa-play text-4xl text-orange-500/20 group-hover:scale-125 transition"></i>
                        </div>
                        <h3 class="font-bold text-lg px-2">${l.name}</h3>
                        <div class="flex items-center gap-2 mt-2 px-2 text-xs text-slate-500">
                            <i class="fa-solid fa-eye"></i> <span>شاهدها الآن</span>
                        </div>
                    </div>
                `).join('');

                // رندر الاختبارات بنفس الطريقة... (يتم تصفية النوع EXAM من الداتا)
            } catch (err) { console.error("Error loading data"); }
        }

        function watchVideo(url, title) {
            const id = url.split('v=')[1] || url.split('/').pop();
            document.getElementById('videoContainer').classList.remove('hidden');
            document.getElementById('currentVideoTitle').innerText = title;
            document.getElementById('playerWrapper').innerHTML = `<iframe class="w-full h-full rounded-3xl shadow-2xl" src="https://www.youtube.com/embed/${id}?autoplay=1" frameborder="0" allowfullscreen></iframe>`;
            window.scrollTo({ top: 0, behavior: 'smooth' });
            
            // تسجيل المشاهدة في الشيت
            fetch(SCRIPT_URL, { method: 'POST', body: JSON.stringify({ action: 'markWatched', title: title, user: currentUser.name }) });
        }

        // أدوات الإدارة
        async function apiAction(type) {
            let payload = { action: type, data: {} };
            if (type === 'addStudent') {
                payload.data = { name: document.getElementById('addStdName').value, user: document.getElementById('addStdUser').value, pass: document.getElementById('addStdPass').value, group: document.getElementById('addStdGroup').value };
            } else if (type === 'addLesson') {
                payload.data = { title: document.getElementById('addLesTitle').value, url: document.getElementById('addLesUrl').value };
            }

            showLoader(true);
            const res = await fetch(SCRIPT_URL, { method: 'POST', body: JSON.stringify(payload) });
            const result = await res.json();
            if (result.success) {
                alert("تمت العملية بنجاح");
                refreshData();
            }
            showLoader(false);
        }

        function switchTab(id) {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            if (window.innerWidth < 768) toggleSidebar();
        }

        function toggleSidebar() { document.getElementById('sidebar').classList.toggle('-translate-x-full'); }
        function showLoader(v) { document.getElementById('loaderOverlay').classList.toggle('hidden', !v); }
        function closeVideo() { document.getElementById('videoContainer').classList.add('hidden'); document.getElementById('playerWrapper').innerHTML = ""; }
        function logout() { localStorage.clear(); location.reload(); }
    </script>
</body>
</html>
