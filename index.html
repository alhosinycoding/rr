<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أكاديمية الشهد</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { font-family: 'Cairo', sans-serif; background-color: #0f172a; color: white; }
        .glass { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(10px); border: 1px solid rgba(255,255,255,0.1); }
        .btn-orange { @apply bg-orange-600 hover:bg-orange-500 transition-all duration-300 rounded-xl font-bold; }
    </style>
</head>
<body class="flex h-screen overflow-hidden">

    <div id="loader" class="fixed inset-0 bg-slate-900 z-[9999] hidden flex flex-col items-center justify-center">
        <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-orange-500"></div>
        <p class="mt-4 text-orange-500 font-bold">جاري معالجة البيانات...</p>
    </div>

    <aside id="sidebar" class="w-64 glass hidden md:flex flex-col p-6 shadow-2xl">
        <div class="mb-10 text-center">
            <h1 class="text-2xl font-black text-orange-500 tracking-tighter">أكاديمية الشهد</h1>
        </div>
        <nav id="navMenu" class="space-y-2 flex-1"></nav>
        <button onclick="logout()" class="p-3 text-red-400 hover:bg-red-500/10 rounded-xl flex items-center gap-2">
            <i class="fa-solid fa-power-off"></i> خروج
        </button>
    </aside>

    <main class="flex-1 overflow-y-auto p-6 md:p-10">
        
        <section id="loginPage" class="max-w-md mx-auto mt-20 p-10 glass rounded-[2rem] shadow-2xl">
            <h2 class="text-center text-3xl font-black mb-8">تسجيل الدخول</h2>
            <div class="space-y-5">
                <input type="text" id="username" placeholder="اسم المستخدم" class="w-full p-4 rounded-xl bg-slate-800 border border-slate-700 outline-none focus:border-orange-500">
                <input type="password" id="password" placeholder="كلمة المرور" class="w-full p-4 rounded-xl bg-slate-800 border border-slate-700 outline-none focus:border-orange-500">
                <button onclick="handleLogin()" class="w-full py-4 btn-orange text-white">دخول للمنصة</button>
            </div>
        </section>

        <section id="mainApp" class="hidden">
            <header class="flex justify-between items-center mb-10 glass p-6 rounded-3xl">
                <div>
                    <h2 id="welcomeMsg" class="text-2xl font-black"></h2>
                    <p id="userRank" class="text-orange-400 text-sm"></p>
                </div>
                <div class="h-14 w-14 rounded-2xl bg-orange-600 flex items-center justify-center font-black text-2xl shadow-lg" id="avatar"></div>
            </header>

            <div id="pageContent" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
        </section>
    </main>

    <script>
        const API_URL = "https://script.google.com/macros/s/AKfycbyT-rR0quGU099MonvAU14p8duwz5GkTfePZj828ubXpgptziJzfMfGebUn8r9stjyF/exec";
        let currentUser = JSON.parse(localStorage.getItem('user')) || null;
        let globalData = {};

        window.onload = () => { if(currentUser) showApp(); };

        async function handleLogin() {
            const u = document.querySelector('#username').value;
            const p = document.querySelector('#password').value;
            if(!u || !p) return alert("أدخل بياناتك");

            toggleLoader(true);
            try {
                const res = await fetch(API_URL, {
                    method: 'POST',
                    body: JSON.stringify({ action: 'login', u, p })
                });
                const data = await res.json();
                if(data.status === 'success') {
                    currentUser = data.user;
                    localStorage.setItem('user', JSON.stringify(currentUser));
                    showApp();
                } else alert(data.msg);
            } catch(e) { alert("خطأ في الاتصال بالسيرفر"); }
            toggleLoader(false);
        }

        async function showApp() {
            document.querySelector('#loginPage').classList.add('hidden');
            document.querySelector('#mainApp').classList.remove('hidden');
            document.querySelector('#sidebar').classList.replace('hidden', 'flex');
            document.querySelector('#welcomeMsg').innerText = `أهلاً، ${currentUser.name}`;
            document.querySelector('#userRank').innerText = `${currentUser.group} | رتبة: ${currentUser.role === 'admin' ? 'مدير' : 'طالب'}`;
            document.querySelector('#avatar').innerText = currentUser.name[0];
            
            renderMenu();
            loadPage('lessons');
        }

        function renderMenu() {
            const menu = [
                { id: 'lessons', icon: 'fa-play', label: 'الحصص' },
                { id: 'exams', icon: 'fa-file-signature', label: 'الاختبارات' }
            ];
            if(currentUser.role === 'admin') menu.push({ id: 'admin', icon: 'fa-tools', label: 'لوحة التحكم' });
            
            document.querySelector('#navMenu').innerHTML = menu.map(m => `
                <button onclick="loadPage('${m.id}')" class="w-full p-4 flex items-center gap-3 rounded-xl hover:bg-orange-600/20 transition group">
                    <i class="fa-solid ${m.icon} group-hover:text-orange-500"></i> ${m.label}
                </button>
            `).join('');
        }

        async function loadPage(page) {
            toggleLoader(true);
            const container = document.querySelector('#pageContent');
            const res = await fetch(`${API_URL}?action=getData`);
            globalData = await res.json();

            if(page === 'lessons') {
                container.innerHTML = globalData.lessons.map(l => `
                    <div class="glass p-5 rounded-[2rem] hover:scale-105 transition-all cursor-pointer border-b-4 border-transparent hover:border-orange-500" onclick="openVideo('${l.الرابط}', '${l.العنوان}')">
                        <div class="h-44 bg-slate-800 rounded-3xl flex items-center justify-center text-5xl mb-4 shadow-inner">
                            <i class="fa-solid fa-play text-orange-600"></i>
                        </div>
                        <h3 class="font-black text-lg">${l.العنوان}</h3>
                        <p class="text-slate-400 text-sm mt-1">${l.الوصف}</p>
                    </div>
                `).join('');
            }

            if(page === 'exams') {
                container.innerHTML = globalData.exams.map(e => `
                    <div class="glass p-6 rounded-[2rem] border-l-4 border-orange-500">
                        <h3 class="font-black text-xl mb-2">${e.الاسم}</h3>
                        <p class="text-sm text-slate-400 mb-4">المدة: ${e.المدة} دقيقة</p>
                        <button onclick="startExam('${e.الاسم}', ${e.المدة}, '${e.الأسئلة_JSON}')" class="w-full py-3 btn-orange text-sm">بدء الاختبار</button>
                    </div>
                `).join('');
            }

            if(page === 'admin') {
                container.className = "col-span-full space-y-8";
                container.innerHTML = `
                    <div class="grid md:grid-cols-2 gap-8">
                        <div class="glass p-8 rounded-[2rem]">
                            <h3 class="text-xl font-black mb-6 border-r-4 border-orange-500 pr-3">إضافة طالب</h3>
                            <div class="space-y-4">
                                <input id="sName" placeholder="الاسم" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none">
                                <input id="sUser" placeholder="اسم المستخدم" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none">
                                <input id="sPass" placeholder="كلمة المرور" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none">
                                <select id="sGrp" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none">
                                    <option>مجموعة السبت</option><option>مجموعة الثلاثاء</option>
                                </select>
                                <button onclick="adminAdd('addStudent')" class="w-full py-3 btn-orange">حفظ الطالب</button>
                            </div>
                        </div>
                        <div class="glass p-8 rounded-[2rem]">
                            <h3 class="text-xl font-black mb-6 border-r-4 border-orange-500 pr-3">رفع حصة</h3>
                            <div class="space-y-4">
                                <input id="lTitle" placeholder="العنوان" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none">
                                <input id="lUrl" placeholder="رابط يوتيوب" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none">
                                <textarea id="lDesc" placeholder="الوصف" class="w-full p-3 rounded-xl bg-slate-800 border border-slate-700 outline-none"></textarea>
                                <button onclick="adminAdd('addLesson')" class="w-full py-3 btn-orange">نشر الحصة</button>
                            </div>
                        </div>
                    </div>
                    <div class="glass p-8 rounded-[2rem] overflow-x-auto">
                         <h3 class="text-xl font-black mb-6">نتائج الطلاب</h3>
                         <table class="w-full text-right">
                            <thead><tr class="text-orange-500 border-b border-slate-700"><th class="p-3">الطالب</th><th class="p-3">الامتحان</th><th class="p-3">الدرجة</th></tr></thead>
                            <tbody>${globalData.results.map(r => `<tr class="border-b border-slate-800"><td>${r.الطالب}</td><td>${r.الامتحان}</td><td>${r.الدرجة}</td></tr>`).join('')}</tbody>
                         </table>
                    </div>
                `;
            } else { container.className = "grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"; }
            toggleLoader(false);
        }

        async function adminAdd(action) {
            toggleLoader(true);
            let payload = { action };
            if(action === 'addStudent') payload = { ...payload, name: sName.value, user: sUser.value, pass: sPass.value, group: sGrp.value };
            if(action === 'addLesson') payload = { ...payload, title: lTitle.value, url: lUrl.value, desc: lDesc.value };
            
            await fetch(API_URL, { method: 'POST', body: JSON.stringify(payload) });
            alert("تمت العملية بنجاح");
            loadPage('admin');
        }

        function openVideo(url, title) {
            const id = url.includes('v=') ? url.split('v=')[1].split('&')[0] : url.split('/').pop();
            document.querySelector('#pageContent').innerHTML = `
                <div class="col-span-full glass p-4 rounded-[2rem]">
                    <button onclick="loadPage('lessons')" class="mb-4 text-orange-500 font-bold"><i class="fa-solid fa-arrow-right"></i> عودة للحصص</button>
                    <iframe src="https://www.youtube.com/embed/${id}?rel=0&modestbranding=1" class="w-full aspect-video rounded-2xl shadow-2xl" allowfullscreen></iframe>
                    <h2 class="text-2xl font-black mt-6 px-4">${title}</h2>
                </div>
            `;
        }

        function logout() { localStorage.clear(); location.reload(); }
        function toggleLoader(s) { document.querySelector('#loader').classList.toggle('hidden', !s); }
    </script>
</body>
</html>
