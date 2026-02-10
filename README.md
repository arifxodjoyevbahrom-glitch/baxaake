<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>baxaVIBES Journal</title>

<style>
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:#2f2f2f;
  color:#fff;
}
.hidden{display:none}

/* ===== LOGIN ===== */
.login-wrap{
  height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
}
.login-box{
  background:#3a3a3a;
  width:380px;
  padding:40px;
  border-radius:16px;
  text-align:center;
  box-shadow:0 20px 50px rgba(0,0,0,.6);
}
.login-box h1{
  margin:0;
  font-size:28px;
  letter-spacing:2px;
}
.login-box p{
  color:#bbb;
  margin:10px 0 30px;
}
.login-box input{
  width:100%;
  padding:14px;
  margin-bottom:18px;
  border:none;
  border-radius:10px;
  background:#555;
  color:#fff;
  font-size:16px;
}
.login-box button{
  width:100%;
  padding:14px;
  border:none;
  border-radius:10px;
  font-size:16px;
  font-weight:bold;
  cursor:pointer;
  background:linear-gradient(135deg,#ff512f,#dd2476);
  color:#fff;
}

/* ===== JADVAL ===== */
#main{padding:15px}
h2{margin-bottom:10px}

.table-wrap{overflow-x:auto}

table{
  border-collapse:collapse;
  width:100%;
  min-width:1100px;
  background:#3b3b3b;
}
th,td{
  border:1px solid #aaa;
  padding:6px;
  font-size:13px;
  text-align:center;
}
th{background:#444}

.name{
  text-align:left;
  white-space:nowrap;
  min-width:230px;
}

input.mark{
  width:100%;
  border:none;
  outline:none;
  background:transparent;
  color:red;
  font-weight:bold;
  text-align:center;
}
input.mark[disabled]{
  color:#999;
}
</style>
</head>

<body>

<!-- LOGIN -->
<div class="login-wrap" id="loginPage">
  <div class="login-box">
    <h1>baxaVIBES</h1>
    <p>Journal Login</p>
    <input id="login" placeholder="Login">
    <input id="password" type="password" placeholder="Parol">
    <button onclick="enter()">KIRISH</button>
  </div>
</div>

<!-- MAIN -->
<div id="main" class="hidden">
  <h2>baxaVIBES Davomat Jurnali</h2>
  <div class="table-wrap">
    <table id="journal"></table>
  </div>
</div>

<script>
/* ===== USERS ===== */
const users={
  bahrom:{pass:"9099021872009",role:"admin"},
  user1:{pass:"1234",role:"view"},
  user2:{pass:"4321",role:"view"}
};
let currentRole="view";

/* ===== LOGIN ===== */
function enter(){
  const l=login.value;
  const p=password.value;
  if(users[l] && users[l].pass===p){
    currentRole=users[l].role;
    loginPage.classList.add("hidden");
    main.classList.remove("hidden");
    createTable();
  }else{
    alert("Login yoki parol xato");
  }
}

/* ===== DATA ===== */
const students=[
"ABDULLAYEV JASURBEK ULUG'BEK O'G'LI",
"ABDUPATTOYEV SAYIDG'OZI ABDULATIF O'G'LI",
"ADXAMOV HUSNIDDIN KAMOLIDDIN O'G'LI",
"ARIFXODJAYEV BAXROMXO'JA BAXODIR O'G'LI",
"BARATOV ABDULAZIZ XUSNIDDIN O'G'LI",
"DONIYOROV NURJAHON BEHZOD O'G'LI",
"ESERKAPOV OZODBEK BAKIR O'G'LI",
"ESHONBOYEV ILHOMJON NEMATULLO O'G'LI",
"HOSHIMOV BEKZOD ISTAM O‘G‘LI",
"MURATJONOV AKBARXON JAHONGIR O'G'LI",
"MUXAMEDJANOV MUXAMMADALI ZOKIRJON O'G'LI",
"NISHANOV RAMZIDDIN TURAYEVICH",
"OZODOV ABDULLOH AZAMAT O'G'LI",
"PARDAYEV BEXZOD KOMOLIDDIN O'G'LI",
"QOBILOV IBROHIMJON IKROMJON O'G'LI",
"SHERMAMATOV ABDUJALIL ABDUJABBOR O'G'LI",
"SHUXRATOV RIXSITILLA RAXMATILLA O'G'LI",
"SOBITOV ISLOM ILXOM O'GLI",
"SULTONBEKOV ABDULAZIZBEK ABDULATIFBEK O'G'LI",
"TO'RAYEV ASILBEK AKBAR O'G'LI",
"TUXTANAZAROV ARSEN DAMIROVICH",
"UMARXO'JAYEV FOZIL SANJAR O'G'LI",
"XAMIDOV SHAVKAT ABDIMALIK O'G'LI",
"XAMINOV ABDURAXMON XURSHID O'G'LI",
"XASANBOYEV ALISHER TURDALI O‘G‘LI",
"ZOKIRJONOV ALISHERMIRZO ZOXID OGLI"
];
const days=30;

/* ===== TABLE ===== */
function createTable(){
  const t=document.getElementById("journal");
  t.innerHTML="";

  let r1="<tr><th rowspan='2'>Ism Familiya</th>";
  for(let d=1;d<=days;d++)r1+=`<th colspan="4">${d}-kun</th>`;
  r1+="</tr>";

  let r2="<tr>";
  for(let d=1;d<=days;d++)r2+="<th>I</th><th>II</th><th>III</th><th>IV</th>";
  r2+="</tr>";

  t.innerHTML+=r1+r2;

  students.forEach((s,i)=>{
    let row=`<tr><td class="name">${s}</td>`;
    for(let d=1;d<=days;d++){
      for(let p=1;p<=4;p++){
        const k=`${i}_${d}_${p}`;
        const v=localStorage.getItem(k)||"";
        row+=`<td><input class="mark" value="${v}"
        ${currentRole!=="admin"?"disabled":""}
        oninput="localStorage.setItem('${k}',this.value)"></td>`;
      }
    }
    row+="</tr>";
    t.innerHTML+=row;
  });
}
</script>

</body>
</html>
