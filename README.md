<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Senior Backend Dev Portfolio</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://unpkg.com/vue@3/dist/vue.global.prod.js"></script>
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

        .preloader { position: fixed; inset: 0; background: var(--bg-color); z-index: 10000; display: flex; justify-content: center; align-items: center; flex-direction: column; transition: opacity 0.5s ease, visibility 0.5s ease; }
        .preloader.hidden { opacity: 0; visibility: hidden; }
        .loader-logo { font-family: var(--font-code); color: var(--accent-color); font-size: 2rem; margin-bottom: 20px; }
        .loader-bar { width: 200px; height: 4px; background: var(--bg-lighter); border-radius: 2px; overflow: hidden; }
        .loader-fill { height: 100%; width: 0%; background: var(--accent-color); transition: width 0.3s ease; }

        nav { position: fixed; top: 0; width: 100%; padding: 20px 50px; display: flex; justify-content: space-between; align-items: center; background: rgba(10, 25, 47, 0.85); backdrop-filter: blur(10px); z-index: 100; border-bottom: 1px solid rgba(100, 255, 218, 0.1); }
        nav .logo { font-size: 24px; font-weight: 800; color: var(--accent-color); font-family: var(--font-code); }
        nav ul { display: flex; list-style: none; gap: 30px; }
        nav ul a { color: var(--text-secondary); text-decoration: none; font-size: 14px; transition: color 0.3s; display: flex; align-items: center; gap: 5px; }
        nav ul a:hover, nav ul a.active { color: var(--accent-color); }
        nav ul a .number { color: var(--accent-color); font-family: var(--font-code); font-size: 12px; }

        main { padding: 100px 50px 50px; max-width: 1200px; margin: 0 auto; }
        section { min-height: 100vh; display: flex; flex-direction: column; justify-content: center; padding: 80px 0; }
        section h2 { font-size: 32px; margin-bottom: 40px; display: flex; align-items: center; gap: 10px; }
        section h2 .title-number { color: var(--accent-color); font-family: var(--font-code); font-size: 20px; }
        section h2::after { content: ''; display: block; height: 1px; width: 300px; background: rgba(100, 255, 218, 0.3); }

        .glitch { position: relative; color: var(--text-primary); }
        .glitch::before, .glitch::after { content: attr(data-text); position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
        .glitch::before { left: 2px; text-shadow: -1px 0 var(--danger); clip: rect(24px, 550px, 90px, 0); animation: glitch-anim 2s infinite linear alternate-reverse; }
        .glitch::after { left: -2px; text-shadow: -1px 0 var(--accent-color); clip: rect(85px, 550px, 140px, 0); animation: glitch-anim2 3s infinite linear alternate-reverse; }
        @keyframes glitch-anim { 0% { clip: rect(11px, 9999px, 83px, 0); } 20% { clip: rect(49px, 9999px, 5px, 0); } 40% { clip: rect(33px, 9999px, 93px, 0); } 60% { clip: rect(70px, 9999px, 35px, 0); } 80% { clip: rect(95px, 9999px, 64px, 0); } 100% { clip: rect(12px, 9999px, 23px, 0); } }
        @keyframes glitch-anim2 { 0% { clip: rect(92px, 9999px, 12px, 0); } 20% { clip: rect(15px, 9999px, 90px, 0); } 40% { clip: rect(55px, 9999px, 28px, 0); } 60% { clip: rect(80px, 9999px, 5px, 0); } 80% { clip: rect(22px, 9999px, 70px, 0); } 100% { clip: rect(40px, 9999px, 90px, 0); } }

        #hero p { font-family: var(--font-code); color: var(--accent-color); margin-bottom: 20px; font-size: 18px; }
        #hero h1 { font-size: 80px; font-weight: 800; line-height: 1.1; margin-bottom: 10px; }
        #hero h3 { font-size: 40px; color: var(--text-secondary); margin-bottom: 30px; font-weight: 600; }
        #hero .cta-group { display: flex; gap: 20px; margin-top: 40px; }
        .typing-cursor { animation: blink 1s infinite; font-weight: 300; }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

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

        .about-container { display: grid; grid-template-columns: 3fr 2fr; gap: 50px; align-items: center; }
        .about-text p { color: var(--text-secondary); margin-bottom: 20px; font-size: 16px; line-height: 1.8; }
        .about-text ul { list-style: none; display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-top: 20px; }
        .about-text ul li { color: var(--text-secondary); font-family: var(--font-code); font-size: 14px; display: flex; align-items: center; gap: 10px; }
        .about-text ul li::before { content: '▹'; color: var(--accent-color); }
        .about-img { position: relative; width: 300px; height: 300px; margin: 0 auto; }
        .about-img .wrapper { width: 100%; height: 100%; background: var(--bg-light); border-radius: 10px; border: 2px solid var(--accent-color); display: flex; justify-content: center; align-items: center; font-size: 100px; color: var(--bg-lighter); overflow: hidden; transition: transform 0.3s; }
        .about-img:hover .wrapper { transform: translate(10px, 10px); }
        .about-img::before { content: ''; position: absolute; top: 20px; left: 20px; width: 100%; height: 100%; border: 2px solid var(--accent-color); border-radius: 10px; z-index: -1; transition: transform 0.3s; }
        .about-img:hover::before { transform: translate(-10px, -10px); }

        .tech-marquee-container { padding: 40px 0; overflow: hidden; background: var(--bg-light); border-top: 1px solid var(--bg-lighter); border-bottom: 1px solid var(--bg-lighter); }
        .tech-marquee { display: flex; gap: 50px; animation: scroll-marquee 20s linear infinite; white-space: nowrap; }
        .tech-marquee span { font-family: var(--font-code); font-size: 24px; color: var(--text-secondary); display: flex; align-items: center; gap: 50px; }
        .tech-marquee span::after { content: '⋆'; color: var(--accent-color); }
        @keyframes scroll-marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; text-align: center; }
        .stat-item { background: var(--bg-light); padding: 30px; border-radius: 8px; border: 1px solid var(--bg-lighter); transition: transform 0.3s; }
        .stat-item:hover { transform: translateY(-5px); border-color: var(--accent-shadow); }
        .stat-number { font-size: 48px; font-weight: 800; color: var(--accent-color); font-family: var(--font-code); margin-bottom: 10px; }
        .stat-desc { color: var(--text-secondary); font-size: 14px; }

        .services-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
        .service-card { background: var(--bg-light); padding: 30px; border-radius: 8px; border: 1px solid var(--bg-lighter); transition: all 0.3s; }
        .service-card:hover { border-color: var(--accent-color); transform: translateY(-5px); box-shadow: 0 10px 30px -15px var(--accent-shadow); }
        .service-icon { font-size: 32px; color: var(--accent-color); margin-bottom: 20px; }
        .service-card h3 { font-size: 20px; margin-bottom: 10px; color: var(--text-primary); }
        .service-card p { color: var(--text-secondary); font-size: 14px; line-height: 1.6; }

        .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; }
        .skill-category { background: var(--bg-light); padding: 25px; border-radius: 8px; transition: transform 0.3s; border: 1px solid transparent; }
        .skill-category:hover { transform: translateY(-5px); border-color: var(--accent-shadow); }
        .skill-category h3 { color: var(--text-primary); margin-bottom: 20px; font-size: 20px; border-bottom: 2px solid var(--bg-lighter); padding-bottom: 10px; display: inline-block; }
        .skill-item { margin-bottom: 15px; }
        .skill-header { display: flex; justify-content: space-between; margin-bottom: 5px; font-family: var(--font-code); font-size: 14px; }
        .skill-bar { height: 6px; background: var(--bg-lighter); border-radius: 3px; overflow: hidden; }
        .skill-fill { height: 100%; background: linear-gradient(90deg, var(--accent-color), #238636); width: 0; transition: width 1.5s cubic-bezier(0.25, 0.1, 0.25, 1); border-radius: 3px; }

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

        .timeline { position: relative; padding-right: 30px; }
        .timeline::before { content: ''; position: absolute; right: 0; top: 0; height: 100%; width: 2px; background: var(--bg-lighter); }
        .timeline-item { position: relative; margin-bottom: 40px; padding-right: 40px; transition: all 0.3s; }
        .timeline-item:hover { transform: translateX(-10px); }
        .timeline-item::before { content: ''; position: absolute; right: -6px; top: 5px; width: 12px; height: 12px; background: var(--accent-color); border-radius: 50%; box-shadow: 0 0 10px var(--accent-color); }
        .timeline-date { font-family: var(--font-code); color: var(--accent-color); font-size: 14px; margin-bottom: 5px; }
        .timeline-title { font-size: 22px; color: var(--text-primary); margin-bottom: 5px; }
        .timeline-company { color: var(--text-secondary); font-style: italic; margin-bottom: 10px; }
        .timeline-desc { color: var(--text-secondary); font-size: 15px; }

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

        footer { background: var(--bg-light); padding: 50px; text-align: center; border-top: 1px solid var(--bg-lighter); }
        .footer-content { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 20px; max-width: 1200px; margin: 0 auto; }
        .footer-links { display: flex; gap: 20px; }
        .footer-links a { color: var(--text-secondary); text-decoration: none; font-size: 14px; transition: color 0.3s; }
        .footer-links a:hover { color: var(--accent-color); }
        .social-links { display: flex; gap: 15px; }
        .social-links a { color: var(--text-secondary); font-size: 20px; transition: all 0.3s; width: 40px; height: 40px; border: 1px solid var(--bg-lighter); border-radius: 50%; display: flex; justify-content: center; align-items: center; }
        .social-links a:hover { color: var(--accent-color); border-color: var(--accent-color); transform: translateY(-3px); }
        footer p { color: var(--text-secondary); font-size: 12px; margin-top: 30px; font-family: var(--font-code); }

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
            .about-container { grid-template-columns: 1fr; }
            .about-img { width: 200px; height: 200px; margin-bottom: 30px; }
            .footer-content { flex-direction: column; text-align: center; }
        }
    </style>
</head>
<body>
    <div id="app">
        <div class="preloader" :class="{ hidden: !isLoading }">
            <div class="loader-logo">&lt; Dev / &gt;</div>
            <div class="loader-bar"><div class="loader-fill" :style="{ width: loadProgress + '%' }"></div></div>
        </div>

        <div class="scroll-progress" :style="{ width: scrollProgress + '%' }"></div>
        <canvas id="bg-canvas"></canvas>

        <nav>
            <div class="logo">&lt; Ahmad / &gt;</div>
            <ul>
                <li v-for="link in navLinks" :key="link.id">
                    <a :href="'#' + link.id" @click.prevent="scrollToSection(link.id)" :class="{ active: activeSection === link.id }">
                        <span class="number">0{{ link.id + 1 }}.</span> <span>{{ link.name }}</span>
                    </a>
                </li>
            </ul>
        </nav>

        <main>
            <section id="0">
                <p>سلام، نام من احمد است</p>
                <h1 class="glitch" data-text="Backend Developer">Backend Developer</h1>
                <h3>من <span style="color: var(--accent-color);">{{ typedText }}</span><span class="typing-cursor">|</span> می‌سازم.</h3>
                <div class="cta-group">
                    <a href="#5" @click.prevent="scrollToSection(5)" class="btn-modern btn-primary">تماس با من</a>
                    <a href="#2" @click.prevent="scrollToSection(2)" class="btn-modern btn-secondary">دیدن نمونه‌کارها</a>
                </div>
            </section>

            <section id="1" v-reveal>
                <h2><span class="title-number">01.</span> درباره من</h2>
                <div class="about-container">
                    <div class="about-text">
                        <p>سلام! من یک برنامه‌نویس بک‌اند با بیش از ۵ سال تجربه در طراحی و توسعه سیستم‌های مقیاس‌پذیر هستم. تخصص من تبدیل ایده‌های پیچیده به محصولاتی قابل اجرا و پایدار است.</p>
                        <p>من عاشق حل چالش‌های معماری، بهینه‌سازی دیتابیس‌ها و کار با تکنولوژی‌های جدید هستم. در پروژه‌هایم همیشه روی تمیزی کد، امنیت و مستندسازی تمرکز دارم تا تیم بتواند به راحتی کار خود را پیش ببرد.</p>
                        <ul>
                            <li>طراحی معماری میکروسرویس</li>
                            <li>بهینه‌سازی کوئری‌های دیتابیس</li>
                            <li>پیاده‌سازی سیستم‌های کشینگ</li>
                            <li>اتوماسیون و CI/CD</li>
                        </ul>
                    </div>
                    <div class="about-img">
                        <div class="wrapper"><i class="fas fa-user-secret"></i></div>
                    </div>
                </div>
            </section>

            <div class="tech-marquee-container">
                <div class="tech-marquee">
                    <span>Python</span><span>C#</span><span>Node.js</span><span>Docker</span><span>Kafka</span><span>PostgreSQL</span><span>Redis</span><span>MongoDB</span>
                    <span>Python</span><span>C#</span><span>Node.js</span><span>Docker</span><span>Kafka</span><span>PostgreSQL</span><span>Redis</span><span>MongoDB</span>
                </div>
            </div>

            <section id="2" v-reveal>
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
                    <div class="stat-item">
                        <div class="stat-number" data-target="15">0</div>
                        <div class="stat-desc">مقاله منتشر شده</div>
                    </div>
                </div>
            </section>

            <section id="3" v-reveal>
                <h2><span class="title-number">02.</span> خدمات</h2>
                <div class="services-grid">
                    <div class="service-card">
                        <i class="fas fa-server service-icon"></i>
                        <h3>طراحی API</h3>
                        <p>طراحی و پیاده‌سازی RESTful API و GraphQL با کارایی بالا، امنیت مناسب و مستندات استاندارد (Swagger).</p>
                    </div>
                    <div class="service-card">
                        <i class="fas fa-spider service-icon"></i>
                        <h3>وب‌اسکریپینگ</h3>
                        <p>استخراج داده‌های پیچیده از وب‌سایت‌ها با استفاده از Selenium و پایتون و ذخیره ساختاریافته در دیتابیس.</p>
                    </div>
                    <div class="service-card">
                        <i class="fas fa-database service-icon"></i>
                        <h3>معماری دیتابیس</h3>
                        <p>طراحی دیتابیس‌های رابطه‌ای (SQL) و غیررابطه‌ای (NoSQL)، بهینه‌سازی کوئری‌ها و پیاده‌سازی سیستم‌های کش.</p>
                    </div>
                    <div class="service-card">
                        <i class="fab fa-docker service-icon"></i>
                        <h3>دواپس و دیپلوی</h3>
                        <p>کانتینرسازی اپلیکیشن‌ها با داکر، راه‌اندازی سرورهای لینوکسی و پیاده‌سازی پایپ‌لاین‌های CI/CD.</p>
                    </div>
                </div>
            </section>

            <section id="4" v-reveal>
                <h2><span class="title-number">03.</span> مهارت‌های فنی</h2>
                <div class="skills-grid">
                    <div class="skill-category" v-for="cat in skillsData" :key="cat.title">
                        <h3>{{ cat.title }}</h3>
                        <div class="skill-item" v-for="skill in cat.items" :key="skill.name">
                            <div class="skill-header"><span>{{ skill.name }}</span><span>{{ skill.level }}%</span></div>
                            <div class="skill-bar"><div class="skill-fill" :data-level="skill.level"></div></div>
                        </div>
                    </div>
                </div>
            </section>

            <section id="5" v-reveal>
                <h2><span class="title-number">04.</span> نمونه‌کارها</h2>
                <div class="projects-grid">
                    <div class="project-card" v-for="project in projects" :key="project.title">
                        <div class="project-header">
                            <i class="fas fa-folder folder-icon"></i>
                            <div class="project-links">
                                <a href="#"><i class="fab fa-github"></i></a>
                                <a href="#"><i class="fas fa-external-link-alt"></i></a>
                            </div>
                        </div>
                        <h3>{{ project.title }}</h3>
                        <p>{{ project.desc }}</p>
                        <div class="tech-tags">
                            <span v-for="tech in project.tech" :key="tech">{{ tech }}</span>
                        </div>
                    </div>
                </div>
            </section>

            <section id="6" v-reveal>
                <h2><span class="title-number">05.</span> سوابق کاری</h2>
                <div class="timeline">
                    <div class="timeline-item" v-for="exp in experiences" :key="exp.date">
                        <div class="timeline-date">{{ exp.date }}</div>
                        <h3 class="timeline-title">{{ exp.title }}</h3>
                        <div class="timeline-company">{{ exp.company }}</div>
                        <p class="timeline-desc">{{ exp.desc }}</p>
                    </div>
                </div>
            </section>

            <section id="7" v-reveal>
                <h2><span class="title-number">06.</span> تماس با من</h2>
                <div class="contact-container">
                    <form @submit.prevent="submitForm">
                        <div class="input-group">
                            <input type="text" v-model="formData.name" required>
                            <label>نام و نام خانوادگی</label>
                            <i class="fas fa-user"></i>
                            <span class="underline"></span>
                            <span class="error-msg">{{ errors.name }}</span>
                        </div>
                        <div class="input-group">
                            <input type="email" v-model="formData.email" required>
                            <label>ایمیل</label>
                            <i class="fas fa-envelope"></i>
                            <span class="underline"></span>
                            <span class="error-msg">{{ errors.email }}</span>
                        </div>
                        <div class="input-group">
                            <textarea v-model="formData.message" required></textarea>
                            <label>متن پیام</label>
                            <i class="fas fa-comment"></i>
                            <span class="underline"></span>
                            <span class="error-msg">{{ errors.message }}</span>
                        </div>
                        <button type="submit" class="btn-modern btn-solid" :class="{ loading: isSubmitting, success: isSubmitted }">
                            <span v-if="!isSubmitting && !isSubmitted"><i class="fas fa-paper-plane"></i> ارسال پیام</span>
                            <span v-if="isSubmitting"><i class="fas fa-spinner fa-spin"></i> در حال ارسال...</span>
                            <span v-if="isSubmitted"><i class="fas fa-check"></i> ارسال شد!</span>
                        </button>
                    </form>
                </div>
            </section>
        </main>

        <footer>
            <div class="footer-content">
                <div class="footer-links">
                    <a href="#1" @click.prevent="scrollToSection(1)">درباره من</a>
                    <a href="#4" @click.prevent="scrollToSection(4)">مهارت‌ها</a>
                    <a href="#5" @click.prevent="scrollToSection(5)">نمونه‌کارها</a>
                    <a href="#7" @click.prevent="scrollToSection(7)">تماس</a>
                </div>
                <div class="social-links">
                    <a href="#"><i class="fab fa-github"></i></a>
                    <a href="#"><i class="fab fa-linkedin"></i></a>
                    <a href="#"><i class="fab fa-twitter"></i></a>
                    <a href="#"><i class="fab fa-telegram"></i></a>
                </div>
            </div>
            <p>طراحی و توسعه با Vue 3 &copy; 2024 Ahmad</p>
        </footer>
    </div>

    <script>
        const { createApp, ref, onMounted, onUnmounted, reactive } = Vue;

        createApp({
            setup() {
                const isLoading = ref(true);
                const loadProgress = ref(0);
                const activeSection = ref(0);
                const scrollProgress = ref(0);
                const navLinks = ref([
                    { id: 0, name: 'خانه' },
                    { id: 1, name: 'درباره' },
                    { id: 3, name: 'خدمات' },
                    { id: 4, name: 'مهارت‌ها' },
                    { id: 5, name: 'نمونه‌کارها' },
                    { id: 7, name: 'تماس' }
                ]);

                const handleScroll = () => {
                    const winHeight = window.innerHeight;
                    const docHeight = document.documentElement.scrollHeight;
                    const scrollTop = window.scrollY;
                    scrollProgress.value = (scrollTop / (docHeight - winHeight)) * 100;

                    const sections = document.querySelectorAll('section');
                    sections.forEach((sec, index) => {
                        const top = sec.offsetTop - 150;
                        const bottom = top + sec.offsetHeight;
                        if (scrollTop >= top && scrollTop < bottom) activeSection.value = index;
                    });
                };

                const scrollToSection = (id) => document.getElementById(id).scrollIntoView({ behavior: 'smooth' });

                const roles = ["REST APIs", "Microservices", "Web Scrapers", "Dockerized Apps"];
                const typedText = ref("");
                let roleIndex = 0, charIndex = 0, isDeleting = false;

                const typeEffect = () => {
                    const current = roles[roleIndex];
                    typedText.value = isDeleting ? current.substring(0, charIndex - 1) : current.substring(0, charIndex + 1);
                    charIndex = isDeleting ? charIndex - 1 : charIndex + 1;
                    if (!isDeleting && charIndex === current.length) setTimeout(() => isDeleting = true, 2000);
                    else if (isDeleting && charIndex === 0) { isDeleting = false; roleIndex = (roleIndex + 1) % roles.length; }
                    setTimeout(typeEffect, isDeleting ? 50 : 150);
                };

                const skillsData = ref([
                    { title: 'Backend & Languages', items: [
                        { name: 'Python (Django/FastAPI)', level: 95 }, { name: 'C# & ASP.NET Core', level: 90 },
                        { name: 'Node.js & Express', level: 85 }, { name: 'RESTful API Design', level: 92 }
                    ]},
                    { title: 'Databases & Caching', items: [
                        { name: 'PostgreSQL & SQL Server', level: 88 }, { name: 'MongoDB', level: 85 },
                        { name: 'Redis', level: 80 }, { name: 'Entity Framework', level: 75 }
                    ]},
                    { title: 'DevOps & Architecture', items: [
                        { name: 'Docker & Linux', level: 82 }, { name: 'Kafka', level: 70 },
                        { name: 'Git & CI/CD', level: 85 }, { name: 'Selenium & Scraping', level: 90 }
                    ]}
                ]);

                const projects = ref([
                    { title: 'Real-time Price Tracker', desc: 'سیستم مانیتورینگ قیمت با پایتون و Selenium که تغییرات را از طریق Kafka به بک‌اند Node.js ارسال می‌کند.', tech: ['Python', 'Node.js', 'Kafka', 'Redis'] },
                    { title: 'Smart Content CMS', desc: 'یک پلتفرم مدیریت محتوای مبتنی بر هوش مصنوعی برای تولید مقالات خودکار با FastAPI و PostgreSQL.', tech: ['FastAPI', 'Postgres', 'Docker'] },
                    { title: 'Microservices Auth System', desc: 'پیاده‌سازی سیستم احراز هویت مبتنی بر میکروسرویس با ASP.NET Core و Entity Framework.', tech: ['C#', 'ASP.NET', 'SQL Server'] }
                ]);

                const experiences = ref([
                    { date: '1400 - اکنون', title: 'Senior Backend Developer', company: 'شرکت فناوری پردازش', desc: 'طراحی و پیاده‌سازی معماری میکروسرویس با پایتون، Node.js و Kafka.' },
                    { date: '1397 - 1400', title: 'Full Stack Developer', company: 'استارتاپ هوش مالی', desc: 'توسعه API های مبتنی بر ASP.NET Core و طراحی اسکریپت‌های هوشمند.' }
                ]);

                const formData = reactive({ name: '', email: '', message: '' });
                const errors = reactive({ name: '', email: '', message: '' });
                const isSubmitting = ref(false);
                const isSubmitted = ref(false);

                const validateForm = () => {
                    errors.name = formData.name.length < 3 ? 'نام باید حداقل ۳ کاراکتر باشد.' : '';
                    errors.email = !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email) ? 'ایمیل معتبر نیست.' : '';
                    errors.message = formData.message.length < 10 ? 'پیام باید حداقل ۱۰ کاراکتر باشد.' : '';
                    return !errors.name && !errors.email && !errors.message;
                };

                const submitForm = async () => {
                    if (!validateForm()) return;
                    isSubmitting.value = true;
                    await new Promise(resolve => setTimeout(resolve, 1500));
                    isSubmitting.value = false;
                    isSubmitted.value = true;
                    setTimeout(() => {
                        isSubmitted.value = false;
                        formData.name = ''; formData.email = ''; formData.message = '';
                    }, 3000);
                };

                const vReveal = {
                    mounted(el) {
                        el.classList.add('reveal');
                        new IntersectionObserver((entries) => {
                            if (entries[0].isIntersecting) {
                                el.classList.add('active');
                                el.querySelectorAll('.skill-fill').forEach(bar => bar.style.width = bar.dataset.level + '%');
                                
                                el.querySelectorAll('.stat-number').forEach(stat => {
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
                        }, { threshold: 0.1 }).observe(el);
                    }
                };

                const initCanvas = () => {
                    const canvas = document.getElementById('bg-canvas');
                    const ctx = canvas.getContext('2d');
                    let particles = [];
                    let mouse = { x: null, y: null, radius: 150 };

                    const resize = () => { canvas.width = innerWidth; canvas.height = innerHeight; };
                    window.addEventListener('resize', resize);
                    resize();
                    window.addEventListener('mousemove', (e) => { mouse.x = e.clientX; mouse.y = e.clientY; });

                    class Particle {
                        constructor() {
                            this.x = Math.random() * canvas.width;
                            this.y = Math.random() * canvas.height;
                            this.size = Math.random() * 2 + 0.5;
                            this.baseX = this.x; this.baseY = this.y;
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

                    for (let i = 0; i < 80; i++) particles.push(new Particle());

                    const connect = () => {
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
                    };

                    const animate = () => {
                        ctx.clearRect(0, 0, canvas.width, canvas.height);
                        particles.forEach(p => { p.update(); p.draw(); });
                        connect();
                        requestAnimationFrame(animate);
                    };
                    animate();
                };

                onMounted(() => {
                    window.addEventListener('scroll', handleScroll);
                    typeEffect();
                    initCanvas();
                    const loadInterval = setInterval(() => {
                        loadProgress.value += 10;
                        if (loadProgress.value >= 100) {
                            clearInterval(loadInterval);
                            setTimeout(() => { isLoading.value = false; }, 500);
                        }
                    }, 100);
                });

                onUnmounted(() => {
                    window.removeEventListener('scroll', handleScroll);
                });

                return {
                    isLoading, loadProgress, activeSection, scrollProgress, navLinks, scrollToSection, typedText, 
                    skillsData, projects, experiences, formData, errors, isSubmitting, isSubmitted, submitForm, vReveal
                };
            }
        }).mount('#app');
    </script>
</body>
</html>
