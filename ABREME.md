<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>¿Quieres ser mi San Valentín? 💖</title>

<style>
body{
    margin:0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg,#ff9a9e,#fad0c4);
    overflow:hidden;
}

.container{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.card{
    background:white;
    padding:30px;
    border-radius:20px;
    text-align:center;
    box-shadow:0 10px 25px rgba(0,0,0,0.2);
    max-width:380px;
    z-index:2;
}

img{
    width:100%;
    border-radius:15px;
    margin-bottom:20px;
}

h1{color:#e63946;}
p{font-size:18px;margin-bottom:20px;}

.buttons{
    display:flex;
    justify-content:center;
    gap:20px;
}

button{
    padding:12px 24px;
    font-size:16px;
    border:none;
    border-radius:25px;
    cursor:pointer;
    transition:transform 0.3s ease;
}

#yes{background:#e63946;color:white;}
#no{background:#ccc;}

/* Corazones flotando */
.heart{
    position:fixed;
    bottom:-20px;
    animation:float 6s linear forwards;
    opacity:.85;
    color:#e63946;
}
@keyframes float{
    from{transform:translateY(0) scale(1);opacity:1;}
    to{transform:translateY(-120vh) scale(1.5);opacity:0;}
}

/* Explosión */
.explode{
    position:fixed;
    animation:boom 1.2s ease-out forwards;
}
@keyframes boom{
    from{transform:translate(0,0) scale(1);opacity:1;}
    to{transform:translate(var(--x),var(--y)) scale(1.6);opacity:0;}
}

/* Pantalla final */
.fullscreen{
    position:fixed;
    top:0;left:0;
    width:100vw;height:100vh;
    background:linear-gradient(135deg,#ff9a9e,#fad0c4);
    display:flex;
    justify-content:center;
    align-items:center;
    z-index:10;
}

.final{
    text-align:center;
    padding:40px;
    max-width:850px;
}

.final h1{
    font-size:42px;
    color:#e63946;
}

.final p{
    font-size:22px;
    color:#333;
}

.counter{
    margin-top:25px;
    font-size:21px;
    color:#e63946;
    font-weight:bold;
}
</style>
</head>

<body>

<!-- Sonido suave -->
<audio id="loveSound" src="https://cdn.pixabay.com/audio/2022/03/15/audio_5a8d6bfa2d.mp3"></audio>

<div class="container">
<div class="card">
<img src="https://i.imgur.com/8QfKQ8U.jpg">
<h1>💘 Con amor, Ian Uriel 💘</h1>
<p id="question">
Hola mi amor 💖<br>
¿Quieres ser el San Valentín de tu Cachorrito? 🐶
</p>

<div class="buttons">
<button id="yes" onclick="sayYes()">Sí 💖</button>
<button id="no" onclick="sayNo()">No 💔</button>
</div>
</div>
</div>

<script>
/* ---------- Lógica del NO ---------- */
let scale=1, attempts=0;
const questions=[
"¿Segura? 🥺",
"Piénsalo bien, mi amor 💭",
"Yo sé que sí quieres 😏",
"Ya casi dices que sí 💕",
"Tu Cachorrito te ama 🐶💘"
];

function sayNo(){
    attempts++;
    document.getElementById("question").textContent =
        questions[Math.min(attempts-1,questions.length-1)];
    scale+=0.3;
    document.getElementById("yes").style.transform=scale(${scale});
}

/* ---------- Explosión de corazones con I + A ---------- */
function explodeHearts(){
    for(let i=0;i<80;i++){
        const h=document.createElement("div");
        h.className="explode";
        h.textContent="💖 I + A";
        h.style.left="50vw";
        h.style.top="50vh";
        h.style.setProperty("--x",(Math.random()*800-400)+"px");
        h.style.setProperty("--y",(Math.random()*800-400)+"px");
        h.style.fontSize=Math.random()*18+14+"px";
        document.body.appendChild(h);
        setTimeout(()=>h.remove(),1200);
    }
}

/* ---------- Fecha inicio: 15 de septiembre más reciente ---------- */
function getStartDate(){
    const now=new Date();
    let year=now.getFullYear();
    let start=new Date(year,8,15);
    if(now<start) start=new Date(year-1,8,15);
    return start;
}
const startDate=getStartDate();

/* ---------- Contador completo ---------- */
function updateCounter(){
    const now=new Date();
    let y=now.getFullYear()-startDate.getFullYear();
    let m=now.getMonth()-startDate.getMonth();
    let d=now.getDate()-startDate.getDate();
    let h=now.getHours()-startDate.getHours();
    let min=now.getMinutes()-startDate.getMinutes();
    let s=now.getSeconds()-startDate.getSeconds();

    if(s<0){s+=60;min--;}
    if(min<0){min+=60;h--;}
    if(h<0){h+=24;d--;}
    if(d<0){
        const prevMonth=new Date(now.getFullYear(),now.getMonth(),0).getDate();
        d+=prevMonth;
        m--;
    }
    if(m<0){m+=12;y--;}

    document.getElementById("counter").textContent =
    💞 Desde que empezó lo nuestro: ${y} años, ${m} meses, ${d} días, ${h} h, ${min} min y ${s} s 💕;
}

/* ---------- SÍ ---------- */
function sayYes(){
    document.getElementById("loveSound").play();
    explodeHearts();

    setTimeout(()=>{
        document.body.innerHTML=`
        <div class="fullscreen">
            <div class="final">
                <h1>💖 ¡Sabía que aceptarías! 💖</h1>
                <p>
                Yo sabía que aceptarías ser mi San Valentín.<br><br>
                Te amo demasiado y cuando estoy contigo soy genuinamente muy feliz.
                No hay lugar donde prefiera estar ni momento que disfrute más
                que compartir mi tiempo a tu lado.<br><br>
                Quiero pasar esta fecha especial contigo y guardarla en nuestro corazón,
                para recordarla con una sonrisa en todos los años que aún nos quedan
                por vivir juntos 💘
                </p>
                <div class="counter" id="counter"></div>
                <p><strong>Con todo mi amor,<br>Ian Uriel (tu Cachorrito 🐶)</strong></p>
            </div>
        </div>
        `;
        updateCounter();
        setInterval(updateCounter,1000);
    },900);
}

/* Corazones flotando constantes */
setInterval(()=>{
    const h=document.createElement("div");
    h.className="heart";
    h.textContent="💖 I + A";
    h.style.left=Math.random()*100+"vw";
    h.style.fontSize=Math.random()*18+14+"px";
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),6000);
},300);
</script>

</body>
</html>
