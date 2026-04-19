<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LLFC eFootball Division System</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@400;500;600;700&family=Montserrat:wght@400;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
/* ===== UCL THEME ===== */
:root{
  --ucl-navy:#0A1628;
  --ucl-blue:#1B3A6B;
  --ucl-mid:#2A5298;
  --ucl-light:#4472C4;
  --ucl-bright:#5B8FE8;
  --ucl-star:#F5C518;
  --ucl-silver:#C8D8F0;
  --ucl-white:#EEF4FF;
  --ucl-dark:#060E1C;
  --ucl-card:#0D1F3C;
  --ucl-border:rgba(68,114,196,0.35);
  --gold:#FFD700;--silver:#C0C0C0;--bronze:#CD7F32;
  --green:#00E676;--yellow:#FFEA00;--red:#FF3D3D;--purple:#CE93D8;
  --card-bg:var(--ucl-card);--card-border:var(--ucl-border);
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{font-family:'Montserrat',sans-serif;background:var(--ucl-dark);color:var(--ucl-white);min-height:100vh;overflow-x:hidden;}

body::before{
  content:'';position:fixed;inset:0;
  background:
    radial-gradient(ellipse at 20% 20%, rgba(27,58,107,0.5) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 80%, rgba(42,82,152,0.3) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 50%, rgba(6,14,28,0.8) 0%, transparent 100%);
  pointer-events:none;z-index:0;
}
body::after{
  content:'';position:fixed;inset:0;
  background-image:
    radial-gradient(1px 1px at 10% 15%, rgba(245,197,24,0.6) 0%, transparent 100%),
    radial-gradient(1px 1px at 30% 40%, rgba(245,197,24,0.4) 0%, transparent 100%),
    radial-gradient(1px 1px at 50% 25%, rgba(255,255,255,0.3) 0%, transparent 100%),
    radial-gradient(1px 1px at 70% 60%, rgba(245,197,24,0.5) 0%, transparent 100%),
    radial-gradient(1px 1px at 85% 20%, rgba(255,255,255,0.25) 0%, transparent 100%),
    radial-gradient(1px 1px at 15% 70%, rgba(245,197,24,0.4) 0%, transparent 100%),
    radial-gradient(1px 1px at 60% 80%, rgba(255,255,255,0.2) 0%, transparent 100%),
    radial-gradient(1px 1px at 90% 45%, rgba(245,197,24,0.35) 0%, transparent 100%),
    radial-gradient(1px 1px at 40% 90%, rgba(255,255,255,0.15) 0%, transparent 100%),
    radial-gradient(1px 1px at 75% 35%, rgba(245,197,24,0.5) 0%, transparent 100%);
  pointer-events:none;z-index:0;
}

/* ===== HEADER ===== */
header{
  position:sticky;top:0;z-index:1000;
  background:rgba(6,14,28,0.97);
  backdrop-filter:blur(16px);
  border-bottom:1px solid var(--ucl-border);
  box-shadow:0 4px 30px rgba(27,58,107,0.5);
}
.header-inner{max-width:1400px;margin:0 auto;padding:0 20px;display:flex;align-items:center;justify-content:space-between;height:62px;gap:8px;}
.logo-area{display:flex;align-items:center;gap:12px;cursor:pointer;flex-shrink:0;}
.logo-badge{
  width:44px;height:44px;
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-blue));
  border:2px solid var(--ucl-light);
  border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-family:'Bebas Neue',sans-serif;font-size:13px;color:white;
  box-shadow:0 0 16px rgba(68,114,196,0.5);flex-shrink:0;letter-spacing:0.5px;
}
.logo-text{display:flex;flex-direction:column;line-height:1.1;}
.logo-main{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:3px;color:var(--ucl-white);}
.logo-sub{font-size:9px;color:var(--ucl-star);letter-spacing:4px;text-transform:uppercase;font-weight:700;}
.header-nav{display:flex;gap:2px;align-items:center;}
.nav-btn{
  background:none;border:1px solid transparent;color:var(--ucl-silver);
  padding:7px 14px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:12px;
  letter-spacing:1px;cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;
}
.nav-btn:hover,.nav-btn.active{color:var(--ucl-white);border-color:var(--ucl-light);background:rgba(68,114,196,0.18);}
.header-auth{display:flex;gap:6px;align-items:center;flex-shrink:0;}
.btn-login{
  background:transparent;border:1px solid var(--ucl-light);color:var(--ucl-bright);
  padding:6px 14px;font-family:'Montserrat',sans-serif;font-weight:700;font-size:12px;
  cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;
}
.btn-login:hover{background:var(--ucl-mid);color:white;}
.btn-register{
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));
  border:none;color:white;padding:6px 14px;
  font-family:'Montserrat',sans-serif;font-weight:700;font-size:12px;
  cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;
}
.btn-register:hover{background:linear-gradient(135deg,var(--ucl-light),var(--ucl-bright));box-shadow:0 0 12px rgba(68,114,196,0.5);}
.user-pill{
  display:flex;align-items:center;gap:8px;
  background:rgba(68,114,196,0.15);border:1px solid var(--ucl-light);
  border-radius:20px;padding:4px 14px 4px 4px;cursor:pointer;
}
.user-avatar{
  width:30px;height:30px;
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));
  border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-size:12px;font-weight:700;flex-shrink:0;font-family:'Bebas Neue',sans-serif;
}
.user-name{font-size:13px;font-weight:600;color:var(--ucl-white);}
.mod-badge-hdr{font-size:9px;background:rgba(206,147,216,0.25);border:1px solid var(--purple);color:var(--purple);padding:1px 5px;border-radius:3px;letter-spacing:1px;}

/* ===== MAIN ===== */
main{position:relative;z-index:1;max-width:1400px;margin:0 auto;padding:24px 20px;min-height:calc(100vh - 62px);}
.page{display:none;}.page.active{display:block;animation:fadeIn 0.3s ease;}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

/* ===== CARDS ===== */
.card{background:var(--ucl-card);border:1px solid var(--ucl-border);border-radius:10px;padding:20px;}
.card-blue{background:linear-gradient(135deg,rgba(27,58,107,0.5),rgba(10,22,40,0.95));border:1px solid var(--ucl-light);}

/* ===== BUTTONS ===== */
.btn-primary{
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));
  color:white;border:none;padding:10px 24px;
  font-family:'Montserrat',sans-serif;font-weight:700;font-size:13px;
  letter-spacing:1px;cursor:pointer;border-radius:6px;text-transform:uppercase;
  transition:all .2s;box-shadow:0 4px 14px rgba(68,114,196,0.35);
}
.btn-primary:hover{background:linear-gradient(135deg,var(--ucl-light),var(--ucl-bright));transform:translateY(-1px);box-shadow:0 6px 18px rgba(68,114,196,0.5);}
.btn-secondary{
  background:transparent;color:var(--ucl-silver);
  border:1px solid rgba(68,114,196,0.5);
  padding:10px 24px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:13px;
  cursor:pointer;border-radius:6px;text-transform:uppercase;transition:all .2s;
}
.btn-secondary:hover{border-color:var(--ucl-light);background:rgba(68,114,196,0.1);color:white;}
.btn-sm{padding:5px 12px;font-family:'Montserrat',sans-serif;font-weight:700;font-size:11px;letter-spacing:0.5px;cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;}
.btn-approve{background:rgba(0,230,118,.15);color:#00E676;border:1px solid rgba(0,230,118,.4);}
.btn-approve:hover{background:rgba(0,230,118,.3);}
.btn-reject{background:rgba(255,61,61,.15);color:#FF3D3D;border:1px solid rgba(255,61,61,.4);}
.btn-reject:hover{background:rgba(255,61,61,.3);}
.btn-edit{background:rgba(255,234,0,.12);color:#FFEA00;border:1px solid rgba(255,234,0,.35);}
.btn-edit:hover{background:rgba(255,234,0,.22);}
.btn-ban{background:rgba(206,147,216,.15);color:#CE93D8;border:1px solid rgba(206,147,216,.35);}
.btn-ban:hover{background:rgba(206,147,216,.25);}
.btn-mod{background:rgba(68,153,255,.14);color:#82B1FF;border:1px solid rgba(68,153,255,.35);}
.btn-mod:hover{background:rgba(68,153,255,.25);}
.w-full{width:100%;}

/* ===== SECTION TITLE ===== */
.section-title{
  font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:4px;
  color:var(--ucl-white);display:flex;align-items:center;gap:14px;margin-bottom:18px;
}
.section-title::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--ucl-light),transparent);}

/* ===== HERO ===== */
.hero{
  background:linear-gradient(135deg,rgba(27,58,107,0.5) 0%,rgba(10,22,40,0.95) 60%);
  border:1px solid var(--ucl-light);border-radius:14px;padding:40px 32px;margin-bottom:24px;
  position:relative;overflow:hidden;
}
.hero::before{
  content:'UCL';position:absolute;right:-20px;bottom:-30px;
  font-family:'Bebas Neue',sans-serif;font-size:220px;
  color:rgba(68,114,196,0.05);pointer-events:none;line-height:1;letter-spacing:10px;
}
.hero::after{
  content:'';position:absolute;top:0;left:0;right:0;height:2px;
  background:linear-gradient(90deg,transparent,var(--ucl-star),var(--ucl-light),transparent);
}
.hero-tag{
  display:inline-block;background:linear-gradient(135deg,var(--ucl-star),#E6A800);
  color:#0A1628;font-size:11px;font-weight:800;letter-spacing:3px;
  padding:3px 12px;border-radius:2px;margin-bottom:12px;text-transform:uppercase;
}
.hero h1{font-family:'Bebas Neue',sans-serif;font-size:clamp(32px,5vw,68px);letter-spacing:5px;line-height:1;margin-bottom:12px;color:var(--ucl-white);}
.hero h1 span{color:var(--ucl-star);}
.hero p{color:var(--ucl-silver);font-size:15px;max-width:520px;margin-bottom:24px;line-height:1.6;}
.hero-actions{display:flex;gap:12px;flex-wrap:wrap;}

/* ===== STATS ===== */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:12px;margin-bottom:24px;}
.stat-card{
  background:var(--ucl-card);border:1px solid var(--ucl-border);border-radius:10px;padding:16px;
  text-align:center;transition:border-color .2s;
  background:linear-gradient(135deg,rgba(27,58,107,0.3),rgba(10,22,40,0.8));
}
.stat-card:hover{border-color:var(--ucl-light);}
.stat-num{font-family:'Bebas Neue',sans-serif;font-size:36px;color:var(--ucl-star);line-height:1;}
.stat-label{font-size:10px;color:var(--ucl-silver);letter-spacing:2px;text-transform:uppercase;margin-top:4px;}

/* ===== GRIDS ===== */
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:22px;}
.three-col{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;}
@media(max-width:900px){.two-col{grid-template-columns:1fr;}.three-col{grid-template-columns:1fr 1fr;}.header-nav{display:none;}}
@media(max-width:500px){.three-col{grid-template-columns:1fr;}}

/* ===== DIVISION BADGES ===== */
.div-badge{
  display:inline-flex;align-items:center;justify-content:center;
  width:34px;height:34px;border-radius:50%;font-weight:800;font-size:13px;
  flex-shrink:0;font-family:'Montserrat',sans-serif;
}
.div-1{background:linear-gradient(135deg,#FFD700,#FF8C00);color:#000;box-shadow:0 0 10px rgba(255,215,0,0.5);}
.div-2{background:linear-gradient(135deg,#E8E8E8,#909090);color:#000;box-shadow:0 0 8px rgba(192,192,192,0.4);}
.div-3{background:linear-gradient(135deg,#E8A060,#8B4513);color:#fff;box-shadow:0 0 8px rgba(205,127,50,0.4);}
.div-4{background:linear-gradient(135deg,#3A8FD4,#1B5A9E);color:#fff;box-shadow:0 0 6px rgba(58,143,212,0.4);}
.div-5{background:linear-gradient(135deg,#2E75B6,#1A4A7A);color:#eee;}
.div-6{background:linear-gradient(135deg,#1B5499,#0E3060);color:#ccc;}
.div-7{background:linear-gradient(135deg,#123C7A,#082050);color:#bbb;}
.div-8{background:linear-gradient(135deg,#0A2850,#061530);color:#999;border:1px solid #1B3A6B;}
.div-9{background:linear-gradient(135deg,#071428,#030A14);color:#667;border:1px solid #1B3A6B;}

/* ===== DIVISION GUIDE CARDS ===== */
.div-guide-card{
  background:linear-gradient(135deg,rgba(0,100,50,0.22),rgba(10,22,40,0.9));
  border:1px solid rgba(0,200,80,0.35);border-radius:12px;padding:18px;
  transition:all .2s;
}
.div-guide-card:hover{border-color:rgba(0,230,118,0.6);transform:translateY(-2px);box-shadow:0 6px 20px rgba(0,200,80,0.15);}
.div-guide-name{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:2px;color:#00E676;margin:8px 0 4px;}
.div-guide-desc{font-size:12px;color:var(--ucl-silver);line-height:1.5;}
.div-guide-pts{font-size:11px;color:#FFEA00;font-weight:700;margin-top:5px;letter-spacing:1px;}
.div-guide-badge{font-size:10px;color:#00E676;margin-top:4px;font-weight:700;letter-spacing:1.5px;}

/* ===== TABLE ===== */
.lb-table-wrap{overflow-x:auto;border-radius:10px;border:1px solid var(--ucl-border);}
table{width:100%;border-collapse:collapse;}
thead tr{background:#0D1E3A !important;}
thead th{
  padding:12px 14px;text-align:left;font-size:10px;letter-spacing:2px;
  text-transform:uppercase;color:#82B1FF !important;font-weight:700;
  white-space:nowrap;background:#0D1E3A !important;
}
tbody tr{border-bottom:1px solid rgba(68,114,196,0.1);transition:background .15s;}
tbody tr:hover{background:rgba(68,114,196,0.1) !important;}
tbody tr:last-child{border-bottom:none;}
tbody td{padding:11px 14px;font-size:14px;font-weight:500;vertical-align:middle;color:#D0E4FF !important;}
tbody tr.top-1{background:linear-gradient(90deg,rgba(255,215,0,0.1),transparent) !important;}
tbody tr.top-2{background:linear-gradient(90deg,rgba(192,192,192,0.07),transparent) !important;}
tbody tr.top-3{background:linear-gradient(90deg,rgba(205,127,50,0.07),transparent) !important;}
.rank-num{font-family:'Bebas Neue',sans-serif;font-size:24px;color:#4472C4;}
.rank-1{color:var(--gold)!important;}.rank-2{color:var(--silver)!important;}.rank-3{color:var(--bronze)!important;}

.wdl-row{display:flex;align-items:center;gap:5px;}
.wdl-pill{display:inline-flex;align-items:center;gap:3px;padding:4px 9px;border-radius:5px;font-size:12px;font-weight:700;white-space:nowrap;}
.wdl-w{background:rgba(0,230,118,.18);color:#00E676;border:1px solid rgba(0,230,118,.35);}
.wdl-d{background:rgba(255,234,0,.15);color:#FFEA00;border:1px solid rgba(255,234,0,.3);}
.wdl-l{background:rgba(255,61,61,.15);color:#FF5555;border:1px solid rgba(255,61,61,.3);}
.wdl-num{font-family:'Bebas Neue',sans-serif;font-size:17px;line-height:1;}

.winrate-wrap{display:flex;align-items:center;gap:5px;}
.winrate-bar{background:rgba(255,255,255,.08);border-radius:8px;height:5px;width:52px;overflow:hidden;flex-shrink:0;position:relative;}
.winrate-fill{position:absolute;left:0;top:0;bottom:0;background:linear-gradient(90deg,var(--ucl-mid),var(--ucl-bright));border-radius:8px;}
.winrate-pct{font-size:12px;font-weight:700;color:#82B1FF;white-space:nowrap;}

.form-dots{display:flex;gap:3px;align-items:center;}
.form-dot{width:9px;height:9px;border-radius:50%;}
.form-w{background:#00E676;}.form-d{background:#FFEA00;}.form-l{background:#FF3D3D;}

.player-link{cursor:pointer;color:#D0E4FF;font-weight:600;transition:color .2s;display:inline-flex;align-items:center;gap:7px;}
.player-link:hover{color:var(--ucl-star);}

.status-badge{display:inline-block;padding:2px 8px;border-radius:8px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;}
.status-confirmed{background:rgba(0,230,118,.18);color:#00E676;border:1px solid rgba(0,230,118,.3);}
.status-pending{background:rgba(255,234,0,.15);color:#FFEA00;border:1px solid rgba(255,234,0,.3);}
.status-disputed{background:rgba(255,61,61,.18);color:#FF5555;border:1px solid rgba(255,61,61,.3);}

.lb-tabs{display:flex;gap:5px;margin-bottom:18px;background:rgba(27,58,107,.2);border:1px solid var(--ucl-border);border-radius:10px;padding:5px;flex-wrap:wrap;}
.lb-tab{flex:1;min-width:70px;background:none;border:none;color:var(--ucl-silver);padding:8px 12px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:12px;cursor:pointer;border-radius:7px;transition:all .2s;text-transform:uppercase;letter-spacing:1px;}
.lb-tab.active{background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));color:white;box-shadow:0 2px 8px rgba(68,114,196,0.4);}

.search-bar{display:flex;gap:8px;margin-bottom:16px;}
.search-input{flex:1;background:rgba(27,58,107,.25);border:1px solid var(--ucl-border);border-radius:6px;color:#D0E4FF;padding:10px 14px;font-family:'Montserrat',sans-serif;font-size:14px;}
.search-input:focus{outline:none;border-color:var(--ucl-light);}
.search-input::placeholder{color:#4472C4;}
.form-select-sm{background:rgba(27,58,107,.25);border:1px solid var(--ucl-border);border-radius:6px;color:#D0E4FF;padding:10px 10px;font-family:'Montserrat',sans-serif;font-size:12px;cursor:pointer;}
.form-select-sm:focus{outline:none;border-color:var(--ucl-light);}
.form-select-sm option{background:#0D1E3A;color:#D0E4FF;}

.match-form{display:grid;gap:14px;}
.form-group{display:flex;flex-direction:column;gap:6px;}
.form-label{font-size:10px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:#82B1FF;}
.form-input,.form-select{
  background:rgba(27,58,107,.2);border:1px solid var(--ucl-border);border-radius:6px;
  color:#D0E4FF;padding:10px 14px;font-family:'Montserrat',sans-serif;font-size:14px;
  font-weight:500;transition:border-color .2s;width:100%;
}
.form-input:focus,.form-select:focus{outline:none;border-color:var(--ucl-light);}
.form-select option{background:#0D1E3A;color:#D0E4FF;}
.score-row{display:grid;grid-template-columns:1fr auto 1fr;gap:12px;align-items:center;}
.score-vs{font-family:'Bebas Neue',sans-serif;font-size:24px;color:var(--ucl-star);text-align:center;}
.score-input{text-align:center;font-size:28px;font-family:'Bebas Neue',sans-serif;padding:10px;}

/* ===== MODAL ===== */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.88);z-index:2000;display:none;align-items:center;justify-content:center;padding:16px;backdrop-filter:blur(6px);}
.modal-overlay.open{display:flex;}
.modal{
  background:#0A1628;border:1px solid var(--ucl-light);border-radius:12px;
  padding:26px;width:100%;max-width:480px;max-height:90vh;overflow-y:auto;position:relative;
  box-shadow:0 20px 60px rgba(0,0,0,.7);
}
.modal-title{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:3px;color:var(--ucl-white);margin-bottom:18px;}
.modal-close{
  position:absolute;top:14px;right:14px;
  background:rgba(68,114,196,.2);border:1px solid var(--ucl-light);
  color:var(--ucl-bright);width:28px;height:28px;border-radius:50%;
  font-size:13px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .2s;
}
.modal-close:hover{background:var(--ucl-mid);color:white;}

/* ===== TOAST ===== */
.toast{
  position:fixed;bottom:80px;right:16px;z-index:9999;
  background:#0D1E3A;border-left:4px solid var(--ucl-light);border-radius:8px;
  padding:13px 18px;min-width:240px;max-width:340px;
  box-shadow:0 8px 30px rgba(0,0,0,.6);transform:translateX(120%);
  transition:transform .3s;font-weight:600;font-size:14px;color:#D0E4FF;
}
.toast.show{transform:translateX(0);}
.toast.success{border-color:var(--green);}
.toast.error{border-color:#FF3D3D;}
.toast.info{border-color:var(--ucl-star);}

/* ===== NEWS TICKER ===== */
.news-ticker{
  background:linear-gradient(135deg,rgba(27,58,107,0.4),rgba(10,22,40,0.9));
  border:1px solid var(--ucl-border);border-radius:8px;margin-bottom:18px;overflow:hidden;display:flex;align-items:center;
}
.news-label{
  background:linear-gradient(135deg,var(--ucl-star),#E6A800);color:#0A1628;
  padding:9px 16px;font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:2px;flex-shrink:0;white-space:nowrap;
}
.news-scroll-wrap{overflow:hidden;flex:1;padding:9px 14px;}
.news-scroll-text{font-size:13px;font-weight:600;color:var(--ucl-star);white-space:nowrap;display:inline-block;animation:scrollNews 22s linear infinite;}
@keyframes scrollNews{0%{transform:translateX(100vw);}100%{transform:translateX(-100%);}}

/* ===== MATCH CARD ===== */
.match-card{
  background:linear-gradient(135deg,rgba(27,58,107,.2),rgba(10,22,40,.8));
  border:1px solid var(--ucl-border);border-radius:8px;padding:13px 16px;margin-bottom:9px;
  display:flex;align-items:center;gap:12px;transition:all .2s;
}
.match-card:hover{border-color:var(--ucl-light);transform:translateX(2px);}
.match-card.high-score{border-color:rgba(245,197,24,.45);}
.match-result-badge{width:36px;height:36px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:17px;font-weight:700;flex-shrink:0;}
.result-W{background:rgba(0,230,118,.2);color:#00E676;border:1px solid rgba(0,230,118,.4);}
.result-D{background:rgba(255,234,0,.18);color:#FFEA00;border:1px solid rgba(255,234,0,.4);}
.result-L{background:rgba(255,61,61,.18);color:#FF5555;border:1px solid rgba(255,61,61,.4);}
.match-info{flex:1;min-width:0;}
.match-vs{font-size:14px;font-weight:600;color:#D0E4FF;}
.match-meta{font-size:11px;color:#4472C4;margin-top:2px;}
.match-score{font-family:'Bebas Neue',sans-serif;font-size:26px;color:var(--ucl-white);text-align:right;flex-shrink:0;}
.high-score-badge{background:rgba(245,197,24,.2);color:var(--ucl-star);border:1px solid rgba(245,197,24,.4);border-radius:4px;font-size:10px;font-weight:700;padding:1px 7px;letter-spacing:1px;}
.x2-badge{background:rgba(0,230,118,.2);color:#00E676;border:1px solid rgba(0,230,118,.4);border-radius:4px;font-size:10px;font-weight:700;padding:1px 7px;letter-spacing:1px;}

/* ===== PENDING ===== */
.pending-item{
  background:linear-gradient(135deg,rgba(27,58,107,.2),rgba(10,22,40,.8));
  border:1px solid var(--ucl-border);border-radius:8px;padding:13px 16px;margin-bottom:8px;
  display:flex;align-items:center;gap:10px;flex-wrap:wrap;
}
.pending-info{flex:1;min-width:120px;}
.pending-name{font-size:15px;font-weight:700;color:#D0E4FF;}
.pending-meta{font-size:11px;color:#4472C4;margin-top:2px;}

/* ===== CONFIRM CARD ===== */
.confirm-card{
  background:linear-gradient(135deg,rgba(68,114,196,.15),rgba(10,22,40,.9));
  border:1px solid var(--ucl-light);border-radius:10px;padding:16px;margin-bottom:12px;
}
.confirm-vs{display:flex;align-items:center;justify-content:space-between;gap:8px;margin-bottom:10px;flex-wrap:wrap;}
.confirm-player{text-align:center;flex:1;}
.confirm-player-name{font-size:15px;font-weight:700;color:#D0E4FF;}
.confirm-score-display{font-family:'Bebas Neue',sans-serif;font-size:36px;color:var(--ucl-star);padding:0 12px;flex-shrink:0;}

/* ===== PROFILE ===== */
.profile-header{display:flex;gap:22px;align-items:flex-start;flex-wrap:wrap;margin-bottom:22px;}
.profile-avatar{
  width:80px;height:80px;
  background:linear-gradient(135deg,var(--ucl-blue),var(--ucl-light));
  border:3px solid var(--ucl-light);border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-family:'Bebas Neue',sans-serif;font-size:32px;color:white;flex-shrink:0;
  box-shadow:0 0 24px rgba(68,114,196,.5);
}
.profile-info{flex:1;}
.profile-name{font-family:'Bebas Neue',sans-serif;font-size:36px;letter-spacing:3px;line-height:1;color:var(--ucl-white);}
.profile-cat{
  display:inline-block;background:rgba(68,114,196,.25);border:1px solid var(--ucl-light);
  color:var(--ucl-bright);font-size:11px;font-weight:700;letter-spacing:2px;
  padding:2px 10px;border-radius:3px;margin-top:5px;text-transform:uppercase;
}
.profile-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(92px,1fr));gap:10px;margin-bottom:18px;}
.p-stat{
  background:linear-gradient(135deg,rgba(27,58,107,.3),rgba(10,22,40,.8));
  border:1px solid var(--ucl-border);border-radius:8px;padding:12px;text-align:center;
}
.p-stat-val{font-family:'Bebas Neue',sans-serif;font-size:28px;line-height:1;}
.p-stat-lbl{font-size:9px;color:#4472C4;letter-spacing:2px;text-transform:uppercase;margin-top:3px;}

/* ===== PROMO ===== */
.promo-tracker{
  background:linear-gradient(135deg,rgba(0,100,50,.2),rgba(10,22,40,.9));
  border:1px solid rgba(0,200,80,.3);border-radius:10px;padding:16px;margin-top:16px;
}
.promo-title{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:#00E676;margin-bottom:8px;}
.promo-bar-wrap{background:rgba(255,255,255,.07);border-radius:8px;height:10px;margin-bottom:6px;overflow:hidden;}
.promo-bar-fill{height:100%;background:linear-gradient(90deg,#00A550,#00E676);border-radius:8px;transition:width .5s;}
.promo-label{font-size:12px;color:#82B1FF;display:flex;justify-content:space-between;}
.promo-cycle-info{font-size:11px;color:#FFEA00;margin-top:6px;font-weight:700;}

/* ===== BADGES ===== */
.badges-row{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px;}
.player-badge{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;border-radius:5px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;border:1px solid;}
.badge-gold{background:rgba(255,215,0,.15);color:var(--gold);border-color:rgba(255,215,0,.4);}
.badge-silver{background:rgba(192,192,192,.12);color:var(--silver);border-color:rgba(192,192,192,.35);}
.badge-green{background:rgba(0,230,118,.13);color:#00E676;border-color:rgba(0,230,118,.35);}
.badge-blue{background:rgba(68,114,196,.15);color:#82B1FF;border-color:rgba(68,114,196,.4);}
.badge-purple{background:rgba(206,147,216,.13);color:#CE93D8;border-color:rgba(206,147,216,.35);}
.badge-red{background:rgba(255,61,61,.13);color:#FF5555;border-color:rgba(255,61,61,.35);}
.badge-star{background:rgba(245,197,24,.13);color:var(--ucl-star);border-color:rgba(245,197,24,.4);}

.cat-main{color:#FF6B6B;font-weight:700;}
.cat-youth{color:#82B1FF;font-weight:700;}
.cat-academy{color:#A5D6A7;font-weight:700;}

/* ===== ADMIN ===== */
.admin-tabs{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:18px;border-bottom:1px solid var(--ucl-border);padding-bottom:10px;}
.admin-tab{background:none;border:1px solid transparent;color:var(--ucl-silver);padding:7px 13px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:11px;cursor:pointer;border-radius:5px;transition:all .2s;text-transform:uppercase;letter-spacing:1px;}
.admin-tab.active{background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));color:white;border-color:var(--ucl-light);}
.admin-tab:hover:not(.active){border-color:var(--ucl-light);color:white;}

.mod-info-box{background:rgba(68,114,196,.1);border:1px solid rgba(68,114,196,.3);border-radius:8px;padding:14px;margin-bottom:16px;}
.mod-info-title{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:2px;color:#82B1FF;margin-bottom:5px;}

/* ===== RANKING CARD ===== */
.rc-card{width:820px;background:#060E1C;border:2px solid #1B3A6B;border-radius:14px;overflow:hidden;font-family:'Montserrat',sans-serif;}
.rc-header{background:linear-gradient(135deg,#0A1E3C 0%,#1B3A6B 40%,#0A1E3C 100%);padding:22px 28px 18px;position:relative;overflow:hidden;}
.rc-header::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,transparent,#F5C518,#4472C4,#F5C518,transparent);}
.rc-header::after{content:'UCL';position:absolute;right:-15px;bottom:-25px;font-family:'Bebas Neue',sans-serif;font-size:100px;color:rgba(68,114,196,0.07);pointer-events:none;}
.rc-header-top{display:flex;align-items:center;justify-content:space-between;}
.rc-title{font-family:'Bebas Neue',sans-serif;font-size:30px;letter-spacing:5px;color:white;}
.rc-subtitle{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:3px;color:rgba(255,255,255,0.6);margin-top:3px;}
.rc-period{background:rgba(245,197,24,.15);border:1px solid rgba(245,197,24,.4);border-radius:5px;padding:5px 14px;font-size:12px;font-weight:700;letter-spacing:2px;color:#F5C518;text-transform:uppercase;}
.rc-body{padding:0;background:#060E1C;}
.rc-row{display:grid;grid-template-columns:48px 1fr 90px 110px 80px 70px;align-items:center;padding:12px 28px;border-bottom:1px solid rgba(27,58,107,0.5);gap:8px;}
.rc-row:last-child{border-bottom:none;}
.rc-header-row{background:#0D1E3A !important;padding:9px 28px;border-bottom:2px solid rgba(68,114,196,0.4);}
.rc-header-row span{font-size:9px;letter-spacing:2px;text-transform:uppercase;color:#4472C4;font-weight:700;}
.rc-row.rank-1-row{background:linear-gradient(90deg,rgba(255,215,0,.08),transparent);}
.rc-row.rank-2-row{background:linear-gradient(90deg,rgba(192,192,192,.06),transparent);}
.rc-row.rank-3-row{background:linear-gradient(90deg,rgba(205,127,50,.06),transparent);}
.rc-rank{font-family:'Bebas Neue',sans-serif;font-size:28px;color:#1B3A6B;}
.rc-rank.r1{color:#FFD700;}.rc-rank.r2{color:#C0C0C0;}.rc-rank.r3{color:#CD7F32;}
.rc-player-info{display:flex;align-items:center;gap:10px;}
.rc-avatar{width:30px;height:30px;border-radius:50%;background:linear-gradient(135deg,#1B3A6B,#4472C4);display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:13px;color:white;flex-shrink:0;}
.rc-name{font-family:'Bebas Neue',sans-serif;font-size:17px;letter-spacing:1px;color:#D0E4FF;}
.rc-div-small{font-size:9px;color:#4472C4;letter-spacing:1px;font-weight:600;}
.rc-rating{font-family:'Bebas Neue',sans-serif;font-size:22px;color:#F5C518;text-align:right;}
.rc-wdl-nums{font-family:'Bebas Neue',sans-serif;font-size:14px;display:flex;gap:6px;}
.rc-w{color:#00E676;}.rc-d{color:#FFEA00;}.rc-l{color:#FF5555;}
.rc-winpct{font-family:'Bebas Neue',sans-serif;font-size:18px;color:#4472C4;text-align:right;}
.rc-footer{background:#040A14;padding:10px 28px;display:flex;justify-content:space-between;align-items:center;border-top:1px solid rgba(27,58,107,.4);}
.rc-footer-brand{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:4px;color:#1B3A6B;}
.rc-footer-date{font-size:10px;color:#1B3A6B;letter-spacing:2px;}

.ranking-card-preview{display:none;position:fixed;inset:0;background:rgba(0,0,0,.93);z-index:3000;align-items:center;justify-content:center;flex-direction:column;gap:18px;padding:20px;overflow:auto;}
.ranking-card-preview.open{display:flex;}
.ranking-card-close{position:absolute;top:16px;right:16px;background:rgba(27,58,107,.4);border:1px solid var(--ucl-light);color:white;width:34px;height:34px;border-radius:50%;font-size:16px;cursor:pointer;display:flex;align-items:center;justify-content:center;}

/* ===== MOBILE NAV ===== */
.mobile-nav{display:none;position:fixed;bottom:0;left:0;right:0;background:rgba(6,14,28,.98);border-top:1px solid var(--ucl-border);z-index:999;padding:6px 0;}
.mobile-nav-inner{display:flex;justify-content:space-around;}
.mob-nav-btn{display:flex;flex-direction:column;align-items:center;gap:2px;background:none;border:none;color:#4472C4;font-family:'Montserrat',sans-serif;font-size:10px;font-weight:600;padding:4px 10px;cursor:pointer;transition:color .2s;text-transform:uppercase;}
.mob-nav-btn.active,.mob-nav-btn:hover{color:var(--ucl-star);}
.mob-nav-icon{font-size:19px;}
@media(max-width:768px){.mobile-nav{display:block;}main{padding-bottom:72px;}}

/* ===== MISC ===== */
.loading-spinner{display:flex;align-items:center;justify-content:center;padding:48px;gap:12px;color:#4472C4;}
.spinner{width:26px;height:26px;border:2px solid rgba(68,114,196,0.2);border-top-color:var(--ucl-light);border-radius:50%;animation:spin .7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.empty-state{text-align:center;padding:48px 20px;color:#4472C4;}
.empty-icon{font-size:44px;margin-bottom:12px;}
.empty-text{font-size:17px;font-weight:700;color:#82B1FF;}
.empty-sub{font-size:13px;margin-top:5px;opacity:.6;}
.text-gold{color:var(--gold);}.text-green{color:#00E676;}.text-red{color:#FF5555;}.text-yellow{color:#FFEA00;}.text-blue{color:#82B1FF;}.text-gray{color:#4472C4;}.text-sm{font-size:13px;}.font-bold{font-weight:700;}
.mt-8{margin-top:8px;}.mt-12{margin-top:12px;}.mt-16{margin-top:16px;}.mb-8{margin-bottom:8px;}.mb-16{margin-bottom:16px;}

/* ====================================================
   ===== TOURNAMENT ANNOUNCEMENT BOARD =====
   ==================================================== */

/* Pulsing glow for live tournament */
@keyframes tourneyGlow {
  0%,100%{box-shadow:0 0 30px rgba(255,215,0,0.25),0 0 60px rgba(255,140,0,0.1);}
  50%{box-shadow:0 0 50px rgba(255,215,0,0.45),0 0 100px rgba(255,140,0,0.2);}
}
@keyframes shimmer {
  0%{transform:translateX(-100%);}
  100%{transform:translateX(100%);}
}
@keyframes pulse-dot {
  0%,100%{opacity:1;transform:scale(1);}
  50%{opacity:0.5;transform:scale(1.4);}
}
@keyframes countdownTick {
  0%{transform:scale(1);}
  50%{transform:scale(1.05);}
  100%{transform:scale(1);}
}

.tourney-announcement {
  position:relative;
  background:linear-gradient(135deg, rgba(10,6,0,0.98) 0%, rgba(40,20,0,0.95) 40%, rgba(10,6,0,0.98) 100%);
  border:2px solid rgba(255,200,0,0.6);
  border-radius:16px;
  padding:0;
  margin-bottom:24px;
  overflow:hidden;
  animation:tourneyGlow 3s ease-in-out infinite;
}
.tourney-announcement::before {
  content:'';
  position:absolute;top:0;left:0;right:0;height:3px;
  background:linear-gradient(90deg, transparent, #FFD700, #FF8C00, #FFD700, transparent);
}
.tourney-announcement::after {
  content:'TOURNAMENT';
  position:absolute;right:-10px;bottom:-15px;
  font-family:'Bebas Neue',sans-serif;font-size:120px;
  color:rgba(255,180,0,0.04);pointer-events:none;line-height:1;letter-spacing:8px;
}

/* Shimmer sweep effect */
.tourney-shimmer {
  position:absolute;inset:0;pointer-events:none;overflow:hidden;border-radius:16px;
}
.tourney-shimmer::after {
  content:'';
  position:absolute;top:0;left:-100%;width:60%;height:100%;
  background:linear-gradient(90deg, transparent, rgba(255,215,0,0.07), transparent);
  animation:shimmer 3.5s ease-in-out infinite;
}

.tourney-inner {
  display:flex;align-items:stretch;gap:0;flex-wrap:wrap;
}

/* LEFT: Big banner side */
.tourney-left {
  flex:1;min-width:200px;
  padding:28px 28px 24px;
  display:flex;flex-direction:column;justify-content:center;
  border-right:1px solid rgba(255,180,0,0.15);
}

.tourney-live-badge {
  display:inline-flex;align-items:center;gap:6px;
  background:rgba(255,50,50,0.15);border:1px solid rgba(255,80,80,0.4);
  border-radius:20px;padding:4px 10px;margin-bottom:12px;
  font-size:10px;font-weight:800;letter-spacing:2px;color:#FF5555;
  text-transform:uppercase;width:fit-content;
}
.live-dot {
  width:7px;height:7px;background:#FF3D3D;border-radius:50%;
  animation:pulse-dot 1s ease-in-out infinite;
}

.tourney-title {
  font-family:'Bebas Neue',sans-serif;
  font-size:clamp(24px,4vw,42px);
  letter-spacing:4px;
  line-height:1.05;
  color:#FFD700;
  text-shadow:0 0 30px rgba(255,215,0,0.4);
  margin-bottom:6px;
}

.tourney-subtitle {
  font-size:11px;font-weight:700;letter-spacing:3px;
  color:rgba(255,200,100,0.7);text-transform:uppercase;margin-bottom:16px;
}

.tourney-cta {
  background:linear-gradient(135deg,#FF8C00,#FFD700);
  color:#0A0600;border:none;
  padding:12px 28px;
  font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:2px;
  cursor:pointer;border-radius:6px;transition:all .2s;
  width:fit-content;
  box-shadow:0 4px 18px rgba(255,180,0,0.35);
}
.tourney-cta:hover {
  background:linear-gradient(135deg,#FFD700,#FFF0A0);
  transform:translateY(-2px);
  box-shadow:0 8px 28px rgba(255,215,0,0.5);
}

/* RIGHT: Stats grid */
.tourney-right {
  display:flex;flex-direction:column;justify-content:center;
  padding:24px 28px;gap:16px;min-width:280px;
}

.tourney-stats {
  display:grid;grid-template-columns:1fr 1fr;gap:10px;
}

.t-stat {
  background:rgba(255,180,0,0.06);
  border:1px solid rgba(255,180,0,0.2);
  border-radius:10px;padding:12px 14px;text-align:center;
  transition:border-color .2s;
}
.t-stat:hover{border-color:rgba(255,215,0,0.5);}

.t-stat-val {
  font-family:'Bebas Neue',sans-serif;
  font-size:28px;color:#FFD700;line-height:1;
}
.t-stat-lbl {
  font-size:9px;color:rgba(255,200,100,0.6);letter-spacing:2px;
  text-transform:uppercase;margin-top:3px;
}

/* Slot progress bar */
.slot-progress-wrap {
  background:rgba(255,180,0,0.06);border:1px solid rgba(255,180,0,0.2);
  border-radius:10px;padding:12px 14px;
}
.slot-progress-label {
  display:flex;justify-content:space-between;margin-bottom:7px;
  font-size:10px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;
}
.slot-progress-label span:first-child{color:rgba(255,200,100,0.7);}
.slot-progress-label span:last-child{color:#FFD700;font-family:'Bebas Neue',sans-serif;font-size:14px;}
.slot-bar {
  background:rgba(255,180,0,0.1);border-radius:6px;height:8px;overflow:hidden;
}
.slot-fill {
  height:100%;border-radius:6px;
  background:linear-gradient(90deg,#FF8C00,#FFD700);
  transition:width .8s ease;
}

/* ====================================================
   ===== TOURNAMENT REGISTRATION MODAL =====
   ==================================================== */

.tourney-modal {
  max-width:520px;
  background:linear-gradient(135deg,rgba(20,10,0,0.99),rgba(10,6,0,0.99));
  border:2px solid rgba(255,180,0,0.5);
}
.tourney-modal-header {
  background:linear-gradient(135deg,rgba(40,20,0,0.8),rgba(20,10,0,0.6));
  margin:-26px -26px 20px -26px;
  padding:22px 26px 18px;
  border-bottom:1px solid rgba(255,180,0,0.2);
  position:relative;overflow:hidden;
}
.tourney-modal-header::before {
  content:'';position:absolute;top:0;left:0;right:0;height:3px;
  background:linear-gradient(90deg,transparent,#FFD700,#FF8C00,#FFD700,transparent);
}
.tourney-modal-title {
  font-family:'Bebas Neue',sans-serif;font-size:28px;letter-spacing:4px;
  color:#FFD700;text-shadow:0 0 20px rgba(255,215,0,0.4);
}
.tourney-modal-sub {
  font-size:11px;color:rgba(255,200,100,0.6);letter-spacing:2px;margin-top:3px;text-transform:uppercase;
}

.t-form-label {
  font-size:10px;font-weight:700;letter-spacing:2px;text-transform:uppercase;
  color:rgba(255,200,100,0.8);
}
.t-form-input, .t-form-select {
  background:rgba(255,180,0,0.06);
  border:1px solid rgba(255,180,0,0.25);
  border-radius:6px;color:#FFE4A0;
  padding:11px 14px;font-family:'Montserrat',sans-serif;font-size:14px;
  font-weight:500;transition:border-color .2s;width:100%;
}
.t-form-input:focus,.t-form-select:focus{outline:none;border-color:rgba(255,215,0,0.6);background:rgba(255,180,0,0.1);}
.t-form-input::placeholder{color:rgba(255,180,0,0.3);}
.t-form-select option{background:#1A0E00;color:#FFE4A0;}
.t-form-input[readonly]{
  background:rgba(255,215,0,0.05);
  color:rgba(255,200,100,0.6);cursor:default;
}

.btn-tourney-submit {
  background:linear-gradient(135deg,#FF8C00,#FFD700);
  color:#0A0600;border:none;
  padding:13px 28px;
  font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:2px;
  cursor:pointer;border-radius:6px;transition:all .2s;width:100%;
  box-shadow:0 4px 18px rgba(255,180,0,0.3);margin-top:6px;
}
.btn-tourney-submit:hover{
  background:linear-gradient(135deg,#FFD700,#FFF0A0);
  transform:translateY(-2px);box-shadow:0 8px 24px rgba(255,215,0,0.45);
}
.tourney-fee-note {
  background:rgba(255,50,50,0.1);
  border:1px solid rgba(255,80,80,0.3);
  border-radius:8px;padding:12px 14px;
  font-size:12px;color:rgba(255,180,100,0.9);
  line-height:1.6;text-align:center;
}
.tourney-fee-amount {
  font-family:'Bebas Neue',sans-serif;font-size:22px;color:#FF5555;letter-spacing:1px;
}
.trx-help {
  font-size:11px;color:rgba(255,180,0,0.5);margin-top:5px;line-height:1.5;
}

/* ===== ADMIN TOURNAMENT TAB ===== */
.tourney-reg-item {
  background:linear-gradient(135deg,rgba(40,20,0,0.5),rgba(10,6,0,0.8));
  border:1px solid rgba(255,180,0,0.25);
  border-radius:8px;padding:13px 16px;margin-bottom:8px;
  display:flex;align-items:center;gap:10px;flex-wrap:wrap;
}
.tourney-reg-item.t-approved{border-color:rgba(0,230,118,0.3);}
.tourney-reg-item.t-rejected{border-color:rgba(255,61,61,0.3);}
.tourney-reg-info{flex:1;min-width:140px;}
.tourney-reg-name{font-size:15px;font-weight:700;color:#FFE4A0;}
.tourney-reg-meta{font-size:11px;color:rgba(255,180,0,0.5);margin-top:3px;}
.t-status-badge{display:inline-block;padding:2px 8px;border-radius:8px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;}
.t-status-pending{background:rgba(255,234,0,.15);color:#FFEA00;border:1px solid rgba(255,234,0,.3);}
.t-status-approved{background:rgba(0,230,118,.18);color:#00E676;border:1px solid rgba(0,230,118,.3);}
.t-status-rejected{background:rgba(255,61,61,.18);color:#FF5555;border:1px solid rgba(255,61,61,.3);}
</style>
</head>
<body>

<header>
  <div class="header-inner">
    <div class="logo-area" onclick="navTo('home')">
      <div class="logo-badge">LLFC</div>
      <div class="logo-text">
        <span class="logo-main">LLFC</span>
        <span class="logo-sub">eFootball Division</span>
      </div>
    </div>
    <nav class="header-nav">
      <button class="nav-btn active" id="navHome" onclick="navTo('home');setNavActive(this)">Home</button>
      <button class="nav-btn" id="navLeaderboard" onclick="navTo('leaderboard');setNavActive(this)">Rankings</button>
      <button class="nav-btn" id="navMatches" onclick="navTo('matches');setNavActive(this)">Matches</button>
      <button class="nav-btn" id="navSubmit" onclick="navTo('submit');setNavActive(this)">Submit</button>
    </nav>
    <div class="header-auth" id="headerAuth">
      <button class="btn-login" onclick="openModal('loginModal')">Login</button>
      <button class="btn-register" onclick="openModal('registerModal')">Register</button>
      <button class="btn-login" style="border-color:var(--ucl-star);color:var(--ucl-star);font-size:11px" onclick="navTo('admin')">Admin</button>
    </div>
  </div>
</header>

<main>

<!-- HOME -->
<div class="page active" id="page-home">

  <!-- NEWS TICKER -->
  <div class="news-ticker" id="newsTicker" style="display:none">
    <div class="news-label">BREAKING</div>
    <div class="news-scroll-wrap"><span class="news-scroll-text" id="newsText"></span></div>
  </div>

  <!-- ===== TOURNAMENT ANNOUNCEMENT BOARD ===== -->
  <div class="tourney-announcement" id="tourneyBoard">
    <div class="tourney-shimmer"></div>
    <div class="tourney-inner">
      <!-- Left: Title & CTA -->
      <div class="tourney-left">
        <div class="tourney-live-badge">
          <span class="live-dot"></span>
          Registration Open
        </div>
        <div class="tourney-title">LLFC PAID SOLO<br>TOURNAMENT</div>
        <div class="tourney-subtitle">Season 1 &bull; Powered by LLFC Division</div>
        <button class="tourney-cta" onclick="openTourneyReg()">
          &#9917; Click Here to Register
        </button>
      </div>
      <!-- Right: Stats -->
      <div class="tourney-right">
        <div class="tourney-stats">
          <div class="t-stat">
            <div class="t-stat-val">16</div>
            <div class="t-stat-lbl">Total Slots</div>
          </div>
          <div class="t-stat">
            <div class="t-stat-val" id="tStatFilled">-</div>
            <div class="t-stat-lbl">Registered</div>
          </div>
          <div class="t-stat">
            <div class="t-stat-val">৳50</div>
            <div class="t-stat-lbl">Entry Fee</div>
          </div>
          <div class="t-stat">
            <div class="t-stat-val">৳800</div>
            <div class="t-stat-lbl">Prize Pool</div>
          </div>
        </div>
        <div class="slot-progress-wrap">
          <div class="slot-progress-label">
            <span>Slot Progress</span>
            <span id="slotProgressText">0 / 16</span>
          </div>
          <div class="slot-bar">
            <div class="slot-fill" id="slotFill" style="width:0%"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- ===== END TOURNAMENT BOARD ===== -->

  <div class="hero">
    <div class="hero-tag">Season Active</div>
    <h1>LLFC <span>eFootball</span> Division</h1>
    <p>Play freely. Submit results. Climb the ranks. From Division 9 to Division 1 — prove yourself on the pitch.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="navTo('leaderboard')">View Rankings</button>
      <button class="btn-secondary" onclick="navTo('submit')">Submit Result</button>
    </div>
  </div>
  <div class="stats-grid">
    <div class="stat-card"><div class="stat-num" id="statPlayers">-</div><div class="stat-label">Active Players</div></div>
    <div class="stat-card"><div class="stat-num" id="statMatches">-</div><div class="stat-label">Total Matches</div></div>
    <div class="stat-card"><div class="stat-num" id="statToday">-</div><div class="stat-label">Today</div></div>
    <div class="stat-card"><div class="stat-num" id="statPending">-</div><div class="stat-label">Pending</div></div>
  </div>
  <div class="two-col">
    <div>
      <div class="section-title">Top Players</div>
      <div id="homeTopPlayers"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
    <div>
      <div class="section-title">Recent Matches</div>
      <div id="homeRecentMatches"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
  </div>
  <div class="mt-16">
    <div class="section-title">Division Structure</div>
    <div class="three-col" id="divisionGuide"></div>
  </div>
</div>

<!-- LEADERBOARD -->
<div class="page" id="page-leaderboard">
  <div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;margin-bottom:18px">
    <div class="section-title" style="margin-bottom:0;flex:1">Rankings</div>
    <button class="btn-primary" style="padding:9px 18px;font-size:11px;flex-shrink:0" onclick="openRankingCardPreview()">Download Ranking Card (JPG)</button>
  </div>
  <div class="lb-tabs">
    <button class="lb-tab active" onclick="switchLbTab('overall',this)">Overall</button>
    <button class="lb-tab" onclick="switchLbTab('monthly',this)">Monthly</button>
    <button class="lb-tab" onclick="switchLbTab('weekly',this)">Weekly</button>
    <button class="lb-tab" onclick="switchLbTab('daily',this)">Daily</button>
  </div>
  <div class="search-bar">
    <input class="search-input" placeholder="Search player..." id="lbSearch" oninput="filterLeaderboard()">
    <select class="form-select-sm" id="lbDivFilter" onchange="filterLeaderboard()">
      <option value="">All Divs</option>
      <option value="1">Div 1</option><option value="2">Div 2</option><option value="3">Div 3</option>
      <option value="4">Div 4</option><option value="5">Div 5</option><option value="6">Div 6</option>
      <option value="7">Div 7</option><option value="8">Div 8</option><option value="9">Div 9</option>
    </select>
  </div>
  <div class="lb-table-wrap">
    <table>
      <thead>
        <tr>
          <th>#</th><th>Player</th><th>Div</th><th>Rating</th>
          <th>W / D / L</th><th>MP</th><th>Win%</th><th>GD</th><th>CS</th><th>Form</th><th>Cycle</th>
        </tr>
      </thead>
      <tbody id="lbTableBody">
        <tr><td colspan="11" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- MATCHES -->
<div class="page" id="page-matches">
  <div class="section-title">Match History</div>
  <div class="search-bar">
    <input class="search-input" placeholder="Search player..." id="matchSearch" oninput="filterMatches()">
    <select class="form-select-sm" id="matchStatusFilter" onchange="filterMatches()">
      <option value="">All</option><option value="confirmed">Confirmed</option>
      <option value="pending">Pending</option><option value="disputed">Disputed</option>
    </select>
  </div>
  <div id="matchesList"><div class="loading-spinner"><div class="spinner"></div></div></div>
  <div id="pendingConfirmSection" style="display:none">
    <div class="section-title mt-16">Awaiting Your Confirmation</div>
    <div id="pendingConfirmList"></div>
  </div>
</div>

<!-- SUBMIT -->
<div class="page" id="page-submit">
  <div class="section-title">Submit Match Result</div>
  <div id="submitRequireLogin" style="display:none">
    <div class="empty-state">
      <div class="empty-icon">&#128274;</div>
      <div class="empty-text">Login Required</div>
      <div class="empty-sub">Please login to submit match results</div>
      <button class="btn-primary mt-12" onclick="openModal('loginModal')">Login Now</button>
    </div>
  </div>
  <div id="submitForm" style="display:none">
    <div class="card card-blue" style="max-width:540px;margin:0 auto">
      <div class="match-form">
        <div class="form-group"><label class="form-label">Your Name</label><input class="form-input" id="submitMyName" readonly></div>
        <div class="form-group"><label class="form-label">Opponent</label>
          <select class="form-select" id="submitOpponent"><option value="">-- Select Opponent --</option></select>
        </div>
        <div class="form-group">
          <label class="form-label">Score</label>
          <div class="score-row">
            <input class="form-input score-input" type="number" min="0" max="99" id="scoreA" placeholder="0">
            <div class="score-vs">VS</div>
            <input class="form-input score-input" type="number" min="0" max="99" id="scoreB" placeholder="0">
          </div>
        </div>
        <div class="form-group"><label class="form-label">Match Date</label><input class="form-input" type="date" id="matchDate"></div>
        <button class="btn-primary w-full" onclick="submitMatchResult()">Submit Result</button>
        <p class="text-gray text-sm" style="text-align:center;margin-top:8px">Opponent must confirm. Multiple pending matches allowed.</p>
      </div>
    </div>
  </div>
</div>

<!-- PROFILE -->
<div class="page" id="page-profile">
  <button class="btn-secondary mb-16" onclick="navBack()">&#8592; Back</button>
  <div id="profileContent"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

<!-- MY PROFILE -->
<div class="page" id="page-myprofile">
  <div class="section-title">My Profile</div>
  <div id="myProfileContent"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">
  <div class="section-title">Admin Panel</div>
  <div id="adminLoginWrap">
    <div class="card" style="max-width:340px;margin:0 auto">
      <div class="modal-title">Admin Access</div>
      <div class="match-form">
        <div class="form-group"><label class="form-label">Password</label>
          <input class="form-input" type="password" id="adminPwInput" placeholder="Enter admin password" onkeydown="if(event.key==='Enter')adminLogin()">
        </div>
        <button class="btn-primary w-full" onclick="adminLogin()">Enter Panel</button>
      </div>
    </div>
  </div>
  <div id="adminPanelWrap" style="display:none">
    <div class="admin-tabs">
      <button class="admin-tab active" onclick="switchAdminTab('pending',this)">Pending</button>
      <button class="admin-tab" onclick="switchAdminTab('players',this)">Players</button>
      <button class="admin-tab" onclick="switchAdminTab('adminMatches',this)">Matches</button>
      <button class="admin-tab" onclick="switchAdminTab('tournament',this)">&#127942; Tournament</button>
      <button class="admin-tab" onclick="switchAdminTab('moderators',this)">Moderators</button>
      <button class="admin-tab" onclick="switchAdminTab('season',this)">Season</button>
      <button class="admin-tab" onclick="switchAdminTab('adminSettings',this)">Settings</button>
    </div>
    <div id="adminTab-pending">
      <div class="section-title">Pending Registrations</div>
      <div id="adminPendingList"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
    <div id="adminTab-players" style="display:none">
      <div class="section-title">All Players</div>
      <div class="search-bar"><input class="search-input" placeholder="Search..." id="adminPlayerSearch" oninput="filterAdminPlayers()"></div>
      <div id="adminPlayersList"></div>
    </div>
    <div id="adminTab-adminMatches" style="display:none">
      <div class="section-title">All Matches</div>
      <div id="adminMatchesList"></div>
    </div>

    <!-- TOURNAMENT ADMIN TAB -->
    <div id="adminTab-tournament" style="display:none">
      <div class="section-title">Tournament Registrations</div>
      <div class="mod-info-box" style="border-color:rgba(255,180,0,0.3);background:rgba(255,180,0,0.06)">
        <div class="mod-info-title" style="color:#FFD700">Paid Solo Tournament</div>
        <p style="font-size:12px;color:rgba(255,200,100,0.7)">Review bKash TRX IDs and approve or reject registrations below. Approved players are added to the 16-slot bracket.</p>
      </div>
      <div style="display:flex;gap:10px;margin-bottom:16px;flex-wrap:wrap">
        <div class="t-stat" style="flex:1;min-width:90px"><div class="t-stat-val" id="adminTotalRegs">-</div><div class="t-stat-lbl">Total Regs</div></div>
        <div class="t-stat" style="flex:1;min-width:90px"><div class="t-stat-val" id="adminApprovedRegs">-</div><div class="t-stat-lbl">Approved</div></div>
        <div class="t-stat" style="flex:1;min-width:90px"><div class="t-stat-val" id="adminPendingRegs">-</div><div class="t-stat-lbl">Pending</div></div>
        <div class="t-stat" style="flex:1;min-width:90px"><div class="t-stat-val" id="adminSlotsLeft">-</div><div class="t-stat-lbl">Slots Left</div></div>
      </div>
      <div id="adminTourneyList"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>

    <div id="adminTab-moderators" style="display:none">
      <div class="section-title">Moderator Management</div>
      <div class="mod-info-box">
        <div class="mod-info-title">About Moderators</div>
        <p class="text-gray text-sm">Moderators can approve or dispute any pending match result. They cannot edit players or change admin settings.</p>
      </div>
      <div class="search-bar"><input class="search-input" placeholder="Search player..." id="modPlayerSearch" oninput="filterModPlayers()"></div>
      <div id="modPlayersList"></div>
    </div>
    <div id="adminTab-season" style="display:none">
      <div class="section-title">Season Management</div>
      <div class="card" style="max-width:480px;margin-bottom:20px">
        <div class="match-form">
          <div class="form-group"><label class="form-label">Season Duration (days)</label><input class="form-input" type="number" id="seasonDuration" value="30" min="7"></div>
          <div class="form-group"><label class="form-label">Season Start Date</label><input class="form-input" type="date" id="seasonStart"></div>
          <button class="btn-primary" onclick="saveSeasonSettings()">Save Settings</button>
        </div>
      </div>
      <div class="card" style="max-width:480px">
        <p class="text-sm mb-16" style="color:#FF5555">Full reset: clears all matches and resets all player stats.</p>
        <button class="btn-reject btn-sm" style="padding:10px 24px;font-size:13px" onclick="confirmSeasonReset()">Reset Season</button>
      </div>
    </div>
    <div id="adminTab-adminSettings" style="display:none">
      <div class="section-title">Settings</div>
      <div class="card" style="max-width:400px">
        <div class="match-form">
          <div class="form-group"><label class="form-label">New Admin Password</label><input class="form-input" type="password" id="newAdminPw"></div>
          <div class="form-group"><label class="form-label">Confirm Password</label><input class="form-input" type="password" id="confirmAdminPw"></div>
          <button class="btn-primary" onclick="changeAdminPassword()">Update Password</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- MOD PANEL -->
<div class="page" id="page-modpanel">
  <div class="section-title">Moderator Panel</div>
  <div class="mod-info-box">
    <div class="mod-info-title">Moderator Access</div>
    <p class="text-gray text-sm">Approve or dispute any pending match result below.</p>
  </div>
  <div id="modPendingMatches"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

</main>

<nav class="mobile-nav">
  <div class="mobile-nav-inner">
    <button class="mob-nav-btn active" onclick="navTo('home');setMobActive(this)"><span class="mob-nav-icon">&#127968;</span>Home</button>
    <button class="mob-nav-btn" onclick="navTo('leaderboard');setMobActive(this)"><span class="mob-nav-icon">&#127942;</span>Ranks</button>
    <button class="mob-nav-btn" onclick="navTo('matches');setMobActive(this)"><span class="mob-nav-icon">&#9917;</span>Matches</button>
    <button class="mob-nav-btn" onclick="navTo('submit');setMobActive(this)"><span class="mob-nav-icon">&#128203;</span>Submit</button>
    <button class="mob-nav-btn" onclick="navTo('myprofile');setMobActive(this)"><span class="mob-nav-icon">&#128100;</span>Me</button>
  </div>
</nav>

<!-- RANKING CARD PREVIEW -->
<div class="ranking-card-preview" id="rankingCardPreview">
  <button class="ranking-card-close" onclick="closeRankingPreview()">X</button>
  <div id="rcCardContainer" style="overflow:auto;max-width:100%"></div>
  <div style="display:flex;gap:10px;flex-wrap:wrap;justify-content:center">
    <button class="btn-primary" onclick="downloadRankingCard()">Download JPG</button>
    <button class="btn-secondary" onclick="closeRankingPreview()">Close</button>
  </div>
</div>

<!-- ============================================
     TOURNAMENT REGISTRATION MODAL
     ============================================ -->
<div class="modal-overlay" id="tourneyRegModal">
  <div class="modal tourney-modal">
    <button class="modal-close" onclick="closeModal('tourneyRegModal')" style="border-color:rgba(255,180,0,0.5);color:#FFD700;">X</button>
    <div class="tourney-modal-header">
      <div class="tourney-modal-title">&#9917; Tournament Registration</div>
      <div class="tourney-modal-sub">LLFC Paid Solo Tournament &bull; Season 1</div>
    </div>

    <!-- Fee notice -->
    <div class="tourney-fee-note" style="margin-bottom:16px">
      <div class="tourney-fee-amount">Entry Fee: ৳50 BDT</div>
      <div style="font-size:11px;margin-top:4px;color:rgba(255,180,100,0.7)">
        Send via <strong style="color:#FFD700">bKash</strong> &bull; Total Prize Pool: <strong style="color:#FFD700">৳800 BDT</strong> &bull; 16 Slots Only
      </div>
    </div>

    <div class="match-form" style="gap:13px">

      <!-- Player name — auto-filled if logged in, else manual -->
      <div class="form-group">
        <label class="t-form-label">Your Name</label>
        <input class="t-form-input" id="tRegName" placeholder="Your registered name">
        <div style="font-size:10px;color:rgba(255,180,0,0.4);margin-top:3px" id="tRegNameHint"></div>
      </div>

      <!-- Priority Time Slot -->
      <div class="form-group">
        <label class="t-form-label">Priority Time Slot</label>
        <select class="t-form-select" id="tRegTimeSlot">
          <option value="">-- Select Your Preferred Time --</option>
          <option value="11:30 PM">&#128337; 11:30 PM</option>
          <option value="12:00 AM">&#128337; 12:00 AM (Midnight)</option>
          <option value="1:00 AM">&#128337; 1:00 AM</option>
        </select>
      </div>

      <!-- bKash TRX ID -->
      <div class="form-group">
        <label class="t-form-label">bKash Transaction ID</label>
        <input class="t-form-input" id="tRegTrxId" placeholder="e.g. 8N7A6B3C2D" maxlength="40">
        <div class="trx-help">
          Send ৳50 to bKash &rarr; enter the 10-digit TRX ID you receive after payment.<br>
          Your registration is pending until admin verifies the transaction.
        </div>
      </div>

      <!-- Slots remaining -->
      <div style="text-align:center;font-size:12px;color:rgba(255,180,0,0.6);padding:6px 0">
        <span id="tRegSlotsLeft" style="font-family:'Bebas Neue',sans-serif;font-size:20px;color:#FFD700">?</span> slots remaining
      </div>

      <button class="btn-tourney-submit" onclick="submitTourneyReg()">
        Submit Registration &#9917;
      </button>
      <p style="text-align:center;font-size:11px;color:rgba(255,180,0,0.4);margin-top:4px">
        Pending admin approval after payment verification
      </p>
    </div>
  </div>
</div>

<!-- EXISTING MODALS -->
<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('loginModal')">X</button>
    <div class="modal-title">Player Login</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Name</label><input class="form-input" id="loginName" placeholder="Your registered name"></div>
      <div class="form-group"><label class="form-label">Password</label><input class="form-input" type="password" id="loginPw" onkeydown="if(event.key==='Enter')doLogin()"></div>
      <button class="btn-primary w-full" onclick="doLogin()">Login</button>
      <p class="text-gray text-sm" style="text-align:center;margin-top:8px">No account? <span style="color:var(--ucl-star);cursor:pointer" onclick="closeModal('loginModal');openModal('registerModal')">Register</span></p>
    </div>
  </div>
</div>

<div class="modal-overlay" id="registerModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('registerModal')">X</button>
    <div class="modal-title">Register</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Full Name</label><input class="form-input" id="regName" placeholder="Your name"></div>
      <div class="form-group"><label class="form-label">Category</label>
        <select class="form-select" id="regCategory">
          <option value="Main">Main Team</option>
          <option value="Youth">Youth</option>
          <option value="Academy">Academy</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Password</label><input class="form-input" type="password" id="regPw"></div>
      <div class="form-group"><label class="form-label">Confirm Password</label><input class="form-input" type="password" id="regPwConfirm"></div>
      <button class="btn-primary w-full" onclick="doRegister()">Register</button>
      <p class="text-gray text-sm" style="text-align:center;margin-top:8px">Requires admin approval before playing.</p>
    </div>
  </div>
</div>

<div class="modal-overlay" id="changePwModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('changePwModal')">X</button>
    <div class="modal-title">Change Password</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Current Password</label><input class="form-input" type="password" id="cpOld"></div>
      <div class="form-group"><label class="form-label">New Password</label><input class="form-input" type="password" id="cpNew"></div>
      <div class="form-group"><label class="form-label">Confirm New</label><input class="form-input" type="password" id="cpConfirm"></div>
      <button class="btn-primary w-full" onclick="changeMyPassword()">Update Password</button>
    </div>
  </div>
</div>

<div class="modal-overlay" id="editPlayerModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('editPlayerModal')">X</button>
    <div class="modal-title">Edit Player</div>
    <div class="match-form">
      <input type="hidden" id="editPlayerId">
      <div class="form-group"><label class="form-label">Division (1-9)</label><input class="form-input" type="number" min="1" max="9" id="editDivision"></div>
      <div class="form-group"><label class="form-label">Category</label>
        <select class="form-select" id="editCategory">
          <option value="Main">Main Team</option>
          <option value="Youth">Youth</option>
          <option value="Academy">Academy</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Wins</label><input class="form-input" type="number" id="editWins"></div>
      <div class="form-group"><label class="form-label">Draws</label><input class="form-input" type="number" id="editDraws"></div>
      <div class="form-group"><label class="form-label">Losses</label><input class="form-input" type="number" id="editLosses"></div>
      <div class="form-group"><label class="form-label">Goals For</label><input class="form-input" type="number" id="editGF"></div>
      <div class="form-group"><label class="form-label">Goals Against</label><input class="form-input" type="number" id="editGA"></div>
      <div class="form-group"><label class="form-label">Clean Sheets</label><input class="form-input" type="number" id="editCS"></div>
      <div class="form-group"><label class="form-label">Cycle MP</label><input class="form-input" type="number" id="editCycleMP"></div>
      <div class="form-group"><label class="form-label">Cycle Points</label><input class="form-input" type="number" id="editCyclePts"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editStatus">
          <option value="active">Active</option><option value="banned">Banned</option><option value="pending">Pending</option>
        </select>
      </div>
      <button class="btn-primary w-full" onclick="savePlayerEdit()">Save Changes</button>
    </div>
  </div>
</div>

<div class="modal-overlay" id="editMatchModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('editMatchModal')">X</button>
    <div class="modal-title">Edit Match</div>
    <div class="match-form">
      <input type="hidden" id="editMatchId">
      <div id="editMatchInfo" class="text-gray text-sm mb-8"></div>
      <div class="form-group"><label class="form-label">Score - Player A</label><input class="form-input" type="number" min="0" id="editScoreA"></div>
      <div class="form-group"><label class="form-label">Score - Player B</label><input class="form-input" type="number" min="0" id="editScoreB"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editMatchStatus">
          <option value="confirmed">Confirmed</option><option value="pending">Pending</option><option value="disputed">Disputed</option>
        </select>
      </div>
      <button class="btn-primary w-full" onclick="saveMatchEdit()">Save</button>
      <button class="btn-reject btn-sm w-full mt-8" onclick="adminDeleteMatch()">Delete Match</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import {
  getFirestore,collection,doc,getDoc,getDocs,addDoc,setDoc,
  updateDoc,deleteDoc,query,where,orderBy,limit,serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const app = initializeApp({
  apiKey:"AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLtDopPq4",
  authDomain:"llfc-4d2df.firebaseapp.com",projectId:"llfc-4d2df",
  storageBucket:"llfc-4d2df.firebasestorage.app",
  messagingSenderId:"697058785471",appId:"1:697058785471:web:7481cae8fe6b682d762e0a"
});
const db = getFirestore(app);

const DIV_RULES = {
  9:{cycle:10,promo:12,relo:0, next:8,name:'Rookie'},
  8:{cycle:10,promo:15,relo:3, next:7,name:'Amateur'},
  7:{cycle:10,promo:18,relo:4, next:6,name:'Regional'},
  6:{cycle:10,promo:21,relo:5, next:5,name:'National'},
  5:{cycle:10,promo:24,relo:6, next:4,name:'League Two'},
  4:{cycle:10,promo:27,relo:7, next:3,name:'League One'},
  3:{cycle:10,promo:30,relo:8, next:2,name:'Championship'},
  2:{cycle:10,promo:33,relo:9, next:1,name:'Premier'},
  1:{cycle:10,promo:999,relo:10,next:1,name:'Elite'},
};

let S={
  user:null,lbTab:'overall',players:[],matches:[],
  lbPlayers:[],allMatchesData:[],adminPlayers:[],
  pageHistory:['home'],adminPw:'fardous',
  tourneyRegs:[],
};

const $=id=>document.getElementById(id);
function T(msg,type='info'){
  const t=$('toast');t.textContent=msg;t.className=`toast show ${type}`;
  clearTimeout(window._tt);window._tt=setTimeout(()=>t.classList.remove('show'),3500);
}
function openModal(id){$(id).classList.add('open');}
function closeModal(id){$(id).classList.remove('open');}
function showPage(pg){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const el=$('page-'+pg);if(el)el.classList.add('active');
}
function navTo(pg){
  S.pageHistory.push(pg);showPage(pg);
  const m={home:'navHome',leaderboard:'navLeaderboard',matches:'navMatches',submit:'navSubmit'};
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  if(m[pg])$(m[pg])?.classList.add('active');
  if(pg==='home')loadHome();
  else if(pg==='leaderboard')loadLeaderboard(S.lbTab);
  else if(pg==='matches')loadMatches();
  else if(pg==='submit')loadSubmitPage();
  else if(pg==='myprofile')loadMyProfile();
  else if(pg==='modpanel')loadModPanel();
}
function navBack(){S.pageHistory.pop();const p=S.pageHistory[S.pageHistory.length-1]||'home';showPage(p);}
function setNavActive(b){document.querySelectorAll('.nav-btn').forEach(x=>x.classList.remove('active'));b.classList.add('active');}
function setMobActive(b){document.querySelectorAll('.mob-nav-btn').forEach(x=>x.classList.remove('active'));b.classList.add('active');}

function divBadge(d){return`<div class="div-badge div-${d||9}">${d||9}</div>`;}
function formBadge(r){const c=r==='W'?'form-w':r==='D'?'form-d':'form-l';return`<div class="form-dot ${c}"></div>`;}
function statusBadge(s){return`<span class="status-badge status-${s}">${s}</span>`;}
function fmtDate(ts){
  if(!ts)return'';
  try{const d=ts.toDate?ts.toDate():new Date(ts);return d.toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'});}catch{return'';}
}
function timeAgo(ts){
  if(!ts)return'';
  try{
    const d=ts.toDate?ts.toDate():new Date(ts),diff=Date.now()-d.getTime(),m=Math.floor(diff/60000);
    if(m<1)return'just now';if(m<60)return m+'m ago';
    const h=Math.floor(m/60);if(h<24)return h+'h ago';return Math.floor(h/24)+'d ago';
  }catch{return'';}
}
function getRC(sA,sB,side){const my=side==='A'?sA:sB,op=side==='A'?sB:sA;return my>op?'W':my<op?'L':'D';}
function isHigh(sA,sB){return(sA+sB)>7;}
function catClass(c){return c==='Main'?'cat-main':c==='Youth'?'cat-youth':'cat-academy';}
function getRatingMultiplier(myCategory,oppCategory,result){
  const imNonMain=myCategory==='Youth'||myCategory==='Academy';
  const oppIsMain=oppCategory==='Main';
  const imMain=myCategory==='Main';
  const oppIsNonMain=oppCategory==='Youth'||oppCategory==='Academy';
  if(imNonMain&&oppIsMain&&result==='W')return 2;
  if(imMain&&oppIsNonMain&&result==='L')return 2;
  return 1;
}
function calcRating(w,d,l,gf,ga,cs){return Math.max(0,w*10+d*5+l*(-5)+(gf-ga)+cs*2);}

// ===== NEWS =====
function buildNews(matches){
  const hi=matches.filter(m=>m.status==='confirmed'&&isHigh(m.scoreA,m.scoreB));
  if(!hi.length){$('newsTicker').style.display='none';return;}
  $('newsText').textContent=hi.slice(0,8).map(m=>`GOAL FEST: ${m.playerAName} ${m.scoreA}-${m.scoreB} ${m.playerBName} (${m.scoreA+m.scoreB} goals!)`).join('     |     ');
  $('newsTicker').style.display='flex';
}

// ===== TOURNAMENT SLOT COUNTER =====
async function loadTourneySlotCount(){
  try{
    const snap=await getDocs(query(collection(db,'tournamentRegs'),where('status','==','approved')));
    const filled=snap.size;
    const remaining=Math.max(0,16-filled);
    $('tStatFilled').textContent=filled;
    $('slotProgressText').textContent=filled+' / 16';
    $('slotFill').style.width=Math.min(100,Math.round(filled/16*100))+'%';
    $('tRegSlotsLeft').textContent=remaining;
  }catch(e){$('tStatFilled').textContent='?';}
}

// ===== TOURNAMENT REG MODAL =====
function openTourneyReg(){
  // Auto-fill name if logged in
  if(S.user){
    $('tRegName').value=S.user.name;
    $('tRegName').readOnly=true;
    $('tRegNameHint').textContent='Signed in as '+S.user.name;
  }else{
    $('tRegName').readOnly=false;
    $('tRegName').value='';
    $('tRegNameHint').textContent='Login for auto-fill, or enter your name manually';
  }
  loadTourneySlotCount();
  openModal('tourneyRegModal');
}

async function submitTourneyReg(){
  const name=$('tRegName').value.trim();
  const slot=$('tRegTimeSlot').value;
  const trxId=$('tRegTrxId').value.trim();
  if(!name)return T('Enter your name','error');
  if(!slot)return T('Select a time slot','error');
  if(!trxId||trxId.length<5)return T('Enter valid bKash TRX ID','error');

  // Check slot availability
  try{
    const approvedSnap=await getDocs(query(collection(db,'tournamentRegs'),where('status','==','approved')));
    if(approvedSnap.size>=16)return T('Sorry! All 16 slots are filled.','error');

    // Check duplicate by name
    const dupSnap=await getDocs(query(collection(db,'tournamentRegs'),where('playerName','==',name)));
    if(!dupSnap.empty)return T('You have already registered!','info');

    await addDoc(collection(db,'tournamentRegs'),{
      playerName:name,
      playerId:S.user?.id||null,
      timeSlot:slot,
      bkashTrxId:trxId,
      status:'pending',
      submittedAt:serverTimestamp(),
    });

    T('Registration submitted! Pending payment verification.','success');
    closeModal('tourneyRegModal');
    $('tRegTimeSlot').value='';
    $('tRegTrxId').value='';
    loadTourneySlotCount();
  }catch(e){T('Error: '+e.message,'error');}
}

// ===== ADMIN: TOURNAMENT =====
async function loadAdminTournament(){
  try{
    const snap=await getDocs(query(collection(db,'tournamentRegs'),orderBy('submittedAt','desc')));
    S.tourneyRegs=snap.docs.map(d=>({id:d.id,...d.data()}));
    const total=S.tourneyRegs.length;
    const approved=S.tourneyRegs.filter(r=>r.status==='approved').length;
    const pending=S.tourneyRegs.filter(r=>r.status==='pending').length;
    $('adminTotalRegs').textContent=total;
    $('adminApprovedRegs').textContent=approved;
    $('adminPendingRegs').textContent=pending;
    $('adminSlotsLeft').textContent=Math.max(0,16-approved);
    const el=$('adminTourneyList');
    if(!S.tourneyRegs.length){
      el.innerHTML='<div class="empty-state"><div class="empty-icon">&#9917;</div><div class="empty-text">No registrations yet</div></div>';return;
    }
    el.innerHTML=S.tourneyRegs.map((r,i)=>{
      const stCls=r.status==='approved'?'t-approved':r.status==='rejected'?'t-rejected':'';
      const stBadge=r.status==='approved'?'t-status-approved':r.status==='rejected'?'t-status-rejected':'t-status-pending';
      return `<div class="tourney-reg-item ${stCls}">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:22px;color:rgba(255,180,0,0.3);width:28px">${i+1}</div>
        <div class="tourney-reg-info">
          <div class="tourney-reg-name">${r.playerName}</div>
          <div class="tourney-reg-meta">
            &#128337; ${r.timeSlot} &nbsp;&bull;&nbsp;
            bKash TRX: <strong style="color:#FFD700;letter-spacing:1px">${r.bkashTrxId}</strong> &nbsp;&bull;&nbsp;
            ${fmtDate(r.submittedAt)} ${timeAgo(r.submittedAt)}
          </div>
        </div>
        <span class="t-status-badge ${stBadge}">${r.status}</span>
        <div style="display:flex;gap:5px;flex-wrap:wrap">
          ${r.status!=='approved'?`<button class="btn-sm btn-approve" onclick="adminTourneyApprove('${r.id}')">Approve</button>`:''}
          ${r.status!=='rejected'?`<button class="btn-sm btn-reject" onclick="adminTourneyReject('${r.id}')">Reject</button>`:''}
          <button class="btn-sm btn-ban" onclick="adminTourneyDelete('${r.id}')">Delete</button>
        </div>
      </div>`;
    }).join('');
  }catch(e){T('Error loading tournament data','error');console.error(e);}
}

async function adminTourneyApprove(id){
  const approvedSnap=await getDocs(query(collection(db,'tournamentRegs'),where('status','==','approved')));
  if(approvedSnap.size>=16)return T('Cannot approve — all 16 slots full!','error');
  await updateDoc(doc(db,'tournamentRegs',id),{status:'approved',approvedAt:serverTimestamp()});
  T('Registration approved! Slot confirmed.','success');
  loadAdminTournament();loadTourneySlotCount();
}
async function adminTourneyReject(id){
  await updateDoc(doc(db,'tournamentRegs',id),{status:'rejected'});
  T('Registration rejected.','info');loadAdminTournament();loadTourneySlotCount();
}
async function adminTourneyDelete(id){
  if(!confirm('Delete this registration permanently?'))return;
  await deleteDoc(doc(db,'tournamentRegs',id));
  T('Deleted.','info');loadAdminTournament();loadTourneySlotCount();
}

// ===== AUTH =====
async function doLogin(){
  const name=$('loginName').value.trim(),pw=$('loginPw').value;
  if(!name||!pw)return T('Fill in all fields','error');
  try{
    const snap=await getDocs(query(collection(db,'players'),where('name','==',name)));
    if(snap.empty)return T('Player not found','error');
    const d=snap.docs[0],p=d.data();
    if(p.password!==pw)return T('Wrong password','error');
    if(p.status==='pending')return T('Account pending admin approval','info');
    if(p.status==='banned')return T('Account banned. Contact admin.','error');
    S.user={id:d.id,...p};
    closeModal('loginModal');updateHeaderAuth();
    T('Welcome back, '+name+'!','success');
    loadSubmitPage();loadMatches();
  }catch(e){T('Login failed: '+e.message,'error');}
}

async function doRegister(){
  const name=$('regName').value.trim(),cat=$('regCategory').value;
  const pw=$('regPw').value,pw2=$('regPwConfirm').value;
  if(!name||!pw)return T('Fill in all fields','error');
  if(pw!==pw2)return T('Passwords do not match','error');
  if(pw.length<4)return T('Password too short','error');
  try{
    const ex=await getDocs(query(collection(db,'players'),where('name','==',name)));
    if(!ex.empty)return T('Name already taken','error');
    await addDoc(collection(db,'players'),{
      name,category:cat,password:pw,status:'pending',division:9,
      wins:0,draws:0,losses:0,goalsFor:0,goalsAgainst:0,cleanSheets:0,
      form:[],rivals:[],isModerator:false,highestDivision:9,
      cycleMP:0,cyclePts:0,
      isPOTD:false,isPOTW:false,isPOTM:false,isPOTS:false,
      createdAt:serverTimestamp()
    });
    closeModal('registerModal');
    T('Registration submitted! Awaiting admin approval','success');
    ['regName','regPw','regPwConfirm'].forEach(id=>$(id).value='');
  }catch(e){T('Registration failed: '+e.message,'error');}
}

function doLogout(){S.user=null;updateHeaderAuth();T('Logged out','info');navTo('home');}

function updateHeaderAuth(){
  const el=$('headerAuth');
  if(S.user){
    const isMod=S.user.isModerator;
    el.innerHTML=`
      <div class="user-pill" onclick="navTo('myprofile')">
        <div class="user-avatar">${S.user.name[0].toUpperCase()}</div>
        <span class="user-name">${S.user.name}</span>
        ${isMod?'<span class="mod-badge-hdr">MOD</span>':''}
      </div>
      ${isMod?`<button class="btn-login" style="border-color:#82B1FF;color:#82B1FF;font-size:11px" onclick="navTo('modpanel')">Mod Panel</button>`:''}
      <button class="btn-login" onclick="doLogout()">Logout</button>
      <button class="btn-login" style="border-color:var(--ucl-star);color:var(--ucl-star);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }else{
    el.innerHTML=`
      <button class="btn-login" onclick="openModal('loginModal')">Login</button>
      <button class="btn-register" onclick="openModal('registerModal')">Register</button>
      <button class="btn-login" style="border-color:var(--ucl-star);color:var(--ucl-star);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }
}

async function changeMyPassword(){
  if(!S.user)return;
  const oldPw=$('cpOld').value,newPw=$('cpNew').value,conf=$('cpConfirm').value;
  if(!oldPw||!newPw||!conf)return T('Fill in all fields','error');
  if(oldPw!==S.user.password)return T('Current password is wrong','error');
  if(newPw!==conf)return T('Passwords do not match','error');
  if(newPw.length<4)return T('Password too short','error');
  try{
    await updateDoc(doc(db,'players',S.user.id),{password:newPw});
    S.user.password=newPw;closeModal('changePwModal');
    T('Password updated successfully','success');
    ['cpOld','cpNew','cpConfirm'].forEach(id=>$(id).value='');
  }catch(e){T('Error: '+e.message,'error');}
}

// ===== HOME =====
async function loadHome(){
  try{
    const [pSnap,mSnap]=await Promise.all([
      getDocs(collection(db,'players')),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(100)))
    ]);
    S.players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    buildNews(S.matches);
    loadTourneySlotCount();
    const now=Date.now();
    $('statPlayers').textContent=S.players.length;
    $('statMatches').textContent=S.matches.filter(m=>m.status==='confirmed').length;
    $('statToday').textContent=S.matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<86400000).length;
    $('statPending').textContent=S.matches.filter(m=>m.status==='pending').length;

    const sorted=[...S.players].map(p=>({
      ...p,rating:calcRating(p.wins||0,p.draws||0,p.losses||0,p.goalsFor||0,p.goalsAgainst||0,p.cleanSheets||0)
    })).sort((a,b)=>b.rating-a.rating).slice(0,5);

    $('homeTopPlayers').innerHTML=sorted.length?sorted.map((p,i)=>`
      <div class="pending-item" style="cursor:pointer" onclick="viewProfile('${p.id}')">
        <span class="rank-num rank-${i+1}" style="font-size:22px;width:28px">${i+1}</span>
        ${divBadge(p.division)}
        <div class="pending-info">
          <div class="pending-name">${p.name} <span class="${catClass(p.category||'Main')}" style="font-size:11px">${p.category||'Main'}</span></div>
          <div class="pending-meta">${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
        </div>
        <span style="font-family:'Bebas Neue',sans-serif;font-size:22px;color:var(--ucl-star)">${p.rating}</span>
      </div>`).join(''):'<div class="empty-state"><div class="empty-text">No players yet</div></div>';

    const recent=S.matches.filter(m=>m.status==='confirmed').slice(0,6);
    $('homeRecentMatches').innerHTML=recent.length?recent.map(m=>{
      const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
      return `<div class="match-card${hi?' high-score':''}">
        <div class="match-info">
          <div class="match-vs">
            <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
            <span class="text-gray"> vs </span>
            <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
            ${hi?' <span class="high-score-badge">GOAL FEST</span>':''}
            ${x2?' <span class="x2-badge">2X RATING</span>':''}
          </div>
          <div class="match-meta">${fmtDate(m.createdAt)}</div>
        </div>
        <div class="match-score">${m.scoreA}-${m.scoreB}</div>
      </div>`;
    }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>';

    const divInfo=[
      {d:1,name:'Elite',promo:'Top Division - Defend your title',relo:'Relegate if <=10 pts'},
      {d:2,name:'Premier',promo:'33 pts in 10 matches to promote',relo:'Relo if <=9 pts'},
      {d:3,name:'Championship',promo:'30 pts in 10 matches',relo:'Relo if <=8 pts'},
      {d:4,name:'League One',promo:'27 pts in 10 matches',relo:'Relo if <=7 pts'},
      {d:5,name:'League Two',promo:'24 pts in 10 matches',relo:'Relo if <=6 pts'},
      {d:6,name:'National',promo:'21 pts in 10 matches',relo:'Relo if <=5 pts'},
      {d:7,name:'Regional',promo:'18 pts in 10 matches',relo:'Relo if <=4 pts'},
      {d:8,name:'Amateur',promo:'15 pts in 10 matches',relo:'Relo if <=3 pts'},
      {d:9,name:'Rookie',promo:'12 pts in 10 matches',relo:'Entry level - no relegation'},
    ];
    $('divisionGuide').innerHTML=divInfo.map(di=>`
      <div class="div-guide-card">
        <div style="display:flex;align-items:center;gap:10px">
          ${divBadge(di.d)}
          <div class="div-guide-name">${di.name}</div>
        </div>
        <div class="div-guide-pts">Promotion: ${di.promo}</div>
        <div class="div-guide-desc">${di.relo}</div>
        ${di.d<=3?'<div class="div-guide-badge">TOP TIER DIVISION</div>':''}
      </div>`).join('');
  }catch(e){console.error(e);T('Error loading home','error');}
}

// ===== LEADERBOARD =====
async function loadLeaderboard(tab='overall'){
  S.lbTab=tab;
  $('lbTableBody').innerHTML='<tr><td colspan="11" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>';
  try{
    const [pSnap,mSnap]=await Promise.all([
      getDocs(collection(db,'players')),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(1000)))
    ]);
    S.players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const now=Date.now();
    const timeFilter={daily:86400000,weekly:604800000,monthly:2592000000,overall:Infinity}[tab];
    const playerCatMap={};S.players.forEach(p=>playerCatMap[p.id]=p.category||'Main');
    let players=S.players.map(p=>{
      let pm=S.matches.filter(m=>(m.playerAId===p.id||m.playerBId===p.id)&&m.status==='confirmed');
      if(tab!=='overall')pm=pm.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<timeFilter);
      let w=0,d=0,l=0,gf=0,ga=0,cs=0;
      pm.forEach(m=>{
        const side=m.playerAId===p.id?'A':'B';
        const result=getRC(m.scoreA,m.scoreB,side);
        const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
        const oppCat=playerCatMap[side==='A'?m.playerBId:m.playerAId]||'Main';
        const mult=getRatingMultiplier(p.category||'Main',oppCat,result);
        if(result==='W')w+=mult;else if(result==='D')d+=1;else l+=mult;
        gf+=myG;ga+=opG;if(opG===0)cs++;
      });
      const total=pm.length,wr=total>0?Math.round((w/(w+d+l||1))*100):0,gd=gf-ga;
      const rating=Math.max(0,w*10+d*5+l*(-5)+gd+cs*2);
      const cyclePts=p.cyclePts||0,cycleMP=p.cycleMP||0;
      return{...p,tw:Math.round(w),td:d,tl:Math.round(l),tgf:gf,tga:ga,tcs:cs,tgd:gd,twr:wr,total,rating,cyclePts,cycleMP};
    });
    if(tab!=='overall')players=players.filter(p=>p.total>0);
    players.sort((a,b)=>b.rating-a.rating||b.tgd-a.tgd||b.twr-a.twr);
    S.lbPlayers=players;renderLbTable(players);
  }catch(e){
    $('lbTableBody').innerHTML='<tr><td colspan="11" style="text-align:center;color:#FF5555">Error loading</td></tr>';console.error(e);
  }
}

function renderLbTable(players){
  const search=($('lbSearch')?.value||'').toLowerCase();
  const divF=$('lbDivFilter')?.value||'';
  const filtered=players.filter(p=>p.name.toLowerCase().includes(search)&&(!divF||String(p.division||9)===divF));
  const tbody=$('lbTableBody');
  if(!filtered.length){tbody.innerHTML='<tr><td colspan="11"><div class="empty-state"><div class="empty-text">No players found</div></div></td></tr>';return;}
  tbody.innerHTML=filtered.map((p,i)=>{
    const r=i+1,rc=r===1?'top-1':r===2?'top-2':r===3?'top-3':'';
    const form=(p.form||[]).slice(-5);
    const rules=DIV_RULES[p.division||9]||DIV_RULES[9];
    const pct=Math.min(100,Math.round((p.cyclePts||0)/(rules.promo||1)*100));
    return`<tr class="${rc}">
      <td><span class="rank-num rank-${r}">${r}</span></td>
      <td>
        <span class="player-link" onclick="viewProfile('${p.id}')">
          <div class="user-avatar" style="width:28px;height:28px;font-size:11px">${p.name[0].toUpperCase()}</div>
          ${p.name}&nbsp;<span class="${catClass(p.category||'Main')}" style="font-size:10px;font-weight:700">${p.category||'Main'}</span>
          ${p.isModerator?'&nbsp;<span class="mod-badge-hdr">MOD</span>':''}
        </span>
      </td>
      <td>${divBadge(p.division)}</td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:20px;color:var(--ucl-star)">${p.rating}</span></td>
      <td>
        <div class="wdl-row">
          <span class="wdl-pill wdl-w"><span class="wdl-num">${p.tw}</span>&nbsp;W</span>
          <span class="wdl-pill wdl-d"><span class="wdl-num">${p.td}</span>&nbsp;D</span>
          <span class="wdl-pill wdl-l"><span class="wdl-num">${p.tl}</span>&nbsp;L</span>
        </div>
      </td>
      <td style="color:#82B1FF">${p.total}</td>
      <td>
        <div class="winrate-wrap">
          <div class="winrate-bar"><div class="winrate-fill" style="width:${p.twr}%"></div></div>
          <span class="winrate-pct">${p.twr}%</span>
        </div>
      </td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:16px;color:${p.tgd>=0?'#00E676':'#FF5555'}">${p.tgd>=0?'+':''}${p.tgd}</span></td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:16px;color:#82B1FF">${p.tcs}</span></td>
      <td><div class="form-dots">${form.map(r=>formBadge(r)).join('')}</div></td>
      <td>
        <div style="font-size:10px;color:#4472C4">${p.cycleMP||0}/10</div>
        <div style="background:rgba(255,255,255,.06);border-radius:3px;height:4px;width:48px;margin-top:3px;overflow:hidden">
          <div style="height:100%;width:${pct}%;background:linear-gradient(90deg,#00A550,#00E676);border-radius:3px"></div>
        </div>
      </td>
    </tr>`;
  }).join('');
}

function filterLeaderboard(){if(S.lbPlayers.length)renderLbTable(S.lbPlayers);}
function switchLbTab(tab,btn){
  document.querySelectorAll('.lb-tab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');loadLeaderboard(tab);
}

// ===== RANKING CARD =====
function openRankingCardPreview(){buildRankingCard();$('rankingCardPreview').classList.add('open');}
function closeRankingPreview(){$('rankingCardPreview').classList.remove('open');}
function buildRankingCard(){
  const top10=S.lbPlayers.slice(0,10);
  const labels={overall:'Overall Season',daily:'Daily',weekly:'Weekly',monthly:'Monthly'};
  const now=new Date().toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'});
  if(!top10.length){$('rcCardContainer').innerHTML='<div style="color:#666;padding:20px">Load leaderboard first</div>';return;}
  const divNames=['','Elite','Premier','Championship','League One','League Two','National','Regional','Amateur','Rookie'];
  const rows=top10.map((p,i)=>{
    const r=i+1,rc=r===1?'rank-1-row':r===2?'rank-2-row':r===3?'rank-3-row':'';
    const rankCls=r===1?'r1':r===2?'r2':r===3?'r3':'';
    return`<div class="rc-row ${rc}">
      <div class="rc-rank ${rankCls}">${r}</div>
      <div class="rc-player-info">
        <div class="rc-avatar">${p.name[0].toUpperCase()}</div>
        <div>
          <div class="rc-name">${p.name}</div>
          <div class="rc-div-small">DIV ${p.division||9} - ${divNames[p.division||9]||''} | ${p.category||'Main'}</div>
        </div>
      </div>
      <div class="rc-rating">${p.rating}</div>
      <div class="rc-wdl-nums"><span class="rc-w">${p.tw}W</span><span class="rc-d">&nbsp;${p.td}D</span><span class="rc-l">&nbsp;${p.tl}L</span></div>
      <div style="display:flex;gap:5px;align-items:center">
        <div style="background:rgba(255,255,255,.06);border-radius:4px;height:5px;width:58px;overflow:hidden">
          <div style="height:100%;width:${p.twr}%;background:linear-gradient(90deg,#1B3A6B,#4472C4);border-radius:4px"></div>
        </div>
        <span style="font-family:'Bebas Neue',sans-serif;font-size:13px;color:#4472C4">${p.twr}%</span>
      </div>
      <div class="rc-winpct" style="color:${p.tgd>=0?'#00E676':'#FF5555'}">${p.tgd>=0?'+':''}${p.tgd}</div>
    </div>`;
  }).join('');
  $('rcCardContainer').innerHTML=`
    <div class="rc-card" id="theRankingCard">
      <div class="rc-header">
        <div class="rc-header-top">
          <div><div class="rc-title">LLFC EFOOTBALL DIVISION</div><div class="rc-subtitle">PLAYER RANKING - TOP 10</div></div>
          <div class="rc-period">${labels[S.lbTab]||'Overall'}</div>
        </div>
      </div>
      <div class="rc-body">
        <div class="rc-row rc-header-row">
          <span>Rank</span><span>Player</span><span>Rating</span><span>W/D/L</span><span>Win%</span><span>GD</span>
        </div>
        ${rows}
      </div>
      <div class="rc-footer">
        <div class="rc-footer-brand">LLFC EFOOTBALL DIVISION SYSTEM</div>
        <div class="rc-footer-date">GENERATED: ${now}</div>
      </div>
    </div>`;
}
async function downloadRankingCard(){
  const card=$('theRankingCard');if(!card)return T('No card to download','error');
  try{
    T('Generating...','info');
    const canvas=await html2canvas(card,{backgroundColor:'#060E1C',scale:2,useCORS:true,logging:false});
    const link=document.createElement('a');
    link.download=`LLFC-Ranking-${S.lbTab}-${new Date().toISOString().split('T')[0]}.jpg`;
    link.href=canvas.toDataURL('image/jpeg',0.95);link.click();T('Downloaded!','success');
  }catch(e){T('Download failed: '+e.message,'error');}
}

// ===== MATCHES =====
async function loadMatches(){
  try{
    const mSnap=await getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(200)));
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    S.allMatchesData=S.matches;renderMatchesList(S.matches);renderPendingConfirms();
  }catch(e){$('matchesList').innerHTML='<div class="empty-state"><div class="empty-text">Error loading</div></div>';console.error(e);}
}
function renderMatchesList(matches){
  const search=($('matchSearch')?.value||'').toLowerCase();
  const sf=$('matchStatusFilter')?.value||'';
  let f=matches;
  if(search)f=f.filter(m=>m.playerAName?.toLowerCase().includes(search)||m.playerBName?.toLowerCase().includes(search));
  if(sf)f=f.filter(m=>m.status===sf);
  const el=$('matchesList');
  if(!f.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#9917;</div><div class="empty-text">No matches found</div></div>';return;}
  el.innerHTML=f.map(m=>{
    const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
    return`<div class="match-card${hi?' high-score':''}">
      <div class="match-info">
        <div class="match-vs">
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
          <span class="text-gray"> vs </span>
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
          ${hi?' <span class="high-score-badge">GOAL FEST</span>':''}
          ${x2?' <span class="x2-badge">2X RATING</span>':''}
        </div>
        <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} - ${statusBadge(m.status)}</div>
      </div>
      <div class="match-score">${m.scoreA}-${m.scoreB}</div>
    </div>`;
  }).join('');
}
function renderPendingConfirms(){
  const section=$('pendingConfirmSection'),list=$('pendingConfirmList');
  if(!S.user){section.style.display='none';return;}
  const isMod=S.user.isModerator;
  const pending=S.allMatchesData.filter(m=>m.status==='pending'&&(isMod||m.playerBId===S.user.id));
  if(!pending.length){section.style.display='none';return;}
  section.style.display='block';
  list.innerHTML=pending.map(m=>`
    <div class="confirm-card">
      ${isMod&&m.playerBId!==S.user.id?'<div style="font-size:11px;color:#CE93D8;font-weight:700;margin-bottom:8px;letter-spacing:1px">MODERATOR REVIEW</div>':''}
      <div class="confirm-vs">
        <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">${m.playerACat||''}</div></div>
        <div class="confirm-score-display">${m.scoreA}-${m.scoreB}</div>
        <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">${m.playerBCat||''}</div></div>
      </div>
      <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} - ${timeAgo(m.createdAt)}</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">Confirm</button>
        <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">Dispute</button>
      </div>
    </div>`).join('');
}
function filterMatches(){if(S.allMatchesData.length)renderMatchesList(S.allMatchesData);}

async function confirmMatch(matchId,confirmed){
  try{
    const mRef=doc(db,'matches',matchId),mSnap=await getDoc(mRef);
    if(!mSnap.exists())return T('Match not found','error');
    const m=mSnap.data();
    if(confirmed){
      await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
      await applyMatchStats(m);T('Match confirmed! Stats updated','success');
    }else{await updateDoc(mRef,{status:'disputed'});T('Match disputed.','info');}
    S.matches=[];S.allMatchesData=[];loadMatches();
  }catch(e){T('Error: '+e.message,'error');}
}

async function applyMatchStats(m){
  const [aSnap,bSnap]=await Promise.all([getDoc(doc(db,'players',m.playerAId)),getDoc(doc(db,'players',m.playerBId))]);
  if(!aSnap.exists()||!bSnap.exists())return;
  const aData=aSnap.data(),bData=bSnap.data();
  const aCat=aData.category||'Main',bCat=bData.category||'Main';
  async function upd(pid,pData,side,oppCat){
    const ref=doc(db,'players',pid);
    const result=getRC(m.scoreA,m.scoreB,side);
    const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
    const isCS=opG===0;
    const form=[...(pData.form||[]).slice(-19),result];
    const cyclePtsGain=result==='W'?3:result==='D'?1:0;
    const newCycleMP=(pData.cycleMP||0)+1,newCyclePts=(pData.cyclePts||0)+cyclePtsGain;
    const mult=getRatingMultiplier(pData.category||'Main',oppCat,result);
    const wInc=result==='W'?mult:0,lInc=result==='L'?mult:0,dInc=result==='D'?1:0;
    const updates={
      wins:(pData.wins||0)+wInc,draws:(pData.draws||0)+dInc,losses:(pData.losses||0)+lInc,
      goalsFor:(pData.goalsFor||0)+myG,goalsAgainst:(pData.goalsAgainst||0)+opG,
      cleanSheets:(pData.cleanSheets||0)+(isCS?1:0),form,cycleMP:newCycleMP,cyclePts:newCyclePts,
    };
    await updateDoc(ref,updates);
    await checkAndApplyDivision(pid,{...pData,...updates});
  }
  await updateDoc(doc(db,'matches',m.id||'x'),{playerACat:aCat,playerBCat:bCat,is2x:
    getRatingMultiplier(aCat,bCat,getRC(m.scoreA,m.scoreB,'A'))>1||
    getRatingMultiplier(bCat,aCat,getRC(m.scoreA,m.scoreB,'B'))>1
  }).catch(()=>{});
  await Promise.all([upd(m.playerAId,aData,'A',bCat),upd(m.playerBId,bData,'B',aCat)]);
}

async function checkAndApplyDivision(pid,p){
  const div=p.division||9,rules=DIV_RULES[div]||DIV_RULES[9];
  const cmp=p.cycleMP||0,cpts=p.cyclePts||0;
  let newDiv=div,action=null;
  if(cpts>=rules.promo&&div>1){newDiv=Math.max(1,div-1);action='promote';}
  else if(cmp>=rules.cycle){
    if(cpts<=rules.relo&&div<9){newDiv=Math.min(9,div+1);action='relegate';}
    else if(cmp>=rules.cycle)action='stay';
  }
  if(action){
    await updateDoc(doc(db,'players',pid),{division:newDiv,cycleMP:0,cyclePts:0,highestDivision:Math.min(newDiv,p.highestDivision||9)});
    if(action==='promote')T(p.name+' promoted to Division '+newDiv+'!','success');
    else if(action==='relegate')T(p.name+' relegated to Division '+newDiv+'.','info');
  }
}

// ===== SUBMIT =====
async function loadSubmitPage(){
  if(!S.user){$('submitRequireLogin').style.display='block';$('submitForm').style.display='none';return;}
  $('submitRequireLogin').style.display='none';$('submitForm').style.display='block';
  $('submitMyName').value=S.user.name;
  $('matchDate').value=new Date().toISOString().split('T')[0];
  const snap=await getDocs(collection(db,'players'));
  S.players=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
  const sel=$('submitOpponent');
  sel.innerHTML='<option value="">-- Select Opponent --</option>'+
    S.players.filter(p=>p.id!==S.user.id).map(p=>`<option value="${p.id}">${p.name} (Div ${p.division||9} - ${p.category||'Main'})</option>`).join('');
}

async function submitMatchResult(){
  if(!S.user)return T('Login required','error');
  const oppId=$('submitOpponent').value;
  const sA=parseInt($('scoreA').value)||0,sB=parseInt($('scoreB').value)||0;
  const matchDate=$('matchDate').value;
  if(!oppId)return T('Select an opponent','error');
  const opp=S.players.find(p=>p.id===oppId);if(!opp)return T('Opponent not found','error');
  try{
    await addDoc(collection(db,'matches'),{
      playerAId:S.user.id,playerAName:S.user.name,playerACat:S.user.category||'Main',
      playerBId:oppId,playerBName:opp.name,playerBCat:opp.category||'Main',
      scoreA:sA,scoreB:sB,status:'pending',matchDate,
      createdAt:serverTimestamp(),submittedBy:S.user.id
    });
    const msg=isHigh(sA,sB)?`GOAL FEST! ${sA+sB} goals submitted. Waiting for ${opp.name}.`:`Result submitted. Waiting for ${opp.name} to confirm.`;
    T(msg,'success');$('scoreA').value='';$('scoreB').value='';S.matches=[];
  }catch(e){T('Submit failed: '+e.message,'error');}
}

// ===== MOD PANEL =====
async function loadModPanel(){
  if(!S.user||!S.user.isModerator){
    $('modPendingMatches').innerHTML='<div class="empty-state"><div class="empty-text">Moderator access required</div></div>';return;
  }
  try{
    const mSnap=await getDocs(query(collection(db,'matches'),where('status','==','pending'),orderBy('createdAt','desc'),limit(100)));
    const pending=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('modPendingMatches');
    if(!pending.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#10003;</div><div class="empty-text">No pending matches</div></div>';return;}
    el.innerHTML=pending.map(m=>`
      <div class="confirm-card">
        <div class="confirm-vs">
          <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">${m.playerACat||''}</div></div>
          <div class="confirm-score-display">${m.scoreA}-${m.scoreB}</div>
          <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">${m.playerBCat||''}</div></div>
        </div>
        <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} - ${timeAgo(m.createdAt)}</div>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">Approve</button>
          <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">Dispute</button>
        </div>
      </div>`).join('');
  }catch(e){T('Error loading mod panel: '+e.message,'error');console.error(e);}
}

// ===== PROFILE =====
async function viewProfile(playerId){
  S.pageHistory.push('profile');showPage('profile');
  $('profileContent').innerHTML='<div class="loading-spinner"><div class="spinner"></div></div>';
  try{
    const [snap,mSnap]=await Promise.all([
      getDoc(doc(db,'players',playerId)),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(500)))
    ]);
    if(!snap.exists()){$('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Player not found</div></div>';return;}
    const p={id:snap.id,...snap.data()};
    const allM=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const myConfirmed=allM.filter(m=>(m.playerAId===playerId||m.playerBId===playerId)&&m.status==='confirmed');
    const recent=myConfirmed.slice(0,10);
    const playerCatMap={};S.players.forEach(pp=>playerCatMap[pp.id]=pp.category||'Main');
    let w=0,d=0,l=0,gf=0,ga=0,cs=0,x2Count=0;
    myConfirmed.forEach(m=>{
      const side=m.playerAId===playerId?'A':'B';
      const result=getRC(m.scoreA,m.scoreB,side);
      const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
      const oppId=side==='A'?m.playerBId:m.playerAId;
      const oppCat=playerCatMap[oppId]||(side==='A'?m.playerBCat:m.playerACat)||'Main';
      const mult=getRatingMultiplier(p.category||'Main',oppCat,result);
      if(mult>1)x2Count++;
      if(result==='W')w+=mult;else if(result==='D')d+=1;else l+=mult;
      gf+=myG;ga+=opG;if(opG===0)cs++;
    });
    const total=myConfirmed.length,wr=total>0?Math.round((w/(w+d+l||1))*100):0;
    const gd=gf-ga,rating=Math.max(0,Math.round(w*10+d*5+l*(-5)+gd+cs*2));
    const div=p.division||9,rules=DIV_RULES[div]||DIV_RULES[9];
    const cmp=p.cycleMP||0,cpts=p.cyclePts||0;
    const pct=Math.min(100,Math.round(cpts/(rules.promo||1)*100));
    const form=(p.form||[]).slice(-5);
    const isMe=S.user&&S.user.id===playerId,isRival=S.user&&(S.user.rivals||[]).includes(playerId);
    const badges=[];
    if(div===1)badges.push({t:'Elite Division',c:'badge-star'});
    else if(div===2)badges.push({t:'Premier Division',c:'badge-silver'});
    else if(div===3)badges.push({t:'Championship',c:'badge-gold'});
    const highest=p.highestDivision||div;
    if(highest<div)badges.push({t:'Peak: Div '+highest,c:'badge-blue'});
    if(wr>=80&&total>=5)badges.push({t:'Win Machine 80%+',c:'badge-gold'});
    else if(wr>=70&&total>=5)badges.push({t:'Sharp 70%+',c:'badge-green'});
    let streak=0;const fm=p.form||[];for(let i=fm.length-1;i>=0;i--){if(fm[i]==='W')streak++;else break;}
    if(streak>=5)badges.push({t:'On Fire '+streak+' Streak',c:'badge-red'});
    else if(streak>=3)badges.push({t:streak+' Win Streak',c:'badge-green'});
    if(x2Count>0)badges.push({t:'2x Upsets: '+x2Count,c:'badge-purple'});
    if(p.isPOTD)badges.push({t:'Player of the Day',c:'badge-star'});
    if(p.isPOTW)badges.push({t:'Player of the Week',c:'badge-gold'});
    if(p.isPOTM)badges.push({t:'Player of the Month',c:'badge-purple'});
    if(p.isPOTS)badges.push({t:'Player of the Season',c:'badge-star'});
    if(p.isModerator)badges.push({t:'Moderator',c:'badge-blue'});
    $('profileContent').innerHTML=`
      <div class="profile-header">
        <div class="profile-avatar">${p.name[0].toUpperCase()}</div>
        <div class="profile-info">
          <div class="profile-name">${p.name}</div>
          <span class="profile-cat ${catClass(p.category||'Main')}">${p.category||'Main'}</span>
          <div style="display:flex;align-items:center;gap:10px;margin-top:8px;flex-wrap:wrap">
            ${divBadge(div)} <span class="text-gray text-sm">Division ${div} - ${rules.name}</span>
            ${highest<div?`<span class="text-blue text-sm">Best Div: ${highest}</span>`:''}
          </div>
          <div class="form-dots mt-8">${form.map(r=>formBadge(r)).join('')}</div>
          <div class="badges-row">${badges.map(b=>`<span class="player-badge ${b.c}">${b.t}</span>`).join('')}</div>
          <div style="display:flex;gap:8px;margin-top:10px;flex-wrap:wrap">
            ${!isMe&&S.user?`<button class="btn-sm ${isRival?'btn-reject':'btn-edit'}" onclick="toggleRival('${playerId}','${p.name}')">${isRival?'Remove Rival':'Add Rival'}</button>`:''}
            ${isMe?`<button class="btn-sm btn-edit" onclick="openModal('changePwModal')">Change Password</button>`:''}
          </div>
        </div>
      </div>
      <div class="profile-stats">
        <div class="p-stat"><div class="p-stat-val" style="color:var(--ucl-star)">${rating}</div><div class="p-stat-lbl">Rating</div></div>
        <div class="p-stat"><div class="p-stat-val text-green">${Math.round(w)}</div><div class="p-stat-lbl">Wins</div></div>
        <div class="p-stat"><div class="p-stat-val text-yellow">${d}</div><div class="p-stat-lbl">Draws</div></div>
        <div class="p-stat"><div class="p-stat-val text-red">${Math.round(l)}</div><div class="p-stat-lbl">Losses</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:#82B1FF">${total}</div><div class="p-stat-lbl">Matches</div></div>
        <div class="p-stat"><div class="p-stat-val">${wr}%</div><div class="p-stat-lbl">Win Rate</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:${gd>=0?'#00E676':'#FF5555'}">${gd>=0?'+':''}${gd}</div><div class="p-stat-lbl">Goal Diff</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:#82B1FF">${cs}</div><div class="p-stat-lbl">Clean Sheets</div></div>
      </div>
      <div class="promo-tracker">
        <div class="promo-title">Division ${div} Cycle - Promotion Progress</div>
        <div class="promo-bar-wrap"><div class="promo-bar-fill" style="width:${pct}%"></div></div>
        <div class="promo-label"><span>${cpts} pts / ${rules.promo} needed</span><span>${cmp}/10 matches</span></div>
        ${cmp>=rules.cycle?'<div class="promo-cycle-info" style="color:#00E676">Cycle complete!</div>':`<div class="promo-cycle-info">${Math.max(0,rules.cycle-cmp)} matches remaining in this cycle</div>`}
      </div>
      <div class="section-title mt-16">Recent Matches</div>
      ${recent.length?recent.map(m=>{
        const side=m.playerAId===playerId?'A':'B';
        const res=getRC(m.scoreA,m.scoreB,side);
        const oppName=side==='A'?m.playerBName:m.playerAName;
        const oppId2=side==='A'?m.playerBId:m.playerAId;
        const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
        const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
        return`<div class="match-card${hi?' high-score':''}">
          <div class="match-result-badge result-${res}">${res}</div>
          <div class="match-info">
            <div class="match-vs">vs <span class="player-link" style="display:inline" onclick="viewProfile('${oppId2}')">${oppName}</span>
              ${hi?' <span class="high-score-badge">GOAL FEST</span>':''}
              ${x2?' <span class="x2-badge">2X</span>':''}
            </div>
            <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} - ${statusBadge(m.status)}</div>
          </div>
          <div class="match-score">${myG}-${opG}</div>
        </div>`;
      }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>'}
    `;
  }catch(e){$('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Error loading profile</div></div>';console.error(e);}
}

async function loadMyProfile(){
  if(!S.user){
    $('myProfileContent').innerHTML='<div class="empty-state"><div class="empty-icon">&#128274;</div><div class="empty-text">Not logged in</div><button class="btn-primary mt-12" onclick="openModal(\'loginModal\')">Login</button></div>';return;
  }
  try{const snap=await getDoc(doc(db,'players',S.user.id));if(snap.exists())S.user={...S.user,...snap.data()};}catch{}
  await viewProfile(S.user.id);
  $('myProfileContent').innerHTML=$('profileContent').innerHTML;
}

async function toggleRival(playerId,playerName){
  if(!S.user)return;
  const rivals=S.user.rivals||[];
  const nr=rivals.includes(playerId)?rivals.filter(r=>r!==playerId):[...rivals,playerId];
  await updateDoc(doc(db,'players',S.user.id),{rivals:nr});
  S.user.rivals=nr;T(rivals.includes(playerId)?playerName+' removed from rivals':playerName+' added as rival','success');
  viewProfile(playerId);
}

// ===== ADMIN =====
async function adminLogin(){
  const pw=$('adminPwInput').value;
  let stored=S.adminPw;
  try{const s=await getDoc(doc(db,'settings','admin'));if(s.exists()&&s.data().password)stored=s.data().password;}catch{}
  if(pw===stored){
    $('adminLoginWrap').style.display='none';$('adminPanelWrap').style.display='block';
    loadAdminPanel('pending');T('Admin access granted','success');
  }else T('Wrong password','error');
}

async function loadAdminPanel(tab){
  if(tab==='pending'){
    const snap=await getDocs(query(collection(db,'players'),where('status','==','pending')));
    const pending=snap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('adminPendingList');
    if(!pending.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#10003;</div><div class="empty-text">No pending</div></div>';return;}
    el.innerHTML=pending.map(p=>`
      <div class="pending-item">
        <div class="pending-info"><div class="pending-name">${p.name}</div><div class="pending-meta">${p.category} - ${fmtDate(p.createdAt)}</div></div>
        <div style="display:flex;gap:6px;flex-wrap:wrap">
          <button class="btn-sm btn-approve" onclick="adminApprove('${p.id}')">Approve</button>
          <button class="btn-sm btn-reject" onclick="adminReject('${p.id}')">Reject</button>
        </div>
      </div>`).join('');
  }
  if(tab==='players'){
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()}));renderAdminPlayers(S.adminPlayers);
  }
  if(tab==='adminMatches'){
    const snap=await getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(100)));
    const matches=snap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('adminMatchesList');
    if(!matches.length){el.innerHTML='<div class="empty-state"><div class="empty-text">No matches</div></div>';return;}
    el.innerHTML=matches.map(m=>`
      <div class="pending-item">
        <div class="pending-info">
          <div class="pending-name">${m.playerAName} ${m.scoreA}-${m.scoreB} ${m.playerBName}${isHigh(m.scoreA,m.scoreB)?' [GOAL FEST]':''}${m.is2x?' [2X]':''}</div>
          <div class="pending-meta">${fmtDate(m.createdAt)} - ${statusBadge(m.status)}</div>
        </div>
        <div style="display:flex;gap:5px;flex-wrap:wrap">
          ${m.status==='pending'?`<button class="btn-sm btn-approve" onclick="adminConfirmMatch('${m.id}')">Confirm</button>`:''}
          <button class="btn-sm btn-edit" onclick="adminEditMatch('${m.id}','${m.playerAName}','${m.playerBName}',${m.scoreA},${m.scoreB},'${m.status}')">Edit</button>
          <button class="btn-sm btn-reject" onclick="adminDeleteMatchDirect('${m.id}')">Delete</button>
        </div>
      </div>`).join('');
  }
  if(tab==='tournament')loadAdminTournament();
  if(tab==='moderators'){
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    renderModPlayers(S.adminPlayers);
  }
  if(tab==='season'){
    try{const s=await getDoc(doc(db,'settings','season'));if(s.exists()){if(s.data().duration)$('seasonDuration').value=s.data().duration;if(s.data().startDate)$('seasonStart').value=s.data().startDate;}}catch{}
  }
}

function renderAdminPlayers(players){
  const search=($('adminPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  const rating=p=>calcRating(p.wins||0,p.draws||0,p.losses||0,p.goalsFor||0,p.goalsAgainst||0,p.cleanSheets||0);
  $('adminPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name} <span class="${catClass(p.category||'Main')}" style="font-size:11px">${p.category||'Main'}</span>${p.status==='banned'?' [BANNED]':''}${p.isModerator?' [MOD]':''}</div>
        <div class="pending-meta">Div${p.division||9} - Rating:${rating(p)} - ${p.wins||0}W ${p.draws||0}D ${p.losses||0}L - Cycle:${p.cycleMP||0}/10 (${p.cyclePts||0}pts) - ${statusBadge(p.status||'active')}</div>
      </div>
      <div style="display:flex;gap:4px;flex-wrap:wrap">
        <button class="btn-sm btn-edit" onclick="adminEditPlayer('${p.id}',${p.division||9},'${p.category||'Main'}',${p.wins||0},${p.draws||0},${p.losses||0},${p.goalsFor||0},${p.goalsAgainst||0},${p.cleanSheets||0},${p.cycleMP||0},${p.cyclePts||0},'${p.status||'active'}')">Edit</button>
        <button class="btn-sm btn-ban" onclick="adminToggleBan('${p.id}','${p.name}','${p.status||'active'}')">
          ${p.status==='banned'?'Unban':'Ban'}</button>
        <button class="btn-sm ${p.isPOTD?'btn-reject':'btn-approve'}" onclick="adminTogglePOTD('${p.id}','${p.name}',${!!p.isPOTD})">${p.isPOTD?'Rem POTD':'POTD'}</button>
        <button class="btn-sm ${p.isPOTW?'btn-reject':'btn-edit'}" onclick="adminTogglePOTW('${p.id}','${p.name}',${!!p.isPOTW})">${p.isPOTW?'Rem POTW':'POTW'}</button>
        <button class="btn-sm ${p.isPOTM?'btn-reject':'btn-mod'}" onclick="adminTogglePOTM('${p.id}','${p.name}',${!!p.isPOTM})">${p.isPOTM?'Rem POTM':'POTM'}</button>
        <button class="btn-sm ${p.isPOTS?'btn-reject':'btn-ban'}" onclick="adminTogglePOTS('${p.id}','${p.name}',${!!p.isPOTS})">${p.isPOTS?'Rem POTS':'POTS'}</button>
      </div>
    </div>`).join(''):'<div class="empty-state"><div class="empty-text">No players</div></div>';
}
function filterAdminPlayers(){if(S.adminPlayers.length)renderAdminPlayers(S.adminPlayers);}

function renderModPlayers(players){
  const search=($('modPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  $('modPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name} <span class="${catClass(p.category||'Main')}" style="font-size:11px">${p.category||'Main'}</span>${p.isModerator?' [MODERATOR]':''}</div>
        <div class="pending-meta">${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
      </div>
      <button class="btn-sm ${p.isModerator?'btn-reject':'btn-mod'}" onclick="adminToggleMod('${p.id}','${p.name}',${!!p.isModerator})">
        ${p.isModerator?'Remove Mod':'Give Mod'}</button>
    </div>`).join(''):'<div class="empty-state"><div class="empty-text">No active players</div></div>';
}
function filterModPlayers(){if(S.adminPlayers.length)renderModPlayers(S.adminPlayers);}

async function adminToggleMod(id,name,isMod){
  const nv=!isMod;
  await updateDoc(doc(db,'players',id),{isModerator:nv});
  T(name+(nv?' is now a Moderator':' mod removed'),nv?'success':'info');
  if(S.user&&S.user.id===id){S.user.isModerator=nv;updateHeaderAuth();}
  loadAdminPanel('moderators');
}

async function adminApprove(id){await updateDoc(doc(db,'players',id),{status:'active'});T('Player approved','success');loadAdminPanel('pending');}
async function adminReject(id){if(!confirm('Reject and delete this registration?'))return;await deleteDoc(doc(db,'players',id));T('Rejected','info');loadAdminPanel('pending');}

function adminEditPlayer(id,div,cat,wins,draws,losses,gf,ga,cs,cmp,cpts,status){
  $('editPlayerId').value=id;$('editDivision').value=div;$('editCategory').value=cat;
  $('editWins').value=wins;$('editDraws').value=draws;$('editLosses').value=losses;
  $('editGF').value=gf;$('editGA').value=ga;$('editCS').value=cs;
  $('editCycleMP').value=cmp;$('editCyclePts').value=cpts;$('editStatus').value=status;
  openModal('editPlayerModal');
}

async function savePlayerEdit(){
  const id=$('editPlayerId').value,div=parseInt($('editDivision').value);
  const cat=$('editCategory').value;
  const wins=parseInt($('editWins').value),draws=parseInt($('editDraws').value),losses=parseInt($('editLosses').value);
  const gf=parseInt($('editGF').value),ga=parseInt($('editGA').value),cs=parseInt($('editCS').value);
  const cmp=parseInt($('editCycleMP').value),cpts=parseInt($('editCyclePts').value);
  const status=$('editStatus').value;
  if(div<1||div>9)return T('Division 1-9 only','error');
  try{
    await updateDoc(doc(db,'players',id),{division:div,category:cat,wins,draws,losses,goalsFor:gf,goalsAgainst:ga,cleanSheets:cs,cycleMP:cmp,cyclePts:cpts,status});
    T('Player updated','success');closeModal('editPlayerModal');loadAdminPanel('players');
  }catch(e){T('Error: '+e.message,'error');}
}

async function adminToggleBan(id,name,cs){const ns=cs==='banned'?'active':'banned';await updateDoc(doc(db,'players',id),{status:ns});T(name+' '+ns,'info');loadAdminPanel('players');}
async function adminTogglePOTD(id,n,c){await updateDoc(doc(db,'players',id),{isPOTD:!c});T(n+(!c?' POTD set':'POTD removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTW(id,n,c){await updateDoc(doc(db,'players',id),{isPOTW:!c});T(n+(!c?' POTW set':'POTW removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTM(id,n,c){await updateDoc(doc(db,'players',id),{isPOTM:!c});T(n+(!c?' POTM set':'POTM removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTS(id,n,c){await updateDoc(doc(db,'players',id),{isPOTS:!c});T(n+(!c?' POTS set':'POTS removed'),'success');loadAdminPanel('players');}

function adminEditMatch(id,nA,nB,sA,sB,status){
  $('editMatchId').value=id;$('editMatchInfo').textContent=`${nA} vs ${nB}`;
  $('editScoreA').value=sA;$('editScoreB').value=sB;$('editMatchStatus').value=status;
  openModal('editMatchModal');
}

async function adminConfirmMatch(matchId){
  const mRef=doc(db,'matches',matchId),mSnap=await getDoc(mRef);
  if(!mSnap.exists())return;
  await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
  await applyMatchStats(mSnap.data());
  T('Match confirmed by admin','success');S.matches=[];loadAdminPanel('adminMatches');
}

async function saveMatchEdit(){
  const id=$('editMatchId').value,sA=parseInt($('editScoreA').value),sB=parseInt($('editScoreB').value);
  const status=$('editMatchStatus').value;
  try{
    const mRef=doc(db,'matches',id);const old=await getDoc(mRef);
    await updateDoc(mRef,{scoreA:sA,scoreB:sB,status});
    if(status==='confirmed'&&old.data().status!=='confirmed'){
      await applyMatchStats({...old.data(),scoreA:sA,scoreB:sB});
    }
    T('Match updated','success');closeModal('editMatchModal');S.matches=[];loadAdminPanel('adminMatches');
  }catch(e){T('Error: '+e.message,'error');}
}

async function adminDeleteMatch(){
  const id=$('editMatchId').value;
  if(!confirm('Delete this match permanently?'))return;
  await deleteDoc(doc(db,'matches',id));
  T('Match deleted','info');closeModal('editMatchModal');S.matches=[];loadAdminPanel('adminMatches');
}

async function adminDeleteMatchDirect(id){
  if(!confirm('Delete this match?'))return;
  await deleteDoc(doc(db,'matches',id));
  T('Match deleted. Ranking will update automatically.','info');S.matches=[];loadAdminPanel('adminMatches');
}

async function saveSeasonSettings(){
  const dur=parseInt($('seasonDuration').value)||30,sd=$('seasonStart').value;
  try{await setDoc(doc(db,'settings','season'),{duration:dur,startDate:sd},{merge:true});T('Season settings saved','success');}catch(e){T('Error','error');}
}

async function confirmSeasonReset(){
  if(!confirm('RESET ENTIRE SEASON?\n\nAll matches deleted, all stats reset.\n\nOK to confirm.'))return;
  try{
    const [pSnap,mSnap]=await Promise.all([getDocs(collection(db,'players')),getDocs(collection(db,'matches'))]);
    await Promise.all([
      ...pSnap.docs.map(d=>updateDoc(doc(db,'players',d.id),{wins:0,draws:0,losses:0,goalsFor:0,goalsAgainst:0,cleanSheets:0,form:[],division:9,cycleMP:0,cyclePts:0,highestDivision:9})),
      ...mSnap.docs.map(d=>deleteDoc(doc(db,'matches',d.id)))
    ]);
    S.players=[];S.matches=[];T('Season reset complete!','success');
  }catch(e){T('Error: '+e.message,'error');}
}

async function changeAdminPassword(){
  const pw=$('newAdminPw').value,pw2=$('confirmAdminPw').value;
  if(!pw||pw.length<4)return T('Password too short','error');
  if(pw!==pw2)return T('Passwords do not match','error');
  try{await setDoc(doc(db,'settings','admin'),{password:pw},{merge:true});S.adminPw=pw;T('Admin password updated','success');$('newAdminPw').value='';$('confirmAdminPw').value='';}catch(e){T('Error','error');}
}

function switchAdminTab(tab,btn){
  document.querySelectorAll('.admin-tab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('[id^="adminTab-"]').forEach(el=>el.style.display='none');
  $('adminTab-'+tab).style.display='block';
  loadAdminPanel(tab);
}

// ===== EXPOSE =====
Object.assign(window,{
  navTo,navBack,setNavActive,setMobActive,openModal,closeModal,
  doLogin,doRegister,doLogout,changeMyPassword,
  switchLbTab,filterLeaderboard,filterMatches,confirmMatch,
  submitMatchResult,loadSubmitPage,viewProfile,toggleRival,loadMyProfile,
  openRankingCardPreview,closeRankingPreview,downloadRankingCard,
  openTourneyReg,submitTourneyReg,
  adminTourneyApprove,adminTourneyReject,adminTourneyDelete,
  adminLogin,loadAdminPanel,switchAdminTab,adminApprove,adminReject,
  adminEditPlayer,savePlayerEdit,adminToggleBan,adminToggleMod,
  adminTogglePOTD,adminTogglePOTW,adminTogglePOTM,adminTogglePOTS,
  adminEditMatch,saveMatchEdit,adminDeleteMatch,adminDeleteMatchDirect,
  adminConfirmMatch,filterAdminPlayers,filterModPlayers,
  confirmSeasonReset,changeAdminPassword,loadModPanel,saveSeasonSettings
});

// INIT
updateHeaderAuth();loadHome();
document.querySelectorAll('.modal-overlay').forEach(m=>{
  m.addEventListener('click',e=>{if(e.target===m)m.classList.remove('open');});
});
</script>
</body>
</html>
