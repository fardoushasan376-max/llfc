
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LLFC Juvenile Division System</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@400;500;600;700&family=Barlow+Condensed:ital,wght@0,400;0,600;0,700;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --red:#CC0000; --red-bright:#FF1A1A; --red-dark:#8B0000; --red-deeper:#5C0000;
  --white:#FFFFFF; --gray-mid:#C8B0B0; --gray-dark:#4A3535;
  --black:#0A0000; --card-bg:#1A0A0A; --card-border:rgba(204,0,0,0.3);
  --gold:#FFD700; --silver:#C0C0C0; --bronze:#CD7F32;
  --green:#00CC44; --yellow:#FFAA00; --blue:#4499FF; --purple:#AA44FF;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'Rajdhani',sans-serif;background:var(--black);color:var(--white);min-height:100vh;overflow-x:hidden;}
body::before{content:'';position:fixed;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 80px,rgba(204,0,0,0.025) 80px,rgba(204,0,0,0.025) 81px),repeating-linear-gradient(90deg,transparent,transparent 80px,rgba(204,0,0,0.025) 80px,rgba(204,0,0,0.025) 81px);pointer-events:none;z-index:0;}

/* HEADER */
header{position:sticky;top:0;z-index:1000;background:rgba(10,0,0,0.97);backdrop-filter:blur(10px);border-bottom:2px solid var(--red);box-shadow:0 4px 30px rgba(204,0,0,0.3);}
.header-inner{max-width:1400px;margin:0 auto;padding:0 16px;display:flex;align-items:center;justify-content:space-between;height:60px;gap:8px;}
.logo-area{display:flex;align-items:center;gap:10px;cursor:pointer;flex-shrink:0;}
.logo-badge{width:42px;height:42px;background:var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:20px;box-shadow:0 0 15px rgba(204,0,0,0.6);flex-shrink:0;}
.logo-text{display:flex;flex-direction:column;line-height:1;}
.logo-main{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:2px;}
.logo-sub{font-size:10px;color:var(--red-bright);letter-spacing:3px;text-transform:uppercase;font-weight:600;}
.header-nav{display:flex;gap:4px;align-items:center;}
.nav-btn{background:none;border:1px solid transparent;color:var(--gray-mid);padding:6px 12px;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:13px;letter-spacing:1px;cursor:pointer;border-radius:4px;transition:all 0.2s;text-transform:uppercase;}
.nav-btn:hover,.nav-btn.active{color:var(--white);border-color:var(--red);background:rgba(204,0,0,0.15);}
.header-auth{display:flex;gap:6px;align-items:center;flex-shrink:0;}
.btn-login{background:transparent;border:1px solid var(--red);color:var(--red-bright);padding:6px 14px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:13px;letter-spacing:1px;cursor:pointer;border-radius:3px;transition:all 0.2s;text-transform:uppercase;}
.btn-login:hover{background:var(--red);color:white;}
.btn-register{background:var(--red);border:1px solid var(--red);color:white;padding:6px 14px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:13px;letter-spacing:1px;cursor:pointer;border-radius:3px;transition:all 0.2s;text-transform:uppercase;}
.btn-register:hover{background:var(--red-bright);}
.user-pill{display:flex;align-items:center;gap:8px;background:rgba(204,0,0,0.15);border:1px solid var(--red);border-radius:20px;padding:4px 12px 4px 4px;cursor:pointer;}
.user-avatar{width:28px;height:28px;background:var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;flex-shrink:0;}
.user-name{font-size:13px;font-weight:600;}
.mod-badge{font-size:9px;background:rgba(170,68,255,0.3);border:1px solid var(--purple);color:var(--purple);padding:1px 5px;border-radius:3px;letter-spacing:1px;}

/* MAIN */
main{position:relative;z-index:1;max-width:1400px;margin:0 auto;padding:20px 16px;min-height:calc(100vh - 60px);}
.page{display:none;}.page.active{display:block;}

/* CARDS */
.card{background:var(--card-bg);border:1px solid var(--card-border);border-radius:8px;padding:20px;}
.card-red{background:linear-gradient(135deg,rgba(204,0,0,0.2),rgba(10,0,0,0.9));border:1px solid var(--red);}

/* SECTION TITLE */
.section-title{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:3px;color:var(--white);display:flex;align-items:center;gap:12px;margin-bottom:16px;}
.section-title::after{content:'';flex:1;height:2px;background:linear-gradient(90deg,var(--red),transparent);}

/* HERO */
.hero{background:linear-gradient(135deg,rgba(139,0,0,0.35) 0%,rgba(10,0,0,0.85) 60%);border:1px solid var(--red);border-radius:12px;padding:36px 28px;margin-bottom:20px;position:relative;overflow:hidden;}
.hero::before{content:'LLFC';position:absolute;right:-10px;top:-10px;font-family:'Bebas Neue',sans-serif;font-size:180px;color:rgba(204,0,0,0.05);letter-spacing:10px;line-height:1;pointer-events:none;}
.hero-tag{display:inline-block;background:var(--red);color:white;font-size:11px;font-weight:700;letter-spacing:3px;padding:3px 10px;border-radius:2px;margin-bottom:10px;text-transform:uppercase;}
.hero h1{font-family:'Bebas Neue',sans-serif;font-size:clamp(32px,5vw,64px);letter-spacing:4px;line-height:1;margin-bottom:10px;}
.hero h1 span{color:var(--red-bright);}
.hero p{color:var(--gray-mid);font-size:15px;max-width:500px;margin-bottom:20px;line-height:1.5;}
.hero-actions{display:flex;gap:10px;flex-wrap:wrap;}

/* BUTTONS */
.btn-primary{background:var(--red);color:white;border:none;padding:11px 26px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:14px;letter-spacing:2px;cursor:pointer;border-radius:4px;text-transform:uppercase;transition:all 0.2s;box-shadow:0 4px 15px rgba(204,0,0,0.3);}
.btn-primary:hover{background:var(--red-bright);box-shadow:0 4px 25px rgba(255,26,26,0.5);transform:translateY(-1px);}
.btn-secondary{background:transparent;color:var(--white);border:1px solid rgba(255,255,255,0.25);padding:11px 26px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:14px;letter-spacing:2px;cursor:pointer;border-radius:4px;text-transform:uppercase;transition:all 0.2s;}
.btn-secondary:hover{border-color:var(--red);background:rgba(204,0,0,0.1);}
.btn-sm{padding:5px 12px;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:12px;letter-spacing:1px;cursor:pointer;border-radius:3px;transition:all 0.2s;text-transform:uppercase;}
.btn-approve{background:rgba(0,204,68,0.2);color:var(--green);border:1px solid rgba(0,204,68,0.4);}
.btn-approve:hover{background:var(--green);color:#000;}
.btn-reject{background:rgba(204,0,0,0.2);color:var(--red-bright);border:1px solid var(--red);}
.btn-reject:hover{background:var(--red);color:white;}
.btn-edit{background:rgba(255,170,0,0.15);color:var(--yellow);border:1px solid rgba(255,170,0,0.4);}
.btn-edit:hover{background:rgba(255,170,0,0.3);}
.btn-ban{background:rgba(80,0,80,0.3);color:#cc88ff;border:1px solid rgba(150,0,150,0.4);}
.btn-ban:hover{background:rgba(150,0,150,0.4);}
.btn-mod{background:rgba(68,153,255,0.15);color:var(--blue);border:1px solid rgba(68,153,255,0.4);}
.btn-mod:hover{background:rgba(68,153,255,0.3);}

/* STATS GRID */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:12px;margin-bottom:20px;}
.stat-card{background:var(--card-bg);border:1px solid var(--card-border);border-radius:8px;padding:14px;text-align:center;transition:border-color 0.2s;}
.stat-card:hover{border-color:var(--red);}
.stat-num{font-family:'Bebas Neue',sans-serif;font-size:34px;color:var(--red-bright);line-height:1;}
.stat-label{font-size:11px;color:var(--gray-mid);letter-spacing:2px;text-transform:uppercase;margin-top:4px;}

/* GRID */
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:20px;}
.three-col{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;}
@media(max-width:900px){.two-col{grid-template-columns:1fr;}.three-col{grid-template-columns:1fr 1fr;}.header-nav{display:none;}}
@media(max-width:500px){.three-col{grid-template-columns:1fr;}}

/* DIV BADGE */
.div-badge{display:inline-flex;align-items:center;justify-content:center;width:30px;height:30px;border-radius:50%;font-weight:700;font-size:13px;flex-shrink:0;}
.div-1{background:linear-gradient(135deg,#FFD700,#FF8C00);color:#000;}
.div-2{background:linear-gradient(135deg,#C0C0C0,#808080);color:#000;}
.div-3{background:linear-gradient(135deg,#CD7F32,#8B4513);color:#fff;}
.div-4{background:rgba(204,0,0,0.8);color:#fff;border:1px solid var(--red);}
.div-5{background:rgba(204,0,0,0.55);color:#fff;border:1px solid rgba(204,0,0,0.5);}
.div-6{background:rgba(120,0,0,0.6);color:#ddd;}
.div-7{background:rgba(70,0,0,0.7);color:#bbb;}
.div-8{background:rgba(40,0,0,0.7);color:#999;}
.div-9{background:rgba(25,15,15,0.9);color:#666;border:1px solid #333;}

/* LB TABS */
.lb-tabs{display:flex;gap:4px;margin-bottom:16px;background:rgba(204,0,0,0.05);border:1px solid var(--card-border);border-radius:8px;padding:4px;flex-wrap:wrap;}
.lb-tab{flex:1;min-width:70px;background:none;border:none;color:var(--gray-mid);padding:8px 10px;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:13px;letter-spacing:1px;cursor:pointer;border-radius:5px;transition:all 0.2s;text-transform:uppercase;}
.lb-tab.active{background:var(--red);color:white;}

/* RANKING TABLE */
.lb-table-wrap{overflow-x:auto;border-radius:8px;border:1px solid var(--card-border);}
table{width:100%;border-collapse:collapse;}
thead tr{background:rgba(204,0,0,0.18);border-bottom:2px solid var(--red);}
thead th{padding:11px 12px;text-align:left;font-size:11px;letter-spacing:2px;text-transform:uppercase;color:var(--gray-mid);font-weight:600;white-space:nowrap;}
tbody tr{border-bottom:1px solid rgba(204,0,0,0.08);transition:background 0.15s;}
tbody tr:hover{background:rgba(204,0,0,0.07);}
tbody tr:last-child{border-bottom:none;}
tbody td{padding:10px 12px;font-size:14px;font-weight:500;vertical-align:middle;}
tbody tr.top-1{background:linear-gradient(90deg,rgba(255,215,0,0.08),transparent);}
tbody tr.top-2{background:linear-gradient(90deg,rgba(192,192,192,0.06),transparent);}
tbody tr.top-3{background:linear-gradient(90deg,rgba(205,127,50,0.06),transparent);}
.rank-num{font-family:'Bebas Neue',sans-serif;font-size:22px;color:var(--gray-mid);}
.rank-1{color:var(--gold);}.rank-2{color:var(--silver);}.rank-3{color:var(--bronze);}

/* WDL PILLS - enhanced focus */
.wdl-row{display:flex;align-items:center;gap:5px;}
.wdl-pill{display:inline-flex;align-items:center;gap:3px;padding:4px 9px;border-radius:4px;font-size:12px;font-weight:700;letter-spacing:0.5px;white-space:nowrap;}
.wdl-w{background:rgba(0,204,68,0.18);color:var(--green);border:1px solid rgba(0,204,68,0.3);}
.wdl-d{background:rgba(255,170,0,0.18);color:var(--yellow);border:1px solid rgba(255,170,0,0.3);}
.wdl-l{background:rgba(204,0,0,0.18);color:var(--red-bright);border:1px solid rgba(204,0,0,0.3);}
.wdl-num{font-family:'Bebas Neue',sans-serif;font-size:17px;line-height:1;}

/* WINRATE */
.winrate-wrap{display:flex;align-items:center;gap:6px;}
.winrate-bar{position:relative;background:rgba(255,255,255,0.08);border-radius:10px;height:6px;width:55px;overflow:hidden;flex-shrink:0;}
.winrate-fill{position:absolute;left:0;top:0;bottom:0;background:linear-gradient(90deg,var(--red),var(--red-bright));border-radius:10px;}
.winrate-pct{font-size:12px;font-weight:700;color:var(--gray-mid);white-space:nowrap;}

/* FORM */
.form-dots{display:flex;gap:3px;align-items:center;}
.form-dot{width:9px;height:9px;border-radius:50%;}
.form-w{background:var(--green);}.form-d{background:var(--yellow);}.form-l{background:var(--red);}

/* PLAYER LINK */
.player-link{cursor:pointer;color:var(--white);font-weight:600;transition:color 0.2s;display:inline-flex;align-items:center;gap:6px;}
.player-link:hover{color:var(--red-bright);}
.rating-val{font-family:'Bebas Neue',sans-serif;font-size:20px;color:var(--red-bright);}

/* STATUS BADGE */
.status-badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;}
.status-confirmed{background:rgba(0,204,68,0.2);color:var(--green);border:1px solid rgba(0,204,68,0.3);}
.status-pending{background:rgba(255,170,0,0.2);color:var(--yellow);border:1px solid rgba(255,170,0,0.3);}
.status-disputed{background:rgba(204,0,0,0.2);color:var(--red-bright);border:1px solid rgba(204,0,0,0.3);}

/* SEARCH */
.search-bar{display:flex;gap:8px;margin-bottom:14px;}
.search-input{flex:1;background:rgba(255,255,255,0.05);border:1px solid rgba(204,0,0,0.3);border-radius:5px;color:var(--white);padding:9px 13px;font-family:'Rajdhani',sans-serif;font-size:14px;}
.search-input:focus{outline:none;border-color:var(--red);}
.search-input::placeholder{color:var(--gray-mid);}

/* FORM INPUTS */
.match-form{display:grid;gap:14px;}
.form-group{display:flex;flex-direction:column;gap:5px;}
.form-label{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--gray-mid);}
.form-input,.form-select{background:rgba(255,255,255,0.05);border:1px solid rgba(204,0,0,0.3);border-radius:5px;color:var(--white);padding:9px 13px;font-family:'Rajdhani',sans-serif;font-size:15px;font-weight:500;transition:border-color 0.2s;width:100%;}
.form-input:focus,.form-select:focus{outline:none;border-color:var(--red);background:rgba(204,0,0,0.08);}
.form-select option{background:#1A0A0A;color:white;}
.score-row{display:grid;grid-template-columns:1fr auto 1fr;gap:10px;align-items:center;}
.score-vs{font-family:'Bebas Neue',sans-serif;font-size:22px;color:var(--red);text-align:center;}
.score-input{text-align:center;font-size:28px;font-family:'Bebas Neue',sans-serif;padding:10px;}

/* MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.85);z-index:2000;display:none;align-items:center;justify-content:center;padding:16px;backdrop-filter:blur(4px);}
.modal-overlay.open{display:flex;}
.modal{background:#140000;border:1px solid var(--red);border-radius:10px;padding:26px;width:100%;max-width:480px;max-height:90vh;overflow-y:auto;position:relative;}
.modal-title{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:3px;color:var(--white);margin-bottom:18px;}
.modal-close{position:absolute;top:14px;right:14px;background:rgba(204,0,0,0.2);border:1px solid var(--red);color:var(--red-bright);width:28px;height:28px;border-radius:50%;font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all 0.2s;}
.modal-close:hover{background:var(--red);color:white;}

/* TOAST */
.toast{position:fixed;bottom:24px;right:24px;z-index:9999;background:var(--card-bg);border-left:4px solid var(--red);border-radius:6px;padding:12px 18px;min-width:240px;max-width:360px;box-shadow:0 8px 30px rgba(0,0,0,0.5);transform:translateX(120%);transition:transform 0.3s;font-weight:600;font-size:14px;}
.toast.show{transform:translateX(0);}
.toast.success{border-color:var(--green);}
.toast.error{border-color:var(--red-bright);}
.toast.info{border-color:var(--yellow);}

/* NEWS TICKER */
.news-ticker{background:rgba(204,0,0,0.1);border:1px solid rgba(204,0,0,0.35);border-radius:6px;margin-bottom:16px;overflow:hidden;display:flex;align-items:center;}
.news-label{background:var(--red);color:white;padding:8px 14px;font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:2px;flex-shrink:0;white-space:nowrap;}
.news-scroll-wrap{overflow:hidden;flex:1;padding:8px 14px;}
.news-scroll-text{font-size:13px;font-weight:600;color:var(--gold);white-space:nowrap;display:inline-block;animation:scrollNews 20s linear infinite;}
@keyframes scrollNews{0%{transform:translateX(100vw);}100%{transform:translateX(-100%);}}

/* MATCH CARD */
.match-card{background:var(--card-bg);border:1px solid var(--card-border);border-radius:6px;padding:12px 14px;margin-bottom:8px;display:flex;align-items:center;gap:10px;transition:border-color 0.2s;}
.match-card:hover{border-color:var(--red);}
.match-card.high-score{border-color:rgba(255,215,0,0.5);background:linear-gradient(135deg,rgba(255,215,0,0.05),var(--card-bg));}
.match-result-badge{width:34px;height:34px;border-radius:4px;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:16px;font-weight:700;flex-shrink:0;}
.result-W{background:rgba(0,204,68,0.2);color:var(--green);border:1px solid var(--green);}
.result-D{background:rgba(255,170,0,0.2);color:var(--yellow);border:1px solid var(--yellow);}
.result-L{background:rgba(204,0,0,0.2);color:var(--red-bright);border:1px solid var(--red);}
.match-info{flex:1;min-width:0;}
.match-vs{font-size:14px;font-weight:600;}
.match-meta{font-size:11px;color:var(--gray-mid);margin-top:2px;}
.match-score{font-family:'Bebas Neue',sans-serif;font-size:24px;color:var(--white);text-align:right;flex-shrink:0;}
.high-score-badge{background:rgba(255,215,0,0.2);color:var(--gold);border:1px solid rgba(255,215,0,0.4);border-radius:3px;font-size:10px;font-weight:700;padding:1px 6px;letter-spacing:1px;white-space:nowrap;}

/* PENDING ITEMS */
.pending-item{background:var(--card-bg);border:1px solid var(--card-border);border-radius:6px;padding:12px 14px;margin-bottom:8px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
.pending-info{flex:1;min-width:120px;}
.pending-name{font-size:15px;font-weight:700;}
.pending-meta{font-size:11px;color:var(--gray-mid);}

/* CONFIRM CARD */
.confirm-card{background:linear-gradient(135deg,rgba(204,0,0,0.1),var(--card-bg));border:1px solid var(--red);border-radius:8px;padding:14px;margin-bottom:10px;}
.confirm-vs{display:flex;align-items:center;justify-content:space-between;gap:8px;margin-bottom:10px;flex-wrap:wrap;}
.confirm-player{text-align:center;flex:1;}
.confirm-player-name{font-size:15px;font-weight:700;}
.confirm-score-display{font-family:'Bebas Neue',sans-serif;font-size:34px;color:var(--red-bright);padding:0 12px;flex-shrink:0;}

/* PROFILE */
.profile-header{display:flex;gap:20px;align-items:flex-start;flex-wrap:wrap;margin-bottom:20px;}
.profile-avatar{width:76px;height:76px;background:var(--red-dark);border:3px solid var(--red);border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:30px;color:white;flex-shrink:0;box-shadow:0 0 20px rgba(204,0,0,0.4);}
.profile-info{flex:1;}
.profile-name{font-family:'Bebas Neue',sans-serif;font-size:34px;letter-spacing:3px;line-height:1;}
.profile-cat{display:inline-block;background:rgba(204,0,0,0.2);border:1px solid var(--red);color:var(--red-bright);font-size:11px;font-weight:700;letter-spacing:2px;padding:2px 8px;border-radius:2px;margin-top:4px;text-transform:uppercase;}
.profile-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(95px,1fr));gap:10px;margin-bottom:20px;}
.p-stat{background:var(--card-bg);border:1px solid var(--card-border);border-radius:6px;padding:12px;text-align:center;}
.p-stat-val{font-family:'Bebas Neue',sans-serif;font-size:28px;line-height:1;}
.p-stat-lbl{font-size:10px;color:var(--gray-mid);letter-spacing:1.5px;text-transform:uppercase;}

/* PROMO */
.promo-tracker{background:var(--card-bg);border:1px solid var(--card-border);border-radius:8px;padding:14px;margin-top:14px;}
.promo-title{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--gray-mid);margin-bottom:8px;}
.promo-bar-wrap{background:rgba(255,255,255,0.08);border-radius:6px;height:9px;margin-bottom:5px;overflow:hidden;}
.promo-bar-fill{height:100%;background:linear-gradient(90deg,var(--red),var(--red-bright));border-radius:6px;transition:width 0.5s;}
.promo-label{font-size:12px;color:var(--gray-mid);display:flex;justify-content:space-between;}

/* ADMIN TABS */
.admin-tabs{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:18px;border-bottom:2px solid var(--red);padding-bottom:8px;}
.admin-tab{background:none;border:1px solid transparent;color:var(--gray-mid);padding:6px 13px;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:12px;letter-spacing:1px;cursor:pointer;border-radius:4px;transition:all 0.2s;text-transform:uppercase;}
.admin-tab.active{background:var(--red);color:white;border-color:var(--red);}
.admin-tab:hover:not(.active){border-color:var(--red);color:white;}

/* MOD INFO */
.mod-panel-info{background:rgba(68,153,255,0.08);border:1px solid rgba(68,153,255,0.3);border-radius:8px;padding:14px;margin-bottom:16px;}
.mod-panel-title{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:2px;color:var(--blue);margin-bottom:6px;}

/* MOBILE NAV */
.mobile-nav{display:none;position:fixed;bottom:0;left:0;right:0;background:rgba(10,0,0,0.98);border-top:2px solid var(--red);z-index:999;padding:6px 0;}
.mobile-nav-inner{display:flex;justify-content:space-around;}
.mob-nav-btn{display:flex;flex-direction:column;align-items:center;gap:2px;background:none;border:none;color:var(--gray-mid);font-family:'Rajdhani',sans-serif;font-size:10px;font-weight:600;letter-spacing:1px;padding:4px 10px;cursor:pointer;transition:color 0.2s;text-transform:uppercase;}
.mob-nav-btn.active,.mob-nav-btn:hover{color:var(--red-bright);}
.mob-nav-icon{font-size:18px;}
@media(max-width:768px){.mobile-nav{display:block;}main{padding-bottom:72px;}}

/* MISC */
.loading-spinner{display:flex;align-items:center;justify-content:center;padding:40px;gap:12px;color:var(--gray-mid);}
.spinner{width:24px;height:24px;border:2px solid rgba(204,0,0,0.2);border-top-color:var(--red);border-radius:50%;animation:spin 0.7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.empty-state{text-align:center;padding:40px 20px;color:var(--gray-mid);}
.empty-icon{font-size:44px;margin-bottom:10px;}
.empty-text{font-size:17px;font-weight:600;}
.empty-sub{font-size:13px;margin-top:5px;opacity:0.6;}
.text-red{color:var(--red-bright);}.text-green{color:var(--green);}.text-yellow{color:var(--yellow);}
.text-gold{color:var(--gold);}.text-blue{color:var(--blue);}.text-purple{color:var(--purple);}
.text-gray{color:var(--gray-mid);}.text-sm{font-size:13px;}.font-bold{font-weight:700;}.w-full{width:100%;}
.mt-8{margin-top:8px;}.mt-12{margin-top:12px;}.mt-16{margin-top:16px;}.mb-8{margin-bottom:8px;}.mb-16{margin-bottom:16px;}
.flex{display:flex;}.gap-6{gap:6px;}.gap-8{gap:8px;}.items-center{align-items:center;}.justify-between{justify-content:space-between;}.flex-wrap{flex-wrap:wrap;}
</style>
</head>
<body>

<header>
  <div class="header-inner">
    <div class="logo-area" onclick="navTo('home')">
      <div class="logo-badge">⚽</div>
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
    <div class="news-label">🔥 NEWS</div>
    <div class="news-scroll-wrap"><span class="news-scroll-text" id="newsText"></span></div>
  </div>
  <div class="hero">
    <div class="hero-tag">🏆 Season Active</div>
    <h1>LLFC <span>Juvenile</span> Division</h1>
    <p>Play freely. Submit results. Climb the ranks. From Division 9 to Division 1 — prove your worth on the pitch.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="navTo('leaderboard')">🏆 View Rankings</button>
      <button class="btn-secondary" onclick="navTo('submit')">📝 Submit Result</button>
    </div>
  </div>
  <div class="stats-grid">
    <div class="stat-card"><div class="stat-num" id="statPlayers">—</div><div class="stat-label">Active Players</div></div>
    <div class="stat-card"><div class="stat-num" id="statMatches">—</div><div class="stat-label">Total Matches</div></div>
    <div class="stat-card"><div class="stat-num" id="statToday">—</div><div class="stat-label">Today's Matches</div></div>
    <div class="stat-card"><div class="stat-num" id="statPending">—</div><div class="stat-label">Pending Confirms</div></div>
  </div>
  <div class="two-col">
    <div>
      <div class="section-title">🔥 Top Players</div>
      <div id="homeTopPlayers"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
    <div>
      <div class="section-title">⚽ Recent Matches</div>
      <div id="homeRecentMatches"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
  </div>
  <div class="mt-16">
    <div class="section-title">📋 Division Guide</div>
    <div class="three-col" id="divisionGuide"></div>
  </div>
</div>

<!-- LEADERBOARD -->
<div class="page" id="page-leaderboard">
  <div class="section-title">🏆 Leaderboards</div>
  <div class="lb-tabs">
    <button class="lb-tab active" onclick="switchLbTab('overall',this)">🏆 Overall</button>
    <button class="lb-tab" onclick="switchLbTab('monthly',this)">🔵 Monthly</button>
    <button class="lb-tab" onclick="switchLbTab('weekly',this)">🟡 Weekly</button>
    <button class="lb-tab" onclick="switchLbTab('daily',this)">🟢 Daily</button>
  </div>
  <div class="search-bar">
    <input class="search-input" placeholder="🔍 Search player..." id="lbSearch" oninput="filterLeaderboard()">
    <select class="form-select" style="width:130px" id="lbDivFilter" onchange="filterLeaderboard()">
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
          <th style="width:42px">#</th>
          <th>Player</th>
          <th>Div</th>
          <th>Rating</th>
          <th>Pts</th>
          <th>W / D / L</th>
          <th>MP</th>
          <th>Win%</th>
          <th>Form</th>
        </tr>
      </thead>
      <tbody id="lbTableBody">
        <tr><td colspan="9" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- MATCHES -->
<div class="page" id="page-matches">
  <div class="section-title">⚽ Match History</div>
  <div class="search-bar">
    <input class="search-input" placeholder="🔍 Search by player..." id="matchSearch" oninput="filterMatches()">
    <select class="form-select" style="width:130px" id="matchStatusFilter" onchange="filterMatches()">
      <option value="">All</option>
      <option value="confirmed">Confirmed</option>
      <option value="pending">Pending</option>
      <option value="disputed">Disputed</option>
    </select>
  </div>
  <div id="matchesList"><div class="loading-spinner"><div class="spinner"></div></div></div>
  <div id="pendingConfirmSection" style="display:none">
    <div class="section-title mt-16">⏳ Awaiting Confirmation</div>
    <div id="pendingConfirmList"></div>
  </div>
</div>

<!-- SUBMIT -->
<div class="page" id="page-submit">
  <div class="section-title">📝 Submit Match Result</div>
  <div id="submitRequireLogin" style="display:none">
    <div class="empty-state">
      <div class="empty-icon">🔒</div>
      <div class="empty-text">Login Required</div>
      <div class="empty-sub">Please login to submit match results</div>
      <button class="btn-primary mt-12" onclick="openModal('loginModal')">Login Now</button>
    </div>
  </div>
  <div id="submitForm" style="display:none">
    <div class="card card-red" style="max-width:560px;margin:0 auto">
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
        <button class="btn-primary w-full" onclick="submitMatchResult()">⚽ Submit Result</button>
        <p class="text-gray text-sm" style="text-align:center;margin-top:6px">Opponent must confirm. Multiple pending matches allowed.</p>
      </div>
    </div>
  </div>
</div>

<!-- PROFILE (others) -->
<div class="page" id="page-profile">
  <button class="btn-secondary mb-16" onclick="navBack()">← Back</button>
  <div id="profileContent"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

<!-- MY PROFILE -->
<div class="page" id="page-myprofile">
  <div class="section-title">👤 My Profile</div>
  <div id="myProfileContent"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">
  <div class="section-title">🔐 Admin Panel</div>
  <div id="adminLoginWrap">
    <div class="card" style="max-width:360px;margin:0 auto">
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
      <button class="admin-tab active" onclick="switchAdminTab('pending',this)">⏳ Pending</button>
      <button class="admin-tab" onclick="switchAdminTab('players',this)">👥 Players</button>
      <button class="admin-tab" onclick="switchAdminTab('adminMatches',this)">⚽ Matches</button>
      <button class="admin-tab" onclick="switchAdminTab('moderators',this)">🛡️ Moderators</button>
      <button class="admin-tab" onclick="switchAdminTab('season',this)">🔄 Season</button>
      <button class="admin-tab" onclick="switchAdminTab('adminSettings',this)">⚙️ Settings</button>
    </div>
    <div id="adminTab-pending">
      <div class="section-title">⏳ Pending Registrations</div>
      <div id="adminPendingList"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
    <div id="adminTab-players" style="display:none">
      <div class="section-title">👥 All Players</div>
      <div class="search-bar"><input class="search-input" placeholder="Search..." id="adminPlayerSearch" oninput="filterAdminPlayers()"></div>
      <div id="adminPlayersList"></div>
    </div>
    <div id="adminTab-adminMatches" style="display:none">
      <div class="section-title">⚽ All Matches</div>
      <div id="adminMatchesList"></div>
    </div>
    <div id="adminTab-moderators" style="display:none">
      <div class="section-title">🛡️ Moderator Management</div>
      <div class="mod-panel-info">
        <div class="mod-panel-title">About Moderators</div>
        <p class="text-gray text-sm">Moderators can approve or dispute any pending match results. They cannot edit players, delete matches, or access admin settings.</p>
      </div>
      <div class="search-bar"><input class="search-input" placeholder="Search player..." id="modPlayerSearch" oninput="filterModPlayers()"></div>
      <div id="modPlayersList"></div>
    </div>
    <div id="adminTab-season" style="display:none">
      <div class="section-title">🔄 Season Management</div>
      <div class="card" style="max-width:480px">
        <p class="text-gray mb-16">Reset the season — clears all points, match history, and resets everyone to Division 9. Player accounts remain.</p>
        <button class="btn-reject btn-sm" style="padding:10px 24px;font-size:14px" onclick="confirmSeasonReset()">⚠️ Reset Season</button>
      </div>
    </div>
    <div id="adminTab-adminSettings" style="display:none">
      <div class="section-title">⚙️ Settings</div>
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
  <div class="section-title">🛡️ Moderator Panel</div>
  <div class="mod-panel-info">
    <div class="mod-panel-title">Moderator Access</div>
    <p class="text-gray text-sm">You can approve or dispute any pending match result below.</p>
  </div>
  <div id="modPendingMatches"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

</main>

<nav class="mobile-nav">
  <div class="mobile-nav-inner">
    <button class="mob-nav-btn active" onclick="navTo('home');setMobActive(this)"><span class="mob-nav-icon">🏠</span>Home</button>
    <button class="mob-nav-btn" onclick="navTo('leaderboard');setMobActive(this)"><span class="mob-nav-icon">🏆</span>Ranks</button>
    <button class="mob-nav-btn" onclick="navTo('matches');setMobActive(this)"><span class="mob-nav-icon">⚽</span>Matches</button>
    <button class="mob-nav-btn" onclick="navTo('submit');setMobActive(this)"><span class="mob-nav-icon">📝</span>Submit</button>
    <button class="mob-nav-btn" onclick="navTo('myprofile');setMobActive(this)"><span class="mob-nav-icon">👤</span>Me</button>
  </div>
</nav>

<!-- MODALS -->
<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('loginModal')">✕</button>
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
    <button class="modal-close" onclick="closeModal('registerModal')">✕</button>
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
    <button class="modal-close" onclick="closeModal('editPlayerModal')">✕</button>
    <div class="modal-title">Edit Player</div>
    <div class="match-form">
      <input type="hidden" id="editPlayerId">
      <div class="form-group"><label class="form-label">Division (1–9)</label><input class="form-input" type="number" min="1" max="9" id="editDivision"></div>
      <div class="form-group"><label class="form-label">Rating</label><input class="form-input" type="number" id="editRating"></div>
      <div class="form-group"><label class="form-label">Points</label><input class="form-input" type="number" id="editPoints"></div>
      <div class="form-group"><label class="form-label">Wins</label><input class="form-input" type="number" id="editWins"></div>
      <div class="form-group"><label class="form-label">Draws</label><input class="form-input" type="number" id="editDraws"></div>
      <div class="form-group"><label class="form-label">Losses</label><input class="form-input" type="number" id="editLosses"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editStatus"><option value="active">Active</option><option value="banned">Banned</option><option value="pending">Pending</option></select>
      </div>
      <button class="btn-primary w-full" onclick="savePlayerEdit()">Save Changes</button>
    </div>
  </div>
</div>

<div class="modal-overlay" id="editMatchModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('editMatchModal')">✕</button>
    <div class="modal-title">Edit Match</div>
    <div class="match-form">
      <input type="hidden" id="editMatchId">
      <div id="editMatchInfo" class="text-gray text-sm mb-8"></div>
      <div class="form-group"><label class="form-label">Score — Player A</label><input class="form-input" type="number" min="0" id="editScoreA"></div>
      <div class="form-group"><label class="form-label">Score — Player B</label><input class="form-input" type="number" min="0" id="editScoreB"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editMatchStatus">
          <option value="confirmed">Confirmed</option><option value="pending">Pending</option><option value="disputed">Disputed</option>
        </select>
      </div>
      <button class="btn-primary w-full" onclick="saveMatchEdit()">Save Changes</button>
      <button class="btn-reject btn-sm w-full mt-8" onclick="adminDeleteMatch()">🗑 Delete Match</button>
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

// ===== STATE =====
let S = {
  user: null,
  lbTab: 'overall',
  players: [],
  matches: [],
  lbPlayers: [],
  allMatchesData: [],
  adminPlayers: [],
  pageHistory: ['home'],
  adminPw: 'fardous'
};

// ===== UTILS =====
const $ = id => document.getElementById(id);
function showToast(msg, type='info') {
  const t = $('toast');
  t.textContent = msg;
  t.className = `toast show ${type}`;
  clearTimeout(window._tt);
  window._tt = setTimeout(() => t.classList.remove('show'), 3500);
}
function openModal(id) { $(id).classList.add('open'); }
function closeModal(id) { $(id).classList.remove('open'); }

function showPage(pg) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  const el = $('page-' + pg);
  if (el) el.classList.add('active');
}

function navTo(pg) {
  S.pageHistory.push(pg);
  showPage(pg);
  // Highlight desktop nav
  const map = {home:'navHome',leaderboard:'navLeaderboard',matches:'navMatches',submit:'navSubmit'};
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  if (map[pg]) $(map[pg])?.classList.add('active');

  if (pg === 'home') loadHome();
  else if (pg === 'leaderboard') loadLeaderboard(S.lbTab);
  else if (pg === 'matches') loadMatches();
  else if (pg === 'submit') loadSubmitPage();
  else if (pg === 'myprofile') loadMyProfile();
  else if (pg === 'modpanel') loadModPanel();
}

function navBack() {
  S.pageHistory.pop();
  const prev = S.pageHistory[S.pageHistory.length - 1] || 'home';
  showPage(prev);
  if (prev === 'leaderboard') { /* already loaded */ }
}

function setNavActive(btn) {
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
}

function setMobActive(btn) {
  document.querySelectorAll('.mob-nav-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
}

// Helpers
function divBadge(d) { return `<div class="div-badge div-${d||9}">${d||9}</div>`; }
function formBadge(r) { const c = r==='W'?'form-w':r==='D'?'form-d':'form-l'; return `<div class="form-dot ${c}" title="${r}"></div>`; }
function statusBadge(s) { return `<span class="status-badge status-${s}">${s}</span>`; }
function fmtDate(ts) {
  if (!ts) return '';
  try { const d = ts.toDate ? ts.toDate() : new Date(ts); return d.toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'}); }
  catch { return ''; }
}
function timeAgo(ts) {
  if (!ts) return '';
  try {
    const d = ts.toDate ? ts.toDate() : new Date(ts);
    const diff = Date.now() - d.getTime();
    const m = Math.floor(diff/60000);
    if (m<1) return 'just now'; if (m<60) return m+'m ago';
    const h = Math.floor(m/60); if (h<24) return h+'h ago';
    return Math.floor(h/24)+'d ago';
  } catch { return ''; }
}
function getRC(sA, sB, side) {
  const my = side==='A'?sA:sB, op = side==='A'?sB:sA;
  return my>op?'W':my<op?'L':'D';
}
function calcPts(sA, sB, side) { const r=getRC(sA,sB,side); return r==='W'?3:r==='D'?1:0; }
function calcRating(sA, sB, side, div) {
  if ((div||9)>3) return 0;
  const r=getRC(sA,sB,side);
  return r==='W'?Math.floor(Math.random()*11)+15:r==='L'?-(Math.floor(Math.random()*11)+10):(Math.random()>.5?3:-3);
}
function isHigh(sA,sB) { return (sA+sB)>7; }

// ===== NEWS =====
function buildNews(matches) {
  const hi = matches.filter(m=>m.status==='confirmed'&&isHigh(m.scoreA,m.scoreB));
  if (!hi.length) { $('newsTicker').style.display='none'; return; }
  $('newsText').textContent = hi.slice(0,8).map(m=>`🔥 GOAL FEST! ${m.playerAName} ${m.scoreA}–${m.scoreB} ${m.playerBName} (${m.scoreA+m.scoreB} goals!)`).join('    ·    ');
  $('newsTicker').style.display='flex';
}

// ===== AUTH =====
async function doLogin() {
  const name=$('loginName').value.trim(), pw=$('loginPw').value;
  if (!name||!pw) return showToast('Fill in all fields','error');
  try {
    const snap = await getDocs(query(collection(db,'players'),where('name','==',name)));
    if (snap.empty) return showToast('Player not found','error');
    const d = snap.docs[0]; const p = d.data();
    if (p.password!==pw) return showToast('Wrong password','error');
    if (p.status==='pending') return showToast('Account pending admin approval','info');
    if (p.status==='banned') return showToast('Account banned. Contact admin.','error');
    S.user = {id:d.id,...p};
    closeModal('loginModal');
    updateHeaderAuth();
    showToast('Welcome back, '+name+'! ⚽','success');
    loadSubmitPage();
    loadMatches();
  } catch(e) { showToast('Login failed: '+e.message,'error'); }
}

async function doRegister() {
  const name=$('regName').value.trim(), cat=$('regCategory').value;
  const pw=$('regPw').value, pw2=$('regPwConfirm').value;
  if (!name||!pw) return showToast('Fill in all fields','error');
  if (pw!==pw2) return showToast('Passwords do not match','error');
  if (pw.length<4) return showToast('Password too short (min 4)','error');
  try {
    const ex = await getDocs(query(collection(db,'players'),where('name','==',name)));
    if (!ex.empty) return showToast('Name already taken','error');
    await addDoc(collection(db,'players'),{
      name,category:cat,password:pw,status:'pending',division:9,rating:1000,
      points:0,wins:0,draws:0,losses:0,form:[],rivals:[],isModerator:false,createdAt:serverTimestamp()
    });
    closeModal('registerModal');
    showToast('Submitted! Awaiting admin approval 🎮','success');
    ['regName','regPw','regPwConfirm'].forEach(id=>$(id).value='');
  } catch(e) { showToast('Registration failed: '+e.message,'error'); }
}

function doLogout() {
  S.user=null; updateHeaderAuth();
  showToast('Logged out','info');
  navTo('home');
}

function updateHeaderAuth() {
  const el=$('headerAuth');
  if (S.user) {
    const isMod=S.user.isModerator;
    el.innerHTML=`
      <div class="user-pill" onclick="navTo('myprofile')">
        <div class="user-avatar">${S.user.name[0].toUpperCase()}</div>
        <span class="user-name">${S.user.name}</span>
        ${isMod?'<span class="mod-badge">MOD</span>':''}
      </div>
      ${isMod?`<button class="btn-login" style="border-color:var(--blue);color:var(--blue);font-size:11px" onclick="navTo('modpanel')">🛡️ Mod</button>`:''}
      <button class="btn-login" onclick="doLogout()">Logout</button>
      <button class="btn-login" style="border-color:var(--yellow);color:var(--yellow);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  } else {
    el.innerHTML=`
      <button class="btn-login" onclick="openModal('loginModal')">Login</button>
      <button class="btn-register" onclick="openModal('registerModal')">Register</button>
      <button class="btn-login" style="border-color:var(--yellow);color:var(--yellow);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }
}

// ===== HOME =====
async function loadHome() {
  try {
    const [pSnap,mSnap] = await Promise.all([
      getDocs(collection(db,'players')),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(100)))
    ]);
    S.players = pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    S.matches = mSnap.docs.map(d=>({id:d.id,...d.data()}));
    buildNews(S.matches);
    const now=Date.now();
    const todayMs=S.matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<86400000);
    $('statPlayers').textContent=S.players.length;
    $('statMatches').textContent=S.matches.filter(m=>m.status==='confirmed').length;
    $('statToday').textContent=todayMs.length;
    $('statPending').textContent=S.matches.filter(m=>m.status==='pending').length;

    const sorted=[...S.players].sort((a,b)=>(b.points||0)-(a.points||0)||(b.rating||0)-(a.rating||0)).slice(0,5);
    $('homeTopPlayers').innerHTML=sorted.length?sorted.map((p,i)=>`
      <div class="pending-item" style="cursor:pointer" onclick="viewProfile('${p.id}')">
        <span class="rank-num rank-${i+1}" style="font-size:20px;width:26px">${i+1}</span>
        ${divBadge(p.division)}
        <div class="pending-info">
          <div class="pending-name">${p.name}</div>
          <div class="pending-meta">${p.wins||0}W ${p.draws||0}D ${p.losses||0}L · ${p.points||0} pts</div>
        </div>
        <span class="rating-val">${p.rating||1000}</span>
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
            ${hi?' <span class="high-score-badge">🔥 GOAL FEST</span>':''}
          </div>
          <div class="match-meta">${fmtDate(m.createdAt)}</div>
        </div>
        <div class="match-score">${m.scoreA}–${m.scoreB}</div>
      </div>`;
    }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>';

    const divInfo=[
      {d:1,name:'Elite',desc:'Top of the ladder. Rating active.'},
      {d:2,name:'Premier',desc:'Near the summit. Rating active.'},
      {d:3,name:'Championship',desc:'Rating system activates here.'},
      {d:4,name:'League One',desc:'Competitive mid-tier.'},
      {d:5,name:'League Two',desc:'Mid-tier battles.'},
      {d:6,name:'National',desc:'Development level.'},
      {d:7,name:'Regional',desc:'Entry competitive.'},
      {d:8,name:'Amateur',desc:'Getting started.'},
      {d:9,name:'Rookie',desc:'All new players start here.'},
    ];
    $('divisionGuide').innerHTML=divInfo.map(di=>`
      <div class="stat-card" style="text-align:left;border-color:${di.d<=3?'rgba(204,0,0,0.4)':'rgba(204,0,0,0.15)'}">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:6px">
          ${divBadge(di.d)}
          <span style="font-family:'Bebas Neue',sans-serif;font-size:16px">${di.name}</span>
        </div>
        <div class="text-gray text-sm">${di.desc}</div>
        ${di.d<=3?'<div style="font-size:10px;color:var(--red-bright);margin-top:4px;letter-spacing:1px">★ RATING ACTIVE</div>':''}
      </div>`).join('');
  } catch(e) { console.error(e); showToast('Error loading home','error'); }
}

// ===== LEADERBOARD =====
async function loadLeaderboard(tab='overall') {
  S.lbTab=tab;
  $('lbTableBody').innerHTML='<tr><td colspan="9" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>';
  try {
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
      if (tab!=='overall') pm=pm.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<timeFilter);
      let w=0,d=0,l=0;
      pm.forEach(m=>{const r=getRC(m.scoreA,m.scoreB,m.playerAId===p.id?'A':'B');if(r==='W')w++;else if(r==='D')d++;else l++;});
      const total=w+d+l, wr=total>0?Math.round(w/total*100):0;
      return {...p,tw:w,td:d,tl:l,twr:wr,tpts:tab==='overall'?(p.points||0):(w*3+d),total};
    });
    if (tab!=='overall') players=players.filter(p=>p.total>0);
    players.sort((a,b)=>b.tpts-a.tpts||(b.rating||0)-(a.rating||0)||b.twr-a.twr);
    S.lbPlayers=players;
    renderLbTable(players);
  } catch(e) {
    $('lbTableBody').innerHTML='<tr><td colspan="9" style="text-align:center;color:var(--red)">Error loading</td></tr>';
    console.error(e);
  }
}

function renderLbTable(players) {
  const search=($('lbSearch')?.value||'').toLowerCase();
  const divF=$('lbDivFilter')?.value||'';
  const filtered=players.filter(p=>p.name.toLowerCase().includes(search)&&(!divF||String(p.division||9)===divF));
  const tbody=$('lbTableBody');
  if (!filtered.length) {
    tbody.innerHTML='<tr><td colspan="9"><div class="empty-state"><div class="empty-icon">🏆</div><div class="empty-text">No players found</div></div></td></tr>';
    return;
  }
  tbody.innerHTML=filtered.map((p,i)=>{
    const r=i+1, rc=r===1?'top-1':r===2?'top-2':r===3?'top-3':'';
    const form=(p.form||[]).slice(-5);
    return `<tr class="${rc}">
      <td><span class="rank-num rank-${r}">${r}</span></td>
      <td>
        <span class="player-link" onclick="viewProfile('${p.id}')">
          <div class="user-avatar" style="width:26px;height:26px;font-size:11px">${p.name[0].toUpperCase()}</div>
          ${p.name}${p.isModerator?' <span class="mod-badge">MOD</span>':''}
        </span>
      </td>
      <td>${divBadge(p.division)}</td>
      <td><span class="rating-val">${p.rating||1000}</span></td>
      <td><strong style="font-size:16px">${p.tpts}</strong></td>
      <td>
        <div class="wdl-row">
          <span class="wdl-pill wdl-w"><span class="wdl-num">${p.tw}</span>&nbsp;W</span>
          <span class="wdl-pill wdl-d"><span class="wdl-num">${p.td}</span>&nbsp;D</span>
          <span class="wdl-pill wdl-l"><span class="wdl-num">${p.tl}</span>&nbsp;L</span>
        </div>
      </td>
      <td class="text-gray">${p.total}</td>
      <td>
        <div class="winrate-wrap">
          <div class="winrate-bar"><div class="winrate-fill" style="width:${p.twr}%"></div></div>
          <span class="winrate-pct">${p.twr}%</span>
        </div>
      </td>
      <td><div class="form-dots">${form.map(r=>formBadge(r)).join('')}</div></td>
    </tr>`;
  }).join('');
}

function filterLeaderboard() { if(S.lbPlayers.length) renderLbTable(S.lbPlayers); }

function switchLbTab(tab,btn) {
  document.querySelectorAll('.lb-tab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  loadLeaderboard(tab);
}

// ===== MATCHES =====
async function loadMatches() {
  try {
    const mSnap=await getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(150)));
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    S.allMatchesData=S.matches;
    renderMatchesList(S.matches);
    const section=$('pendingConfirmSection'), list=$('pendingConfirmList');
    if (S.user) {
      const isMod=S.user.isModerator;
      const pending=S.matches.filter(m=>m.status==='pending'&&(isMod||m.playerBId===S.user.id));
      if (pending.length) {
        section.style.display='block';
        list.innerHTML=pending.map(m=>`
          <div class="confirm-card">
            ${isMod&&m.playerBId!==S.user.id?'<div class="text-purple text-sm mb-8">🛡️ Moderator review</div>':''}
            <div class="confirm-vs">
              <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">Submitted by</div></div>
              <div class="confirm-score-display">${m.scoreA}–${m.scoreB}</div>
              <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">Opponent</div></div>
            </div>
            <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} · ${timeAgo(m.createdAt)}</div>
            <div style="display:flex;gap:8px;flex-wrap:wrap">
              <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">✔ Confirm</button>
              <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">✕ Dispute</button>
            </div>
          </div>`).join('');
      } else section.style.display='none';
    } else section.style.display='none';
  } catch(e) { $('matchesList').innerHTML='<div class="empty-state"><div class="empty-text">Error loading matches</div></div>'; console.error(e); }
}

function renderMatchesList(matches) {
  const search=($('matchSearch')?.value||'').toLowerCase();
  const sf=$('matchStatusFilter')?.value||'';
  let f=matches;
  if(search) f=f.filter(m=>m.playerAName?.toLowerCase().includes(search)||m.playerBName?.toLowerCase().includes(search));
  if(sf) f=f.filter(m=>m.status===sf);
  const el=$('matchesList');
  if (!f.length) { el.innerHTML='<div class="empty-state"><div class="empty-icon">⚽</div><div class="empty-text">No matches found</div></div>'; return; }
  el.innerHTML=f.map(m=>{
    const hi=isHigh(m.scoreA,m.scoreB);
    return `<div class="match-card${hi?' high-score':''}">
      <div class="match-info">
        <div class="match-vs">
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
          <span class="text-gray"> vs </span>
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
          ${hi?' &nbsp;<span class="high-score-badge">🔥 GOAL FEST</span>':''}
        </div>
        <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} · ${statusBadge(m.status)}</div>
      </div>
      <div class="match-score">${m.scoreA}–${m.scoreB}</div>
    </div>`;
  }).join('');
}

function filterMatches() { if(S.allMatchesData.length) renderMatchesList(S.allMatchesData); }

async function confirmMatch(matchId, confirmed) {
  try {
    const mRef=doc(db,'matches',matchId);
    const mSnap=await getDoc(mRef);
    if (!mSnap.exists()) return showToast('Match not found','error');
    const m=mSnap.data();
    if (confirmed) {
      await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
      await applyMatchStats(m);
      showToast('Match confirmed! Stats updated ✅','success');
    } else {
      await updateDoc(mRef,{status:'disputed'});
      showToast('Match disputed. Admin will review.','info');
    }
    S.matches=[]; loadMatches();
  } catch(e) { showToast('Error: '+e.message,'error'); }
}

async function applyMatchStats(m) {
  async function upd(pid, side) {
    const ref=doc(db,'players',pid), snap=await getDoc(ref);
    if (!snap.exists()) return;
    const p=snap.data();
    const result=getRC(m.scoreA,m.scoreB,side);
    const pts=calcPts(m.scoreA,m.scoreB,side);
    const rc=calcRating(m.scoreA,m.scoreB,side,p.division||9);
    const form=[...(p.form||[]).slice(-9),result];
    await updateDoc(ref,{
      points:(p.points||0)+pts, rating:Math.max(500,(p.rating||1000)+rc),
      wins:(p.wins||0)+(result==='W'?1:0), draws:(p.draws||0)+(result==='D'?1:0),
      losses:(p.losses||0)+(result==='L'?1:0), form
    });
  }
  await Promise.all([upd(m.playerAId,'A'), upd(m.playerBId,'B')]);
}

// ===== SUBMIT =====
async function loadSubmitPage() {
  if (!S.user) { $('submitRequireLogin').style.display='block'; $('submitForm').style.display='none'; return; }
  $('submitRequireLogin').style.display='none'; $('submitForm').style.display='block';
  $('submitMyName').value=S.user.name;
  $('matchDate').value=new Date().toISOString().split('T')[0];
  const snap=await getDocs(collection(db,'players'));
  S.players=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
  const sel=$('submitOpponent');
  sel.innerHTML='<option value="">-- Select Opponent --</option>'+
    S.players.filter(p=>p.id!==S.user.id).map(p=>`<option value="${p.id}">${p.name} (Div ${p.division||9})</option>`).join('');
}

async function submitMatchResult() {
  if (!S.user) return showToast('Login required','error');
  const oppId=$('submitOpponent').value;
  const sA=parseInt($('scoreA').value)||0, sB=parseInt($('scoreB').value)||0;
  const matchDate=$('matchDate').value;
  if (!oppId) return showToast('Select an opponent','error');
  const opp=S.players.find(p=>p.id===oppId);
  if (!opp) return showToast('Opponent not found','error');
  try {
    await addDoc(collection(db,'matches'),{
      playerAId:S.user.id,playerAName:S.user.name,
      playerBId:oppId,playerBName:opp.name,
      scoreA:sA,scoreB:sB,status:'pending',matchDate,
      createdAt:serverTimestamp(),submittedBy:S.user.id
    });
    const msg=isHigh(sA,sB)?`🔥 GOAL FEST! ${sA+sB} goals submitted! Waiting for ${opp.name} to confirm.`:`Result submitted! Waiting for ${opp.name} to confirm ⚽`;
    showToast(msg,'success');
    $('scoreA').value=''; $('scoreB').value='';
    S.matches=[];
  } catch(e) { showToast('Submit failed: '+e.message,'error'); }
}

// ===== MOD PANEL =====
async function loadModPanel() {
  if (!S.user||!S.user.isModerator) {
    $('modPendingMatches').innerHTML='<div class="empty-state"><div class="empty-icon">🚫</div><div class="empty-text">Moderator access required</div></div>';
    return;
  }
  try {
    const mSnap=await getDocs(query(collection(db,'matches'),where('status','==','pending'),orderBy('createdAt','desc'),limit(100)));
    const pending=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('modPendingMatches');
    if (!pending.length) { el.innerHTML='<div class="empty-state"><div class="empty-icon">✅</div><div class="empty-text">No pending matches</div></div>'; return; }
    el.innerHTML=pending.map(m=>`
      <div class="confirm-card">
        <div class="confirm-vs">
          <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">Player A</div></div>
          <div class="confirm-score-display">${m.scoreA}–${m.scoreB}</div>
          <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">Player B</div></div>
        </div>
        <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} · ${timeAgo(m.createdAt)}</div>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">✔ Approve</button>
          <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">✕ Dispute</button>
        </div>
      </div>`).join('');
  } catch(e) { showToast('Error: '+e.message,'error'); }
}

// ===== PROFILE =====
async function viewProfile(playerId) {
  S.pageHistory.push('profile');
  showPage('profile');
  $('profileContent').innerHTML='<div class="loading-spinner"><div class="spinner"></div></div>';
  try {
    const [snap,mSnap]=await Promise.all([
      getDoc(doc(db,'players',playerId)),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(300)))
    ]);
    if (!snap.exists()) { $('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Player not found</div></div>'; return; }
    const p={id:snap.id,...snap.data()};
    const matches=mSnap.docs.map(d=>({id:d.id,...d.data()})).filter(m=>m.playerAId===playerId||m.playerBId===playerId).slice(0,10);
    const total=(p.wins||0)+(p.draws||0)+(p.losses||0);
    const wr=total>0?Math.round((p.wins||0)/total*100):0;
    const form=(p.form||[]).slice(-5);
    const promoNeed={9:15,8:20,7:25,6:30,5:35,4:40,3:45,2:50,1:0};
    const need=promoNeed[p.division||9]||50;
    const pct=need>0?Math.min(100,Math.round((p.points||0)/need*100)):100;
    const isRival=S.user&&(S.user.rivals||[]).includes(playerId);
    const isMe=S.user&&S.user.id===playerId;

    $('profileContent').innerHTML=`
      <div class="profile-header">
        <div class="profile-avatar">${p.name[0].toUpperCase()}</div>
        <div class="profile-info">
          <div class="profile-name">${p.name}${p.isModerator?' <span class="mod-badge" style="font-size:13px">🛡️MOD</span>':''}</div>
          <span class="profile-cat">${p.category||'Youth'}</span>
          <div style="display:flex;align-items:center;gap:10px;margin-top:8px;flex-wrap:wrap">
            ${divBadge(p.division)} <span class="text-gray text-sm">Division ${p.division||9}</span>
            <span class="rating-val" style="font-size:26px">${p.rating||1000}</span>
            <span class="text-gray text-sm">Rating</span>
          </div>
          <div class="form-dots mt-8">${form.map(r=>formBadge(r)).join('')}</div>
          ${!isMe&&S.user?`<button class="btn-sm ${isRival?'btn-reject':'btn-edit'} mt-8" onclick="toggleRival('${playerId}','${p.name}')">
            ${isRival?'❌ Remove Rival':'⚔️ Add Rival'}</button>`:''}
        </div>
      </div>
      <div class="profile-stats">
        <div class="p-stat"><div class="p-stat-val">${p.points||0}</div><div class="p-stat-lbl">Points</div></div>
        <div class="p-stat"><div class="p-stat-val text-green">${p.wins||0}</div><div class="p-stat-lbl">Wins</div></div>
        <div class="p-stat"><div class="p-stat-val text-yellow">${p.draws||0}</div><div class="p-stat-lbl">Draws</div></div>
        <div class="p-stat"><div class="p-stat-val text-red">${p.losses||0}</div><div class="p-stat-lbl">Losses</div></div>
        <div class="p-stat"><div class="p-stat-val">${total}</div><div class="p-stat-lbl">Matches</div></div>
        <div class="p-stat"><div class="p-stat-val">${wr}%</div><div class="p-stat-lbl">Win Rate</div></div>
        <div class="p-stat"><div class="p-stat-val">${p.rating||1000}</div><div class="p-stat-lbl">Rating</div></div>
      </div>
      <div class="promo-tracker">
        <div class="promo-title">Promotion Progress${p.division<=1?' — 🏆 Top Division!':''}</div>
        <div class="promo-bar-wrap"><div class="promo-bar-fill" style="width:${pct}%"></div></div>
        <div class="promo-label"><span>${p.points||0} pts</span><span>${p.division<=1?'MAX':need+' pts needed'}</span></div>
      </div>
      <div class="section-title mt-16">📅 Recent Matches</div>
      ${matches.length?matches.map(m=>{
        const side=m.playerAId===playerId?'A':'B';
        const res=getRC(m.scoreA,m.scoreB,side);
        const oppName=side==='A'?m.playerBName:m.playerAName;
        const oppId=side==='A'?m.playerBId:m.playerAId;
        const my=side==='A'?m.scoreA:m.scoreB, op=side==='A'?m.scoreB:m.scoreA;
        const hi=isHigh(m.scoreA,m.scoreB);
        return `<div class="match-card${hi?' high-score':''}">
          <div class="match-result-badge result-${res}">${res}</div>
          <div class="match-info">
            <div class="match-vs">vs <span class="player-link" style="display:inline" onclick="viewProfile('${oppId}')">${oppName}</span>${hi?' <span class="high-score-badge">🔥</span>':''}</div>
            <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} · ${statusBadge(m.status)}</div>
          </div>
          <div class="match-score">${my}–${op}</div>
        </div>`;
      }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>'}
    `;
  } catch(e) { $('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Error loading profile</div></div>'; console.error(e); }
}

async function loadMyProfile() {
  if (!S.user) {
    $('myProfileContent').innerHTML='<div class="empty-state"><div class="empty-icon">🔒</div><div class="empty-text">Not logged in</div><button class="btn-primary mt-12" onclick="openModal(\'loginModal\')">Login</button></div>';
    return;
  }
  await viewProfile(S.user.id);
  $('myProfileContent').innerHTML=$('profileContent').innerHTML;
}

async function toggleRival(playerId, playerName) {
  if (!S.user) return;
  const rivals=S.user.rivals||[];
  const nr=rivals.includes(playerId)?rivals.filter(r=>r!==playerId):[...rivals,playerId];
  await updateDoc(doc(db,'players',S.user.id),{rivals:nr});
  S.user.rivals=nr;
  showToast(rivals.includes(playerId)?playerName+' removed from rivals':playerName+' added as rival ⚔️','success');
  viewProfile(playerId);
}

// ===== ADMIN =====
async function adminLogin() {
  const pw=$('adminPwInput').value;
  let stored=S.adminPw;
  try { const snap=await getDoc(doc(db,'settings','admin')); if(snap.exists()&&snap.data().password) stored=snap.data().password; } catch {}
  if (pw===stored) {
    $('adminLoginWrap').style.display='none';
    $('adminPanelWrap').style.display='block';
    loadAdminPanel('pending');
    showToast('Admin access granted ✅','success');
  } else showToast('Wrong password','error');
}

async function loadAdminPanel(tab) {
  if (tab==='pending') {
    const snap=await getDocs(query(collection(db,'players'),where('status','==','pending')));
    const pending=snap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('adminPendingList');
    if (!pending.length) { el.innerHTML='<div class="empty-state"><div class="empty-icon">✅</div><div class="empty-text">No pending registrations</div></div>'; return; }
    el.innerHTML=pending.map(p=>`
      <div class="pending-item">
        <div class="pending-info"><div class="pending-name">${p.name}</div><div class="pending-meta">${p.category} · ${fmtDate(p.createdAt)}</div></div>
        <div style="display:flex;gap:6px;flex-wrap:wrap">
          <button class="btn-sm btn-approve" onclick="adminApprove('${p.id}')">✔ Approve</button>
          <button class="btn-sm btn-reject" onclick="adminReject('${p.id}')">✕ Reject</button>
        </div>
      </div>`).join('');
  }
  if (tab==='players') {
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()}));
    renderAdminPlayers(S.adminPlayers);
  }
  if (tab==='adminMatches') {
    const snap=await getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(100)));
    const matches=snap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('adminMatchesList');
    if (!matches.length) { el.innerHTML='<div class="empty-state"><div class="empty-text">No matches</div></div>'; return; }
    el.innerHTML=matches.map(m=>{
      const hi=isHigh(m.scoreA,m.scoreB);
      return `<div class="pending-item${hi?' high-score':''}">
        <div class="pending-info">
          <div class="pending-name">${m.playerAName} ${m.scoreA}–${m.scoreB} ${m.playerBName}${hi?' 🔥':''}</div>
          <div class="pending-meta">${fmtDate(m.createdAt)} · ${statusBadge(m.status)}</div>
        </div>
        <div style="display:flex;gap:5px;flex-wrap:wrap">
          ${m.status==='pending'?`<button class="btn-sm btn-approve" onclick="adminConfirmMatch('${m.id}')">✔ Confirm</button>`:''}
          <button class="btn-sm btn-edit" onclick="adminEditMatch('${m.id}','${m.playerAName}','${m.playerBName}',${m.scoreA},${m.scoreB},'${m.status}')">Edit</button>
          <button class="btn-sm btn-reject" onclick="adminDeleteMatchDirect('${m.id}')">Delete</button>
        </div>
      </div>`;
    }).join('');
  }
  if (tab==='moderators') {
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    renderModPlayers(S.adminPlayers);
  }
}

function renderAdminPlayers(players) {
  const search=($('adminPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  $('adminPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name}${p.status==='banned'?' 🚫':p.status==='pending'?' ⏳':''}${p.isModerator?' 🛡️':''}</div>
        <div class="pending-meta">${p.category||'Youth'} · Div${p.division||9} · ${p.rating||1000} rating · ${p.points||0}pts · ${p.wins||0}W ${p.draws||0}D ${p.losses||0}L · ${statusBadge(p.status||'active')}</div>
      </div>
      <div style="display:flex;gap:5px;flex-wrap:wrap">
        <button class="btn-sm btn-edit" onclick="adminEditPlayer('${p.id}',${p.division||9},${p.rating||1000},${p.points||0},${p.wins||0},${p.draws||0},${p.losses||0},'${p.status||'active'}')">Edit</button>
        <button class="btn-sm btn-ban" onclick="adminToggleBan('${p.id}','${p.name}','${p.status||'active'}')">
          ${p.status==='banned'?'Unban':'Ban'}</button>
      </div>
    </div>`).join(''):'<div class="empty-state"><div class="empty-text">No players</div></div>';
}

function filterAdminPlayers() { if(S.adminPlayers.length) renderAdminPlayers(S.adminPlayers); }

function renderModPlayers(players) {
  const search=($('modPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  $('modPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name}${p.isModerator?' <span class="mod-badge">🛡️ MODERATOR</span>':''}</div>
        <div class="pending-meta">${p.category||'Youth'} · ${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
      </div>
      <button class="btn-sm ${p.isModerator?'btn-reject':'btn-mod'}" onclick="adminToggleMod('${p.id}','${p.name}',${!!p.isModerator})">
        ${p.isModerator?'Remove Mod':'Give Mod'}</button>
    </div>`).join(''):'<div class="empty-state"><div class="empty-text">No active players</div></div>';
}

function filterModPlayers() { if(S.adminPlayers.length) renderModPlayers(S.adminPlayers); }

async function adminToggleMod(id, name, isMod) {
  const nv=!isMod;
  await updateDoc(doc(db,'players',id),{isModerator:nv});
  showToast(name+(nv?' is now a Moderator 🛡️':' moderator removed'),nv?'success':'info');
  if (S.user&&S.user.id===id) { S.user.isModerator=nv; updateHeaderAuth(); }
  loadAdminPanel('moderators');
}

async function adminApprove(id) {
  await updateDoc(doc(db,'players',id),{status:'active'});
  showToast('Player approved ✅','success'); loadAdminPanel('pending');
}

async function adminReject(id) {
  if (!confirm('Reject and delete this registration?')) return;
  await deleteDoc(doc(db,'players',id));
  showToast('Rejected','info'); loadAdminPanel('pending');
}

function adminEditPlayer(id,div,rating,pts,wins,draws,losses,status) {
  $('editPlayerId').value=id; $('editDivision').value=div; $('editRating').value=rating;
  $('editPoints').value=pts; $('editWins').value=wins; $('editDraws').value=draws;
  $('editLosses').value=losses; $('editStatus').value=status;
  openModal('editPlayerModal');
}

async function savePlayerEdit() {
  const id=$('editPlayerId').value, div=parseInt($('editDivision').value);
  const rating=parseInt($('editRating').value), pts=parseInt($('editPoints').value);
  const wins=parseInt($('editWins').value), draws=parseInt($('editDraws').value);
  const losses=parseInt($('editLosses').value), status=$('editStatus').value;
  if (div<1||div>9) return showToast('Division 1–9 only','error');
  try {
    await updateDoc(doc(db,'players',id),{division:div,rating,points:pts,wins,draws,losses,status});
    showToast('Player updated ✅','success'); closeModal('editPlayerModal'); loadAdminPanel('players');
  } catch(e) { showToast('Error: '+e.message,'error'); }
}

async function adminToggleBan(id,name,cs) {
  const ns=cs==='banned'?'active':'banned';
  await updateDoc(doc(db,'players',id),{status:ns});
  showToast(name+' '+ns,'info'); loadAdminPanel('players');
}

function adminEditMatch(id,nA,nB,sA,sB,status) {
  $('editMatchId').value=id; $('editMatchInfo').textContent=`${nA} vs ${nB}`;
  $('editScoreA').value=sA; $('editScoreB').value=sB; $('editMatchStatus').value=status;
  openModal('editMatchModal');
}

async function adminConfirmMatch(matchId) {
  const mRef=doc(db,'matches',matchId), mSnap=await getDoc(mRef);
  if (!mSnap.exists()) return;
  await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
  await applyMatchStats(mSnap.data());
  showToast('Match confirmed by admin ✅','success');
  S.matches=[]; loadAdminPanel('adminMatches');
}

async function saveMatchEdit() {
  const id=$('editMatchId').value, sA=parseInt($('editScoreA').value), sB=parseInt($('editScoreB').value);
  const status=$('editMatchStatus').value;
  try {
    await updateDoc(doc(db,'matches',id),{scoreA:sA,scoreB:sB,status});
    showToast('Match updated ✅','success'); closeModal('editMatchModal');
    S.matches=[]; loadAdminPanel('adminMatches');
  } catch(e) { showToast('Error: '+e.message,'error'); }
}

async function adminDeleteMatch() {
  const id=$('editMatchId').value;
  if (!confirm('Delete this match permanently?')) return;
  await deleteDoc(doc(db,'matches',id));
  showToast('Match deleted','info'); closeModal('editMatchModal');
  S.matches=[]; loadAdminPanel('adminMatches');
}

async function adminDeleteMatchDirect(id) {
  if (!confirm('Delete this match?')) return;
  await deleteDoc(doc(db,'matches',id));
  showToast('Match deleted','info');
  S.matches=[]; loadAdminPanel('adminMatches');
}

async function confirmSeasonReset() {
  if (!confirm('⚠️ RESET ENTIRE SEASON?\n\nAll matches deleted, all player stats reset to zero. Accounts remain.\n\nPress OK to confirm.')) return;
  try {
    const [pSnap,mSnap]=await Promise.all([getDocs(collection(db,'players')),getDocs(collection(db,'matches'))]);
    await Promise.all([
      ...pSnap.docs.map(d=>updateDoc(doc(db,'players',d.id),{points:0,wins:0,draws:0,losses:0,form:[],division:9,rating:1000})),
      ...mSnap.docs.map(d=>deleteDoc(doc(db,'matches',d.id)))
    ]);
    S.players=[]; S.matches=[];
    showToast('Season reset! 🔄','success');
  } catch(e) { showToast('Error: '+e.message,'error'); }
}

async function changeAdminPassword() {
  const pw=$('newAdminPw').value, pw2=$('confirmAdminPw').value;
  if (!pw||pw.length<4) return showToast('Password too short','error');
  if (pw!==pw2) return showToast('Passwords do not match','error');
  try {
    await setDoc(doc(db,'settings','admin'),{password:pw},{merge:true});
    S.adminPw=pw; showToast('Admin password updated ✅','success');
    $('newAdminPw').value=''; $('confirmAdminPw').value='';
  } catch(e) { showToast('Error: '+e.message,'error'); }
}

function switchAdminTab(tab,btn) {
  document.querySelectorAll('.admin-tab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('[id^="adminTab-"]').forEach(el=>el.style.display='none');
  $('adminTab-'+tab).style.display='block';
  loadAdminPanel(tab);
}

// ===== EXPOSE =====
Object.assign(window,{
  navTo, navBack, setNavActive, setMobActive,
  openModal, closeModal,
  doLogin, doRegister, doLogout,
  switchLbTab, filterLeaderboard,
  filterMatches, confirmMatch,
  submitMatchResult, loadSubmitPage,
  viewProfile, toggleRival, loadMyProfile,
  adminLogin, loadAdminPanel, switchAdminTab,
  adminApprove, adminReject, adminEditPlayer, savePlayerEdit,
  adminToggleBan, adminToggleMod,
  adminEditMatch, saveMatchEdit, adminDeleteMatch, adminDeleteMatchDirect,
  adminConfirmMatch, filterAdminPlayers, filterModPlayers,
  confirmSeasonReset, changeAdminPassword, loadModPanel
});

// ===== INIT =====
updateHeaderAuth();
loadHome();
document.querySelectorAll('.modal-overlay').forEach(m => {
  m.addEventListener('click', e => { if(e.target===m) m.classList.remove('open'); });
});
</script>
</body>
</html>
