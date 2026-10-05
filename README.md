<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Senior Backend Dev Portfolio</title>
    <link rel="icon" href="data:,">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-color: #0a192f;
            --bg-light: #112240;
            --bg-lighter: #233554;
            --text-primary: #e6f1ff;
            --text-secondary: #8892b0;
            --accent-color: #64ffda;
            --accent-shadow: rgba(100, 255, 218, 0.1);
            --danger: #ff6464;
            --font-main: 'Poppins', sans-serif;
            --font-code: 'Fira Code', monospace;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }

        body {
            background-color: var(--bg-color);
            color: var(--text-primary);
            font-family: var(--font-main);
            overflow-x: hidden;
            line-height: 1.5;
        }

        #bg-canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; }
        .scroll-progress { position: fixed; top: 0; left: 0; height: 4px; width: 0%; background: var(--accent-color); z-index: 1001; box-shadow: 0 0 10px var(--accent-color); }

        /* Preloader */
        .preloader { position: fixed; inset: 0; background: var(--bg-color); z-index: 10000; display: flex; justify-content: center; align-items: center; flex-direction: column; transition: opacity 0.5s ease, visibility 0.5s ease; }
        .preloader.hidden { opacity: 0; visibility: hidden; }
        .loader-logo { font-family: var(--font-code); color: var(--accent-color); font-size: 2rem; margin-bottom: 20px; }
        .loader-bar { width: 200px; height: 4px; background: var(--bg-lighter); border-radius: 2px; overflow: hidden; }
        .loader-fill { height: 100%; width: 0%; background: var(--accent-color); transition: width 0.3s ease; }

        /* Navbar */
        nav { position: fixed; top: 0; width: 100%; padding: 20px 50px; display: flex; justify-content: space-between; align-items: center; background: rgba(10, 25, 47, 0.85); backdrop-filter: blur(10px); z-index: 100; border-bottom: 1px solid rgba(100, 255, 218, 0.1); }
        nav .logo { font-size: 24px; font-weight: 800; color: var(--accent-color); font-family: var(--font-code); }
        nav ul { display: flex; list-style: none; gap: 30px; }
        nav ul a { color: var(--text-secondary); text-decoration: none; font-size: 14px; transition: color 0.3s; display: flex; align-items: center; gap: 5px; }
        nav ul a:hover, nav ul a.active { color: var(--accent-color); }
        nav ul a .number { color: var(--accent-color); font-family: var(--font-code); font-size: 12px; }

        /* Sections General */
        main { padding: 100px 50px 50px; max-width: 1200px; margin: 0 auto; }
        section { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; padding: 80px 0; }
        section h2 { font-size: 32px; margin-bottom: 40px; display: flex; align-items: center; gap: 10px; }
        section h2 .title-number { color: var(--accent-color); font-family: var(--font-code); font-size: 20px; }
        section h2::after { content: ''; display: block; height: 1px; width: 300px; background: rgba(100, 255, 218, 0.3); }

        /* Glitch Text */
        .glitch { position: relative; color: var(--text-primary); }
        .glitch::before, .glitch::after { content: attr(data-text); position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
        .glitch::before { left: 2px; text-shadow: -1px 0 var(--danger); clip: rect(24px, 550px, 90px, 0); animation: glitch-anim 2s infinite linear alternate-reverse; }
        .glitch::after { left: -2px; text-shadow: -1px 0 var(--accent-color); clip: rect(85px, 550px, 140px, 0); animation: glitch-anim2 3s infinite linear alternate-reverse; }
        @keyframes glitch-anim { 0% { clip: rect(11px, 9999px, 83px, 0); } 20% { clip: rect(49px, 9999px, 5px, 0); } 40% { clip: rect(33px, 9999px, 93px, 0); } 60% { clip: rect(70px, 9999px, 35px, 0); } 80% { clip: rect(95px, 9999px, 64px, 0); } 100% { clip: rect(12px, 9999px, 23px, 0); } }
        @keyframes glitch-anim2 { 0% { clip: rect(92px, 9999px, 12px, 0); } 20% { clip: rect(15px, 9999px, 90px, 0); } 40% { clip: rect(55px, 9999px, 28px, 0); } 60% { clip: rect(80px, 9999px, 5px, 0); } 80% { clip: rect(22px, 9999px, 70px, 0); } 100% { clip: rect(40px, 9999px, 90px, 0); } }

        /* Hero */
        #hero p { font-family: var(--font-code); color: var(--accent-color); margin-bottom: 20px; font-size: 18px; }
        #hero h1 { font-size: 80px; font-weight: 800; line-height: 1.1; margin-bottom: 10px; }
        #hero h3 { font-size: 40px; color: var(--text-secondary); margin-bottom: 30px; font-weight: 600; }
        #hero .cta-group { display: flex; gap: 20px; margin-top: 40px; }
        .typing-cursor { animation: blink 1s infinite; font-weight: 300; }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

        /* Modern Pill Buttons */
        .btn-modern { position: relative; overflow: hidden; isolation: isolate; padding: 14px 32px; border-radius: 50px; font-family: var(--font-code); font-size: 15px; font-weight: 600; cursor: pointer; text-decoration: none; display: inline-flex; justify-content: center; align-items: center; gap: 10px; transition: color 0.4s ease, box-shadow 0.4s ease, transform 0.2s ease; z-index: 1; }
        .btn-modern::before { content: ''; position: absolute; right: 0; top: 0; width: 0; height: 100%; background: var(--accent-color); z-index: -1; transition: width 0.4s cubic-bezier(0.25, 0.1, 0.25, 1); }
        .btn-modern:hover { color: var(--bg-color); box-shadow: 0 0 20px var(--accent-shadow); transform: translateY(-2px); }
        .btn-modern:hover::before { width: 100%; }
        .btn-primary { background: transparent; color: var(--accent-color); border: 1px solid var(--accent-color); }
        .btn-secondary { background: transparent; color: var(--text-secondary); border: 1px solid var(--text-secondary); }
        .btn-secondary::before { background: var(--text-secondary); }
        .btn-solid { background: var(--accent-color); color: var(--bg-color); border: 1px solid var(--accent-color); width: 100%; }
        .btn-solid::before { background: var(--bg-lighter); }
        .btn-solid:hover { color: var(--accent-color); }
        .btn-solid.loading { background: var(--bg-lighter); color: var(--text-secondary); border-color: var(--bg-lighter); pointer-events: none; }
        .btn-solid.success { background: #238636; color: #fff; border-color: #238636; pointer-events: none; }

        /* Stats */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; text-align: center; }
        .stat-item { background: var(--bg-light); padding: 30px; border-radius: 8px; border: 1px solid var(--bg-lighter); transition: transform 0.3s; }
        .stat-item:hover { transform: translateY(-5px); border-color: var(--accent-shadow); }
        .stat-number { font-size: 48px; font-weight: 800; color: var(--accent-color); font-family: var(--font-code); margin-bottom: 10px; }
        .stat-desc { color: var(--text-secondary); font-size: 14px; }

        /* Skills */
        .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; }
        .skill-category { background: var(--bg-light); padding: 25px; border-radius: 8px; transition: transform 0.3s; border: 1px solid transparent; }
        .skill-category:hover { transform: translateY(-5px); border-color: var(--accent-shadow); }
        .skill-category h3 { color: var(--text-primary); margin-bottom: 20px; font-size: 20px; border-bottom: 2px solid var(--bg-lighter); padding-bottom: 10px; display: inline-block; }
        .skill-item { margin-bottom: 15px; }
        .skill-header { display: flex; justify-content: space-between; margin-bottom: 5px; font-family: var(--font-code); font-size: 14px; }
        .skill-bar { height: 6px; background: var(--bg-lighter); border-radius: 3px; overflow: hidden; }
        .skill-fill { height: 100%; background: linear-gradient(90deg, var(--accent-color), #238636); width: 0; transition: width 1.5s cubic-bezier(0.25, 0.1, 0.25, 1); border-radius: 3px; }

        /* Projects */
        .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        .project-card { background: rgba(17, 34, 64, 0.7); backdrop-filter: blur(5px); padding: 30px; border-radius: 8px; border: 1px solid var(--bg-lighter); transition: all 0.4s ease; transform-style: preserve-3d; }
        .project-card:hover { transform: translateY(-10px) rotateX(2deg); border-color: var(--accent-color); box-shadow: 0 10px 30px -15px var(--accent-shadow); }
        .project-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .folder-icon { font-size: 40px; color: var(--accent-color); }
        .project-links { display: flex; gap: 15px; }
        .project-links a { color: var(--text-secondary); font-size: 20px; transition: color 0.3s; }
        .project-links a:hover { color: var(--accent-color); }
        .project-card h3 { font-size: 22px; margin-bottom: 15px; color: var(--text-primary); }
        .project-card p { color: var(--text-secondary); font-size: 15px; margin-bottom: 20px; line-height: 1.6; }
        .tech-tags { display: flex; flex-wrap: wrap; gap: 10px; font-family: var(--font-code); font-size: 12px; }
        .tech-tags span { background: var(--bg-color); padding: 5px 10px; border-radius: 4px; color: var(--text-secondary); }

        /* Contact Form */
        .contact-container { max-width: 600px; margin: 0 auto; }
        .input-group { position: relative; margin-bottom: 20px; }
        .input-group input, .input-group textarea { width: 100%; padding: 10px 40px 10px 10px; background: transparent; border: none; border-bottom: 1px solid var(--text-secondary); color: var(--text-primary); font-family: var(--font-main); font-size: 16px; transition: border-color 0.3s; resize: vertical; }
        .input-group textarea { min-height: 100px; }
        .input-group label { position: absolute; top: 10px; right: 40px; color: var(--text-secondary); pointer-events: none; transition: all 0.3s ease; font-size: 16px; }
        .input-group input:focus ~ label, .input-group input:valid ~ label, .input-group textarea:focus ~ label, .input-group textarea:valid ~ label { top: -15px; right: 0; font-size: 14px; color: var(--accent-color); font-family: var(--font-code); }
        .input-group i { position: absolute; top: 12px; right: 0; color: var(--text-secondary); transition: color 0.3s; font-size: 18px; }
        .input-group input:focus ~ i, .input-group textarea:focus ~ i { color: var(--accent-color); }
        .underline { position: absolute; bottom: 0; right: 0; height: 2px; width: 0%; background: var(--accent-color); transition: width 0.4s ease; }
        .input-group input:focus ~ .underline, .input-group textarea:focus ~ .underline { width: 100%; }
        .error-msg { color: var(--danger); font-size: 12px; margin-top: 2px; font-family: var(--font-code); display: block; height: 12px; text-align: right; }

        /* Footer */
        footer { background: var(--bg-light); padding: 50px; text-align: center; border-top: 1px solid var(--bg-lighter); }
        .social-links { display: flex; justify-content: center; gap: 15px; margin-bottom: 20px; }
        .social-links a { color: var(--text-secondary); font-size: 20px; transition: all 0.3s; width: 40px; height: 40px; border: 1px solid var(--bg-lighter); border-radius: 50%; display: flex; justify-content: center; align-items: center; }
        .social-links a:hover { color: var(--accent-color); border-color: var(--accent-color); transform: translateY(-3px); }
        footer p { color: var(--text-secondary); font-size: 12px; font-family: var(--font-code); }

        /* Reveal Animation */
        .reveal { opacity: 0; transform: translateY(40px); transition: all 1s cubic-bezier(0.25, 0.1, 0.25, 1); }
        .reveal.active { opacity: 1; transform: translateY(0); }

        @media (max-width: 768px) {
            nav { padding: 15px 20px; }
            nav ul { gap: 15px; }
            nav ul a span:not(.number) { display: none; }
            main { padding: 80px 20px; }
            #hero h1 { font-size: 40px; }
            #hero h3 { font-size: 24px; }
            section h2::after { width: 100px; }
            .btn-modern { width: 100%; text-align: center; }
            #hero .cta-group { flex-direction: column; }
        }
    </style>
</head>
<body>
    <!-- Preloader -->
    <div class="preloader" id="preloader">
        <div class="loader-logo">&lt; Dev / &gt;</div>
        <div class="loader-bar"><div class="loader-fill" id="loader-fill"></div></div>
    </div>

    <div class="scroll-progress" id="scroll-progress"></div>
    <canvas id="bg-canvas"></canvas>

    <!-- Navbar -->
    <nav>
        <div class="logo">&lt; Ahmad / &gt;</div>
        <ul>
            <li><a href="#0" class="active"><span class="number">01.</span> <span>خانه</span></a></li>
            <li><a href="#1"><span class="number">02.</span> <span>آمار</span></a></li>
            <li><a href="#2"><span class="number">03.</span> <span>مهارت‌ها</span></a></li>
            <li><a href="#3"><span class="number">04.</span> <span>نمونه‌کارها</span></a></li>
            <li><a href="#4"><span class="number">05.</span> <span>تماس</span></a></li>
        </ul>
    </nav>

    <main>
        <!-- Hero -->
        <section id="0">
            <p>سلام، نام من احمد است</p>
            <h1 class="glitch" data-text="Backend Developer">Backend Developer</h1>
            <h3>من <span style="color: var(--accent-color);" id="typed-text"></span><span class="typing-cursor">|</span> می‌سازم.</h3>
            <div class="cta-group">
                <a href="#4" class="btn-modern btn-primary">تماس با من</a>
                <a href="#3" class="btn-modern btn-secondary">دیدن نمونه‌کارها</a>
            </div>
        </section>

        <!-- Stats -->
        <section id="1" class="reveal">
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-number" data-target="50">0</div>
                    <div class="stat-desc">پروژه‌ی انجام شده</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" data-target="5">0</div>
                    <div class="stat-desc">سال تجربه</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number" data-target="20">0</div>
                    <div class="stat-desc">مشتری راضی</div>
                </div>
            </div>
        </section>

        <!-- Skills -->
        <section id="2" class="reveal">
            <h2><span class="title-number">01.</span> مهارت‌های فنی</h2>
            <div class="skills-grid">
                <div class="skill-category">
                    <h3>Backend & Languages</h3>
                    <div class="skill-item">
                        <div class="skill-header"><span>Python (Django/FastAPI)</span><span>95%</span></div>
                        <div class="skill-bar"><div class="skill-fill" data-level="95"></div></div>
                    </div>
                    <div class="skill-item">
                        <div class="skill-header"><span>C# & ASP.NET Core</span><span>90%</span></div>
                        <div class="skill-bar"><div class="skill-fill" data-level="90"></div></div>
                    </div>
                    <div class="skill-item">
                        <div class="skill-header"><span>Node.js & Express</span><span>85%</span></div>
                        <div class="skill-bar"><div class="skill-fill" data-level="85"></div></div>
                    </div>
                </div>
                <div class="skill-category">
                    <h3>Databases & Caching</h3>
                    <div class="skill-item">
                        <div class="skill-header"><span>PostgreSQL & SQL Server</span><span>88%</span></div>
                        <div class="skill-bar"><div class="skill-fill" data-level="88"></div></div>
                    </div>
                    <div class="skill-item">
                        <div class="skill-header"><span>MongoDB</span><span>85%</span></div>
                        <div class="skill-bar"><div class="skill-fill" data-level="85"></div></div>
                    </div>
                    <div class="skill-item">
                        <div class="skill-header"><span>Redis</span><span>80%</span></div>
                        <div class="skill-bar"><div class="skill-fill" data-level="80"></div></div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Projects -->
        <section id="3" class="reveal">
            <h2><span class="title-number">02.</span> نمونه‌کارها</h2>
            <div class="projects-grid">
                <div class="project-card">
                    <div class="project-header">
                        <i class="fas fa-folder folder-icon"></i>
                        <div class="project-links">
                            <a href="#"><i class="fab fa-github"></i></a>
                            <a href="#"><i class="fas fa-external-link-alt"></i></a>
                        </div>
                    </div>
                    <h3>Real-time Price Tracker</h3>
                    <p>سیستم مانیتورینگ قیمت با پایتون و Selenium که تغییرات را از طریق Kafka به بک‌اند Node.js ارسال می‌کند.</p>
                    <div class="tech-tags"><span>Python</span><span>Node.js</span><span>Kafka</span><span>Redis</span></div>
                </div>
                <div class="project-card">
                    <div class="project-header">
                        <i class="fas fa-folder folder-icon"></i>
                        <div class="project-links">
                            <a href="#"><i class="fab fa-github"></i></a>
                            <a href="#"><i class="fas fa-external-link-alt"></i></a>
                        </div>
                    </div>
                    <h3>Smart Content CMS</h3>
                    <p>یک پلتفرم مدیریت محتوای مبتنی بر هوش مصنوعی برای تولید مقالات خودکار با FastAPI و PostgreSQL.</p>
                    <div class="tech-tags"><span>FastAPI</span><span>Postgres</span><span>Docker</span></div>
                </div>
                <div class="project-card">
                    <div class="project-header">
                        <i class="fas fa-folder folder-icon"></i>
                        <div class="project-links">
                            <a href="#"><i class="fab fa-github"></i></a>
                            <a href="#"><i class="fas fa-external-link-alt"></i></a>
                        </div>
                    </div>
                    <h3>Microservices Auth System</h3>
                    <p>پیاده‌سازی سیستم احراز هویت مبتنی بر میکروسرویس با ASP.NET Core و Entity Framework.</p>
                    <div class="tech-tags"><span>C#</span><span>ASP.NET</span><span>SQL Server</span></div>
                </div>
            </div>
        </section>

        <!-- Contact -->
        <section id="4" class="reveal">
            <h2><span class="title-number">03.</span> تماس با من</h2>
            <div class="contact-container">
                <form id="contact-form">
                    <div class="input-group">
                        <input type="text" id="name" required>
                        <label>نام و نام خانوادگی</label>
                        <i class="fas fa-user"></i>
                        <span class="underline"></span>
                        <span class="error-msg" id="error-name"></span>
                    </div>
                    <div class="input-group">
                        <input type="email" id="email" required>
                        <label>ایمیل</label>
                        <i class="fas fa-envelope"></i>
                        <span class="underline"></span>
                        <span class="error-msg" id="error-email"></span>
                    </div>
                    <div class="input-group">
                        <textarea id="message" required></textarea>
                        <label>متن پیام</label>
                        <i class="fas fa-comment"></i>
                        <span class="underline"></span>
                        <span class="error-msg" id="error-message"></span>
                    </div>
                    <button type="submit" class="btn-modern btn-solid" id="submit-btn">
                        <span class="btn-text"><i class="fas fa-paper-plane"></i> ارسال پیام</span>
                    </button>
                </form>
            </div>
        </section>
    </main>

    <footer>
        <div class="social-links">
            <a href="#"><i class="fab fa-github"></i></a>
            <a href="#"><i class="fab fa-linkedin"></i></a>
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="#"><i class="fab fa-telegram"></i></a>
        </div>
        <p>طراحی و توسعه با Vanilla JS &copy; 2024 Ahmad</p>
    </footer>

    <script>
        // --- 1. Preloader ---
        const preloader = document.getElementById('preloader');
        const loaderFill = document.getElementById('loader-fill');
        let loadProgress = 0;
        const loadInterval = setInterval(() => {
            loadProgress += 10;
            loaderFill.style.width = loadProgress + '%';
            if (loadProgress >= 100) {
                clearInterval(loadInterval);
                setTimeout(() => preloader.classList.add('hidden'), 500);
            }
        }, 100);

        // --- 2. Scroll Progress & Navbar Active ---
        const scrollProgress = document.getElementById('scroll-progress');
        const navLinks = document.querySelectorAll('nav ul a');
        const sections = document.querySelectorAll('section');

        window.addEventListener('scroll', () => {
            const winHeight = window.innerHeight;
            const docHeight = document.documentElement.scrollHeight;
            const scrollTop = window.scrollY;
            scrollProgress.style.width = (scrollTop / (docHeight - winHeight)) * 100 + '%';

            sections.forEach((sec, index) => {
                const top = sec.offsetTop - 150;
                const bottom = top + sec.offsetHeight;
                if (scrollTop >= top && scrollTop < bottom) {
                    navLinks.forEach(a => a.classList.remove('active'));
                    if (navLinks[index]) navLinks[index].classList.add('active');
                }
            });
        });

        // --- 3. Typing Effect ---
        const roles = ["REST APIs", "Microservices", "Web Scrapers", "Dockerized Apps"];
        const typedTextSpan = document.getElementById('typed-text');
        let roleIndex = 0, charIndex = 0, isDeleting = false;

        function typeEffect() {
            const current = roles[roleIndex];
            typedTextSpan.textContent = isDeleting ? current.substring(0, charIndex - 1) : current.substring(0, charIndex + 1);
            charIndex = isDeleting ? charIndex - 1 : charIndex + 1;

            if (!isDeleting && charIndex === current.length) {
                setTimeout(() => isDeleting = true, 2000);
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                roleIndex = (roleIndex + 1) % roles.length;
            }
            setTimeout(typeEffect, isDeleting ? 50 : 150);
        }
        setTimeout(typeEffect, 1000); // Start after preloader

        // --- 4. Reveal on Scroll & Animate Stats/Skills ---
        const revealElements = document.querySelectorAll('.reveal');
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                    
                    // Animate Skill Bars
                    entry.target.querySelectorAll('.skill-fill').forEach(bar => {
                        bar.style.width = bar.dataset.level + '%';
                    });

                    // Animate Stats
                    entry.target.querySelectorAll('.stat-number').forEach(stat => {
                        const target = +stat.dataset.target;
                        let current = 0;
                        const increment = target / 50;
                        const updateStat = () => {
                            current += increment;
                            if (current < target) {
                                stat.textContent = Math.ceil(current);
                                requestAnimationFrame(updateStat);
                            } else {
                                stat.textContent = target + (target > 15 ? '+' : '');
                            }
                        };
                        updateStat();
                    });
                }
            });
        }, { threshold: 0.1 });
        revealElements.forEach(el => observer.observe(el));

        // --- 5. Contact Form Validation ---
        const form = document.getElementById('contact-form');
        const submitBtn = document.getElementById('submit-btn');
        const btnText = submitBtn.querySelector('.btn-text');

        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const message = document.getElementById('message').value;

            let isValid = true;
            
            document.getElementById('error-name').textContent = name.length < 3 ? 'نام باید حداقل ۳ کاراکتر باشد.' : '';
            if(name.length < 3) isValid = false;
            
            document.getElementById('error-email').textContent = !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email) ? 'ایمیل معتبر نیست.' : '';
            if(!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) isValid = false;
            
            document.getElementById('error-message').textContent = message.length < 10 ? 'پیام باید حداقل ۱۰ کاراکتر باشد.' : '';
            if(message.length < 10) isValid = false;

            if (!isValid) return;

            submitBtn.classList.add('loading');
            btnText.innerHTML = '<i class="fas fa-spinner fa-spin"></i> در حال ارسال...';

            // Simulate API Call
            await new Promise(resolve => setTimeout(resolve, 1500));

            submitBtn.classList.remove('loading');
            submitBtn.classList.add('success');
            btnText.innerHTML = '<i class="fas fa-check"></i> ارسال شد!';

            setTimeout(() => {
                submitBtn.classList.remove('success');
                btnText.innerHTML = '<i class="fas fa-paper-plane"></i> ارسال پیام';
                form.reset();
            }, 3000);
        });

        // --- 6. Background Particles Canvas ---
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [];
        let mouse = { x: null, y: null, radius: 150 };

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        window.addEventListener('mousemove', (e) => {
            mouse.x = e.clientX;
            mouse.y = e.clientY;
        });

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 0.5;
                this.baseX = this.x;
                this.baseY = this.y;
                this.density = Math.random() * 30 + 1;
            }
            draw() {
                ctx.fillStyle = 'rgba(100, 255, 218, 0.4)';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.closePath();
                ctx.fill();
            }
            update() {
                let dx = mouse.x - this.x;
                let dy = mouse.y - this.y;
                let dist = Math.sqrt(dx * dx + dy * dy);
                if (dist < mouse.radius) {
                    let forceDirectionX = dx / dist;
                    let forceDirectionY = dy / dist;
                    let force = (mouse.radius - dist) / mouse.radius;
                    this.x -= forceDirectionX * force * this.density / 5;
                    this.y -= forceDirectionY * force * this.density / 5;
                } else {
                    if (this.x !== this.baseX) this.x -= (this.x - this.baseX) / 10;
                    if (this.y !== this.baseY) this.y -= (this.y - this.baseY) / 10;
                }
            }
        }

        function initParticles() {
            particles = [];
            for (let i = 0; i < 80; i++) {
                particles.push(new Particle());
            }
        }
        initParticles();

        function connectParticles() {
            let opacity = 1;
            for (let a = 0; a < particles.length; a++) {
                for (let b = a; b < particles.length; b++) {
                    let dx = particles[a].x - particles[b].x;
                    let dy = particles[a].y - particles[b].y;
                    let dist = Math.sqrt(dx * dx + dy * dy);
                    if (dist < 120) {
                        opacity = 1 - (dist / 120);
                        ctx.strokeStyle = `rgba(100, 255, 218, ${opacity * 0.2})`;
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(particles[a].x, particles[a].y);
                        ctx.lineTo(particles[b].x, particles[b].y);
                        ctx.stroke();
                    }
                }
            }
        }

        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => { p.update(); p.draw(); });
            connectParticles();
            requestAnimationFrame(animateParticles);
        }
        animateParticles();
    </script>
</body>
</html>
