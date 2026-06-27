<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Algorithmic Pricing Audit Platform — Journey of Insight</title>
<style>
:root{
  --bg:#06080F;--s1:#0C1422;--s2:#111D30;--s3:#162440;
  --cyan:#00CFFF;--cdim:rgba(0,207,255,.12);--cb:rgba(0,207,255,.2);
  --gold:#C8A96A;--gdim:rgba(200,169,106,.14);--gb:rgba(200,169,106,.28);
  --red:#FF4B6E;--rdim:rgba(255,75,110,.12);
  --grn:#2ECC98;--grdim:rgba(46,204,152,.12);--grb:rgba(46,204,152,.28);
  --amb:#F59E0B;--adim:rgba(245,158,11,.12);
  --wt:#E8EFFF;--mu:#6A8BAF;--di:#3D5A7A;
  --br:rgba(255,255,255,.06);--bcn:rgba(0,207,255,.16);
  --rad:12px;--rads:8px;--radl:18px;
}
*{margin:0;padding:0;box-sizing:border-box}
html,body{height:100%}
body{background:var(--bg);color:var(--wt);font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',system-ui,sans-serif;font-size:14px;line-height:1.5}

/* LAYOUT */
.wrap{display:flex;min-height:100vh}
.sidebar{width:256px;min-width:256px;background:var(--s1);border-right:1px solid var(--bcn);display:flex;flex-direction:column;position:fixed;top:0;left:0;bottom:0;z-index:200;overflow-y:auto}
.content{margin-left:256px;flex:1;min-height:100vh;display:flex;flex-direction:column}
.main{padding:32px;flex:1}
.sec{display:none}.sec.on{display:block}

/* SIDEBAR */
.sbrand{padding:24px 20px 16px;border-bottom:1px solid var(--br)}
.spill{display:inline-flex;align-items:center;gap:5px;background:var(--cdim);border:1px solid var(--cb);border-radius:20px;padding:3px 10px;font-size:10px;color:var(--cyan);letter-spacing:1.4px;text-transform:uppercase;margin-bottom:10px}
.stitle{font-size:15px;font-weight:800;color:var(--wt);letter-spacing:-.3px}
.ssub{font-size:11px;color:var(--mu);margin-top:3px}
.snav{padding:10px 0;flex:1}
.slabel{font-size:9px;color:var(--di);letter-spacing:1.5px;text-transform:uppercase;padding:14px 20px 5px}
.sitem{display:flex;align-items:center;gap:11px;padding:10px 20px;cursor:pointer;color:var(--mu);font-size:13px;font-weight:500;border-left:3px solid transparent;transition:all .18s}
.sitem:hover{background:var(--cdim);color:var(--wt)}
.sitem.on{background:var(--cdim);color:var(--cyan);border-left-color:var(--cyan)}
.sico{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.sbadge{margin-left:auto;background:var(--red);color:#fff;font-size:10px;border-radius:10px;padding:2px 7px;min-width:20px;text-align:center}
.sbadge.a{background:var(--amb);color:#000}
.sfooter{padding:14px 20px;border-top:1px solid var(--br);font-size:10px;color:var(--di);line-height:1.6}

/* PAGE HEADER */
.ph{margin-bottom:26px}
.ptitle{font-size:24px;font-weight:900;letter-spacing:-.5px}
.ptitle em{color:var(--cyan);font-style:normal}
.psub{font-size:13px;color:var(--mu);margin-top:6px;max-width:680px}

/* CARDS */
.card{background:var(--s1);border:1px solid var(--bcn);border-radius:var(--rad);padding:22px;margin-bottom:18px}
.ch{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
.ct{font-size:14px;font-weight:700;display:flex;align-items:center;gap:8px}
.ct .ci{color:var(--cyan)}

/* STATS */
.sg{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:14px;margin-bottom:22px}
.sc{background:var(--s2);border:1px solid var(--bcn);border-radius:var(--rad);padding:18px}
.sc.r .sv{color:var(--red)}.sc.g .sv{color:var(--grn)}.sc.a .sv{color:var(--amb)}.sc.go .sv{color:var(--gold)}
.sl{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:1px;margin-bottom:7px}
.sv{font-size:26px;font-weight:900;color:var(--cyan);line-height:1}
.ss{font-size:11px;color:var(--mu);margin-top:3px}

/* GRIDS */
.g2{display:grid;grid-template-columns:1fr 1fr;gap:18px}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:14px}

/* FORMS */
.fg{margin-bottom:14px}
.fl{display:block;font-size:11px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.8px;margin-bottom:5px}
.fi,.fsel,.fta{width:100%;background:var(--s2);border:1px solid var(--bcn);border-radius:var(--rads);padding:9px 13px;color:var(--wt);font-size:13px;font-family:inherit;transition:border-color .18s}
.fi:focus,.fsel:focus,.fta:focus{outline:none;border-color:var(--cyan);box-shadow:0 0 0 3px var(--cdim)}
.fsel option{background:var(--s2)}
.fta{resize:vertical;min-height:72px}
.fr{display:grid;grid-template-columns:1fr 1fr;gap:11px}
.fr3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:11px}

/* BUTTONS */
.btn{display:inline-flex;align-items:center;gap:7px;padding:9px 18px;border-radius:var(--rads);border:none;cursor:pointer;font-size:13px;font-weight:600;font-family:inherit;transition:all .18s;text-decoration:none}
.bp{background:var(--cyan);color:#000}.bp:hover{background:#20E5FF;transform:translateY(-1px);box-shadow:0 4px 16px rgba(0,207,255,.35)}
.bs{background:var(--s2);color:var(--wt);border:1px solid var(--bcn)}.bs:hover{background:var(--s3);border-color:var(--cyan)}
.bd{background:var(--rdim);color:var(--red);border:1px solid rgba(255,75,110,.3)}.bd:hover{background:var(--red);color:#fff}
.bgo{background:var(--gdim);color:var(--gold);border:1px solid var(--gb)}.bgo:hover{background:var(--gold);color:#000}
.bgrn{background:var(--grdim);color:var(--grn);border:1px solid var(--grb)}.bgrn:hover{background:var(--grn);color:#000}
.btn.sm{padding:5px 11px;font-size:11px}

/* TABLE */
.tc{overflow-x:auto;border-radius:var(--rad);border:1px solid var(--bcn)}
table{width:100%;border-collapse:collapse}
thead th{background:var(--s2);padding:11px 14px;text-align:left;font-size:10px;font-weight:700;color:var(--mu);text-transform:uppercase;letter-spacing:.8px;border-bottom:1px solid var(--bcn);white-space:nowrap}
tbody tr{border-bottom:1px solid var(--br);transition:background .12s}
tbody tr:hover{background:var(--s2)}
tbody tr:last-child{border-bottom:none}
tbody td{padding:11px 14px;font-size:13px;vertical-align:middle}
.tm{color:var(--mu);font-size:12px}

/* BADGES */
.badge{display:inline-flex;align-items:center;padding:3px 9px;border-radius:20px;font-size:11px;font-weight:600}
.bg{background:var(--grdim);color:var(--grn);border:1px solid var(--grb)}
.br2{background:var(--rdim);color:var(--red);border:1px solid rgba(255,75,110,.3)}
.ba{background:var(--adim);color:var(--amb);border:1px solid rgba(245,158,11,.28)}
.bc{background:var(--cdim);color:var(--cyan);border:1px solid var(--cb)}
.bgo2{background:var(--gdim);color:var(--gold);border:1px solid var(--gb)}

/* ALERTS */
.alert{border-radius:var(--rads);padding:13px 15px;margin-bottom:14px;font-size:13px;display:flex;gap:10px;align-items:flex-start;line-height:1.5}
.ai{font-size:16px;flex-shrink:0;margin-top:1px}
.ac{background:var(--cdim);border:1px solid var(--cb);color:#9EE8FF}
.ar{background:var(--rdim);border:1px solid rgba(255,75,110,.3);color:#FF8FA3}
.ag{background:var(--grdim);border:1px solid var(--grb);color:var(--grn)}
.aa{background:var(--adim);border:1px solid rgba(245,158,11,.28);color:var(--amb)}
.ago{background:var(--gdim);border:1px solid var(--gb);color:var(--gold)}

/* PROGRESS */
.pb{height:6px;background:var(--s3);border-radius:3px;overflow:hidden;margin-top:5px}
.pf{height:100%;border-radius:3px;background:linear-gradient(90deg,var(--cyan),#0080FF);transition:width .6s ease}
.pf.g{background:var(--grn)}.pf.r{background:var(--red)}.pf.a{background:var(--amb)}

/* INNER TABS */
.itabs{display:flex;gap:3px;background:var(--s2);border-radius:10px;padding:4px;margin-bottom:18px;width:fit-content}
.itab{padding:7px 16px;border-radius:8px;font-size:12px;font-weight:600;cursor:pointer;color:var(--mu);transition:all .18s;border:none;background:transparent;font-family:inherit}
.itab.on{background:var(--cyan);color:#000}
.ipanel{display:none}.ipanel.on{display:block}

/* SCORE RING */
.sring{width:140px;height:140px;position:relative;margin:0 auto 14px}
.sring svg{transform:rotate(-90deg)}
.snum{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.sbig{font-size:34px;font-weight:900;line-height:1}
.ssmall{font-size:10px;color:var(--mu);text-transform:uppercase;letter-spacing:1px}

/* QUIZ */
.qi{background:var(--s2);border:1px solid var(--br);border-radius:var(--rad);padding:15px;margin-bottom:10px}
.qt{font-size:13px;color:var(--wt);margin-bottom:11px;line-height:1.4;font-weight:500}
.qopts{display:flex;flex-wrap:wrap;gap:7px}
.qbtn{padding:6px 13px;border-radius:20px;border:1px solid var(--bcn);background:transparent;color:var(--mu);font-size:12px;cursor:pointer;font-family:inherit;transition:all .15s}
.qbtn:hover{border-color:var(--cyan);color:var(--wt)}
.qbtn.on{background:var(--cyan);border-color:var(--cyan);color:#000;font-weight:700}

/* RISK GRID */
.rg{display:grid;grid-template-columns:repeat(auto-fill,minmax(195px,1fr));gap:11px}
.rc{background:var(--s2);border:1px solid var(--br);border-radius:var(--rad);padding:15px;cursor:pointer;transition:all .18s}
.rc:hover{border-color:var(--bcn);background:var(--s3)}
.rc.exp{border-color:var(--cyan)}
.rdots{display:flex;gap:4px;margin-bottom:7px}
.rd{width:7px;height:7px;border-radius:50%;background:var(--s3)}
.rdh{background:var(--red)}.rdm{background:var(--amb)}.rdl{background:var(--grn)}
.rname{font-size:13px;font-weight:700;margin-bottom:3px}
.rsum{font-size:11px;color:var(--mu)}
.rdet{display:none;margin-top:11px;padding-top:11px;border-top:1px solid var(--br)}
.rdet.on{display:block}
.rtip{font-size:12px;color:var(--mu);margin-bottom:5px;padding-left:13px;position:relative;line-height:1.4}
.rtip::before{content:'→';position:absolute;left:0;color:var(--cyan)}

/* PROTOCOL CARD */
.pcard{background:var(--s2);border:1px solid var(--br);border-radius:var(--rad);padding:18px;margin-bottom:11px}
.phdr{display:flex;align-items:center;gap:12px;margin-bottom:13px}
.pico{width:40px;height:40px;background:var(--cdim);border:1px solid var(--cb);border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
.pname{font-size:15px;font-weight:700}
.prisk{font-size:11px;margin-top:2px}
.psteps{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.ps{background:var(--bg);border-radius:var(--rads);padding:9px 11px}
.psl{font-size:9px;color:var(--di);text-transform:uppercase;letter-spacing:1px;margin-bottom:3px}
.psv{font-size:12px;color:var(--wt);font-weight:600;line-height:1.3}

/* SCRIPTS */
.scard{background:var(--s2);border:1px solid var(--br);border-radius:var(--rad);overflow:hidden;margin-bottom:10px}
.shdr{padding:13px 15px;display:flex;align-items:center;justify-content:space-between;cursor:pointer;transition:background .15s}
.shdr:hover{background:var(--s3)}
.stit{font-size:13px;font-weight:600}
.sbdy{display:none;padding:0 15px 15px}
.sbdy.on{display:block}
.stxt{background:var(--bg);border-radius:var(--rads);padding:15px;font-size:13px;color:var(--mu);line-height:1.7;border-left:3px solid var(--cyan);white-space:pre-line}

/* CHECKLIST */
.cli{display:flex;align-items:flex-start;gap:12px;padding:10px 0;border-bottom:1px solid var(--br)}
.cli:last-child{border-bottom:none}
.ck{width:18px;height:18px;min-width:18px;border:2px solid var(--bcn);border-radius:4px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .15s;margin-top:2px;font-size:11px;color:transparent}
.ck.on{background:var(--cyan);border-color:var(--cyan);color:#000}
.clt{font-size:13px;line-height:1.4}
.cls{font-size:11px;color:var(--mu);margin-top:2px}

/* SAVINGS WIN */
.sw{display:flex;align-items:center;gap:15px;background:var(--s2);border-radius:var(--rad);padding:13px 15px;margin-bottom:9px;border:1px solid var(--br)}
.samt{font-size:20px;font-weight:900;color:var(--grn);white-space:nowrap}
.sdet{flex:1}
.stitle2{font-size:13px;font-weight:600}
.smeta{font-size:11px;color:var(--mu);margin-top:2px}

/* COUNTDOWN PILL */
.cp{display:inline-flex;align-items:center;gap:5px;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700}
.cpu{background:var(--rdim);color:var(--red);border:1px solid rgba(255,75,110,.3)}
.cps{background:var(--adim);color:var(--amb);border:1px solid rgba(245,158,11,.28)}
.cpo{background:var(--grdim);color:var(--grn);border:1px solid var(--grb)}

/* TIP GRID */
.tg{display:grid;grid-template-columns:1fr 1fr;gap:9px}
.ti{background:var(--bg);border:1px solid var(--br);border-radius:var(--rads);padding:12px}
.tc2{font-size:10px;color:var(--cyan);text-transform:uppercase;letter-spacing:1px;margin-bottom:4px}
.tv{font-size:12px;line-height:1.45}

/* EMPTY STATE */
.empty{text-align:center;padding:48px 20px}
.ei{font-size:44px;margin-bottom:13px;opacity:.35}
.et{font-size:15px;font-weight:600;color:var(--mu);margin-bottom:6px}
.es{font-size:12px;color:var(--di)}

/* MODALS */
.mo{position:fixed;inset:0;background:rgba(0,0,0,.72);z-index:1000;display:none;align-items:center;justify-content:center;padding:20px}
.mo.on{display:flex}
.md{background:var(--s1);border:1px solid var(--bcn);border-radius:var(--radl);padding:26px;width:100%;max-width:540px;max-height:85vh;overflow-y:auto;box-shadow:0 20px 60px rgba(0,0,0,.6)}
.mhdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}
.mttl{font-size:17px;font-weight:800}
.mcl{background:none;border:none;color:var(--mu);font-size:22px;cursor:pointer;padding:2px 6px;line-height:1}
.mcl:hover{color:var(--wt)}

/* TOAST */
.toast{position:fixed;bottom:24px;right:24px;background:var(--s2);border:1px solid var(--bcn);color:var(--wt);padding:13px 17px;border-radius:var(--rad);font-size:13px;z-index:9999;display:none;align-items:center;gap:9px;box-shadow:0 8px 32px rgba(0,0,0,.4);transition:all .25s}
.toast.on{display:flex}

/* DIVIDER */
hr{border:none;border-top:1px solid var(--br);margin:18px 0}

/* DISCLAIMER BAR */
.discbar{background:var(--s1);border-top:1px solid var(--br);padding:12px 32px;font-size:10px;color:var(--di);line-height:1.6;margin-left:256px}


/* CURRENCY PICKER */
.curr-item{display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:var(--rads);cursor:pointer;transition:background .15s;border:1px solid transparent}
.curr-item:hover{background:var(--cdim);border-color:var(--cb)}
.curr-item.curr-active{background:var(--cdim);border-color:var(--cyan)}
.curr-sym{font-size:16px;font-weight:700;color:var(--cyan);width:32px;text-align:center;flex-shrink:0}
.curr-name{flex:1;font-size:13px;color:var(--wt)}
.curr-code{font-size:11px;color:var(--mu);font-family:monospace;letter-spacing:.5px}
.curr-btn{display:inline-flex;align-items:center;gap:6px;background:var(--cdim);border:1px solid var(--cb);border-radius:20px;padding:5px 12px;cursor:pointer;font-size:12px;font-weight:700;color:var(--cyan);font-family:inherit;transition:all .18s;margin-top:10px;width:100%}
.curr-btn:hover{background:var(--cb);color:var(--wt)}

/* SCROLL */
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--s3);border-radius:3px}

/* ACTION ROW */
.ar2{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:18px;align-items:center}

/* RESPONSIVE */
@media(max-width:880px){
  .sidebar{width:56px;min-width:56px}
  .sbrand,.slabel,.sitem>span:not(.sico),.sbadge,.sfooter{display:none}
  .sitem{padding:14px;justify-content:center}
  .content,.discbar{margin-left:56px}
  .g2,.g3{grid-template-columns:1fr}
  .fr,.fr3{grid-template-columns:1fr}
  .psteps{grid-template-columns:1fr}
  .tg{grid-template-columns:1fr}
}
@media print{
  .sidebar,.btn,.mo,.toast,.discbar{display:none!important}
  .content{margin-left:0}
  .sec{display:block!important}
  body{background:#fff;color:#000}
  .card,.sc,.pcard,.scard,.qi,.rc,.sw,.cli{background:#f9f9f9;border:1px solid #ddd}
}
</style>
</head>
<body>

<!-- TOAST -->
<div class="toast" id="toast"><span id="ticon">✓</span><span id="tmsg">Saved</span></div>

<!-- MODALS -->
<div class="mo" id="m-sub">
 <div class="md">
  <div class="mhdr"><div class="mttl">Add Subscription</div><button class="mcl" onclick="cm('m-sub')">✕</button></div>
  <div class="fg"><label class="fl">Service Name</label><input class="fi" id="sn" placeholder="e.g. Netflix, Adobe, Spotify…"></div>
  <div class="fr">
   <div class="fg"><label class="fl">Category</label>
    <select class="fsel" id="sc2">
     <option>Streaming</option><option>Software / SaaS</option><option>Insurance</option>
     <option>Delivery</option><option>Utilities</option><option>Mobile / Internet</option>
     <option>Gym / Fitness</option><option>News / Media</option><option>Cloud Storage</option>
     <option>Gaming</option><option>Other</option>
    </select></div>
   <div class="fg"><label class="fl">Monthly Cost ($)</label><input class="fi" id="scost" type="number" step="0.01" placeholder="0.00"></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Your Sign-Up Price ($)</label><input class="fi" id="sorig" type="number" step="0.01" placeholder="What you paid at start"></div>
   <div class="fg"><label class="fl">New-Customer Price Today ($)</label><input class="fi" id="snew" type="number" step="0.01" placeholder="Check in private window"></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Date Joined</label><input class="fi" id="sjoin" type="date"></div>
   <div class="fg"><label class="fl">Payment Method</label>
    <select class="fsel" id="spay">
     <option>Rewards Credit Card</option><option>Regular Credit Card</option>
     <option>Debit Card</option><option>PayPal</option><option>Prepaid Card</option>
     <option>Bank Transfer</option>
    </select></div>
  </div>
  <div class="fg"><label class="fl">Notes (bundle details, usage level…)</label><textarea class="fta" id="snote" placeholder="e.g. Part of family plan, includes delivery, rarely use premium features…"></textarea></div>
  <div class="ar2" style="justify-content:flex-end"><button class="btn bs" onclick="cm('m-sub')">Cancel</button><button class="btn bp" onclick="addSub()">Add Subscription</button></div>
 </div>
</div>

<div class="mo" id="m-price">
 <div class="md">
  <div class="mhdr"><div class="mttl">Log a Price Check</div><button class="mcl" onclick="cm('m-price')">✕</button></div>
  <div class="fg"><label class="fl">What You Searched</label><input class="fi" id="pi" placeholder="e.g. Flight NYC → LA, Nov 14 · Hotel downtown Chicago 2 nights"></div>
  <div class="fr">
   <div class="fg"><label class="fl">Date</label><input class="fi" id="pd" type="date"></div>
   <div class="fg"><label class="fl">Time of Day</label>
    <select class="fsel" id="pt">
     <option>Morning (6am–10am)</option><option>Midday (10am–2pm)</option>
     <option>Afternoon (2pm–6pm)</option><option>Evening (6pm–10pm)</option><option>Late Night</option>
    </select></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Device Used</label>
    <select class="fsel" id="pdev">
     <option>Laptop / Desktop</option><option>Mobile App</option>
     <option>Mobile Browser</option><option>Tablet</option><option>Public / Library Computer</option>
    </select></div>
   <div class="fg"><label class="fl">Session Mode</label>
    <select class="fsel" id="pmode">
     <option>Normal — Logged In</option><option>Normal — Logged Out</option>
     <option>Incognito / Private</option><option>VPN Active</option><option>VPN + Incognito</option>
    </select></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Price Shown ($)</label><input class="fi" id="pamt" type="number" step="0.01" placeholder="0.00"></div>
   <div class="fg"><label class="fl">Category</label>
    <select class="fsel" id="pcat">
     <option>Flight</option><option>Hotel</option><option>Insurance</option>
     <option>Streaming</option><option>Retail</option><option>Rideshare</option>
     <option>Grocery / Delivery</option><option>Software</option><option>Event Ticket</option><option>Other</option>
    </select></div>
  </div>
  <div class="fg"><label class="fl">Notes — What felt off? Same item, different price?</label><textarea class="fta" id="pnote" placeholder="e.g. Same flight was $287 yesterday. Incognito showed $298 vs $341 logged in."></textarea></div>
  <div class="ar2" style="justify-content:flex-end"><button class="btn bs" onclick="cm('m-price')">Cancel</button><button class="btn bp" onclick="addPrice()">Save Price Log</button></div>
 </div>
</div>

<div class="mo" id="m-neg">
 <div class="md">
  <div class="mhdr"><div class="mttl">Log Negotiation Attempt</div><button class="mcl" onclick="cm('m-neg')">✕</button></div>
  <div class="fr">
   <div class="fg"><label class="fl">Company / Service</label><input class="fi" id="nc" placeholder="e.g. Netflix"></div>
   <div class="fg"><label class="fl">Date</label><input class="fi" id="nd" type="date"></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Before ($/mo)</label><input class="fi" id="nb" type="number" step="0.01" placeholder="0.00"></div>
   <div class="fg"><label class="fl">After ($/mo)</label><input class="fi" id="na" type="number" step="0.01" placeholder="0.00 if won"></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Method</label>
    <select class="fsel" id="nm">
     <option>Phone Call</option><option>Live Chat</option><option>Email</option>
     <option>Cancellation Threat</option><option>Competitor Quote</option>
     <option>Loyalty / Long-Term Customer Argument</option><option>Combination</option>
    </select></div>
   <div class="fg"><label class="fl">Outcome</label>
    <select class="fsel" id="no">
     <option value="Won">✅ Won — Price Reduced</option>
     <option value="Partial">🟡 Partial — Some Benefit</option>
     <option value="Lost">❌ Lost — No Change</option>
     <option value="Cancelled">🚪 Cancelled Service</option>
    </select></div>
  </div>
  <div class="fg"><label class="fl">What worked / what they said</label><textarea class="fta" id="nnote" placeholder="e.g. Mentioned competitor price, they offered 3 months at new-customer rate."></textarea></div>
  <div class="ar2" style="justify-content:flex-end"><button class="btn bs" onclick="cm('m-neg')">Cancel</button><button class="btn bp" onclick="addNeg()">Log Negotiation</button></div>
 </div>
</div>

<div class="mo" id="m-ren">
 <div class="md">
  <div class="mhdr"><div class="mttl">Track a Renewal</div><button class="mcl" onclick="cm('m-ren')">✕</button></div>
  <div class="fr">
   <div class="fg"><label class="fl">Service / Policy Name</label><input class="fi" id="rn" placeholder="e.g. Home Insurance Annual"></div>
   <div class="fg"><label class="fl">Renewal Date</label><input class="fi" id="rd" type="date"></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Annual Cost ($)</label><input class="fi" id="rc" type="number" step="0.01" placeholder="0.00"></div>
   <div class="fg"><label class="fl">Category</label>
    <select class="fsel" id="rcat">
     <option>Home Insurance</option><option>Auto Insurance</option><option>Health Insurance</option>
     <option>Life Insurance</option><option>Software Annual Plan</option>
     <option>Streaming Annual</option><option>Membership</option>
     <option>Internet / Phone Contract</option><option>Domain / Hosting</option><option>Other Contract</option>
    </select></div>
  </div>
  <div class="fg"><label class="fl">Notes / Past Negotiation Results</label><textarea class="fta" id="rnote" placeholder="e.g. Last year got 12% off by calling 10 days before. Ask for loyalty rate."></textarea></div>
  <div class="ar2" style="justify-content:flex-end"><button class="btn bs" onclick="cm('m-ren')">Cancel</button><button class="btn bp" onclick="addRen()">Track Renewal</button></div>
 </div>
</div>

<div class="mo" id="m-sav">
 <div class="md">
  <div class="mhdr"><div class="mttl">Log a Win</div><button class="mcl" onclick="cm('m-sav')">✕</button></div>
  <div class="fr">
   <div class="fg"><label class="fl">What You Saved On</label><input class="fi" id="svn" placeholder="e.g. Car insurance, Netflix subscription"></div>
   <div class="fg"><label class="fl">Date</label><input class="fi" id="svd" type="date"></div>
  </div>
  <div class="fr">
   <div class="fg"><label class="fl">Was Paying ($ total or /mo)</label><input class="fi" id="svb" type="number" step="0.01" placeholder="0.00"></div>
   <div class="fg"><label class="fl">Now Paying</label><input class="fi" id="sva" type="number" step="0.01" placeholder="0.00"></div>
  </div>
  <div class="fg"><label class="fl">How You Did It</label>
   <select class="fsel" id="svm">
    <option>Negotiated by phone</option><option>Used competitor quote</option>
    <option>Threatened to cancel</option><option>Switched provider</option>
    <option>Cancelled unused service</option><option>Changed device/session for better price</option>
    <option>Timed purchase to off-peak</option><option>Unpacked a bundle — removed dead weight</option>
    <option>Rejoined as new customer</option><option>Caught a silent price increase</option><option>Other</option>
   </select></div>
  <div class="ar2" style="justify-content:flex-end"><button class="btn bs" onclick="cm('m-sav')">Cancel</button><button class="btn bp" onclick="addSav()">Log This Win</button></div>
 </div>
</div>


<div class="mo" id="m-currency">
 <div class="md" style="max-width:480px">
  <div class="mhdr"><div class="mttl">Select Your Currency</div><button class="mcl" onclick="cm('m-currency')">✕</button></div>
  <div class="fg" style="margin-bottom:12px">
   <input class="fi" id="curr-search" placeholder="Search by name or code (e.g. Euro, GBP, INR)…" oninput="renderCurrencyPicker(this.value)" autocomplete="off">
  </div>
  <div id="curr-list" style="max-height:380px;overflow-y:auto;display:flex;flex-direction:column;gap:4px"></div>
 </div>
</div>

<!-- SIDEBAR -->
<aside class="sidebar">
 <div class="sbrand">
  <div class="spill">⚡ Audit Platform</div>
  <div class="stitle">Pricing Audit</div>
  <div class="ssub">Journey of Insight</div>
 </div>
 <nav class="snav">
  <div class="slabel">Overview</div>
  <div class="sitem on" onclick="nav('dash',this)"><span class="sico">🏠</span><span>Dashboard</span></div>
  <div class="slabel">Audit Tools</div>
  <div class="sitem" onclick="nav('subs',this)"><span class="sico">💳</span><span>Subscription Autopsy</span><span class="sbadge a" id="b-subs">0</span></div>
  <div class="sitem" onclick="nav('price',this)"><span class="sico">📊</span><span>Price Intelligence</span></div>
  <div class="sitem" onclick="nav('score',this)"><span class="sico">🧠</span><span>Profiling Score</span></div>
  <div class="slabel">Defence</div>
  <div class="sitem" onclick="nav('disrupt',this)"><span class="sico">🛡️</span><span>Disruption Protocol</span></div>
  <div class="sitem" onclick="nav('neg',this)"><span class="sico">💬</span><span>Negotiation Hub</span></div>
  <div class="sitem" onclick="nav('risk',this)"><span class="sico">⚠️</span><span>Risk Map</span></div>
  <div class="slabel">Tracking</div>
  <div class="sitem" onclick="nav('ren',this)"><span class="sico">📅</span><span>Renewal War Room</span><span class="sbadge" id="b-ren" style="display:none">!</span></div>
  <div class="sitem" onclick="nav('savs',this)"><span class="sico">💰</span><span>Savings Ledger</span></div>
  <div class="slabel">Data</div>
  <div class="sitem" onclick="nav('exp',this)"><span class="sico">📋</span><span>Export & Backup</span></div>
 </nav>
 <div class="sfooter"><button class="curr-btn" onclick="document.getElementById('curr-search').value='';renderCurrencyPicker();om('m-currency')"><span id="curr-display">$ USD</span> <span style="margin-left:auto;opacity:.5">▼</span></button><div style="margin-top:8px">© Journey of Insight<br>Educational use only · Not financial advice</div></div>
</aside>

<!-- MAIN CONTENT -->
<div class="content">
<main class="main">

<!-- DASHBOARD -->
<section id="s-dash" class="sec on">
 <div class="ph"><div class="ptitle">Your <em>Financial</em> Control Centre</div><div class="psub">Everything you're paying, everything you're overpaying, and the tools to close the gap. Start at the top and work down.</div></div>
 <div class="sg" id="dstats">
  <div class="sc r"><div class="sl">Monthly Subscriptions</div><div class="sv" id="d-mo">$0</div><div class="ss">Per year: <span id="d-yr">$0</span></div></div>
  <div class="sc a"><div class="sl">Estimated Overpayment</div><div class="sv" id="d-over">$0/mo</div><div class="ss">vs. what new customers pay today</div></div>
  <div class="sc g"><div class="sl">Total Savings Logged</div><div class="sv" id="d-saved">$0</div><div class="ss">Money reclaimed to date</div></div>
  <div class="sc"><div class="sl">Renewals Due ≤ 30 Days</div><div class="sv" id="d-ren">0</div><div class="ss">Needing your attention now</div></div>
 </div>
 <div class="g2">
  <div class="card">
   <div class="ch"><div class="ct"><span class="ci">🚀</span> First-Time Setup</div></div>
   <div id="setup-cl">
    <div class="cli"><div class="ck" id="ck1" onclick="toggleCk(this,'ck1')"></div><div><div class="clt">Add all your subscriptions to the Subscription Autopsy</div><div class="cls">Include the new-customer price for each — this instantly shows your invisible tax.</div></div></div>
    <div class="cli"><div class="ck" id="ck2" onclick="toggleCk(this,'ck2')"></div><div><div class="clt">Complete your Profiling Score questionnaire</div><div class="cls">Understand how precisely the algorithm can currently target you.</div></div></div>
    <div class="cli"><div class="ck" id="ck3" onclick="toggleCk(this,'ck3')"></div><div><div class="clt">Add all annual renewals to the Renewal War Room</div><div class="cls">Insurance, annual plans, contracts — all of them. Act 14 days before each date.</div></div></div>
    <div class="cli"><div class="ck" id="ck4" onclick="toggleCk(this,'ck4')"></div><div><div class="clt">Read the Category Risk Map and identify your highest-risk spending</div><div class="cls">Flights and insurance are most aggressively targeted. Know before you buy.</div></div></div>
    <div class="cli"><div class="ck" id="ck5" onclick="toggleCk(this,'ck5')"></div><div><div class="clt">Make your first negotiation call this week</div><div class="cls">Start with the subscription you've had longest. Use the scripts in the Negotiation Hub.</div></div></div>
   </div>
  </div>
  <div class="card">
   <div class="ch"><div class="ct"><span class="ci">💡</span> Facts Most People Never Check</div></div>
   <div class="alert ac"><span class="ai">⚡</span><span><strong>Renewal customers pay 15–40% more</strong> than new customers for identical services. Companies rely entirely on your inertia. This platform fights inertia.</span></div>
   <div class="alert ar"><span class="ai">📱</span><span><strong>Mobile app prices run 8–23% higher</strong> than the same item on a desktop browser. Use the Disruption Protocol before every in-app purchase over $15.</span></div>
   <div class="alert ago"><span class="ai">🏆</span><span><strong>Loyalty membership signals price tolerance</strong> to the algorithm. Your rewards points may be costing you more in dynamic pricing premiums than they earn you back.</span></div>
   <div class="alert aa"><span class="ai">⏰</span><span><strong>Best time to negotiate: Tuesday–Thursday, 10am–2pm.</strong> Retention agents have more authority and more time. Evening and Monday calls close at lower rates.</span></div>
  </div>
 </div>
 <div class="card">
  <div class="ch"><div class="ct"><span class="ci">📋</span> Subscription Snapshot</div><button class="btn bs sm" onclick="navTo('subs')">Full Autopsy →</button></div>
  <div id="d-subprev"><div class="empty"><div class="ei">💳</div><div class="et">No subscriptions added yet</div><div class="es">Go to Subscription Autopsy to begin your audit.</div></div></div>
 </div>
</section>

<!-- SUBSCRIPTION AUTOPSY -->
<section id="s-subs" class="sec">
 <div class="ph"><div class="ptitle">Subscription <em>Autopsy</em></div><div class="psub">Every recurring charge — and what a new customer pays for the same thing today. The difference is your monthly invisible tax.</div></div>
 <div class="alert ac"><span class="ai">💡</span><span><strong>How to find the new-customer price:</strong> Open a private/incognito browser window, visit the service website <em>without logging in</em>, and check the price for new sign-ups. That is the number to enter here.</span></div>
 <div class="ar2">
  <button class="btn bp" onclick="om('m-sub')">+ Add Subscription</button>
  <button class="btn bs" onclick="exportSubsCSV()">⬇ Export CSV</button>
 </div>
 <div class="sg">
  <div class="sc"><div class="sl">Monthly Total</div><div class="sv" id="ss-mo">$0</div></div>
  <div class="sc r"><div class="sl">Overpaying vs New Customer</div><div class="sv" id="ss-over">$0/mo</div><div class="ss" id="ss-overyr"></div></div>
  <div class="sc a"><div class="sl">Silent Price Increases Detected</div><div class="sv" id="ss-sil">0</div><div class="ss">vs. your original sign-up price</div></div>
  <div class="sc g"><div class="sl">Subscriptions Tracked</div><div class="sv" id="ss-cnt">0</div></div>
 </div>
 <div class="tc" id="sub-wrap">
  <table><thead><tr><th>Service</th><th>Category</th><th>You Pay/mo</th><th>New Customer Today</th><th>Overpay/mo</th><th>Silent Increase?</th><th>Status</th><th>Del</th></tr></thead>
  <tbody id="sub-tb"><tr><td colspan="8"><div class="empty"><div class="ei">📋</div><div class="et">No subscriptions yet</div><div class="es">Click "Add Subscription" to begin.</div></div></td></tr></tbody></table>
 </div>
 <div class="card" style="margin-top:18px">
  <div class="ct" style="margin-bottom:12px"><span class="ci">🧩</span> Bundle Toxicity Check</div>
  <div class="psub" style="margin-bottom:14px">Bundles hide dead weight. If a subscription is part of a bundle, list below what you actually use versus what you're paying for. Use this as negotiation ammunition.</div>
  <div class="alert aa"><span class="ai">⚠️</span><span>If you use less than 60% of what a bundle provides, you have negotiation leverage. Call and say: <em>"I'm only using X feature — can we move me to a plan that matches what I actually use?"</em> Companies frequently comply rather than lose you entirely.</span></div>
  <div class="tg">
   <div class="ti"><div class="tc2">Streaming bundles</div><div class="tv">Check if you're on a tier that includes 4K/HDR you never use, or audio features on music services that serve your use case. Downgrade requests are rarely declined.</div></div>
   <div class="ti"><div class="tc2">Software / SaaS</div><div class="tv">Professional tiers often include team features, API access, and storage you don't use. A lower tier may serve identical needs at 40–60% of the cost.</div></div>
   <div class="ti"><div class="tc2">Delivery memberships</div><div class="tv">Calculate whether you actually order often enough to justify the annual fee vs. paying per delivery. Many people break even or lose money on these memberships.</div></div>
   <div class="ti"><div class="tc2">Telecom bundles</div><div class="tv">Phone + Internet + TV bundles frequently include channels watched for less than 2 hours a month. Unbundle and rebuild only what you use. The savings are usually significant.</div></div>
  </div>
 </div>
</section>

<!-- PRICE INTELLIGENCE -->
<section id="s-price" class="sec">
 <div class="ph"><div class="ptitle">Price <em>Intelligence</em> Log</div><div class="psub">Track prices across devices, sessions, and times of day. Patterns in your own log reveal whether you're being individually targeted — and by how much.</div></div>
 <div class="alert ar"><span class="ai">🔍</span><span><strong>The exposure test — run it now:</strong> Search the same item on (1) your regular browser while logged in, (2) incognito mode logged out, (3) a completely different device. Price differences above 5% confirm active profiling. Log all three here.</span></div>
 <div class="ar2"><button class="btn bp" onclick="om('m-price')">+ Log a Price Check</button></div>
 <div class="tc">
  <table><thead><tr><th>Item</th><th>Date</th><th>Time</th><th>Device</th><th>Mode</th><th>Price</th><th>Category</th><th>Del</th></tr></thead>
  <tbody id="price-tb"><tr><td colspan="8"><div class="empty"><div class="ei">📊</div><div class="et">No price logs yet</div><div class="es">Start logging prices to spot patterns over time.</div></div></td></tr></tbody></table>
 </div>
 <div class="card" style="margin-top:18px">
  <div class="ct" style="margin-bottom:12px"><span class="ci">⏰</span> Know Your Expensive Hours</div>
  <div class="psub" style="margin-bottom:14px">Use your price logs to identify when prices are highest for you specifically. Your personal data reveals more than any general guide.</div>
  <div class="tg">
   <div class="ti"><div class="tc2">Evening Browsing Risk</div><div class="tv">Prices are commonly highest 7–10pm when purchase-intent data shows people are most relaxed and impulsive. Log your prices at different times to verify your personal pattern.</div></div>
   <div class="ti"><div class="tc2">The Monday Penalty</div><div class="tv">Travel and hotel prices spike Monday–Tuesday when people plan weekend trips at work. The algorithm anticipates demand surges. Wednesday–Thursday searches return lower baseline prices.</div></div>
   <div class="ti"><div class="tc2">The App vs Browser Gap</div><div class="tv">Log the same purchase in your mobile app AND a desktop browser. For flights and hotels, the gap frequently runs 5–23%. Quantify your personal app tax.</div></div>
   <div class="ti"><div class="tc2">The Return Visit Tax</div><div class="tv">Prices often rise after your second or third visit to the same page within the same session. This is retargeting pricing in action. Log first-visit vs. revisit prices to measure it.</div></div>
   <div class="ti"><div class="tc2">Wishlist Surveillance</div><div class="tv">Saving items to platform wishlists signals intent and can trigger price increases on those specific items. Keep a private notepad list instead — no data leakage.</div></div>
   <div class="ti"><div class="tc2">Weather / Event Surges</div><div class="tv">Insurance quotes spike after local weather events. Rideshare surges near concerts and stadiums. These are predictable — anticipate and shop before the trigger event, not during.</div></div>
  </div>
 </div>
</section>

<!-- PROFILING SCORE -->
<section id="s-score" class="sec">
 <div class="ph"><div class="ptitle">Your <em>Profiling Score</em></div><div class="psub">How precisely can pricing algorithms read you right now? Answer honestly — this is about understanding your exposure so you can reduce it.</div></div>
 <div class="g2">
  <div><div id="quiz-qs"></div><button class="btn bp" onclick="calcScore()" style="margin-top:6px">Calculate My Score</button></div>
  <div>
   <div class="card" style="text-align:center">
    <div class="ct" style="justify-content:center;margin-bottom:18px"><span class="ci">🧠</span> Profiling Exposure Score</div>
    <div class="sring">
     <svg width="140" height="140" viewBox="0 0 140 140">
      <circle cx="70" cy="70" r="56" fill="none" stroke="#111D30" stroke-width="14"/>
      <circle cx="70" cy="70" r="56" fill="none" stroke="#00CFFF" stroke-width="14" stroke-dasharray="351.86" id="sarc" stroke-dashoffset="351.86" stroke-linecap="round"/>
     </svg>
     <div class="snum"><div class="sbig" id="sdisp">–</div><div class="ssmall">/ 100</div></div>
    </div>
    <div id="slbl" style="font-size:13px;color:var(--mu);margin-bottom:14px">Answer the questions to see your score</div>
    <div id="sbrkdwn" style="text-align:left"></div>
   </div>
   <div class="card" id="srecs" style="display:none">
    <div class="ct" style="margin-bottom:12px"><span class="ci">🛡️</span> Your Priority Actions</div>
    <div id="sreclist"></div>
   </div>
  </div>
 </div>
</section>

<!-- DISRUPTION PROTOCOL -->
<section id="s-disrupt" class="sec">
 <div class="ph"><div class="ptitle">Disruption <em>Protocol</em></div><div class="psub">Category-specific steps to break your data profile. No single action defeats the system — consistent friction across sessions degrades the model's confidence in you over time.</div></div>
 <div class="alert ac"><span class="ai">⚡</span><span><strong>The core principle:</strong> Algorithms need a stable, consistent picture of you to price precisely. Vary your device, session mode, timing, and account status enough, and the model defaults to a more generic — and cheaper — price.</span></div>
 <div id="proto-list"></div>
 <div class="card">
  <div class="ct" style="margin-bottom:14px"><span class="ci">🚨</span> Urgency Masking — When You Genuinely Need It Now</div>
  <div class="psub" style="margin-bottom:14px">Sometimes you cannot wait. Here's how to suppress urgency signals while still completing the purchase you need:</div>
  <div class="tg">
   <div class="ti"><div class="tc2">Flight — Tonight or Tomorrow</div><div class="tv">Use public WiFi (library, café) on a device not normally used for travel searches. Search 4–5 date variants even if only one works — never search only your target date alone.</div></div>
   <div class="ti"><div class="tc2">Hotel — Same Night</div><div class="tv">Call the hotel directly rather than booking through an app. Direct reservations often allow room to negotiate same-night rates — unsold rooms are worth nothing to them after midnight.</div></div>
   <div class="ti"><div class="tc2">Insurance — Gap in Cover</div><div class="tv">Request quotes from 4+ providers simultaneously. Multiple quote requests in the same window signal a competitive buyer — quotes returned are materially better than single-provider approaches.</div></div>
   <div class="ti"><div class="tc2">Renewal — Expiring This Week</div><div class="tv">Never mention the renewal is imminent. Call as if evaluating from scratch: <em>"What would it cost me to start with you?"</em> gets a different answer than <em>"My renewal is Friday."</em></div></div>
   <div class="ti"><div class="tc2">Medical / Health Supplies</div><div class="tv">Search on a device without a history of health-related browsing. Health profile data is among the most aggressively monetised for pricing. Library computer or fresh device is the safest route.</div></div>
   <div class="ti"><div class="tc2">Event Tickets — Selling Fast</div><div class="tv">Dynamic ticket pricing often drops 24–48 hours before an event as unsold inventory is offloaded. If you can wait, do. If you cannot — buy in one decisive session; return visits drive the price up.</div></div>
  </div>
 </div>
 <div class="card">
  <div class="ct" style="margin-bottom:12px"><span class="ci">🏆</span> The Loyalty Programme Paradox</div>
  <div class="alert ago"><span class="ai">⚠️</span><span>Being enrolled in a loyalty programme tells the algorithm you have a purchase history here — which the model reads as reduced price sensitivity. In plain terms: <strong>loyalty membership can raise the price you're shown.</strong> This is the opposite of what most people believe.</span></div>
  <div class="tg">
   <div class="ti"><div class="tc2">How to check if it's affecting you</div><div class="tv">Compare prices shown to your logged-in loyalty account vs. the same search in a fresh private browser session. If private mode is cheaper, your loyalty membership is costing you money.</div></div>
   <div class="ti"><div class="tc2">The reward maths most people ignore</div><div class="tv">If loyalty membership causes a 10% price premium and you earn 2% back in points, you're net –8% vs. shopping without the membership. Calculate this for your three biggest loyalty programmes.</div></div>
   <div class="ti"><div class="tc2">Wishlist trap</div><div class="tv">Platform wishlists and "save for later" features signal purchase intent directly to the pricing engine. Items you've saved are monitored — prices on them can increase based on your engagement with the listing.</div></div>
   <div class="ti"><div class="tc2">Rewards card data sharing</div><div class="tv">Many rewards credit cards sell anonymised spending data to the merchants you purchase from. This data can feed into your price profile. A regular non-rewards card reduces this data leakage significantly.</div></div>
  </div>
 </div>
</section>

<!-- NEGOTIATION HUB -->
<section id="s-neg" class="sec">
 <div class="ph"><div class="ptitle">Negotiation <em>Hub</em></div><div class="psub">Scripts that work, phrases to avoid, and a tracker for every attempt so you build your own win database over time.</div></div>
 <div class="itabs">
  <button class="itab on" onclick="itab(this,'nscripts')">Scripts</button>
  <button class="itab" onclick="itab(this,'ntracker')">Outcome Tracker</button>
  <button class="itab" onclick="itab(this,'nphrases')">Phrases & Timing</button>
 </div>
 <div id="nscripts" class="ipanel on"><div id="neg-scripts"></div></div>
 <div id="ntracker" class="ipanel">
  <div class="ar2"><button class="btn bp" onclick="om('m-neg')">+ Log Negotiation</button></div>
  <div class="sg">
   <div class="sc g"><div class="sl">Attempts Made</div><div class="sv" id="n-cnt">0</div></div>
   <div class="sc"><div class="sl">Success Rate</div><div class="sv" id="n-rate">–</div></div>
   <div class="sc go"><div class="sl">Monthly Savings Won</div><div class="sv" id="n-saved">$0</div></div>
  </div>
  <div class="tc"><table><thead><tr><th>Company</th><th>Date</th><th>Before</th><th>After</th><th>Saved/mo</th><th>Method</th><th>Outcome</th><th>Del</th></tr></thead>
  <tbody id="neg-tb"><tr><td colspan="8"><div class="empty"><div class="ei">💬</div><div class="et">No negotiations logged yet</div></div></td></tr></tbody></table></div>
 </div>
 <div id="nphrases" class="ipanel">
  <div class="g2">
   <div class="card">
    <div class="ct" style="margin-bottom:12px;color:var(--grn)">✅ Phrases That Open Doors</div>
    <div style="display:flex;flex-direction:column;gap:9px">
     <div class="ps"><div class="psl">Opening</div><div class="psv">"I've been a customer for [X] years and I value the service. But I need to talk about cost — it's become more than I can justify right now."</div></div>
     <div class="ps"><div class="psl">Competitor Mention</div><div class="psv">"I checked [Competitor] and they're offering the same tier for [$ amount]. I'd rather stay, but I can't ignore that difference."</div></div>
     <div class="ps"><div class="psl">New-Customer Rate</div><div class="psv">"Your website shows [$ amount] for new sign-ups. I've been here longer than any new customer — can you match that rate for me?"</div></div>
     <div class="ps"><div class="psl">The Productive Pause</div><div class="psv">After they offer something, say: "I appreciate that — is that the best you can do?" Then stop talking. Wait. Silence almost always produces a better offer.</div></div>
     <div class="ps"><div class="psl">Escalation Request</div><div class="psv">"I may need to cancel. Before I do that, can I speak with someone in your retention team about what options you have?"</div></div>
    </div>
   </div>
   <div class="card">
    <div class="ct" style="margin-bottom:12px;color:var(--red)">❌ Phrases That Close Doors</div>
    <div style="display:flex;flex-direction:column;gap:9px">
     <div class="ps" style="border-left:2px solid var(--red)"><div class="psl">Never Say</div><div class="psv">"My renewal is this week" — signals urgency, removes all your leverage immediately.</div></div>
     <div class="ps" style="border-left:2px solid var(--red)"><div class="psl">Never Say</div><div class="psv">"I love this service" — save enthusiasm for after you've won the negotiation.</div></div>
     <div class="ps" style="border-left:2px solid var(--red)"><div class="psl">Never Say</div><div class="psv">"I can probably afford it if I have to" — even hinting you'll pay prevents the discount from coming.</div></div>
     <div class="ps" style="border-left:2px solid var(--red)"><div class="psl">Never Say</div><div class="psv">"Is there any discount available?" — too vague. Name a specific target: "Can we get to $X per month?"</div></div>
     <div class="ps" style="border-left:2px solid var(--red)"><div class="psl">Never Say</div><div class="psv">"I just want to check my options" — signals you're not ready to act, removing urgency from their side.</div></div>
    </div>
   </div>
  </div>
  <div class="card">
   <div class="ct" style="margin-bottom:12px"><span class="ci">📅</span> When to Call for Maximum Success</div>
   <div class="tg">
    <div class="ti"><div class="tc2">Best Days</div><div class="tv">Tuesday, Wednesday, Thursday. Agents are settled, management is present, queues are shorter. Avoid Mondays (hectic) and Fridays (skeleton crews, early departures).</div></div>
    <div class="ti"><div class="tc2">Best Hours</div><div class="tv">10am–2pm in the company's timezone. Agents are past the morning rush and not yet watching the clock. Early-morning and pre-close calls underperform.</div></div>
    <div class="ti"><div class="tc2">Lead Time</div><div class="tv">Call 10–14 days before renewal. The company still needs to retain you. Day-of or post-renewal calls have near-zero leverage — they already have your money.</div></div>
    <div class="ti"><div class="tc2">Second Call Rule</div><div class="tv">If the first agent declines, hang up and call again later. Different agents have different discretion. Three calls on three different days frequently produces three different offers.</div></div>
    <div class="ti"><div class="tc2">Retention Team</div><div class="tv">Always ask to be transferred to the "retention team" or "loyalty team." These agents have specific budget authority to offer discounts that front-line agents cannot.</div></div>
    <div class="ti"><div class="tc2">Chat vs Phone</div><div class="tv">Phone calls tend to produce better outcomes because agents can make real-time decisions. Chat agents often operate from a narrower script. Use chat as a fallback, not first choice.</div></div>
   </div>
  </div>
 </div>
</section>

<!-- CATEGORY RISK MAP -->
<section id="s-risk" class="sec">
 <div class="ph"><div class="ptitle">Category <em>Risk Map</em></div><div class="psub">Not all spending is equally targeted. Know which categories the algorithms are most aggressive in — and what to do in each one. Click any card to expand.</div></div>
 <div class="alert ar"><span class="ai">⚠️</span><span><strong>High-risk categories</strong> use real-time behavioural data to set individual prices. The same item can vary by 20–60% based solely on your profile. <strong>Lower-risk categories</strong> still use pricing strategy, but it's less personalised.</span></div>
 <div class="rg" id="risk-grid"></div>
</section>

<!-- RENEWAL WAR ROOM -->
<section id="s-ren" class="sec">
 <div class="ph"><div class="ptitle">Renewal <em>War Room</em></div><div class="psub">Every contract that auto-renews is a risk. Track all of them here and act 10–14 days before each date — never after.</div></div>
 <div class="alert aa"><span class="ai">📅</span><span><strong>The negotiation window:</strong> Contact your provider 10–14 days before renewal. After renewal, your leverage falls to near zero — they have your money for another year. Before renewal, they still need yours.</span></div>
 <div class="ar2"><button class="btn bp" onclick="om('m-ren')">+ Track a Renewal</button></div>
 <div id="ren-urgent" style="margin-bottom:16px"></div>
 <div class="tc"><table><thead><tr><th>Service</th><th>Category</th><th>Renewal Date</th><th>Days Until</th><th>Annual Cost</th><th>Status</th><th>Notes</th><th>Del</th></tr></thead>
 <tbody id="ren-tb"><tr><td colspan="8"><div class="empty"><div class="ei">📅</div><div class="et">No renewals tracked yet</div><div class="es">Add insurance, annual plans, and all auto-renewing contracts.</div></div></td></tr></tbody></table></div>
</section>

<!-- SAVINGS LEDGER -->
<section id="s-savs" class="sec">
 <div class="ph"><div class="ptitle">Savings <em>Ledger</em></div><div class="psub">Every dollar you recover belongs here. The running total is the most compelling reason to keep going.</div></div>
 <div class="ar2"><button class="btn bp" onclick="om('m-sav')">+ Log a Win</button></div>
 <div class="sg">
  <div class="sc g"><div class="sl">Total Saved</div><div class="sv" id="sv-total">$0</div><div class="ss">All-time logged</div></div>
  <div class="sc"><div class="sl">Wins Logged</div><div class="sv" id="sv-cnt">0</div></div>
  <div class="sc go"><div class="sl">Average Win</div><div class="sv" id="sv-avg">$0</div></div>
  <div class="sc a"><div class="sl">Best Single Win</div><div class="sv" id="sv-best">$0</div></div>
 </div>
 <div id="savs-list"><div class="empty"><div class="ei">💰</div><div class="et">No savings logged yet</div><div class="es">When you negotiate a price down, cancel a dead subscription, or catch a silent increase — log it here.</div></div></div>
</section>

<!-- EXPORT -->
<section id="s-exp" class="sec">
 <div class="ph"><div class="ptitle">Export <em>& Backup</em></div><div class="psub">Your data lives only on this device. Export to back it up, move it between browsers, or print a full report.</div></div>
 <div class="g2">
  <div class="card">
   <div class="ct" style="margin-bottom:14px"><span class="ci">📤</span> Export Your Data</div>
   <div class="psub" style="margin-bottom:14px">All subscriptions, price logs, negotiations, renewals, and savings — exported as a single JSON file you keep.</div>
   <div class="ar2">
    <button class="btn bgo" onclick="exportPDF()" style="font-weight:800">📄 Export PDF Report</button>
    <button class="btn bp" onclick="exportJSON()">⬇ Export All (JSON)</button>
   </div>
   <div class="ar2" style="margin-top:8px">
    <button class="btn bs" onclick="exportSubsCSV()">⬇ Subscriptions (CSV)</button>
    <button class="btn bs" onclick="window.print()">🖨 Print This Page</button>
   </div>
  </div>
  <div class="card">
   <div class="ct" style="margin-bottom:14px"><span class="ci">📥</span> Import Backup</div>
   <div class="psub" style="margin-bottom:14px">Load a previously exported JSON file. <strong style="color:var(--red)">This overwrites all current data.</strong></div>
   <input type="file" id="imp-file" accept=".json" style="display:none" onchange="importJSON(event)">
   <button class="btn bs" onclick="document.getElementById('imp-file').click()">📁 Select Backup File</button>
  </div>
 </div>
 <div class="card">
  <div class="ct" style="margin-bottom:12px"><span class="ci">🔄</span> Quarterly Audit Checklist</div>
  <div class="psub" style="margin-bottom:14px">Run this every 90 days. The full process takes under 30 minutes and typically recovers far more per hour than almost any other financial task.</div>
  <div class="cli"><div class="ck" id="q1" onclick="toggleCk(this,'q1')"></div><div><div class="clt">Pull your bank/card statement — find every recurring charge from the past 3 months</div><div class="cls">Add new ones to Subscription Autopsy, remove anything cancelled.</div></div></div>
  <div class="cli"><div class="ck" id="q2" onclick="toggleCk(this,'q2')"></div><div><div class="clt">For every subscription: check what a new customer pays today in a private window</div><div class="cls">Update the "New Customer Price" column — this number changes more often than you'd expect.</div></div></div>
  <div class="cli"><div class="ck" id="q3" onclick="toggleCk(this,'q3')"></div><div><div class="clt">Call or chat the 3 biggest gaps between your price and new-customer rate</div><div class="cls">Use the scripts in the Negotiation Hub. Log every attempt — wins and losses both matter.</div></div></div>
  <div class="cli"><div class="ck" id="q4" onclick="toggleCk(this,'q4')"></div><div><div class="clt">Review the Renewal War Room for anything due in the next 60 days</div><div class="cls">Set your action plan for each: negotiate, switch provider, cancel, or accept at current rate.</div></div></div>
  <div class="cli"><div class="ck" id="q5" onclick="toggleCk(this,'q5')"></div><div><div class="clt">Retake the Profiling Score quiz — has your exposure improved since last quarter?</div><div class="cls">Track the score change over time. A downward trend means your habits are working.</div></div></div>
  <div class="cli"><div class="ck" id="q6" onclick="toggleCk(this,'q6')"></div><div><div class="clt">Log all wins from this quarter in the Savings Ledger and export a backup</div><div class="cls">The total recovered is the most compelling number in this platform. Keep it current.</div></div></div>
 </div>
 <div class="card" style="background:var(--rdim);border-color:rgba(255,75,110,.3)">
  <div class="ct" style="color:var(--red);margin-bottom:10px"><span>⚠️</span> Reset All Data</div>
  <div class="psub" style="margin-bottom:13px;color:#FF8FA3">Permanently deletes everything stored in this browser. Export a backup first.</div>
  <button class="btn bd" onclick="resetAll()">Delete All Data</button>
 </div>
 <div class="card" style="margin-top:16px;border-color:var(--br)">
  <div class="ct" style="margin-bottom:10px;color:var(--mu)">📄 Disclaimer</div>
  <div style="font-size:11px;color:var(--di);line-height:1.8">This tool is provided by <strong style="color:var(--mu)">Journey of Insight</strong> for <strong style="color:var(--mu)">educational and informational purposes only.</strong> It does not constitute financial, legal, or professional advice of any kind. All calculations are based solely on data you enter and are for personal reference. No information entered here is transmitted anywhere — all data is stored exclusively on your own device via browser localStorage. The creator is not liable for any outcomes resulting from actions based on information in this tool. Consult qualified professionals before making significant financial decisions. This tool is provided "as is" with no warranty. © Journey of Insight. All rights reserved.</div>
 </div>
</section>

</main>
<div class="discbar">Educational tool only. Not financial or legal advice. All data stored on your device only. No data is ever transmitted. © Journey of Insight.</div>
</div>

<script>
// ================================================================
// DATA
// ================================================================
const KEY='joi_audit_v2';
let D={subs:[],prices:[],negs:[],rens:[],savs:[],quiz:{},cks:{},currency:{code:'USD',symbol:'$',name:'US Dollar'},lastSaved:null};

function save(){D.lastSaved=new Date().toISOString();localStorage.setItem(KEY,JSON.stringify(D))}
function load(){try{const r=localStorage.getItem(KEY);if(r)D={...D,...JSON.parse(r)}}catch(e){}}

// ================================================================
// NAV
// ================================================================
function nav(id,el){
  document.querySelectorAll('.sec').forEach(s=>s.classList.remove('on'));
  document.querySelectorAll('.sitem').forEach(s=>s.classList.remove('on'));
  document.getElementById('s-'+id).classList.add('on');
  if(el)el.classList.add('on');
  render(id);
}



// ================================================================
// MODALS
// ================================================================
function om(id){
  const today=new Date().toISOString().split('T')[0];
  document.querySelectorAll('#'+id+' input[type=date]').forEach(f=>{if(!f.value)f.value=today});
  document.getElementById(id).classList.add('on');
}
function cm(id){document.getElementById(id).classList.remove('on')}
document.querySelectorAll('.mo').forEach(o=>o.addEventListener('click',e=>{if(e.target===o)o.classList.remove('on')}));

// ================================================================
// TOAST
// ================================================================
function toast(msg,t='ok'){
  const el=document.getElementById('toast');
  document.getElementById('ticon').textContent={ok:'✓',err:'✕',info:'ℹ'}[t]||'✓';
  document.getElementById('tmsg').textContent=msg;
  el.style.borderColor=t==='err'?'rgba(255,75,110,.4)':'rgba(0,207,255,.3)';
  el.classList.add('on');
  setTimeout(()=>el.classList.remove('on'),2800);
}

// ================================================================
// HELPERS
// ================================================================
// ================================================================
// CURRENCIES
// ================================================================
const CURRENCIES=[
  {code:'USD',symbol:'$',name:'US Dollar'},{code:'EUR',symbol:'€',name:'Euro'},
  {code:'GBP',symbol:'£',name:'British Pound'},{code:'JPY',symbol:'¥',name:'Japanese Yen'},
  {code:'AUD',symbol:'A$',name:'Australian Dollar'},{code:'CAD',symbol:'C$',name:'Canadian Dollar'},
  {code:'CHF',symbol:'Fr',name:'Swiss Franc'},{code:'CNY',symbol:'¥',name:'Chinese Yuan'},
  {code:'INR',symbol:'₹',name:'Indian Rupee'},{code:'BRL',symbol:'R$',name:'Brazilian Real'},
  {code:'MXN',symbol:'$',name:'Mexican Peso'},{code:'KRW',symbol:'₩',name:'South Korean Won'},
  {code:'SGD',symbol:'S$',name:'Singapore Dollar'},{code:'HKD',symbol:'HK$',name:'Hong Kong Dollar'},
  {code:'SEK',symbol:'kr',name:'Swedish Krona'},{code:'NOK',symbol:'kr',name:'Norwegian Krone'},
  {code:'DKK',symbol:'kr',name:'Danish Krone'},{code:'NZD',symbol:'NZ$',name:'New Zealand Dollar'},
  {code:'ZAR',symbol:'R',name:'South African Rand'},{code:'AED',symbol:'د.إ',name:'UAE Dirham'},
  {code:'SAR',symbol:'﷼',name:'Saudi Riyal'},{code:'QAR',symbol:'﷼',name:'Qatari Riyal'},
  {code:'KWD',symbol:'د.ك',name:'Kuwaiti Dinar'},{code:'BHD',symbol:'.د.ب',name:'Bahraini Dinar'},
  {code:'PKR',symbol:'₨',name:'Pakistani Rupee'},{code:'NGN',symbol:'₦',name:'Nigerian Naira'},
  {code:'EGP',symbol:'£',name:'Egyptian Pound'},{code:'KES',symbol:'KSh',name:'Kenyan Shilling'},
  {code:'GHS',symbol:'₵',name:'Ghanaian Cedi'},{code:'TZS',symbol:'TSh',name:'Tanzanian Shilling'},
  {code:'UGX',symbol:'USh',name:'Ugandan Shilling'},{code:'ETB',symbol:'Br',name:'Ethiopian Birr'},
  {code:'MAD',symbol:'MAD',name:'Moroccan Dirham'},{code:'TND',symbol:'د.ت',name:'Tunisian Dinar'},
  {code:'THB',symbol:'฿',name:'Thai Baht'},{code:'MYR',symbol:'RM',name:'Malaysian Ringgit'},
  {code:'PHP',symbol:'₱',name:'Philippine Peso'},{code:'IDR',symbol:'Rp',name:'Indonesian Rupiah'},
  {code:'VND',symbol:'₫',name:'Vietnamese Dong'},{code:'BDT',symbol:'৳',name:'Bangladeshi Taka'},
  {code:'LKR',symbol:'₨',name:'Sri Lankan Rupee'},{code:'NPR',symbol:'₨',name:'Nepalese Rupee'},
  {code:'MMK',symbol:'K',name:'Myanmar Kyat'},{code:'KHR',symbol:'₭',name:'Cambodian Riel'},
  {code:'PLN',symbol:'zł',name:'Polish Zloty'},{code:'CZK',symbol:'Kč',name:'Czech Koruna'},
  {code:'HUF',symbol:'Ft',name:'Hungarian Forint'},{code:'RON',symbol:'lei',name:'Romanian Leu'},
  {code:'TRY',symbol:'₺',name:'Turkish Lira'},{code:'ILS',symbol:'₪',name:'Israeli Shekel'},
  {code:'UAH',symbol:'₴',name:'Ukrainian Hryvnia'},{code:'RUB',symbol:'₽',name:'Russian Ruble'},
  {code:'CLP',symbol:'$',name:'Chilean Peso'},{code:'COP',symbol:'$',name:'Colombian Peso'},
  {code:'ARS',symbol:'$',name:'Argentine Peso'},{code:'PEN',symbol:'S/',name:'Peruvian Sol'},
  {code:'UYU',symbol:'$U',name:'Uruguayan Peso'},{code:'BOB',symbol:'Bs',name:'Bolivian Boliviano'},
  {code:'PYG',symbol:'₲',name:'Paraguayan Guaraní'},{code:'VES',symbol:'Bs.S',name:'Venezuelan Bolívar'},
];

function setCurrency(code){
  const curr=CURRENCIES.find(c=>c.code===code);
  if(!curr)return;
  D.currency=curr;
  save();
  // Update all currency displays
  document.getElementById('curr-display').textContent=curr.symbol+' '+curr.code;
  cm('m-currency');
  // Re-render current active section
  const active=document.querySelector('.sec.on');
  if(active){const id=active.id.replace('s-','');render(id);}
  toast('Currency set to '+curr.name+' ('+curr.symbol+')');
}

function renderCurrencyPicker(filter=''){
  const list=document.getElementById('curr-list');
  const filtered=filter?CURRENCIES.filter(c=>c.name.toLowerCase().includes(filter.toLowerCase())||c.code.toLowerCase().includes(filter.toLowerCase())):CURRENCIES;
  const curr=getCurr().code;
  list.innerHTML=filtered.map(c=>`
    <div class="curr-item ${c.code===curr?'curr-active':''}" onclick="setCurrency('${c.code}')">
      <span class="curr-sym">${c.symbol}</span>
      <span class="curr-name">${c.name}</span>
      <span class="curr-code">${c.code}</span>
    </div>`).join('');
}

function getCurr(){return D.currency||{code:'USD',symbol:'$',name:'US Dollar'}}
function fmt(n){
  const sym=getCurr().symbol;
  if(!n||isNaN(n))return sym+'0';
  const abs=Math.abs(n);
  const noD=['JPY','KRW','VND','HUF','IDR','CLP','COP','BDT','MMK'].includes(getCurr().code);
  const num=noD?Math.round(abs).toLocaleString():abs.toLocaleString('en-US',{minimumFractionDigits:2,maximumFractionDigits:2});
  return sym+num;
}
function esc(s){return String(s??'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;')}
function clr(ids){ids.forEach(id=>{const e=document.getElementById(id);if(e)e.value=''})}
function dl(name,content,type){const b=new Blob([content],{type});const u=URL.createObjectURL(b);const a=document.createElement('a');a.href=u;a.download=name;a.click();URL.revokeObjectURL(u)}
function badges(){
  document.getElementById('b-subs').textContent=D.subs.length;
  const today=new Date();
  const urg=D.rens.filter(r=>{if(!r.date)return false;const d=Math.ceil((new Date(r.date)-today)/86400000);return d>=0&&d<=30}).length;
  const bren=document.getElementById('b-ren');
  bren.style.display=urg?'':'none';
}

// ================================================================
// CHECKLISTS
// ================================================================
function toggleCk(el,key){
  el.classList.toggle('on');
  el.textContent=el.classList.contains('on')?'✓':'';
  if(!D.cks)D.cks={};
  D.cks[key]=el.classList.contains('on');
  save();
}
function restoreCks(){
  Object.keys(D.cks||{}).forEach(k=>{const e=document.getElementById(k);if(e&&D.cks[k]){e.classList.add('on');e.textContent='✓'}});
}

// ================================================================
// DASHBOARD
// ================================================================
function rDash(){
  const mo=D.subs.reduce((a,s)=>a+s.cost,0);
  const over=D.subs.reduce((a,s)=>a+Math.max(0,(s.newCust>0?s.cost-s.newCust:0)),0);
  const saved=D.savs.reduce((a,s)=>a+s.saved,0);
  const today=new Date();
  const urg=D.rens.filter(r=>{if(!r.date)return false;const d=Math.ceil((new Date(r.date)-today)/86400000);return d>=0&&d<=30}).length;
  document.getElementById('d-mo').textContent=fmt(mo);
  document.getElementById('d-yr').textContent=fmt(mo*12);
  document.getElementById('d-over').textContent=fmt(over)+'/mo';
  document.getElementById('d-saved').textContent=fmt(saved);
  document.getElementById('d-ren').textContent=urg;
  restoreCks();
  const prev=document.getElementById('d-subprev');
  if(!D.subs.length){prev.innerHTML='<div class="empty"><div class="ei">💳</div><div class="et">No subscriptions added yet</div><div class="es">Go to Subscription Autopsy to begin your audit.</div></div>';return}
  const show=D.subs.slice(0,6);
  prev.innerHTML='<div class="g3">'+show.map(s=>{const over2=s.newCust>0?s.cost-s.newCust:0;return`<div class="ps"><div class="psl">${esc(s.category)}</div><div class="psv">${esc(s.name)} — ${fmt(s.cost)}/mo${over2>0.5?` <span style="color:var(--red);font-size:10px">(+${fmt(over2)} over new rate)</span>`:''}</div></div>`}).join('')+(D.subs.length>6?`<div class="ps"><div class="psv" style="color:var(--mu)">+${D.subs.length-6} more in Subscription Autopsy</div></div>`:'')+`</div>`;
}

// ================================================================
// SUBSCRIPTIONS
// ================================================================
function addSub(){
  const name=document.getElementById('sn').value.trim();
  if(!name){toast('Please enter a service name.','err');return}
  D.subs.push({id:Date.now(),name,cat:document.getElementById('sc2').value,cost:+document.getElementById('scost').value||0,orig:+document.getElementById('sorig').value||0,newCust:+document.getElementById('snew').value||0,joined:document.getElementById('sjoin').value,pay:document.getElementById('spay').value,note:document.getElementById('snote').value});
  save();cm('m-sub');clr(['sn','scost','sorig','snew','snote']);rSubs();badges();toast('Subscription added.');
}
function delSub(id){if(!confirm('Remove this subscription?'))return;D.subs=D.subs.filter(s=>s.id!==id);save();rSubs();badges();toast('Removed.')}
function rSubs(){
  const mo=D.subs.reduce((a,s)=>a+s.cost,0);
  const over=D.subs.reduce((a,s)=>a+Math.max(0,s.newCust>0?s.cost-s.newCust:0),0);
  const sil=D.subs.filter(s=>s.orig>0&&s.cost>s.orig).length;
  document.getElementById('ss-mo').textContent=fmt(mo);
  document.getElementById('ss-over').textContent=fmt(over)+'/mo';
  document.getElementById('ss-overyr').textContent=over>0?`${fmt(over*12)}/yr overpaid`:'At or below new-customer rates';
  document.getElementById('ss-sil').textContent=sil;
  document.getElementById('ss-cnt').textContent=D.subs.length;
  const tb=document.getElementById('sub-tb');
  if(!D.subs.length){tb.innerHTML='<tr><td colspan="8"><div class="empty"><div class="ei">📋</div><div class="et">No subscriptions yet</div><div class="es">Click "Add Subscription" to begin.</div></div></td></tr>';return}
  tb.innerHTML=D.subs.map(s=>{
    const ov=s.newCust>0?s.cost-s.newCust:0;
    const sil2=s.orig>0&&s.cost>s.orig;
    const sc=ov>5?'br2':ov>0?'ba':'bg';
    const st=ov>5?'⚠ Overpaying':ov>0?'↑ Slightly Over':'✓ At Market Rate';
    return`<tr><td><strong>${esc(s.name)}</strong><div class="tm">${esc(s.pay)}</div></td><td><span class="badge bc">${esc(s.cat)}</span></td><td><strong>${fmt(s.cost)}</strong></td><td>${s.newCust>0?`<span style="color:var(--cyan)">${fmt(s.newCust)}</span>`:'<span class="tm">Not checked</span>'}</td><td>${ov>0?`<span style="color:var(--red);font-weight:700">+${fmt(ov)}</span>`:'<span style="color:var(--grn)">–</span>'}</td><td>${sil2?`<span class="badge br2">↑ +${fmt(s.cost-s.orig)}/mo</span>`:'<span class="tm">No data</span>'}</td><td><span class="badge ${sc}">${st}</span></td><td><button class="btn bd sm" onclick="delSub(${s.id})">✕</button></td></tr>`;
  }).join('');
}
function exportSubsCSV(){
  if(!D.subs.length){toast('No subscriptions to export.','err');return}
  const rows=[['Name','Category','Monthly Cost','Original Price','New Customer Price','Overpay/mo','Joined','Payment','Notes']];
  D.subs.forEach(s=>rows.push([s.name,s.cat,s.cost,s.orig,s.newCust,(s.cost-(s.newCust||s.cost)).toFixed(2),s.joined,s.pay,s.note]));
  dl('subscriptions.csv',rows.map(r=>r.map(c=>`"${String(c||'').replace(/"/g,'""')}"`).join(',')).join('\n'),'text/csv');
}

// ================================================================
// PRICE LOG
// ================================================================
function addPrice(){
  const item=document.getElementById('pi').value.trim();
  if(!item){toast('Please describe what you searched.','err');return}
  D.prices.push({id:Date.now(),item,date:document.getElementById('pd').value,time:document.getElementById('pt').value,device:document.getElementById('pdev').value,mode:document.getElementById('pmode').value,amt:+document.getElementById('pamt').value||0,cat:document.getElementById('pcat').value,note:document.getElementById('pnote').value});
  save();cm('m-price');clr(['pi','pamt','pnote']);rPrice();toast('Price logged.');
}
function delPrice(id){D.prices=D.prices.filter(p=>p.id!==id);save();rPrice()}
function rPrice(){
  const tb=document.getElementById('price-tb');
  if(!D.prices.length){tb.innerHTML='<tr><td colspan="8"><div class="empty"><div class="ei">📊</div><div class="et">No price logs yet</div><div class="es">Start logging to spot patterns.</div></div></td></tr>';return}
  tb.innerHTML=[...D.prices].reverse().map(p=>`<tr><td><strong>${esc(p.item)}</strong>${p.note?`<div class="tm">${esc(p.note.slice(0,55))}${p.note.length>55?'...':''}</div>`:''}</td><td class="tm">${p.date||'–'}</td><td class="tm">${p.time||'–'}</td><td><span class="badge bc">${esc(p.device||'–')}</span></td><td><span class="badge ${p.mode?.includes('Incognito')||p.mode?.includes('VPN')?'bg':'ba'}">${esc(p.mode||'–')}</span></td><td><strong style="color:var(--cyan)">${fmt(p.amt)}</strong></td><td><span class="badge bc">${esc(p.cat||'–')}</span></td><td><button class="btn bd sm" onclick="delPrice(${p.id})">✕</button></td></tr>`).join('');
}

// ================================================================
// PROFILING SCORE
// ================================================================
const QUIZ=[
  {k:'q01',text:'How many loyalty programmes or rewards accounts are you actively enrolled in?',opts:[['None or 1',0],['2–3',5],['4–6',12],['7 or more',20]],cat:'Loyalty Exposure'},
  {k:'q02',text:'Do you use the same device for most of your online purchases?',opts:[['No — I vary devices often',0],['Mostly the same device',12],['Always the same device',20]],cat:'Device Consistency'},
  {k:'q03',text:'When researching a purchase, how many times do you revisit the same page before buying?',opts:[['I tend to buy on first visit',0],['1–2 return visits',5],['3–5 return visits',12],['Many visits over multiple days',18]],cat:'Return Visit Signal'},
  {k:'q04',text:'Do you tend to buy things at roughly the same time of day or week?',opts:[['No consistent pattern',0],['Somewhat consistent',8],['Very consistent — same time most days',16]],cat:'Time Consistency'},
  {k:'q05',text:'Do you usually browse in standard mode while logged into your accounts?',opts:[['I use incognito/private mode often',0],['Sometimes incognito',6],['Almost always standard mode and logged in',15]],cat:'Account History Exposure'},
  {k:'q06',text:'How do you typically pay for online subscriptions?',opts:[['Prepaid / gift cards',0],['PayPal',4],['Regular debit or credit card',8],['Rewards credit card',14]],cat:'Payment Data Exposure'},
  {k:'q07',text:'Do you use mobile apps from companies you purchase from regularly?',opts:[['No — I use browsers',0],['A few apps',7],['Apps for most purchases',16]],cat:'App Tracking Exposure'},
  {k:'q08',text:'Do you have items saved in wishlists or shopping carts on retail platforms?',opts:[['No saved items anywhere',0],['A few items',5],['Many items across multiple platforms',14]],cat:'Wishlist Surveillance'},
  {k:'q09',text:'Have your recurring subscription prices gone up without you being notified?',opts:[['I track prices closely — no unnoticed increases',0],["I'm not sure — possible",10],['Yes, I\'ve spotted silent increases',20]],cat:'Silent Increase Exposure'},
  {k:'q10',text:'How long have you been a customer at your major service providers?',opts:[['Less than 1 year',0],['1–3 years',6],['3–6 years',12],['Over 6 years',18]],cat:'Tenure-Based Targeting'}
];

function rScore(){
  const c=document.getElementById('quiz-qs');
  c.innerHTML=QUIZ.map((q,i)=>`<div class="qi"><div class="qt">${i+1}. ${q.text}</div><div class="qopts">${q.opts.map(([l,s])=>`<button class="qbtn ${D.quiz[q.k]===s?'on':''}" onclick="selQ('${q.k}',${s},this)">${esc(l)}</button>`).join('')}</div></div>`).join('');
}

function selQ(k,score,el){
  el.closest('.qopts').querySelectorAll('.qbtn').forEach(b=>b.classList.remove('on'));
  el.classList.add('on');
  D.quiz[k]=score;
  save();
}

function calcScore(){
  const answered=Object.keys(D.quiz).length;
  if(answered<5){toast('Please answer at least 5 questions.','err');return}
  let total=0;
  QUIZ.forEach(q=>{total+=(D.quiz[q.k]||0)});
  const max=QUIZ.reduce((a,q)=>a+Math.max(...q.opts.map(o=>o[1])),0);
  const score=Math.round((total/max)*100);
  document.getElementById('sdisp').textContent=score;
  const circ=2*Math.PI*56;
  document.getElementById('sarc').setAttribute('stroke-dashoffset',circ*(1-score/100));
  const [col,lbl]=score>=70?['#FF4B6E','HIGH EXPOSURE — You are a well-profiled target. Immediate action recommended.']:score>=40?['#F59E0B','MEDIUM EXPOSURE — Real steps can meaningfully reduce your profile.']:['#2ECC98','LOW EXPOSURE — Good habits in place. Maintain and review quarterly.'];
  document.getElementById('sarc').setAttribute('stroke',col);
  document.getElementById('slbl').textContent=lbl;
  document.getElementById('slbl').style.color=col;
  // breakdown
  const cats={};
  QUIZ.forEach(q=>{if(!cats[q.cat])cats[q.cat]={s:0,m:0};cats[q.cat].s+=D.quiz[q.k]||0;cats[q.cat].m+=Math.max(...q.opts.map(o=>o[1]))});
  document.getElementById('sbrkdwn').innerHTML=Object.entries(cats).map(([c,{s,m}])=>{const p=Math.round(s/m*100);const pc=p>=70?'r':p>=40?'a':'';return`<div style="margin-bottom:9px"><div style="display:flex;justify-content:space-between;font-size:12px;color:var(--mu);margin-bottom:3px"><span>${c}</span><span style="font-weight:700;color:var(--wt)">${p}%</span></div><div class="pb"><div class="pf ${pc}" style="width:${p}%"></div></div></div>`}).join('');
  // recs
  const recs=[];
  if((D.quiz.q02||0)>=12)recs.push({i:'💻',t:'Use a different device for each spending category (travel, shopping, streaming). This breaks the consistent device fingerprint the model relies on.',p:'High'});
  if((D.quiz.q01||0)>=12)recs.push({i:'🏆',t:'For each loyalty membership, compare your logged-in price vs. a private-window new-customer price. If private is cheaper, that membership is costing you money.',p:'High'});
  if((D.quiz.q05||0)>=10)recs.push({i:'🕵️',t:'Log out of accounts before browsing without intent to buy. Log in only at the point of completing a purchase you\'ve already committed to.',p:'High'});
  if((D.quiz.q07||0)>=7)recs.push({i:'📱',t:'Check the same price on a desktop browser before completing any in-app purchase over $15. App prices are frequently higher for identical items.',p:'Medium'});
  if((D.quiz.q08||0)>=5)recs.push({i:'💝',t:'Clear all platform wishlists and saved carts. Keep a private handwritten or plain-text note of items you\'re considering instead — no platform surveillance.',p:'Medium'});
  if((D.quiz.q04||0)>=8)recs.push({i:'⏰',t:'Vary your purchase timing deliberately. Avoid buying at the same time every day. Early morning on Tuesday–Thursday typically returns the lowest baseline prices.',p:'Medium'});
  if((D.quiz.q10||0)>=12)recs.push({i:'📅',t:'Long-tenured customers are the most profitable target for renewal premiums. Schedule a negotiation call for your three oldest service relationships within the next 30 days.',p:'High'});
  if(!recs.length)recs.push({i:'✅',t:'Your current habits are disrupting your profile effectively. Maintain these practices and run a quarterly review to keep the model\'s confidence low.',p:'Low'});
  document.getElementById('srecs').style.display='block';
  document.getElementById('sreclist').innerHTML=recs.map(r=>`<div style="display:flex;gap:11px;align-items:flex-start;padding:10px 0;border-bottom:1px solid var(--br)"><span style="font-size:20px">${r.i}</span><div><div style="font-size:13px;line-height:1.4">${r.t}</div><span class="badge ${r.p==='High'?'br2':r.p==='Medium'?'ba':'bg'}" style="margin-top:6px">${r.p} Priority</span></div></div>`).join('');
  toast(`Score: ${score}/100 — see recommendations below.`);
}

// ================================================================
// DISRUPTION PROTOCOL
// ================================================================
const PROTOS=[
  {ico:'✈️',name:'Flights',risk:'VERY HIGH',rc:'red',steps:[{l:'Device',v:'Desktop laptop — never mobile app for booking'},{l:'Browser',v:'Incognito + fully logged out'},{l:'Best Timing',v:'Tuesday or Wednesday, 9am–12pm'},{l:'Session Rule',v:'Search once, decide, book. No revisits.'},{l:'Payment',v:'Non-rewards debit or plain credit card'},{l:'Key Tactic',v:'Search 4–5 date variants even if only one works — never search only your actual date'}]},
  {ico:'🏨',name:'Hotels',risk:'VERY HIGH',rc:'red',steps:[{l:'Device',v:'Desktop browser only — not the hotel app'},{l:'Browser',v:'Incognito + logged out of loyalty programme'},{l:'Best Timing',v:'Mid-week searches for any dates'},{l:'Session Rule',v:'One research session, decide within 48 hrs'},{l:'Payment',v:'Card without hotel brand affiliation'},{l:'Key Tactic',v:'Get the online price then call the hotel directly — direct reservations are often 5–15% lower'}]},
  {ico:'🛡️',name:'Insurance',risk:'HIGH',rc:'red',steps:[{l:'Device',v:'Desktop — not a device used for health browsing'},{l:'Browser',v:'Clean private session only'},{l:'Best Timing',v:'Request quotes 60 days before renewal'},{l:'Session Rule',v:'Request 4–5 quotes simultaneously — signals genuine competition'},{l:'Payment',v:'Annual lump-sum often 5–12% cheaper than monthly'},{l:'Key Tactic',v:'Never mention your renewal is approaching. Ask as if starting fresh: "What would it cost me to sign up?"'}]},
  {ico:'🚗',name:'Rideshare',risk:'HIGH',rc:'red',steps:[{l:'Device',v:'Phone app required — but use two competing apps'},{l:'Browser',v:'Check both apps before requesting any ride'},{l:'Best Timing',v:'Avoid Mon 8–9am and Fri 5–7pm surge peaks'},{l:'Session Rule',v:'Compare apps simultaneously, pick best'},{l:'Payment',v:'Price varies by demand, not card type'},{l:'Key Tactic',v:'Walk 1–2 blocks from your pickup point — often places you outside the surge pricing zone'}]},
  {ico:'🎟️',name:'Event Tickets',risk:'HIGH',rc:'red',steps:[{l:'Device',v:'Desktop browser — app prices run higher'},{l:'Browser',v:'Incognito — do NOT add to cart without buying'},{l:'Best Timing',v:'First day of sale OR within 72 hours of the event'},{l:'Session Rule',v:'One decisive session — each page revisit raises the price'},{l:'Payment',v:'Check for credit card presale access — often the cheapest route'},{l:'Key Tactic',v:'Unsold inventory for many events drops in the final 24–48 hours. If you can wait, wait.'}]},
  {ico:'📺',name:'Streaming / SaaS',risk:'MEDIUM',rc:'amber',steps:[{l:'Device',v:'Any — prices less variable here'},{l:'Browser',v:'Incognito to check new-customer rate before renewing'},{l:'Best Timing',v:'Call during trial period end, not renewal'},{l:'Session Rule',v:'Annual billing is usually 15–20% cheaper than monthly'},{l:'Payment',v:'Gift cards for popular services often sell at 10–20% discount'},{l:'Key Tactic',v:'Let a subscription lapse for 7–14 days, then rejoin at the new-customer rate'}]},
  {ico:'📡',name:'Internet / Mobile / Utilities',risk:'MEDIUM',rc:'amber',steps:[{l:'Device',v:'Any — phone call is the most effective channel'},{l:'Browser',v:'Research 2 competitor rates in incognito first'},{l:'Best Timing',v:'Call 14 days before contract renewal date'},{l:'Session Rule',v:'Have 2 named competitor quotes ready before calling'},{l:'Payment',v:'Ask specifically for auto-pay and paperless billing discounts'},{l:'Key Tactic',v:'"I have a written quote from [Competitor] for $X for equivalent service — can you match it?"'}]},
  {ico:'📦',name:'Grocery / Food Delivery',risk:'MEDIUM',rc:'amber',steps:[{l:'Device',v:'Browser over app where possible'},{l:'Browser',v:'Check service fees before logging in'},{l:'Best Timing',v:'Avoid meal times and Sunday evenings'},{l:'Session Rule',v:'Build cart in one session — do not save and return'},{l:'Payment',v:'Look for one-time promo codes before checkout'},{l:'Key Tactic',v:'Scheduled delivery windows are cheaper than on-demand. Pickup nearly always beats delivery cost.'}]}
];

function rDisrupt(){
  document.getElementById('proto-list').innerHTML=PROTOS.map(p=>`<div class="pcard"><div class="phdr"><div class="pico">${p.ico}</div><div><div class="pname">${p.name}</div><div class="prisk" style="color:var(--${p.rc})">Pricing Risk: ${p.risk}</div></div></div><div class="psteps">${p.steps.map(s=>`<div class="ps"><div class="psl">${s.l}</div><div class="psv">${s.v}</div></div>`).join('')}</div></div>`).join('');
}

// ================================================================
// NEGOTIATION
// ================================================================
const SCRIPTS=[
  {title:'📺 Streaming Service',when:'Price has increased OR new-customer rate is lower than yours',script:`"Hi — I've been a customer for [X] years and I genuinely value the service. However, I noticed my monthly charge has risen to $[amount], and I can see that new customers are currently offered [new rate]. I'd like to continue, but I need a price that works for my budget. Can you help me get to that new-customer rate or close to it?"

[If they say no]:
"I understand. Is there a different plan tier, or a loyalty offer, that might work? I'm hoping to stay."

[If still no]:
"I may need to cancel and come back as a new subscriber. Before I do that — is there someone in your retention team I can speak with?"`},
  {title:'🛡️ Insurance (Home / Auto)',when:'14 days before renewal with competitor quotes ready',script:`"Hi — my policy is coming up for renewal and I've been comparing options. I've received a quote from [Competitor] for $[amount] for comparable coverage. I've been with you for [X] years and would prefer to stay, but I can't justify the difference unless you can come close to matching that.

Can you review my policy and tell me what you can do?"

[Key]: Have the specific competitor quote ready. Named numbers carry far more weight than vague statements.

[After their offer]:
"I appreciate that. Is that your best available? I want to make this decision today."`},
  {title:'📡 Internet / Phone / Cable',when:'Contract end or when you\'ve found a better rate elsewhere',script:`"I'm reviewing my bill and it's time to re-evaluate. I've been a customer for [X] years but my rate has increased and I'm seeing [Competitor] offer [amount] for comparable service.

I'd prefer to stay, but the difference is hard to ignore. What can you do for me as a long-term customer?"

[Magic phrase]: "Can you transfer me to your retention team? I'm seriously considering my options."

[Retention agents have more discount authority — always ask for them specifically.]`},
  {title:'🏋️ Gym / Fitness Membership',when:'Contract renewal or when usage has dropped significantly',script:`"Hi — I'm reviewing my membership and thinking about my options. I noticed you offer a different rate for new members. I've been here [X] time, and I'd like to discuss whether there's a rate that better reflects what I'm using.

What options do you have — whether that's a rate reduction, a different plan, or a pause option while I decide?"

[For cancellation intent]:
"I need to pause or cancel for budget reasons. What's the process — and is there anything you can offer that would change that?"`},
  {title:'☁️ Software / SaaS',when:'Annual renewal — especially professional or team plans',script:`"I'm reviewing our software costs and re-evaluating subscriptions for the year. We've been using [product] for [X] time, but the current rate is above our budget threshold.

I know annual billing can change the monthly cost significantly. What options do you have — whether that's annual billing, a different tier, or an adjusted rate for long-term users?

Specifically, what would it look like on an annual plan, and is there any flexibility there?"`}
];

function rNeg(){
  document.getElementById('neg-scripts').innerHTML=SCRIPTS.map(s=>`<div class="scard"><div class="shdr" onclick="togScript(this)"><div class="stit">${s.title}</div><span style="color:var(--cyan);font-size:12px">▼ Show Script</span></div><div class="sbdy"><div class="alert ac" style="margin-bottom:10px"><span class="ai">🎯</span><span><strong>When to use:</strong> ${s.when}</span></div><div class="stxt">${esc(s.script)}</div><button class="btn bs sm" onclick="copyTxt(this)" style="margin-top:9px" data-t="${esc(s.script)}">📋 Copy Script</button></div></div>`).join('');
  rNegTb();
}

function togScript(h){const b=h.nextElementSibling;const a=h.querySelector('span:last-child');b.classList.toggle('on');a.textContent=b.classList.contains('on')?'▲ Hide Script':'▼ Show Script'}

function copyTxt(btn){const t=btn.dataset.t.replace(/&amp;/g,'&').replace(/&lt;/g,'<').replace(/&gt;/g,'>').replace(/&#039;/g,"'").replace(/&quot;/g,'"');navigator.clipboard.writeText(t).then(()=>toast('Script copied to clipboard.'))}

function addNeg(){
  const co=document.getElementById('nc').value.trim();
  if(!co){toast('Please enter a company name.','err');return}
  const b=+document.getElementById('nb').value||0,a=+document.getElementById('na').value||0;
  D.negs.push({id:Date.now(),co,date:document.getElementById('nd').value,b,a,method:document.getElementById('nm').value,outcome:document.getElementById('no').value,note:document.getElementById('nnote').value});
  save();cm('m-neg');clr(['nc','nb','na','nnote']);rNegTb();toast('Negotiation logged.');
}
function delNeg(id){D.negs=D.negs.filter(n=>n.id!==id);save();rNegTb()}
function rNegTb(){
  const wins=D.negs.filter(n=>n.outcome==='Won');
  const rate=D.negs.length?Math.round(wins.length/D.negs.length*100)+'%':'–';
  const saved=wins.reduce((a,n)=>a+Math.max(0,n.b-n.a),0);
  document.getElementById('n-cnt').textContent=D.negs.length;
  document.getElementById('n-rate').textContent=rate;
  document.getElementById('n-saved').textContent=fmt(saved);
  const tb=document.getElementById('neg-tb');
  if(!D.negs.length){tb.innerHTML='<tr><td colspan="8"><div class="empty"><div class="ei">💬</div><div class="et">No negotiations logged yet</div></div></td></tr>';return}
  const oc={'Won':'bg','Partial':'ba','Lost':'br2','Cancelled':'bc'};
  tb.innerHTML=[...D.negs].reverse().map(n=>{const d=Math.max(0,n.b-n.a);return`<tr><td><strong>${esc(n.co)}</strong></td><td class="tm">${n.date||'–'}</td><td>${fmt(n.b)}</td><td>${n.a>0?fmt(n.a):'–'}</td><td>${d>0?`<span style="color:var(--grn);font-weight:700">–${fmt(d)}</span>`:'–'}</td><td class="tm">${esc(n.method)}</td><td><span class="badge ${oc[n.outcome]||'bc'}">${n.outcome}</span></td><td><button class="btn bd sm" onclick="delNeg(${n.id})">✕</button></td></tr>`}).join('');
}

// ================================================================
// RISK MAP
// ================================================================
const RISKS=[
  {n:'Flights',r:5,s:'Real-time personalised pricing per user',tips:['Search Tuesday/Wednesday 9am–12pm','Desktop incognito only — never app','Search 4–5 date variants each session','Never revisit the same search','Price difference of logged-in vs private window often 10–30%']},
  {n:'Hotels',r:5,s:'Demand surge + loyalty profile pricing',tips:['Call hotel directly after online quote','Never book via app — always desktop browser','Same-night rates often drop after 8pm local time','Loyalty programme membership can raise your shown price']},
  {n:'Event Tickets',r:5,s:'Scarcity pricing + demand-surge algorithms',tips:['Buy on first sale day or within 72hrs of event','Never add to cart without completing the purchase immediately','Prices for many events fall 24–48hrs before showtime','Use credit card presale access for best rates']},
  {n:'Rideshare',r:4,s:'Real-time demand and location surge pricing',tips:['Check two competing apps simultaneously','Walk 1–2 blocks from your actual location','Avoid peak demand windows (commute hours, rain)','Surge pricing is zone-based — moving slightly can exit the zone']},
  {n:'Insurance',r:4,s:'Renewal inertia + tenure-based premium escalation',tips:['Get 4+ quotes simultaneously to signal competitive intent','Never mention your renewal is upcoming when requesting quotes','Annual payment discount is real — always ask','Use an independent broker for impartial comparison']},
  {n:'Grocery Delivery',r:3,s:'Time-window fees + membership upsells',tips:['Pickup is almost always cheaper than delivery','Scheduled delivery windows cheaper than on-demand','Build cart in one sitting — return visits can add fees','Membership break-even point is often higher than expected']},
  {n:'Streaming',r:2,s:'Renewal price creep + silent tier increases',tips:['New-customer rate is almost always lower — check it quarterly','Annual billing saves 15–20% vs monthly','Gift cards for major platforms sell at 10–20% discount','Family/student plans rarely mentioned unless asked']},
  {n:'Internet / Mobile',r:3,s:'Loyalty penalty + inertia contract pricing',tips:['Call retention team specifically — not general customer service','Call 14 days before contract end with competitor quote ready','Ask for the "loyalty rate" or "long-term customer rate" by name','Second call rule: different agent, often different outcome']},
  {n:'Software / SaaS',r:2,s:'Plan complexity hides better-value tiers',tips:['Annual billing often 20–40% cheaper than monthly','Non-profit / startup / student rates exist but are never advertised proactively','Request downgrade to lower tier rather than outright cancellation','Pause options almost always exist and are rarely offered unprompted']},
  {n:'Retail Shopping',r:3,s:'Profile-based personalised discount targeting',tips:['Mobile app and desktop browser often show different prices for identical items','Clearing cookies before purchase removes your shopping history from the session','Email sign-up discounts sometimes apply to your current cart retroactively','Cart abandonment triggers discount emails — use this deliberately']},
  {n:'Gym / Fitness',r:2,s:'Inertia pricing + lock-in contract design',tips:['Corporate/employer discounts exist at most gym chains — rarely advertised','Free membership freeze option usually exists — ask for it before cancelling','Cancellation window is often the only time a price reduction is offered','New-member rates are significantly lower — use as negotiation anchor']},
  {n:'Utilities',r:2,s:'Contract renewal re-pricing + passive customer targeting',tips:['Off-peak tariff options exist and are rarely offered proactively','Annual vs. rolling contract — compare the actual numbers explicitly','Switching provider rather than renegotiating renewal often achieves more','Direct debit discount is commonly 3–8% — always ask if not offered']}
];

function rRisk(){
  const el=document.getElementById('risk-grid');
  el.innerHTML=RISKS.map((r,i)=>{
    const lv=r.r>=4?'h':r.r>=3?'m':'l';
    const dc=lv==='h'?'rdh':lv==='m'?'rdm':'rdl';
    const dots=Array.from({length:5},(_,j)=>`<div class="rd ${j<r.r?dc:''}"></div>`).join('');
    return`<div class="rc" id="rc${i}" onclick="togRisk(${i})"><div class="rdots">${dots}</div><div class="rname">${r.n}</div><div class="rsum">${r.s}</div><div class="rdet" id="rd${i}">${r.tips.map(t=>`<div class="rtip">${t}</div>`).join('')}</div></div>`;
  }).join('');
}
function togRisk(i){document.getElementById('rd'+i).classList.toggle('on');document.getElementById('rc'+i).classList.toggle('exp')}

// ================================================================
// RENEWALS
// ================================================================
function addRen(){
  const name=document.getElementById('rn').value.trim();
  if(!name){toast('Please enter a service name.','err');return}
  D.rens.push({id:Date.now(),name,date:document.getElementById('rd').value,cost:+document.getElementById('rc').value||0,cat:document.getElementById('rcat').value,note:document.getElementById('rnote').value,status:'Not Reviewed'});
  save();cm('m-ren');clr(['rn','rc','rnote']);rRen();badges();toast('Renewal tracked.');
}
function delRen(id){D.rens=D.rens.filter(r=>r.id!==id);save();rRen();badges()}
function updRenStatus(id,status){const r=D.rens.find(r=>r.id===id);if(r){r.status=status;save()}}
function rRen(){
  const today=new Date();
  const rens=D.rens.map(r=>({...r,days:r.date?Math.ceil((new Date(r.date)-today)/86400000):null})).sort((a,b)=>(a.days??9999)-(b.days??9999));
  const urg=rens.filter(r=>r.days!==null&&r.days<=30&&r.days>=0);
  const urgEl=document.getElementById('ren-urgent');
  urgEl.innerHTML=urg.length?`<div class="alert ar"><span class="ai">🚨</span><div><strong>${urg.length} renewal${urg.length>1?'s':''} due within 30 days — act before the date, not after.</strong>${urg.map(r=>`<div style="margin-top:5px;font-size:12px">• ${esc(r.name)} — <strong>${r.days} days</strong> (${r.date})</div>`).join('')}</div></div>`:'';
  const tb=document.getElementById('ren-tb');
  if(!rens.length){tb.innerHTML='<tr><td colspan="8"><div class="empty"><div class="ei">📅</div><div class="et">No renewals tracked yet</div><div class="es">Add insurance, annual plans, and auto-renewing contracts.</div></div></td></tr>';return}
  const statuses=['Not Reviewed','Reviewing','Negotiating','Renewed — Same Rate','Renewed — Better Rate','Cancelled'];
  tb.innerHTML=rens.map(r=>{
    let pill='–';
    if(r.days!==null){
      if(r.days<0)pill=`<span class="cp cpu">Overdue</span>`;
      else if(r.days<=14)pill=`<span class="cp cpu">${r.days}d</span>`;
      else if(r.days<=45)pill=`<span class="cp cps">${r.days}d</span>`;
      else pill=`<span class="cp cpo">${r.days}d</span>`;
    }
    return`<tr><td><strong>${esc(r.name)}</strong></td><td class="tm">${esc(r.cat)}</td><td class="tm">${r.date||'–'}</td><td>${pill}</td><td>${r.cost>0?fmt(r.cost)+'/yr':'–'}</td><td><select class="fsel" style="width:auto;padding:4px 8px;font-size:11px" onchange="updRenStatus(${r.id},this.value)">${statuses.map(s=>`<option ${r.status===s?'selected':''}>${s}</option>`).join('')}</select></td><td class="tm">${r.note?esc(r.note.slice(0,45))+(r.note.length>45?'...':''):'–'}</td><td><button class="btn bd sm" onclick="delRen(${r.id})">✕</button></td></tr>`;
  }).join('');
}

// ================================================================
// SAVINGS
// ================================================================
function addSav(){
  const name=document.getElementById('svn').value.trim();
  if(!name){toast('Please enter what you saved on.','err');return}
  const b=+document.getElementById('svb').value||0,a=+document.getElementById('sva').value||0;
  D.savs.push({id:Date.now(),name,date:document.getElementById('svd').value,b,a,saved:b-a,method:document.getElementById('svm').value});
  save();cm('m-sav');clr(['svn','svb','sva']);rSavs();toast(`Win logged — ${fmt(b-a)} saved!`);
}
function delSav(id){D.savs=D.savs.filter(s=>s.id!==id);save();rSavs()}
function rSavs(){
  const total=D.savs.reduce((a,s)=>a+s.saved,0);
  const best=D.savs.length?Math.max(...D.savs.map(s=>s.saved)):0;
  const avg=D.savs.length?total/D.savs.length:0;
  document.getElementById('sv-total').textContent=fmt(total);
  document.getElementById('sv-cnt').textContent=D.savs.length;
  document.getElementById('sv-avg').textContent=fmt(avg);
  document.getElementById('sv-best').textContent=fmt(best);
  const list=document.getElementById('savs-list');
  if(!D.savs.length){list.innerHTML='<div class="empty"><div class="ei">💰</div><div class="et">No savings logged yet</div><div class="es">When you negotiate, cancel, or catch a silent increase — log the win here.</div></div>';return}
  list.innerHTML=[...D.savs].reverse().map(s=>`<div class="sw"><div class="samt">${fmt(s.saved)}</div><div class="sdet"><div class="stitle2">${esc(s.name)}</div><div class="smeta">${s.date?s.date+' · ':''}${esc(s.method)} · Was ${fmt(s.b)}, now ${fmt(s.a)}</div></div><button class="btn bd sm" onclick="delSav(${s.id})">✕</button></div>`).join('');
}

// ================================================================
// EXPORT / IMPORT / RESET
// ================================================================
function exportJSON(){dl('pricing_audit_backup_'+new Date().toISOString().split('T')[0]+'.json',JSON.stringify(D,null,2),'application/json');toast('Data exported successfully.')}
function importJSON(e){
  const f=e.target.files[0];if(!f)return;
  const r=new FileReader();
  r.onload=ev=>{try{const d=JSON.parse(ev.target.result);if(confirm('This will replace all current data. Continue?')){D={...D,...d};save();rDash();toast('Data imported successfully.')}}catch{toast('Invalid backup file.','err')}};
  r.readAsText(f);e.target.value='';
}
function resetAll(){
  if(!confirm('Delete ALL data? Export a backup first. This cannot be undone.'))return;
  if(!confirm('Absolutely sure? Everything will be erased.'))return;
  localStorage.removeItem(KEY);
  D={subs:[],prices:[],negs:[],rens:[],savs:[],quiz:{},cks:{},lastSaved:null};
  rDash();toast('All data deleted.');
}

// ================================================================
// INNER TABS
// ================================================================
function itab(btn,panel){
  btn.closest('.itabs').querySelectorAll('.itab').forEach(t=>t.classList.remove('on'));
  btn.classList.add('on');
  btn.closest('.sec').querySelectorAll('.ipanel').forEach(p=>p.classList.remove('on'));
  document.getElementById(panel).classList.add('on');
  if(panel==='ntracker')rNegTb();
}


// ================================================================
// PDF EXPORT
// ================================================================
function exportPDF(){
  const curr=getCurr();
  const today=new Date().toLocaleDateString('en-GB',{day:'2-digit',month:'long',year:'numeric'});
  const mo=D.subs.reduce((a,s)=>a+s.cost,0);
  const over=D.subs.reduce((a,s)=>a+Math.max(0,s.newCust>0?s.cost-s.newCust:0),0);
  const totalSaved=D.savs.reduce((a,s)=>a+s.saved,0);
  const negWins=D.negs.filter(n=>n.outcome==='Won');
  const negSaved=negWins.reduce((a,n)=>a+Math.max(0,n.b-n.a),0);

  const subRows=D.subs.map(s=>{
    const ov=s.newCust>0?s.cost-s.newCust:0;
    const sil=s.orig>0&&s.cost>s.orig;
    return`<tr>
      <td><strong>${s.name}</strong></td>
      <td>${s.cat}</td>
      <td>${fmt(s.cost)}</td>
      <td>${s.newCust>0?fmt(s.newCust):'—'}</td>
      <td class="${ov>0?'over':''}">${ov>0?'+'+fmt(ov):'✓'}</td>
      <td>${sil?'↑ +'+fmt(s.cost-s.orig):'No data'}</td>
    </tr>`;
  }).join('');

  const negRows=D.negs.map(n=>{
    const d=Math.max(0,n.b-n.a);
    return`<tr>
      <td>${n.co}</td><td>${n.date||'—'}</td>
      <td>${fmt(n.b)}</td><td>${n.a>0?fmt(n.a):'—'}</td>
      <td class="${d>0?'win':''}">${d>0?'–'+fmt(d):'—'}</td>
      <td>${n.outcome}</td>
    </tr>`;
  }).join('');

  const renRows=D.rens.map(r=>{
    const days=r.date?Math.ceil((new Date(r.date)-new Date())/86400000):null;
    const urgency=days!==null&&days<=30?'🔴 Act Now':days!==null&&days<=60?'🟡 Soon':'🟢 OK';
    return`<tr>
      <td>${r.name}</td><td>${r.cat}</td>
      <td>${r.date||'—'}</td>
      <td>${days!==null?days+' days':'—'}</td>
      <td>${r.cost>0?fmt(r.cost)+'/yr':'—'}</td>
      <td>${urgency}</td>
    </tr>`;
  }).join('');

  const savRows=D.savs.map(s=>`<tr>
    <td>${s.name}</td><td>${s.date||'—'}</td>
    <td class="win">${fmt(s.saved)}</td>
    <td>${fmt(s.b)}</td><td>${fmt(s.a)}</td><td>${s.method}</td>
  </tr>`).join('');

  // Score summary
  let scoreHTML='';
  if(Object.keys(D.quiz).length>=5){
    const QMAX=D.quiz.q01!==undefined?170:0;
    let total=0;Object.values(D.quiz).forEach(v=>total+=v);
    if(QMAX>0){const sc=Math.round((total/170)*100);scoreHTML=`<div class="stat"><div class="stat-label">Profiling Score</div><div class="stat-val" style="color:${sc>=70?'#e53e3e':sc>=40?'#d69e2e':'#38a169'}">${sc}/100</div></div>`;}
  }

  const html=`<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Pricing Audit Report — ${today}</title>
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  body{font-family:Arial,Helvetica,sans-serif;color:#1a202c;background:#fff;padding:36px;font-size:13px;line-height:1.5}
  .hdr{display:flex;align-items:flex-start;justify-content:space-between;border-bottom:3px solid #00CFFF;padding-bottom:16px;margin-bottom:28px}
  .hdr-left h1{font-size:24px;font-weight:900;color:#06080F;letter-spacing:-0.5px;margin-bottom:3px}
  .hdr-left .sub{font-size:11px;color:#718096;text-transform:uppercase;letter-spacing:1.2px;margin-bottom:8px}
  .hdr-left .meta{font-size:12px;color:#718096}
  .hdr-right{text-align:right;font-size:11px;color:#718096}
  .badge-curr{display:inline-block;background:#EBF8FF;color:#2B6CB0;border:1px solid #90CDF4;border-radius:12px;padding:3px 10px;font-size:11px;font-weight:700;margin-top:6px}
  .stats{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:28px}
  .stat{background:#F7FAFC;border:1px solid #E2E8F0;border-radius:8px;padding:14px}
  .stat-label{font-size:9px;color:#718096;text-transform:uppercase;letter-spacing:1px;margin-bottom:5px}
  .stat-val{font-size:20px;font-weight:900;color:#1a202c}
  .stat-sub{font-size:11px;color:#718096;margin-top:2px}
  .sec-hdr{display:flex;align-items:center;gap:8px;margin-bottom:12px;margin-top:28px}
  h2{font-size:14px;font-weight:800;color:#06080F;border-left:4px solid #00CFFF;padding-left:10px}
  .sec-count{background:#EBF8FF;color:#2B6CB0;border-radius:10px;padding:2px 8px;font-size:11px;font-weight:700}
  table{width:100%;border-collapse:collapse;margin-bottom:8px;font-size:12px}
  thead th{background:#06080F;color:#fff;padding:8px 10px;text-align:left;font-size:10px;text-transform:uppercase;letter-spacing:.8px;font-weight:600}
  tbody td{padding:8px 10px;border-bottom:1px solid #EDF2F7;vertical-align:middle}
  tbody tr:last-child td{border-bottom:none}
  tbody tr:hover{background:#F7FAFC}
  .over{color:#C53030;font-weight:700}
  .win{color:#276749;font-weight:700}
  .ok{color:#276749}
  .empty-note{padding:20px;text-align:center;color:#A0AEC0;font-size:13px;background:#F7FAFC;border-radius:6px}
  .alert-box{background:#FFF5F5;border:1px solid #FEB2B2;border-radius:6px;padding:10px 14px;margin-bottom:16px;font-size:12px;color:#742A2A}
  .alert-green{background:#F0FFF4;border-color:#9AE6B4;color:#1C4532}
  .footer{margin-top:40px;padding-top:16px;border-top:1px solid #E2E8F0;font-size:10px;color:#A0AEC0;line-height:1.7}
  .page-break{page-break-before:always}
  @media print{
    body{padding:20px}
    .no-print{display:none}
    @page{margin:1.5cm;size:A4}
  }
</style>
</head>
<body>

<div class="hdr">
  <div class="hdr-left">
    <div class="sub">Journey of Insight</div>
    <h1>Algorithmic Pricing Audit Report</h1>
    <div class="meta">Generated: ${today}</div>
    <div class="badge-curr">${curr.symbol} ${curr.code} — ${curr.name}</div>
  </div>
  <div class="hdr-right">
    <div style="font-size:20px;margin-bottom:4px">💰</div>
    <div>Financial Control Report</div>
    <div style="color:#A0AEC0;font-size:10px;margin-top:2px">For personal use only</div>
  </div>
</div>

<div class="stats">
  <div class="stat">
    <div class="stat-label">Monthly Subscriptions</div>
    <div class="stat-val">${fmt(mo)}</div>
    <div class="stat-sub">Per year: ${fmt(mo*12)}</div>
  </div>
  <div class="stat" style="border-color:#FEB2B2">
    <div class="stat-label">Monthly Overpayment</div>
    <div class="stat-val" style="color:#C53030">${fmt(over)}</div>
    <div class="stat-sub">vs. new-customer rates</div>
  </div>
  <div class="stat" style="border-color:#9AE6B4">
    <div class="stat-label">Total Savings Logged</div>
    <div class="stat-val" style="color:#276749">${fmt(totalSaved)}</div>
    <div class="stat-sub">${D.savs.length} wins recorded</div>
  </div>
  ${scoreHTML||`<div class="stat"><div class="stat-label">Negotiations Won</div><div class="stat-val">${negWins.length}</div><div class="stat-sub">of ${D.negs.length} attempts</div></div>`}
</div>

${over>0?`<div class="alert-box">⚠️ You are currently paying an estimated <strong>${fmt(over)}/month (${fmt(over*12)}/year)</strong> more than new customers for identical services. The Negotiation scripts in this platform can help recover this.</div>`:'<div class="alert-box alert-green">✅ All tracked subscriptions are at or below new-customer rates. Run the quarterly audit to keep it this way.</div>'}

<!-- SUBSCRIPTIONS -->
<div class="sec-hdr"><h2>Subscription Autopsy</h2><span class="sec-count">${D.subs.length} tracked</span></div>
${D.subs.length?`
<table>
  <thead><tr><th>Service</th><th>Category</th><th>You Pay</th><th>New Customer</th><th>Overpay/mo</th><th>Silent Increase</th></tr></thead>
  <tbody>${subRows}</tbody>
</table>`:
'<div class="empty-note">No subscriptions tracked yet — add them in the Subscription Autopsy section.</div>'}

<!-- RENEWALS -->
<div class="sec-hdr page-break"><h2>Renewal War Room</h2><span class="sec-count">${D.rens.length} tracked</span></div>
${D.rens.length?`
<table>
  <thead><tr><th>Service</th><th>Category</th><th>Renewal Date</th><th>Days Until</th><th>Annual Cost</th><th>Urgency</th></tr></thead>
  <tbody>${renRows}</tbody>
</table>`:
'<div class="empty-note">No renewals tracked yet — add them in the Renewal War Room section.</div>'}

<!-- NEGOTIATIONS -->
<div class="sec-hdr"><h2>Negotiation Outcomes</h2><span class="sec-count">${D.negs.length} logged</span></div>
${D.negs.length?`
<table>
  <thead><tr><th>Company</th><th>Date</th><th>Before</th><th>After</th><th>Saved/mo</th><th>Outcome</th></tr></thead>
  <tbody>${negRows}</tbody>
</table>`:
'<div class="empty-note">No negotiations logged yet — use the Negotiation Hub to track every attempt.</div>'}

<!-- SAVINGS LEDGER -->
<div class="sec-hdr"><h2>Savings Ledger</h2><span class="sec-count">${D.savs.length} wins · ${fmt(totalSaved)} total</span></div>
${D.savs.length?`
<table>
  <thead><tr><th>What You Saved On</th><th>Date</th><th>Amount Saved</th><th>Was Paying</th><th>Now Paying</th><th>Method</th></tr></thead>
  <tbody>${savRows}</tbody>
</table>`:
'<div class="empty-note">No savings logged yet — log every win in the Savings Ledger section.</div>'}

<div class="footer">
  <strong>DISCLAIMER:</strong> This report is generated by the Algorithmic Pricing Audit Platform by Journey of Insight. It is for educational and personal tracking purposes only. It does not constitute financial, legal, or professional advice. All data entered is stored exclusively on the user's device and is never transmitted anywhere. The creator is not liable for any outcomes resulting from actions based on this report. © Journey of Insight. All rights reserved.
</div>

<script>window.onload=function(){setTimeout(function(){window.print()},400)}<\/script>
</body>
</html>`;

  const win=window.open('','_blank','width=900,height=700');
  if(!win){toast('Please allow pop-ups for PDF export, then try again.','err');return;}
  win.document.write(html);
  win.document.close();
  toast('PDF report opening — choose "Save as PDF" in the print dialog.');
}

// ================================================================
// RENDER & NAVIGATION HELPERS
// ================================================================
function render(id){
  const m={dash:rDash,subs:rSubs,price:rPrice,score:rScore,disrupt:rDisrupt,neg:rNeg,risk:rRisk,ren:rRen,savs:rSavs,exp:()=>{}};
  if(m[id])m[id]();
}
function navTo(id){
  document.querySelectorAll('.sec').forEach(s=>s.classList.remove('on'));
  document.querySelectorAll('.sitem').forEach(s=>s.classList.remove('on'));
  document.getElementById('s-'+id).classList.add('on');
  const sidemap={dash:0,subs:1,price:2,score:3,disrupt:4,neg:5,risk:6,ren:7,savs:8,exp:9};
  const items=document.querySelectorAll('.sitem');
  if(items[sidemap[id]])items[sidemap[id]].classList.add('on');
  render(id);
}

// ================================================================
// INIT
// ================================================================
load();
rDash();
badges();
// Restore currency display
(function(){
  const curr=getCurr();
  const disp=document.getElementById('curr-display');
  if(disp)disp.textContent=curr.symbol+' '+curr.code;
})();
</script>
</body>
</html>
