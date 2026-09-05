<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Presensi Kehadiran SMAN 2 Nusa - Kelola Data & Tautan</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: { 50: '#eef2ff', 500: '#6366f1', 600: '#4f46e5', 700: '#4338ca' }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style id="responsive-modern-ui">
/* ===== MODERN RESPONSIVE UI — hanya tampilan ===== */
:root{
  --ui-radius:18px;
  --ui-shadow:0 10px 30px rgba(15,23,42,.08);
  --ui-shadow-hover:0 16px 38px rgba(15,23,42,.13);
}
html{scroll-behavior:smooth}
body{
  -webkit-tap-highlight-color:transparent;
  background:
    radial-gradient(circle at 0% 0%, rgba(59,130,246,.07), transparent 30%),
    radial-gradient(circle at 100% 0%, rgba(16,185,129,.06), transparent 28%),
    #f8fafc;
}
.dark body{
  background:
    radial-gradient(circle at 0% 0%, rgba(59,130,246,.12), transparent 30%),
    #0f172a;
}

/* Header / cards */
header, .card, [class*="shadow"]{
  transition:box-shadow .2s ease, transform .2s ease, border-color .2s ease;
}
button{
  min-height:40px;
  border-radius:12px !important;
  transition:transform .15s ease, box-shadow .15s ease, opacity .15s ease;
}
button:hover{transform:translateY(-1px)}
button:active{transform:translateY(0) scale(.98)}
input, select, textarea{
  border-radius:12px !important;
  transition:border-color .15s ease, box-shadow .15s ease;
}
input:focus,select:focus,textarea:focus{
  outline:none;
  box-shadow:0 0 0 3px rgba(59,130,246,.14);
}

/* Class tabs */
#classTabs{
  scrollbar-width:thin;
  -webkit-overflow-scrolling:touch;
}
#classTabs button{
  white-space:nowrap;
  flex-shrink:0;
}

/* Student rows */
#studentList > *,
#studentList .student-row{
  transition:transform .15s ease, box-shadow .15s ease;
}
#studentList > *:hover{
  box-shadow:var(--ui-shadow-hover);
}

/* Link result */
#outputLinkArea{
  font-family:ui-monospace,SFMono-Regular,Menlo,monospace;
  line-height:1.55;
}

/* ===== Windows / desktop ===== */
@media (min-width: 1024px){
  main{max-width:1500px !important}
  header .container{max-width:1500px !important}
  #studentList{
    display:grid;
    grid-template-columns:repeat(2,minmax(0,1fr));
    gap:12px;
  }
}

/* ===== HP / tablet ===== */
@media (max-width: 1023px){
  body{font-size:15px}
  header{
    position:sticky;
    top:0;
    z-index:40;
    backdrop-filter:blur(14px);
    background:rgba(255,255,255,.88) !important;
  }
  .dark header{background:rgba(15,23,42,.88) !important}
  main{padding-left:12px !important;padding-right:12px !important}
  #studentList{display:block}
  #studentList > *{margin-bottom:10px}
}

/* ===== HP portrait ===== */
@media (max-width: 640px){
  header{
    padding:10px 12px !important;
  }
  header h1{
    font-size:1rem !important;
    line-height:1.25 !important;
  }
  header p{font-size:.72rem !important}

  /* Tombol header menjadi lebih ringkas */
  header button{
    min-height:38px;
    padding-left:10px !important;
    padding-right:10px !important;
  }

  /* Jangan biarkan tabel/area melebar keluar layar */
  .overflow-x-auto{
    max-width:100%;
    overflow-x:auto;
  }

  /* Modal nyaman disentuh */
  [role="dialog"] > div,
  .fixed > div{
    max-height:92vh;
  }

  /* Form 2 kolom turun menjadi 1 kolom */
  .grid.grid-cols-2{
    grid-template-columns:1fr !important;
  }

  /* Area tombol lebih mudah disentuh */
  .flex.gap-2, .flex.gap-3{
    flex-wrap:wrap;
  }

  button{min-height:42px}

  /* Font dan padding kartu siswa */
  #studentList .p-4,
  #studentList .p-3{
    padding:12px !important;
  }
}

/* ===== HP sangat kecil ===== */
@media (max-width: 400px){
  main{padding-left:8px !important;padding-right:8px !important}
  header{padding-left:8px !important;padding-right:8px !important}
  header .flex{gap:5px !important}
  button{font-size:.78rem}
}
</style>

<style id="view-mode-overrides">
@media (min-width:641px){
  html.force-phone body{font-size:15px}
  html.force-phone main{max-width:700px !important;margin-left:auto;margin-right:auto}
  html.force-phone #studentList{display:block}
}
@media (max-width:1023px){
  html.force-windows main{max-width:1500px !important;margin-left:auto;margin-right:auto}
  html.force-windows #studentList{
    display:grid;
    grid-template-columns:repeat(2,minmax(0,1fr));
    gap:12px;
  }
}
@media (max-width:640px){
  html.force-windows #studentList{display:block}
}
</style>

<style id="background-submit-ui">
#bgSendPanel{
  position:fixed; inset:0; z-index:100;
  display:none; align-items:center; justify-content:center;
  background:rgba(15,23,42,.48); backdrop-filter:blur(6px);
}
#bgSendPanel .bg-send-card{
  width:min(520px,calc(100vw - 28px));
  border-radius:22px;
  padding:22px;
  background:white;
  color:#0f172a;
  box-shadow:0 25px 70px rgba(0,0,0,.22);
}
.dark #bgSendPanel .bg-send-card{background:#1e293b;color:#f8fafc}
#bgSendProgress{
  height:10px; border-radius:999px; overflow:hidden;
  background:#e2e8f0;
}
#bgSendProgressBar{
  width:0%; height:100%; border-radius:999px;
  background:linear-gradient(90deg,#2563eb,#06b6d4);
  transition:width .2s ease;
}
</style>

<style id="modern-final-design">
:root{--blue:#2563eb;--border:#e2e8f0;--bg:#f6f8fc}
body{
  background:
    radial-gradient(circle at 10% -5%,rgba(37,99,235,.10),transparent 28%),
    radial-gradient(circle at 95% 0%,rgba(16,185,129,.07),transparent 25%),
    var(--bg);
}
.dark body{background:radial-gradient(circle at 10% -5%,rgba(37,99,235,.14),transparent 28%),#0f172a}
header{box-shadow:0 5px 24px rgba(15,23,42,.07);border-bottom:1px solid rgba(148,163,184,.18)}
button{min-height:36px!important;border-radius:10px!important;font-size:.82rem!important;transition:.16s ease}
button:hover{transform:translateY(-1px);box-shadow:0 5px 14px rgba(15,23,42,.08)}
#classTabs{
  gap:6px!important;padding:5px!important;border-radius:14px;
  background:rgba(255,255,255,.76);border:1px solid var(--border);
  overflow-x:auto;scrollbar-width:none;backdrop-filter:blur(10px)
}
#classTabs::-webkit-scrollbar{display:none}
#classTabs button{min-width:54px;min-height:34px!important;padding:6px 11px!important}
#studentList{gap:10px!important}
#studentList>*{
  border:1px solid var(--border);border-radius:15px!important;
  background:rgba(255,255,255,.95);box-shadow:0 3px 13px rgba(15,23,42,.045);
  overflow:hidden;transition:transform .16s ease,box-shadow .16s ease,border-color .16s ease
}
#studentList>*:hover{transform:translateY(-2px);box-shadow:0 10px 25px rgba(15,23,42,.09);border-color:#bfdbfe}
.dark #studentList>*{background:rgba(30,41,59,.9);border-color:#334155}
#studentList input[type=checkbox]{width:20px!important;height:20px!important;accent-color:var(--blue);cursor:pointer}
input[type=text],input[type=search],select{min-height:40px;border-radius:11px!important}
#outputLinkArea{border-radius:14px!important}
@media(min-width:1024px){
  main{max-width:1480px!important}
  #studentList{display:grid!important;grid-template-columns:repeat(2,minmax(0,1fr))}
}
@media(max-width:640px){
  main{padding-left:10px!important;padding-right:10px!important}
  #studentList{display:block!important}
  #studentList>*{margin-bottom:8px}
  #classTabs button{min-width:50px;padding-left:9px!important;padding-right:9px!important}
  #viewModeMenu{bottom:8px!important}
  #viewModeMenu button{min-height:31px!important;padding:5px 8px!important;font-size:.7rem!important}
}
html.force-phone main{max-width:760px!important;margin:auto}
html.force-phone #studentList{display:block!important}
html.force-windows #studentList{display:grid!important;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px}
@media(max-width:700px){html.force-windows #studentList{grid-template-columns:1fr}}
</style>


<style id="super-rapi-ui-only">
/* =========================================================
   SUPER RAPI UI
   CSS ONLY — DATA & LOGIKA TIDAK DISENTUH
   ========================================================= */
:root{
  --ui-primary:#2563eb;
  --ui-primary-dark:#1d4ed8;
  --ui-success:#059669;
  --ui-warning:#d97706;
  --ui-danger:#dc2626;
  --ui-text:#0f172a;
  --ui-muted:#64748b;
  --ui-border:#e2e8f0;
  --ui-surface:#ffffff;
  --ui-surface-soft:#f8fafc;
  --ui-radius:18px;
}

html{scroll-behavior:smooth}
body{
  color:var(--ui-text);
  background:
    radial-gradient(900px 420px at -5% -10%,rgba(37,99,235,.12),transparent 60%),
    radial-gradient(700px 360px at 105% 0%,rgba(16,185,129,.08),transparent 58%),
    #f6f8fc;
}

/* ===== HEADER ===== */
header{
  position:sticky;
  top:0;
  z-index:50;
  border-bottom:1px solid rgba(148,163,184,.20);
  background:rgba(255,255,255,.88)!important;
  backdrop-filter:blur(18px) saturate(150%);
  box-shadow:0 6px 24px rgba(15,23,42,.06);
}
header h1{
  letter-spacing:-.035em;
  line-height:1.15!important;
}
header p{letter-spacing:.01em}

/* ===== GLOBAL BUTTONS ===== */
button{
  min-height:38px!important;
  border-radius:11px!important;
  font-weight:650!important;
  letter-spacing:-.01em;
  transition:transform .15s ease,box-shadow .15s ease,filter .15s ease,background .15s ease;
}
button:hover{
  transform:translateY(-1px);
  filter:saturate(1.04);
}
button:active{transform:translateY(0) scale(.98)}
button:focus-visible{
  outline:none!important;
  box-shadow:0 0 0 3px rgba(37,99,235,.18)!important;
}

/* ===== MAIN CONTENT ===== */
main{padding-bottom:80px}
main > *{max-width:100%}

/* ===== SECTION/CARD POLISH ===== */
main .rounded-lg,
main .rounded-xl,
main .rounded-2xl{
  border-color:rgba(226,232,240,.9);
}
main .shadow,
main .shadow-sm,
main .shadow-md,
main .shadow-lg{
  box-shadow:0 5px 20px rgba(15,23,42,.055)!important;
}

/* ===== CLASS TABS ===== */
#classTabs{
  display:flex!important;
  align-items:center;
  gap:6px!important;
  padding:5px!important;
  min-height:48px;
  overflow-x:auto;
  scrollbar-width:none;
  border:1px solid var(--ui-border);
  border-radius:15px!important;
  background:rgba(255,255,255,.76);
  backdrop-filter:blur(12px);
}
#classTabs::-webkit-scrollbar{display:none}
#classTabs button{
  flex:0 0 auto;
  min-width:56px;
  min-height:35px!important;
  padding:6px 13px!important;
  border-radius:10px!important;
}

/* ===== STUDENT DIRECTORY ===== */
#studentList{
  display:grid;
  grid-template-columns:repeat(2,minmax(0,1fr));
  gap:11px!important;
  align-items:stretch;
}
#studentList > *{
  position:relative;
  min-width:0;
  border:1px solid var(--ui-border)!important;
  border-radius:16px!important;
  background:rgba(255,255,255,.96)!important;
  box-shadow:0 3px 14px rgba(15,23,42,.045)!important;
  overflow:hidden;
  transition:transform .16s ease,box-shadow .16s ease,border-color .16s ease;
}
#studentList > *::before{
  content:"";
  position:absolute;
  left:0;top:0;bottom:0;
  width:3px;
  background:linear-gradient(180deg,#2563eb,#06b6d4);
  opacity:.75;
}
#studentList > *:hover{
  transform:translateY(-2px);
  border-color:#bfdbfe!important;
  box-shadow:0 10px 28px rgba(15,23,42,.085)!important;
}

/* Checkbox lebih nyaman */
#studentList input[type="checkbox"]{
  width:21px!important;
  height:21px!important;
  accent-color:var(--ui-primary);
  cursor:pointer;
}

/* Nama siswa lebih tegas */
#studentList [class*="font-semibold"],
#studentList [class*="font-bold"]{
  letter-spacing:-.015em;
}

/* ===== INPUT & SEARCH ===== */
input[type="text"],
input[type="search"],
input[type="number"],
select,
textarea{
  border-radius:12px!important;
  border:1px solid #dbe3ee!important;
  background:rgba(255,255,255,.95)!important;
  min-height:40px;
  box-shadow:0 2px 8px rgba(15,23,42,.025);
}
input:focus,select:focus,textarea:focus{
  border-color:#93c5fd!important;
  box-shadow:0 0 0 3px rgba(37,99,235,.11)!important;
  outline:none!important;
}

/* ===== OUTPUT TAUTAN ===== */
#outputLinkArea{
  border-radius:14px!important;
  border:1px solid #dbe3ee!important;
  background:#f8fafc!important;
  line-height:1.55;
  scrollbar-width:thin;
}

/* ===== MODAL ===== */
.fixed > div{
  border-radius:20px!important;
}
.fixed{
  backdrop-filter:blur(2px);
}

/* ===== VIEW MODE BAR ===== */
#viewModeMenu{
  bottom:12px!important;
}
#viewModeMenu > div{
  padding:4px!important;
  border-radius:16px!important;
  box-shadow:0 10px 30px rgba(15,23,42,.16)!important;
}
#viewModeMenu button{
  min-height:32px!important;
  padding:5px 10px!important;
  font-size:.72rem!important;
}

/* ===== BACKGROUND SEND PANEL ===== */
#bgSendPanel .bg-send-card{
  border:1px solid rgba(226,232,240,.9);
  box-shadow:0 24px 70px rgba(15,23,42,.22);
}

/* ===== DARK MODE ===== */
.dark body{
  background:
    radial-gradient(900px 420px at -5% -10%,rgba(37,99,235,.17),transparent 60%),
    #0f172a;
  color:#e2e8f0;
}
.dark header{
  background:rgba(15,23,42,.88)!important;
  border-bottom-color:#334155;
}
.dark #classTabs{
  background:rgba(15,23,42,.78);
  border-color:#334155;
}
.dark #studentList > *{
  background:rgba(30,41,59,.94)!important;
  border-color:#334155!important;
}
.dark #studentList > *:hover{border-color:#475569!important}
.dark input[type="text"],
.dark input[type="search"],
.dark input[type="number"],
.dark select,
.dark textarea{
  background:#1e293b!important;
  border-color:#475569!important;
  color:#e2e8f0;
}
.dark #outputLinkArea{
  background:#0f172a!important;
  border-color:#334155!important;
}

/* ===== WINDOWS ===== */
@media(min-width:1024px){
  main{max-width:1500px!important}
  #studentList{
    grid-template-columns:repeat(2,minmax(0,1fr));
  }
}

/* ===== TABLET ===== */
@media(min-width:641px) and (max-width:1023px){
  main{padding-left:16px!important;padding-right:16px!important}
  #studentList{grid-template-columns:repeat(2,minmax(0,1fr))}
}

/* ===== HP ===== */
@media(max-width:640px){
  body{font-size:14px}
  header{padding-left:10px!important;padding-right:10px!important}
  main{
    padding-left:10px!important;
    padding-right:10px!important;
    padding-bottom:70px!important;
  }
  #studentList{
    display:block!important;
  }
  #studentList > *{
    margin-bottom:8px;
  }
  #classTabs{
    min-height:45px;
  }
  #classTabs button{
    min-width:50px;
    min-height:34px!important;
    padding:6px 9px!important;
  }
  button{
    min-height:40px!important;
  }
  #viewModeMenu{bottom:7px!important}
  #viewModeMenu > div{max-width:calc(100vw - 16px)}
  #viewModeMenu button{
    min-height:31px!important;
    padding:5px 8px!important;
  }
}

/* ===== FORCED MODES ===== */
html.force-phone main{
  max-width:760px!important;
  margin-left:auto!important;
  margin-right:auto!important;
}
html.force-phone #studentList{display:block!important}
html.force-windows #studentList{
  display:grid!important;
  grid-template-columns:repeat(2,minmax(0,1fr))!important;
}
@media(max-width:700px){
  html.force-windows #studentList{grid-template-columns:1fr!important}
}
</style>

<style id="send-and-class-premium-ui">
/* Kelas: kartu/tab premium */
#classTabs{display:flex!important;flex-wrap:nowrap!important;gap:9px!important;padding:8px!important;border-radius:18px!important;background:linear-gradient(135deg,rgba(255,255,255,.9),rgba(241,245,249,.82))!important;border:1px solid rgba(148,163,184,.22)!important;box-shadow:0 8px 28px rgba(15,23,42,.07)!important;overflow-x:auto!important;scrollbar-width:none!important}
#classTabs::-webkit-scrollbar{display:none}
#classTabs>div{border-radius:14px!important;overflow:hidden!important;background:transparent!important;box-shadow:none!important}
#classTabs button{position:relative!important;min-width:78px!important;padding:11px 14px!important;border:1px solid transparent!important;border-radius:13px!important;font-size:12px!important;font-weight:800!important;letter-spacing:.15px!important;box-shadow:none!important;background:rgba(255,255,255,.8)!important;color:#475569!important}
#classTabs button:hover{transform:translateY(-2px)!important;box-shadow:0 8px 18px rgba(37,99,235,.14)!important}
#classTabs button[onclick*="switchClass"]:has(+ *){}
.dark #classTabs{background:linear-gradient(135deg,rgba(30,41,59,.94),rgba(15,23,42,.94))!important;border-color:rgba(148,163,184,.16)!important}
.dark #classTabs button{background:rgba(30,41,59,.92)!important;color:#cbd5e1!important}
/* Aktif mengikuti class Tailwind yang sudah dihasilkan renderClassTabs */
#classTabs button.bg-indigo-600{background:linear-gradient(135deg,#2563eb,#4f46e5)!important;color:#fff!important;border-color:rgba(255,255,255,.18)!important;box-shadow:0 9px 22px rgba(37,99,235,.28)!important}
#classTabs button.bg-indigo-600:after{content:'✓';position:absolute;top:4px;right:7px;font-size:8px;opacity:.8}
/* Panel kirim */
.send-progress-overlay{position:fixed;inset:0;z-index:300;display:none;align-items:center;justify-content:center;padding:18px;background:rgba(2,6,23,.62);backdrop-filter:blur(12px)}
.send-progress-overlay.show{display:flex;animation:sendFadeIn .2s ease}
.send-progress-card{position:relative;width:min(500px,100%);padding:28px 24px 22px;border-radius:28px;background:linear-gradient(145deg,#fff,#f8fafc);box-shadow:0 30px 90px rgba(0,0,0,.30);border:1px solid rgba(255,255,255,.7);overflow:hidden}
.dark .send-progress-card{background:linear-gradient(145deg,#1e293b,#0f172a);border-color:rgba(148,163,184,.16)}
.send-progress-card:before{content:'';position:absolute;width:240px;height:240px;left:50%;top:-170px;transform:translateX(-50%);border-radius:50%;background:rgba(37,99,235,.13);filter:blur(8px)}
.send-progress-close{position:absolute;right:13px;top:13px;width:34px!important;height:34px!important;min-height:34px!important;border-radius:10px!important;background:rgba(148,163,184,.12)!important;color:#64748b!important;z-index:2}
.send-progress-close:disabled{opacity:.35;cursor:not-allowed;transform:none!important}
.send-progress-orbit{width:86px;height:86px;margin:0 auto;position:relative;display:grid;place-items:center}
.send-progress-orbit-ring{position:absolute;inset:0;border-radius:50%;border:3px solid rgba(37,99,235,.12);border-top-color:#2563eb;animation:sendSpin 1s linear infinite}
.send-progress-icon{width:62px;height:62px;border-radius:20px;display:grid;place-items:center;background:linear-gradient(135deg,#2563eb,#4f46e5);color:#fff;font-size:24px;box-shadow:0 12px 30px rgba(37,99,235,.28);animation:sendFloat 1.7s ease-in-out infinite}
.send-progress-kicker{font-size:10px;font-weight:900;letter-spacing:.18em;color:#2563eb}
.send-progress-track{height:12px;margin-top:22px;border-radius:999px;background:#e2e8f0;overflow:hidden;box-shadow:inset 0 2px 4px rgba(15,23,42,.08)}
.dark .send-progress-track{background:#334155}
.send-progress-fill{height:100%;width:0;border-radius:999px;background:linear-gradient(90deg,#2563eb,#06b6d4,#22c55e);background-size:200% 100%;animation:sendGradient 2s linear infinite;transition:width .25s ease}
.send-progress-student{margin-top:14px;padding:12px 14px;border-radius:14px;background:rgba(37,99,235,.07);border:1px solid rgba(37,99,235,.12);font-size:12px;font-weight:700;color:#334155;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.dark .send-progress-student{color:#e2e8f0;background:rgba(37,99,235,.12);border-color:rgba(96,165,250,.15)}
.send-progress-tip{margin-top:12px;font-size:10px;text-align:center;color:#64748b}.dark .send-progress-tip{color:#94a3b8}
.send-summary-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:12px}
.send-summary-item{padding:10px 8px;border-radius:14px;border:1px solid rgba(148,163,184,.18);background:rgba(248,250,252,.9);text-align:center}
.dark .send-summary-item{background:rgba(30,41,59,.72);border-color:rgba(148,163,184,.16)}
.send-summary-item span{display:block;font-size:9px;font-weight:800;color:#64748b;white-space:nowrap}
.dark .send-summary-item span{color:#94a3b8}
.send-summary-item strong{display:block;font-size:20px;line-height:1.1;margin-top:4px}
.send-summary-item.success strong{color:#16a34a}.send-summary-item.failed strong{color:#dc2626}.send-summary-item.pending strong{color:#d97706}
@media(max-width:640px){.send-summary-grid{gap:6px}.send-summary-item{padding:9px 5px}.send-summary-item span{font-size:8px}.send-summary-item strong{font-size:18px}}

@keyframes sendSpin{to{transform:rotate(360deg)}}@keyframes sendFloat{50%{transform:translateY(-4px) scale(1.03)}}@keyframes sendGradient{to{background-position:200% 0}}@keyframes sendFadeIn{from{opacity:0;transform:scale(.98)}to{opacity:1;transform:scale(1)}}
@media(max-width:640px){#classTabs button{min-width:72px!important;padding:10px 12px!important;font-size:11px!important}.send-progress-card{padding:25px 18px 18px;border-radius:24px}.send-progress-student{font-size:11px}}
</style>

<style id="premium-class-send-ui">
#classTabs{display:grid!important;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));gap:10px!important;padding:10px!important;background:linear-gradient(135deg,rgba(248,250,252,.96),rgba(239,246,255,.96))!important;border:1px solid rgba(148,163,184,.18)!important;border-radius:22px!important;box-shadow:0 10px 30px rgba(15,23,42,.07)!important}
#classTabs>div{display:block!important}
#classTabs button{position:relative!important;width:100%!important;min-height:68px!important;padding:10px 8px!important;border-radius:16px!important;border:1px solid rgba(148,163,184,.20)!important;background:linear-gradient(145deg,#fff,#f8fafc)!important;color:#334155!important;box-shadow:0 5px 14px rgba(15,23,42,.07)!important;transition:.2s ease!important;overflow:hidden!important}
#classTabs button:before{content:'';position:absolute;left:0;top:0;width:5px;height:100%;background:linear-gradient(180deg,#60a5fa,#6366f1);opacity:.35}
#classTabs button:hover{transform:translateY(-3px) scale(1.01)!important;box-shadow:0 12px 24px rgba(37,99,235,.15)!important}
#classTabs button.bg-indigo-600{background:linear-gradient(145deg,#2563eb,#4f46e5)!important;color:#fff!important;border-color:transparent!important;box-shadow:0 12px 28px rgba(37,99,235,.32)!important;transform:translateY(-2px)!important}
#classTabs button.bg-indigo-600:before{background:#fff!important;opacity:.7}
.dark #classTabs{background:linear-gradient(135deg,rgba(15,23,42,.96),rgba(30,41,59,.96))!important}
.dark #classTabs button{background:linear-gradient(145deg,#1e293b,#0f172a)!important;color:#cbd5e1!important;border-color:rgba(148,163,184,.15)!important}
.dark #classTabs button.bg-indigo-600{background:linear-gradient(145deg,#2563eb,#4f46e5)!important;color:#fff!important}
.send-retry-btn{display:none!important;margin-top:12px;width:100%;border:0;border-radius:13px;padding:11px 14px;font-weight:800;color:#fff;background:linear-gradient(135deg,#f59e0b,#ea580c);box-shadow:0 8px 20px rgba(234,88,12,.22);cursor:pointer;transition:.2s}
.send-retry-btn.show{display:block!important}.send-retry-btn:hover{transform:translateY(-1px);filter:brightness(1.04)}
.send-complete-badge{display:none;margin-top:12px;padding:9px 12px;border-radius:12px;background:rgba(16,185,129,.10);color:#059669;font-size:12px;font-weight:800;text-align:center}.send-complete-badge.show{display:block}
@media(max-width:640px){#classTabs{grid-template-columns:repeat(2,minmax(0,1fr))!important;gap:8px!important;padding:8px!important}#classTabs button{min-height:64px!important;border-radius:14px!important;font-size:.82rem!important}}
</style>
</head>
<body class="bg-gray-50 dark:bg-gray-900 text-gray-800 dark:text-gray-100 h-full flex flex-col transition-colors duration-200">

    <!-- Header -->
    <header class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 shadow-sm py-4 px-4 sm:px-6 flex flex-wrap justify-between items-center gap-4">
        <div class="flex items-center space-x-3">
            <div class="bg-indigo-600 text-white p-2.5 rounded-xl shadow-md">
                <i class="fa-solid fa-school text-xl"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold tracking-tight text-gray-900 dark:text-white">Presensi Kehadiran SMAN 2 Nusa</h1>
                <p class="text-xs text-gray-500 dark:text-gray-400">Pilih siswa per kelas, tambah/edit data, dan kelola tautan otomatis</p>
            </div>
        </div>
        
        <div class="flex items-center flex-wrap gap-2">
            <button onclick="openSettingsPanel()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-slate-700 text-white hover:bg-slate-800 shadow-sm transition flex items-center gap-1.5" title="Pengaturan aplikasi">
                <i class="fa-solid fa-gear"></i>
                <span>Pengaturan</span>
            </button>
            <button onclick="openResultsSheet()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-amber-500 text-white hover:bg-amber-600 shadow-sm transition flex items-center gap-1.5" title="Lihat dashboard hasil presensi"><i class="fa-solid fa-chart-pie"></i><span>Lihat Hasil</span></button>
            <button onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition" title="Ganti Tema">
                <i class="fa-solid fa-moon dark:hidden"></i>
                <i class="fa-solid fa-sun hidden dark:block text-yellow-400"></i>
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6 overflow-y-auto">

        <!-- Notification Banner -->
        <div id="alertBox" class="col-span-12 hidden bg-indigo-50 dark:bg-indigo-950/60 border border-indigo-200 dark:border-indigo-800 text-indigo-800 dark:text-indigo-200 px-4 py-3 rounded-xl flex items-center justify-between text-sm shadow-sm transition-all">
            <div class="flex items-center space-x-2">
                <i class="fa-solid fa-circle-info text-indigo-500"></i>
                <span id="alertText">Pesan peringatan.</span>
            </div>
            <button onclick="hideAlert()" class="text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 font-bold">&times;</button>
        </div>

        <!-- Kolom Kiri: Daftar Siswa Berdasarkan Kelas & Pengaturan Tautan -->
        <div class="lg:col-span-7 flex flex-col gap-6">
            <!-- Bagian Pemilihan Siswa Per Kelas -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4 flex-1">
                
                <div class="flex flex-wrap justify-between items-center gap-2 border-b border-gray-100 dark:border-gray-700 pb-3">
                    <h2 class="font-semibold text-sm flex items-center gap-2">
                        <i class="fa-solid fa-users text-indigo-500"></i> Direktori Siswa & Klasifikasi Kelas
                    </h2>
                    <div class="flex items-center gap-2">
                        <button type="button" onclick="selectAll(true)" class="px-3 py-1.5 text-xs font-medium rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition" title="Pilih semua siswa pada kelas yang sedang ditandai/aktif">Pilih Semua</button>
<button type="button" id="btnKosongkanSemua" onclick="kosongkanSemuaPilihan()"
  class="px-3 py-2 rounded-xl bg-amber-500 hover:bg-amber-600 text-white font-semibold shadow-sm"
  title="Hapus semua pilihan siswa dari seluruh kelas">
  <i class="fa-solid fa-eraser mr-1"></i> Kosongkan
</button>


                    </div>
                </div>

                <!-- Tab Kelas Selector -->
                <div id="classTabs" class="flex flex-wrap gap-2 items-center">
                    <!-- Dinamis via JS -->
                </div>

                <!-- Filter & Search Bar -->
                <div class="relative">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-xs text-gray-400"></i>
                    <input type="text" id="searchInput" oninput="renderStudentList()" placeholder="Cari nama, NIS, atau NISN siswa..." class="w-full pl-8 pr-3 py-2 text-xs rounded-xl border border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-900 focus:ring-2 focus:ring-indigo-500 focus:outline-none transition">
                </div>

                <!-- Kontainer Info Daftar Siswa -->
                <div class="flex justify-between items-center text-xs text-gray-500 px-1">
                    <span id="activeClassTitle" class="font-bold text-gray-700 dark:text-gray-300">Kelas XA</span>
                    <span id="classSelectedCount">0 terpilih di kelas ini</span>
                </div>

                <!-- Scrollable Student List -->
                <div id="studentListContainer" class="min-h-[260px] max-h-[380px] overflow-y-auto border border-gray-100 dark:border-gray-700 rounded-xl p-3 bg-gray-50/50 dark:bg-gray-900/50 flex flex-col gap-2">
                    <!-- Dinamis via JS -->
                </div>
            </div>

        </div>

        <!-- MENU PRESENSI KHUSUS -->
        <div class="lg:col-span-5 bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-3">
            <div class="flex flex-col border-b border-gray-100 dark:border-gray-700 pb-3">
                <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                    <i class="fa-solid fa-bars-staggered text-indigo-500"></i> Menu Presensi Khusus
                </h2>
                <span class="text-[11px] text-gray-500 dark:text-gray-400 mt-1">Pilih jenis presensi khusus untuk membuka formulir terkait.</span>
            </div>
            <div class="grid grid-cols-2 gap-3 mt-1">
                <a href="https://forms.gle/c4dMAXtYNpahjm4F8" target="_blank" rel="noopener noreferrer" class="presensi-khusus-btn bg-blue-500 hover:bg-blue-600">
                    <i class="fa-solid fa-bed-pulse"></i><span>SAKIT</span>
                </a>
                <a href="https://forms.gle/sQYzvpgkqvaqeY1q6" target="_blank" rel="noopener noreferrer" class="presensi-khusus-btn bg-yellow-500 hover:bg-yellow-600">
                    <i class="fa-solid fa-envelope-open-text"></i><span>IZIN</span>
                </a>
                <a href="https://forms.gle/AGDTUVeq7MmFkSV38" target="_blank" rel="noopener noreferrer" class="presensi-khusus-btn bg-orange-500 hover:bg-orange-600">
                    <i class="fa-solid fa-person-running"></i><span>TERLAMBAT</span>
                </a>
                <a href="https://forms.gle/XHoob5yMRTac19y9A" target="_blank" rel="noopener noreferrer" class="presensi-khusus-btn bg-red-500 hover:bg-red-600">
                    <i class="fa-solid fa-user-xmark"></i><span>BOLOS</span>
                </a>
            </div>
        </div>

        <!-- Ringkasan Data Siswa Terpilih -->
        <div class="lg:col-span-5 flex flex-col gap-6">
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4">
                <div class="flex items-center justify-between border-b border-gray-100 dark:border-gray-700 pb-3">
                    <div>
                        <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                            <i class="fa-solid fa-circle-check text-emerald-500"></i> Data Siswa Terpilih
                        </h2>
                        <p class="text-[11px] text-gray-400 mt-1">Keterangan jumlah siswa yang sedang dipilih.</p>
                    </div>
                    <span id="totalSelectedBadge" class="bg-indigo-100 dark:bg-indigo-900/50 text-indigo-700 dark:text-indigo-300 px-2.5 py-1 rounded-full text-xs font-bold">0 Siswa</span>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div class="rounded-xl bg-indigo-50 dark:bg-indigo-950/40 border border-indigo-100 dark:border-indigo-900/50 p-4">
                        <span class="text-[10px] text-gray-500 dark:text-gray-400 block">Total Terpilih</span>
                        <span id="totalSelectedCount" class="text-2xl font-extrabold text-indigo-600 dark:text-indigo-400">0</span>
                        <span class="text-[10px] text-gray-500 dark:text-gray-400 block">siswa</span>
                    </div>
                    <div class="rounded-xl bg-slate-50 dark:bg-slate-900/50 border border-slate-100 dark:border-slate-700 p-4">
                        <span class="text-[10px] text-gray-500 dark:text-gray-400 block">Kelas Aktif</span>
                        <span id="selectedActiveClassCount" class="text-2xl font-extrabold text-slate-700 dark:text-slate-200">0</span>
                        <span class="text-[10px] text-gray-500 dark:text-gray-400 block">terpilih</span>
                    </div>
                </div>

                <div class="rounded-xl bg-gray-50 dark:bg-gray-900/60 border border-gray-100 dark:border-gray-800 p-4 text-xs">
                    <div class="flex justify-between gap-3 py-1">
                        <span class="text-gray-500 dark:text-gray-400">Total siswa terdaftar</span>
                        <b id="statTotalStudents" class="text-gray-700 dark:text-gray-200">0</b>
                    </div>
                    <div class="flex justify-between gap-3 py-1">
                        <span class="text-gray-500 dark:text-gray-400">Total kelas</span>
                        <b id="statTotalClasses" class="text-gray-700 dark:text-gray-200">0</b>
                    </div>
                </div>

                <button type="button" id="btnKirimSemuaData"
                  onclick="kirimSemuaData()"
                  class="w-full px-4 py-3 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-bold shadow-sm transition flex items-center justify-center gap-2"
                  title="Kirim data siswa terpilih tanpa membuka tab baru">
                  <i class="fa-solid fa-paper-plane"></i> Kirim Semua Data
                </button>
            </div>
        </div>

    </main>

    <!-- Modal Tambah / Edit Siswa -->
    <div id="studentModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-md w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <h3 id="studentModalTitle" class="font-bold text-base text-gray-800 dark:text-gray-100">Tambah Siswa Baru</h3>
                <button onclick="closeStudentModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg">&times;</button>
            </div>

            <form id="studentForm" onsubmit="handleSaveStudent(event)" class="flex flex-col gap-3 text-xs">
                <input type="hidden" id="editOriginalClass">
                <input type="hidden" id="editOriginalId">

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Kelas Target</label>
                    <select id="modalStudentClass" required class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                        <!-- Populated dynamically -->
                    </select>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">NIS (ID Unik)</label>
                        <input type="text" id="modalStudentId" required placeholder="Contoh: 260120" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                    </div>
                    <div>
                        <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">NISN</label>
                        <input type="text" id="modalStudentNisn" required placeholder="Contoh: 0105432109" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                    </div>
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Nama Lengkap Siswa</label>
                    <input type="text" id="modalStudentName" required placeholder="Contoh: AHMAD FAUZI" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Jenis Kelamin</label>
                    <select id="modalStudentGender" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                        <option value="LAKI-LAKI">LAKI-LAKI</option>
                        <option value="PEREMPUAN">PEREMPUAN</option>
                    </select>
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Tautan Presensi (Opsional)</label>
                    <input type="url" id="modalStudentLink" placeholder="Biarkan kosong untuk menggunakan tautan default kelas" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div class="flex justify-end gap-2 pt-3 border-t border-gray-100 dark:border-gray-700">
                    <button type="button" onclick="closeStudentModal()" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                    <button type="submit" class="px-4 py-2 rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 font-semibold transition">Simpan Data</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Input Siswa Massal -->
    <div id="bulkStudentModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-3xl w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <div>
                    <h3 class="font-bold text-base text-gray-800 dark:text-gray-100">Input Data Siswa Secara Massal</h3>
                    <p class="text-[11px] text-gray-400 mt-1">Masukkan banyak siswa sekaligus dengan format NIS, NISN, Nama, Jenis Kelamin.</p>
                </div>
                <button onclick="closeBulkStudentModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg">&times;</button>
            </div>

            <div class="flex flex-col gap-3 text-xs">
                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Kelas Target</label>
                    <select id="bulkStudentClass" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-violet-500 focus:outline-none"></select>
                </div>

                <div class="bg-violet-50 dark:bg-violet-950/30 border border-violet-100 dark:border-violet-900 rounded-xl p-3 text-[11px] text-violet-800 dark:text-violet-200">
                    <b>Format:</b> satu siswa per baris dengan urutan
                    <code>NIS[TAB]NISN[TAB]NAMA[TAB]JENIS KELAMIN</code>.
                    Bisa langsung <b>copy-paste dari Excel/Google Sheets</b>.
                    Pemisah <b>tab</b>, titik koma (<b>;</b>), atau koma (<b>,</b>) juga didukung.
                    <br><b>Contoh:</b> 260120[TAB]0101234567[TAB]AHMAD FAUZI[TAB]LAKI-LAKI
                </div>

                <textarea id="bulkStudentData" rows="12" spellcheck="false"
                    placeholder="260120&#9;0101234567&#9;AHMAD FAUZI&#9;LAKI-LAKI
260121&#9;0101234568&#9;BUDI SANTOSO&#9;LAKI-LAKI
260122&#9;0101234569&#9;SITI AISYAH&#9;PEREMPUAN"
                    class="w-full p-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs font-mono focus:ring-2 focus:ring-violet-500 focus:outline-none resize-y"></textarea>

                <div class="flex items-center justify-between gap-2">
                    <button type="button" onclick="fillBulkExample()" class="px-3 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">
                        Contoh Format
                    </button>
                    <div class="flex gap-2">
                        <button type="button" onclick="closeBulkStudentModal()" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                        <button type="button" onclick="handleBulkSaveStudents()" class="px-4 py-2 rounded-xl bg-violet-600 text-white hover:bg-violet-700 font-semibold transition">
                            Simpan Semua Siswa
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Tambah Kelas -->
    <div id="classModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <h3 class="font-bold text-base text-gray-800 dark:text-gray-100">Tambah Kelas Baru</h3>
                <button onclick="closeClassModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg">&times;</button>
            </div>

            <form onsubmit="handleSaveClass(event)" class="flex flex-col gap-3 text-xs">
                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Nama Kelas Baru</label>
                    <input type="text" id="newClassNameInput" required placeholder="Contoh: Kelas XE atau Kelas XI-IPA 1" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div class="flex justify-end gap-2 pt-3 border-t border-gray-100 dark:border-gray-700">
                    <button type="button" onclick="closeClassModal()" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                    <button type="submit" class="px-4 py-2 rounded-xl bg-emerald-600 text-white hover:bg-emerald-700 font-semibold transition">Tambah Kelas</button>
                </div>
            </form>
        </div>
    </div>



    <!-- Modal Konfirmasi Hapus -->
    <div id="confirmModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4 text-center">
            <div class="w-12 h-12 bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 rounded-full flex items-center justify-center mx-auto text-xl">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <h3 id="confirmTitle" class="font-bold text-base text-gray-800 dark:text-gray-100">Konfirmasi Hapus</h3>
            <p id="confirmMessage" class="text-xs text-gray-500 dark:text-gray-400">Apakah Anda yakin ingin menghapus data ini?</p>

            <div class="flex justify-center gap-3 pt-2">
                <button onclick="closeConfirmModal()" class="px-4 py-2 text-xs rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                <button id="confirmExecuteBtn" class="px-4 py-2 text-xs rounded-xl bg-red-600 text-white hover:bg-red-700 font-semibold transition">Ya, Hapus</button>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="text-center py-4 text-xs text-gray-400 dark:text-gray-500 border-t border-gray-200 dark:border-gray-700">
        Presensi Kehadiran SMAN 2 Nusa &bull; Sistem Pengelola Data & Tautan Siswa
    </footer>

    <!-- Script Logika Aplikasi -->
    <script>
        const initialSchoolData = {
    "Kelas XA": [
        {
            "id": "260004",
            "nisn": "0106148762",
            "name": "ABDUL WAHIP",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ABDUL+WAHIP&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260010",
            "nisn": "0107923109",
            "name": "ALFON AQUINO SAKA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALFON+AQUINO+SAKA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260012",
            "nisn": "0105052057",
            "name": "AMANDA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMANDA+PUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260017",
            "nisn": "0118971241",
            "name": "ARAYYA NUR ZAHIRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARAYYA+NUR+ZAHIRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260019",
            "nisn": "0105469341",
            "name": "ARIL SAHRUL RAMADANI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARIL+SAHRUL+RAMADANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260024",
            "nisn": "3097712728",
            "name": "ELSYA APRILIA ANTHONY",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ELSYA+APRILIA+ANTHONY&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260030",
            "nisn": "0111628831",
            "name": "FITRIANI XA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FITRIANI+XA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260031",
            "nisn": "0112035176",
            "name": "HADIR JUMANSA PUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HADIR+JUMANSA+PUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260037",
            "nisn": "0101869333",
            "name": "IMAM AMROSI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IMAM+AMROSI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260039",
            "nisn": "0115027428",
            "name": "INDIAN ILYANDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INDIAN+ILYANDA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260046",
            "nisn": "0117832504",
            "name": "KIRANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KIRANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260049",
            "nisn": "0101496080",
            "name": "MHD. ISWANDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MHD.+ISWANDI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260053",
            "nisn": "3103877484",
            "name": "MUH. ALBAR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+ALBAR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260057",
            "nisn": "0102802885",
            "name": "MUHAMMAD FADLI ADRIANO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FADLI+ADRIANO&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260061",
            "nisn": "0118519658",
            "name": "MUHAMMAD ISRA SYAHPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ISRA+SYAHPUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260065",
            "nisn": "0101834198",
            "name": "MUHAMMAD RESA SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RESA+SAPUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260069",
            "nisn": "3105715277",
            "name": "MUHAMMAD WILDAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+WILDAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260072",
            "nisn": "0098401328",
            "name": "NADA KAMELIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NADA+KAMELIA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260076",
            "nisn": "0108527238",
            "name": "NOVIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NOVIANA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260080",
            "nisn": "0111176983",
            "name": "NUR VEBRIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+VEBRIANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260084",
            "nisn": "0107839346",
            "name": "NURHIKMAH ABDI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURHIKMAH+ABDI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260090",
            "nisn": "0104278399",
            "name": "RASTI PRITA ANDINI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RASTI+PRITA+ANDINI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260092",
            "nisn": "0107010100",
            "name": "REFAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REFAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260098",
            "nisn": "0111191658",
            "name": "REZKY AFANDY",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REZKY+AFANDY&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260101",
            "nisn": "0109392495",
            "name": "SAMSINAR",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAMSINAR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260105",
            "nisn": "0123968886",
            "name": "SITI SAILAH SAPUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SITI+SAILAH+SAPUTRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260109",
            "nisn": "0104154107",
            "name": "SYAHRUL RAMADHANI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYAHRUL+RAMADHANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260110",
            "nisn": "0116564777",
            "name": "WA ODE NURTADAHLIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WA+ODE+NURTADAHLIA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260114",
            "nisn": "0101000649",
            "name": "YAFFA ALENA FAAIZA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YAFFA+ALENA+FAAIZA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260116",
            "nisn": "0104888082",
            "name": "YUNITA HALIMATUN SYA'DIAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YUNITA+HALIMATUN+SYA'DIAH&entry.201529640=HS",
            "selected": false
        }
    ],
    "Kelas XB": [
        {
            "id": "260005",
            "nisn": "0102094669",
            "name": "ADAM ALIF RAHMAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADAM+ALIF+RAHMAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260011",
            "nisn": "0116883035",
            "name": "ALI IRSAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALI+IRSAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260014",
            "nisn": "0109930277",
            "name": "ANDI NURHALIZAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+NURHALIZAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260020",
            "nisn": "0119525847",
            "name": "BADAR IBADIN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=BADAR+IBADIN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260021",
            "nisn": "0117889037",
            "name": "DINDA KIRANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DINDA+KIRANA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260025",
            "nisn": "0109248575",
            "name": "ERNI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ERNI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260032",
            "nisn": "0116390313",
            "name": "HAJRIYANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HAJRIYANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260033",
            "nisn": "0103097316",
            "name": "HERUL AGUSTIAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HERUL+AGUSTIAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260040",
            "nisn": "0112728658",
            "name": "INTAN BATRISYIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INTAN+BATRISYIA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260041",
            "nisn": "0107422875",
            "name": "IQBAL IRFANSA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IQBAL+IRFANSA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260047",
            "nisn": "0106837618",
            "name": "MARWAH SYAFITRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MARWAH+SYAFITRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260054",
            "nisn": "0101515411",
            "name": "MUH. UMARSYAM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+UMARSYAM&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260050",
            "nisn": "3100506286",
            "name": "MOHAMMAD IRWAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOHAMMAD+IRWAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260058",
            "nisn": "0111136908",
            "name": "MUHAMMAD FHAYSAL SYUKUR AHMAD",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FHAYSAL+SYUKUR+AHMAD&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260062",
            "nisn": "0106705459",
            "name": "MUHAMMAD KARIM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+KARIM&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260066",
            "nisn": "0104922371",
            "name": "MUHAMMAD RIFQI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RIFQI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260073",
            "nisn": "0106033650",
            "name": "NANDA ERISKA LIHU",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NANDA+ERISKA+LIHU&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260070",
            "nisn": "0104388826",
            "name": "MULTAZAM NISYAM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MULTAZAM+NISYAM&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260077",
            "nisn": "0109625541",
            "name": "NUR ANISA RAMADAN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+ANISA+RAMADAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260081",
            "nisn": "0116968436",
            "name": "NURAIRAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURAIRAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260085",
            "nisn": "0113740296",
            "name": "NURUL SAFIKAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURUL+SAFIKAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260091",
            "nisn": "0117058653",
            "name": "RATU RAMAYANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RATU+RAMAYANA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260093",
            "nisn": "0104116976",
            "name": "REIVAN ARADILA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REIVAN+ARADILA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260099",
            "nisn": "0104428616",
            "name": "RIFALDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIFALDI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260102",
            "nisn": "3114740852",
            "name": "SASKIA AMANDA WULANDARI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SASKIA+AMANDA+WULANDARI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260106",
            "nisn": "0119225802",
            "name": "SITY NUR CAHYA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SITY+NUR+CAHYA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260111",
            "nisn": "3112662330",
            "name": "WAFRI THALITA ZAINUN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WAFRI+THALITA+ZAINUN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260115",
            "nisn": "0103410698",
            "name": "YOFARNO YOSAFAI RATU LUBUR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YOFARNO+YOSAFAI+RATU+LUBUR&entry.201529640=HS",
            "selected": false
        }
    ],
    "Kelas XC": [
        {
            "id": "260003",
            "nisn": "0116790414",
            "name": "A. NURFARIDAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=A.+NURFARIDAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260006",
            "nisn": "3111658883",
            "name": "AFIKA ADELIA SIREGAR",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AFIKA+ADELIA+SIREGAR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260008",
            "nisn": "0115123543",
            "name": "AHMAD ANGGA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AHMAD+ANGGA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260013",
            "nisn": "0119993291",
            "name": "AMMAR FAIQ HAWRIEL ADNAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMMAR+FAIQ+HAWRIEL+ADNAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260015",
            "nisn": "0113593653",
            "name": "ANDI NURUL SHAZIRAWATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+NURUL+SHAZIRAWATI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260022",
            "nisn": "0115190109",
            "name": "EGY DESTRI AMALIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=EGY+DESTRI+AMALIA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260026",
            "nisn": "0107565355",
            "name": "FALDIANZAH TAUFIK NUR HIDAYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FALDIANZAH+TAUFIK+NUR+HIDAYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260027",
            "nisn": "0107224310",
            "name": "FAUZIAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FAUZIAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260034",
            "nisn": "0115714284",
            "name": "HIJRIYANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HIJRIYANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260035",
            "nisn": "0118616933",
            "name": "HIKMAL MARUDDANI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HIKMAL+MARUDDANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260042",
            "nisn": "0111180220",
            "name": "IZMI AULIA ARHAM",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IZMI+AULIA+ARHAM&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260043",
            "nisn": "0102119722",
            "name": "KAKA ARBI GILARDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KAKA+ARBI+GILARDI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260048",
            "nisn": "0105220301",
            "name": "MARWANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MARWANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260051",
            "nisn": "0101797683",
            "name": "MOHAMMAD REZA R. LIHU",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOHAMMAD+REZA+R.+LIHU&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260055",
            "nisn": "0105499299",
            "name": "MUHAMMAD AIDIL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+AIDIL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260059",
            "nisn": "0107742019",
            "name": "MUHAMMAD FIKRAM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FIKRAM&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260063",
            "nisn": "0107664477",
            "name": "MUHAMMAD RAMADHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RAMADHAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260067",
            "nisn": "0109751609",
            "name": "MUHAMMAD SYAFIAN MONE",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SYAFIAN+MONE&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260074",
            "nisn": "0111950492",
            "name": "NIDHIFAH NAYLAH SAPUTRY",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NIDHIFAH+NAYLAH+SAPUTRY&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260078",
            "nisn": "0111695633",
            "name": "NUR HAFIZA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+HAFIZA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260082",
            "nisn": "0103516333",
            "name": "NURFADILA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURFADILA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260086",
            "nisn": "0095554229",
            "name": "PUTRI ANGRENI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+ANGRENI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260088",
            "nisn": "0105946200",
            "name": "RAHMAT REZKY HIDAYAT",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RAHMAT+REZKY+HIDAYAT&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260094",
            "nisn": "3112122465",
            "name": "REIZA HAMZAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REIZA+HAMZAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260095",
            "nisn": "0102337788",
            "name": "RENITA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RENITA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260107",
            "nisn": "0119619702",
            "name": "ST.RAHMAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ST.RAHMAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260103",
            "nisn": "0104451032",
            "name": "SEKAR WANGI RAHMADINI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SEKAR+WANGI+RAHMADINI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260112",
            "nisn": "0107736381",
            "name": "WANDA NOVI AULIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WANDA+NOVI+AULIA&entry.201529640=HS",
            "selected": true
        }
    ],
    "Kelas XD": [
        {
            "id": "260007",
            "nisn": "0108884814",
            "name": "AFRAH FATHANIA PRABA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AFRAH+FATHANIA+PRABA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260009",
            "nisn": "0109166563",
            "name": "AKBAR MAULANA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AKBAR+MAULANA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260016",
            "nisn": "0111791555",
            "name": "ANISA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANISA+PUTRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260018",
            "nisn": "0108722663",
            "name": "ARHAM NURWAHID",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARHAM+NURWAHID&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260023",
            "nisn": "0106033839",
            "name": "ELSA HANDAYANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ELSA+HANDAYANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260028",
            "nisn": "0116745293",
            "name": "FEBRIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FEBRIANSYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260029",
            "nisn": "0108662406",
            "name": "FITRIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FITRIANI+X-D&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260036",
            "nisn": "0112586711",
            "name": "ILMANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ILMANSYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260038",
            "nisn": "0107462839",
            "name": "INDAYANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INDAYANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260044",
            "nisn": "0106940038",
            "name": "KAKA IBRA GILARDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KAKA+IBRA+GILARDI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260045",
            "nisn": "3101143313",
            "name": "KARMILA SYAHRINA SAPUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KARMILA+SYAHRINA+SAPUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260052",
            "nisn": "0105410277",
            "name": "MUH AIDIN ROIHAN AL FURQAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH+AIDIN+ROIHAN+AL+FURQAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260056",
            "nisn": "0111414121",
            "name": "MUHAMMAD ARDIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ARDIANSYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260060",
            "nisn": "0118399845",
            "name": "MUHAMMAD IQBAL MULIYADI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+IQBAL+MULIYADI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260064",
            "nisn": "0119799802",
            "name": "MUHAMMAD REEFAN BASTIAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+REEFAN+BASTIAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260068",
            "nisn": "0108012631",
            "name": "MUHAMMAD SYAFIQ",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SYAFIQ&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260071",
            "nisn": "0107544031",
            "name": "MUSFIRA RAMADANI MARMAN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUSFIRA+RAMADANI+MARMAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260075",
            "nisn": "0108546784",
            "name": "NOVI AMELIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NOVI+AMELIA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260079",
            "nisn": "0105691485",
            "name": "NUR HAISA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+HAISA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260083",
            "nisn": "0103802830",
            "name": "NURHAFIZA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURHAFIZA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260087",
            "nisn": "0101679788",
            "name": "PUTRI NABILA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+NABILA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260089",
            "nisn": "3084790876",
            "name": "RASMAN RAM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RASMAN+RAM&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260096",
            "nisn": "0107266947",
            "name": "REVARINDI TINDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REVARINDI+TINDA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260097",
            "nisn": "0109887410",
            "name": "REZA AGUNGTAMA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REZA+AGUNGTAMA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260100",
            "nisn": "3110853510",
            "name": "RIZKI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIZKI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260104",
            "nisn": "0105182137",
            "name": "SELVIA RAHMADANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SELVIA+RAHMADANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260108",
            "nisn": "0111290947",
            "name": "SYAHRINI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYAHRINI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260113",
            "nisn": "0106354045",
            "name": "WULAN SAFITRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WULAN+SAFITRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260117",
            "nisn": "0104920937",
            "name": "ZASKIA SULISTYAWATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZASKIA+SULISTYAWATI&entry.201529640=HS",
            "selected": true
        }
    ],
    "Kelas XIA": [
        {
            "id": "250006",
            "nisn": "0097492386",
            "name": "A. ASYURA IBTISAMAH ANNUR",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=A.+ASYURA+IBTISAMAH+ANNUR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250014",
            "nisn": "0092443821",
            "name": "AKGLENSIA SIMON SOLON",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AKGLENSIA+SIMON+SOLON&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250017",
            "nisn": "0094550813",
            "name": "ALIF SYAFAR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALIF+SYAFAR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250018",
            "nisn": "0102444480",
            "name": "ALISA LANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALISA+LANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250022",
            "nisn": "0094181282",
            "name": "ANDI ATIQAH ZYAFIRA MAWAN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+ATIQAH+ZYAFIRA+MAWAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250025",
            "nisn": "0102988633",
            "name": "ANDI SYIFA ROCHIDAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+SYIFA+ROCHIDAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250028",
            "nisn": "0104444256",
            "name": "ANGGI ANGREINI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANGGI+ANGREINI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250031",
            "nisn": "0084781778",
            "name": "ARNIS RAMADANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARNIS+RAMADANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250032",
            "nisn": "0109823116",
            "name": "ASRIANA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ASRIANA+PUTRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250033",
            "nisn": "0104233399",
            "name": "ASSYFA TRIQANAYA ISRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ASSYFA+TRIQANAYA+ISRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250034",
            "nisn": "0094891693",
            "name": "ASTI KRISMAWATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ASTI+KRISMAWATI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250035",
            "nisn": "0107213702",
            "name": "BILAL PUTRA SYAWAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=BILAL+PUTRA+SYAWAL&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250042",
            "nisn": "0095736168",
            "name": "DIHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DIHAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250049",
            "nisn": "0105716068",
            "name": "FITRIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FITRIANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250050",
            "nisn": "0107340111",
            "name": "HANIFA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HANIFA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250060",
            "nisn": "0091637614",
            "name": "M. AIDIL FITRA RAMADHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=M.+AIDIL+FITRA+RAMADHAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250063",
            "nisn": "0106857190",
            "name": "MEISYARA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MEISYARA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250078",
            "nisn": "0106302571",
            "name": "MUHAMMAD ASHAR TIRO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ASHAR+TIRO&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250081",
            "nisn": "0108959367",
            "name": "MUHAMMAD JUMALDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+JUMALDI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250079",
            "nisn": "0091351028",
            "name": "MUHAMMAD ASRAF",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ASRAF&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250092",
            "nisn": "0108275929",
            "name": "NIKITA NURSYAFIRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NIKITA+NURSYAFIRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250093",
            "nisn": "0123678476",
            "name": "NISRINA JUNIATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NISRINA+JUNIATI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250096",
            "nisn": "0096584140",
            "name": "NUR INTAN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+INTAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250100",
            "nisn": "0108849481",
            "name": "NURFAHIMA RASYID",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURFAHIMA+RASYID&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250102",
            "nisn": "3090573895",
            "name": "NURHASMIDAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURHASMIDAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250103",
            "nisn": "0081968270",
            "name": "NURUL AINSYAFIKAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURUL+AINSYAFIKAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250104",
            "nisn": "0102251540",
            "name": "NURUL SUHAIMAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURUL+SUHAIMAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250105",
            "nisn": "0091504500",
            "name": "PAHRIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PAHRIA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250106",
            "nisn": "0104153418",
            "name": "PANCA ANDRIYANTO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PANCA+ANDRIYANTO&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250112",
            "nisn": "0102421668",
            "name": "RAFIDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RAFIDA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250115",
            "nisn": "0107239195",
            "name": "RANI RINDIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RANI+RINDIANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250118",
            "nisn": "0107996255",
            "name": "RISKA FITRIA ASRYAD",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RISKA+FITRIA+ASRYAD&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250129",
            "nisn": "0106345602",
            "name": "SALWA AZAHRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SALWA+AZAHRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250140",
            "nisn": "0099883545",
            "name": "SYAHWALANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYAHWALANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250141",
            "nisn": "0097143695",
            "name": "SYIFA QOLBUHA MUNAWWAROH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYIFA+QOLBUHA+MUNAWWAROH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250146",
            "nisn": "0097799545",
            "name": "ZAKIYATUN NAFSIAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZAKIYATUN+NAFSIAH&entry.201529640=HS",
            "selected": true
        }
    ],
    "Kelas XIB": [
        {
            "id": "250007",
            "nisn": "0099344528",
            "name": "A. ASTI PRATIWI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=A.+ASTI+PRATIWI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250008",
            "nisn": "0098769202",
            "name": "ADRIAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADRIAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250010",
            "nisn": "0098774254",
            "name": "AGUS SABRANI LAYENDRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AGUS+SABRANI+LAYENDRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250020",
            "nisn": "0103411781",
            "name": "AMIRA MARIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMIRA+MARIANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250023",
            "nisn": "0092326306",
            "name": "ANDI MEGAWATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+MEGAWATI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250036",
            "nisn": "0097363626",
            "name": "DAFA KHAIRULLAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DAFA+KHAIRULLAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250045",
            "nisn": "0109985704",
            "name": "FADHIL ADSYAR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FADHIL+ADSYAR&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250057",
            "nisn": "0105552836",
            "name": "KHAIRUL IKHSAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KHAIRUL+IKHSAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250055",
            "nisn": "3102066273",
            "name": "INTAN NURFAUZIAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INTAN+NURFAUZIAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250061",
            "nisn": "0088633139",
            "name": "MASWIN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MASWIN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250062",
            "nisn": "0107732153",
            "name": "MAYRA ALAMANDA SALSABILA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MAYRA+ALAMANDA+SALSABILA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250065",
            "nisn": "0094537101",
            "name": "MOHAMMAD DERMAWAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOHAMMAD+DERMAWAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250066",
            "nisn": "0095457422",
            "name": "MOHD. FEBRIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOHD.+FEBRIANSYAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250069",
            "nisn": "0097267938",
            "name": "MUH FADILLA FANZA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH+FADILLA+FANZA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250071",
            "nisn": "0102129545",
            "name": "MUH. ALFI SYAHRI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+ALFI+SYAHRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250083",
            "nisn": "0092581616",
            "name": "MUHAMMAD PATIR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+PATIR&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250089",
            "nisn": "0108205390",
            "name": "MUHAMMAD YUSUF DAHANIS SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+YUSUF+DAHANIS+SAPUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250090",
            "nisn": "0088980747",
            "name": "MUHD NABIL AIMAN SHAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHD+NABIL+AIMAN+SHAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250094",
            "nisn": "0093466487",
            "name": "NUR AIN RAMADHANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+AIN+RAMADHANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250095",
            "nisn": "0096968111",
            "name": "NUR HAFIZA XIB",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+HAFIZA+XIB&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250098",
            "nisn": "0094447417",
            "name": "NUR SYAHRANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+SYAHRANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250101",
            "nisn": "0089761491",
            "name": "NURFIYANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURFIYANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250108",
            "nisn": "0093540249",
            "name": "PUTRI DEWI YANTI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+DEWI+YANTI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250110",
            "nisn": "0094123531",
            "name": "PUTRI NABILA XIB",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+NABILA+XIB&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250111",
            "nisn": "0084197654",
            "name": "PUTRI SEPTIANA RAMADHANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+SEPTIANA+RAMADHANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250114",
            "nisn": "0094964080",
            "name": "RAMADHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RAMADHAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250117",
            "nisn": "0109173719",
            "name": "RIRIN AULIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIRIN+AULIA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250119",
            "nisn": "0091817765",
            "name": "ROSMAWATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ROSMAWATI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250120",
            "nisn": "0102319298",
            "name": "RULIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RULIANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250124",
            "nisn": "0096118493",
            "name": "SAHRUL XI-B",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAHRUL+XIB&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250130",
            "nisn": "3108169531",
            "name": "SAMSINAR XI-B",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAMSINAR+XIB&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250131",
            "nisn": "0093062983",
            "name": "SASKIA XI-B",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SASKIA+XIB&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250134",
            "nisn": "0105124428",
            "name": "SISKA AMULFAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SISKA+AMULFAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250135",
            "nisn": "0092734594",
            "name": "SITI NURHIKMAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SITI+NURHIKMAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250136",
            "nisn": "0096203239",
            "name": "SRI AINUN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SRI+AINUN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250142",
            "nisn": "0101718058",
            "name": "SYIFAH SYAFANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYIFAH+SYAFANA&entry.201529640=HS",
            "selected": false
        }
    ],
    "Kelas XIC": [
        {
            "id": "250019",
            "nisn": "0081638119",
            "name": "AMBO UPE",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMBO+UPE&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250021",
            "nisn": "0102785603",
            "name": "ANASTASYA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANASTASYA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250030",
            "nisn": "0104897480",
            "name": "ARIP PRIMA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARIP+PRIMA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250041",
            "nisn": "0094881878",
            "name": "DIAN FAHIRA ZURAJNI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DIAN+FAHIRA+ZURAJNI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250044",
            "nisn": "0091322136",
            "name": "EKAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=EKAL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250047",
            "nisn": "0093518313",
            "name": "FIKRI ALFIANTO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FIKRI+ALFIANTO&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250048",
            "nisn": "0091078860",
            "name": "FITRAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FITRAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250052",
            "nisn": "0105364118",
            "name": "HASNENI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HASNENI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250054",
            "nisn": "0104438363",
            "name": "IMROATUL MUTIAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IMROATUL+MUTIAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250056",
            "nisn": "0101661672",
            "name": "JEFRI ALBUKHARI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=JEFRI+ALBUKHARI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250064",
            "nisn": "0102590137",
            "name": "MOH HAFIZUL SYAID",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOH+HAFIZUL+SYAID&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250068",
            "nisn": "0103056023",
            "name": "MOUDY SALSYA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOUDY+SALSYA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250070",
            "nisn": "0089272656",
            "name": "MUH HAIKAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH+HAIKAL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250072",
            "nisn": "0093427255",
            "name": "MUH. JIBRIL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+JIBRIL&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250073",
            "nisn": "0095050507",
            "name": "MUHAMMAD ADNAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ADNAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250074",
            "nisn": "0094858813",
            "name": "MUHAMMAD ADRIAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ADRIAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250076",
            "nisn": "0129770348",
            "name": "MUHAMMAD ARFIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ARFIANSYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250077",
            "nisn": "0091453110",
            "name": "MUHAMMAD ARKAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ARKAN&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250082",
            "nisn": "0104013885",
            "name": "MUHAMMAD NUR GANI YUSUF",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+NUR+GANI+YUSUF&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250085",
            "nisn": "0103952473",
            "name": "MUHAMMAD REZA HIDAYAT",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+REZA+HIDAYAT&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250086",
            "nisn": "0081463238",
            "name": "MUHAMMAD SYAFIQ MONE",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SYAFIQ+MONE&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250087",
            "nisn": "0098199674",
            "name": "MUHAMMAD SYUKRI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SYUKRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250091",
            "nisn": "0099045572",
            "name": "MUTMAINNAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUTMAINNAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250109",
            "nisn": "0101562884",
            "name": "PUTRI JUPERA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+JUPERA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250121",
            "nisn": "0107581672",
            "name": "RUSTIANA MANDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RUSTIANA+MANDA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250122",
            "nisn": "0107177004",
            "name": "SAHAR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAHAR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250127",
            "nisn": "0099466841",
            "name": "SALDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SALDI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250132",
            "nisn": "0096726908",
            "name": "SHARIFAH ATIKAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SHARIFAH+ATIKAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250133",
            "nisn": "0091417345",
            "name": "SHIIREEN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SHIIREEN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250137",
            "nisn": "0094807679",
            "name": "SRI MULIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SRI+MULIANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250138",
            "nisn": "0097534395",
            "name": "SUSANDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SUSANDI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250147",
            "nisn": "0108401281",
            "name": "ZAKY AHMAD MUSOFFAR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZAKY+AHMAD+MUSOFFAR&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250148",
            "nisn": "0101720889",
            "name": "ZIDAN OKTA PRANATA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZIDAN+OKTA+PRANATA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250149",
            "nisn": "0093186469",
            "name": "ZUL ABADI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZUL+ABADI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260121",
            "nisn": "0108916727",
            "name": "NURHALIZA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURHALIZA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260122",
            "nisn": "0091101952",
            "name": "ARTI AULIYA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARTI+AULIYA&entry.201529640=HS",
            "selected": true
        }
    ],
    "Kelas XID": [
        {
            "id": "250009",
            "nisn": "0105508144",
            "name": "ADRIAN AJ",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADRIAN+AJ&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250011",
            "nisn": "0108980994",
            "name": "AHMAD FARHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AHMAD+FARHAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250012",
            "nisn": "0108831435",
            "name": "AHMAD JUNAIDIL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AHMAD+JUNAIDIL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250013",
            "nisn": "0103000877",
            "name": "AIDIL SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AIDIL+SAPUTRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250015",
            "nisn": "0108954434",
            "name": "ALFIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALFIANSYAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250024",
            "nisn": "0095452407",
            "name": "ANDI REVI MERISKA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+REVI+MERISKA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250026",
            "nisn": "0085625536",
            "name": "ANDIKA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDIKA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250027",
            "nisn": "0084067796",
            "name": "ANEL NOVRIZAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANEL+NOVRIZAL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250029",
            "nisn": "3049396393",
            "name": "ARIMI K GORANG",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARIMI+K+GORANG&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250037",
            "nisn": "0098875445",
            "name": "DESTHY AULIYA RAMADANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DESTHY+AULIYA+RAMADANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250038",
            "nisn": "0109814677",
            "name": "DEWI SELFIANA MUALIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DEWI+SELFIANA+MUALIANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250039",
            "nisn": "0091431226",
            "name": "DHIKA PRATAMA ARDHY",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DHIKA+PRATAMA+ARDHY&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250043",
            "nisn": "0093363357",
            "name": "DIMAS SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DIMAS+SAPUTRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250051",
            "nisn": "0099834003",
            "name": "HASDING",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HASDING&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250059",
            "nisn": "0096621921",
            "name": "LEO NARDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=LEO+NARDI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250075",
            "nisn": "0109828665",
            "name": "MUHAMMAD AKBAR NOVAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+AKBAR+NOVAL&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250080",
            "nisn": "0105190938",
            "name": "MUHAMMAD HAIKAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+HAIKAL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250084",
            "nisn": "0105680915",
            "name": "MUHAMMAD RAFFLY DWI SANTOSO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RAFFLY+DWI+SANTOSO&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250088",
            "nisn": "3085256149",
            "name": "MUHAMMAD YUSUF ADITYA SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+YUSUF+ADITYA+SAPUTRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250097",
            "nisn": "0095854815",
            "name": "NUR NATASYAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+NATASYAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250116",
            "nisn": "0095141120",
            "name": "RIFKI HARDYANTO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIFKI+HARDYANTO&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250123",
            "nisn": "0092651933",
            "name": "SAHRUL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAHRUL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250125",
            "nisn": "0071989228",
            "name": "SAIPUL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAIPUL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250126",
            "nisn": "0094209467",
            "name": "SAKIRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAKIRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250128",
            "nisn": "0101489107",
            "name": "SALSIA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SALSIA+PUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250143",
            "nisn": "0095749423",
            "name": "SYILA AULYA FITRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYILA+AULYA+FITRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "250144",
            "nisn": "0101357837",
            "name": "TIRTA PANJI WINATA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=TIRTA+PANJI+WINATA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250145",
            "nisn": "0091788807",
            "name": "ZAHRA AMELIA BILQIS",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZAHRA+AMELIA+BILQIS&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260001",
            "nisn": "0106702229",
            "name": "MUHAMMAD IBRAHIM ZAKARIAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+IBRAHIM+ZAKARIAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260118",
            "nisn": "0107571376",
            "name": "SASKIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SASKIA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260119",
            "nisn": "0093530060",
            "name": "ANDI FAZRIAN NUR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+FAZRIAN+NUR&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "260120",
            "nisn": "0098057105",
            "name": "ASTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ASTRI&entry.201529640=HS",
            "selected": true
        }
    ],
    "Kelas XIIA": [
        {
            "id": "240003",
            "nisn": "0091191496",
            "name": "AAN SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AAN+SAPUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240004",
            "nisn": "0095334209",
            "name": "ABDI PRATAMA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ABDI+PRATAMA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240009",
            "nisn": "0084112113",
            "name": "AGUNG DZUHRI PRATAMA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AGUNG+DZUHRI+PRATAMA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240011",
            "nisn": "0091892645",
            "name": "AIQAL MUHAMMAD SYAHRIL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AIQAL+MUHAMMAD+SYAHRIL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240013",
            "nisn": "0084072548",
            "name": "AISYAH REMBU KOBORU",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AISYAH+REMBU+KOBORU&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240018",
            "nisn": "0092615517",
            "name": "ANDI KAMAL ABDILLAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+KAMAL+ABDILLAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240023",
            "nisn": "0091447722",
            "name": "APRILIA PRATIWI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=APRILIA+PRATIWI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240024",
            "nisn": "3095581688",
            "name": "APRILLIA SALSABILAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=APRILLIA+SALSABILAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240026",
            "nisn": "0091083800",
            "name": "ARTIKA NURSYIFA ALIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARTIKA+NURSYIFA+ALIA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240028",
            "nisn": "0096663453",
            "name": "ATIKA RAHMAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ATIKA+RAHMAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240030",
            "nisn": "0094648701",
            "name": "AULIA PUTRA SAJIDIN ATMAJA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AULIA+PUTRA+SAJIDIN+ATMAJA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240032",
            "nisn": "3084113291",
            "name": "AYU RAHMA DANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AYU+RAHMA+DANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240033",
            "nisn": "0073285520",
            "name": "BASRI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=BASRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240039",
            "nisn": "0081068230",
            "name": "DIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DIANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240044",
            "nisn": "0087043362",
            "name": "IBNU HANIF RISQI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IBNU+HANIF+RISQI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240047",
            "nisn": "0084361059",
            "name": "IRMISA SYABANI PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IRMISA+SYABANI+PUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240054",
            "nisn": "0082403481",
            "name": "LUTVIA NABILA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=LUTVIA+NABILA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240056",
            "nisn": "0093372955",
            "name": "M. IRWANSYA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=M.+IRWANSYA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240058",
            "nisn": "0081249862",
            "name": "MARIAMA ULFHA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MARIAMA+ULFHA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240059",
            "nisn": "0082897538",
            "name": "MAYLANI FERLIANA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MAYLANI+FERLIANA+PUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240068",
            "nisn": "3099613275",
            "name": "MUH. RAHMAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+RAHMAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240076",
            "nisn": "0091840588",
            "name": "MUHAMMAD HAFIZ RAMADHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+HAFIZ+RAMADHAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240080",
            "nisn": "0093459172",
            "name": "MUHAMMAD RAFLI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RAFLI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240083",
            "nisn": "0082810406",
            "name": "MUHAMMAD TAQWA ALFATIHA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+TAQWA+ALFATIHA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240086",
            "nisn": "0085160184",
            "name": "MUSLINDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUSLINDA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240096",
            "nisn": "0086218744",
            "name": "NUR LAILAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+LAILAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240106",
            "nisn": "3088994773",
            "name": "RESKY ADITYA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RESKY+ADITYA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240109",
            "nisn": "0091153356",
            "name": "RIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240110",
            "nisn": "0087067554",
            "name": "RIFALDY AZANIL ALAM KALLA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIFALDY+AZANIL+ALAM+KALLA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240127",
            "nisn": "0085915382",
            "name": "SULAIMAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SULAIMAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240132",
            "nisn": "0092859675",
            "name": "TRANITA DIRYAWATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=TRANITA+DIRYAWATI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "260002",
            "nisn": "0097480772",
            "name": "RAIHAN TRI BAGASKARA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RAIHAN+TRI+BAGASKARA&entry.201529640=HS",
            "selected": false
        }
    ],
    "Kelas XIIB": [
        {
            "id": "240010",
            "nisn": "0084436280",
            "name": "AHMAD DANI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AHMAD+DANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240012",
            "nisn": "0097963943",
            "name": "AISYAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AISYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240029",
            "nisn": "0081935080",
            "name": "ATTILA WANA RAYA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ATTILA+WANA+RAYA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240031",
            "nisn": "0083398087",
            "name": "AUREL ANGGRAENY RAMADHANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AUREL+ANGGRAENY+RAMADHANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240040",
            "nisn": "0091974486",
            "name": "DWI PRASEDTYO SUPRAMTO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DWI+PRASEDTYO+SUPRAMTO&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240041",
            "nisn": "0085574612",
            "name": "EDWARD NUGROHO PUTRA TEFBANA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=EDWARD+NUGROHO+PUTRA+TEFBANA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240042",
            "nisn": "0096335920",
            "name": "EGI HIDAYAT",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=EGI+HIDAYAT&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "250004",
            "nisn": "0094900328",
            "name": "FARAMASTI ADRIANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FARAMASTI+ADRIANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240049",
            "nisn": "0099402937",
            "name": "JUSRIYANSA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=JUSRIYANSA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240052",
            "nisn": "0086322970",
            "name": "KIKI RISKI AMANDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KIKI+RISKI+AMANDA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240053",
            "nisn": "0091488219",
            "name": "LEDY HERWINDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=LEDY+HERWINDA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240060",
            "nisn": "0082442156",
            "name": "MEGA RISKIA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MEGA+RISKIA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240067",
            "nisn": "0087299320",
            "name": "MUH. FADHIL PANDHITA UGHI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+FADHIL+PANDHITA+UGHI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240072",
            "nisn": "0089505979",
            "name": "MUHAMMAD BAAITS",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+BAAITS&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240075",
            "nisn": "0098166977",
            "name": "M. FAZRI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=M.+FAZRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240078",
            "nisn": "0108050952",
            "name": "MUHAMMAD ILHAM AHMI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ILHAM+AHMI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240092",
            "nisn": "0083732636",
            "name": "NUR AGUS MARLIYANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+AGUS+MARLIYANI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240095",
            "nisn": "0085973638",
            "name": "NUR ASMARANI SYAFITRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+ASMARANI+SYAFITRI&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240100",
            "nisn": "0086506528",
            "name": "PERA YUNITA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PERA+YUNITA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240103",
            "nisn": "0095066598",
            "name": "RABHIEL ARNANDO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RABHIEL+ARNANDO&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240108",
            "nisn": "0097626825",
            "name": "RHEFAYA NUR SYAFIQAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RHEFAYA+NUR+SYAFIQAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240112",
            "nisn": "0099655102",
            "name": "RIFKY ALFIDIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIFKY+ALFIDIANSYAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240114",
            "nisn": "0093361901",
            "name": "RINA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RINA+PUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240115",
            "nisn": "0088494586",
            "name": "RISMA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RISMA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240118",
            "nisn": "0082130561",
            "name": "RYO RAMADHAN HABIBURAHMAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RYO+RAMADHAN+HABIBURAHMAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240119",
            "nisn": "0093307504",
            "name": "SALSABIL ZAHRA ADILLAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SALSABIL+ZAHRA+ADILLAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240120",
            "nisn": "0082073606",
            "name": "SAMSUL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAMSUL&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240124",
            "nisn": "0097754934",
            "name": "SHASTA FRIANY MARANNU",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SHASTA+FRIANY+MARANNU&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240125",
            "nisn": "0089144010",
            "name": "SILFIA RIEKA SHOLEHA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SILFIA+RIEKA+SHOLEHA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240130",
            "nisn": "0099604495",
            "name": "SYARFIKAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYARFIKAH&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240134",
            "nisn": "3089520864",
            "name": "WAHYU RISKY ARYO SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WAHYU+RISKY+ARYO+SAPUTRA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240137",
            "nisn": "3159684046",
            "name": "WULAN SYAFIRAH NUGRAHA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WULAN+SYAFIRAH+NUGRAHA&entry.201529640=HS",
            "selected": true
        },
        {
            "id": "240139",
            "nisn": "0099792794",
            "name": "YULIA NINSI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YULIA+NINSI&entry.201529640=HS",
            "selected": true
        }
    ],
    "Kelas XIIC": [
        {
            "id": "240001",
            "nisn": "0096593916",
            "name": "A. NIA RAMADANI JIHAN P",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=A.+NIA+RAMADANI+JIHAN+P&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240005",
            "nisn": "0094422699",
            "name": "ADELLIA RAHMAN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADELLIA+RAHMAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240006",
            "nisn": "0086034186",
            "name": "ADICA PUTRI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADICA+PUTRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240008",
            "nisn": "0095751661",
            "name": "ADRIAN FIRANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADRIAN+FIRANSYAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240014",
            "nisn": "0081069242",
            "name": "ALDIASMIN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALDIASMIN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240016",
            "nisn": "0097846898",
            "name": "AMALIA ZAHRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMALIA+ZAHRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240017",
            "nisn": "0084954211",
            "name": "AMNUR GUNAWAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMNUR+GUNAWAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240022",
            "nisn": "0084333309",
            "name": "ANISA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANISA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240035",
            "nisn": "0084592653",
            "name": "CACA APRILIYANTI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=CACA+APRILIYANTI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240036",
            "nisn": "0085322415",
            "name": "CINTA LAURA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=CINTA+LAURA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240037",
            "nisn": "0097365585",
            "name": "DANI AHMAD SYARIZAL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DANI+AHMAD+SYARIZAL&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240043",
            "nisn": "0099456718",
            "name": "FAREZZY AHMAD",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FAREZZY+AHMAD&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240045",
            "nisn": "0096431600",
            "name": "IBRAHIM SURYADINATA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IBRAHIM+SURYADINATA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240055",
            "nisn": "0082339379",
            "name": "M. ARFAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=M.+ARFAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240070",
            "nisn": "0081214726",
            "name": "MUHAMMAD ARDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ARDI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240073",
            "nisn": "0097585759",
            "name": "MUHAMMAD BENI WIJAYA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+BENI+WIJAYA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240074",
            "nisn": "0088635463",
            "name": "MUHAMMAD FAJRI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FAJRI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240079",
            "nisn": "0094448545",
            "name": "MUHAMMAD RAFI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RAFI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240084",
            "nisn": "0086125154",
            "name": "MUHAMMAD YUSUF FADLAN HASTA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+YUSUF+FADLAN+HASTA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240094",
            "nisn": "0094729569",
            "name": "NUR ALFIAH",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+ALFIAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240102",
            "nisn": "0085747707",
            "name": "PUTRI KIRANA SYAFRIDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+KIRANA+SYAFRIDA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240104",
            "nisn": "0098604279",
            "name": "RAIHAN SAMJAYA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RAIHAN+SAMJAYA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240121",
            "nisn": "0097681348",
            "name": "SAVI NAMANDASI NIRA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAVI+NAMANDASI+NIRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240126",
            "nisn": "0099544572",
            "name": "ST GHADIA UMMAYYAH SUPRATMAN",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ST+GHADIA+UMMAYYAH+SUPRATMAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240128",
            "nisn": "0086896744",
            "name": "SULTAN HASANUDDIN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SULTAN+HASANUDDIN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240131",
            "nisn": "0081910122",
            "name": "TASYAH PUTRI LESTARI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=TASYAH+PUTRI+LESTARI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240133",
            "nisn": "0087635902",
            "name": "VICTOPER",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=VICTOPER&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240140",
            "nisn": "0074574294",
            "name": "ZULKIFLI SYAHRIL",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZULKIFLI+SYAHRIL&entry.201529640=HS",
            "selected": false
        }
    ],
    "Kelas XIID": [
        {
            "id": "240007",
            "nisn": "0087368234",
            "name": "ADIT SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADIT+SAPUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240002",
            "nisn": "0062254988",
            "name": "ANGGA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANGGA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240149",
            "nisn": "0083094561",
            "name": "ANDINI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDINI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240020",
            "nisn": "0096983283",
            "name": "ANDI MUHAMMAD SYAHBAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+MUHAMMAD+SYAHBAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240046",
            "nisn": "0081730404",
            "name": "IRENA RAHMADHANI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IRENA+RAHMADHANI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240048",
            "nisn": "0082167044",
            "name": "JOVAN OCTAVIAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=JOVAN+OCTAVIAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240057",
            "nisn": "3081176359",
            "name": "M. RAHMAT",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=M.+RAHMAT&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240061",
            "nisn": "0099652380",
            "name": "MIZWAR",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MIZWAR&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240062",
            "nisn": "0089825314",
            "name": "MOH. FAIZ",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOH.+FAIZ&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240063",
            "nisn": "0085419928",
            "name": "MOH. AQIL FAHREZA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOH.+AQIL+FAHREZA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240064",
            "nisn": "0099475207",
            "name": "MUCKLAS SAPUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUCKLAS+SAPUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240066",
            "nisn": "3093166298",
            "name": "MUH RIZKI APRIANSYAH",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH+RIZKI+APRIANSYAH&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240069",
            "nisn": "0076440891",
            "name": "MUHAMMAD ALDO",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ALDO&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240081",
            "nisn": "0083944002",
            "name": "MUHAMMAD RIFAI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RIFAI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240082",
            "nisn": "0883591832",
            "name": "MUHAMMAD SAYID YASIN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SAYID+YASIN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240088",
            "nisn": "0082145228",
            "name": "NIRMALA DEWI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NIRMALA+DEWI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240089",
            "nisn": "0084704907",
            "name": "NISRINA SIFA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NISRINA+SIFA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240090",
            "nisn": "3099019837",
            "name": "NIZAM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NIZAM&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240091",
            "nisn": "0075969238",
            "name": "NOR IMAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NOR+IMAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240097",
            "nisn": "0087572371",
            "name": "NUR SYAFIKA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+SYAFIKA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240098",
            "nisn": "0096003172",
            "name": "NURFIKA AMANDA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURFIKA+AMANDA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240101",
            "nisn": "0096067615",
            "name": "PUTRI DESI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+DESI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240105",
            "nisn": "0089937399",
            "name": "RENDY SAHAM",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RENDY+SAHAM&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240107",
            "nisn": "0087945982",
            "name": "REZA RAMADHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REZA+RAMADHAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240111",
            "nisn": "0088469002",
            "name": "RIFAT NABIHAN",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIFAT+NABIHAN&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240116",
            "nisn": "0099650589",
            "name": "RIZKY TRI PUTRA",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIZKY+TRI+PUTRA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240117",
            "nisn": "0095704016",
            "name": "ROSDIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ROSDIANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240122",
            "nisn": "0079557028",
            "name": "SELVIANA",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SELVIANA&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240129",
            "nisn": "0083157960",
            "name": "SURNIATI",
            "gender": "PEREMPUAN",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SURNIATI&entry.201529640=HS",
            "selected": false
        },
        {
            "id": "240136",
            "nisn": "0058340828",
            "name": "WANDI",
            "gender": "LAKI-LAKI",
            "link": "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WANDI&entry.201529640=HS",
            "selected": false
        }
    ]
};

        let schoolData = {};
        let selectedStudents = {};
        let currentActiveClassName = '';
        let pendingConfirmCallback = null;

        // ===== Lihat Hasil dari Google Spreadsheet =====
        const RESULTS_SHEET_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vR3f_LifCDZ3C341cJYzRbdsJSfRqirIHuD7O7mk-TzyApW36N2bQlRMuZfM0g1BTFdGzDp8W4oFrgq/pubhtml';

        function openResultsSheet() {
            const panel = document.getElementById('resultsDashboardPanel');
            if (!panel) return;
            panel.classList.remove('hidden');
            document.body.classList.add('results-dashboard-open');
            loadResultsDashboard();
        }

        function closeResultsDashboard() {
            const panel = document.getElementById('resultsDashboardPanel');
            if (panel) panel.classList.add('hidden');
            document.body.classList.remove('results-dashboard-open');
        }

        async function loadResultsDashboard() {
            const status = document.getElementById('resultsDashboardStatus');
            if (status) status.textContent = 'Memuat data dari Google Spreadsheet…';
            const endpoint = RESULTS_SHEET_URL.replace('/pubhtml', '/gviz/tq?tqx=out:json');
            try {
                const response = await fetch(endpoint, { cache: 'no-store' });
                if (!response.ok) throw new Error('HTTP ' + response.status);
                const text = await response.text();
                const start = text.indexOf('{');
                const end = text.lastIndexOf('}');
                if (start < 0 || end < start) throw new Error('Format data Google tidak dikenali');
                const data = JSON.parse(text.slice(start, end + 1));
                const rows = (data.table && data.table.rows) || [];
                const counts = {Hadir:0, Sakit:0, Izin:0, Terlambat:0, Bolos:0};
                const aliases = {
                    H:'Hadir', HADIR:'Hadir',
                    S:'Sakit', SAKIT:'Sakit',
                    I:'Izin', IZIN:'Izin',
                    T:'Terlambat', TERLAMBAT:'Terlambat',
                    B:'Bolos', BOLOS:'Bolos'
                };
                rows.forEach(row => {
                    (row.c || []).forEach(cell => {
                        if (!cell) return;
                        const raw = String(cell.f ?? cell.v ?? '').trim().toUpperCase();
                        if (aliases[raw]) counts[aliases[raw]]++;
                    });
                });
                Object.keys(counts).forEach(k => {
                    const el = document.getElementById('resultCount' + k);
                    if (el) el.textContent = counts[k].toLocaleString('id-ID');
                });
                if (status) status.textContent = 'Data berhasil diperbarui · ' + rows.length.toLocaleString('id-ID') + ' baris';
            } catch (err) {
                if (status) status.textContent = 'Tampilan tabel tetap tersedia. Rekap kartu belum dapat dibaca otomatis dari Spreadsheet.';
                console.warn('Dashboard presensi:', err);
            }
        }

        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
        }

        window.addEventListener('DOMContentLoaded', () => {
            loadSchoolData();
            renderClassTabs();
            renderStudentList();
            updateOutputLinks();
            updateStatistics();
        });

        function loadSchoolData() {
            const savedData = localStorage.getItem('sman2_presensi_data_v4');
            if (savedData) {
                try {
                    schoolData = JSON.parse(savedData);
                } catch (e) {
                    schoolData = JSON.parse(JSON.stringify(initialSchoolData));
                }
            } else {
                schoolData = JSON.parse(JSON.stringify(initialSchoolData));
            }

            const classKeys = Object.keys(schoolData);
            if (classKeys.length > 0) {
                if (!currentActiveClassName || !schoolData[currentActiveClassName]) {
                    currentActiveClassName = classKeys[0];
                }
            } else {
                currentActiveClassName = '';
            }

            // Sync selections
            selectedStudents = {};
            Object.keys(schoolData).forEach(className => {
                schoolData[className].forEach(student => {
                    if (student.selected) {
                        selectedStudents[student.id] = true;
                    }
                });
            });
        }

        function saveSchoolData() {
            // Keep student.selected synced with selectedStudents map
            Object.keys(schoolData).forEach(className => {
                schoolData[className].forEach(student => {
                    student.selected = !!selectedStudents[student.id];
                });
            });
            localStorage.setItem('sman2_presensi_data_v4', JSON.stringify(schoolData));
            updateStatistics();
        }

        function resetToDefaultData() {
            showConfirmModal(
                'Reset Data Bawaan',
                'Apakah Anda yakin ingin mengembalikan seluruh data siswa dan kelas ke data awal? Perubahan kustom Anda akan terhapus.',
                () => {
                    localStorage.removeItem('sman2_presensi_data_v4');
                    loadSchoolData();
                    renderClassTabs();
                    renderStudentList();
                    updateOutputLinks();
                    showAlert('Data berhasil dikembalikan ke format awal.');
                }
            );
        }

        function renderClassTabs() {
            const container = document.getElementById('classTabs');
            const classKeys = Object.keys(schoolData || {});
            if (!classKeys.length) {
                container.innerHTML = '<span class="text-xs text-gray-400">Belum ada kelas. Silakan tambah kelas baru.</span>';
                return;
            }
            container.innerHTML = classKeys.map(className => {
                const isActive = className === currentActiveClassName;
                const total = (schoolData[className] || []).length;
                const selected = (schoolData[className] || []).filter(s => !!selectedStudents[s.id]).length;
                const btnClass = isActive ? 'bg-indigo-600 text-white' : 'bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-300';
                return `
                    <div>
                        <button type="button" onclick="switchClass('${String(className).replace(/'/g, "\\'")}')" class="${btnClass}">
                            <div class="flex flex-col items-center justify-center gap-1">
                                <span class="text-sm font-black tracking-wide">${className}</span>
                                <span class="text-[10px] font-semibold opacity-80">${total} siswa${selected ? ` • ${selected} terpilih` : ''}</span>
                            </div>
                        </button>
                    </div>`;
            }).join('');
        }

        function switchClass(className) {
            currentActiveClassName = className;
            document.getElementById('activeClassTitle').textContent = `Kelas ${className}`;
            renderClassTabs();
            renderStudentList();
        }

        function renderStudentList() {
            const container = document.getElementById('studentListContainer');
            const searchKeyword = (document.getElementById('searchInput')?.value || '').toLowerCase().trim();
            const students = schoolData[currentActiveClassName] || [];
            
            let html = '';
            let countSelectedInClass = 0;

            const filteredStudents = students.filter(student => {
                if (!searchKeyword) return true;
                return student.name.toLowerCase().includes(searchKeyword) || 
                       String(student.id ?? '').toLowerCase().includes(searchKeyword) ||
                       String(student.nisn ?? '').toLowerCase().includes(searchKeyword);
            });

            if (filteredStudents.length === 0) {
                container.innerHTML = `
                    <div class="flex flex-col items-center justify-center p-8 text-center text-gray-400">
                        <i class="fa-solid fa-folder-open text-2xl mb-2 opacity-50"></i>
                        <p class="text-xs">Tidak ada data siswa ditemukan.</p>
                    </div>`;
            } else {
                filteredStudents.forEach(student => {
                    const isSelected = !!selectedStudents[student.id];
                    if (isSelected) countSelectedInClass++;

                    const bgClass = isSelected ? 'bg-indigo-50/50 dark:bg-indigo-900/20 border-indigo-200 dark:border-indigo-800' : 'bg-white dark:bg-gray-800 border-gray-100 dark:border-gray-700';
                    const iconClass = isSelected ? 'text-indigo-500' : 'text-gray-300 dark:text-gray-600';
                    const checkIcon = isSelected ? 'fa-solid fa-square-check' : 'fa-regular fa-square';

                    html += `
                        <div class="flex items-center justify-between p-2.5 rounded-xl border shadow-sm transition hover:shadow-md ${bgClass}">
                            <div class="flex items-center gap-3 flex-1 min-w-0 cursor-pointer" onclick="toggleStudentSelection('${student.id}')">
                                <div class="text-lg ${iconClass} transition-colors">
                                    <i class="${checkIcon}"></i>
                                </div>
                                <div class="flex-1 min-w-0">
                                    <div class="flex items-center gap-2">
                                        <h4 class="text-xs font-bold text-gray-800 dark:text-gray-200 truncate" title="${student.name}">${student.name}</h4>
                                        <span class="text-[9px] px-1.5 py-0.5 rounded-md bg-gray-100 dark:bg-gray-700 text-gray-500 truncate">${student.gender === 'LAKI-LAKI' ? 'L' : 'P'}</span>
                                    </div>
                                    <p class="text-[10px] text-gray-500 dark:text-gray-400 truncate">NIS: ${student.id} &bull; NISN: ${student.nisn}</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-1.5 pl-2 border-l border-gray-200 dark:border-gray-700">
                                <a href="${student.link}" target="_blank" onclick="event.stopPropagation()" class="w-7 h-7 flex items-center justify-center rounded-lg bg-indigo-50 text-indigo-600 hover:bg-indigo-100 dark:bg-indigo-900/40 dark:text-indigo-400 dark:hover:bg-indigo-900/60 transition" title="Buka Link">
                                    <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                                </a>
                                <button onclick="openEditStudentModal('${student.id}')" class="w-7 h-7 flex items-center justify-center rounded-lg bg-gray-50 text-gray-600 hover:bg-gray-100 dark:bg-gray-700 dark:text-gray-300 dark:hover:bg-gray-600 transition" title="Edit">
                                    <i class="fa-solid fa-pen text-[10px]"></i>
                                </button>
                                <button onclick="askDeleteStudent('${student.id}')" class="w-7 h-7 flex items-center justify-center rounded-lg bg-red-50 text-red-500 hover:bg-red-100 dark:bg-red-900/20 dark:text-red-400 dark:hover:bg-red-900/40 transition" title="Hapus">
                                    <i class="fa-solid fa-trash text-[10px]"></i>
                                </button>
                            </div>
                        </div>
                    `;
                });
                container.innerHTML = html;
            }

            document.getElementById('classSelectedCount').textContent = `${countSelectedInClass} terpilih di kelas ini`;
        }

        function toggleStudentSelection(id) {
            selectedStudents[id] = !selectedStudents[id];
            saveSchoolData();
            renderStudentList();
            updateOutputLinks();
        }

        function selectAll(isSelect) {
            // PILIH SEMUA hanya berlaku pada KELAS YANG SEDANG DITANDAI/AKTIF.
            // Kelas lain tidak disentuh.
            if (!currentActiveClassName || !Array.isArray(schoolData[currentActiveClassName])) {
                showAlert('Pilih/tandai kelas terlebih dahulu.');
                return;
            }

            const students = schoolData[currentActiveClassName];
            students.forEach(student => {
                if (!student || student.id == null) return;
                const key = String(student.id);
                selectedStudents[key] = true;
                student.selected = true;
            });

            saveSchoolData();
            renderStudentList();
            updateOutputLinks();
            showAlert(`Semua ${students.length} siswa di Kelas ${currentActiveClassName} telah dipilih.`);
        }

        function kosongkanSemuaPilihan() {
            // KOSONGKAN menghapus SEMUA PILIHAN dari seluruh kelas,
            // tetapi TIDAK menghapus data siswa, kelas, NIS, NISN, gender, atau link.
            let jumlahDipilih = 0;
            Object.keys(schoolData || {}).forEach(className => {
                (schoolData[className] || []).forEach(student => {
                    if (student.selected || selectedStudents[String(student.id)]) jumlahDipilih++;
                    student.selected = false;
                    delete selectedStudents[String(student.id)];
                });
            });

            saveSchoolData();
            renderClassTabs();
            renderStudentList();
            updateOutputLinks();

            showAlert(jumlahDipilih > 0
                ? `${jumlahDipilih} siswa terpilih telah dikosongkan dari semua kelas.`
                : 'Tidak ada siswa yang sedang dipilih.');
        }

        function updateOutputLinks() {
            const textarea = document.getElementById('outputLinkArea');
            let outputLinks = [];
            
            Object.keys(schoolData).forEach(className => {
                schoolData[className].forEach(student => {
                    if (selectedStudents[student.id]) {
                        outputLinks.push(student.link);
                    }
                });
            });

            const total = outputLinks.length;
            const badge = document.getElementById('totalSelectedBadge');
            const countEl = document.getElementById('totalSelectedCount');
            if (badge) badge.textContent = `${total} Siswa`;
            if (countEl) countEl.textContent = total;
            if (textarea) textarea.value = total === 0 ? '' : outputLinks.join('\n');
            const activeClassCount = document.getElementById('selectedActiveClassCount');
            if (activeClassCount) {
                let kelasTerpilih = 0;
                Object.keys(schoolData || {}).forEach(className => {
                    if ((schoolData[className] || []).some(student => selectedStudents[student.id])) kelasTerpilih++;
                });
                activeClassCount.textContent = kelasTerpilih;
            }
        }

        function updateStatistics() {
            let totalStudents = 0;
            const classKeys = Object.keys(schoolData);
            
            classKeys.forEach(className => {
                totalStudents += schoolData[className].length;
            });
            
            const totalStudentsEl = document.getElementById('statTotalStudents');
            const totalClassesEl = document.getElementById('statTotalClasses');
            if (totalStudentsEl) totalStudentsEl.textContent = totalStudents;
            if (totalClassesEl) totalClassesEl.textContent = classKeys.length;
        }

        function applyGlobalLink() {
            if (!currentActiveClassName) {
                showAlert('Pilih kelas terlebih dahulu.');
                return;
            }
            
            const template = document.getElementById('globalLinkInput').value.trim();
            if (!template) {
                showAlert('Format tautan tidak boleh kosong.');
                return;
            }

            showConfirmModal(
                'Terapkan Tautan Global',
                `Apakah Anda yakin ingin menerapkan format tautan ini untuk seluruh siswa di ${currentActiveClassName}? Tautan sebelumnya akan tertimpa.`,
                () => {
                    let updatedCount = 0;
                    schoolData[currentActiveClassName].forEach(student => {
                        let link = template;
                        const encodedName = encodeURIComponent(student.name).replace(/%20/g, '+');
                        link = link.replace(/{nama}/gi, encodedName);
                        link = link.replace(/{nis}/gi, student.id);
                        link = link.replace(/{nisn}/gi, student.nisn);
                        
                        student.link = link;
                        updatedCount++;
                    });
                    
                    saveSchoolData();
                    renderStudentList();
                    updateOutputLinks();
                    showAlert(`Berhasil menerapkan tautan baru untuk ${updatedCount} siswa di ${currentActiveClassName}.`);
                    document.getElementById('globalLinkInput').value = '';
                }
            );
        }


        // Mengirim seluruh data siswa terpilih tanpa membuka tab/jendela baru.
        // Catatan: mode no-cors tidak dapat membaca balasan Google Forms,
        // sehingga keberhasilan di sini berarti permintaan telah dikirim ke browser/network.
        async function kirimSemuaData() {
            const links = [];
            Object.keys(schoolData || {}).forEach(className => (schoolData[className] || []).forEach(student => {
                if (selectedStudents[student.id] && student.link) links.push({ link: student.link.trim(), name: student.name, className, id: student.id });
            }));
            if (!links.length) { showAlert('Tidak ada siswa yang dipilih untuk dikirim.'); return; }
            showConfirmModal('Kirim Semua Data', `Kirim data ${links.length} siswa terpilih tanpa membuka tab baru?`, () => startSendProcess(links));
        }

        let failedSendItems = [];
        async function startSendProcess(links) {
            const panel=document.getElementById('sendProgressPanel'), bar=document.getElementById('sendProgressBar'), percent=document.getElementById('sendProgressPercent'), count=document.getElementById('sendProgressCount'), status=document.getElementById('sendProgressStatus'), student=document.getElementById('sendProgressStudent'), closeBtn=document.getElementById('sendProgressClose'), icon=document.getElementById('sendProgressIcon'), retry=document.getElementById('sendRetryFailed'), badge=document.getElementById('sendCompleteBadge');
            if(panel) panel.classList.add('show'); if(closeBtn) closeBtn.disabled=true; if(retry) retry.classList.remove('show'); if(badge) badge.classList.remove('show');
            let success=0, failed=0, pending=links.length; failedSendItems=[];
            const update=(done=0)=>{ const e=id=>document.getElementById(id); if(e('sendSuccessCount'))e('sendSuccessCount').textContent=success; if(e('sendFailedCount'))e('sendFailedCount').textContent=failed; if(e('sendPendingCount'))e('sendPendingCount').textContent=pending; if(bar)bar.style.width=Math.round(done/links.length*100)+'%'; if(percent)percent.textContent=Math.round(done/links.length*100)+'%'; if(count)count.textContent=`${done} / ${links.length} data`; };
            if(bar)bar.style.width='0%'; if(percent)percent.textContent='0%'; if(count)count.textContent=`0 / ${links.length} data`; if(status)status.textContent='Menyiapkan pengiriman...'; if(student)student.textContent='Mohon tunggu, data sedang diproses'; if(icon)icon.className='fa-solid fa-paper-plane'; update(0);
            for(let i=0;i<links.length;i++){
                const item=links[i]; if(student)student.textContent=`${item.name} • ${item.className}`; if(status)status.textContent=`Mengirim data ${i+1} dari ${links.length}`;
                let ok=false;
                try{ await fetch(item.link,{method:'GET',mode:'no-cors',cache:'no-store',keepalive:true}); ok=true; }
                catch(err){ try{ const img=new Image(); img.src=item.link; ok=true; }catch(e){} }
                if(ok){success++;pending=Math.max(0,pending-1);}else{failed++;failedSendItems.push(item);pending=Math.max(0,pending-1);}
                update(i+1); await new Promise(r=>setTimeout(r,80));
            }
            finishSendProcess(success,failed,pending,closeBtn,retry,badge,status,student,icon);
        }

        function finishSendProcess(success,failed,pending,closeBtn,retry,badge,status,student,icon){
            if(status)status.textContent=failed?'Pengiriman selesai dengan beberapa data gagal':'Semua data berhasil diproses';
            if(student)student.textContent=`Selesai: ${success} berhasil, ${failed} gagal, ${pending} belum terkirim.`;
            if(icon)icon.className=failed?'fa-solid fa-circle-exclamation':'fa-solid fa-circle-check';
            if(retry)retry.classList.toggle('show',failed>0); if(badge)badge.classList.toggle('show',failed===0); if(closeBtn)closeBtn.disabled=false;
            if(failed===0){ setTimeout(()=>closeSendProgress(),1400); }
        }

        async function retryFailedData(){
            if(!failedSendItems.length)return;
            const retryItems=[...failedSendItems];
            const retryBtn=document.getElementById('sendRetryFailed'); if(retryBtn)retryBtn.disabled=true;
            const panel=document.getElementById('sendProgressPanel'), bar=document.getElementById('sendProgressBar'), percent=document.getElementById('sendProgressPercent'), count=document.getElementById('sendProgressCount'), status=document.getElementById('sendProgressStatus'), student=document.getElementById('sendProgressStudent'), closeBtn=document.getElementById('sendProgressClose'), icon=document.getElementById('sendProgressIcon'), badge=document.getElementById('sendCompleteBadge');
            let success=0,failed=0; failedSendItems=[]; if(closeBtn)closeBtn.disabled=true; if(badge)badge.classList.remove('show');
            for(let i=0;i<retryItems.length;i++){ const item=retryItems[i]; if(student)student.textContent=`Mengulangi: ${item.name} • ${item.className}`; if(status)status.textContent=`Mengulangi data ${i+1} dari ${retryItems.length}`; let ok=false; try{await fetch(item.link,{method:'GET',mode:'no-cors',cache:'no-store',keepalive:true});ok=true}catch(e){try{const img=new Image();img.src=item.link;ok=true}catch(x){}} if(!ok){failed++;failedSendItems.push(item)}else success++; const pct=Math.round((i+1)/retryItems.length*100); if(bar)bar.style.width=pct+'%'; if(percent)percent.textContent=pct+'%'; if(count)count.textContent=`${i+1} / ${retryItems.length} data gagal`; document.getElementById('sendSuccessCount').textContent=success; document.getElementById('sendFailedCount').textContent=failed; document.getElementById('sendPendingCount').textContent=retryItems.length-(i+1); await new Promise(r=>setTimeout(r,100)); }
            if(status)status.textContent=failed?'Pengulangan selesai, masih ada data gagal':'Semua data gagal berhasil dikirim ulang'; if(student)student.textContent=failed?`${success} berhasil diulang, ${failed} masih gagal.`:`${success} data berhasil dikirim ulang.`; if(icon)icon.className=failed?'fa-solid fa-circle-exclamation':'fa-solid fa-circle-check'; if(retry)retry.classList.toggle('show',failed>0); if(badge)badge.classList.toggle('show',failed===0); if(closeBtn)closeBtn.disabled=false; if(retryBtn)retryBtn.disabled=false; if(failed===0)setTimeout(()=>closeSendProgress(),1400);
        }

        function closeSendProgress() {
            const panel = document.getElementById('sendProgressPanel');
            if (panel) panel.classList.remove('show');
        }

        function processAndOpen() {
            const links = document.getElementById('outputLinkArea').value.split('\n').filter(l => l.trim() !== '');
            if (links.length === 0) {
                showAlert('Tidak ada tautan yang dipilih.');
                return;
            }
            
            if (links.length > 20) {
                showConfirmModal('Membuka Banyak Tautan', `Anda akan membuka ${links.length} tab baru. Browser Anda mungkin memblokir popup ini. Lanjutkan?`, () => {
                    executeOpenLinks(links);
                });
            } else {
                executeOpenLinks(links);
            }
        }

        function executeOpenLinks(links) {
            let blocked = false;
            links.forEach(link => {
                const win = window.open(link.trim(), '_blank');
                if (!win || win.closed || typeof win.closed == 'undefined') {
                    blocked = true;
                }
            });
            if (blocked) {
                showAlert('Beberapa tab diblokir oleh browser. Harap izinkan pop-up untuk situs ini.');
            }
        }

        function copyAllOutputLinks() {
            const textarea = document.getElementById('outputLinkArea');
            if (!textarea.value) {
                showAlert('Tidak ada tautan untuk disalin.');
                return;
            }
            
            textarea.select();
            document.execCommand('copy');
            window.getSelection().removeAllRanges();
            showAlert('Tautan berhasil disalin ke clipboard!');
        }

        function populateClassDropdown(selectId) {
            const select = document.getElementById(selectId);
            select.innerHTML = '';
            Object.keys(schoolData).forEach(className => {
                const option = document.createElement('option');
                option.value = className;
                option.textContent = className;
                if (className === currentActiveClassName) {
                    option.selected = true;
                }
                select.appendChild(option);
            });
        }

        function openAddStudentModal() {
            if (Object.keys(schoolData).length === 0) {
                showAlert('Silakan tambah kelas terlebih dahulu sebelum menambah siswa.');
                return;
            }
            document.getElementById('studentModalTitle').textContent = 'Tambah Siswa Baru';
            document.getElementById('studentForm').reset();
            document.getElementById('editOriginalClass').value = '';
            document.getElementById('editOriginalId').value = '';
            populateClassDropdown('modalStudentClass');
            document.getElementById('studentModal').classList.remove('hidden');
        }

        function openEditStudentModal(id) {
            let foundStudent = null;
            let foundClass = '';
            
            Object.keys(schoolData).forEach(className => {
                const student = schoolData[className].find(s => s.id === id);
                if (student) {
                    foundStudent = student;
                    foundClass = className;
                }
            });

            if (!foundStudent) return;

            document.getElementById('studentModalTitle').textContent = 'Edit Data Siswa';
            document.getElementById('editOriginalClass').value = foundClass;
            document.getElementById('editOriginalId').value = foundStudent.id;
            
            populateClassDropdown('modalStudentClass');
            document.getElementById('modalStudentClass').value = foundClass;
            
            document.getElementById('modalStudentId').value = foundStudent.id;
            document.getElementById('modalStudentNisn').value = foundStudent.nisn;
            document.getElementById('modalStudentName').value = foundStudent.name;
            document.getElementById('modalStudentGender').value = foundStudent.gender;
            document.getElementById('modalStudentLink').value = foundStudent.link;

            document.getElementById('studentModal').classList.remove('hidden');
        }

        function closeStudentModal() {
            document.getElementById('studentModal').classList.add('hidden');
        }

        function handleSaveStudent(e) {
            e.preventDefault();
            
            const originalClass = document.getElementById('editOriginalClass').value;
            const originalId = document.getElementById('editOriginalId').value;
            
            const targetClass = document.getElementById('modalStudentClass').value;
            const id = document.getElementById('modalStudentId').value.trim();
            const nisn = document.getElementById('modalStudentNisn').value.trim();
            const name = document.getElementById('modalStudentName').value.trim().toUpperCase();
            const gender = document.getElementById('modalStudentGender').value;
            let link = document.getElementById('modalStudentLink').value.trim();

            if (!id || !name) {
                showAlert('NIS dan Nama wajib diisi.');
                return;
            }

            let isDuplicate = false;
            Object.keys(schoolData).forEach(className => {
                if (schoolData[className].some(s => s.id === id && s.id !== originalId)) {
                    isDuplicate = true;
                }
            });

            if (isDuplicate) {
                showAlert(`Siswa dengan NIS ${id} sudah ada!`);
                return;
            }

            const newStudent = { id, nisn, name, gender, link, selected: false };

            if (originalId) {
                newStudent.selected = !!selectedStudents[originalId]; 
                if (originalClass === targetClass && id === originalId) {
                    const index = schoolData[targetClass].findIndex(s => s.id === originalId);
                    if (index !== -1) schoolData[targetClass][index] = newStudent;
                } else {
                    schoolData[originalClass] = schoolData[originalClass].filter(s => s.id !== originalId);
                    if (originalId !== id) {
                        selectedStudents[id] = selectedStudents[originalId];
                        delete selectedStudents[originalId];
                    }
                    schoolData[targetClass].push(newStudent);
                }
            } else {
                schoolData[targetClass].push(newStudent);
            }

            schoolData[targetClass].sort((a, b) => a.name.localeCompare(b.name));

            saveSchoolData();
            if (targetClass !== currentActiveClassName) {
                switchClass(targetClass);
            } else {
                renderClassTabs();
                renderStudentList();
            }
            updateOutputLinks();
            closeStudentModal();
            showAlert('Data siswa berhasil disimpan.');
        }

        function askDeleteStudent(id) {
            let name = '';
            Object.keys(schoolData).forEach(className => {
                const s = schoolData[className].find(st => st.id === id);
                if (s) name = s.name;
            });

            showConfirmModal('Hapus Siswa', `Apakah Anda yakin ingin menghapus siswa ${name} (NIS: ${id})?`, () => {
                deleteStudent(id);
            });
        }

        function deleteStudent(id) {
            Object.keys(schoolData).forEach(className => {
                schoolData[className] = schoolData[className].filter(s => s.id !== id);
            });
            delete selectedStudents[id];
            saveSchoolData();
            renderClassTabs();
            renderStudentList();
            updateOutputLinks();
            showAlert('Siswa berhasil dihapus.');
        }

        function openAddClassModal() {
            document.getElementById('newClassNameInput').value = '';
            document.getElementById('classModal').classList.remove('hidden');
        }

        function closeClassModal() {
            document.getElementById('classModal').classList.add('hidden');
        }

        function handleSaveClass(e) {
            e.preventDefault();
            const className = document.getElementById('newClassNameInput').value.trim();
            if (!className) return;

            if (schoolData[className]) {
                showAlert('Nama kelas sudah ada!');
                return;
            }

            schoolData[className] = [];
            saveSchoolData();
            switchClass(className);
            closeClassModal();
            showAlert(`Kelas ${className} berhasil ditambahkan.`);
        }

        function askDeleteClass(className) {
            const count = schoolData[className].length;
            showConfirmModal('Hapus Kelas', `Anda akan menghapus Kelas ${className} beserta ${count} siswa di dalamnya. Lanjutkan?`, () => {
                deleteClass(className);
            });
        }

        function deleteClass(className) {
            schoolData[className].forEach(s => {
                delete selectedStudents[s.id];
            });
            delete schoolData[className];
            
            const classKeys = Object.keys(schoolData);
            if (classKeys.length > 0) {
                currentActiveClassName = classKeys[0];
            } else {
                currentActiveClassName = '';
            }
            
            saveSchoolData();
            renderClassTabs();
            renderStudentList();
            updateOutputLinks();
            showAlert(`Kelas ${className} telah dihapus.`);
            if (typeof populateDeleteClassSettings === 'function') populateDeleteClassSettings();
        }

        function openBulkStudentModal() {
            if (Object.keys(schoolData).length === 0) {
                showAlert('Silakan tambah kelas terlebih dahulu.');
                return;
            }
            populateClassDropdown('bulkStudentClass');
            document.getElementById('bulkStudentData').value = '';
            document.getElementById('bulkStudentModal').classList.remove('hidden');
        }

        function closeBulkStudentModal() {
            document.getElementById('bulkStudentModal').classList.add('hidden');
        }

        function fillBulkExample() {
            document.getElementById('bulkStudentData').value = "260120\t0101234567\tAHMAD FAUZI\tLAKI-LAKI\n260121\t0101234568\tBUDI SANTOSO\tLAKI-LAKI\n260122\t0101234569\tSITI AISYAH\tPEREMPUAN";
        }

        function handleBulkSaveStudents() {
            const targetClass = document.getElementById('bulkStudentClass').value;
            const rawData = document.getElementById('bulkStudentData').value.trim();
            if (!rawData) {
                showAlert('Data tidak boleh kosong.');
                return;
            }

            const lines = rawData.split('\n');
            let addedCount = 0;
            let skipCount = 0;

            lines.forEach(line => {
                if (!line.trim()) return;
                
                let parts = line.split('\t');
                if (parts.length < 3) parts = line.split(';');
                if (parts.length < 3) parts = line.split(',');

                if (parts.length >= 3) {
                    const id = parts[0].trim();
                    const nisn = parts[1].trim();
                    const name = parts[2].trim().toUpperCase();
                    let gender = 'LAKI-LAKI';
                    if (parts.length >= 4) {
                        const g = parts[3].trim().toUpperCase();
                        if (g === 'P' || g === 'PEREMPUAN' || g === 'W' || g === 'WANITA') {
                            gender = 'PEREMPUAN';
                        }
                    }

                    let isDuplicate = false;
                    Object.keys(schoolData).forEach(cName => {
                        if (schoolData[cName].some(s => s.id === id)) {
                            isDuplicate = true;
                        }
                    });

                    if (!isDuplicate && id && name) {
                        schoolData[targetClass].push({
                            id, nisn, name, gender, link: '', selected: false
                        });
                        addedCount++;
                    } else {
                        skipCount++;
                    }
                }
            });

            schoolData[targetClass].sort((a, b) => a.name.localeCompare(b.name));
            saveSchoolData();
            
            if (targetClass !== currentActiveClassName) {
                switchClass(targetClass);
            } else {
                renderClassTabs();
                renderStudentList();
            }
            updateOutputLinks();
            closeBulkStudentModal();

            let msg = `Berhasil menambah ${addedCount} siswa secara massal.`;
            if (skipCount > 0) msg += ` (Dilewati ${skipCount} data karena format salah atau NIS duplikat)`;
            showAlert(msg);
        }

        function exportDataJSON() {
            const dataStr = JSON.stringify(schoolData, null, 2);
            const blob = new Blob([dataStr], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `Sman2_Presensi_Backup_${new Date().getTime()}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        function importDataJSON(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = (e) => {
                try {
                    const parsedData = JSON.parse(e.target.result);
                    if (typeof parsedData === 'object' && !Array.isArray(parsedData)) {
                        schoolData = parsedData;
                        
                        selectedStudents = {};
                        Object.keys(schoolData).forEach(className => {
                            schoolData[className].forEach(s => {
                                if (s.selected) selectedStudents[s.id] = true;
                            });
                        });
                        
                        saveSchoolData();
                        
                        const classKeys = Object.keys(schoolData);
                        if (classKeys.length > 0) {
                            currentActiveClassName = classKeys[0];
                        } else {
                            currentActiveClassName = '';
                        }
                        
                        renderClassTabs();
                        renderStudentList();
                        updateOutputLinks();
                        showAlert('Data berhasil diimpor.');
                    } else {
                        showAlert('Format file JSON tidak valid.');
                    }
                } catch (err) {
                    showAlert('Gagal mengurai file JSON.');
                }
            };
            reader.readAsText(file);
            event.target.value = '';
        }

        function showAlert(msg) {
            document.getElementById('alertText').textContent = msg;
            const alertBox = document.getElementById('alertBox');
            alertBox.classList.remove('hidden');
            setTimeout(() => {
                hideAlert();
            }, 5000);
        }

        function hideAlert() {
            document.getElementById('alertBox').classList.add('hidden');
        }

        function showConfirmModal(title, message, callback) {
            const modal = document.getElementById('confirmModal');
            const iconWrap = modal.querySelector('.w-12.h-12');
            const icon = iconWrap ? iconWrap.querySelector('i') : null;
            const executeBtn = document.getElementById('confirmExecuteBtn');
            const isSend = /kirim/i.test(title);

            document.getElementById('confirmTitle').textContent = title;
            document.getElementById('confirmMessage').textContent = message;
            pendingConfirmCallback = callback;

            if (isSend) {
                if (iconWrap) iconWrap.className = 'w-12 h-12 bg-sky-100 dark:bg-sky-900/30 text-sky-600 dark:text-sky-300 rounded-full flex items-center justify-center mx-auto text-xl';
                if (icon) icon.className = 'fa-solid fa-paper-plane';
                if (executeBtn) {
                    executeBtn.textContent = 'Kirim';
                    executeBtn.className = 'px-4 py-2 text-xs rounded-xl bg-sky-500 hover:bg-sky-600 text-white font-semibold transition shadow-sm';
                }
            } else {
                if (iconWrap) iconWrap.className = 'w-12 h-12 bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 rounded-full flex items-center justify-center mx-auto text-xl';
                if (icon) icon.className = 'fa-solid fa-triangle-exclamation';
                if (executeBtn) {
                    executeBtn.textContent = 'Ya, Hapus';
                    executeBtn.className = 'px-4 py-2 text-xs rounded-xl bg-red-600 text-white hover:bg-red-700 font-semibold transition';
                }
            }
            modal.classList.remove('hidden');
        }

        function closeConfirmModal() {
            document.getElementById('confirmModal').classList.add('hidden');
            pendingConfirmCallback = null;
        }

        document.getElementById('confirmExecuteBtn').addEventListener('click', () => {
            if (pendingConfirmCallback) {
                pendingConfirmCallback();
            }
            closeConfirmModal();
        });
        
    </script>

<!-- PANEL PROGRES KIRIM DATA -->
<div id="sendProgressPanel" class="send-progress-overlay">
  <div class="send-progress-card">
    <button id="sendProgressClose" type="button" class="send-progress-close" onclick="closeSendProgress()" disabled aria-label="Tutup"><i class="fa-solid fa-xmark"></i></button>
    <div class="send-progress-orbit"><div class="send-progress-orbit-ring"></div><div class="send-progress-icon"><i id="sendProgressIcon" class="fa-solid fa-paper-plane"></i></div></div>
    <div class="text-center mt-3">
      <div class="send-progress-kicker">PENGIRIMAN DATA</div>
      <h3 class="text-xl font-extrabold text-slate-900 dark:text-white mt-1">Kirim Semua Data</h3>
      <p id="sendProgressStatus" class="text-sm text-slate-500 dark:text-slate-300 mt-1">Menyiapkan pengiriman...</p>
    </div>
    <div class="send-progress-track"><div id="sendProgressBar" class="send-progress-fill"></div></div>
    <div class="flex items-center justify-between mt-2 text-xs font-bold"><span id="sendProgressCount">0 / 0 data</span><span id="sendProgressPercent">0%</span></div>
    <div class="send-progress-student"><i class="fa-solid fa-user mr-2"></i><span id="sendProgressStudent">Mohon tunggu, data sedang diproses</span></div>
    <div class="send-summary-grid">
      <div class="send-summary-item success"><span><i class="fa-solid fa-circle-check"></i> Berhasil</span><strong id="sendSuccessCount">0</strong></div>
      <div class="send-summary-item failed"><span><i class="fa-solid fa-circle-xmark"></i> Gagal</span><strong id="sendFailedCount">0</strong></div>
      <div class="send-summary-item pending"><span><i class="fa-solid fa-clock"></i> Belum terkirim</span><strong id="sendPendingCount">0</strong></div>
    </div>
    <button id="sendRetryFailed" type="button" class="send-retry-btn" onclick="retryFailedData()"><i class="fa-solid fa-rotate-right mr-2"></i> Ulangi Data Gagal</button><div id="sendCompleteBadge" class="send-complete-badge"><i class="fa-solid fa-circle-check mr-1"></i> Semua data selesai diproses</div>
    <div class="send-progress-tip"><i class="fa-solid fa-shield-halved mr-2"></i> Tetap di halaman ini sampai proses selesai. Tidak ada tab baru yang dibuka.</div>
  </div>
</div>

<!-- PANEL PENGATURAN -->
<div id="settingsPanel" class="hidden fixed inset-0 z-[100] bg-black/50 backdrop-blur-sm p-4 flex items-center justify-center">
  <div class="w-full max-w-lg bg-white dark:bg-gray-800 rounded-2xl shadow-2xl border border-gray-200 dark:border-gray-700 overflow-hidden">
    <div class="px-5 py-4 border-b border-gray-200 dark:border-gray-700 flex items-center justify-between">
      <div><h3 class="font-bold text-base text-gray-900 dark:text-white"><i class="fa-solid fa-gear text-indigo-500 mr-2"></i>Pengaturan & Kelola Data</h3>
      <p class="text-[11px] text-gray-500 mt-1">Fungsi pengelolaan data siswa tersedia di sini.</p></div>
      <button type="button" onclick="closeSettingsPanel()" class="w-9 h-9 rounded-xl bg-gray-100 dark:bg-gray-700"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div class="p-5 grid grid-cols-1 sm:grid-cols-2 gap-3">
      <button type="button" onclick="closeSettingsPanel();openAddStudentModal()" class="settings-action bg-indigo-600 text-white"><i class="fa-solid fa-user-plus"></i>Tambah Siswa</button>
      <button type="button" onclick="closeSettingsPanel();openBulkStudentModal()" class="settings-action bg-violet-600 text-white"><i class="fa-solid fa-users"></i>Tambah Siswa Massal</button>
      <button type="button" onclick="closeSettingsPanel();openAddClassModal()" class="settings-action bg-emerald-600 text-white"><i class="fa-solid fa-folder-plus"></i>Tambah Kelas</button>
      <div class="sm:col-span-2 settings-link-section"><!-- Konfigurasi Tautan / Format Link per Kelas -->
            <div class="bg-slate-50 dark:bg-slate-900/50 p-4 rounded-xl border border-slate-200 dark:border-slate-700 flex flex-col gap-3">
                <div class="flex justify-between items-center">
                    <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                        <i class="fa-solid fa-link text-indigo-500"></i> Pola Tautan Presensi / Kelas
                    </h2>
                    <button onclick="resetToDefaultData()" class="text-[11px] text-red-500 hover:underline flex items-center gap-1">
                        <i class="fa-solid fa-rotate-left"></i> Reset Data Awal
                    </button>
                </div>
                <p class="text-xs text-gray-400">Masukkan tautan Google Forms/format umum. Gunakan placeholder <code class="bg-gray-100 dark:bg-gray-700 px-1 py-0.5 rounded text-indigo-500">{nama}</code> atau <code class="bg-gray-100 dark:bg-gray-700 px-1 py-0.5 rounded text-indigo-500">{nis}</code> untuk kustomisasi dinamis.</p>
                
                <div class="flex flex-col sm:flex-row gap-2">
                    <input type="text" id="globalLinkInput" placeholder="Contoh: https://docs.google.com/forms/.../entry.123={nama}&entry.456={nis}" class="flex-1 p-2.5 text-xs rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 focus:ring-2 focus:ring-indigo-500 focus:outline-none transition">
                    <button onclick="applyGlobalLink()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 transition whitespace-nowrap">Terapkan Kelas Ini</button>
                </div>
            </div></div>
      <button type="button" onclick="toggleManageMode()" id="btnManageMode" class="settings-action bg-slate-700 text-white"><i class="fa-solid fa-pen-to-square"></i><span>Kelola / Edit Data Siswa</span></button>
      <div class="sm:col-span-2 rounded-xl bg-red-50 dark:bg-red-950/30 border border-red-200 dark:border-red-900/50 p-3">
        <div class="flex items-center gap-2 mb-2 text-xs font-semibold text-red-700 dark:text-red-300"><i class="fa-solid fa-trash-can"></i> Hapus Kelas</div>
        <div class="flex gap-2">
          <select id="settingsDeleteClass" class="flex-1 min-w-0 p-2.5 rounded-xl border border-red-200 dark:border-red-800 bg-white dark:bg-gray-800 text-xs text-gray-700 dark:text-gray-200 focus:ring-2 focus:ring-red-500 focus:outline-none"></select>
          <button type="button" onclick="deleteClassFromSettings()" class="px-4 py-2 rounded-xl bg-red-600 hover:bg-red-700 text-white text-xs font-bold shadow-sm">Hapus</button>
        </div>
        <p class="text-[10px] text-red-500 dark:text-red-300 mt-2">Menghapus kelas juga menghapus seluruh data siswa di dalam kelas tersebut.</p>
      </div>
      <div class="sm:col-span-2 rounded-xl bg-slate-50 dark:bg-slate-900/50 border border-slate-200 dark:border-slate-700 p-3">
        <div class="flex items-center gap-2 mb-2 text-xs font-semibold text-gray-700 dark:text-gray-200"><i class="fa-solid fa-display text-indigo-500"></i> Tampilan Aplikasi</div>
        <div class="grid grid-cols-3 gap-2">
          <button type="button" id="viewModePhone" class="settings-view bg-white dark:bg-gray-800 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700" title="Tampilan HP"><i class="fa-solid fa-mobile-screen mr-1"></i>HP</button>
          <button type="button" id="viewModeWindows" class="settings-view bg-white dark:bg-gray-800 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700" title="Tampilan Windows"><i class="fa-brands fa-windows mr-1"></i>Windows</button>
          <button type="button" id="viewModeAuto" class="settings-view bg-white dark:bg-gray-800 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700" title="Ikuti ukuran layar"><i class="fa-solid fa-wand-magic-sparkles mr-1"></i>Otomatis</button>
        </div>
      </div>
      <button type="button" onclick="closeSettingsPanel();resetToDefaultData()" class="settings-action bg-red-600 text-white sm:col-span-2"><i class="fa-solid fa-rotate-left"></i>Reset ke Data Awal</button>
    </div>
    <div class="px-5 pb-5"><div class="rounded-xl bg-indigo-50 dark:bg-indigo-950/40 border border-indigo-100 p-3 text-[11px] text-indigo-700 dark:text-indigo-300">
      <i class="fa-solid fa-circle-info mr-1"></i> Aktifkan <b>Kelola / Edit Data Siswa</b> untuk menampilkan tombol Edit dan Hapus pada kartu siswa.
    </div></div>
  </div>
</div>
<style id="settings-mobile-fix">
.settings-view{min-height:42px!important;border-radius:11px!important;font-size:11px;font-weight:700}.settings-action{min-height:48px!important;border-radius:13px!important;display:flex;align-items:center;justify-content:center;gap:9px;font-size:12px;box-shadow:0 4px 12px rgba(15,23,42,.10)}
body:not(.manage-data-mode) #studentListContainer button[title="Edit"],body:not(.manage-data-mode) #studentListContainer button[title="Hapus"]{display:none!important}
@media(max-width:700px){
 #studentListContainer{max-height:none!important;overflow-y:visible!important;padding:8px!important}
 #studentListContainer > div{padding:11px!important}
 #studentListContainer h4{white-space:normal!important;overflow:visible!important;text-overflow:clip!important;word-break:normal!important;overflow-wrap:anywhere!important;line-height:1.35!important;font-size:13px!important}
 #studentListContainer p{white-space:normal!important;line-height:1.35!important}
}
</style>
<script id="view-mode-ui-only">
(function(){
  const root=document.documentElement;
  const menu=document.getElementById('viewModeMenu');
  const phone=document.getElementById('viewModePhone');
  const windows=document.getElementById('viewModeWindows');
  const auto=document.getElementById('viewModeAuto');

  function setMode(mode){
    root.classList.remove('force-phone','force-windows');
    if(mode==='phone') root.classList.add('force-phone');
    if(mode==='windows') root.classList.add('force-windows');
    try{localStorage.setItem('sman2_view_mode',mode)}catch(e){}
    [phone,windows,auto].forEach(b=>{
      if(b) b.classList.remove('bg-blue-600','text-white');
    });
    const active=mode==='phone'?phone:mode==='windows'?windows:auto;
    if(active) active.classList.add('bg-blue-600','text-white');
  }

  phone && phone.addEventListener('click',()=>setMode('phone'));
  windows && windows.addEventListener('click',()=>setMode('windows'));
  auto && auto.addEventListener('click',()=>setMode('auto'));

  let saved='auto';
  try{saved=localStorage.getItem('sman2_view_mode')||'auto'}catch(e){}
  setMode(saved);
})();
</script>
<script id="settings-panel-script">
(function(){
 window.populateDeleteClassSettings=function(){
   var sel=document.getElementById('settingsDeleteClass');
   if(!sel || typeof schoolData==='undefined') return;
   var keys=Object.keys(schoolData);
   sel.innerHTML=keys.map(function(k){return '<option value="'+k.replace(/"/g,'&quot;')+'">'+k+' ('+(schoolData[k]||[]).length+' siswa)</option>';}).join('');
   sel.disabled=keys.length<=1;
 };
 window.openSettingsPanel=function(){var e=document.getElementById('settingsPanel');if(e)e.classList.remove('hidden');populateDeleteClassSettings()};
 window.deleteClassFromSettings=function(){
   var sel=document.getElementById('settingsDeleteClass');
   var cls=sel && sel.value;
   if(!cls) return;
   if(Object.keys(schoolData).length<=1){showAlert('Minimal harus ada satu kelas.');return;}
   closeSettingsPanel();
   askDeleteClass(cls);
 };
 window.closeSettingsPanel=function(){var e=document.getElementById('settingsPanel');if(e)e.classList.add('hidden')};
 window.toggleManageMode=function(){
   document.body.classList.toggle('manage-data-mode');
   var active=document.body.classList.contains('manage-data-mode');
   var b=document.getElementById('btnManageMode');
   if(b){b.classList.toggle('bg-emerald-600',active);b.classList.toggle('bg-slate-700',!active);var sp=b.querySelector('span');if(sp)sp.textContent=active?'Selesai Kelola Data':'Kelola / Edit Data Siswa'}
   if(typeof renderStudentList==='function')renderStudentList();
   if(typeof showAlert==='function')showAlert(active?'Mode kelola aktif. Tombol Edit dan Hapus ditampilkan.':'Mode kelola dinonaktifkan.');
 };
 document.addEventListener('click',function(e){var p=document.getElementById('settingsPanel');if(p&&e.target===p)closeSettingsPanel()});
})();
</script>


<style id="presensi-khusus-modern">
.presensi-khusus-btn{position:relative;min-height:92px;display:flex;flex-direction:column;align-items:flex-start;justify-content:center;gap:8px;padding:14px 15px;color:#fff;font-size:12px;font-weight:800;letter-spacing:.02em;border:1px solid rgba(255,255,255,.28);border-radius:18px;overflow:hidden;box-shadow:0 8px 22px rgba(15,23,42,.14),inset 0 1px 0 rgba(255,255,255,.22);transition:transform .2s ease,box-shadow .2s ease,filter .2s ease}
.presensi-khusus-btn::before{content:"";position:absolute;inset:0;background:linear-gradient(135deg,rgba(255,255,255,.18),transparent 48%,rgba(0,0,0,.08));pointer-events:none}
.presensi-khusus-btn::after{content:"Buka formulir";position:absolute;right:12px;bottom:10px;font-size:9px;font-weight:600;opacity:.78;letter-spacing:.01em}
.presensi-khusus-btn:hover{transform:translateY(-4px) scale(1.015);box-shadow:0 14px 28px rgba(15,23,42,.20),inset 0 1px 0 rgba(255,255,255,.25);filter:saturate(1.08)}
.presensi-khusus-btn:active{transform:translateY(-1px) scale(.99)}
.presensi-khusus-btn i{position:relative;z-index:1;width:38px;height:38px;display:flex;align-items:center;justify-content:center;border-radius:12px;background:rgba(255,255,255,.18);border:1px solid rgba(255,255,255,.22);font-size:17px;box-shadow:inset 0 1px 0 rgba(255,255,255,.18)}
.presensi-khusus-btn span{position:relative;z-index:1;font-size:13px;line-height:1}
.presensi-khusus-btn:nth-child(1){background:linear-gradient(135deg,#2563eb,#1d4ed8)}
.presensi-khusus-btn:nth-child(2){background:linear-gradient(135deg,#eab308,#ca8a04)}
.presensi-khusus-btn:nth-child(3){background:linear-gradient(135deg,#f97316,#ea580c)}
.presensi-khusus-btn:nth-child(4){background:linear-gradient(135deg,#ef4444,#dc2626)}
@media(max-width:640px){.presensi-khusus-btn{min-height:86px;padding:12px;border-radius:16px}.presensi-khusus-btn i{width:34px;height:34px;border-radius:10px;font-size:15px}.presensi-khusus-btn span{font-size:11px}.presensi-khusus-btn::after{font-size:8px;right:10px;bottom:9px}}
</style>


<style id="settings-link-aesthetic">
.settings-link-section .settings-link-card{background:transparent!important;box-shadow:none!important;border:0!important;padding:0!important}
.settings-link-section h2{font-size:12px!important}
.settings-link-section input{background:white}
.dark .settings-link-section input{background:#111827}
</style>
<style id="send-confirm-cool">
#confirmModal .bg-sky-100{box-shadow:0 0 0 8px rgba(14,165,233,.08),0 10px 30px rgba(14,165,233,.12)}
</style>


<!-- DASHBOARD HASIL PRESENSI DI DALAM APLIKASI -->
<div id="resultsDashboardPanel" class="results-dashboard hidden">
  <div class="results-dashboard-card">
    <div class="results-dashboard-head">
      <div>
        <div class="results-dashboard-kicker"><i class="fa-solid fa-chart-pie"></i> REKAP PRESENSI</div>
        <h2>Dashboard Hasil Presensi</h2>
        <p id="resultsDashboardStatus">Menyiapkan data…</p>
      </div>
      <div class="results-dashboard-actions">
        <button type="button" onclick="loadResultsDashboard()" class="results-dashboard-refresh" title="Refresh data"><i class="fa-solid fa-rotate"></i><span>Refresh</span></button>
        <button type="button" onclick="closeResultsDashboard()" class="results-dashboard-close" title="Kembali"><i class="fa-solid fa-xmark"></i></button>
      </div>
    </div>

    <div class="results-stat-grid">
      <div class="results-stat-card hadir"><div class="results-stat-icon"><i class="fa-solid fa-circle-check"></i></div><div><span>Hadir</span><strong id="resultCountHadir">—</strong></div></div>
      <div class="results-stat-card sakit"><div class="results-stat-icon"><i class="fa-solid fa-bed-pulse"></i></div><div><span>Sakit</span><strong id="resultCountSakit">—</strong></div></div>
      <div class="results-stat-card izin"><div class="results-stat-icon"><i class="fa-solid fa-file-signature"></i></div><div><span>Izin</span><strong id="resultCountIzin">—</strong></div></div>
      <div class="results-stat-card terlambat"><div class="results-stat-icon"><i class="fa-solid fa-clock"></i></div><div><span>Terlambat</span><strong id="resultCountTerlambat">—</strong></div></div>
      <div class="results-stat-card bolos"><div class="results-stat-icon"><i class="fa-solid fa-person-walking-arrow-right"></i></div><div><span>Bolos</span><strong id="resultCountBolos">—</strong></div></div>
    </div>

    <div class="results-sheet-wrap">
      <div class="results-sheet-title"><i class="fa-solid fa-table-list"></i><span>Data Google Spreadsheet</span><span class="results-live-badge"><i class="fa-solid fa-circle"></i> LIVE</span></div>
      <iframe id="resultsSheetFrame" title="Hasil Presensi Google Spreadsheet" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR3f_LifCDZ3C341cJYzRbdsJSfRqirIHuD7O7mk-TzyApW36N2bQlRMuZfM0g1BTFdGzDp8W4oFrgq/pubhtml?widget=true&headers=false" loading="lazy"></iframe>
    </div>
  </div>
</div>

<style id="results-dashboard-style">
body.results-dashboard-open{overflow:hidden}
.results-dashboard{position:fixed;inset:0;z-index:180;background:rgba(2,6,23,.62);backdrop-filter:blur(12px);padding:16px;overflow-y:auto}
.results-dashboard-card{width:min(1180px,100%);min-height:calc(100vh - 32px);margin:auto;background:linear-gradient(145deg,#f8fbff,#fff);border:1px solid rgba(255,255,255,.75);border-radius:28px;box-shadow:0 30px 100px rgba(0,0,0,.28);overflow:hidden}
.dark .results-dashboard-card{background:linear-gradient(145deg,#0f172a,#111827);border-color:rgba(148,163,184,.16)}
.results-dashboard-head{display:flex;align-items:center;justify-content:space-between;gap:16px;padding:22px 24px 18px;border-bottom:1px solid rgba(148,163,184,.16);background:linear-gradient(135deg,rgba(59,130,246,.10),rgba(99,102,241,.06),transparent)}
.results-dashboard-kicker{font-size:10px;font-weight:900;letter-spacing:.14em;color:#2563eb;margin-bottom:5px}.dark .results-dashboard-kicker{color:#60a5fa}
.results-dashboard-head h2{margin:0;font-size:22px;font-weight:900;color:#0f172a}.dark .results-dashboard-head h2{color:#f8fafc}
.results-dashboard-head p{margin:5px 0 0;font-size:11px;color:#64748b}.dark .results-dashboard-head p{color:#94a3b8}
.results-dashboard-actions{display:flex;align-items:center;gap:8px}.results-dashboard-refresh,.results-dashboard-close{border:0;border-radius:12px;display:flex;align-items:center;justify-content:center;gap:7px;cursor:pointer;transition:.18s}.results-dashboard-refresh{padding:10px 13px;background:#e0f2fe;color:#0369a1;font-size:11px;font-weight:800}.results-dashboard-refresh:hover{transform:translateY(-1px);background:#bae6fd}.results-dashboard-close{width:40px;height:40px;background:#f1f5f9;color:#475569;font-size:17px}.results-dashboard-close:hover{background:#e2e8f0;transform:rotate(4deg)}.dark .results-dashboard-refresh{background:#082f49;color:#7dd3fc}.dark .results-dashboard-close{background:#1e293b;color:#cbd5e1}
.results-stat-grid{display:grid;grid-template-columns:repeat(5,minmax(0,1fr));gap:12px;padding:18px 24px}.results-stat-card{position:relative;display:flex;align-items:center;gap:11px;min-height:82px;padding:14px;border-radius:18px;color:#0f172a;overflow:hidden;border:1px solid rgba(255,255,255,.75);box-shadow:0 8px 22px rgba(15,23,42,.08)}.dark .results-stat-card{color:#f8fafc;border-color:rgba(148,163,184,.12)}.results-stat-card:after{content:"";position:absolute;width:70px;height:70px;border-radius:50%;right:-24px;bottom:-28px;background:rgba(255,255,255,.28)}
.results-stat-card.hadir{background:linear-gradient(135deg,#dcfce7,#bbf7d0)}.results-stat-card.sakit{background:linear-gradient(135deg,#dbeafe,#bfdbfe)}.results-stat-card.izin{background:linear-gradient(135deg,#fef3c7,#fde68a)}.results-stat-card.terlambat{background:linear-gradient(135deg,#ffedd5,#fed7aa)}.results-stat-card.bolos{background:linear-gradient(135deg,#fee2e2,#fecaca)}
.dark .results-stat-card.hadir{background:linear-gradient(135deg,#064e3b,#065f46)}.dark .results-stat-card.sakit{background:linear-gradient(135deg,#1e3a8a,#1d4ed8)}.dark .results-stat-card.izin{background:linear-gradient(135deg,#713f12,#92400e)}.dark .results-stat-card.terlambat{background:linear-gradient(135deg,#7c2d12,#9a3412)}.dark .results-stat-card.bolos{background:linear-gradient(135deg,#7f1d1d,#991b1b)}
.results-stat-icon{width:38px;height:38px;flex:0 0 38px;border-radius:12px;display:flex;align-items:center;justify-content:center;background:rgba(255,255,255,.62);font-size:16px}.dark .results-stat-icon{background:rgba(255,255,255,.12)}.results-stat-card span{display:block;font-size:10px;font-weight:800;opacity:.72}.results-stat-card strong{display:block;font-size:23px;line-height:1.1;font-weight:950;margin-top:3px}
.results-sheet-wrap{margin:0 24px 24px;border:1px solid rgba(148,163,184,.18);border-radius:20px;overflow:hidden;background:#fff;box-shadow:0 10px 28px rgba(15,23,42,.08)}.dark .results-sheet-wrap{background:#0b1220}.results-sheet-title{height:44px;display:flex;align-items:center;gap:8px;padding:0 14px;font-size:11px;font-weight:800;color:#475569;background:#f8fafc;border-bottom:1px solid rgba(148,163,184,.16)}.dark .results-sheet-title{background:#111827;color:#cbd5e1}.results-live-badge{margin-left:auto;font-size:9px;color:#16a34a;background:#dcfce7;border-radius:999px;padding:4px 8px}.results-live-badge i{font-size:6px;vertical-align:middle}.results-sheet-wrap iframe{display:block;width:100%;height:58vh;min-height:420px;border:0}
@media(max-width:900px){.results-stat-grid{grid-template-columns:repeat(2,minmax(0,1fr));}.results-stat-card:last-child{grid-column:1/-1}.results-dashboard-head{padding:18px}.results-stat-grid{padding:14px 18px}.results-sheet-wrap{margin:0 18px 18px}}
@media(max-width:560px){.results-dashboard{padding:0}.results-dashboard-card{min-height:100vh;border-radius:0}.results-dashboard-head{align-items:flex-start}.results-dashboard-head h2{font-size:18px}.results-dashboard-refresh span{display:none}.results-dashboard-refresh{width:40px;height:40px;padding:0}.results-stat-grid{gap:8px}.results-stat-card{min-height:76px;padding:11px}.results-stat-card strong{font-size:20px}.results-sheet-wrap iframe{height:55vh;min-height:360px}}
</style>

</body>
</html>
