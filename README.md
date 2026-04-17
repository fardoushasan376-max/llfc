<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LLFC Juvenile Division System</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
:root{
  --red:#CC0000;--red-bright:#FF1A1A;--red-dark:#8B0000;
  --white:#FFFFFF;--gray-mid:#B0A0A0;--black:#080000;
  --card-bg:#160808;--card-border:rgba(204,0,0,0.28);
  --gold:#FFD700;--silver:#C0C0C0;--bronze:#CD7F32;
  --green:#00CC44;--yellow:#FFAA00;--blue:#4499FF;--purple:#AA44FF;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{font-family:'Rajdhani',sans-serif;background:var(--black);color:var(--white);min-height:100vh;overflow-x:hidden;}
body::before{content:'';position:fixed;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 80px,rgba(204,0,0,0.02) 80px,rgba(204,0,0,0.02) 81px),repeating-linear-gradient(90deg,transparent,transparent 80px,rgba(204,0,0,0.02) 80px,rgba(204,0,0,0.02) 81px);pointer-events:none;z-index:0;}

/* HEADER */
header{position:sticky;top:0;z-index:1000;background:rgba(8,0,0,0.97);backdrop-filter:blur(12px);border-bottom:2px solid var(--red);box-shadow:0 4px 30px rgba(204,0,0,0.25);}
.header-inner{max-width:1400px;margin:0 auto;padding:0 16px;display:flex;align-items:center;justify-content:space-between;height:60px;gap:8px;}
.logo-area{display:flex;align-items:center;gap:10px;cursor:pointer;flex-shrink:0;}
.logo-badge{width:42px;height:42px;background:var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:14px;color:white;box-shadow:0 0 15px rgba(204,0,0,0.5);flex-shrink:0;letter-spacing:1px;}
.logo-text{display:flex;flex-direction:column;line-height:1;}
.logo-main{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:2px;}
.logo-sub{font-size:10px;color:var(--red-bright);letter-spacing:3px;text-transform:uppercase;font-weight:600;}
.header-nav{display:flex;gap:4px;align-items:center;}
.nav-btn{background:none;border:1px solid transparent;color:var(--gray-mid);padding:6px 12px;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:13px;letter-spacing:1px;cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;}
.nav-btn:hover,.nav-btn.active{color:var(--white);border-color:var(--red);background:rgba(204,0,0,0.14);}
.header-auth{display:flex;gap:6px;align-items:center;flex-shrink:0;}
.btn-login{background:transparent;border:1px solid var(--red);color:var(--red-bright);padding:6px 14px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:13px;letter-spacing:1px;cursor:pointer;border-radius:3px;transition:all .2s;text-transform:uppercase;}
.btn-login:hover{background:var(--red);color:white;}
.btn-register{background:var(--red);border:1px solid var(--red);color:white;padding:6px 14px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:13px;cursor:pointer;border-radius:3px;transition:all .2s;text-transform:uppercase;}
.btn-register:hover{background:var(--red-bright);}
.user-pill{display:flex;align-items:center;gap:8px;background:rgba(204,0,0,0.14);border:1px solid var(--red);border-radius:20px;padding:4px 12px 4px 4px;cursor:pointer;}
.user-avatar{width:28px;height:28px;background:var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;flex-shrink:0;}
.user-name{font-size:13px;font-weight:600;}
.mod-badge-hdr{font-size:9px;background:rgba(170,68,255,0.3);border:1px solid var(--purple);color:var(--purple);padding:1px 5px;border-radius:3px;}

/* MAIN */
main{position:relative;z-index:1;max-width:1400px;margin:0 auto;padding:20px 16px;min-height:calc(100vh - 60px);}
.page{display:none;}.page.active{display:block;}

/* BUTTONS */
.btn-primary{background:var(--red);color:white;border:none;padding:10px 24px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:14px;letter-spacing:2px;cursor:pointer;border-radius:4px;text-transform:uppercase;transition:all .2s;box-shadow:0 4px 12px rgba(204,0,0,0.3);}
.btn-primary:hover{background:var(--red-bright);transform:translateY(-1px);}
.btn-secondary{background:transparent;color:var(--white);border:1px solid rgba(255,255,255,0.22);padding:10px 24px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:14px;cursor:pointer;border-radius:4px;text-transform:uppercase;transition:all .2s;}
.btn-secondary:hover{border-color:var(--red);background:rgba(204,0,0,0.1);}
.btn-sm{padding:5px 11px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:11px;letter-spacing:1px;cursor:pointer;border-radius:3px;transition:all .2s;text-transform:uppercase;}
.btn-approve{background:rgba(0,204,68,.2);color:var(--green);border:1px solid rgba(0,204,68,.4);}
.btn-approve:hover{background:var(--green);color:#000;}
.btn-reject{background:rgba(204,0,0,.2);color:var(--red-bright);border:1px solid var(--red);}
.btn-reject:hover{background:var(--red);color:white;}
.btn-edit{background:rgba(255,170,0,.15);color:var(--yellow);border:1px solid rgba(255,170,0,.4);}
.btn-edit:hover{background:rgba(255,170,0,.3);}
.btn-ban{background:rgba(80,0,80,.3);color:#cc88ff;border:1px solid rgba(150,0,150,.4);}
.btn-ban:hover{background:rgba(150,0,150,.4);}
.btn-mod{background:rgba(68,153,255,.15);color:var(--blue);border:1px solid rgba(68,153,255,.4);}
.btn-mod:hover{background:rgba(68,153,255,.3);}
.w-full{width:100%;}

/* SECTION TITLE */
.section-title{font-family:'Bebas Neue',sans-serif;font-size:24px;letter-spacing:3px;color:var(--white);display:flex;align-items:center;gap:12px;margin-bottom:16px;}
.section-title::after{content:'';flex:1;height:2px;background:linear-gradient(90deg,var(--red),transparent);}

/* HERO */
.hero{background:linear-gradient(135deg,rgba(139,0,0,.35) 0%,rgba(8,0,0,.9) 60%);border:1px solid var(--red);border-radius:12px;padding:34px 26px;margin-bottom:20px;position:relative;overflow:hidden;}
.hero::before{content:'LLFC';position:absolute;right:-10px;top:-10px;font-family:'Bebas Neue',sans-serif;font-size:160px;color:rgba(204,0,0,.04);pointer-events:none;}
.hero-tag{display:inline-block;background:var(--red);color:white;font-size:11px;font-weight:700;letter-spacing:3px;padding:3px 10px;border-radius:2px;margin-bottom:10px;text-transform:uppercase;}
.hero h1{font-family:'Bebas Neue',sans-serif;font-size:clamp(30px,5vw,60px);letter-spacing:4px;line-height:1;margin-bottom:10px;}
.hero h1 span{color:var(--red-bright);}
.hero p{color:var(--gray-mid);font-size:15px;max-width:500px;margin-bottom:20px;line-height:1.5;}
.hero-actions{display:flex;gap:10px;flex-wrap:wrap;}

/* STATS */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:10px;margin-bottom:20px;}
.stat-card{background:var(--card-bg);border:1px solid var(--card-border);border-radius:8px;padding:14px;text-align:center;}
.stat-num{font-family:'Bebas Neue',sans-serif;font-size:32px;color:var(--red-bright);line-height:1;}
.stat-label{font-size:10px;color:var(--gray-mid);letter-spacing:2px;text-transform:uppercase;margin-top:4px;}

/* GRIDS */
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:20px;}
.three-col{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;}
@media(max-width:900px){.two-col{grid-template-columns:1fr;}.three-col{grid-template-columns:1fr 1fr;}.header-nav{display:none;}}
@media(max-width:500px){.three-col{grid-template-columns:1fr;}}

/* DIVISION BADGES - visual */
.div-badge{display:inline-flex;align-items:center;justify-content:center;width:32px;height:32px;border-radius:50%;font-weight:700;font-size:13px;flex-shrink:0;position:relative;}
.div-1{background:linear-gradient(135deg,#FFD700,#FF8C00);color:#000;box-shadow:0 0 8px rgba(255,215,0,.5);}
.div-2{background:linear-gradient(135deg,#E8E8E8,#909090);color:#000;box-shadow:0 0 6px rgba(192,192,192,.4);}
.div-3{background:linear-gradient(135deg,#E8A060,#8B4513);color:#fff;box-shadow:0 0 6px rgba(205,127,50,.4);}
.div-4{background:linear-gradient(135deg,#CC0000,#800000);color:#fff;box-shadow:0 0 6px rgba(204,0,0,.4);}
.div-5{background:linear-gradient(135deg,#990000,#500000);color:#eee;}
.div-6{background:linear-gradient(135deg,#660000,#300000);color:#ccc;}
.div-7{background:linear-gradient(135deg,#440000,#200000);color:#aaa;}
.div-8{background:linear-gradient(135deg,#2a0000,#180000);color:#888;border:1px solid #440000;}
.div-9{background:linear-gradient(135deg,#1a1010,#0a0808);color:#666;border:1px solid #333;}

/* LARGE DIV BADGE for profile */
.div-badge-lg{width:70px;height:70px;border-radius:50%;display:flex;flex-direction:column;align-items:center;justify-content:center;font-weight:700;font-size:22px;flex-shrink:0;position:relative;}
.div-badge-lg .div-label{font-family:'Bebas Neue',sans-serif;font-size:9px;letter-spacing:2px;margin-top:1px;}

/* NEWS TICKER */
.news-ticker{background:rgba(204,0,0,.1);border:1px solid rgba(204,0,0,.3);border-radius:6px;margin-bottom:16px;overflow:hidden;display:flex;align-items:center;}
.news-label{background:var(--red);color:white;padding:8px 14px;font-family:'Bebas Neue',sans-serif;font-size:13px;letter-spacing:2px;flex-shrink:0;white-space:nowrap;}
.news-scroll-wrap{overflow:hidden;flex:1;padding:8px 12px;}
.news-scroll-text{font-size:13px;font-weight:600;color:var(--gold);white-space:nowrap;display:inline-block;animation:scrollNews 22s linear infinite;}
@keyframes scrollNews{0%{transform:translateX(100vw);}100%{transform:translateX(-100%);}}

/* TABLE - FIXED for readability */
.lb-table-wrap{overflow-x:auto;border-radius:8px;border:1px solid var(--card-border);}
table{width:100%;border-collapse:collapse;}
thead tr{background:#2a0808;border-bottom:2px solid var(--red);}
thead th{padding:11px 12px;text-align:left;font-size:11px;letter-spacing:2px;text-transform:uppercase;color:#D0B0B0;font-weight:700;white-space:nowrap;background:#2a0808;}
tbody tr{border-bottom:1px solid rgba(204,0,0,.1);transition:background .15s;}
tbody tr:hover{background:rgba(204,0,0,.08);}
tbody tr:last-child{border-bottom:none;}
tbody td{padding:10px 12px;font-size:14px;font-weight:500;vertical-align:middle;color:#F0E0E0;background:transparent;}
tbody tr.top-1{background:linear-gradient(90deg,rgba(255,215,0,.09),transparent) !important;}
tbody tr.top-2{background:linear-gradient(90deg,rgba(192,192,192,.07),transparent) !important;}
tbody tr.top-3{background:linear-gradient(90deg,rgba(205,127,50,.07),transparent) !important;}
.rank-num{font-family:'Bebas Neue',sans-serif;font-size:22px;color:var(--gray-mid);}
.rank-1{color:var(--gold);}.rank-2{color:var(--silver);}.rank-3{color:var(--bronze);}

/* WDL PILLS */
.wdl-row{display:flex;align-items:center;gap:5px;}
.wdl-pill{display:inline-flex;align-items:center;gap:2px;padding:3px 8px;border-radius:4px;font-size:11px;font-weight:700;white-space:nowrap;}
.wdl-w{background:rgba(0,204,68,.2);color:#44FF88;border:1px solid rgba(0,204,68,.35);}
.wdl-d{background:rgba(255,170,0,.2);color:#FFCC44;border:1px solid rgba(255,170,0,.35);}
.wdl-l{background:rgba(204,0,0,.2);color:#FF6666;border:1px solid rgba(204,0,0,.35);}
.wdl-num{font-family:'Bebas Neue',sans-serif;font-size:16px;line-height:1;}

/* WINRATE */
.winrate-wrap{display:flex;align-items:center;gap:5px;}
.winrate-bar{position:relative;background:rgba(255,255,255,.08);border-radius:10px;height:5px;width:50px;overflow:hidden;flex-shrink:0;}
.winrate-fill{position:absolute;left:0;top:0;bottom:0;background:linear-gradient(90deg,var(--red),var(--red-bright));border-radius:10px;}
.winrate-pct{font-size:12px;font-weight:700;color:#C0A0A0;white-space:nowrap;}

/* FORM DOTS */
.form-dots{display:flex;gap:3px;align-items:center;}
.form-dot{width:8px;height:8px;border-radius:50%;}
.form-w{background:var(--green);}.form-d{background:var(--yellow);}.form-l{background:var(--red);}

/* PLAYER LINK */
.player-link{cursor:pointer;color:#F0E0E0;font-weight:600;transition:color .2s;display:inline-flex;align-items:center;gap:6px;}
.player-link:hover{color:var(--red-bright);}

/* STATUS */
.status-badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;}
.status-confirmed{background:rgba(0,204,68,.2);color:#44FF88;border:1px solid rgba(0,204,68,.3);}
.status-pending{background:rgba(255,170,0,.2);color:#FFCC44;border:1px solid rgba(255,170,0,.3);}
.status-disputed{background:rgba(204,0,0,.2);color:#FF6666;border:1px solid rgba(204,0,0,.3);}

/* LB TABS */
.lb-tabs{display:flex;gap:4px;margin-bottom:16px;background:rgba(204,0,0,.05);border:1px solid var(--card-border);border-radius:8px;padding:4px;flex-wrap:wrap;}
.lb-tab{flex:1;min-width:70px;background:none;border:none;color:var(--gray-mid);padding:8px 10px;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:13px;cursor:pointer;border-radius:5px;transition:all .2s;text-transform:uppercase;}
.lb-tab.active{background:var(--red);color:white;}

/* SEARCH */
.search-bar{display:flex;gap:8px;margin-bottom:14px;}
.search-input{flex:1;background:rgba(255,255,255,.05);border:1px solid rgba(204,0,0,.3);border-radius:5px;color:#F0E0E0;padding:9px 13px;font-family:'Rajdhani',sans-serif;font-size:14px;}
.search-input:focus{outline:none;border-color:var(--red);}
.search-input::placeholder{color:#806060;}
.form-select-sm{background:rgba(255,255,255,.05);border:1px solid rgba(204,0,0,.3);border-radius:5px;color:#F0E0E0;padding:9px 10px;font-family:'Rajdhani',sans-serif;font-size:13px;cursor:pointer;}
.form-select-sm:focus{outline:none;border-color:var(--red);}
.form-select-sm option{background:#1a0808;color:#F0E0E0;}

/* CARD */
.card{background:var(--card-bg);border:1px solid var(--card-border);border-radius:8px;padding:18px;}
.card-red{background:linear-gradient(135deg,rgba(204,0,0,.18),rgba(8,0,0,.95));border:1px solid var(--red);}

/* FORM INPUTS */
.match-form{display:grid;gap:14px;}
.form-group{display:flex;flex-direction:column;gap:5px;}
.form-label{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--gray-mid);}
.form-input,.form-select{background:rgba(255,255,255,.05);border:1px solid rgba(204,0,0,.3);border-radius:5px;color:#F0E0E0;padding:9px 13px;font-family:'Rajdhani',sans-serif;font-size:15px;font-weight:500;transition:border-color .2s;width:100%;}
.form-input:focus,.form-select:focus{outline:none;border-color:var(--red);background:rgba(204,0,0,.07);}
.form-select option{background:#160808;color:#F0E0E0;}
.score-row{display:grid;grid-template-columns:1fr auto 1fr;gap:10px;align-items:center;}
.score-vs{font-family:'Bebas Neue',sans-serif;font-size:22px;color:var(--red);text-align:center;}
.score-input{text-align:center;font-size:26px;font-family:'Bebas Neue',sans-serif;padding:10px;}

/* MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.87);z-index:2000;display:none;align-items:center;justify-content:center;padding:16px;backdrop-filter:blur(4px);}
.modal-overlay.open{display:flex;}
.modal{background:#120000;border:1px solid var(--red);border-radius:10px;padding:24px;width:100%;max-width:480px;max-height:90vh;overflow-y:auto;position:relative;}
.modal-title{font-family:'Bebas Neue',sans-serif;font-size:24px;letter-spacing:3px;color:var(--white);margin-bottom:16px;}
.modal-close{position:absolute;top:12px;right:12px;background:rgba(204,0,0,.2);border:1px solid var(--red);color:var(--red-bright);width:26px;height:26px;border-radius:50%;font-size:13px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .2s;}
.modal-close:hover{background:var(--red);color:white;}

/* TOAST */
.toast{position:fixed;bottom:80px;right:16px;z-index:9999;background:#160808;border-left:4px solid var(--red);border-radius:6px;padding:12px 16px;min-width:220px;max-width:340px;box-shadow:0 8px 24px rgba(0,0,0,.5);transform:translateX(120%);transition:transform .3s;font-weight:600;font-size:14px;color:#F0E0E0;}
.toast.show{transform:translateX(0);}
.toast.success{border-color:var(--green);}
.toast.error{border-color:var(--red-bright);}
.toast.info{border-color:var(--yellow);}

/* MATCH CARD */
.match-card{background:var(--card-bg);border:1px solid var(--card-border);border-radius:6px;padding:12px 14px;margin-bottom:8px;display:flex;align-items:center;gap:10px;transition:border-color .2s;}
.match-card:hover{border-color:var(--red);}
.match-card.high-score{border-color:rgba(255,215,0,.45);background:linear-gradient(135deg,rgba(255,215,0,.04),var(--card-bg));}
.match-result-badge{width:34px;height:34px;border-radius:4px;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:16px;font-weight:700;flex-shrink:0;}
.result-W{background:rgba(0,204,68,.2);color:#44FF88;border:1px solid rgba(0,204,68,.4);}
.result-D{background:rgba(255,170,0,.2);color:#FFCC44;border:1px solid rgba(255,170,0,.4);}
.result-L{background:rgba(204,0,0,.2);color:#FF6666;border:1px solid rgba(204,0,0,.4);}
.match-info{flex:1;min-width:0;}
.match-vs{font-size:14px;font-weight:600;color:#F0E0E0;}
.match-meta{font-size:11px;color:var(--gray-mid);margin-top:2px;}
.match-score{font-family:'Bebas Neue',sans-serif;font-size:24px;color:var(--white);text-align:right;flex-shrink:0;}
.high-score-badge{background:rgba(255,215,0,.2);color:var(--gold);border:1px solid rgba(255,215,0,.4);border-radius:3px;font-size:10px;font-weight:700;padding:1px 6px;}

/* PENDING */
.pending-item{background:var(--card-bg);border:1px solid var(--card-border);border-radius:6px;padding:12px 14px;margin-bottom:8px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
.pending-info{flex:1;min-width:120px;}
.pending-name{font-size:15px;font-weight:700;color:#F0E0E0;}
.pending-meta{font-size:11px;color:var(--gray-mid);}
.confirm-card{background:linear-gradient(135deg,rgba(204,0,0,.1),var(--card-bg));border:1px solid var(--red);border-radius:8px;padding:14px;margin-bottom:10px;}
.confirm-vs{display:flex;align-items:center;justify-content:space-between;gap:8px;margin-bottom:10px;flex-wrap:wrap;}
.confirm-player{text-align:center;flex:1;}
.confirm-player-name{font-size:15px;font-weight:700;color:#F0E0E0;}
.confirm-score-display{font-family:'Bebas Neue',sans-serif;font-size:32px;color:var(--red-bright);padding:0 12px;flex-shrink:0;}

/* PROFILE */
.profile-header{display:flex;gap:20px;align-items:flex-start;flex-wrap:wrap;margin-bottom:20px;}
.profile-avatar{width:76px;height:76px;background:var(--red-dark);border:3px solid var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:30px;color:white;flex-shrink:0;box-shadow:0 0 20px rgba(204,0,0,.4);}
.profile-info{flex:1;}
.profile-name{font-family:'Bebas Neue',sans-serif;font-size:32px;letter-spacing:3px;line-height:1;color:#F0E0E0;}
.profile-cat{display:inline-block;background:rgba(204,0,0,.2);border:1px solid var(--red);color:var(--red-bright);font-size:11px;font-weight:700;letter-spacing:2px;padding:2px 8px;border-radius:2px;margin-top:4px;text-transform:uppercase;}
.profile-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(90px,1fr));gap:9px;margin-bottom:18px;}
.p-stat{background:var(--card-bg);border:1px solid var(--card-border);border-radius:6px;padding:11px;text-align:center;}
.p-stat-val{font-family:'Bebas Neue',sans-serif;font-size:26px;line-height:1;}
.p-stat-lbl{font-size:10px;color:var(--gray-mid);letter-spacing:1.5px;text-transform:uppercase;}

/* PROMO TRACKER */
.promo-tracker{background:var(--card-bg);border:1px solid var(--card-border);border-radius:8px;padding:14px;margin-top:14px;}
.promo-title{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--gray-mid);margin-bottom:8px;}
.promo-bar-wrap{background:rgba(255,255,255,.07);border-radius:6px;height:9px;margin-bottom:5px;overflow:hidden;}
.promo-bar-fill{height:100%;background:linear-gradient(90deg,var(--red),var(--red-bright));border-radius:6px;transition:width .5s;}
.promo-label{font-size:12px;color:var(--gray-mid);display:flex;justify-content:space-between;}
.promo-cycle-info{font-size:11px;color:#FFAA00;margin-top:6px;font-weight:600;}

/* BADGES - player profile */
.badges-row{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px;}
.player-badge{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;border-radius:4px;font-size:11px;font-weight:700;letter-spacing:1px;text-transform:uppercase;border:1px solid;}
.badge-gold{background:rgba(255,215,0,.15);color:var(--gold);border-color:rgba(255,215,0,.4);}
.badge-silver{background:rgba(192,192,192,.15);color:var(--silver);border-color:rgba(192,192,192,.4);}
.badge-red{background:rgba(204,0,0,.2);color:#FF6666;border-color:rgba(204,0,0,.4);}
.badge-green{background:rgba(0,204,68,.15);color:#44FF88;border-color:rgba(0,204,68,.4);}
.badge-blue{background:rgba(68,153,255,.15);color:#88CCFF;border-color:rgba(68,153,255,.4);}
.badge-purple{background:rgba(170,68,255,.15);color:#CC88FF;border-color:rgba(170,68,255,.4);}

/* ADMIN */
.admin-tabs{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:16px;border-bottom:2px solid var(--red);padding-bottom:8px;}
.admin-tab{background:none;border:1px solid transparent;color:var(--gray-mid);padding:6px 12px;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:12px;cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;}
.admin-tab.active{background:var(--red);color:white;border-color:var(--red);}
.admin-tab:hover:not(.active){border-color:var(--red);color:white;}

/* MOD INFO */
.mod-info-box{background:rgba(68,153,255,.07);border:1px solid rgba(68,153,255,.3);border-radius:8px;padding:14px;margin-bottom:16px;}
.mod-info-title{font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:2px;color:var(--blue);margin-bottom:5px;}

/* MOBILE NAV */
.mobile-nav{display:none;position:fixed;bottom:0;left:0;right:0;background:rgba(8,0,0,.98);border-top:2px solid var(--red);z-index:999;padding:5px 0;}
.mobile-nav-inner{display:flex;justify-content:space-around;}
.mob-nav-btn{display:flex;flex-direction:column;align-items:center;gap:2px;background:none;border:none;color:var(--gray-mid);font-family:'Rajdhani',sans-serif;font-size:10px;font-weight:600;padding:4px 10px;cursor:pointer;transition:color .2s;text-transform:uppercase;}
.mob-nav-btn.active,.mob-nav-btn:hover{color:var(--red-bright);}
.mob-nav-icon{font-size:18px;}
@media(max-width:768px){.mobile-nav{display:block;}main{padding-bottom:70px;}}

/* LOADING / EMPTY */
.loading-spinner{display:flex;align-items:center;justify-content:center;padding:40px;gap:12px;color:var(--gray-mid);}
.spinner{width:24px;height:24px;border:2px solid rgba(204,0,0,.2);border-top-color:var(--red);border-radius:50%;animation:spin .7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.empty-state{text-align:center;padding:40px 20px;color:var(--gray-mid);}
.empty-icon{font-size:40px;margin-bottom:10px;}
.empty-text{font-size:16px;font-weight:600;color:#C0A0A0;}
.empty-sub{font-size:13px;margin-top:5px;opacity:.6;}

/* TEXT UTILS */
.text-red{color:#FF6666;}.text-green{color:#44FF88;}.text-yellow{color:#FFCC44;}.text-gold{color:var(--gold);}.text-blue{color:#88CCFF;}.text-purple{color:#CC88FF;}.text-gray{color:var(--gray-mid);}.text-sm{font-size:13px;}.font-bold{font-weight:700;}
.mt-8{margin-top:8px;}.mt-12{margin-top:12px;}.mt-16{margin-top:16px;}.mb-8{margin-bottom:8px;}.mb-16{margin-bottom:16px;}
.flex{display:flex;}.gap-6{gap:6px;}.gap-8{gap:8px;}.items-center{align-items:center;}.justify-between{justify-content:space-between;}.flex-wrap{flex-wrap:wrap;}

/* ===== RANKING GRAPHIC CARD ===== */
#rankingCardCanvas{display:none;}
.ranking-card-preview{display:none;position:fixed;inset:0;background:rgba(0,0,0,.92);z-index:3000;align-items:center;justify-content:center;flex-direction:column;gap:16px;padding:20px;}
.ranking-card-preview.open{display:flex;}
.ranking-card-close{position:absolute;top:16px;right:16px;background:rgba(204,0,0,.3);border:1px solid var(--red);color:white;width:32px;height:32px;border-radius:50%;font-size:16px;cursor:pointer;display:flex;align-items:center;justify-content:center;}

/* The actual rendered card */
.rc-card{width:800px;background:#0a0000;border:2px solid #CC0000;border-radius:12px;overflow:hidden;position:relative;font-family:'Rajdhani',sans-serif;}
.rc-header{background:linear-gradient(135deg,#CC0000 0%,#800000 50%,#400000 100%);padding:20px 24px 16px;position:relative;overflow:hidden;}
.rc-header::before{content:'LLFC';position:absolute;right:-15px;top:-15px;font-family:'Bebas Neue',sans-serif;font-size:120px;color:rgba(255,255,255,.07);pointer-events:none;}
.rc-header-top{display:flex;align-items:center;justify-content:space-between;}
.rc-title{font-family:'Bebas Neue',sans-serif;font-size:28px;letter-spacing:4px;color:white;}
.rc-subtitle{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:3px;color:rgba(255,255,255,.7);margin-top:2px;}
.rc-period{background:rgba(0,0,0,.4);border:1px solid rgba(255,255,255,.2);border-radius:4px;padding:4px 12px;font-size:12px;font-weight:700;letter-spacing:2px;color:rgba(255,255,255,.8);text-transform:uppercase;}
.rc-body{padding:0;}
.rc-row{display:grid;grid-template-columns:44px 1fr 80px 80px 140px 70px;align-items:center;padding:11px 24px;border-bottom:1px solid rgba(204,0,0,.12);gap:8px;}
.rc-row:last-child{border-bottom:none;}
.rc-row.header-row{background:#1a0606;padding:9px 24px;border-bottom:2px solid rgba(204,0,0,.3);}
.rc-row.header-row span{font-size:10px;letter-spacing:2px;text-transform:uppercase;color:#906060;font-weight:700;}
.rc-row.rank-1-row{background:linear-gradient(90deg,rgba(255,215,0,.1),transparent);}
.rc-row.rank-2-row{background:linear-gradient(90deg,rgba(192,192,192,.07),transparent);}
.rc-row.rank-3-row{background:linear-gradient(90deg,rgba(205,127,50,.07),transparent);}
.rc-rank{font-family:'Bebas Neue',sans-serif;font-size:26px;color:#806060;}
.rc-rank.r1{color:#FFD700;}.rc-rank.r2{color:#C0C0C0;}.rc-rank.r3{color:#CD7F32;}
.rc-player-info{display:flex;align-items:center;gap:8px;}
.rc-avatar{width:28px;height:28px;border-radius:50%;background:#CC0000;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:13px;color:white;flex-shrink:0;}
.rc-name{font-family:'Bebas Neue',sans-serif;font-size:16px;letter-spacing:1px;color:#F0E0E0;}
.rc-div-small{font-family:'Bebas Neue',sans-serif;font-size:10px;color:#906060;letter-spacing:1px;}
.rc-rating{font-family:'Bebas Neue',sans-serif;font-size:20px;color:#FF4444;text-align:right;}
.rc-wdl{display:flex;flex-direction:column;gap:3px;}
.rc-wdl-num{font-family:'Bebas Neue',sans-serif;font-size:14px;display:flex;gap:6px;}
.rc-w{color:#44FF88;}.rc-d{color:#FFCC44;}.rc-l{color:#FF6666;}
.rc-winpct{font-family:'Bebas Neue',sans-serif;font-size:20px;color:#C0A0A0;text-align:right;}
.rc-footer{background:#0d0000;padding:10px 24px;display:flex;justify-content:space-between;align-items:center;border-top:1px solid rgba(204,0,0,.2);}
.rc-footer-brand{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:3px;color:#603030;}
.rc-footer-date{font-size:11px;color:#503030;letter-spacing:1px;}
</style>
</head>
<body>

<header>
  <div class="header-inner">
    <div class="logo-area" onclick="navTo('home')">
      <div class="logo-badge">LLFC</div>
      <div class="logo-text">
        <span class="logo-main">LLFC</span>
        <span class="logo-sub">Juvenile Division</span>
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
      <button class="btn-login" style="border-color:var(--yellow);color:var(--yellow);font-size:11px" onclick="navTo('admin')">Admin</button>
    </div>
  </div>
</header>

<main>

<!-- HOME -->
<div class="page active" id="page-home">
  <div class="news-ticker" id="newsTicker" style="display:none">
    <div class="news-label">BREAKING</div>
    <div class="news-scroll-wrap"><span class="news-scroll-text" id="newsText"></span></div>
  </div>
  <div class="hero">
    <div class="hero-tag">Season Active</div>
    <h1>LLFC <span>Juvenile</span> Division</h1>
    <p>Play freely. Submit results. Climb the ranks. From Division 9 to Division 1.</p>
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
    <div class="section-title">Division Guide</div>
    <div class="three-col" id="divisionGuide"></div>
  </div>
</div>

<!-- LEADERBOARD -->
<div class="page" id="page-leaderboard">
  <div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:10px;margin-bottom:16px;">
    <div class="section-title" style="margin-bottom:0">Leaderboards</div>
    <button class="btn-primary" style="padding:8px 18px;font-size:12px" onclick="openRankingCardPreview()">Download Ranking Card (JPG)</button>
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
          <th style="width:42px">Rank</th>
          <th>Player</th>
          <th>Div</th>
          <th>Rating</th>
          <th>W / D / L</th>
          <th>MP</th>
          <th>Win%</th>
          <th>GD</th>
          <th>Form</th>
          <th>Cycle</th>
        </tr>
      </thead>
      <tbody id="lbTableBody">
        <tr><td colspan="10" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- MATCHES -->
<div class="page" id="page-matches">
  <div class="section-title">Match History</div>
  <div class="search-bar">
    <input class="search-input" placeholder="Search by player..." id="matchSearch" oninput="filterMatches()">
    <select class="form-select-sm" id="matchStatusFilter" onchange="filterMatches()">
      <option value="">All</option>
      <option value="confirmed">Confirmed</option>
      <option value="pending">Pending</option>
      <option value="disputed">Disputed</option>
    </select>
  </div>
  <div id="matchesList"><div class="loading-spinner"><div class="spinner"></div></div></div>
  <div id="pendingConfirmSection" style="display:none">
    <div class="section-title mt-16">Awaiting Confirmation</div>
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
    <div class="card card-red" style="max-width:540px;margin:0 auto">
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
        <p class="text-gray text-sm" style="text-align:center;margin-top:6px">Opponent must confirm. Multiple pending allowed.</p>
      </div>
    </div>
  </div>
</div>

<!-- PROFILE -->
<div class="page" id="page-profile">
  <button class="btn-secondary mb-16" onclick="navBack()">Back</button>
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
    <div id="adminTab-moderators" style="display:none">
      <div class="section-title">Moderator Management</div>
      <div class="mod-info-box">
        <div class="mod-info-title">About Moderators</div>
        <p class="text-gray text-sm">Moderators can approve or dispute any pending match. Cannot edit players or admin settings.</p>
      </div>
      <div class="search-bar"><input class="search-input" placeholder="Search player..." id="modPlayerSearch" oninput="filterModPlayers()"></div>
      <div id="modPlayersList"></div>
    </div>
    <div id="adminTab-season" style="display:none">
      <div class="section-title">Season Management</div>
      <div class="card" style="max-width:480px;margin-bottom:20px">
        <p class="text-gray mb-16">Configure season duration and division promotion cycle.</p>
        <div class="match-form">
          <div class="form-group"><label class="form-label">Season Duration (days)</label><input class="form-input" type="number" id="seasonDuration" value="30" min="7"></div>
          <div class="form-group"><label class="form-label">Season Start Date</label><input class="form-input" type="date" id="seasonStart"></div>
          <button class="btn-primary" onclick="saveSeasonSettings()">Save Season Settings</button>
        </div>
      </div>
      <div class="card" style="max-width:480px">
        <p class="text-gray mb-16" style="color:#FF8888;">Full reset: clears all match results, resets all player stats to zero. Player accounts remain.</p>
        <button class="btn-reject btn-sm" style="padding:10px 24px;font-size:13px" onclick="confirmSeasonReset()">Reset Season</button>
      </div>
    </div>
    <div id="adminTab-adminSettings" style="display:none">
      <div class="section-title">Settings</div>
      <div class="card" style="max-width:400px">
        <div class="match-form">
          <div class="form-group"><label class="form-label">New Admin Password</label><input class="form-input" type="password" id="newAdminPw" placeholder="New password"></div>
          <div class="form-group"><label class="form-label">Confirm Password</label><input class="form-input" type="password" id="confirmAdminPw" placeholder="Confirm"></div>
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
  <div id="rcCardContainer"></div>
  <div style="display:flex;gap:10px;flex-wrap:wrap;justify-content:center;">
    <button class="btn-primary" onclick="downloadRankingCard()">Download JPG</button>
    <button class="btn-secondary" onclick="closeRankingPreview()">Close</button>
  </div>
</div>

<!-- MODALS -->
<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('loginModal')">X</button>
    <div class="modal-title">Player Login</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Name</label><input class="form-input" id="loginName" placeholder="Your registered name"></div>
      <div class="form-group"><label class="form-label">Password</label><input class="form-input" type="password" id="loginPw" placeholder="Password" onkeydown="if(event.key==='Enter')doLogin()"></div>
      <button class="btn-primary w-full" onclick="doLogin()">Login</button>
      <p class="text-gray text-sm" style="text-align:center;margin-top:8px">No account? <span class="text-red" style="cursor:pointer" onclick="closeModal('loginModal');openModal('registerModal')">Register</span></p>
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
        <select class="form-select" id="regCategory"><option value="Youth">Youth</option><option value="Academy">Academy</option></select>
      </div>
      <div class="form-group"><label class="form-label">Password</label><input class="form-input" type="password" id="regPw" placeholder="Password"></div>
      <div class="form-group"><label class="form-label">Confirm Password</label><input class="form-input" type="password" id="regPwConfirm" placeholder="Confirm"></div>
      <button class="btn-primary w-full" onclick="doRegister()">Register</button>
      <p class="text-gray text-sm" style="text-align:center;margin-top:8px">Requires admin approval before you can play.</p>
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
      <div class="form-group"><label class="form-label">Points</label><input class="form-input" type="number" id="editPoints"></div>
      <div class="form-group"><label class="form-label">Wins</label><input class="form-input" type="number" id="editWins"></div>
      <div class="form-group"><label class="form-label">Draws</label><input class="form-input" type="number" id="editDraws"></div>
      <div class="form-group"><label class="form-label">Losses</label><input class="form-input" type="number" id="editLosses"></div>
      <div class="form-group"><label class="form-label">Goals For (overall)</label><input class="form-input" type="number" id="editGF"></div>
      <div class="form-group"><label class="form-label">Goals Against (overall)</label><input class="form-input" type="number" id="editGA"></div>
      <div class="form-group"><label class="form-label">Cycle Matches Played</label><input class="form-input" type="number" id="editCycleMP"></div>
      <div class="form-group"><label class="form-label">Cycle Points</label><input class="form-input" type="number" id="editCyclePts"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editStatus"><option value="active">Active</option><option value="banned">Banned</option><option value="pending">Pending</option></select>
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
  getFirestore, collection, doc, getDoc, getDocs, addDoc, setDoc,
  updateDoc, deleteDoc, query, where, orderBy, limit, serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const app = initializeApp({
  apiKey:"AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLtDopPq4",
  authDomain:"llfc-4d2df.firebaseapp.com",
  projectId:"llfc-4d2df",
  storageBucket:"llfc-4d2df.firebasestorage.app",
  messagingSenderId:"697058785471",
  appId:"1:697058785471:web:7481cae8fe6b682d762e0a"
});
const db = getFirestore(app);

// ===== DIVISION SYSTEM =====
// Each division has: cycle (max matches), points needed to promote early, relegation points
// Div 9 = easy entry, higher = harder
const DIV_RULES = {
  9: { cycle:10, promoPoints:12, reloPoints:0,  nextDiv:8, name:'Rookie',       color:'#333333' },
  8: { cycle:10, promoPoints:15, reloPoints:3,  nextDiv:7, name:'Amateur',      color:'#440000' },
  7: { cycle:10, promoPoints:18, reloPoints:4,  nextDiv:6, name:'Regional',     color:'#550000' },
  6: { cycle:10, promoPoints:21, reloPoints:5,  nextDiv:5, name:'National',     color:'#660000' },
  5: { cycle:10, promoPoints:24, reloPoints:6,  nextDiv:4, name:'League Two',   color:'#880000' },
  4: { cycle:10, promoPoints:27, reloPoints:7,  nextDiv:3, name:'League One',   color:'#CC0000' },
  3: { cycle:10, promoPoints:30, reloPoints:8,  nextDiv:2, name:'Championship', color:'#CD7F32' },
  2: { cycle:10, promoPoints:33, reloPoints:9,  nextDiv:1, name:'Premier',      color:'#C0C0C0' },
  1: { cycle:10, promoPoints:999,reloPoints:10, nextDiv:1, name:'Elite',        color:'#FFD700' },
};

// ===== GLOBAL STATE =====
let S = {
  user:null, lbTab:'overall', players:[], matches:[],
  lbPlayers:[], allMatchesData:[], adminPlayers:[],
  pageHistory:['home'], adminPw:'fardous',
  seasonStart: null, seasonDuration: 30
};

// ===== UTILS =====
const $ = id => document.getElementById(id);
function T(msg,type='info'){const t=$('toast');t.textContent=msg;t.className=`toast show ${type}`;clearTimeout(window._tt);window._tt=setTimeout(()=>t.classList.remove('show'),3500);}
function openModal(id){$(id).classList.add('open');}
function closeModal(id){$(id).classList.remove('open');}

function showPage(pg){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const el=$('page-'+pg); if(el)el.classList.add('active');
}
function navTo(pg){
  S.pageHistory.push(pg); showPage(pg);
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
function navBack(){S.pageHistory.pop();const prev=S.pageHistory[S.pageHistory.length-1]||'home';showPage(prev);}
function setNavActive(b){document.querySelectorAll('.nav-btn').forEach(x=>x.classList.remove('active'));b.classList.add('active');}
function setMobActive(b){document.querySelectorAll('.mob-nav-btn').forEach(x=>x.classList.remove('active'));b.classList.add('active');}

// --- Helpers ---
function divBadge(d,size='sm'){
  const s=size==='lg'?'div-badge-lg':'div-badge';
  return `<div class="${s} div-${d||9}">${d||9}</div>`;
}
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
function statusBadge(s){return`<span class="status-badge status-${s}">${s}</span>`;}
function formBadge(r){const c=r==='W'?'form-w':r==='D'?'form-d':'form-l';return`<div class="form-dot ${c}" title="${r}"></div>`;}

// ===== RATING CALCULATION (from match history) =====
// Rating = W*10 + D*5 + L*(-5) + GD*1 + CleanSheets*2
function calcRatingFromStats(w,d,l,gf,ga,cs){
  return Math.max(0, w*10 + d*5 + l*(-5) + (gf-ga)*1 + cs*2);
}

// ===== DIVISION CYCLE LOGIC =====
// After each confirmed match, check if cycle complete (cycleMP >= 10) or early promo
// Returns {promoted, relegated, cycleComplete}
function checkDivisionStatus(player) {
  const div = player.division || 9;
  const rules = DIV_RULES[div];
  const cmp = player.cycleMP || 0;
  const cpts = player.cyclePts || 0;
  
  // Early promotion: hit points target before 10 matches
  if(cpts >= rules.promoPoints && div > 1) return 'promote';
  // Cycle complete (10 matches played)
  if(cmp >= rules.cycle) {
    if(cpts >= rules.promoPoints) return 'promote';
    if(cpts <= rules.reloPoints && div < 9) return 'relegate';
    return 'stay';
  }
  return null;
}

async function applyDivisionCheck(pid, playerData) {
  const div = playerData.division || 9;
  const result = checkDivisionStatus(playerData);
  if(!result) return;
  
  let newDiv = div;
  if(result === 'promote') {
    newDiv = Math.max(1, div - 1);
  } else if(result === 'relegate') {
    newDiv = Math.min(9, div + 1);
  }
  
  // Reset cycle
  await updateDoc(doc(db,'players',pid), {
    division: newDiv,
    cycleMP: 0,
    cyclePts: 0,
    highestDivision: Math.min(newDiv, playerData.highestDivision || 9)
  });
  
  return result;
}

// ===== BADGES CALCULATION =====
function calcBadges(player, allMatches) {
  const badges = [];
  const div = player.division || 9;
  const highest = player.highestDivision || div;
  const total = (player.wins||0)+(player.draws||0)+(player.losses||0);
  const wr = total>0 ? Math.round((player.wins||0)/total*100) : 0;
  
  // Division badge
  if(div <= 1) badges.push({text:'Elite Division', cls:'badge-gold'});
  else if(div <= 2) badges.push({text:'Premier Division', cls:'badge-silver'});
  else if(div <= 3) badges.push({text:'Championship', cls:'badge-red'});
  
  // Highest division badge
  if(highest < div) badges.push({text:'Was Div '+highest, cls:'badge-blue'});
  
  // Win ratio badges
  if(wr >= 80 && total >= 5) badges.push({text:'Win Machine 80%+', cls:'badge-gold'});
  else if(wr >= 70 && total >= 5) badges.push({text:'Sharp 70%+', cls:'badge-green'});
  
  // Winning streak
  const form = (player.form || []);
  let streak = 0;
  for(let i=form.length-1;i>=0;i--){ if(form[i]==='W') streak++; else break; }
  if(streak >= 5) badges.push({text:'On Fire '+ streak + ' Streak', cls:'badge-red'});
  else if(streak >= 3) badges.push({text:streak+' Win Streak', cls:'badge-green'});
  
  // Special awards
  if(player.isPOTD) badges.push({text:'Player of the Day', cls:'badge-gold'});
  if(player.isPOTW) badges.push({text:'Player of the Week', cls:'badge-gold'});
  if(player.isPOTM) badges.push({text:'Player of the Month', cls:'badge-purple'});
  if(player.isPOTS) badges.push({text:'Player of the Season', cls:'badge-gold'});
  if(player.isModerator) badges.push({text:'Moderator', cls:'badge-blue'});
  
  return badges;
}

// ===== NEWS =====
function buildNews(matches) {
  const hi = matches.filter(m=>m.status==='confirmed'&&isHigh(m.scoreA,m.scoreB));
  if(!hi.length){$('newsTicker').style.display='none';return;}
  $('newsText').textContent = hi.slice(0,8).map(m=>`GOAL FEST: ${m.playerAName} ${m.scoreA}-${m.scoreB} ${m.playerBName} (${m.scoreA+m.scoreB} goals)`).join('     |     ');
  $('newsTicker').style.display='flex';
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
    closeModal('loginModal'); updateHeaderAuth();
    T('Welcome back, '+name+'!','success');
    loadSubmitPage(); loadMatches();
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
      ${isMod?`<button class="btn-login" style="border-color:var(--blue);color:var(--blue);font-size:11px" onclick="navTo('modpanel')">Mod Panel</button>`:''}
      <button class="btn-login" onclick="doLogout()">Logout</button>
      <button class="btn-login" style="border-color:var(--yellow);color:var(--yellow);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }else{
    el.innerHTML=`
      <button class="btn-login" onclick="openModal('loginModal')">Login</button>
      <button class="btn-register" onclick="openModal('registerModal')">Register</button>
      <button class="btn-login" style="border-color:var(--yellow);color:var(--yellow);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }
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
    const now=Date.now();
    const todayMs=S.matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<86400000);
    $('statPlayers').textContent=S.players.length;
    $('statMatches').textContent=S.matches.filter(m=>m.status==='confirmed').length;
    $('statToday').textContent=todayMs.length;
    $('statPending').textContent=S.matches.filter(m=>m.status==='pending').length;

    // Top 5 with computed rating
    const sorted=[...S.players].map(p=>{
      const r=calcRatingFromStats(p.wins||0,p.draws||0,p.losses||0,p.goalsFor||0,p.goalsAgainst||0,p.cleanSheets||0);
      return {...p,computedRating:r};
    }).sort((a,b)=>b.computedRating-a.computedRating).slice(0,5);

    $('homeTopPlayers').innerHTML=sorted.length?sorted.map((p,i)=>`
      <div class="pending-item" style="cursor:pointer" onclick="viewProfile('${p.id}')">
        <span class="rank-num rank-${i+1}" style="font-size:20px;width:26px">${i+1}</span>
        ${divBadge(p.division)}
        <div class="pending-info">
          <div class="pending-name">${p.name}</div>
          <div class="pending-meta">${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
        </div>
        <span style="font-family:'Bebas Neue',sans-serif;font-size:20px;color:#FF4444">${p.computedRating}</span>
      </div>`).join(''):'<div class="empty-state"><div class="empty-text">No players yet</div></div>';

    const recent=S.matches.filter(m=>m.status==='confirmed').slice(0,6);
    $('homeRecentMatches').innerHTML=recent.length?recent.map(m=>{
      const hi=isHigh(m.scoreA,m.scoreB);
      return `<div class="match-card${hi?' high-score':''}">
        <div class="match-info">
          <div class="match-vs">
            <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
            <span class="text-gray"> vs </span>
            <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
            ${hi?'&nbsp;<span class="high-score-badge">GOAL FEST</span>':''}
          </div>
          <div class="match-meta">${fmtDate(m.createdAt)}</div>
        </div>
        <div class="match-score">${m.scoreA}-${m.scoreB}</div>
      </div>`;
    }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>';

    const divInfo=[
      {d:1,name:'Elite',pts:999,desc:'Top division. Defend your spot.'},
      {d:2,name:'Premier',pts:33,desc:'Promote: 33 pts in 10 matches.'},
      {d:3,name:'Championship',pts:30,desc:'Promote: 30 pts in 10 matches.'},
      {d:4,name:'League One',pts:27,desc:'Promote: 27 pts in 10 matches.'},
      {d:5,name:'League Two',pts:24,desc:'Promote: 24 pts in 10 matches.'},
      {d:6,name:'National',pts:21,desc:'Promote: 21 pts in 10 matches.'},
      {d:7,name:'Regional',pts:18,desc:'Promote: 18 pts in 10 matches.'},
      {d:8,name:'Amateur',pts:15,desc:'Promote: 15 pts in 10 matches.'},
      {d:9,name:'Rookie',pts:12,desc:'Promote: 12 pts in 10 matches. Easy start!'},
    ];
    $('divisionGuide').innerHTML=divInfo.map(di=>`
      <div class="stat-card" style="text-align:left;border-color:${di.d<=3?'rgba(204,0,0,.4)':'rgba(204,0,0,.15)'}">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:6px">
          ${divBadge(di.d)}
          <span style="font-family:'Bebas Neue',sans-serif;font-size:15px">${di.name}</span>
        </div>
        <div class="text-gray text-sm">${di.desc}</div>
        ${di.d<=3?'<div style="font-size:10px;color:var(--red-bright);margin-top:4px;letter-spacing:1px">TOP TIER</div>':''}
      </div>`).join('');
  }catch(e){console.error(e);T('Error loading home','error');}
}

// ===== LEADERBOARD =====
async function loadLeaderboard(tab='overall'){
  S.lbTab=tab;
  $('lbTableBody').innerHTML='<tr><td colspan="10" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>';
  try{
    const [pSnap,mSnap]=await Promise.all([
      getDocs(collection(db,'players')),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(500)))
    ]);
    S.players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const now=Date.now();
    const timeFilter={daily:86400000,weekly:604800000,monthly:2592000000,overall:Infinity}[tab];

    let players=S.players.map(p=>{
      let pm=S.matches.filter(m=>(m.playerAId===p.id||m.playerBId===p.id)&&m.status==='confirmed');
      if(tab!=='overall') pm=pm.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<timeFilter);
      
      let w=0,d=0,l=0,gf=0,ga=0,cs=0;
      pm.forEach(m=>{
        const side=m.playerAId===p.id?'A':'B';
        const r=getRC(m.scoreA,m.scoreB,side);
        const my=side==='A'?m.scoreA:m.scoreB,op=side==='A'?m.scoreB:m.scoreA;
        if(r==='W')w++;else if(r==='D')d++;else l++;
        gf+=my; ga+=op;
        if(op===0)cs++;
      });
      
      const total=w+d+l;
      const wr=total>0?Math.round(w/total*100):0;
      const gd=gf-ga;
      // Rating computed from these filtered stats
      const rating=calcRatingFromStats(w,d,l,gf,ga,cs);
      
      return {...p,tw:w,td:d,tl:l,tgf:gf,tga:ga,tcs:cs,tgd:gd,twr:wr,total,rating};
    });

    if(tab!=='overall') players=players.filter(p=>p.total>0);
    players.sort((a,b)=>b.rating-a.rating||b.tgd-a.tgd||b.twr-a.twr);
    S.lbPlayers=players;
    renderLbTable(players);
  }catch(e){
    $('lbTableBody').innerHTML='<tr><td colspan="10" style="text-align:center;color:var(--red)">Error loading</td></tr>';
    console.error(e);
  }
}

function renderLbTable(players){
  const search=($('lbSearch')?.value||'').toLowerCase();
  const divF=$('lbDivFilter')?.value||'';
  const filtered=players.filter(p=>p.name.toLowerCase().includes(search)&&(!divF||String(p.division||9)===divF));
  const tbody=$('lbTableBody');
  if(!filtered.length){tbody.innerHTML='<tr><td colspan="10"><div class="empty-state"><div class="empty-icon">&#127942;</div><div class="empty-text">No players found</div></div></td></tr>';return;}
  tbody.innerHTML=filtered.map((p,i)=>{
    const r=i+1,rc=r===1?'top-1':r===2?'top-2':r===3?'top-3':'';
    const form=(p.form||[]).slice(-5);
    const rules=DIV_RULES[p.division||9];
    const cmp=p.cycleMP||0, cpts=p.cyclePts||0;
    const pct=Math.min(100,Math.round(cpts/rules.promoPoints*100));
    return `<tr class="${rc}">
      <td><span class="rank-num rank-${r}">${r}</span></td>
      <td>
        <span class="player-link" onclick="viewProfile('${p.id}')">
          <div class="user-avatar" style="width:26px;height:26px;font-size:11px;background:#CC0000">${p.name[0].toUpperCase()}</div>
          ${p.name}${p.isModerator?'&nbsp;<span class="mod-badge-hdr">MOD</span>':''}
        </span>
      </td>
      <td>${divBadge(p.division)}</td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:19px;color:#FF4444">${p.rating}</span></td>
      <td>
        <div class="wdl-row">
          <span class="wdl-pill wdl-w"><span class="wdl-num">${p.tw}</span>&nbsp;W</span>
          <span class="wdl-pill wdl-d"><span class="wdl-num">${p.td}</span>&nbsp;D</span>
          <span class="wdl-pill wdl-l"><span class="wdl-num">${p.tl}</span>&nbsp;L</span>
        </div>
      </td>
      <td style="color:#C0A0A0">${p.total}</td>
      <td>
        <div class="winrate-wrap">
          <div class="winrate-bar"><div class="winrate-fill" style="width:${p.twr}%"></div></div>
          <span class="winrate-pct">${p.twr}%</span>
        </div>
      </td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:16px;color:${p.tgd>=0?'#44FF88':'#FF6666'}">${p.tgd>=0?'+':''}${p.tgd}</span></td>
      <td><div class="form-dots">${form.map(r=>formBadge(r)).join('')}</div></td>
      <td>
        <div style="font-size:11px;color:#906060">${cmp}/10</div>
        <div style="background:rgba(255,255,255,.07);border-radius:4px;height:4px;width:50px;margin-top:3px;overflow:hidden">
          <div style="height:100%;width:${pct}%;background:var(--red);border-radius:4px"></div>
        </div>
      </td>
    </tr>`;
  }).join('');
}

function filterLeaderboard(){if(S.lbPlayers.length)renderLbTable(S.lbPlayers);}
function switchLbTab(tab,btn){document.querySelectorAll('.lb-tab').forEach(b=>b.classList.remove('active'));btn.classList.add('active');loadLeaderboard(tab);}

// ===== RANKING CARD (JPG Download) =====
function openRankingCardPreview(){
  buildRankingCard();
  $('rankingCardPreview').classList.add('open');
}
function closeRankingPreview(){$('rankingCardPreview').classList.remove('open');}

function buildRankingCard(){
  const top10=S.lbPlayers.slice(0,10);
  const tabLabels={overall:'Overall Season',daily:'Daily',weekly:'Weekly',monthly:'Monthly'};
  const now=new Date().toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'});
  
  if(!top10.length){$('rcCardContainer').innerHTML='<div style="color:#666;padding:20px">Load leaderboard first</div>';return;}
  
  const rows=top10.map((p,i)=>{
    const rank=i+1;
    const rowCls=rank===1?'rank-1-row':rank===2?'rank-2-row':rank===3?'rank-3-row':'';
    const rankCls=rank===1?'r1':rank===2?'r2':rank===3?'r3':'';
    const divNames=['','Elite','Premier','Championship','League One','League Two','National','Regional','Amateur','Rookie'];
    return `<div class="rc-row ${rowCls}">
      <div class="rc-rank ${rankCls}">${rank}</div>
      <div class="rc-player-info">
        <div class="rc-avatar">${p.name[0].toUpperCase()}</div>
        <div>
          <div class="rc-name">${p.name}</div>
          <div class="rc-div-small">DIV ${p.division||9} - ${divNames[p.division||9]||'Rookie'}</div>
        </div>
      </div>
      <div class="rc-rating">${p.rating}</div>
      <div class="rc-wdl">
        <div class="rc-wdl-num"><span class="rc-w">${p.tw}W</span><span class="rc-d">${p.td}D</span><span class="rc-l">${p.tl}L</span></div>
      </div>
      <div style="display:flex;gap:5px;align-items:center">
        <div style="background:rgba(255,255,255,.07);border-radius:4px;height:5px;width:60px;overflow:hidden">
          <div style="height:100%;width:${p.twr}%;background:#CC0000;border-radius:4px"></div>
        </div>
        <span style="font-family:'Bebas Neue',sans-serif;font-size:14px;color:#906060">${p.twr}%</span>
      </div>
      <div class="rc-winpct">${p.tgd>=0?'+':''}${p.tgd}</div>
    </div>`;
  }).join('');
  
  $('rcCardContainer').innerHTML=`
    <div class="rc-card" id="theRankingCard">
      <div class="rc-header">
        <div class="rc-header-top">
          <div>
            <div class="rc-title">LLFC EFOOT DIVISION</div>
            <div class="rc-subtitle">PLAYER RANKING - TOP 10</div>
          </div>
          <div class="rc-period">${tabLabels[S.lbTab]||'Overall'}</div>
        </div>
      </div>
      <div class="rc-body">
        <div class="rc-row header-row">
          <span>Rank</span><span>Player</span><span style="text-align:right">Rating</span>
          <span>W/D/L</span><span>Win%</span><span style="text-align:right">GD</span>
        </div>
        ${rows}
      </div>
      <div class="rc-footer">
        <div class="rc-footer-brand">LLFC JUVENILE DIVISION SYSTEM</div>
        <div class="rc-footer-date">Generated: ${now}</div>
      </div>
    </div>`;
}

async function downloadRankingCard(){
  const card=$('theRankingCard');
  if(!card){T('No card to download','error');return;}
  try{
    T('Generating image...','info');
    const canvas=await html2canvas(card,{
      backgroundColor:'#0a0000',scale:2,useCORS:true,logging:false
    });
    const link=document.createElement('a');
    link.download=`LLFC-Ranking-${S.lbTab}-${new Date().toISOString().split('T')[0]}.jpg`;
    link.href=canvas.toDataURL('image/jpeg',0.95);
    link.click();
    T('Ranking card downloaded!','success');
  }catch(e){T('Download failed: '+e.message,'error');console.error(e);}
}

// ===== MATCHES =====
async function loadMatches(){
  try{
    const mSnap=await getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(150)));
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    S.allMatchesData=S.matches;
    renderMatchesList(S.matches);
    const section=$('pendingConfirmSection'),list=$('pendingConfirmList');
    if(S.user){
      const isMod=S.user.isModerator;
      const pending=S.matches.filter(m=>m.status==='pending'&&(isMod||m.playerBId===S.user.id));
      if(pending.length){
        section.style.display='block';
        list.innerHTML=pending.map(m=>`
          <div class="confirm-card">
            ${isMod&&m.playerBId!==S.user.id?'<div class="text-purple text-sm mb-8">Moderator review</div>':''}
            <div class="confirm-vs">
              <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">Submitted by</div></div>
              <div class="confirm-score-display">${m.scoreA}-${m.scoreB}</div>
              <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">Opponent</div></div>
            </div>
            <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} - ${timeAgo(m.createdAt)}</div>
            <div style="display:flex;gap:8px;flex-wrap:wrap">
              <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">Confirm</button>
              <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">Dispute</button>
            </div>
          </div>`).join('');
      }else section.style.display='none';
    }else section.style.display='none';
  }catch(e){$('matchesList').innerHTML='<div class="empty-state"><div class="empty-text">Error loading matches</div></div>';console.error(e);}
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
    const hi=isHigh(m.scoreA,m.scoreB);
    return `<div class="match-card${hi?' high-score':''}">
      <div class="match-info">
        <div class="match-vs">
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
          <span class="text-gray"> vs </span>
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
          ${hi?' &nbsp;<span class="high-score-badge">GOAL FEST</span>':''}
        </div>
        <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} - ${statusBadge(m.status)}</div>
      </div>
      <div class="match-score">${m.scoreA}-${m.scoreB}</div>
    </div>`;
  }).join('');
}

function filterMatches(){if(S.allMatchesData.length)renderMatchesList(S.allMatchesData);}

async function confirmMatch(matchId,confirmed){
  try{
    const mRef=doc(db,'matches',matchId);
    const mSnap=await getDoc(mRef);
    if(!mSnap.exists())return T('Match not found','error');
    const m=mSnap.data();
    if(confirmed){
      await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
      await applyMatchStats(m);
      T('Match confirmed! Stats updated','success');
    }else{
      await updateDoc(mRef,{status:'disputed'});
      T('Match disputed. Admin will review.','info');
    }
    S.matches=[];loadMatches();
  }catch(e){T('Error: '+e.message,'error');}
}

async function applyMatchStats(m){
  async function upd(pid,side){
    const ref=doc(db,'players',pid),snap=await getDoc(ref);
    if(!snap.exists())return;
    const p=snap.data();
    const result=getRC(m.scoreA,m.scoreB,side);
    const my=side==='A'?m.scoreA:m.scoreB, op=side==='A'?m.scoreB:m.scoreA;
    const isCS=op===0;
    const form=[...(p.form||[]).slice(-19),result]; // keep last 20
    
    // Cycle points: W=3, D=1, L=0
    const cyclePtsGain=result==='W'?3:result==='D'?1:0;
    const newCycleMP=(p.cycleMP||0)+1;
    const newCyclePts=(p.cyclePts||0)+cyclePtsGain;
    
    const updates={
      wins:(p.wins||0)+(result==='W'?1:0),
      draws:(p.draws||0)+(result==='D'?1:0),
      losses:(p.losses||0)+(result==='L'?1:0),
      goalsFor:(p.goalsFor||0)+my,
      goalsAgainst:(p.goalsAgainst||0)+op,
      cleanSheets:(p.cleanSheets||0)+(isCS?1:0),
      form,
      cycleMP:newCycleMP,
      cyclePts:newCyclePts,
    };
    await updateDoc(ref,updates);
    
    // Check division status
    const updatedPlayer={...p,...updates};
    const divResult=await applyDivisionCheck(pid,updatedPlayer);
    if(divResult==='promote'){T(p.name+' promoted to Division '+(Math.max(1,(p.division||9)-1))+'!','success');}
    else if(divResult==='relegate'){T(p.name+' relegated to Division '+(Math.min(9,(p.division||9)+1))+'.','info');}
    else if(divResult==='stay'){T(p.name+' cycle complete. Division maintained.','info');}
  }
  await Promise.all([upd(m.playerAId,'A'),upd(m.playerBId,'B')]);
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
    S.players.filter(p=>p.id!==S.user.id).map(p=>`<option value="${p.id}">${p.name} (Div ${p.division||9})</option>`).join('');
}

async function submitMatchResult(){
  if(!S.user)return T('Login required','error');
  const oppId=$('submitOpponent').value;
  const sA=parseInt($('scoreA').value)||0,sB=parseInt($('scoreB').value)||0;
  const matchDate=$('matchDate').value;
  if(!oppId)return T('Select an opponent','error');
  const opp=S.players.find(p=>p.id===oppId);
  if(!opp)return T('Opponent not found','error');
  try{
    await addDoc(collection(db,'matches'),{
      playerAId:S.user.id,playerAName:S.user.name,
      playerBId:oppId,playerBName:opp.name,
      scoreA:sA,scoreB:sB,status:'pending',matchDate,
      createdAt:serverTimestamp(),submittedBy:S.user.id
    });
    const msg=isHigh(sA,sB)?`GOAL FEST! ${sA+sB} goals. Waiting for ${opp.name} to confirm.`:`Result submitted! Waiting for ${opp.name} to confirm.`;
    T(msg,'success');
    $('scoreA').value='';$('scoreB').value='';
    S.matches=[];
  }catch(e){T('Submit failed: '+e.message,'error');}
}

// ===== MOD PANEL =====
async function loadModPanel(){
  if(!S.user||!S.user.isModerator){
    $('modPendingMatches').innerHTML='<div class="empty-state"><div class="empty-icon">&#128683;</div><div class="empty-text">Moderator access required</div></div>';
    return;
  }
  try{
    const mSnap=await getDocs(query(collection(db,'matches'),where('status','==','pending'),orderBy('createdAt','desc'),limit(100)));
    const pending=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('modPendingMatches');
    if(!pending.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#10003;</div><div class="empty-text">No pending matches</div></div>';return;}
    el.innerHTML=pending.map(m=>`
      <div class="confirm-card">
        <div class="confirm-vs">
          <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">Player A</div></div>
          <div class="confirm-score-display">${m.scoreA}-${m.scoreB}</div>
          <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">Player B</div></div>
        </div>
        <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} - ${timeAgo(m.createdAt)}</div>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">Approve</button>
          <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">Dispute</button>
        </div>
      </div>`).join('');
  }catch(e){T('Error: '+e.message,'error');}
}

// ===== PROFILE =====
async function viewProfile(playerId){
  S.pageHistory.push('profile');showPage('profile');
  $('profileContent').innerHTML='<div class="loading-spinner"><div class="spinner"></div></div>';
  try{
    const [snap,mSnap]=await Promise.all([
      getDoc(doc(db,'players',playerId)),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(300)))
    ]);
    if(!snap.exists()){$('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Player not found</div></div>';return;}
    const p={id:snap.id,...snap.data()};
    const allM=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const myMatches=allM.filter(m=>(m.playerAId===playerId||m.playerBId===playerId)&&m.status==='confirmed');
    const recent=myMatches.slice(0,10);
    
    // Compute stats from match history
    let gf=0,ga=0,cs=0;
    myMatches.forEach(m=>{
      const side=m.playerAId===playerId?'A':'B';
      const my=side==='A'?m.scoreA:m.scoreB, op=side==='A'?m.scoreB:m.scoreA;
      gf+=my; ga+=op; if(op===0)cs++;
    });
    
    const w=p.wins||0,d=p.draws||0,l=p.losses||0;
    const total=w+d+l;
    const wr=total>0?Math.round(w/total*100):0;
    const gd=gf-ga;
    const rating=calcRatingFromStats(w,d,l,gf,ga,cs);
    
    const div=p.division||9;
    const rules=DIV_RULES[div];
    const cmp=p.cycleMP||0, cpts=p.cyclePts||0;
    const pct=Math.min(100,Math.round(cpts/(rules.promoPoints||1)*100));
    const remaining=Math.max(0,rules.cycle-cmp);
    
    const isRival=S.user&&(S.user.rivals||[]).includes(playerId);
    const isMe=S.user&&S.user.id===playerId;
    const badges=calcBadges(p,myMatches);
    const highest=p.highestDivision||div;
    
    const form=(p.form||[]).slice(-5);
    
    $('profileContent').innerHTML=`
      <div class="profile-header">
        <div class="profile-avatar">${p.name[0].toUpperCase()}</div>
        <div class="profile-info">
          <div class="profile-name">${p.name}</div>
          <span class="profile-cat">${p.category||'Youth'}</span>
          <div style="display:flex;align-items:center;gap:10px;margin-top:8px;flex-wrap:wrap">
            ${divBadge(div)}
            <span class="text-gray text-sm">Division ${div} - ${rules.name}</span>
            ${highest<div?`<span style="font-size:11px;color:#88CCFF">Best: Div ${highest}</span>`:''}
          </div>
          <div style="display:flex;gap:4px;margin-top:8px">
            ${form.map(r=>formBadge(r)).join('')}
          </div>
          <div class="badges-row">${badges.map(b=>`<span class="player-badge ${b.cls}">${b.text}</span>`).join('')}</div>
          ${!isMe&&S.user?`<button class="btn-sm ${isRival?'btn-reject':'btn-edit'} mt-8" onclick="toggleRival('${playerId}','${p.name}')">
            ${isRival?'Remove Rival':'Add Rival'}</button>`:''}
        </div>
      </div>
      
      <div class="profile-stats">
        <div class="p-stat"><div class="p-stat-val" style="color:#FF4444">${rating}</div><div class="p-stat-lbl">Rating</div></div>
        <div class="p-stat"><div class="p-stat-val text-green">${w}</div><div class="p-stat-lbl">Wins</div></div>
        <div class="p-stat"><div class="p-stat-val text-yellow">${d}</div><div class="p-stat-lbl">Draws</div></div>
        <div class="p-stat"><div class="p-stat-val text-red">${l}</div><div class="p-stat-lbl">Losses</div></div>
        <div class="p-stat"><div class="p-stat-val">${total}</div><div class="p-stat-lbl">Matches</div></div>
        <div class="p-stat"><div class="p-stat-val">${wr}%</div><div class="p-stat-lbl">Win Rate</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:${gd>=0?'#44FF88':'#FF6666'}">${gd>=0?'+':''}${gd}</div><div class="p-stat-lbl">Goal Diff</div></div>
        <div class="p-stat"><div class="p-stat-val">${cs}</div><div class="p-stat-lbl">Clean Sheets</div></div>
      </div>
      
      <div class="promo-tracker">
        <div class="promo-title">Division ${div} Cycle - Promotion Progress</div>
        <div class="promo-bar-wrap"><div class="promo-bar-fill" style="width:${pct}%"></div></div>
        <div class="promo-label"><span>${cpts} pts / ${rules.promoPoints} needed</span><span>${cmp}/10 matches</span></div>
        ${remaining>0?`<div class="promo-cycle-info">${remaining} matches remaining in this cycle</div>`:'<div class="promo-cycle-info" style="color:var(--green)">Cycle complete!</div>'}
      </div>
      
      <div class="section-title mt-16">Recent Matches</div>
      ${recent.length?recent.map(m=>{
        const side=m.playerAId===playerId?'A':'B';
        const res=getRC(m.scoreA,m.scoreB,side);
        const oppName=side==='A'?m.playerBName:m.playerAName;
        const oppId=side==='A'?m.playerBId:m.playerAId;
        const my=side==='A'?m.scoreA:m.scoreB, op=side==='A'?m.scoreB:m.scoreA;
        const hi=isHigh(m.scoreA,m.scoreB);
        return `<div class="match-card${hi?' high-score':''}">
          <div class="match-result-badge result-${res}">${res}</div>
          <div class="match-info">
            <div class="match-vs">vs <span class="player-link" style="display:inline" onclick="viewProfile('${oppId}')">${oppName}</span>${hi?' <span class="high-score-badge">GOAL FEST</span>':''}</div>
            <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} - ${statusBadge(m.status)}</div>
          </div>
          <div class="match-score">${my}-${op}</div>
        </div>`;
      }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>'}
    `;
  }catch(e){$('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Error loading profile</div></div>';console.error(e);}
}

async function loadMyProfile(){
  if(!S.user){
    $('myProfileContent').innerHTML='<div class="empty-state"><div class="empty-icon">&#128274;</div><div class="empty-text">Not logged in</div><button class="btn-primary mt-12" onclick="openModal(\'loginModal\')">Login</button></div>';
    return;
  }
  await viewProfile(S.user.id);
  $('myProfileContent').innerHTML=$('profileContent').innerHTML;
}

async function toggleRival(playerId,playerName){
  if(!S.user)return;
  const rivals=S.user.rivals||[];
  const nr=rivals.includes(playerId)?rivals.filter(r=>r!==playerId):[...rivals,playerId];
  await updateDoc(doc(db,'players',S.user.id),{rivals:nr});
  S.user.rivals=nr;
  T(rivals.includes(playerId)?playerName+' removed from rivals':playerName+' added as rival','success');
  viewProfile(playerId);
}

// ===== ADMIN =====
async function adminLogin(){
  const pw=$('adminPwInput').value;
  let stored=S.adminPw;
  try{const snap=await getDoc(doc(db,'settings','admin'));if(snap.exists()&&snap.data().password)stored=snap.data().password;}catch{}
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
    if(!pending.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#10003;</div><div class="empty-text">No pending registrations</div></div>';return;}
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
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()}));
    renderAdminPlayers(S.adminPlayers);
  }
  if(tab==='adminMatches'){
    const snap=await getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(100)));
    const matches=snap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('adminMatchesList');
    if(!matches.length){el.innerHTML='<div class="empty-state"><div class="empty-text">No matches</div></div>';return;}
    el.innerHTML=matches.map(m=>{
      const hi=isHigh(m.scoreA,m.scoreB);
      return `<div class="pending-item${hi?' high-score':''}">
        <div class="pending-info">
          <div class="pending-name">${m.playerAName} ${m.scoreA}-${m.scoreB} ${m.playerBName}${hi?' [GOAL FEST]':''}</div>
          <div class="pending-meta">${fmtDate(m.createdAt)} - ${statusBadge(m.status)}</div>
        </div>
        <div style="display:flex;gap:5px;flex-wrap:wrap">
          ${m.status==='pending'?`<button class="btn-sm btn-approve" onclick="adminConfirmMatch('${m.id}')">Confirm</button>`:''}
          <button class="btn-sm btn-edit" onclick="adminEditMatch('${m.id}','${m.playerAName}','${m.playerBName}',${m.scoreA},${m.scoreB},'${m.status}')">Edit</button>
          <button class="btn-sm btn-reject" onclick="adminDeleteMatchDirect('${m.id}')">Delete</button>
        </div>
      </div>`;
    }).join('');
  }
  if(tab==='moderators'){
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    renderModPlayers(S.adminPlayers);
  }
  if(tab==='season'){
    // Load season settings
    try{
      const snap=await getDoc(doc(db,'settings','season'));
      if(snap.exists()){
        const sd=snap.data();
        if(sd.duration)$('seasonDuration').value=sd.duration;
        if(sd.startDate)$('seasonStart').value=sd.startDate;
      }
    }catch{}
  }
}

async function saveSeasonSettings(){
  const duration=parseInt($('seasonDuration').value)||30;
  const startDate=$('seasonStart').value;
  try{
    await setDoc(doc(db,'settings','season'),{duration,startDate},{merge:true});
    T('Season settings saved','success');
  }catch(e){T('Error: '+e.message,'error');}
}

function renderAdminPlayers(players){
  const search=($('adminPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  $('adminPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name}${p.status==='banned'?' [BANNED]':p.status==='pending'?' [PENDING]':''}${p.isModerator?' [MOD]':''}</div>
        <div class="pending-meta">${p.category||'Youth'} - Div${p.division||9} - Rating:${calcRatingFromStats(p.wins||0,p.draws||0,p.losses||0,p.goalsFor||0,p.goalsAgainst||0,p.cleanSheets||0)} - ${p.wins||0}W ${p.draws||0}D ${p.losses||0}L - Cycle:${p.cycleMP||0}/10 (${p.cyclePts||0}pts) - ${statusBadge(p.status||'active')}</div>
      </div>
      <div style="display:flex;gap:5px;flex-wrap:wrap">
        <button class="btn-sm btn-edit" onclick="adminEditPlayer('${p.id}',${p.division||9},0,${p.wins||0},${p.draws||0},${p.losses||0},${p.goalsFor||0},${p.goalsAgainst||0},${p.cycleMP||0},${p.cyclePts||0},'${p.status||'active'}')">Edit</button>
        <button class="btn-sm btn-ban" onclick="adminToggleBan('${p.id}','${p.name}','${p.status||'active'}')">
          ${p.status==='banned'?'Unban':'Ban'}</button>
        <button class="btn-sm ${p.isPOTW?'btn-reject':'btn-edit'}" onclick="adminTogglePOTW('${p.id}','${p.name}',${!!p.isPOTW})" style="${p.isPOTW?'':''}">
          ${p.isPOTW?'Remove POTW':'Set POTW'}</button>
        <button class="btn-sm ${p.isPOTM?'btn-reject':'btn-mod'}" onclick="adminTogglePOTM('${p.id}','${p.name}',${!!p.isPOTM})">
          ${p.isPOTM?'Remove POTM':'Set POTM'}</button>
        <button class="btn-sm ${p.isPOTD?'btn-reject':'btn-approve'}" onclick="adminTogglePOTD('${p.id}','${p.name}',${!!p.isPOTD})">
          ${p.isPOTD?'Remove POTD':'Set POTD'}</button>
        <button class="btn-sm ${p.isPOTS?'btn-reject':'btn-ban'}" onclick="adminTogglePOTS('${p.id}','${p.name}',${!!p.isPOTS})">
          ${p.isPOTS?'Remove POTS':'Set POTS'}</button>
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
        <div class="pending-name">${p.name}${p.isModerator?' [MODERATOR]':''}</div>
        <div class="pending-meta">${p.category||'Youth'} - ${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
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

async function adminTogglePOTW(id,name,cur){await updateDoc(doc(db,'players',id),{isPOTW:!cur});T(name+(!cur?' is now POTW':'POTW removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTM(id,name,cur){await updateDoc(doc(db,'players',id),{isPOTM:!cur});T(name+(!cur?' is now POTM':'POTM removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTD(id,name,cur){await updateDoc(doc(db,'players',id),{isPOTD:!cur});T(name+(!cur?' is now POTD':'POTD removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTS(id,name,cur){await updateDoc(doc(db,'players',id),{isPOTS:!cur});T(name+(!cur?' is now Player of the Season':'POTS removed'),'success');loadAdminPanel('players');}

async function adminApprove(id){
  await updateDoc(doc(db,'players',id),{status:'active'});
  T('Player approved','success');loadAdminPanel('pending');
}
async function adminReject(id){
  if(!confirm('Reject and delete this registration?'))return;
  await deleteDoc(doc(db,'players',id));T('Rejected','info');loadAdminPanel('pending');
}

function adminEditPlayer(id,div,pts,wins,draws,losses,gf,ga,cmp,cpts,status){
  $('editPlayerId').value=id;$('editDivision').value=div;$('editPoints').value=pts;
  $('editWins').value=wins;$('editDraws').value=draws;$('editLosses').value=losses;
  $('editGF').value=gf;$('editGA').value=ga;$('editCycleMP').value=cmp;$('editCyclePts').value=cpts;
  $('editStatus').value=status;openModal('editPlayerModal');
}

async function savePlayerEdit(){
  const id=$('editPlayerId').value,div=parseInt($('editDivision').value);
  const wins=parseInt($('editWins').value),draws=parseInt($('editDraws').value),losses=parseInt($('editLosses').value);
  const gf=parseInt($('editGF').value),ga=parseInt($('editGA').value);
  const cmp=parseInt($('editCycleMP').value),cpts=parseInt($('editCyclePts').value);
  const status=$('editStatus').value;
  if(div<1||div>9)return T('Division 1-9 only','error');
  try{
    await updateDoc(doc(db,'players',id),{division:div,wins,draws,losses,goalsFor:gf,goalsAgainst:ga,cycleMP:cmp,cyclePts:cpts,status});
    T('Player updated','success');closeModal('editPlayerModal');loadAdminPanel('players');
  }catch(e){T('Error: '+e.message,'error');}
}

async function adminToggleBan(id,name,cs){
  const ns=cs==='banned'?'active':'banned';
  await updateDoc(doc(db,'players',id),{status:ns});
  T(name+' '+ns,'info');loadAdminPanel('players');
}

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
    await updateDoc(doc(db,'matches',id),{scoreA:sA,scoreB:sB,status});
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
  T('Match deleted','info');S.matches=[];loadAdminPanel('adminMatches');
}

async function confirmSeasonReset(){
  if(!confirm('RESET ENTIRE SEASON?\n\nAll matches deleted, all stats reset. Player accounts remain.\n\nPress OK to confirm.'))return;
  try{
    const [pSnap,mSnap]=await Promise.all([getDocs(collection(db,'players')),getDocs(collection(db,'matches'))]);
    await Promise.all([
      ...pSnap.docs.map(d=>updateDoc(doc(db,'players',d.id),{
        wins:0,draws:0,losses:0,goalsFor:0,goalsAgainst:0,cleanSheets:0,
        form:[],division:9,cycleMP:0,cyclePts:0,highestDivision:9
      })),
      ...mSnap.docs.map(d=>deleteDoc(doc(db,'matches',d.id)))
    ]);
    S.players=[];S.matches=[];T('Season reset complete!','success');
  }catch(e){T('Error: '+e.message,'error');}
}

async function changeAdminPassword(){
  const pw=$('newAdminPw').value,pw2=$('confirmAdminPw').value;
  if(!pw||pw.length<4)return T('Password too short','error');
  if(pw!==pw2)return T('Passwords do not match','error');
  try{
    await setDoc(doc(db,'settings','admin'),{password:pw},{merge:true});
    S.adminPw=pw;T('Admin password updated','success');
    $('newAdminPw').value='';$('confirmAdminPw').value='';
  }catch(e){T('Error: '+e.message,'error');}
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
  navTo,navBack,setNavActive,setMobActive,
  openModal,closeModal,
  doLogin,doRegister,doLogout,
  switchLbTab,filterLeaderboard,
  filterMatches,confirmMatch,
  submitMatchResult,loadSubmitPage,
  viewProfile,toggleRival,loadMyProfile,
  openRankingCardPreview,closeRankingPreview,downloadRankingCard,
  adminLogin,loadAdminPanel,switchAdminTab,
  adminApprove,adminReject,adminEditPlayer,savePlayerEdit,
  adminToggleBan,adminToggleMod,
  adminTogglePOTW,adminTogglePOTM,adminTogglePOTD,adminTogglePOTS,
  adminEditMatch,saveMatchEdit,adminDeleteMatch,adminDeleteMatchDirect,
  adminConfirmMatch,filterAdminPlayers,filterModPlayers,
  confirmSeasonReset,changeAdminPassword,loadModPanel,saveSeasonSettings
});

// ===== INIT =====
updateHeaderAuth();
loadHome();
document.querySelectorAll('.modal-overlay').forEach(m=>{
  m.addEventListener('click',e=>{if(e.target===m)m.classList.remove('open');});
});
</script>
</body>
</html>
