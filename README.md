<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Samirxxx Panel</title>

<style>
*{box-sizing:border-box;font-family:-apple-system,BlinkMacSystemFont,Segoe UI}
body{
  margin:0;height:100vh;display:flex;align-items:center;justify-content:center;
  background:#000;color:#fff;overflow:hidden;
}

/* FONDO SUTIL */
.bg{
  position:fixed;inset:0;
  background:radial-gradient(circle at 20% 10%,#20003a,#000 60%),
             radial-gradient(circle at 80% 90%,#12002a,#000 60%);
  filter:blur(0.5px);
}

/* ANIMACIONES GENERALES */
@keyframes fadeZoom{from{opacity:0;transform:scale(.92)}to{opacity:1;transform:scale(1)}}
@keyframes floaty{0%,100%{transform:translateY(0)}50%{transform:translateY(-4px)}}
@keyframes neon{
  0%{box-shadow:0 0 12px #b100ff}
  50%{box-shadow:0 0 28px #ff00ff}
  100%{box-shadow:0 0 12px #b100ff}
}
@keyframes scan{
  from{transform:translateY(-120%)}
  to{transform:translateY(120%)}
}
@keyframes shimmer{
  from{transform:translateX(-120%)}
  to{transform:translateX(120%)}
}
@keyframes slideIn{from{opacity:0;transform:translateX(-12px)}to{opacity:1;transform:none}}
@keyframes pulse{0%{transform:scale(1)}50%{transform:scale(1.03)}100%{transform:scale(1)}}

/* TARJETA BASE */
.card{
  position:relative;
  width:90vw;max-width:360px;
  background:#141421;border-radius:22px;padding:18px;
  animation:fadeZoom .6s ease,floaty 4s ease-in-out infinite,neon 3s infinite;
  z-index:2;
  overflow:hidden;
}

/* EFECTOS SOBRE TODO EL PANEL */
.card::before{
  content:"";position:absolute;inset:-40%;
  background:linear-gradient(120deg,transparent 40%,rgba(255,255,255,.08),transparent 60%);
  animation:shimmer 4s linear infinite;
}
.card::after{
  content:"";position:absolute;left:0;right:0;height:18%;
  background:linear-gradient(to bottom,transparent,rgba(177,0,255,.18),transparent);
  animation:scan 3.5s linear infinite;
  pointer-events:none;
}

/* TITULOS */
h1,h2{text-align:center;color:#b100ff;margin:6px 0}

/* INPUTS */
input{
  width:100%;padding:14px;border-radius:14px;border:none;margin-top:10px;font-size:16px;
}

/* BOTONES */
button{
  width:100%;padding:15px;border:none;border-radius:18px;margin-top:14px;
  background:linear-gradient(90deg,#b100ff,#ff00ff);
  color:#fff;font-size:17px;transition:.15s;
}
button:active{transform:scale(.96)}

/* PANEL */
#panel{display:none}

/* OPCIONES */
.option{
  display:flex;justify-content:space-between;align-items:center;margin:14px 0;
  animation:slideIn .4s ease both;
}
.option:nth-child(1){animation-delay:.05s}
.option:nth-child(2){animation-delay:.10s}
.option:nth-child(3){animation-delay:.15s}

.switch{
  width:46px;height:26px;background:#333;border-radius:20px;position:relative;transition:.3s;
}
.switch::after{
  content:"";width:22px;height:22px;background:#fff;border-radius:50%;
  position:absolute;top:2px;left:2px;
  transition:.3s cubic-bezier(.68,-0.55,.27,1.55);
}
.switch.active{background:#b100ff;box-shadow:0 0 10px #b100ff}
.switch.active::after{left:22px}

/* LOADER */
.loader{
  height:8px;background:#222;border-radius:10px;overflow:hidden;display:none;margin-top:10px;
}
.loader div{
  height:100%;background:#b100ff;animation:load 2s linear forwards;
}
@keyframes load{from{width:0}to{width:100%}}

/* LOGS */
.logs{
  margin-top:10px;background:#0d0d16;padding:8px;height:80px;overflow:auto;
  font-size:12px;border-radius:12px;color:#7cff9e;
}
.logs div{animation:slideIn .25s}

/* INYECTAR PULSO */
.injecting{animation:pulse .6s ease 2}

footer{text-align:center;font-size:11px;color:#777;margin-top:8px}
</style>
</head>

<body>
<div class="bg"></div>

<!-- LOGIN -->
<div class="card" id="login">
  <h1>Samirxxx</h1>
  <input id="user" placeholder="Usuario">
  <input id="pass" type="password" placeholder="Contraseña">
  <button onclick="login()">Entrar</button>
</div>

<!-- PANEL -->
<div class="card" id="panel">
  <h2>Samirxxx</h2>

  <div class="option">Aimbot <div class="switch" onclick="toggle(this,'Aimbot')"></div></div>
  <div class="option">No Recoil <div class="switch" onclick="toggle(this,'Recoil')"></div></div>
  <div class="option">Precisión <div class="switch" onclick="toggle(this,'Precision')"></div></div>

  <button id="injectBtn" onclick="inject()">INJECTAR</button>
  <div class="loader" id="loader"><div></div></div>

  <div class="logs" id="logs"></div>
  <footer>@Samirxxx</footer>
</div>

<script>
const logs=document.getElementById("logs")
const loginDiv=document.getElementById("login")
const panel=document.getElementById("panel")
const loader=document.getElementById("loader")
const injectBtn=document.getElementById("injectBtn")

function login(){
  if(user.value.trim()==="Samirxxx" && pass.value.trim()==="S"){
    loginDiv.style.display="none"
    panel.style.display="block"
    log("Login correcto")
  }else alert("Datos incorrectos")
}

function toggle(el,name){
  el.classList.toggle("active")
  log(name+(el.classList.contains("active")?" ON":" OFF"))
}

function inject(){
  injectBtn.classList.add("injecting")
  loader.style.display="block"
  log("Inyectando (visual)…")
  setTimeout(()=>{
    log("✔ Activado")
    injectBtn.classList.remove("injecting")
  },2000)
}

function log(t){
  const d=document.createElement("div")
  d.textContent="> "+t
  logs.appendChild(d)
  logs.scrollTop=logs.scrollHeight
}
</script>
</body>
</html>
