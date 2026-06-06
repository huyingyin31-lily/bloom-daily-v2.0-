# bloom daily
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>今日成长记录</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg: #fff7f8;
      --bg2: #f3ece7;
      --card: rgba(255,255,255,.82);
      --text: #44343a;
      --muted: #8a737b;
      --primary: #dc7f9a;
      --deep: #bd637d;
      --green: #8fb79b;
      --border: rgba(219,178,190,.46);
      --shadow: 0 20px 55px rgba(169,116,130,.18);
    }
    body {
      min-height: 100vh;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif;
      color: var(--text);
      background:
        radial-gradient(circle at 12% 8%, #ffe2eb 0 18%, transparent 34%),
        radial-gradient(circle at 88% 18%, #dcecdf 0 16%, transparent 33%),
        linear-gradient(135deg, var(--bg), var(--bg2));
    }
    button, input, textarea { font: inherit; }
    button { border: 0; cursor: pointer; }

    .auth-screen {
      min-height: 100vh;
      display: grid;
      place-items: center;
      padding: 28px 16px;
    }
    body.logged-in .auth-screen { display: none; }
    body:not(.logged-in) .app { display: none; }

    .auth-card {
      width: min(980px, 100%);
      display: grid;
      grid-template-columns: .9fr 1.1fr;
      overflow: hidden;
      border-radius: 34px;
      background: var(--card);
      border: 1px solid var(--border);
      box-shadow: var(--shadow);
      backdrop-filter: blur(18px);
    }
    .auth-art {
      min-height: 540px;
      padding: 34px;
      color: #fff;
      background: linear-gradient(135deg, #de86a0, #c9a0b2 52%, #8fb79b);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }
    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
      font-weight: 900;
      color: var(--deep);
    }
    .auth-art .logo { color: #fff; }
    .mark {
      display: grid;
      width: 36px;
      height: 36px;
      place-items: center;
      border-radius: 14px;
      color: #fff;
      background: linear-gradient(135deg, var(--primary), #c995aa);
      box-shadow: 0 10px 20px rgba(220,127,154,.28);
    }
    .auth-art h1 {
      margin-top: 40px;
      font-size: clamp(36px, 5vw, 58px);
      line-height: 1.08;
    }
    .auth-art p {
      margin-top: 18px;
      line-height: 1.8;
      color: rgba(255,255,255,.9);
      font-weight: 700;
    }
    .auth-note {
      padding: 18px;
      border-radius: 24px;
      background: rgba(255,255,255,.2);
      border: 1px solid rgba(255,255,255,.28);
    }

    .auth-main { padding: clamp(26px, 5vw, 48px); }
    .tabs {
      display: inline-flex;
      gap: 6px;
      padding: 6px;
      margin-bottom: 24px;
      border-radius: 999px;
      background: #fff4f7;
      border: 1px solid var(--border);
    }
    .tab {
      min-height: 38px;
      padding: 0 16px;
      border-radius: 999px;
      background: transparent;
      color: var(--muted);
      font-weight: 900;
    }
    .tab.active {
      color: #fff;
      background: var(--primary);
      box-shadow: 0 10px 20px rgba(220,127,154,.24);
    }
    .auth-panel { display: none; }
    .auth-panel.active { display: block; }
    .auth-panel h2 { font-size: clamp(28px, 4vw, 40px); margin-bottom: 10px; }
    .auth-panel p { color: var(--muted); line-height: 1.75; margin-bottom: 22px; }
    .field { margin-bottom: 14px; }
    label {
      display: block;
      margin-bottom: 8px;
      color: var(--deep);
      font-size: 13px;
      font-weight: 900;
    }
    input, textarea {
      width: 100%;
      min-height: 48px;
      border: 1px solid var(--border);
      border-radius: 18px;
      outline: none;
      color: var(--text);
      background: rgba(255,255,255,.78);
      padding: 13px 15px;
    }
    textarea { min-height: 160px; resize: vertical; line-height: 1.7; }
    input:focus, textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 4px rgba(220,127,154,.14);
    }
    .btn {
      min-height: 48px;
      padding: 0 18px;
      border-radius: 999px;
      color: #fff;
      background: linear-gradient(135deg, var(--primary), #c58ca3);
      box-shadow: 0 12px 24px rgba(220,127,154,.25);
      font-weight: 900;
      white-space: nowrap;
    }
    .btn.light {
      color: var(--deep);
      background: #fff;
      border: 1px solid var(--border);
      box-shadow: none;
    }
    .text-btn {
      color: var(--deep);
      background: transparent;
      font-weight: 900;
    }
    .help {
      display: flex;
      justify-content: space-between;
      gap: 12px;
      flex-wrap: wrap;
      margin-top: 12px;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.6;
    }
    .msg {
      min-height: 24px;
      margin-top: 12px;
      color: var(--deep);
      font-weight: 900;
    }
    .msg.error { color: #a84d61; }

    .app {
      width: min(1160px, calc(100% - 32px));
      margin: 0 auto;
      padding: 22px 0 36px;
    }
    .navbar {
      position: sticky;
      top: 14px;
      z-index: 20;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 18px;
      padding: 14px 16px;
      border: 1px solid var(--border);
      border-radius: 26px;
      background: rgba(255,255,255,.75);
      box-shadow: 0 14px 36px rgba(176,119,134,.14);
      backdrop-filter: blur(18px);
    }
    .nav-right {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 8px;
      flex-wrap: wrap;
    }
    .nav-links { display: flex; flex-wrap: wrap; gap: 8px; }
    .nav-link {
      display: inline-flex;
      align-items: center;
      min-height: 38px;
      padding: 0 14px;
      border-radius: 999px;
      color: var(--muted);
      text-decoration: none;
      font-size: 14px;
      font-weight: 800;
    }
    .nav-link.active, .nav-link:hover {
      color: #fff;
      background: var(--primary);
    }

    .hero {
      display: grid;
      grid-template-columns: 1.1fr .9fr;
      gap: 28px;
      margin: 34px 0 20px;
    }
    .card, .panel {
      border: 1px solid var(--border);
      border-radius: 32px;
      background: var(--card);
      box-shadow: var(--shadow);
      backdrop-filter: blur(14px);
    }
    .card { padding: clamp(26px, 5vw, 48px); }
    .eyebrow { color: var(--deep); font-weight: 900; margin-bottom: 14px; }
    h1 { font-size: clamp(38px, 6vw, 68px); line-height: 1.06; margin-bottom: 18px; }
    .copy { color: var(--muted); font-size: 17px; line-height: 1.85; }
    .stats {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 14px;
      margin-top: 26px;
    }
    .stat {
      min-height: 104px;
      padding: 18px;
      border-radius: 24px;
      background: rgba(255,255,255,.64);
      border: 1px solid var(--border);
    }
    .stat strong { display: block; font-size: 28px; color: var(--deep); margin-bottom: 6px; }
    .stat span { color: var(--muted); font-size: 14px; font-weight: 700; }

    .visual {
      position: relative;
      overflow: hidden;
      min-height: 360px;
      border-radius: 32px;
      background: linear-gradient(135deg, #f5cdd8, #dce8d6 54%, #f8e6bc);
      box-shadow: var(--shadow);
    }
    .sun {
      position: absolute;
      width: 132px;
      height: 132px;
      right: 34px;
      top: 34px;
      border-radius: 999px;
      background: #fff4bd;
      box-shadow: 0 0 58px rgba(255,230,140,.76);
    }
    .book {
      position: absolute;
      left: 50%;
      top: 52%;
      width: 210px;
      height: 260px;
      padding: 30px 28px;
      border-radius: 26px;
      background: #fffaf6;
      box-shadow: 0 24px 46px rgba(97,69,78,.2);
      transform: translate(-50%, -50%) rotate(-5deg);
    }
    .line {
      height: 10px;
      margin-bottom: 18px;
      border-radius: 999px;
      background: #e9dadd;
    }
    .line:nth-child(1) { width: 72%; background: #dd8ba0; }
    .line:nth-child(2) { width: 90%; }
    .line:nth-child(3) { width: 78%; }
    .line:nth-child(4) { width: 64%; background: #a8c3a8; }
    .hill {
      position: absolute;
      bottom: -14%;
      left: -12%;
      width: 124%;
      height: 42%;
      border-radius: 60% 60% 0 0;
      background: var(--green);
    }

    .view { display: none; margin-top: 22px; }
    .view.active { display: block; }
    .panel { padding: clamp(20px, 4vw, 34px); }
    .panel-head {
      display: flex;
      justify-content: space-between;
      gap: 14px;
      margin-bottom: 24px;
      align-items: flex-start;
    }
    .panel h2 { font-size: clamp(26px, 4vw, 38px); margin-bottom: 8px; }
    .panel p { color: var(--muted); line-height: 1.7; }

    .form-grid {
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 12px;
      margin-bottom: 18px;
    }
    .weight-grid {
      display: grid;
      grid-template-columns: 170px 1fr auto;
      gap: 12px;
      margin-bottom: 18px;
    }
    .weight-grid textarea { grid-column: 1 / -1; }

    .todo-list, .record-list { display: grid; gap: 12px; }
    .todo-item, .record-item {
      display: grid;
      grid-template-columns: auto 1fr auto;
      gap: 12px;
      align-items: center;
      padding: 14px;
      border: 1px solid var(--border);
      border-radius: 22px;
      background: rgba(255,255,255,.62);
    }
    .check {
      display: grid;
      width: 30px;
      height: 30px;
      place-items: center;
      border-radius: 999px;
      border: 2px solid #d6adb9;
      background: transparent;
      color: #fff;
      font-weight: 900;
    }
    .todo-item.done .check { background: var(--primary); border-color: var(--primary); }
    .todo-item.done .todo-text { color: var(--muted); text-decoration: line-through; }
    .danger {
      padding: 9px 12px;
      border-radius: 999px;
      color: #9e5366;
      background: #fff0f4;
      font-size: 13px;
      font-weight: 900;
    }
    .record-item { grid-template-columns: 1fr auto; }
    .record-item strong { display: block; color: var(--deep); margin-bottom: 5px; }
    .empty {
      padding: 26px;
      border: 1px dashed var(--border);
      border-radius: 22px;
      color: var(--muted);
      background: rgba(255,255,255,.46);
      text-align: center;
    }

    .photo-layout {
      display: grid;
      grid-template-columns: .9fr 1.1fr;
      gap: 20px;
    }
    .photo-box {
      min-height: 330px;
      border: 1px dashed rgba(189,99,125,.5);
      border-radius: 28px;
      overflow: hidden;
      background: rgba(255,255,255,.5);
    }
    .photo-preview {
      width: 100%;
      height: 100%;
      min-height: 330px;
      display: none;
      object-fit: cover;
    }
    .photo-empty {
      display: grid;
      min-height: 330px;
      place-items: center;
      padding: 28px;
      color: var(--muted);
      text-align: center;
      font-weight: 800;
    }
    .photo-side {
      padding: 24px;
      border-radius: 28px;
      background: rgba(255,255,255,.58);
      border: 1px solid var(--border);
    }
    .photo-side h3 { font-size: 25px; margin-bottom: 10px; }
    .photo-actions, .diary-actions {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      justify-content: space-between;
      margin-top: 14px;
    }
    .hidden-file { display: none; }
    .save-note { color: var(--deep); font-weight: 900; }

    footer {
      padding: 28px 0 10px;
      color: var(--muted);
      text-align: center;
      font-size: 14px;
    }

    @media (max-width: 860px) {
      .auth-card, .hero, .photo-layout { grid-template-columns: 1fr; }
      .auth-art { min-height: 320px; }
      .navbar { align-items: flex-start; flex-direction: column; }
      .stats, .form-grid, .weight-grid { grid-template-columns: 1fr; }
      .panel-head { flex-direction: column; }
    }
  </style>
</head>

<body>
  <section class="auth-screen">
    <div class="auth-card">
      <div class="auth-art">
        <div>
          <div class="logo"><span class="mark">今</span><span>今日成长记录</span></div>
          <h1>先登录，再记录今天</h1>
          <p>用电话和密码进入你的个人成长空间。当前版本为本地登录体验，数据保存在浏览器里。</p>
        </div>
        <div class="auth-note">支持：电话登录、创建账号、忘记密码用电话找回。</div>
      </div>

      <div class="auth-main">
        <div class="tabs">
          <button class="tab active" data-tab="login">登录</button>
          <button class="tab" data-tab="reset">忘记密码</button>
        </div>

        <div class="auth-panel active" id="loginPanel">
          <h2>欢迎回来</h2>
          <p>新手机号会自动创建账号。</p>
          <form id="loginForm">
            <div class="field">
              <label for="loginPhone">电话</label>
              <input id="loginPhone" type="tel" placeholder="请输入手机号" />
            </div>
            <div class="field">
              <label for="loginPassword">密码</label>
              <input id="loginPassword" type="password" placeholder="请输入密码" />
            </div>
            <button class="btn" type="submit">登录 / 创建账号</button>
          </form>
          <div class="help">
            <span>密码至少 4 位。</span>
            <button class="text-btn" id="toResetBtn">忘记密码？用电话找回</button>
          </div>
          <div class="msg" id="loginMsg"></div>
        </div>

        <div class="auth-panel" id="resetPanel">
          <h2>用电话找回密码</h2>
          <p>输入已注册电话和新密码。</p>
          <form id="resetForm">
            <div class="field">
              <label for="resetPhone">电话</label>
              <input id="resetPhone" type="tel" placeholder="请输入已注册手机号" />
            </div>
            <div class="field">
              <label for="resetPassword">新密码</label>
              <input id="resetPassword" type="password" placeholder="至少 4 位" />
            </div>
            <button class="btn" type="submit">重设密码</button>
          </form>
          <div class="help">
            <span>电话不存在时，请先创建账号。</span>
            <button class="text-btn" id="toLoginBtn">返回登录</button>
          </div>
          <div class="msg" id="resetMsg"></div>
        </div>
      </div>
    </div>
  </section>

  <div class="app">
    <nav class="navbar">
      <div class="logo"><span class="mark">今</span><span>今日成长记录</span></div>
      <div class="nav-right">
        <div class="nav-links">
          <a class="nav-link" href="#home" data-route="home">首页</a>
          <a class="nav-link" href="#todo" data-route="todo">每日 Todo</a>
          <a class="nav-link" href="#weight" data-route="weight">体重记录</a>
          <a class="nav-link" href="#diary" data-route="diary">每日日记</a>
          <a class="nav-link" href="#photo" data-route="photo">今日照片</a>
        </div>
        <button class="btn light" id="logoutBtn">退出登录</button>
      </div>
    </nav>

    <header class="hero">
      <section class="card">
        <div class="eyebrow" id="todayLabel">今天</div>
        <h1>把生活里的小进步，都温柔地存下来</h1>
        <p class="copy">记录任务、体重、日记和照片。点击导航可以跳转到不同功能页。</p>
        <div class="stats">
          <div class="stat"><strong id="todoStat">0/0</strong><span>Todo 完成</span></div>
          <div class="stat"><strong id="weightStat">未记录</strong><span>最近体重</span></div>
          <div class="stat"><strong id="diaryStat">0 字</strong><span>今日日记</span></div>
          <div class="stat"><strong id="photoStat">未上传</strong><span>今日照片</span></div>
        </div>
      </section>

      <section class="visual">
        <div class="sun"></div>
        <div class="book">
          <div class="line"></div><div class="line"></div><div class="line"></div><div class="line"></div>
        </div>
        <div class="hill"></div>
      </section>
    </header>

    <main>
      <section class="view active" id="view-home">
        <div class="panel">
          <div class="panel-head">
            <div>
              <h2>今天从哪里开始？</h2>
              <p>选择一个入口，进入对应页面开始记录。</p>
            </div>
          </div>
          <div class="stats">
            <button class="btn" data-go="todo">去写 Todo</button>
            <button class="btn" data-go="weight">记录体重</button>
            <button class="btn" data-go="diary">写日记</button>
            <button class="btn" data-go="photo">上传照片</button>
          </div>
        </div>
      </section>

      <section class="view" id="view-todo">
        <div class="panel">
          <div class="panel-head">
            <div>
              <h2>每日 Todo</h2>
              <p>添加、完成、删除今天的任务。</p>
            </div>
            <button class="btn light" id="clearDoneBtn">清除已完成</button>
          </div>
          <form class="form-grid" id="todoForm">
            <input id="todoInput" placeholder="例如：散步 20 分钟" />
            <button class="btn" type="submit">添加任务</button>
          </form>
          <div class="todo-list" id="todoList"></div>
        </div>
      </section>

      <section class="view" id="view-weight">
        <div class="panel">
          <div class="panel-head">
            <div>
              <h2>体重记录</h2>
              <p>记录日期、体重和备注。</p>
            </div>
          </div>
          <form class="weight-grid" id="weightForm">
            <input id="weightDate" type="date" />
            <input id="weightInput" type="number" step="0.1" min="1" placeholder="体重 kg" />
            <button class="btn" type="submit">保存记录</button>
            <textarea id="weightNote" placeholder="备注：睡眠、饮食、运动、心情"></textarea>
          </form>
          <div class="record-list" id="weightList"></div>
        </div>
      </section>

      <section class="view" id="view-diary">
        <div class="panel">
          <div class="panel-head">
            <div>
              <h2>每日日记</h2>
              <p>写下今天发生的事、心情或一句想留给自己的话。</p>
            </div>
          </div>
          <textarea id="diaryInput" placeholder="今天我想记录……"></textarea>
          <div class="diary-actions">
            <span class="save-note" id="diaryStatus"></span>
            <button class="btn" id="saveDiaryBtn">保存日记</button>
          </div>
        </div>
      </section>

      <section class="view" id="view-photo">
        <div class="panel">
          <div class="panel-head">
            <div>
              <h2>今日照片</h2>
              <p>上传一张今天的照片。</p>
            </div>
          </div>
          <div class="photo-layout">
            <div class="photo-box">
              <img class="photo-preview" id="photoPreview" alt="今日照片" />
              <div class="photo-empty" id="photoEmpty">还没有照片。点击右侧按钮上传。</div>
            </div>
            <div class="photo-side">
              <h3>保存今天的一帧</h3>
              <p>照片会保存在当前浏览器本地。</p>
              <input class="hidden-file" id="photoInput" type="file" accept="image/*" />
              <div class="photo-actions">
                <button class="btn" id="pickPhotoBtn">选择照片</button>
                <button class="btn light" id="removePhotoBtn">移除照片</button>
              </div>
              <span class="save-note" id="photoStatus"></span>
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer>© 2026 今日成长记录。内容保存在当前浏览器本地。</footer>
  </div>

  <script>
    const AUTH_USERS_KEY = "growth-users-v1";
    const AUTH_SESSION_KEY = "growth-session-v1";
    const DATA_PREFIX = "growth-data-v1:";
    const today = new Date();
    const todayKey = dateKey(today);

    const defaultData = { todos: [], weights: [], diaries: {}, photos: {} };
    let currentPhone = localStorage.getItem(AUTH_SESSION_KEY) || "";
    let data = loadData();

    const $ = (id) => document.getElementById(id);

    const el = {
      tabs: document.querySelectorAll(".tab"),
      loginPanel: $("loginPanel"),
      resetPanel: $("resetPanel"),
      loginForm: $("loginForm"),
      loginPhone: $("loginPhone"),
      loginPassword: $("loginPassword"),
      loginMsg: $("loginMsg"),
      resetForm: $("resetForm"),
      resetPhone: $("resetPhone"),
      resetPassword: $("resetPassword"),
      resetMsg: $("resetMsg"),
      toResetBtn: $("toResetBtn"),
      toLoginBtn: $("toLoginBtn"),
      logoutBtn: $("logoutBtn"),
      navLinks: document.querySelectorAll(".nav-link"),
      views: document.querySelectorAll(".view"),
      goButtons: document.querySelectorAll("[data-go]"),
      todayLabel: $("todayLabel"),
      todoForm: $("todoForm"),
      todoInput: $("todoInput"),
      todoList: $("todoList"),
      clearDoneBtn: $("clearDoneBtn"),
      weightForm: $("weightForm"),
      weightDate: $("weightDate"),
      weightInput: $("weightInput"),
      weightNote: $("weightNote"),
      weightList: $("weightList"),
      diaryInput: $("diaryInput"),
      diaryStatus: $("diaryStatus"),
      saveDiaryBtn: $("saveDiaryBtn"),
      photoInput: $("photoInput"),
      pickPhotoBtn: $("pickPhotoBtn"),
      removePhotoBtn: $("removePhotoBtn"),
      photoPreview: $("photoPreview"),
      photoEmpty: $("photoEmpty"),
      photoStatus: $("photoStatus"),
      todoStat: $("todoStat"),
      weightStat: $("weightStat"),
      diaryStat: $("diaryStat"),
      photoStat: $("photoStat")
    };

    el.todayLabel.textContent = new Intl.DateTimeFormat("zh-CN", {
      month: "long", day: "numeric", weekday: "long"
    }).format(today);

    el.weightDate.value = todayKey;
    el.diaryInput.value = data.diaries[todayKey] || "";

    updateLoginState();
    renderRoute();
    renderAll();

    el.tabs.forEach(tab => {
      tab.addEventListener("click", () => showAuth(tab.dataset.tab));
    });

    el.toResetBtn.addEventListener("click", () => {
      el.resetPhone.value = el.loginPhone.value;
      showAuth("reset");
    });

    el.toLoginBtn.addEventListener("click", () => showAuth("login"));

    el.loginForm.addEventListener("submit", (e) => {
      e.preventDefault();
      const phone = cleanPhone(el.loginPhone.value);
      const password = el.loginPassword.value;

      if (!validPhone(phone)) return message(el.loginMsg, "请输入正确电话。", true);
      if (password.length < 4) return message(el.loginMsg, "密码至少 4 位。", true);

      const users = loadUsers();

      if (users[phone] && users[phone].password !== password) {
        return message(el.loginMsg, "密码不正确，可以用电话找回。", true);
      }

      if (!users[phone]) {
        users[phone] = { phone, password, createdAt: new Date().toISOString() };
        saveUsers(users);
      }

      currentPhone = phone;
      localStorage.setItem(AUTH_SESSION_KEY, phone);
      data = loadData();
      el.diaryInput.value = data.diaries[todayKey] || "";
      message(el.loginMsg, "登录成功。");
      updateLoginState();
      renderAll();
    });

    el.resetForm.addEventListener("submit", (e) => {
      e.preventDefault();
      const phone = cleanPhone(el.resetPhone.value);
      const password = el.resetPassword.value;
      const users = loadUsers();

      if (!validPhone(phone)) return message(el.resetMsg, "请输入正确电话。", true);
      if (!users[phone]) return message(el.resetMsg, "这个电话还没有注册。", true);
      if (password.length < 4) return message(el.resetMsg, "新密码至少 4 位。", true);

      users[phone].password = password;
      users[phone].updatedAt = new Date().toISOString();
      saveUsers(users);

      currentPhone = phone;
      localStorage.setItem(AUTH_SESSION_KEY, phone);
      data = loadData();
      message(el.resetMsg, "密码已重设，已登录。");
      updateLoginState();
      renderAll();
    });

    el.logoutBtn.addEventListener("click", () => {
      localStorage.removeItem(AUTH_SESSION_KEY);
      currentPhone = "";
      updateLoginState();
      showAuth("login");
    });

    window.addEventListener("hashchange", renderRoute);

    el.goButtons.forEach(btn => {
      btn.addEventListener("click", () => location.hash = btn.dataset.go);
    });

    el.todoForm.addEventListener("submit", (e) => {
      e.preventDefault();
      const title = el.todoInput.value.trim();
      if (!title) return el.todoInput.focus();

      data.todos.unshift({
        id: id(),
        title,
        done: false,
        date: todayKey,
        createdAt: new Date().toISOString()
      });

      el.todoInput.value = "";
      saveAndRender();
    });

    el.todoList.addEventListener("click", (e) => {
      const action = e.target.dataset.action;
      const itemId = e.target.dataset.id;
      if (!action || !itemId) return;

      if (action === "toggle") {
        data.todos = data.todos.map(t => t.id === itemId ? { ...t, done: !t.done } : t);
      }
      if (action === "delete") {
        data.todos = data.todos.filter(t => t.id !== itemId);
      }
      saveAndRender();
    });

    el.clearDoneBtn.addEventListener("click", () => {
      data.todos = data.todos.filter(t => !t.done);
      saveAndRender();
    });

    el.weightForm.addEventListener("submit", (e) => {
      e.preventDefault();
      const weight = Number(el.weightInput.value);
      if (!weight || weight <= 0) return el.weightInput.focus();

      data.weights.unshift({
        id: id(),
        date: el.weightDate.value || todayKey,
        weight,
        note: el.weightNote.value.trim(),
        createdAt: new Date().toISOString()
      });

      el.weightInput.value = "";
      el.weightNote.value = "";
      saveAndRender();
    });

    el.weightList.addEventListener("click", (e) => {
      const itemId = e.target.dataset.id;
      if (!itemId) return;
      data.weights = data.weights.filter(w => w.id !== itemId);
      saveAndRender();
    });

    el.saveDiaryBtn.addEventListener("click", () => {
      data.diaries[todayKey] = el.diaryInput.value;
      el.diaryStatus.textContent = "日记已保存";
      saveAndRender();
      setTimeout(() => el.diaryStatus.textContent = "", 1600);
    });

    el.diaryInput.addEventListener("input", () => {
      el.diaryStatus.textContent = "有未保存内容";
      renderStats();
    });

    el.pickPhotoBtn.addEventListener("click", () => el.photoInput.click());

    el.photoInput.addEventListener("change", () => {
      const file = el.photoInput.files && el.photoInput.files[0];
      if (!file) return;

      const reader = new FileReader();
      reader.onload = () => {
        data.photos[todayKey] = reader.result;
        el.photoStatus.textContent = "照片已保存";
        saveAndRender();
      };
      reader.readAsDataURL(file);
    });

    el.removePhotoBtn.addEventListener("click", () => {
      delete data.photos[todayKey];
      el.photoInput.value = "";
      el.photoStatus.textContent = "照片已移除";
      saveAndRender();
    });

    function showAuth(name) {
      const isReset = name === "reset";
      el.loginPanel.classList.toggle("active", !isReset);
      el.resetPanel.classList.toggle("active", isReset);
      el.tabs.forEach(t => t.classList.toggle("active", t.dataset.tab === name));
      el.loginMsg.textContent = "";
      el.resetMsg.textContent = "";
    }

    function updateLoginState() {
      document.body.classList.toggle("logged-in", Boolean(currentPhone));
    }

    function renderRoute() {
      const route = (location.hash || "#home").replace("#", "");
      const safe = ["home", "todo", "weight", "diary", "photo"].includes(route) ? route : "home";

      el.views.forEach(v => v.classList.toggle("active", v.id === "view-" + safe));
      el.navLinks.forEach(a => a.classList.toggle("active", a.dataset.route === safe));
    }

    function renderAll() {
      renderTodos();
      renderWeights();
      renderPhoto();
      renderStats();
    }

    function renderTodos() {
      if (!data.todos.length) {
        el.todoList.innerHTML = '<div class="empty">今天还没有任务。添加一个小目标，轻轻开始。</div>';
        return;
      }

      el.todoList.innerHTML = data.todos.map(t => `
        <div class="todo-item ${t.done ? "done" : ""}">
          <button class="check" data-action="toggle" data-id="${t.id}">${t.done ? "✓" : ""}</button>
          <div class="todo-text">${escapeHtml(t.title)}</div>
          <button class="danger" data-action="delete" data-id="${t.id}">删除</button>
        </div>
      `).join("");
    }

    function renderWeights() {
      if (!data.weights.length) {
        el.weightList.innerHTML = '<div class="empty">还没有体重记录。保存第一条后会显示在这里。</div>';
        return;
      }

      el.weightList.innerHTML = data.weights.map(w => `
        <div class="record-item">
          <div>
            <strong>${escapeHtml(w.date)} · ${w.weight} kg</strong>
            <p>${w.note ? escapeHtml(w.note) : "没有备注"}</p>
          </div>
          <button class="danger" data-id="${w.id}">删除</button>
        </div>
      `).join("");
    }

    function renderPhoto() {
      const photo = data.photos[todayKey];
      if (photo) {
        el.photoPreview.src = photo;
        el.photoPreview.style.display = "block";
        el.photoEmpty.style.display = "none";
      } else {
        el.photoPreview.removeAttribute("src");
        el.photoPreview.style.display = "none";
        el.photoEmpty.style.display = "grid";
      }
    }

    function renderStats() {
      const done = data.todos.filter(t => t.done).length;
      el.todoStat.textContent = done + "/" + data.todos.length;
      el.weightStat.textContent = data.weights[0] ? data.weights[0].weight + " kg" : "未记录";
      el.diaryStat.textContent = (data.diaries[todayKey] || el.diaryInput.value || "").length + " 字";
      el.photoStat.textContent = data.photos[todayKey] ? "已上传" : "未上传";
    }

    function saveAndRender() {
      if (!currentPhone) return;
      localStorage.setItem(DATA_PREFIX + currentPhone, JSON.stringify(data));
      renderAll();
    }

    function loadData() {
      if (!currentPhone) return { ...defaultData, todos: [], weights: [], diaries: {}, photos: {} };
      try {
        const raw = localStorage.getItem(DATA_PREFIX + currentPhone);
        return raw ? { ...defaultData, ...JSON.parse(raw) } : { ...defaultData, todos: [], weights: [], diaries: {}, photos: {} };
      } catch {
        return { ...defaultData, todos: [], weights: [], diaries: {}, photos: {} };
      }
    }

    function loadUsers() {
      try {
        return JSON.parse(localStorage.getItem(AUTH_USERS_KEY) || "{}");
      } catch {
        return {};
      }
    }

    function saveUsers(users) {
      localStorage.setItem(AUTH_USERS_KEY, JSON.stringify(users));
    }

    function message(node, text, isError = false) {
      node.textContent = text;
      node.classList.toggle("error", isError);
    }

    function cleanPhone(value) {
      return value.trim().replace(/\s+/g, "");
    }

    function validPhone(phone) {
      return /^(\+?\d{7,15})$/.test(phone);
    }

    function dateKey(date) {
      const y = date.getFullYear();
      const m = String(date.getMonth() + 1).padStart(2, "0");
      const d = String(date.getDate()).padStart(2, "0");
      return `${y}-${m}-${d}`;
    }

    function id() {
      return Date.now().toString(36) + Math.random().toString(36).slice(2, 8);
    }

    function escapeHtml(value) {
      return String(value)
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;")
        .replaceAll('"', "&quot;")
        .replaceAll("'", "&#039;");
    }
  </script>
</body>
</html>
    
