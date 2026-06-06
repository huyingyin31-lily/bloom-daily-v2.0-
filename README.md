# bloom-daily-v2.0-
<!doctype html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width,initial-scale=1.0" />
<title>Bloom daily</title>
<style>
:root{--bg:#fff9f8;--card:#fff;--soft:#fff0f2;--text:#30292b;--muted:#8b7679;--p:#df6f81;--line:#f1dde0}
*{box-sizing:border-box}body{margin:0;min-height:100vh;color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;background:radial-gradient(circle at 10% 0,var(--soft),transparent 35%),linear-gradient(135deg,var(--bg),#fff)}
button,input,textarea{font:inherit}button{cursor:pointer;border:0;border-radius:10px;padding:12px 16px;font-weight:700}.primary{color:white;background:var(--p)}.ghost{color:var(--p);background:var(--soft)}
.hidden{display:none!important}.auth{min-height:100vh;display:grid;place-items:center;padding:24px}.card,.panel,.tile{border:1px solid var(--line);border-radius:14px;background:rgba(255,255,255,.86);box-shadow:0 20px 60px rgba(120,72,82,.12)}
.auth-card{width:min(100%,430px);padding:28px}.brand{display:flex;gap:12px;align-items:center;margin-bottom:22px}.logo{width:48px;height:48px;display:grid;place-items:center;border-radius:16px;background:var(--p);color:white;font-size:24px;font-weight:900}
h1,h2,h3,p{margin-top:0}.muted{color:var(--muted)}label span{display:block;margin-bottom:8px;color:var(--muted);font-size:14px;font-weight:700}input,textarea{width:100%;border:1px solid var(--line);border-radius:10px;padding:12px;background:white;color:var(--text)}
form{display:grid;gap:14px}.tabs{display:grid;grid-template-columns:1fr 1fr;gap:8px;background:var(--soft);padding:4px;border-radius:12px;margin-bottom:16px}.tabs button{background:transparent;color:var(--muted)}.tabs .on{background:var(--p);color:white}
.themes{display:grid;grid-template-columns:repeat(5,1fr);gap:8px;margin-top:18px}.dot{height:42px;border-radius:12px;border:1px solid var(--line)}
.app{display:grid;grid-template-columns:240px 1fr;min-height:100vh}aside{padding:24px;border-right:1px solid var(--line);background:rgba(255,255,255,.55)}nav{display:grid;gap:8px}nav button{text-align:left;background:transparent;color:var(--muted)}nav .on{background:var(--soft);color:var(--p)}
main{padding:32px;max-width:1000px}.top{display:flex;justify-content:space-between;gap:16px;align-items:center;margin-bottom:22px}.view{display:none}.view.on{display:block}.grid{display:grid;grid-template-columns:repeat(2,minmax(180px,1fr));gap:16px}.tile{min-height:150px;padding:20px;text-align:left;color:var(--text)}
.panel{padding:22px}.row{display:grid;grid-template-columns:1fr auto;gap:10px}.list{display:grid;gap:10px;margin-top:14px}.todo{display:grid;grid-template-columns:auto 1fr auto;gap:10px;align-items:center;padding:12px;border:1px solid var(--line);border-radius:10px;background:var(--bg)}.done{text-decoration:line-through;color:var(--muted)}
.photo{display:grid;place-items:center;min-height:260px;border-radius:12px;background:var(--soft);overflow:hidden}.photo img{width:100%;height:100%;object-fit:cover}.toast{position:fixed;left:50%;bottom:22px;transform:translateX(-50%);background:#222;color:white;padding:10px 14px;border-radius:10px;opacity:0}.toast.show{opacity:1}
@media(max-width:760px){.app{grid-template-columns:1fr}aside{position:sticky;top:0;z-index:2;border-right:0;border-bottom:1px solid var(--line)}nav{display:flex;overflow:auto}.grid,.row{grid-template-columns:1fr}main{padding:18px}}
</style>
</head>
<body>
<section id="auth" class="auth">
  <div class="auth-card card">
    <div class="brand"><div class="logo">B</div><div><h1>Bloom daily</h1><p class="muted" id="note">今天也可以慢慢盛开</p></div></div>
    <div class="tabs"><button id="loginTab" class="on">登录</button><button id="regTab">注册</button></div>
    <form id="authForm">
      <label id="nameBox" class="hidden"><span>昵称</span><input id="name" /></label>
      <label><span>邮箱</span><input id="email" type="email" required /></label>
      <label><span>密码</span><input id="pwd" type="password" required /></label>
      <button class="primary" id="authBtn">登录</button>
    </form>
    <div class="themes" id="themes"></div>
  </div>
</section>

<div id="app" class="app hidden">
  <aside><div class="brand"><div class="logo">B</div><div><h1>Bloom daily</h1><p class="muted">成长日记</p></div></div>
    <nav><button class="nav on" data-v="home">今日</button><button class="nav" data-v="todos">Todo</button><button class="nav" data-v="weight">体重</button><button class="nav" data-v="diary">日记</button><button class="nav" data-v="photo">照片</button><button class="nav" data-v="settings">设置</button></nav>
  </aside>
  <main>
    <div class="top"><div><p class="muted" id="hello">晚上好</p><h2 id="dateText">今天</h2></div><div><span id="who" class="muted"></span> <input id="date" type="date"> <button id="logout" class="ghost">退出</button></div></div>
    <section id="home" class="view on"><div class="panel" style="margin-bottom:16px"><b>今日微光</b><p class="muted" id="homeNote">今天也可以慢慢盛开</p></div><div class="grid"><button class="tile" data-j="todos">今日 Todo<br><h2 id="sTodo">待添加</h2></button><button class="tile" data-j="weight">今日体重<br><h2 id="sWeight">待记录</h2></button><button class="tile" data-j="diary">今日日记<br><h2 id="sDiary">写下今天</h2></button><button class="tile" data-j="photo">今日照片<br><h2 id="sPhoto">未上传</h2></button></div></section>
    <section id="todos" class="view"><div class="panel"><h3>今日 Todo</h3><form id="todoForm" class="row"><input id="todoInput" placeholder="添加新任务"><button class="primary">添加</button></form><div id="todoList" class="list"></div></div></section>
    <section id="weight" class="view"><div class="panel"><h3>今日体重</h3><form id="weightForm"><input id="weightInput" type="number" step=".1" placeholder="例如 55.5"><textarea id="weightNote" placeholder="备注"></textarea><button class="primary">保存记录</button></form></div></section>
    <section id="diary" class="view"><div class="panel"><h3>今日日记</h3><form id="diaryForm"><textarea id="diaryInput" rows="10" placeholder="今天发生了什么？"></textarea><button class="primary">保存日记</button></form></div></section>
    <section id="photo" class="view"><div class="panel"><h3>今日照片</h3><div id="photoView" class="photo">选择一张照片记录今天</div><p><input id="photoInput" type="file" accept="image/*"> <button id="delPhoto" class="ghost">删除照片</button></p></div></section>
    <section id="settings" class="view"><div class="panel"><h3>设置</h3><div id="themes2" class="themes"></div></div></section>
  </main>
</div>
<div id="toast" class="toast"></div>

<script>
const $=s=>document.querySelector(s),$$=s=>[...document.querySelectorAll(s)];
const T={rose:["#fff9f8","#fff0f2","#df6f81","今天也可以慢慢盛开"],sage:["#f7fbf7","#eaf5ed","#5d9f75","小小生长也值得被看见"],linen:["#fdfaf4","#f6efdf","#c89a4a","把今天过得轻一点"],mist:["#f7fafc","#eaf2f7","#5e95b4","安静记录，也是一种照顾"],plum:["#fbf7f8","#f3e9ec","#9d6b7d","给今天留一盏温柔的小灯"]};
let mode="login",theme=localStorage.theme||"rose",user=JSON.parse(localStorage.user||"null"),day=new Date().toLocaleDateString("en-CA");
const db=()=>JSON.parse(localStorage.db||"{}"),save=o=>localStorage.db=JSON.stringify(o),k=t=>`${user.email}:${day}:${t}`,msg=t=>{toast.textContent=t;toast.classList.add("show");setTimeout(()=>toast.classList.remove("show"),1500)};
function apply(x){theme=x;localStorage.theme=x;let v=T[x];document.documentElement.style.cssText=`--bg:${v[0]};--soft:${v[1]};--p:${v[2]};--line:${v[1]};`;note.textContent=homeNote.textContent=v[3];$$(".dot").forEach(d=>d.classList.toggle("active",d.dataset.t==x))}
function themeBtns(el){el.innerHTML=Object.keys(T).map(t=>`<button class="dot" data-t="${t}" style="background:${T[t][1]}"></button>`).join("");el.querySelectorAll("button").forEach(b=>b.onclick=()=>apply(b.dataset.t))}
themeBtns(themes);themeBtns(themes2);apply(theme);date.value=day;
loginTab.onclick=()=>{mode="login";nameBox.classList.add("hidden");authBtn.textContent="登录";loginTab.classList.add("on");regTab.classList.remove("on")};
regTab.onclick=()=>{mode="reg";nameBox.classList.remove("hidden");authBtn.textContent="注册并进入";regTab.classList.add("on");loginTab.classList.remove("on")};
authForm.onsubmit=e=>{e.preventDefault();let us=JSON.parse(localStorage.users||"[]"),email=$("#email").value.trim(),pwd=$("#pwd").value;if(mode=="reg"){if(us.some(u=>u.email==email))return msg("邮箱已注册");user={name:name.value||"Bloom",email,pwd};us.push(user);localStorage.users=JSON.stringify(us)}else{user=us.find(u=>u.email==email&&u.pwd==pwd);if(!user)return msg("邮箱或密码不正确")}localStorage.user=JSON.stringify(user);showApp()};
logout.onclick=()=>{localStorage.removeItem("user");user=null;auth.classList.remove("hidden");app.classList.add("hidden")};
function showApp(){auth.classList.add("hidden");app.classList.remove("hidden");who.textContent=user.name;load("home")}
$$(".nav").forEach(b=>b.onclick=()=>load(b.dataset.v));$$(".tile").forEach(b=>b.onclick=()=>load(b.dataset.j));date.onchange=e=>{day=e.target.value;load(document.querySelector(".view.on").id)};
function load(v){$$(".view").forEach(x=>x.classList.toggle("on",x.id==v));$$(".nav").forEach(x=>x.classList.toggle("on",x.dataset.v==v));dateText.textContent=new Intl.DateTimeFormat("zh-CN",{month:"long",day:"numeric",weekday:"long"}).format(new Date(day+"T00:00:00"));if(v=="home")sum();if(v=="todos")todos();if(v=="weight"){let w=db()[k("w")]||{};weightInput.value=w.n||"";weightNote.value=w.note||""}if(v=="diary")diaryInput.value=db()[k("d")]||"";if(v=="photo")photo(db()[k("p")])}
function sum(){let d=db(),ts=d[k("t")]||[],w=d[k("w")],di=d[k("d")],p=d[k("p")];sTodo.textContent=ts.length?`${ts.filter(x=>x.done).length}/${ts.length}`:"待添加";sWeight.textContent=w?`${w.n} kg`:"待记录";sDiary.textContent=di?di.slice(0,8):"写下今天";sPhoto.textContent=p?"已记录":"未上传"}
todoForm.onsubmit=e=>{e.preventDefault();let d=db(),a=d[k("t")]||[];a.unshift({id:Date.now(),text:todoInput.value,done:false});d[k("t")]=a;save(d);todoInput.value="";todos();sum()};
function todos(){let a=db()[k("t")]||[];todoList.innerHTML=a.map(x=>`<div class="todo ${x.done?'done':''}" data-id="${x.id}"><input type="checkbox" ${x.done?'checked':''}><span>${x.text}</span><button class="ghost">删</button></div>`).join("")||"<p class='muted'>今天还没有任务</p>"}
todoList.onclick=e=>{let it=e.target.closest(".todo");if(!it)return;let d=db(),a=d[k("t")]||[];if(e.target.type=="checkbox")a.find(x=>x.id==it.dataset.id).done=e.target.checked;if(e.target.tagName=="BUTTON")a=a.filter(x=>x.id!=it.dataset.id);d[k("t")]=a;save(d);todos();sum()};
weightForm.onsubmit=e=>{e.preventDefault();let d=db();d[k("w")]={n:weightInput.value,note:weightNote.value};save(d);sum();msg("已保存")};
diaryForm.onsubmit=e=>{e.preventDefault();let d=db();d[k("d")]=diaryInput.value;save(d);sum();msg("已保存")};
photoInput.onchange=e=>{let f=e.target.files[0],r=new FileReader();r.onload=()=>{let d=db();d[k("p")]=r.result;save(d);photo(r.result);sum()};if(f)r.readAsDataURL(f)};
delPhoto.onclick=()=>{let d=db();delete d[k("p")];save(d);photo(null);sum()};function photo(src){photoView.innerHTML=src?`<img src="${src}">`:"选择一张照片记录今天"}
if(user)showApp();
</script>
</body>
</html>
