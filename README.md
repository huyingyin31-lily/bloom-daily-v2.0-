<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>今日成长记录</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #fff7f8;
      --bg-2: #f3ece7;
      --card: rgba(255, 255, 255, 0.82);
      --text: #44343a;
      --muted: #8a737b;
      --primary: #dc7f9a;
      --primary-deep: #bd637d;
      --green: #8fb79b;
      --border: rgba(219, 178, 190, 0.46);
      --shadow: 0 20px 55px rgba(169, 116, 130, 0.18);
    }

    body {
      min-height: 100vh;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC",
        "Microsoft YaHei", sans-serif;
      color: var(--text);
      background:
        radial-gradient(circle at 12% 8%, #ffe2eb 0 18%, transparent 34%),
        radial-gradient(circle at 88% 18%, #dcecdf 0 16%, transparent 33%),
        linear-gradient(135deg, var(--bg), var(--bg-2));
    }

    button, input, textarea { font: inherit; }
    button { cursor: pointer; border: 0; }

    .app-shell {
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
      background: rgba(255, 255, 255, 0.75);
      box-shadow: 0 14px 36px rgba(176, 119, 134, 0.14);
      backdrop-filter: blur(18px);
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      min-width: max-content;
      font-weight: 900;
      color: var(--primary-deep);
    }

    .brand-mark {
      display: grid;
      width: 34px;
      height: 34px;
      place-items: center;
      border-radius: 14px;
      color: white;
      background: linear-gradient(135deg, var(--primary), #c995aa);
      box-shadow: 0 10px 20px rgba(220, 127, 154, 0.28);
    }

    .nav-links {
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-end;
      gap: 8px;
    }

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
      transition: 0.18s ease;
    }

    .nav-link:hover,
    .nav-link.active {
      color: #fff;
      background: var(--primary);
      box-shadow: 0 10px 18px rgba(220, 127, 154, 0.22);
      transform: translateY(-1px);
    }

    .hero {
      display: grid;
      grid-template-columns: 1.1fr 0.9fr;
      gap: 28px;
      align-items: stretch;
      margin: 34px 0 20px;
    }

    .hero-card,
    .panel {
      border: 1px solid var(--border);
      border-radius: 32px;
      background: var(--card);
      box-shadow: var(--shadow);
      backdrop-filter: blur(14px);
    }

    .hero-card { padding: clamp(26px, 5vw, 48px); }

    .eyebrow {
      color: var(--primary-deep);
      font-size: 14px;
      font-weight: 900;
      margin-bottom: 14px;
    }

    h1 {
      max-width: 720px;
      font-size: clamp(38px, 6vw, 68px);
      line-height: 1.06;
      margin-bottom: 18px;
    }

    .hero-copy {
      max-width: 650px;
      color: var(--muted);
      font-size: 17px;
      line-height: 1.85;
    }

    .quick-stats {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 14px;
      margin-top: 26px;
    }

    .stat {
      min-height: 104px;
      padding: 18px;
      border-radius: 24px;
      background: rgba(255, 255, 255, 0.64);
      border: 1px solid var(--border);
    }

    .stat[data-go] {
      cursor: pointer;
      text-align: left;
      transition: 0.18s ease;
    }

    .stat[data-go]:hover {
      border-color: var(--primary);
      box-shadow: 0 14px 28px rgba(220, 127, 154, 0.16);
      transform: translateY(-2px);
    }

    .stat strong {
      display: block;
      font-size: 28px;
      color: var(--primary-deep);
      margin-bottom: 6px;
    }

    .stat span {
      color: var(--muted);
      font-size: 14px;
      font-weight: 700;
    }

    .visual-card {
      position: relative;
      overflow: hidden;
      min-height: 360px;
      border-radius: 32px;
      background:
        linear-gradient(145deg, rgba(255, 255, 255, 0.3), transparent 46%),
        linear-gradient(135deg, #f5cdd8, #dce8d6 54%, #f8e6bc);
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
      box-shadow: 0 0 58px rgba(255, 230, 140, 0.76);
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
      box-shadow: 0 24px 46px rgba(97, 69, 78, 0.2);
      transform: translate(-50%, -50%) rotate(-5deg);
    }

    .book::before {
      content: "";
      position: absolute;
      left: 30px;
      top: 0;
      width: 20px;
      height: 100%;
      background: #efbdca;
    }

    .book-line {
      height: 10px;
      margin-bottom: 18px;
      border-radius: 999px;
      background: #e9dadd;
    }

    .book-line:nth-child(1) { width: 72%; background: #dd8ba0; }
    .book-line:nth-child(2) { width: 90%; }
    .book-line:nth-child(3) { width: 78%; }
    .book-line:nth-child(4) { width: 64%; background: #a8c3a8; }

    .hill {
      position: absolute;
      bottom: -14%;
      left: -12%;
      width: 124%;
      height: 42%;
      border-radius: 60% 60% 0 0;
      background: var(--green);
    }

    .hill.second {
      left: 18%;
      bottom: -20%;
      background: #719c7d;
    }

    .view {
      display: none;
      margin-top: 22px;
      animation: fadeIn 0.22s ease;
    }

    .view.active { display: block; }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .panel { padding: clamp(20px, 4vw, 34px); }

    .entry-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 14px;
      margin-top: 20px;
    }

    .entry-card {
      min-height: 148px;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: space-between;
      gap: 16px;
      padding: 20px;
      border: 1px solid var(--border);
      border-radius: 24px;
      color: var(--text);
      background: rgba(255, 255, 255, 0.68);
      box-shadow: 0 12px 26px rgba(169, 116, 130, 0.1);
      text-align: left;
      transition: 0.18s ease;
    }

    .entry-card:hover {
      border-color: var(--primary);
      box-shadow: 0 18px 34px rgba(220, 127, 154, 0.18);
      transform: translateY(-3px);
    }

    .entry-card:active { transform: scale(0.98); }

    .entry-card strong {
      color: var(--primary-deep);
      font-size: 19px;
    }

    .entry-card span {
      color: var(--muted);
      line-height: 1.6;
      font-size: 14px;
      font-weight: 700;
    }

    .panel-header {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 14px;
      margin-bottom: 24px;
    }

    .panel-title h2 {
      font-size: clamp(26px, 4vw, 38px);
      line-height: 1.12;
      margin-bottom: 8px;
    }

    .panel-title p {
      color: var(--muted);
      line-height: 1.7;
    }

    .form-grid {
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 12px;
      align-items: start;
      margin-bottom: 18px;
    }

    .weight-grid {
      display: grid;
      grid-template-columns: 170px 1fr auto;
      gap: 12px;
      align-items: start;
      margin-bottom: 18px;
    }

    .weight-grid textarea { grid-column: 1 / -1; }

    input,
    textarea {
      width: 100%;
      min-height: 48px;
      border: 1px solid var(--border);
      border-radius: 18px;
      outline: none;
      color: var(--text);
      background: rgba(255, 255, 255, 0.78);
      padding: 13px 15px;
      transition: 0.18s ease;
    }

    textarea {
      min-height: 170px;
      resize: vertical;
      line-height: 1.7;
    }

    input:focus,
    textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 4px rgba(220, 127, 154, 0.14);
    }

    .btn {
      min-height: 48px;
      padding: 0 18px;
      border-radius: 999px;
      color: #fff;
      background: linear-gradient(135deg, var(--primary), #c58ca3);
      box-shadow: 0 12px 24px rgba(220, 127, 154, 0.25);
      font-weight: 900;
      transition: 0.18s ease;
      white-space: nowrap;
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 16px 30px rgba(220, 127, 154, 0.3);
    }

    .btn:active { transform: scale(0.97); }

    .btn.light {
      color: var(--primary-deep);
      background: #fff;
      border: 1px solid var(--border);
      box-shadow: none;
    }

    .todo-list,
    .record-list {
      display: grid;
      gap: 12px;
    }

    .todo-item,
    .record-item {
      display: grid;
      grid-template-columns: auto 1fr auto;
      gap: 12px;
      align-items: center;
      padding: 14px;
      border: 1px solid var(--border);
      border-radius: 22px;
      background: rgba(255, 255, 255, 0.62);
    }

    .check {
      display: grid;
      width: 30px;
      height: 30px;
      place-items: center;
      border-radius: 999px;
      border: 2px solid #d6adb9;
      background: transparent;
      color: white;
      font-weight: 900;
    }

    .todo-item.done .check {
      border-color: var(--primary);
      background: var(--primary);
    }

    .todo-item.done .todo-text {
      color: var(--muted);
      text-decoration: line-through;
    }

    .todo-text {
      line-height: 1.5;
      overflow-wrap: anywhere;
    }

    .danger {
      padding: 9px 12px;
      border-radius: 999px;
      color: #9e5366;
      background: #fff0f4;
      font-size: 13px;
      font-weight: 900;
    }

    .record-item { grid-template-columns: 1fr auto; }

    .record-item strong {
      display: block;
      margin-bottom: 5px;
      color: var(--primary-deep);
    }

    .record-item p {
      color: var(--muted);
      line-height: 1.6;
      overflow-wrap: anywhere;
    }

    .diary-actions,
    .photo-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      align-items: center;
      justify-content: space-between;
      margin-top: 14px;
    }

    .save-note {
      color: var(--primary-deep);
      font-weight: 800;
      min-height: 22px;
    }

    .photo-layout {
      display: grid;
      grid-template-columns: 0.9fr 1.1fr;
      gap: 20px;
      align-items: stretch;
    }

    .photo-box {
      min-height: 330px;
      border: 1px dashed rgba(189, 99, 125, 0.5);
      border-radius: 28px;
      overflow: hidden;
      background:
        linear-gradient(135deg, rgba(255, 255, 255, 0.64), rgba(255, 240, 245, 0.7)),
        repeating-linear-gradient(45deg, transparent, transparent 12px, rgba(220, 127, 154, 0.07) 12px, rgba(220, 127, 154, 0.07) 24px);
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
      line-height: 1.7;
      font-weight: 800;
    }

    .photo-side {
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 14px;
      padding: 24px;
      border-radius: 28px;
      background: rgba(255, 255, 255, 0.58);
      border: 1px solid var(--border);
    }

    .photo-side h3 { font-size: 25px; }

    .photo-side p {
      color: var(--muted);
      line-height: 1.75;
    }

    .hidden-file { display: none; }

    .empty {
      padding: 26px;
      border: 1px dashed var(--border);
      border-radius: 22px;
      color: var(--muted);
      background: rgba(255, 255, 255, 0.46);
      text-align: center;
      line-height: 1.7;
    }

    footer {
      padding: 28px 0 10px;
      color: var(--muted);
      text-align: center;
      font-size: 14px;
    }

    @media (max-width: 860px) {
      .navbar {
        align-items: flex-start;
        flex-direction: column;
      }

      .nav-links { justify-content: flex-start; }

      .hero,
      .photo-layout {
        grid-template-columns: 1fr;
      }

      .visual-card { min-height: 330px; }

      .quick-stats,
      .entry-grid,
      .weight-grid,
      .form-grid {
        grid-template-columns: 1fr;
      }

      .panel-header { flex-direction: column; }
    }

    @media (max-width: 520px) {
      .app-shell {
        width: min(100% - 20px, 1160px);
        padding-top: 10px;
      }

      .navbar,
      .panel,
      .hero-card,
      .visual-card {
        border-radius: 24px;
      }

      .nav-link {
        min-height: 34px;
        padding: 0 11px;
        font-size: 13px;
      }

      .todo-item,
      .record-item {
        grid-template-columns: auto 1fr;
      }

      .danger {
        grid-column: 2;
        justify-self: start;
      }
    }
  </style>
</head>
<body>
  <div class="app-shell">
    <nav class="navbar">
      <div class="brand">
        <span class="brand-mark">今</span>
        <span>今日成长记录</span>
      </div>
      <div class="nav-links" aria-label="页面导航">
        <a class="nav-link" href="#home" data-route="home">首页</a>
        <a class="nav-link" href="#todo" data-route="todo">每日 Todo</a>
        <a class="nav-link" href="#weight" data-route="weight">体重记录</a>
        <a class="nav-link" href="#diary" data-route="diary">每日日记</a>
        <a class="nav-link" href="#photo" data-route="photo">今日照片</a>
      </div>
    </nav>

    <header class="hero">
      <section class="hero-card">
        <div class="eyebrow" id="todayLabel">今天</div>
        <h1>把生活里的小进步，都温柔地存下来</h1>
        <p class="hero-copy">
          这里是一个可以直接使用的个人成长记录网页。点击导航可以跳转到不同功能：
          记录任务、体重、日记和照片。所有内容都会保存在当前浏览器里。
        </p>
        <div class="quick-stats">
          <button class="stat" data-go="todo" type="button">
            <strong id="todoStat">0/0</strong>
            <span>今日 Todo 完成</span>
          </button>
          <button class="stat" data-go="weight" type="button">
            <strong id="weightStat">未记录</strong>
            <span>最近体重</span>
          </button>
          <button class="stat" data-go="diary" type="button">
            <strong id="diaryStat">0 字</strong>
            <span>今日日记</span>
          </button>
          <button class="stat" data-go="photo" type="button">
            <strong id="photoStat">未上传</strong>
            <span>今日照片</span>
          </button>
        </div>
      </section>

      <section class="visual-card" aria-label="成长记录插画">
        <div class="sun"></div>
        <div class="book">
          <div class="book-line"></div>
          <div class="book-line"></div>
          <div class="book-line"></div>
          <div class="book-line"></div>
        </div>
        <div class="hill"></div>
        <div class="hill second"></div>
      </section>
    </header>

    <main>
      <section class="view active" id="view-home">
        <div class="panel">
          <div class="panel-header">
            <div class="panel-title">
              <h2>今天从哪里开始？</h2>
              <p>选择一个入口，进入对应页面开始记录。</p>
            </div>
          </div>
          <div class="entry-grid">
            <button class="entry-card" data-go="todo" type="button">
              <strong>每日 Todo</strong>
              <span>添加、完成、删除今天的任务。</span>
            </button>
            <button class="entry-card" data-go="weight" type="button">
              <strong>体重记录</strong>
              <span>选择日期，保存体重和备注。</span>
            </button>
            <button class="entry-card" data-go="diary" type="button">
              <strong>每日日记</strong>
              <span>写下今天的心情和片段。</span>
            </button>
            <button class="entry-card" data-go="photo" type="button">
              <strong>今日照片</strong>
              <span>上传一张当天照片并预览。</span>
            </button>
          </div>
        </div>
      </section>

      <section class="view" id="view-todo">
        <div class="panel">
          <div class="panel-header">
            <div class="panel-title">
              <h2>每日 Todo</h2>
              <p>添加今天要做的事，完成后点圆圈打勾，也可以删除不需要的任务。</p>
            </div>
            <button class="btn light" id="clearDoneBtn">清除已完成</button>
          </div>
          <form class="form-grid" id="todoForm">
            <input id="todoInput" type="text" placeholder="例如：散步 20 分钟、整理书桌、读 10 页书" autocomplete="off" />
            <button class="btn" type="submit">添加任务</button>
          </form>
          <div class="todo-list" id="todoList"></div>
        </div>
      </section>

      <section class="view" id="view-weight">
        <div class="panel">
          <div class="panel-header">
            <div class="panel-title">
              <h2>体重记录</h2>
              <p>记录日期、体重和备注，适合补记，也适合写下当天状态。</p>
            </div>
          </div>
          <form class="weight-grid" id="weightForm">
            <input id="weightDate" type="date" />
            <input id="weightInput" type="number" step="0.1" min="1" placeholder="体重 kg" />
            <button class="btn" type="submit">保存记录</button>
            <textarea id="weightNote" placeholder="备注：比如睡眠、饮食、运动、心情"></textarea>
          </form>
          <div class="record-list" id="weightList"></div>
        </div>
      </section>

      <section class="view" id="view-diary">
        <div class="panel">
          <div class="panel-header">
            <div class="panel-title">
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
          <div class="panel-header">
            <div class="panel-title">
              <h2>今日照片</h2>
              <p>上传一张今天的照片，给这一页留下一点具体的画面。</p>
            </div>
          </div>
          <div class="photo-layout">
            <div class="photo-box">
              <img class="photo-preview" id="photoPreview" alt="今日照片预览" />
              <div class="photo-empty" id="photoEmpty">还没有照片。点击右侧按钮上传一张今天的照片。</div>
            </div>
            <div class="photo-side">
              <h3>保存今天的一帧</h3>
              <p>照片会保存在当前浏览器本地。适合记录饭、天空、运动、读书，或者任何让今天变得具体的小片段。</p>
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

    <footer>© 2026 今日成长记录。内容仅保存在你的浏览器本地。</footer>
  </div>

  <script>
    const STORAGE_KEY = "gentle-growth-single-page-v2";
    const today = new Date();
    const todayKey = toDateKey(today);

    const defaultState = {
      todos: [],
      weights: [],
      diaries: {},
      photos: {}
    };

    let state = loadState();

    const els = {
      todayLabel: document.getElementById("todayLabel"),
      navLinks: document.querySelectorAll(".nav-link"),
      views: document.querySelectorAll(".view"),
      goButtons: document.querySelectorAll("[data-go]"),
      todoForm: document.getElementById("todoForm"),
      todoInput: document.getElementById("todoInput"),
      todoList: document.getElementById("todoList"),
      clearDoneBtn: document.getElementById("clearDoneBtn"),
      weightForm: document.getElementById("weightForm"),
      weightDate: document.getElementById("weightDate"),
      weightInput: document.getElementById("weightInput"),
      weightNote: document.getElementById("weightNote"),
      weightList: document.getElementById("weightList"),
      diaryInput: document.getElementById("diaryInput"),
      diaryStatus: document.getElementById("diaryStatus"),
      saveDiaryBtn: document.getElementById("saveDiaryBtn"),
      photoInput: document.getElementById("photoInput"),
      pickPhotoBtn: document.getElementById("pickPhotoBtn"),
      removePhotoBtn: document.getElementById("removePhotoBtn"),
      photoPreview: document.getElementById("photoPreview"),
      photoEmpty: document.getElementById("photoEmpty"),
      photoStatus: document.getElementById("photoStatus"),
      todoStat: document.getElementById("todoStat"),
      weightStat: document.getElementById("weightStat"),
      diaryStat: document.getElementById("diaryStat"),
      photoStat: document.getElementById("photoStat")
    };

    els.todayLabel.textContent = new Intl.DateTimeFormat("zh-CN", {
      month: "long",
      day: "numeric",
      weekday: "long"
    }).format(today);

    els.weightDate.value = todayKey;
    els.diaryInput.value = state.diaries[todayKey] || "";

    window.addEventListener("hashchange", renderRoute);

    els.goButtons.forEach((button) => {
      button.addEventListener("click", () => {
        location.hash = button.dataset.go;
        scrollToActiveView(button.dataset.go);
      });
    });

    els.todoForm.addEventListener("submit", (event) => {
      event.preventDefault();
      const title = els.todoInput.value.trim();

      if (!title) {
        pulseInput(els.todoInput);
        return;
      }

      state.todos.unshift({
        id: createId(),
        title,
        done: false,
        date: todayKey,
        createdAt: new Date().toISOString()
      });

      els.todoInput.value = "";
      saveAndRender();
    });

    els.todoList.addEventListener("click", (event) => {
      const action = event.target.dataset.action;
      const id = event.target.dataset.id;

      if (!action || !id) return;

      if (action === "toggle") {
        state.todos = state.todos.map((todo) =>
          todo.id === id ? { ...todo, done: !todo.done } : todo
        );
      }

      if (action === "delete") {
        state.todos = state.todos.filter((todo) => todo.id !== id);
      }

      saveAndRender();
    });

    els.clearDoneBtn.addEventListener("click", () => {
      state.todos = state.todos.filter((todo) => !todo.done);
      saveAndRender();
    });

    els.weightForm.addEventListener("submit", (event) => {
      event.preventDefault();
      const date = els.weightDate.value || todayKey;
      const weight = Number(els.weightInput.value);
      const note = els.weightNote.value.trim();

      if (!weight || Number.isNaN(weight) || weight <= 0) {
        pulseInput(els.weightInput);
        return;
      }

      state.weights.unshift({
        id: createId(),
        date,
        weight,
        note,
        createdAt: new Date().toISOString()
      });

      els.weightInput.value = "";
      els.weightNote.value = "";
      saveAndRender();
    });

    els.weightList.addEventListener("click", (event) => {
      const id = event.target.dataset.id;

      if (!id) return;

      state.weights = state.weights.filter((record) => record.id !== id);
      saveAndRender();
    });

    els.saveDiaryBtn.addEventListener("click", () => {
      state.diaries[todayKey] = els.diaryInput.value;
      els.diaryStatus.textContent = "日记已保存";
      saveAndRender();

      setTimeout(() => {
        els.diaryStatus.textContent = "";
      }, 1800);
    });

    els.diaryInput.addEventListener("input", () => {
      els.diaryStatus.textContent = "有未保存内容";
    });

    els.pickPhotoBtn.addEventListener("click", () => {
      els.photoInput.click();
    });

    els.photoInput.addEventListener("change", () => {
      const file = els.photoInput.files && els.photoInput.files[0];

      if (!file) return;

      const reader = new FileReader();

      reader.onload = () => {
        state.photos[todayKey] = reader.result;
        els.photoStatus.textContent = "照片已保存";
        saveAndRender();
      };

      reader.readAsDataURL(file);
    });

    els.removePhotoBtn.addEventListener("click", () => {
      delete state.photos[todayKey];
      els.photoInput.value = "";
      els.photoStatus.textContent = "照片已移除";
      saveAndRender();
    });

    renderRoute();
    renderAll();

    function renderRoute() {
      const route = (location.hash || "#home").replace("#", "");
      const safeRoute = ["home", "todo", "weight", "diary", "photo"].includes(route)
        ? route
        : "home";

      els.views.forEach((view) => {
        view.classList.toggle("active", view.id === "view-" + safeRoute);
      });

      els.navLinks.forEach((link) => {
        link.classList.toggle("active", link.dataset.route === safeRoute);
      });

      scrollToActiveView(safeRoute);
    }

    function scrollToActiveView(route) {
      const target = route === "home"
        ? document.querySelector(".hero")
        : document.getElementById("view-" + route);

      if (target) {
        setTimeout(() => {
          target.scrollIntoView({ behavior: "smooth", block: "start" });
        }, 40);
      }
    }

    function renderAll() {
      renderTodos();
      renderWeights();
      renderDiaryStats();
      renderPhoto();
      renderStats();
    }

    function renderTodos() {
      if (!state.todos.length) {
        els.todoList.innerHTML = '<div class="empty">今天还没有任务。添加一个小目标，轻轻开始。</div>';
        return;
      }

      els.todoList.innerHTML = state.todos
        .map((todo) => `
          <div class="todo-item ${todo.done ? "done" : ""}">
            <button class="check" data-action="toggle" data-id="${todo.id}" aria-label="切换完成状态">${todo.done ? "✓" : ""}</button>
            <div class="todo-text">${escapeHtml(todo.title)}</div>
            <button class="danger" data-action="delete" data-id="${todo.id}">删除</button>
          </div>
        `)
        .join("");
    }

    function renderWeights() {
      if (!state.weights.length) {
        els.weightList.innerHTML = '<div class="empty">还没有体重记录。保存第一条后会显示在这里。</div>';
        return;
      }

      els.weightList.innerHTML = state.weights
        .map((record) => `
          <div class="record-item">
            <div>
              <strong>${escapeHtml(record.date)} · ${record.weight} kg</strong>
              <p>${record.note ? escapeHtml(record.note) : "没有备注"}</p>
            </div>
            <button class="danger" data-id="${record.id}">删除</button>
          </div>
        `)
        .join("");
    }

    function renderDiaryStats() {
      const text = els.diaryInput.value || state.diaries[todayKey] || "";
      els.diaryStat.textContent = text.length + " 字";
    }

    function renderPhoto() {
      const photo = state.photos[todayKey];

      if (photo) {
        els.photoPreview.src = photo;
        els.photoPreview.style.display = "block";
        els.photoEmpty.style.display = "none";
      } else {
        els.photoPreview.removeAttribute("src");
        els.photoPreview.style.display = "none";
        els.photoEmpty.style.display = "grid";
      }
    }

    function renderStats() {
      const done = state.todos.filter((todo) => todo.done).length;

      els.todoStat.textContent = done + "/" + state.todos.length;
      els.weightStat.textContent = state.weights[0] ? state.weights[0].weight + " kg" : "未记录";
      els.diaryStat.textContent = (state.diaries[todayKey] || els.diaryInput.value || "").length + " 字";
      els.photoStat.textContent = state.photos[todayKey] ? "已上传" : "未上传";
    }

    function saveAndRender() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
      renderAll();
    }

    function loadState() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        return raw ? { ...defaultState, ...JSON.parse(raw) } : { ...defaultState };
      } catch {
        return { ...defaultState };
      }
    }

    function toDateKey(date) {
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, "0");
      const day = String(date.getDate()).padStart(2, "0");
      return `${year}-${month}-${day}`;
    }

    function createId() {
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

    function pulseInput(input) {
      input.focus();
      input.style.transform = "translateX(4px)";

      setTimeout(() => {
        input.style.transform = "";
      }, 120);
    }
  </script>
</body>
</html>
