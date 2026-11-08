# Medi_Alarm
Pengingat jadwal minum obat pasien digital
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>MEDI-ALARM</title>
<style>
body{font-family:Arial;background:#eef5f7;margin:0;padding:20px;color:#18343d}
.container{max-width:480px;margin:auto;background:white;padding:22px;border-radius:18px}
h1{text-align:center;color:#087e8b}
input,button{width:100%;padding:13px;margin:8px 0;box-sizing:border-box;border-radius:9px;border:1px solid #ccd8dc}
button{background:#087e8b;color:white;border:0;font-weight:bold}
.item{background:#e7f5f5;padding:12px;margin:10px 0;border-radius:10px}
</style>
</head>
<body>
<div class="container">
<h1>MEDI-ALARM</h1>
<p style="text-align:center">Pengingat Minum Obat</p>
<label>Nama obat</label>
<input id="nama" placeholder="Contoh: Vitamin">
<label>Dosis sesuai resep</label>
<input id="dosis" placeholder="Contoh: 1 tablet">
<label>Jam minum</label>
<input id="jam" type="time">
<label>Frekuensi</label>
<select id="ulang" style="width:100%;padding:12px">
<option value="sekali">Sekali</option>
<option value="harian">Setiap hari</option>
</select>
<button onclick="tambah()">Simpan Jadwal</button>
<h3>Jadwal Obat</h3>
<div id="daftar"></div>
</div>
<script>
let data=JSON.parse(localStorage.getItem("obat")||"[]");
function tampil(){
daftar.innerHTML="";
data.forEach((o,i)=>{
daftar.innerHTML+=`<div class="item"><b>${o.nama}</b><br>${o.dosis}<br>Jam: ${o.jam}<br>${o.ulang}<br><button onclick="hapus(${i})">Hapus</button></div>`;
});
}
function tambah(){
let nama=document.getElementById("nama").value;
let dosis=document.getElementById("dosis").value;
let jam=document.getElementById("jam").value;
let ulang=document.getElementById("ulang").value;
if(!nama||!dosis||!jam){alert("Lengkapi semua data");return;}
data.push({nama,dosis,jam,ulang});
localStorage.setItem("obat",JSON.stringify(data));
tampil();
document.getElementById("nama").value="";
document.getElementById("dosis").value="";
document.getElementById("jam").value="";
alert("Jadwal tersimpan");
}
function hapus(i){
data.splice(i,1);
localStorage.setItem("obat",JSON.stringify(data));
tampil();
}
tampil();
</script>
</body>
</html>
