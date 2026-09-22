# CliniScribe
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="color-scheme" content="light dark">
<title>CliniScribe</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Figtree:wght@400;500;600;700&family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400&family=Noto+Sans+Devanagari:wght@400;500;600;700&family=Noto+Sans+Telugu:wght@400;500;600;700&family=Noto+Sans+Tamil:wght@400;500;600;700&family=Noto+Sans+Kannada:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#f6faf8; --surface:#ffffff; --ink:#12302e; --muted:#54706c;
  --line:#d6e4e0; --line-strong:#9db8b3;
  --brand:#0d6a60; --brand-ink:#ffffff; --brand-soft:#e0f1ed; --focus:#2b6fd6;
  --paper:#ffffff;
  --alarm:#b3261e; --alarm-ink:#ffffff;
  --danger:#a8231b; --danger-bg:#fde9e7;
  --warn:#7a4f00; --warn-bg:#fff1cf;
  --ok:#0f6a49; --ok-bg:#dff3e8;
  --pend:#4b625f; --pend-bg:#e8efed;
  --shadow:0 1px 0 rgba(18,48,46,.04),0 14px 34px -20px rgba(18,48,46,.35);
  --indic:"Noto Sans Devanagari","Noto Sans Telugu","Noto Sans Tamil","Noto Sans Kannada";
  --ui:"Figtree",var(--indic),system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  --serif:"Newsreader",var(--indic),"Iowan Old Style",Georgia,"Times New Roman",serif;
  --chrome-h:64px;
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#0b1716; --surface:#112220; --ink:#e3f0ed; --muted:#9db5b0;
    --line:#23403b; --line-strong:#3d6059;
    --brand:#5cd1bf; --brand-ink:#04211e; --brand-soft:#173430; --focus:#8ab4ff;
    --paper:#152826;
    --alarm:#ff9a90; --alarm-ink:#3b0d09;
    --danger:#ff9a90; --danger-bg:#3b1815;
    --warn:#f2c46a; --warn-bg:#34290c;
    --ok:#84dcb0; --ok-bg:#10301f;
    --pend:#a9c1bc; --pend-bg:#1a2f2c;
    --shadow:0 1px 0 rgba(0,0,0,.3),0 14px 34px -20px rgba(0,0,0,.8);
  }
}
:root[data-theme="dark"]{
  --bg:#0b1716; --surface:#112220; --ink:#e3f0ed; --muted:#9db5b0;
  --line:#23403b; --line-strong:#3d6059;
  --brand:#5cd1bf; --brand-ink:#04211e; --brand-soft:#173430; --focus:#8ab4ff;
  --paper:#152826;
  --alarm:#ff9a90; --alarm-ink:#3b0d09;
  --danger:#ff9a90; --danger-bg:#3b1815;
  --warn:#f2c46a; --warn-bg:#34290c;
  --ok:#84dcb0; --ok-bg:#10301f;
  --pend:#a9c1bc; --pend-bg:#1a2f2c;
  --shadow:0 1px 0 rgba(0,0,0,.3),0 14px 34px -20px rgba(0,0,0,.8);
}

*{box-sizing:border-box}
[hidden]{display:none !important}
html{-webkit-text-size-adjust:100%}
body{margin:0;background:var(--bg);color:var(--ink);font:400 1rem/1.55 var(--ui)}
h1,h2,h3,p,ul,ol,dl{margin:0}
button,input,select,textarea{font:inherit;color:inherit}
:focus-visible{outline:3px solid var(--focus);outline-offset:2px}
/* Indic scripts need more vertical room for stacked conjuncts */
html:not(:lang(en)) body{line-height:1.65}
html:not(:lang(en)) h1{line-height:1.3}
html:not(:lang(en)) h2.step-title{line-height:1.35}
html:not(:lang(en)) .paper h2{line-height:1.4}

[data-level="pending"]{--lv-bg:var(--pend-bg);--lv-ink:var(--pend)}
[data-level="routine"]{--lv-bg:var(--ok-bg);--lv-ink:var(--ok)}
[data-level="urgent"]{--lv-bg:var(--warn-bg);--lv-ink:var(--warn)}
[data-level="emergency"]{--lv-bg:var(--danger-bg);--lv-ink:var(--danger)}

/* Chrome */
.chrome{position:sticky;top:0;z-index:30;background:var(--bg);border-bottom:1px solid var(--line)}
.top{max-width:1180px;margin:0 auto;padding:10px 20px;display:flex;align-items:center;gap:8px 14px;flex-wrap:wrap}
.brand{display:flex;align-items:center;gap:10px;font-weight:700;font-size:1.1875rem;letter-spacing:-.01em}
.brand svg{width:32px;height:32px;flex:none}
.tabs{margin-left:auto;display:flex;gap:4px;align-items:center;flex-wrap:wrap}
.tab{background:none;border:0;padding:.5rem .8rem;border-radius:8px;font-weight:600;font-size:.9375rem;color:var(--muted);cursor:pointer;min-height:40px}
.tab[aria-current="page"]{color:var(--ink);background:var(--brand-soft)}
.count{display:inline-block;min-width:1.35rem;padding:0 .4rem;margin-left:.35rem;border-radius:999px;background:var(--brand);color:var(--brand-ink);font-size:.75rem;line-height:1.35rem;text-align:center}
.icon-btn{width:40px;height:40px;border-radius:8px;border:0;background:none;color:var(--muted);cursor:pointer;display:grid;place-items:center}
.icon-btn:hover{background:var(--brand-soft);color:var(--ink)}
.icon-btn svg{width:20px;height:20px}
.lang-sel{width:auto;min-height:40px;padding:.3rem .6rem;border:1.5px solid var(--line-strong);border-radius:8px;background:var(--surface);color:var(--ink);font-weight:600;font-size:.9375rem;cursor:pointer}
#emergencyBar{background:var(--alarm);color:var(--alarm-ink);padding:12px 20px;text-align:center;font-size:.9375rem;line-height:1.5}
#emergencyBar a{color:inherit;font-weight:700;text-decoration:underline}

main{max-width:1180px;margin:0 auto;padding:28px 20px 72px}

/* Layout */
.layout{display:grid;gap:44px;grid-template-columns:minmax(0,1fr) minmax(0,1fr);align-items:start}
.form-col{max-width:600px}
.note-col{position:sticky;top:calc(var(--chrome-h) + 16px);max-height:calc(100vh - var(--chrome-h) - 32px);overflow:auto;padding:2px 2px 8px}
.view-switch{display:none}
@media (max-width:959px){
  .layout{grid-template-columns:minmax(0,1fr);gap:0}
  .form-col{max-width:none}
  .note-col{position:static;max-height:none;overflow:visible}
  .view-switch{display:flex;gap:4px;margin-bottom:22px;border:1.5px solid var(--line-strong);border-radius:12px;padding:4px}
  .view-switch button{flex:1;min-height:42px;border:0;border-radius:8px;background:none;font-weight:600;font-size:.9375rem;color:var(--muted);cursor:pointer}
  .view-switch button[aria-pressed="true"]{background:var(--brand);color:var(--brand-ink)}
}
@media screen and (max-width:959px){
  .layout[data-view="form"] .note-col{display:none}
  .layout[data-view="note"] .form-col{display:none}
}
.dot{display:inline-block;width:9px;height:9px;border-radius:50%;background:var(--lv-ink);margin-left:8px;vertical-align:middle;border:1.5px solid currentColor}

/* Type */
h1{font:500 clamp(2rem,4.6vw,3.1rem)/1.08 var(--serif);letter-spacing:-.02em;margin-bottom:16px}
h2.step-title{font:500 1.9rem/1.15 var(--serif);letter-spacing:-.01em;margin-bottom:8px}
.lede{color:var(--muted);font-size:1.0625rem;max-width:34rem;margin-bottom:26px}
.step-count{color:var(--muted);font-size:.875rem;font-weight:600;margin-bottom:6px}

/* Consent */
.promises{list-style:none;padding:0;margin:0 0 26px;border-bottom:1px solid var(--line)}
.promises li{padding:14px 0;border-top:1px solid var(--line)}
.promises strong{display:block;margin-bottom:2px}
.promises span{color:var(--muted)}
.agree{display:flex;gap:12px;align-items:flex-start;margin-bottom:18px;cursor:pointer}
.agree input{width:22px;height:22px;margin-top:2px;accent-color:var(--brand);flex:none}
.resume{border-left:4px solid var(--brand);background:var(--brand-soft);padding:14px 16px;border-radius:0 10px 10px 0;margin-bottom:26px}
.resume p{margin-bottom:10px}
.resume .row{gap:8px}
.langbox{margin-bottom:26px}

/* Steps */
.steps{list-style:none;margin:0 0 28px;padding:0;display:flex;gap:6px}
.steps li{flex:1;min-width:0}
.steps button{width:100%;text-align:left;background:none;border:0;border-top:4px solid var(--line);padding:8px 2px 0;font-weight:600;font-size:.8125rem;color:var(--muted);cursor:pointer}
.steps .done button,.steps .current button{border-top-color:var(--brand);color:var(--ink)}
.steps button:disabled{cursor:default}
.steps .t{display:block;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
@media (max-width:640px){
  .steps li:not(.current) .t{display:none}
  .steps .current{flex:4}
}

/* Fields */
.field{margin:0 0 24px}
.lbl,legend{display:block;font-weight:600;margin:0 0 6px;padding:0}
.hint{color:var(--muted);font-size:.875rem;margin:0 0 8px}
fieldset{border:0;padding:0;margin:0 0 24px;min-width:0}
input[type=text],input[type=number],select,textarea{width:100%;min-height:46px;padding:.6rem .8rem;border:1.5px solid var(--line-strong);border-radius:10px;background:var(--surface);color:var(--ink)}
textarea{min-height:96px;resize:vertical}
input[aria-invalid="true"],textarea[aria-invalid="true"]{border-color:var(--danger)}
.err{color:var(--danger);font-weight:600;font-size:.9rem;margin-top:6px}
.row{display:flex;gap:10px;align-items:center;flex-wrap:wrap}
.w-sm{width:7.5rem}
.w-md{width:11rem}
.chips{display:flex;flex-wrap:wrap;gap:8px}
.chip{position:relative;display:inline-flex;align-items:center;min-height:42px;padding:.45rem .95rem;border:1.5px solid var(--line-strong);border-radius:999px;background:var(--surface);cursor:pointer;font-size:.9375rem;user-select:none}
.chip input{position:absolute;inset:0;width:100%;height:100%;margin:0;opacity:0;cursor:pointer}
.chip:has(input:checked){background:var(--brand-soft);border-color:var(--brand);font-weight:600}
.chip:has(input:checked) span::before{content:"\2713\00a0"}
.chip:has(input:focus-visible){outline:3px solid var(--focus);outline-offset:2px}
.group-title{font-weight:600;font-size:.9375rem;color:var(--muted);margin:16px 0 8px}
.langbox .group-title{margin-top:0}
.flags{border-bottom:1px solid var(--line)}
.flag{display:flex;gap:12px;align-items:flex-start;padding:14px 0;border-top:1px solid var(--line);cursor:pointer}
.flag input{width:22px;height:22px;margin-top:2px;accent-color:var(--danger);flex:none}
.flag:has(input:checked){color:var(--danger);font-weight:600}
.sev{display:flex;align-items:baseline;gap:12px;margin-bottom:4px}
.sev-out{font:500 1.9rem/1.2 var(--serif)}
.sev-out.unset{font:400 1rem var(--ui);color:var(--muted)}
input[type=range]{width:100%;height:34px;accent-color:var(--brand)}
.scale{display:flex;justify-content:space-between;gap:10px;color:var(--muted);font-size:.8125rem}
.tag-row{display:flex;gap:8px;margin-bottom:10px}
.tags{list-style:none;padding:0;margin:0 0 10px;display:flex;flex-wrap:wrap;gap:8px}
.tag{display:inline-flex;align-items:center;gap:4px;padding:.25rem .3rem .25rem .8rem;border-radius:999px;background:var(--brand-soft);border:1.5px solid var(--brand);font-size:.9375rem}
.tag button{width:30px;height:30px;border:0;border-radius:50%;background:none;cursor:pointer;font-size:1.2rem;line-height:1;color:var(--ink)}
.tag button:hover{background:var(--surface)}

/* Buttons */
.btn{min-height:46px;padding:.6rem 1.25rem;border-radius:10px;font-weight:600;border:1.5px solid transparent;cursor:pointer}
.btn.sm{min-height:40px;padding:.4rem .9rem;font-size:.9375rem}
.btn:hover:not(:disabled){filter:brightness(.95)}
.primary{background:var(--brand);color:var(--brand-ink)}
.secondary{background:transparent;border-color:var(--brand);color:var(--brand)}
.ghost{background:transparent;color:var(--muted)}
.danger-btn{background:transparent;border-color:var(--danger);color:var(--danger)}
.btn:disabled{opacity:.45;cursor:not-allowed}
.nav{display:flex;gap:10px;justify-content:flex-end;flex-wrap:wrap;margin-top:34px;padding-top:22px;border-top:1px solid var(--line)}
.nav .ghost{margin-right:auto}

/* Triage block */
.tri{border-left:6px solid var(--lv-ink);background:var(--lv-bg);padding:16px 18px;border-radius:0 10px 10px 0;margin-bottom:26px}
.tri h3{font:500 1.5rem/1.25 var(--serif);color:var(--lv-ink);margin-bottom:8px}
.tri ul{margin:0 0 10px;padding-left:1.2rem}
.tri p{margin:0}

/* Note language switch */
.notelang{display:flex;align-items:center;gap:8px 10px;flex-wrap:wrap;margin-bottom:12px}
.notelang .lbl-inline{font-weight:600;font-size:.875rem;color:var(--muted)}
.seg{display:inline-flex;border:1.5px solid var(--line-strong);border-radius:10px;padding:3px;gap:3px}
.seg button{border:0;background:none;border-radius:7px;min-height:36px;padding:.2rem .85rem;font-weight:600;cursor:pointer;color:var(--muted)}
.seg button[aria-pressed="true"]{background:var(--brand);color:var(--brand-ink)}
.notelang .fine{flex-basis:100%;margin:0}

/* Note paper */
.paper{background:var(--paper);border:1px solid var(--line);border-radius:6px;box-shadow:var(--shadow);padding:22px 26px 26px;font-family:var(--serif);font-size:1.0625rem;line-height:1.5}
html:not(:lang(en)) .paper{line-height:1.7}
.paper h2{font:500 1.55rem/1.2 var(--serif);letter-spacing:-.01em}
.paper .meta{color:var(--muted);font-family:var(--ui);font-size:.8125rem;margin:2px 0 14px}
.strip{display:flex;align-items:center;gap:14px;padding:8px 14px;border-radius:8px;background:var(--lv-bg);color:var(--lv-ink);margin-bottom:6px}
.strip svg{width:120px;height:28px;flex:none;overflow:visible}
.strip path{fill:none;stroke:currentColor;stroke-width:2;stroke-linecap:round;stroke-linejoin:round;vector-effect:non-scaling-stroke}
.strip.fresh path{stroke-dasharray:100;stroke-dashoffset:100;animation:draw .9s ease-out forwards}
@keyframes draw{to{stroke-dashoffset:0}}
.strip-label{font-family:var(--ui);font-weight:700;font-size:.875rem}
.ns{padding:12px 0;border-top:1px solid var(--line)}
.ns:first-of-type{margin-top:10px}
.ns h3{font:700 .8125rem/1.2 var(--ui);color:var(--brand);margin-bottom:6px;letter-spacing:.01em}
.ns dl{display:grid;grid-template-columns:7.5rem minmax(0,1fr);gap:2px 12px}
.ns dt{color:var(--muted);font-family:var(--ui);font-size:.875rem;padding-top:3px}
.ns dd{margin:0;overflow-wrap:anywhere}
.ns .quote{font-style:italic;margin-bottom:6px;overflow-wrap:anywhere}
.ns ul{margin:6px 0 0;padding-left:1.2rem}
.ph{color:var(--muted);font-style:italic;font-size:.95rem}
.fine{color:var(--muted);font-family:var(--ui);font-size:.8125rem;margin-top:8px}
.badge{display:inline-block;padding:2px 10px;border-radius:999px;font:600 .8125rem var(--ui);background:var(--lv-bg);color:var(--lv-ink)}
.note-actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:14px}
.copy-fallback{margin-top:12px}
.copy-fallback textarea{min-height:140px;font-size:.875rem}

/* History */
.hist{display:grid;gap:36px;grid-template-columns:minmax(0,340px) minmax(0,1fr);align-items:start}
@media (max-width:820px){.hist{grid-template-columns:minmax(0,1fr)}}
.hlist{list-style:none;margin:0 0 20px;padding:0;border-bottom:1px solid var(--line)}
.hitem{display:grid;width:100%;text-align:left;gap:2px;background:none;border:0;border-top:1px solid var(--line);padding:12px 10px;cursor:pointer}
.hitem[aria-current="true"]{background:var(--brand-soft)}
.hitem .hn{font-weight:700}
.hitem .hd{color:var(--muted);font-size:.8125rem}
.hitem .hc{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;color:var(--muted)}
.hitem .badge{justify-self:start;margin-top:4px}
.empty{padding:18px 0;color:var(--muted)}
.confirm{display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-top:14px}
.confirm p{font-weight:600;margin-right:6px}

.toast{position:fixed;left:50%;bottom:22px;transform:translateX(-50%);background:var(--ink);color:var(--bg);padding:.7rem 1.1rem;border-radius:10px;font-weight:600;font-size:.9375rem;z-index:60;max-width:calc(100vw - 32px);box-shadow:var(--shadow)}
.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0);white-space:nowrap}

@media (prefers-reduced-motion:reduce){
  .strip.fresh path{animation:none;stroke-dashoffset:0}
}
@media print{
  body{background:#fff}
  .chrome,.no-print,.view-switch,.form-col,.toast{display:none !important}
  main{padding:0;max-width:none}
  .layout,.hist{display:block}
  .note-col{position:static;max-height:none;overflow:visible}
  .paper,.paper *{color:#000 !important;background:#fff !important;box-shadow:none !important}
  .paper{border:0;padding:0}
  .strip,.badge{border:1px solid #000}
  .ns{break-inside:avoid}
}
</style>
</head>
<body>
<noscript><p style="padding:24px">CliniScribe needs JavaScript to run. Turn it on for this page and reload.</p></noscript>

<div class="chrome" id="chrome">
  <div class="top">
    <div class="brand">
      <svg viewBox="0 0 32 32" aria-hidden="true"><rect x="1" y="1" width="30" height="30" rx="9" fill="var(--brand)"/><path d="M5 17h5l2.6-6 3.6 12 2.8-8H27" fill="none" stroke="var(--brand-ink)" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
      <span>CliniScribe</span>
    </div>
    <nav class="tabs" aria-label="Main">
      <button type="button" class="tab" data-nav="intake" aria-current="page"><span data-i18n="New intake">New intake</span></button>
      <button type="button" class="tab" data-nav="history"><span data-i18n="Saved visits">Saved visits</span><span class="count" id="count" hidden>0</span></button>
      <select class="lang-sel" id="langSel" data-i18n-aria="Language" aria-label="Language"></select>
      <button type="button" class="icon-btn" data-act="theme" data-i18n-aria="Switch between light and dark theme" aria-label="Switch between light and dark theme">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M12 3v18" /><path d="M12 3a9 9 0 0 1 0 18z" fill="currentColor"/></svg>
      </button>
    </nav>
  </div>
  <div id="emergencyBar" role="alert" hidden></div>
</div>

<main>
  <section id="viewIntake" aria-label="New intake">
    <div class="layout" id="layout" data-view="form">
      <div class="view-switch" role="group" aria-label="Choose what to show">
        <button type="button" data-view="form" aria-pressed="true"><span data-i18n="Your answers">Your answers</span></button>
        <button type="button" data-view="note" aria-pressed="false"><span data-i18n="Note">Note</span><span class="dot" id="noteDot" data-level="pending"></span></button>
      </div>

      <section class="form-col" id="leftCol">
        <div id="consentPane">
          <div class="langbox">
            <p class="group-title" data-i18n="Choose your language">Choose your language</p>
            <div class="chips" id="langPick" role="radiogroup" aria-label="Language"></div>
          </div>
          <h1 data-i18n="Tell us what's going on before your visit.">Tell us what's going on before your visit.</h1>
          <p class="lede" data-i18n="Answer a few questions in about five minutes. CliniScribe turns them into a one-page note you can show or send to your doctor. If you're filling this in for a child or relative, enter their details.">Answer a few questions in about five minutes. CliniScribe turns them into a one-page note you can show or send to your doctor. If you're filling this in for a child or relative, enter their details.</p>
          <div class="resume" id="resumeBox" hidden></div>
          <ul class="promises">
            <li><strong data-i18n="Your answers stay on this device.">Your answers stay on this device.</strong><span data-i18n="Nothing is sent to a server. Clearing your browser data deletes saved visits.">Nothing is sent to a server. Clearing your browser data deletes saved visits.</span></li>
            <li><strong data-i18n="This is not a diagnosis.">This is not a diagnosis.</strong><span data-i18n="The safety check follows simple rules and can miss things. A doctor should always review your note.">The safety check follows simple rules and can miss things. A doctor should always review your note.</span></li>
            <li><strong data-i18n="In an emergency, call 112.">In an emergency, call 112.</strong><span data-i18n="Use your local emergency number if you're outside India. Don't fill in a form first.">Use your local emergency number if you're outside India. Don't fill in a form first.</span></li>
          </ul>
          <label class="agree"><input type="checkbox" id="agree"><span data-i18n="I understand, and I want to continue.">I understand, and I want to continue.</span></label>
          <button type="button" class="btn primary" id="startBtn" data-i18n="Start intake" disabled>Start intake</button>
        </div>

        <div id="wizardPane" hidden>
          <ol class="steps" id="steps" aria-label="Progress"></ol>
          <div id="stepBody"></div>
          <div class="nav" id="nav"></div>
        </div>
      </section>

      <aside class="note-col" aria-label="Live note">
        <div class="notelang no-print" id="noteLangBox" hidden></div>
        <div id="noteBody"></div>
        <div class="note-actions no-print">
          <button type="button" class="btn secondary" data-act="copy-live" data-i18n="Copy note">Copy note</button>
          <button type="button" class="btn secondary" data-act="print" data-i18n="Print">Print</button>
        </div>
        <div class="copy-fallback no-print" id="copyFallbackLive" hidden></div>
      </aside>
    </div>
  </section>

  <section id="viewHistory" aria-label="Saved visits" hidden>
    <div class="hist">
      <div class="no-print">
        <h1 style="font-size:2.2rem" data-i18n="Saved visits">Saved visits</h1>
        <p class="lede" style="margin-bottom:18px" data-i18n="Stored only in this browser. If you clear your browser data or switch devices, they're gone, so copy any note you want to keep.">Stored only in this browser. If you clear your browser data or switch devices, they're gone, so copy any note you want to keep.</p>
        <ul class="hlist" id="histList"></ul>
        <div id="wipeBox"></div>
      </div>
      <div id="histDetail"></div>
    </div>
  </section>
</main>

<div class="toast" id="toast" role="status" aria-live="polite" hidden></div>

<script>
(() => {
'use strict';

/* ---------- helpers ---------- */
const $ = (s, r = document) => r.querySelector(s);
const $$ = (s, r = document) => Array.from(r.querySelectorAll(s));
const esc = s => String(s == null ? '' : s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const uid = () => Date.now().toString(36) + Math.random().toString(36).slice(2, 6);
const getPath = (o, p) => p.split('.').reduce((a, k) => a == null ? a : a[k], o);
const setPath = (o, p, v) => { const ks = p.split('.'); const last = ks.pop(); const t = ks.reduce((a, k) => a[k], o); t[last] = v; };
const store = {
  get(k){ try { const v = localStorage.getItem(k); return v ? JSON.parse(v) : null; } catch (e) { return null; } },
  set(k, v){ try { localStorage.setItem(k, JSON.stringify(v)); return true; } catch (e) { return false; } },
  del(k){ try { localStorage.removeItem(k); } catch (e) {} }
};

/* ---------- languages ----------
   Keys are the English text. Stored data always keeps the English value,
   so notes stay consistent and any language can be shown from the same record. */
const NATIVE = {en:'English', hi:'हिन्दी', te:'తెలుగు', ta:'தமிழ்', kn:'ಕನ್ನಡ'};
const LOC = {en:'en-IN', hi:'hi-IN', te:'te-IN', ta:'ta-IN', kn:'kn-IN'};
const LANGS = ['hi', 'te', 'ta', 'kn'];
/* row = [English, Hindi, Telugu, Tamil, Kannada] */
const TABLE = [
["New intake","नई प्रविष्टि","కొత్త నమోదు","புதிய பதிவு","ಹೊಸ ನೋಂದಣಿ"],
["Saved visits","सहेजी गई विज़िट","సేవ్ చేసిన సందర్శనలు","சேமித்த வருகைகள்","ಉಳಿಸಿದ ಭೇಟಿಗಳು"],
["Switch between light and dark theme","लाइट और डार्क थीम बदलें","లైట్/డార్క్ థీమ్ మార్చండి","ஒளி/இருள் தீமை மாற்றவும்","ಲೈಟ್/ಡಾರ್ಕ್ ಥೀಮ್ ಬದಲಿಸಿ"],
["Language","भाषा","భాష","மொழி","ಭಾಷೆ"],
["Your answers","आपके उत्तर","మీ సమాధానాలు","உங்கள் பதில்கள்","ನಿಮ್ಮ ಉತ್ತರಗಳು"],
["Note","नोट","నోట్","குறிப்பு","ಟಿಪ್ಪಣಿ"],
["Choose your language","अपनी भाषा चुनें","మీ భాషను ఎంచుకోండి","உங்கள் மொழியைத் தேர்ந்தெடுக்கவும்","ನಿಮ್ಮ ಭಾಷೆಯನ್ನು ಆರಿಸಿ"],
["Tell us what's going on before your visit.","डॉक्टर के पास जाने से पहले हमें बताइए कि क्या हो रहा है।","డాక్టర్‌ను కలవడానికి ముందు మీకు ఏమి జరుగుతోందో మాకు చెప్పండి.","மருத்துவரைப் பார்ப்பதற்கு முன் உங்களுக்கு என்ன நடக்கிறது என்று சொல்லுங்கள்.","ವೈದ್ಯರನ್ನು ಭೇಟಿಯಾಗುವ ಮೊದಲು ನಿಮಗೆ ಏನಾಗುತ್ತಿದೆ ಎಂದು ನಮಗೆ ತಿಳಿಸಿ."],
["Answer a few questions in about five minutes. CliniScribe turns them into a one-page note you can show or send to your doctor. If you're filling this in for a child or relative, enter their details.","करीब पाँच मिनट में कुछ सवालों के जवाब दीजिए। CliniScribe उन्हें एक पन्ने के नोट में बदल देता है, जो आप अपने डॉक्टर को दिखा या भेज सकते हैं। अगर आप किसी बच्चे या रिश्तेदार के लिए भर रहे हैं, तो उनका विवरण भरें।","సుమారు ఐదు నిమిషాల్లో కొన్ని ప్రశ్నలకు సమాధానం ఇవ్వండి. CliniScribe వాటిని ఒక పేజీ నోట్‌గా మారుస్తుంది; దాన్ని మీ డాక్టర్‌కు చూపించవచ్చు లేదా పంపవచ్చు. మీరు పిల్లల కోసం లేదా బంధువు కోసం నింపుతున్నట్లయితే, వారి వివరాలు నమోదు చేయండి.","சுமார் ஐந்து நிமிடங்களில் சில கேள்விகளுக்குப் பதிலளியுங்கள். CliniScribe அவற்றை ஒரு பக்கக் குறிப்பாக மாற்றும்; அதை உங்கள் மருத்துவரிடம் காட்டலாம் அல்லது அனுப்பலாம். குழந்தை அல்லது உறவினருக்காக நிரப்பினால், அவர்களின் விவரங்களை உள்ளிடுங்கள்.","ಸುಮಾರು ಐದು ನಿಮಿಷಗಳಲ್ಲಿ ಕೆಲವು ಪ್ರಶ್ನೆಗಳಿಗೆ ಉತ್ತರಿಸಿ. CliniScribe ಅವುಗಳನ್ನು ಒಂದು ಪುಟದ ಟಿಪ್ಪಣಿಯಾಗಿ ಮಾಡುತ್ತದೆ; ಅದನ್ನು ನಿಮ್ಮ ವೈದ್ಯರಿಗೆ ತೋರಿಸಬಹುದು ಅಥವಾ ಕಳುಹಿಸಬಹುದು. ನೀವು ಮಗು ಅಥವಾ ಸಂಬಂಧಿಕರ ಪರವಾಗಿ ತುಂಬುತ್ತಿದ್ದರೆ, ಅವರ ವಿವರಗಳನ್ನು ನಮೂದಿಸಿ."],
["Your answers stay on this device.","आपके उत्तर इसी डिवाइस पर रहते हैं।","మీ సమాధానాలు ఈ పరికరంలోనే ఉంటాయి.","உங்கள் பதில்கள் இந்தச் சாதனத்திலேயே இருக்கும்.","ನಿಮ್ಮ ಉತ್ತರಗಳು ಈ ಸಾಧನದಲ್ಲಿಯೇ ಇರುತ್ತವೆ."],
["Nothing is sent to a server. Clearing your browser data deletes saved visits.","कुछ भी सर्वर पर नहीं भेजा जाता। ब्राउज़र डेटा साफ़ करने पर सहेजी गई विज़िट मिट जाती हैं।","ఏదీ సర్వర్‌కు పంపబడదు. బ్రౌజర్ డేటాను క్లియర్ చేస్తే సేవ్ చేసిన సందర్శనలు తొలగిపోతాయి.","எதுவும் சர்வருக்கு அனுப்பப்படுவதில்லை. உலாவித் தரவை அழித்தால் சேமித்த வருகைகள் நீக்கப்படும்.","ಯಾವುದೂ ಸರ್ವರ್‌ಗೆ ಕಳುಹಿಸಲಾಗುವುದಿಲ್ಲ. ಬ್ರೌಸರ್ ಡೇಟಾ ಅಳಿಸಿದರೆ ಉಳಿಸಿದ ಭೇಟಿಗಳು ಅಳಿಯುತ್ತವೆ."],
["This is not a diagnosis.","यह कोई निदान नहीं है।","ఇది రోగనిర్ధారణ కాదు.","இது நோய் கண்டறிதல் அல்ல.","ಇದು ರೋಗನಿರ್ಣಯವಲ್ಲ."],
["The safety check follows simple rules and can miss things. A doctor should always review your note.","सुरक्षा जाँच सरल नियमों पर चलती है और कुछ बातें छूट सकती हैं। आपके नोट को हमेशा डॉक्टर से दिखाइए।","భద్రతా తనిఖీ సాధారణ నియమాలను అనుసరిస్తుంది, కొన్ని విషయాలను గుర్తించకపోవచ్చు. మీ నోట్‌ను ఎల్లప్పుడూ డాక్టర్ పరిశీలించాలి.","பாதுகாப்புச் சோதனை எளிய விதிகளைப் பின்பற்றுகிறது; சிலவற்றைத் தவறவிடலாம். உங்கள் குறிப்பை எப்போதும் மருத்துவர் பார்க்க வேண்டும்.","ಸುರಕ್ಷತಾ ಪರಿಶೀಲನೆ ಸರಳ ನಿಯಮಗಳನ್ನು ಅನುಸರಿಸುತ್ತದೆ, ಕೆಲವು ಸಂಗತಿಗಳನ್ನು ತಪ್ಪಿಸಬಹುದು. ನಿಮ್ಮ ಟಿಪ್ಪಣಿಯನ್ನು ಯಾವಾಗಲೂ ವೈದ್ಯರು ಪರಿಶೀಲಿಸಬೇಕು."],
["In an emergency, call 112.","आपातकाल में 112 पर कॉल करें।","అత్యవసర పరిస్థితిలో 112కు కాల్ చేయండి.","அவசர நிலையில் 112-ஐ அழைக்கவும்.","ತುರ್ತು ಪರಿಸ್ಥಿತಿಯಲ್ಲಿ 112ಕ್ಕೆ ಕರೆ ಮಾಡಿ."],
["Use your local emergency number if you're outside India. Don't fill in a form first.","अगर आप भारत से बाहर हैं तो अपने स्थानीय आपातकालीन नंबर का उपयोग करें। पहले फ़ॉर्म न भरें।","మీరు భారతదేశం వెలుపల ఉంటే స్థానిక అత్యవసర నంబర్‌ను ఉపయోగించండి. ముందుగా ఫారం నింపకండి.","நீங்கள் இந்தியாவுக்கு வெளியே இருந்தால் உள்ளூர் அவசர எண்ணைப் பயன்படுத்துங்கள். முதலில் படிவத்தை நிரப்ப வேண்டாம்.","ನೀವು ಭಾರತದ ಹೊರಗಿದ್ದರೆ ಸ್ಥಳೀಯ ತುರ್ತು ಸಂಖ್ಯೆಯನ್ನು ಬಳಸಿ. ಮೊದಲು ಫಾರ್ಮ್ ತುಂಬಬೇಡಿ."],
["I understand, and I want to continue.","मैं समझता/समझती हूँ, आगे बढ़ना चाहता/चाहती हूँ।","నాకు అర్థమైంది, కొనసాగించాలనుకుంటున్నాను.","எனக்குப் புரிகிறது, தொடர விரும்புகிறேன்.","ನನಗೆ ಅರ್ಥವಾಗಿದೆ, ಮುಂದುವರಿಯಲು ಬಯಸುತ್ತೇನೆ."],
["Start intake","शुरू करें","ప్రారంభించండి","தொடங்கவும்","ಪ್ರಾರಂಭಿಸಿ"],
["You have an unfinished intake from {d}.","{d} से आपकी एक अधूरी प्रविष्टि है।","{d} నుండి మీకు పూర్తికాని నమోదు ఉంది.","{d} முதல் உங்களுக்கு முடிக்கப்படாத பதிவு உள்ளது.","{d} ರಿಂದ ನಿಮ್ಮ ಅಪೂರ್ಣ ನೋಂದಣಿ ಇದೆ."],
["Resume it","जारी रखें","కొనసాగించండి","தொடரவும்","ಮುಂದುವರಿಸಿ"],
["Start over","फिर से शुरू करें","మళ్ళీ మొదలుపెట్టండి","மீண்டும் தொடங்கவும்","ಮತ್ತೆ ಪ್ರಾರಂಭಿಸಿ"],
["Copy note","नोट कॉपी करें","నోట్ కాపీ చేయండి","குறிப்பை நகலெடுக்கவும்","ಟಿಪ್ಪಣಿ ನಕಲಿಸಿ"],
["Print","प्रिंट करें","ప్రింట్ చేయండి","அச்சிடவும்","ಮುದ್ರಿಸಿ"],
["Show note in","नोट दिखाएँ:","నోట్ ఈ భాషలో చూపు:","குறிப்பைக் காட்டு:","ಟಿಪ್ಪಣಿ ತೋರಿಸಿ:"],
["English is best for your doctor. Your own words stay as you typed them.","डॉक्टर के लिए अंग्रेज़ी सबसे अच्छी है। आपके अपने शब्द वैसे ही रहते हैं जैसे आपने लिखे।","డాక్టర్‌కు ఇంగ్లీష్ ఉత్తమం. మీరు టైప్ చేసిన మీ స్వంత మాటలు అలాగే ఉంటాయి.","மருத்துவருக்கு ஆங்கிலம் சிறந்தது. நீங்கள் தட்டச்சு செய்த உங்கள் சொந்த வார்த்தைகள் அப்படியே இருக்கும்.","ವೈದ್ಯರಿಗೆ ಇಂಗ್ಲಿಷ್ ಉತ್ತಮ. ನೀವು ಟೈಪ್ ಮಾಡಿದ ನಿಮ್ಮ ಸ್ವಂತ ಮಾತುಗಳು ಹಾಗೆಯೇ ಇರುತ್ತವೆ."],
["About you","आपके बारे में","మీ గురించి","உங்களைப் பற்றி","ನಿಮ್ಮ ಬಗ್ಗೆ"],
["Safety check","सुरक्षा जाँच","భద్రతా తనిఖీ","பாதுகாப்புச் சோதனை","ಸುರಕ್ಷತಾ ಪರಿಶೀಲನೆ"],
["Your symptoms","आपके लक्षण","మీ లక్షణాలు","உங்கள் அறிகுறிகள்","ನಿಮ್ಮ ಲಕ್ಷಣಗಳು"],
["Background","स्वास्थ्य इतिहास","ఆరోగ్య నేపథ్యం","உடல்நலப் பின்னணி","ಆರೋಗ್ಯ ಹಿನ್ನೆಲೆ"],
["Medicines and allergies","दवाएँ और एलर्जी","మందులు మరియు అలెర్జీలు","மருந்துகள் மற்றும் ஒவ்வாமைகள்","ಔಷಧಿಗಳು ಮತ್ತು ಅಲರ್ಜಿಗಳು"],
["Review and save","जाँचें और सहेजें","సమీక్షించి సేవ్ చేయండి","சரிபார்த்துச் சேமிக்கவும்","ಪರಿಶೀಲಿಸಿ ಮತ್ತು ಉಳಿಸಿ"],
["Step {n} of 6","चरण {n} / 6","దశ {n} / 6","படி {n} / 6","ಹಂತ {n} / 6"],
["Only what your doctor needs to put your symptoms in context.","सिर्फ़ वही जो डॉक्टर को आपके लक्षण समझने के लिए चाहिए।","మీ లక్షణాలను అర్థం చేసుకోవడానికి డాక్టర్‌కు అవసరమైనవి మాత్రమే.","உங்கள் அறிகுறிகளைப் புரிந்துகொள்ள மருத்துவருக்குத் தேவையானவை மட்டும்.","ನಿಮ್ಮ ಲಕ್ಷಣಗಳನ್ನು ಅರ್ಥಮಾಡಿಕೊಳ್ಳಲು ವೈದ್ಯರಿಗೆ ಬೇಕಾದವು ಮಾತ್ರ."],
["Name or nickname","नाम या उपनाम","పేరు లేదా ముద్దుపేరు","பெயர் அல்லது செல்லப்பெயர்","ಹೆಸರು ಅಥವಾ ಅಡ್ಡಹೆಸರು"],
["Age in years","उम्र (वर्षों में)","వయస్సు (సంవత్సరాల్లో)","வயது (ஆண்டுகளில்)","ವಯಸ್ಸು (ವರ್ಷಗಳಲ್ಲಿ)"],
["Sex","लिंग","లింగం","பாலினம்","ಲಿಂಗ"],
["Female","महिला","స్త్రీ","பெண்","ಮಹಿಳೆ"],
["Male","पुरुष","పురుషుడు","ஆண்","ಪುರುಷ"],
["Other","अन्य","ఇతర","மற்றவை","ಇತರೆ"],
["Prefer not to say","बताना नहीं चाहते","చెప్పడానికి ఇష్టం లేదు","சொல்ல விரும்பவில்லை","ಹೇಳಲು ಇಷ್ಟವಿಲ್ಲ"],
["Are you pregnant, or could you be?","क्या आप गर्भवती हैं, या हो सकती हैं?","మీరు గర్భవతా, లేదా అయి ఉండవచ్చా?","நீங்கள் கர்ப்பமாக இருக்கிறீர்களா, அல்லது இருக்கலாமா?","ನೀವು ಗರ್ಭಿಣಿಯೇ, ಅಥವಾ ಆಗಿರಬಹುದೇ?"],
["Yes","हाँ","అవును","ஆம்","ಹೌದು"],
["No","नहीं","కాదు","இல்லை","ಇಲ್ಲ"],
["Not sure","पक्का नहीं","ఖచ్చితంగా తెలియదు","உறுதியாகத் தெரியாது","ಖಚಿತವಿಲ್ಲ"],
["Enter your name or a nickname so the note can be matched to you.","अपना नाम या उपनाम भरें ताकि नोट आपसे जोड़ा जा सके।","నోట్‌ను మీతో జత చేయడానికి మీ పేరు లేదా ముద్దుపేరు నమోదు చేయండి.","குறிப்பை உங்களுடன் பொருத்த உங்கள் பெயர் அல்லது செல்லப்பெயரை உள்ளிடுங்கள்.","ಟಿಪ್ಪಣಿಯನ್ನು ನಿಮ್ಮೊಂದಿಗೆ ಹೊಂದಿಸಲು ನಿಮ್ಮ ಹೆಸರು ಅಥವಾ ಅಡ್ಡಹೆಸರು ನಮೂದಿಸಿ."],
["Enter an age between 0 and 120.","0 से 120 के बीच उम्र भरें।","0 నుండి 120 మధ్య వయస్సు నమోదు చేయండి.","0 முதல் 120 வரையிலான வயதை உள்ளிடுங்கள்.","0 ರಿಂದ 120ರ ನಡುವಿನ ವಯಸ್ಸನ್ನು ನಮೂದಿಸಿ."],
["Tick anything that applies right now. If you tick one, get emergency help first. You can finish this note afterwards.","अभी जो भी लागू हो उसे चुनें। अगर आप कोई चुनते हैं, तो पहले आपातकालीन मदद लें। यह नोट बाद में पूरा कर सकते हैं।","ఇప్పుడు వర్తించే వాటిని టిక్ చేయండి. ఏదైనా టిక్ చేస్తే, ముందు అత్యవసర సహాయం పొందండి. ఈ నోట్‌ను తర్వాత పూర్తి చేయవచ్చు.","இப்போது பொருந்தும் எதையும் குறிக்கவும். ஏதாவது குறித்தால், முதலில் அவசர உதவி பெறுங்கள். இந்தக் குறிப்பைப் பிறகு முடிக்கலாம்.","ಈಗ ಅನ್ವಯಿಸುವುದನ್ನು ಗುರುತಿಸಿ. ಯಾವುದನ್ನಾದರೂ ಗುರುತಿಸಿದರೆ, ಮೊದಲು ತುರ್ತು ಸಹಾಯ ಪಡೆಯಿರಿ. ಈ ಟಿಪ್ಪಣಿಯನ್ನು ನಂತರ ಪೂರ್ಣಗೊಳಿಸಬಹುದು."],
["Emergency symptoms","आपातकालीन लक्षण","అత్యవసర లక్షణాలు","அவசர அறிகுறிகள்","ತುರ್ತು ಲಕ್ಷಣಗಳು"],
["Chest pain, pressure or tightness right now","अभी सीने में दर्द, दबाव या जकड़न","ఇప్పుడు ఛాతీలో నొప్పి, ఒత్తిడి లేదా బిగుతు","இப்போது மார்பில் வலி, அழுத்தம் அல்லது இறுக்கம்","ಈಗ ಎದೆಯಲ್ಲಿ ನೋವು, ಒತ್ತಡ ಅಥವಾ ಬಿಗಿತ"],
["Severe difficulty breathing, or unable to speak a full sentence","सांस लेने में बहुत कठिनाई, या पूरा वाक्य बोल न पाना","శ్వాస తీసుకోవడంలో తీవ్రమైన ఇబ్బంది, లేదా పూర్తి వాక్యం మాట్లాడలేకపోవడం","மூச்சு விடுவதில் கடுமையான சிரமம், அல்லது முழு வாக்கியம் பேச முடியாமை","ಉಸಿರಾಡಲು ತೀವ್ರ ತೊಂದರೆ, ಅಥವಾ ಪೂರ್ಣ ವಾಕ್ಯ ಮಾತನಾಡಲು ಆಗದಿರುವುದು"],
["Sudden weakness or numbness on one side, a drooping face, or slurred speech","अचानक एक तरफ़ कमज़ोरी या सुन्नपन, चेहरा टेढ़ा होना, या अस्पष्ट बोलना","ఒక వైపు అకస్మాత్తుగా బలహీనత లేదా తిమ్మిరి, ముఖం వాలిపోవడం, లేదా మాట తడబడటం","ஒரு பக்கம் திடீர் பலவீனம் அல்லது மரத்துப்போதல், முகம் கோணல், அல்லது குழறிய பேச்சு","ಒಂದು ಬದಿಯಲ್ಲಿ ಹಠಾತ್ ದೌರ್ಬಲ್ಯ ಅಥವಾ ಜೋಮು, ಮುಖ ಕುಸಿಯುವುದು, ಅಥವಾ ತೊದಲುವ ಮಾತು"],
["A sudden, severe headache, the worst you have ever had","अचानक तेज़ सिरदर्द, जो अब तक का सबसे बुरा हो","అకస్మాత్తుగా తీవ్రమైన తలనొప్పి, ఇంతవరకు వచ్చిన వాటిలో అత్యంత దారుణమైనది","திடீரென கடுமையான தலைவலி, இதுவரை இல்லாத மிக மோசமானது","ಹಠಾತ್ ತೀವ್ರ ತಲೆನೋವು, ಇದುವರೆಗಿನ ಅತ್ಯಂತ ಕೆಟ್ಟದು"],
["Fainting or loss of consciousness","बेहोशी या होश खोना","మూర్ఛపోవడం లేదా స్పృహ కోల్పోవడం","மயக்கம் அல்லது நினைவிழப்பு","ಮೂರ್ಛೆ ಅಥವಾ ಪ್ರಜ್ಞೆ ತಪ್ಪುವುದು"],
["A seizure","दौरा पड़ना","ఫిట్స్ (మూర్ఛ)","வலிப்பு","ಸೆಳೆತ (ಫಿಟ್ಸ್)"],
["Vomiting blood, black stools, or bleeding that will not stop","खून की उल्टी, काला मल, या रुकता न हुआ रक्तस्राव","రక్తం వాంతులు, నల్లని మలం, లేదా ఆగని రక్తస్రావం","இரத்த வாந்தி, கருப்பு மலம், அல்லது நிற்காத இரத்தப்போக்கு","ರಕ್ತ ವಾಂತಿ, ಕಪ್ಪು ಮಲ, ಅಥವಾ ನಿಲ್ಲದ ರಕ್ತಸ್ರಾವ"],
["Swelling of the lips, tongue or throat after food, medicine or a sting","खाने, दवा या डंक के बाद होंठ, जीभ या गले में सूजन","ఆహారం, మందు లేదా కుట్టిన తర్వాత పెదవులు, నాలుక లేదా గొంతు వాపు","உணவு, மருந்து அல்லது கடிக்குப் பிறகு உதடு, நாக்கு அல்லது தொண்டை வீக்கம்","ಆಹಾರ, ಔಷಧಿ ಅಥವಾ ಕಡಿತದ ನಂತರ ತುಟಿ, ನಾಲಿಗೆ ಅಥವಾ ಗಂಟಲು ಊತ"],
["Thoughts of harming yourself or ending your life","खुद को नुकसान पहुँचाने या जीवन खत्म करने के विचार","మిమ్మల్ని మీరు హాని చేసుకోవడం లేదా జీవితం ముగించుకోవడం గురించి ఆలోచనలు","உங்களைத் தீங்கு செய்துகொள்ளும் அல்லது வாழ்க்கையை முடித்துக்கொள்ளும் எண்ணங்கள்","ನಿಮಗೆ ಹಾನಿ ಮಾಡಿಕೊಳ್ಳುವ ಅಥವಾ ಜೀವ ಕೊನೆಗೊಳಿಸುವ ಆಲೋಚನೆಗಳು"],
["chest pain or pressure right now","अभी सीने में दर्द या दबाव","ఇప్పుడు ఛాతీ నొప్పి లేదా ఒత్తిడి","இப்போது மார்பு வலி அல்லது அழுத்தம்","ಈಗ ಎದೆ ನೋವು ಅಥವಾ ಒತ್ತಡ"],
["severe difficulty breathing","सांस लेने में बहुत कठिनाई","శ్వాసలో తీవ్రమైన ఇబ్బంది","மூச்சுவிடுவதில் கடுமையான சிரமம்","ಉಸಿರಾಟದಲ್ಲಿ ತೀವ್ರ ತೊಂದರೆ"],
["possible stroke signs","स्ट्रोक के संभावित संकेत","స్ట్రోక్ సంకేతాలు అయి ఉండవచ్చు","பக்கவாதத்தின் சாத்தியமான அறிகுறிகள்","ಪಾರ್ಶ್ವವಾಯುವಿನ ಸಂಭಾವ್ಯ ಲಕ್ಷಣಗಳು"],
["sudden severe headache","अचानक तेज़ सिरदर्द","అకస్మాత్తుగా తీవ్రమైన తలనొప్పి","திடீர் கடுமையான தலைவலி","ಹಠಾತ್ ತೀವ್ರ ತಲೆನೋವು"],
["fainting or loss of consciousness","बेहोशी या होश खोना","మూర్ఛపోవడం లేదా స్పృహ కోల్పోవడం","மயக்கம் அல்லது நினைவிழப்பு","ಮೂರ್ಛೆ ಅಥವಾ ಪ್ರಜ್ಞೆ ತಪ್ಪುವುದು"],
["a seizure","दौरा","ఫిట్స్","வலிப்பு","ಸೆಳೆತ"],
["serious bleeding","गंभीर रक्तस्राव","తీవ్రమైన రక్తస్రావం","கடுமையான இரத்தப்போக்கு","ತೀವ್ರ ರಕ್ತಸ್ರಾವ"],
["possible severe allergic reaction","गंभीर एलर्जी की संभावित प्रतिक्रिया","తీవ్రమైన అలెర్జీ ప్రతిచర్య అయి ఉండవచ్చు","கடுமையான ஒவ்வாமை எதிர்வினை இருக்கலாம்","ತೀವ್ರ ಅಲರ್ಜಿ ಪ್ರತಿಕ್ರಿಯೆ ಇರಬಹುದು"],
["thoughts of self-harm","खुद को नुकसान पहुँचाने के विचार","స్వీయ హాని ఆలోచనలు","தன்னைத் தானே தீங்கு செய்யும் எண்ணங்கள்","ಸ್ವಯಂ ಹಾನಿಯ ಆಲೋಚನೆಗಳು"],
["You reported {x}.","आपने बताया: {x}।","మీరు తెలిపారు: {x}.","நீங்கள் தெரிவித்தது: {x}.","ನೀವು ತಿಳಿಸಿದ್ದು: {x}."],
["Nothing ticked? Continue. That's the answer we need.","कुछ नहीं चुना? आगे बढ़ें। हमें यही जवाब चाहिए।","ఏదీ టిక్ చేయలేదా? కొనసాగండి. మాకు కావలసిన సమాధానం అదే.","எதுவும் குறிக்கவில்லையா? தொடருங்கள். எங்களுக்குத் தேவையான பதில் அதுதான்.","ಯಾವುದೂ ಗುರುತಿಸಿಲ್ಲವೇ? ಮುಂದುವರಿಯಿರಿ. ನಮಗೆ ಬೇಕಾದ ಉತ್ತರ ಅದೇ."],
["Continue","आगे बढ़ें","కొనసాగండి","தொடர்க","ಮುಂದುವರಿಯಿರಿ"],
["Continue anyway","फिर भी आगे बढ़ें","అయినా కొనసాగండి","இருந்தாலும் தொடரவும்","ಆದರೂ ಮುಂದುವರಿಯಿರಿ"],
["Back","पीछे","వెనుకకు","பின்","ಹಿಂದೆ"],
["Save visit","विज़िट सहेजें","సందర్శన సేవ్ చేయండి","வருகையைச் சேமிக்கவும்","ಭೇಟಿ ಉಳಿಸಿ"],
["View saved visits","सहेजी गई विज़िट देखें","సేవ్ చేసిన సందర్శనలు చూడండి","சேமித்த வருகைகளைப் பார்க்கவும்","ಉಳಿಸಿದ ಭೇಟಿಗಳನ್ನು ನೋಡಿ"],
["Start new intake","नई प्रविष्टि शुरू करें","కొత్త నమోదు ప్రారంభించండి","புதிய பதிவைத் தொடங்கவும்","ಹೊಸ ನೋಂದಣಿ ಪ್ರಾರಂಭಿಸಿ"],
["You reported symptoms that need emergency care.","आपने ऐसे लक्षण बताए हैं जिनके लिए आपातकालीन देखभाल ज़रूरी है।","మీరు అత్యవసర వైద్యం అవసరమైన లక్షణాలను తెలిపారు.","நீங்கள் அவசர சிகிச்சை தேவைப்படும் அறிகுறிகளைத் தெரிவித்துள்ளீர்கள்.","ನೀವು ತುರ್ತು ಚಿಕಿತ್ಸೆ ಅಗತ್ಯವಿರುವ ಲಕ್ಷಣಗಳನ್ನು ತಿಳಿಸಿದ್ದೀರಿ."],
["Call {tel} (or your local emergency number) or go to the nearest emergency department now. Do not drive yourself.","अभी {tel} पर कॉल करें (या अपना स्थानीय आपातकालीन नंबर) या नज़दीकी आपातकालीन विभाग में जाएँ। खुद गाड़ी न चलाएँ।","ఇప్పుడే {tel}కు కాల్ చేయండి (లేదా మీ స్థానిక అత్యవసర నంబర్) లేదా సమీప అత్యవసర విభాగానికి వెళ్లండి. మీరే వాహనం నడపకండి.","இப்போதே {tel}-ஐ அழைக்கவும் (அல்லது உங்கள் உள்ளூர் அவசர எண்) அல்லது அருகிலுள்ள அவசர சிகிச்சைப் பிரிவுக்குச் செல்லுங்கள். நீங்களே வாகனம் ஓட்ட வேண்டாம்.","ಈಗಲೇ {tel}ಗೆ ಕರೆ ಮಾಡಿ (ಅಥವಾ ನಿಮ್ಮ ಸ್ಥಳೀಯ ತುರ್ತು ಸಂಖ್ಯೆ) ಅಥವಾ ಹತ್ತಿರದ ತುರ್ತು ವಿಭಾಗಕ್ಕೆ ಹೋಗಿ. ನೀವೇ ವಾಹನ ಚಲಾಯಿಸಬೇಡಿ."],
["If you are thinking of harming yourself, call Tele-MANAS on {tel} (India, free, 24 hours a day) or tell someone near you right now.","अगर आप खुद को नुकसान पहुँचाने के बारे में सोच रहे हैं, तो Tele-MANAS को {tel} पर कॉल करें (भारत, मुफ़्त, 24 घंटे) या अभी अपने पास के किसी व्यक्ति को बताएँ।","మీరు మిమ్మల్ని మీరు హాని చేసుకోవాలని ఆలోచిస్తుంటే, Tele-MANASకు {tel}లో కాల్ చేయండి (భారతదేశం, ఉచితం, 24 గంటలు) లేదా వెంటనే మీ దగ్గరున్న ఎవరికైనా చెప్పండి.","நீங்கள் உங்களைத் தீங்கு செய்துகொள்ள நினைத்தால், Tele-MANAS-ஐ {tel} என்ற எண்ணில் அழைக்கவும் (இந்தியா, இலவசம், 24 மணி நேரம்) அல்லது உடனே உங்கள் அருகில் உள்ள ஒருவரிடம் சொல்லுங்கள்.","ನಿಮಗೆ ಹಾನಿ ಮಾಡಿಕೊಳ್ಳುವ ಆಲೋಚನೆ ಇದ್ದರೆ, Tele-MANAS ಗೆ {tel} ನಲ್ಲಿ ಕರೆ ಮಾಡಿ (ಭಾರತ, ಉಚಿತ, 24 ಗಂಟೆ) ಅಥವಾ ಈಗಲೇ ನಿಮ್ಮ ಹತ್ತಿರದ ಯಾರಿಗಾದರೂ ತಿಳಿಸಿ."],
["Describe it the way you would to a friend. Details matter more than medical words.","इसे ऐसे बताइए जैसे किसी दोस्त को बताते। विवरण चिकित्सा शब्दों से ज़्यादा मायने रखते हैं।","స్నేహితుడికి చెప్పినట్లు వివరించండి. వైద్య పదాల కంటే వివరాలు ముఖ్యం.","நண்பரிடம் சொல்வது போலச் சொல்லுங்கள். மருத்துவச் சொற்களை விட விவரங்களே முக்கியம்.","ಸ್ನೇಹಿತರಿಗೆ ಹೇಳುವಂತೆ ವಿವರಿಸಿ. ವೈದ್ಯಕೀಯ ಪದಗಳಿಗಿಂತ ವಿವರಗಳು ಮುಖ್ಯ."],
["What is the main problem?","मुख्य समस्या क्या है?","ప్రధాన సమస్య ఏమిటి?","முக்கியப் பிரச்சினை என்ன?","ಮುಖ್ಯ ಸಮಸ್ಯೆ ಏನು?"],
["For example: sore throat and fever since Monday, worse at night","उदाहरण: सोमवार से गले में खराश और बुखार, रात में ज़्यादा","ఉదాహరణ: సోమవారం నుండి గొంతు నొప్పి మరియు జ్వరం, రాత్రి ఎక్కువ","எ.கா: திங்கள் முதல் தொண்டை வலி மற்றும் காய்ச்சல், இரவில் அதிகம்","ಉದಾಹರಣೆ: ಸೋಮವಾರದಿಂದ ಗಂಟಲು ನೋವು ಮತ್ತು ಜ್ವರ, ರಾತ್ರಿ ಹೆಚ್ಚು"],
["How long has this been going on?","यह कब से हो रहा है?","ఇది ఎంత కాలంగా ఉంది?","இது எவ்வளவு காலமாக இருக்கிறது?","ಇದು ಎಷ್ಟು ಸಮಯದಿಂದ ಇದೆ?"],
["hours","घंटे","గంటలు","மணி நேரம்","ಗಂಟೆಗಳು"],
["days","दिन","రోజులు","நாட்கள்","ದಿನಗಳು"],
["weeks","हफ़्ते","వారాలు","வாரங்கள்","ವಾರಗಳು"],
["months","महीने","నెలలు","மாதங்கள்","ತಿಂಗಳುಗಳು"],
["Number","संख्या","సంఖ్య","எண்","ಸಂಖ್ಯೆ"],
["Unit of time","समय की इकाई","సమయ యూనిట్","காலப் பிரிவு","ಸಮಯದ ಘಟಕ"],
["How did it start?","यह कैसे शुरू हुआ?","ఇది ఎలా మొదలైంది?","இது எப்படித் தொடங்கியது?","ಇದು ಹೇಗೆ ಪ್ರಾರಂಭವಾಯಿತು?"],
["Sudden","अचानक","అకస్మాత్తుగా","திடீரென","ಹಠಾತ್ತಾಗಿ"],
["Gradual","धीरे-धीरे","క్రమంగా","படிப்படியாக","ಕ್ರಮೇಣ"],
["Comes and goes","आता-जाता रहता है","వచ్చి పోతూ ఉంటుంది","வந்து போகும்","ಬಂದು ಹೋಗುತ್ತದೆ"],
["How bad is it at its worst?","सबसे ज़्यादा होने पर यह कितना बुरा है?","అత్యధికంగా ఉన్నప్పుడు ఎంత తీవ్రంగా ఉంది?","மிக அதிகமாக இருக்கும்போது எவ்வளவு மோசம்?","ಅತ್ಯಂತ ಹೆಚ್ಚಾದಾಗ ಎಷ್ಟು ಕೆಟ್ಟದಾಗಿದೆ?"],
["Not rated yet. Move the slider.","अभी रेटिंग नहीं दी। स्लाइडर हिलाइए।","ఇంకా రేటింగ్ ఇవ్వలేదు. స్లైడర్‌ను జరపండి.","இன்னும் மதிப்பிடவில்லை. ஸ்லைடரை நகர்த்தவும்.","ಇನ್ನೂ ರೇಟ್ ಮಾಡಿಲ್ಲ. ಸ್ಲೈಡರ್ ಸರಿಸಿ."],
["{n} out of 10","10 में से {n}","10కి {n}","10-ல் {n}","10ರಲ್ಲಿ {n}"],
["0, none","0, कुछ नहीं","0, ఏమీ లేదు","0, எதுவுமில்லை","0, ಏನೂ ಇಲ್ಲ"],
["10, worst imaginable","10, कल्पना से भी बुरा","10, ఊహించలేనంత తీవ్రం","10, கற்பனை செய்ய முடியாத மோசம்","10, ಊಹಿಸಲಾಗದಷ್ಟು ತೀವ್ರ"],
["Any other symptoms?","कोई और लक्षण?","ఇతర లక్షణాలు ఏమైనా ఉన్నాయా?","வேறு அறிகுறிகள் ஏதேனும் உள்ளதா?","ಬೇರೆ ಯಾವುದಾದರೂ ಲಕ್ಷಣಗಳಿವೆಯೇ?"],
["General","सामान्य","సాధారణం","பொது","ಸಾಮಾನ್ಯ"],
["Head and senses","सिर और इंद्रियाँ","తల మరియు ఇంద్రియాలు","தலை மற்றும் புலன்கள்","ತಲೆ ಮತ್ತು ಇಂದ್ರಿಯಗಳು"],
["Chest and breathing","सीना और साँस","ఛాతీ మరియు శ్వాస","மார்பு மற்றும் மூச்சு","ಎದೆ ಮತ್ತು ಉಸಿರಾಟ"],
["Stomach and bowels","पेट और आँतें","కడుపు మరియు ప్రేగులు","வயிறு மற்றும் குடல்","ಹೊಟ್ಟೆ ಮತ್ತು ಕರುಳು"],
["Body and skin","शरीर और त्वचा","శరీరం మరియు చర్మం","உடல் மற்றும் தோல்","ದೇಹ ಮತ್ತು ಚರ್ಮ"],
["Mood and sleep","मन और नींद","మనస్థితి మరియు నిద్ర","மனநிலை மற்றும் தூக்கம்","ಮನಸ್ಥಿತಿ ಮತ್ತು ನಿದ್ರೆ"],
["Fever","बुखार","జ్వరం","காய்ச்சல்","ಜ್ವರ"],
["Chills","ठंड लगना","వణుకు (చలి)","குளிர்","ಚಳಿ"],
["Fatigue","थकान","అలసట","சோர்வு","ಆಯಾಸ"],
["Unintended weight loss","अनचाहा वज़न घटना","కావాలని కాకుండా బరువు తగ్గడం","தெரியாமல் எடை குறைவு","ಉದ್ದೇಶವಿಲ್ಲದೆ ತೂಕ ಇಳಿಕೆ"],
["Night sweats","रात में पसीना","రాత్రి చెమటలు","இரவு வியர்வை","ರಾತ್ರಿ ಬೆವರು"],
["Loss of appetite","भूख न लगना","ఆకలి లేకపోవడం","பசியின்மை","ಹಸಿವಿಲ್ಲದಿರುವುದು"],
["Headache","सिरदर्द","తలనొప్పి","தலைவலி","ತಲೆನೋವು"],
["Dizziness","चक्कर आना","తల తిరగడం","தலைச்சுற்றல்","ತಲೆ ಸುತ್ತುವುದು"],
["Blurred vision","धुंधला दिखना","మసకగా కనిపించడం","பார்வை மங்கல்","ಮಂಜು ದೃಷ್ಟಿ"],
["Sore throat","गले में खराश","గొంతు నొప్పి","தொண்டை வலி","ಗಂಟಲು ನೋವು"],
["Ear pain","कान दर्द","చెవి నొప్పి","காது வலி","ಕಿವಿ ನೋವು"],
["Runny or blocked nose","नाक बहना या बंद होना","ముక్కు కారడం లేదా మూసుకుపోవడం","மூக்கு ஒழுகுதல் அல்லது அடைப்பு","ಮೂಗು ಸೋರುವುದು ಅಥವಾ ಕಟ್ಟುವುದು"],
["Cough","खाँसी","దగ్గు","இருமல்","ಕೆಮ್ಮು"],
["Shortness of breath","साँस फूलना","ఊపిరి ఆడకపోవడం","மூச்சுத் திணறல்","ಉಸಿರಾಟದ ತೊಂದರೆ"],
["Chest pain","सीने में दर्द","ఛాతీ నొప్పి","மார்பு வலி","ಎದೆ ನೋವು"],
["Palpitations","दिल की तेज़ धड़कन","గుండె దడ","நெஞ்சு படபடப்பு","ಹೃದಯ ಬಡಿತ ಹೆಚ್ಚಳ"],
["Wheezing","साँस में सीटी जैसी आवाज़","ఊపిరిలో గురక శబ్దం","மூச்சில் விசில் சத்தம்","ಉಸಿರಾಟದಲ್ಲಿ ಸೀಟಿ ಶಬ್ದ"],
["Nausea","जी मिचलाना","వికారం","குமட்டல்","ವಾಕರಿಕೆ"],
["Vomiting","उल्टी","వాంతులు","வாந்தி","ವಾಂತಿ"],
["Abdominal pain","पेट दर्द","కడుపు నొప్పి","வயிற்று வலி","ಹೊಟ್ಟೆ ನೋವು"],
["Diarrhea","दस्त","విరేచనాలు","வயிற்றுப்போக்கு","ಅತಿಸಾರ"],
["Constipation","कब्ज़","మలబద్ధకం","மலச்சிக்கல்","ಮಲಬದ್ಧತೆ"],
["Blood in stool","मल में खून","మలంలో రక్తం","மலத்தில் இரத்தம்","ಮಲದಲ್ಲಿ ರಕ್ತ"],
["Heartburn","सीने में जलन","గుండెలో మంట","நெஞ்செரிச்சல்","ಎದೆ ಉರಿ"],
["Rash","चकत्ते","దద్దుర్లు","தடிப்பு","ದದ್ದು"],
["Joint pain","जोड़ों में दर्द","కీళ్ల నొప్పి","மூட்டு வலி","ಕೀಲು ನೋವು"],
["Muscle aches","मांसपेशियों में दर्द","కండరాల నొప్పులు","தசை வலி","ಸ್ನಾಯು ನೋವು"],
["Swelling in legs","पैरों में सूजन","కాళ్ల వాపు","கால் வீக்கம்","ಕಾಲು ಊತ"],
["Burning when urinating","पेशाब में जलन","మూత్ర విసర్జనలో మంట","சிறுநீர் கழிக்கும்போது எரிச்சல்","ಮೂತ್ರ ವಿಸರ್ಜನೆಯಲ್ಲಿ ಉರಿ"],
["Blood in urine","पेशाब में खून","మూత్రంలో రక్తం","சிறுநீரில் இரத்தம்","ಮೂತ್ರದಲ್ಲಿ ರಕ್ತ"],
["Low mood","उदासी","మనస్సు కుంగిపోవడం","மனச்சோர்வு","ಮನಸ್ಸು ಕುಗ್ಗುವುದು"],
["Anxiety","घबराहट/चिंता","ఆందోళన","பதற்றம்","ಆತಂಕ"],
["Trouble sleeping","नींद न आना","నిద్ర పట్టకపోవడం","தூக்கமின்மை","ನಿದ್ರೆ ಬಾರದಿರುವುದು"],
["What makes it worse?","किससे यह बढ़ता है?","దేనివల్ల ఇది ఎక్కువవుతుంది?","எதனால் இது அதிகமாகிறது?","ಯಾವುದರಿಂದ ಇದು ಹೆಚ್ಚಾಗುತ್ತದೆ?"],
["What makes it better?","किससे आराम मिलता है?","దేనివల్ల ఉపశమనం కలుగుతుంది?","எதனால் இது குறைகிறது?","ಯಾವುದರಿಂದ ಉಪಶಮನವಾಗುತ್ತದೆ?"],
["Describe the main problem in a few words.","मुख्य समस्या कुछ शब्दों में बताइए।","ప్రధాన సమస్యను కొన్ని పదాల్లో వివరించండి.","முக்கியப் பிரச்சினையை சில வார்த்தைகளில் விவரியுங்கள்.","ಮುಖ್ಯ ಸಮಸ್ಯೆಯನ್ನು ಕೆಲವು ಪದಗಳಲ್ಲಿ ವಿವರಿಸಿ."],
["Enter how long this has been going on, for example 3 days.","यह कब से हो रहा है, जैसे 3 दिन, यह भरें।","ఇది ఎంత కాలంగా ఉందో నమోదు చేయండి, ఉదాహరణకు 3 రోజులు.","இது எவ்வளவு காலமாக உள்ளது என்பதை உள்ளிடுங்கள், எ.கா. 3 நாட்கள்.","ಇದು ಎಷ್ಟು ಸಮಯದಿಂದ ಇದೆ ಎಂದು ನಮೂದಿಸಿ, ಉದಾಹರಣೆಗೆ 3 ದಿನಗಳು."],
["Past health and habits help your doctor read today's symptoms. Skip anything you don't know.","पिछला स्वास्थ्य और आदतें डॉक्टर को आज के लक्षण समझने में मदद करती हैं। जो न पता हो उसे छोड़ दें।","గత ఆరోగ్యం మరియు అలవాట్లు నేటి లక్షణాలను అర్థం చేసుకోవడంలో డాక్టర్‌కు సహాయపడతాయి. తెలియనివి వదిలేయండి.","கடந்தகால உடல்நலமும் பழக்கங்களும் இன்றைய அறிகுறிகளைப் புரிந்துகொள்ள மருத்துவருக்கு உதவும். தெரியாததைத் தவிர்க்கலாம்.","ಹಿಂದಿನ ಆರೋಗ್ಯ ಮತ್ತು ಅಭ್ಯಾಸಗಳು ಇಂದಿನ ಲಕ್ಷಣಗಳನ್ನು ಅರ್ಥಮಾಡಿಕೊಳ್ಳಲು ವೈದ್ಯರಿಗೆ ಸಹಾಯ ಮಾಡುತ್ತವೆ. ಗೊತ್ತಿಲ್ಲದ್ದನ್ನು ಬಿಟ್ಟುಬಿಡಿ."],
["Do you have any of these conditions?","क्या आपको इनमें से कोई बीमारी है?","మీకు వీటిలో ఏవైనా ఆరోగ్య సమస్యలు ఉన్నాయా?","இவற்றில் ஏதேனும் உடல்நிலை பாதிப்பு உங்களுக்கு உள்ளதா?","ನಿಮಗೆ ಇವುಗಳಲ್ಲಿ ಯಾವುದಾದರೂ ಸಮಸ್ಯೆ ಇದೆಯೇ?"],
["Diabetes","मधुमेह (डायबिटीज़)","మధుమేహం (డయాబెటిస్)","நீரிழிவு","ಮಧುಮೇಹ"],
["High blood pressure","उच्च रक्तचाप","అధిక రక్తపోటు","உயர் இரத்த அழுத்தம்","ಅಧಿಕ ರಕ್ತದೊತ್ತಡ"],
["Heart disease","हृदय रोग","గుండె జబ్బు","இதய நோய்","ಹೃದ್ರೋಗ"],
["Asthma or COPD","दमा या सीओपीडी","ఆస్తమా లేదా COPD","ஆஸ்துமா அல்லது சிஓபிடி","ಆಸ್ತಮಾ ಅಥವಾ ಸಿಒಪಿಡಿ"],
["Kidney disease","गुर्दे की बीमारी","కిడ్నీ జబ్బు","சிறுநீரக நோய்","ಮೂತ್ರಪಿಂಡ ಕಾಯಿಲೆ"],
["Liver disease","लिवर की बीमारी","కాలేయ జబ్బు","கல்லீரல் நோய்","ಯಕೃತ್ತಿನ ಕಾಯಿಲೆ"],
["Thyroid disorder","थायरॉइड की समस्या","థైరాయిడ్ సమస్య","தைராய்டு பிரச்சினை","ಥೈರಾಯ್ಡ್ ಸಮಸ್ಯೆ"],
["Epilepsy","मिर्गी","మూర్ఛ వ్యాధి","வலிப்பு நோய்","ಅಪಸ್ಮಾರ"],
["Cancer","कैंसर","క్యాన్సర్","புற்றுநோய்","ಕ್ಯಾನ್ಸರ್"],
["Weakened immunity","कमज़ोर रोग-प्रतिरोधक क्षमता","తగ్గిన రోగనిరోధక శక్తి","பலவீனமான நோய் எதிர்ப்பு சக்தி","ದುರ್ಬಲ ರೋಗನಿರೋಧಕ ಶಕ್ತಿ"],
["Depression or anxiety","अवसाद या चिंता","డిప్రెషన్ లేదా ఆందోళన","மனச்சோர்வு அல்லது பதற்றம்","ಖಿನ್ನತೆ ಅಥವಾ ಆತಂಕ"],
["Tuberculosis","टीबी (क्षय रोग)","క్షయ (టీబీ)","காசநோய்","ಕ್ಷಯ (ಟಿಬಿ)"],
["Any other condition?","कोई और बीमारी?","ఇంకేదైనా ఆరోగ్య సమస్య?","வேறு ஏதேனும் நிலை?","ಬೇರೆ ಯಾವುದಾದರೂ ಸಮಸ್ಯೆ?"],
["Past surgeries or hospital stays","पिछली सर्जरी या अस्पताल में भर्ती","గత శస్త్రచికిత్సలు లేదా ఆసుపత్రిలో చేరికలు","முந்தைய அறுவை சிகிச்சைகள் அல்லது மருத்துவமனை தங்கல்","ಹಿಂದಿನ ಶಸ್ತ್ರಚಿಕಿತ್ಸೆ ಅಥವಾ ಆಸ್ಪತ್ರೆ ದಾಖಲಾತಿ"],
["For example: appendix removed, 2019","उदाहरण: अपेंडिक्स निकाला गया, 2019","ఉదాహరణ: అపెండిక్స్ తొలగింపు, 2019","எ.கா: குடல்வால் நீக்கம், 2019","ಉದಾಹರಣೆ: ಅಪೆಂಡಿಕ್ಸ್ ತೆಗೆದಿದೆ, 2019"],
["Close family with any of these?","क्या नज़दीकी परिवार में इनमें से किसी को है?","మీ దగ్గరి కుటుంబ సభ్యులకు వీటిలో ఏవైనా ఉన్నాయా?","நெருங்கிய குடும்பத்தில் இவற்றில் ஏதேனும் உள்ளதா?","ನಿಮ್ಮ ಹತ್ತಿರದ ಕುಟುಂಬದಲ್ಲಿ ಇವುಗಳಲ್ಲಿ ಯಾವುದಾದರೂ ಇದೆಯೇ?"],
["Stroke","स्ट्रोक (लकवा)","స్ట్రోక్ (పక్షవాతం)","பக்கவாதம்","ಪಾರ್ಶ್ವವಾಯು"],
["Asthma","दमा","ఆస్తమా","ஆஸ்துமா","ಆಸ್ತಮಾ"],
["Smoking","धूम्रपान","ధూమపానం","புகைப்பழக்கம்","ಧೂಮಪಾನ"],
["Never","कभी नहीं","ఎప్పుడూ లేదు","ஒருபோதும் இல்லை","ಎಂದಿಗೂ ಇಲ್ಲ"],
["Former smoker","पहले धूम्रपान करते थे","గతంలో ధూమపానం చేసేవారు","முன்பு புகைத்தவர்","ಹಿಂದೆ ಧೂಮಪಾನ ಮಾಡುತ್ತಿದ್ದರು"],
["Current smoker","अभी धूम्रपान करते हैं","ప్రస్తుతం ధూమపానం చేస్తున్నారు","தற்போது புகைக்கிறார்","ಪ್ರಸ್ತುತ ಧೂಮಪಾನ ಮಾಡುತ್ತಾರೆ"],
["Alcohol","शराब","మద్యం","மது","ಮದ್ಯ"],
["None","बिल्कुल नहीं","లేదు","இல்லை","ಇಲ್ಲ"],
["Occasional","कभी-कभार","అప్పుడప్పుడు","எப்போதாவது","ಆಗಾಗ"],
["Regular","नियमित","క్రమం తప్పకుండా","தொடர்ந்து","ನಿಯಮಿತವಾಗಿ"],
["Sleep per night","रात में नींद","రాత్రి నిద్ర","இரவுத் தூக்கம்","ರಾತ್ರಿ ನಿದ್ರೆ"],
["Under 5 hours","5 घंटे से कम","5 గంటల కంటే తక్కువ","5 மணி நேரத்துக்குக் குறைவு","5 ಗಂಟೆಗಿಂತ ಕಡಿಮೆ"],
["5 to 7 hours","5 से 7 घंटे","5 నుండి 7 గంటలు","5 முதல் 7 மணி நேரம்","5 ರಿಂದ 7 ಗಂಟೆ"],
["7 to 9 hours","7 से 9 घंटे","7 నుండి 9 గంటలు","7 முதல் 9 மணி நேரம்","7 ರಿಂದ 9 ಗಂಟೆ"],
["Over 9 hours","9 घंटे से ज़्यादा","9 గంటల కంటే ఎక్కువ","9 மணி நேரத்துக்கு மேல்","9 ಗಂಟೆಗಿಂತ ಹೆಚ್ಚು"],
["Physical activity","शारीरिक गतिविधि","శారీరక వ్యాయామం","உடல் செயல்பாடு","ದೈಹಿಕ ಚಟುವಟಿಕೆ"],
["Rarely","बहुत कम","అరుదుగా","அரிதாக","ಅಪರೂಪಕ್ಕೆ"],
["1 to 2 times a week","हफ़्ते में 1 से 2 बार","వారానికి 1 నుండి 2 సార్లు","வாரத்திற்கு 1 முதல் 2 முறை","ವಾರಕ್ಕೆ 1 ರಿಂದ 2 ಬಾರಿ"],
["3 or more times a week","हफ़्ते में 3 या ज़्यादा बार","వారానికి 3 లేదా అంతకంటే ఎక్కువ సార్లు","வாரத்திற்கு 3 அல்லது அதற்கு மேற்பட்ட முறை","ವಾರಕ್ಕೆ 3 ಅಥವಾ ಹೆಚ್ಚು ಬಾರಿ"],
["Include vitamins, herbal remedies and over-the-counter medicines.","विटामिन, हर्बल उपचार और बिना पर्ची वाली दवाएँ भी शामिल करें।","విటమిన్లు, మూలికా చికిత్సలు మరియు కౌంటర్‌లో దొరికే మందులను కూడా చేర్చండి.","வைட்டமின்கள், மூலிகை மருந்துகள் மற்றும் மருந்துச்சீட்டு இல்லாமல் வாங்கும் மருந்துகளையும் சேர்க்கவும்.","ವಿಟಮಿನ್‌ಗಳು, ಗಿಡಮೂಲಿಕೆ ಔಷಧಿಗಳು ಮತ್ತು ಚೀಟಿ ಇಲ್ಲದೆ ಪಡೆಯುವ ಔಷಧಿಗಳನ್ನೂ ಸೇರಿಸಿ."],
["Medicines you take regularly","जो दवाएँ आप नियमित लेते हैं","మీరు క్రమం తప్పకుండా వాడే మందులు","நீங்கள் தொடர்ந்து எடுக்கும் மருந்துகள்","ನೀವು ನಿಯಮಿತವಾಗಿ ತೆಗೆದುಕೊಳ್ಳುವ ಔಷಧಿಗಳು"],
["Type a name and dose, then press Enter or Add.","नाम और मात्रा लिखें, फिर Enter या जोड़ें दबाएँ।","పేరు మరియు మోతాదు టైప్ చేసి, Enter లేదా జోడించు నొక్కండి.","பெயர் மற்றும் அளவை தட்டச்சு செய்து, Enter அல்லது சேர் அழுத்தவும்.","ಹೆಸರು ಮತ್ತು ಪ್ರಮಾಣ ಟೈಪ್ ಮಾಡಿ, Enter ಅಥವಾ ಸೇರಿಸಿ ಒತ್ತಿ."],
["For example: Metformin 500 mg, twice a day","उदाहरण: मेटफॉर्मिन 500 mg, दिन में दो बार","ఉదాహరణ: మెట్‌ఫార్మిన్ 500 mg, రోజుకు రెండుసార్లు","எ.கா: மெட்ஃபார்மின் 500 mg, ஒரு நாளைக்கு இரண்டு முறை","ಉದಾಹರಣೆ: ಮೆಟ್‌ಫಾರ್ಮಿನ್ 500 mg, ದಿನಕ್ಕೆ ಎರಡು ಬಾರಿ"],
["I take no regular medicines","मैं कोई नियमित दवा नहीं लेता/लेती","నేను క్రమం తప్పకుండా ఏ మందులూ వాడను","நான் தொடர்ந்து எந்த மருந்தும் எடுப்பதில்லை","ನಾನು ನಿಯಮಿತವಾಗಿ ಯಾವ ಔಷಧಿಯನ್ನೂ ತೆಗೆದುಕೊಳ್ಳುವುದಿಲ್ಲ"],
["Add","जोड़ें","జోడించు","சேர்","ಸೇರಿಸಿ"],
["Remove {x}","{x} हटाएँ","{x} తొలగించు","{x} நீக்கு","{x} ತೆಗೆಯಿರಿ"],
["Allergies","एलर्जी","అలెర్జీలు","ஒவ்வாமைகள்","ಅಲರ್ಜಿಗಳು"],
["Medicines, foods, latex, or anything that caused a reaction.","दवाएँ, खाने की चीज़ें, लेटेक्स, या कुछ भी जिससे प्रतिक्रिया हुई हो।","మందులు, ఆహారాలు, లేటెక్స్, లేదా ప్రతిచర్య కలిగించిన ఏదైనా.","மருந்துகள், உணவுகள், லேடெக்ஸ் அல்லது எதிர்வினை ஏற்படுத்திய எதுவும்.","ಔಷಧಿಗಳು, ಆಹಾರ, ಲ್ಯಾಟೆಕ್ಸ್, ಅಥವಾ ಪ್ರತಿಕ್ರಿಯೆ ಉಂಟುಮಾಡಿದ ಯಾವುದೇ ವಸ್ತು."],
["For example: Penicillin, rash","उदाहरण: पेनिसिलिन, चकत्ते","ఉదాహరణ: పెన్సిలిన్, దద్దుర్లు","எ.கா: பெனிசிலின், தடிப்பு","ಉದಾಹರಣೆ: ಪೆನ್ಸಿಲಿನ್, ದದ್ದು"],
["I have no known allergies","मुझे कोई ज्ञात एलर्जी नहीं है","నాకు తెలిసిన అలెర్జీలు ఏవీ లేవు","எனக்குத் தெரிந்த ஒவ்வாமைகள் எதுவும் இல்லை","ನನಗೆ ತಿಳಿದಿರುವ ಅಲರ್ಜಿಗಳಿಲ್ಲ"],
["Saved","सहेज लिया गया","సేవ్ అయింది","சேமிக்கப்பட்டது","ಉಳಿಸಲಾಗಿದೆ"],
["This visit is saved in this browser. Copy the note to send it to your doctor, or print it.","यह विज़िट इस ब्राउज़र में सहेजी गई है। नोट कॉपी करके डॉक्टर को भेजें, या प्रिंट करें।","ఈ సందర్శన ఈ బ్రౌజర్‌లో సేవ్ అయింది. నోట్‌ను కాపీ చేసి డాక్టర్‌కు పంపండి, లేదా ప్రింట్ చేయండి.","இந்த வருகை இந்த உலாவியில் சேமிக்கப்பட்டது. குறிப்பை நகலெடுத்து மருத்துவருக்கு அனுப்பவும், அல்லது அச்சிடவும்.","ಈ ಭೇಟಿಯನ್ನು ಈ ಬ್ರೌಸರ್‌ನಲ್ಲಿ ಉಳಿಸಲಾಗಿದೆ. ಟಿಪ್ಪಣಿಯನ್ನು ನಕಲಿಸಿ ವೈದ್ಯರಿಗೆ ಕಳುಹಿಸಿ, ಅಥವಾ ಮುದ್ರಿಸಿ."],
["Read the note next to your answers. Fix anything that's wrong, then save it to this device.","अपने उत्तरों के साथ नोट पढ़ें। जो गलत हो उसे ठीक करें, फिर इस डिवाइस में सहेजें।","మీ సమాధానాలతో పాటు నోట్‌ను చదవండి. తప్పులుంటే సరిచేసి, ఈ పరికరంలో సేవ్ చేయండి.","உங்கள் பதில்களுடன் குறிப்பைப் படியுங்கள். தவறு இருந்தால் திருத்தி, இந்தச் சாதனத்தில் சேமிக்கவும்.","ನಿಮ್ಮ ಉತ್ತರಗಳೊಂದಿಗೆ ಟಿಪ್ಪಣಿಯನ್ನು ಓದಿ. ತಪ್ಪಿದ್ದರೆ ಸರಿಪಡಿಸಿ, ನಂತರ ಈ ಸಾಧನದಲ್ಲಿ ಉಳಿಸಿ."],
["Change an answer","कोई उत्तर बदलें","సమాధానాన్ని మార్చండి","பதிலை மாற்றவும்","ಉತ್ತರ ಬದಲಿಸಿ"],
["Not assessed yet","अभी आकलन नहीं हुआ","ఇంకా అంచనా వేయలేదు","இன்னும் மதிப்பிடப்படவில்லை","ಇನ್ನೂ ಮೌಲ್ಯಮಾಪನ ಮಾಡಿಲ್ಲ"],
["Pending","लंबित","పెండింగ్","நிலுவையில்","ಬಾಕಿ"],
["Complete the safety check and describe your main problem to see a result.","नतीजा देखने के लिए सुरक्षा जाँच पूरी करें और अपनी मुख्य समस्या बताएँ।","ఫలితం చూడటానికి భద్రతా తనిఖీని పూర్తి చేసి, మీ ప్రధాన సమస్యను వివరించండి.","முடிவைப் பார்க்க பாதுகாப்புச் சோதனையை முடித்து, உங்கள் முக்கியப் பிரச்சினையை விவரிக்கவும்.","ಫಲಿತಾಂಶ ನೋಡಲು ಸುರಕ್ಷತಾ ಪರಿಶೀಲನೆ ಪೂರ್ಣಗೊಳಿಸಿ ಮತ್ತು ನಿಮ್ಮ ಮುಖ್ಯ ಸಮಸ್ಯೆಯನ್ನು ವಿವರಿಸಿ."],
["Routine appointment","सामान्य अपॉइंटमेंट","సాధారణ అపాయింట్‌మెంట్","வழக்கமான சந்திப்பு","ಸಾಮಾನ್ಯ ಅಪಾಯಿಂಟ್‌ಮೆಂಟ್"],
["Routine","सामान्य","సాధారణం","வழக்கமான","ಸಾಮಾನ್ಯ"],
["A routine appointment is fine","सामान्य अपॉइंटमेंट काफ़ी है","సాధారణ అపాయింట్‌మెంట్ సరిపోతుంది","வழக்கமான சந்திப்பு போதும்","ಸಾಮಾನ್ಯ ಅಪಾಯಿಂಟ್‌ಮೆಂಟ್ ಸಾಕು"],
["Book a regular visit. Get emergency help if you develop chest pain, trouble breathing, or anything from the safety check.","सामान्य विज़िट बुक करें। अगर सीने में दर्द, साँस में तकलीफ़ या सुरक्षा जाँच की कोई बात हो जाए तो आपातकालीन मदद लें।","సాధారణ సందర్శన బుక్ చేయండి. ఛాతీ నొప్పి, శ్వాస ఇబ్బంది లేదా భద్రతా తనిఖీలోని ఏదైనా లక్షణం వస్తే అత్యవసర సహాయం పొందండి.","வழக்கமான வருகையை முன்பதிவு செய்யுங்கள். மார்பு வலி, மூச்சுத் திணறல் அல்லது பாதுகாப்புச் சோதனையில் உள்ள ஏதேனும் வந்தால் அவசர உதவி பெறுங்கள்.","ಸಾಮಾನ್ಯ ಭೇಟಿ ಬುಕ್ ಮಾಡಿ. ಎದೆ ನೋವು, ಉಸಿರಾಟದ ತೊಂದರೆ ಅಥವಾ ಸುರಕ್ಷತಾ ಪರಿಶೀಲನೆಯ ಯಾವುದೇ ಲಕ್ಷಣ ಕಾಣಿಸಿದರೆ ತುರ್ತು ಸಹಾಯ ಪಡೆಯಿರಿ."],
["See a doctor within 24 hours","24 घंटे के भीतर डॉक्टर को दिखाएँ","24 గంటల్లో డాక్టర్‌ను కలవండి","24 மணி நேரத்துக்குள் மருத்துவரைப் பாருங்கள்","24 ಗಂಟೆಗಳೊಳಗೆ ವೈದ್ಯರನ್ನು ಭೇಟಿಯಾಗಿ"],
["Urgent","जल्दी","త్వరితం","விரைவு","ತ್ವರಿತ"],
["Book a same-day or next-day visit, or go to an urgent care clinic. If things get worse, treat it as an emergency.","उसी दिन या अगले दिन की विज़िट बुक करें, या अर्जेंट केयर क्लिनिक जाएँ। हालत बिगड़े तो इसे आपातकाल मानें।","అదే రోజు లేదా మరుసటి రోజు సందర్శన బుక్ చేయండి, లేదా అర్జెంట్ కేర్ క్లినిక్‌కు వెళ్లండి. పరిస్థితి మరింత దిగజారితే దీన్ని అత్యవసరంగా భావించండి.","அதே நாள் அல்லது மறுநாள் வருகையை முன்பதிவு செய்யுங்கள், அல்லது அவசர சிகிச்சை மையத்துக்குச் செல்லுங்கள். நிலைமை மோசமானால் அதை அவசரமாகக் கருதுங்கள்.","ಅದೇ ದಿನ ಅಥವಾ ಮರುದಿನದ ಭೇಟಿ ಬುಕ್ ಮಾಡಿ, ಅಥವಾ ತುರ್ತು ಆರೈಕೆ ಕ್ಲಿನಿಕ್‌ಗೆ ಹೋಗಿ. ಪರಿಸ್ಥಿತಿ ಹದಗೆಟ್ಟರೆ ಇದನ್ನು ತುರ್ತು ಎಂದು ಪರಿಗಣಿಸಿ."],
["Emergency care now","अभी आपातकालीन देखभाल","ఇప్పుడే అత్యవసర వైద్యం","இப்போதே அவசர சிகிச்சை","ಈಗಲೇ ತುರ್ತು ಚಿಕಿತ್ಸೆ"],
["Emergency","आपातकाल","అత్యవసరం","அவசரம்","ತುರ್ತು"],
["Get emergency care now","अभी आपातकालीन देखभाल लें","ఇప్పుడే అత్యవసర వైద్యం పొందండి","இப்போதே அவசர சிகிச்சை பெறுங்கள்","ಈಗಲೇ ತುರ್ತು ಚಿಕಿತ್ಸೆ ಪಡೆಯಿರಿ"],
["Call 112 or go to the nearest emergency department. Do not wait for an appointment and do not drive yourself.","112 पर कॉल करें या नज़दीकी आपातकालीन विभाग जाएँ। अपॉइंटमेंट का इंतज़ार न करें और खुद गाड़ी न चलाएँ।","112కు కాల్ చేయండి లేదా సమీప అత్యవసర విభాగానికి వెళ్లండి. అపాయింట్‌మెంట్ కోసం వేచి ఉండకండి, మీరే వాహనం నడపకండి.","112-ஐ அழைக்கவும் அல்லது அருகிலுள்ள அவசர சிகிச்சைப் பிரிவுக்குச் செல்லுங்கள். சந்திப்புக்காகக் காத்திருக்க வேண்டாம், நீங்களே வாகனம் ஓட்ட வேண்டாம்.","112ಕ್ಕೆ ಕರೆ ಮಾಡಿ ಅಥವಾ ಹತ್ತಿರದ ತುರ್ತು ವಿಭಾಗಕ್ಕೆ ಹೋಗಿ. ಅಪಾಯಿಂಟ್‌ಮೆಂಟ್‌ಗಾಗಿ ಕಾಯಬೇಡಿ, ನೀವೇ ವಾಹನ ಚಲಾಯಿಸಬೇಡಿ."],
["You rated the problem {n} out of 10 at its worst.","आपने समस्या को सबसे ज़्यादा होने पर 10 में से {n} आँका।","మీరు సమస్యను అత్యధికంగా 10కి {n}గా రేట్ చేశారు.","நீங்கள் பிரச்சினையை மிக அதிகமாக இருக்கும்போது 10-ல் {n} என மதிப்பிட்டீர்கள்.","ನೀವು ಸಮಸ್ಯೆಯನ್ನು ಅತ್ಯಂತ ಹೆಚ್ಚಾದಾಗ 10ರಲ್ಲಿ {n} ಎಂದು ರೇಟ್ ಮಾಡಿದ್ದೀರಿ."],
["Fever lasting 3 days or more.","3 दिन या उससे ज़्यादा समय से बुखार।","3 రోజులు లేదా అంతకంటే ఎక్కువ కాలంగా జ్వరం.","3 நாட்கள் அல்லது அதற்கு மேல் நீடிக்கும் காய்ச்சல்.","3 ದಿನ ಅಥವಾ ಹೆಚ್ಚು ಕಾಲದ ಜ್ವರ."],
["Fever in a young child or an adult aged 65 or over.","छोटे बच्चे या 65 वर्ष या उससे अधिक उम्र के व्यक्ति में बुखार।","చిన్న పిల్లలో లేదా 65 ఏళ్లు పైబడిన వారిలో జ్వరం.","சிறு குழந்தை அல்லது 65 வயது மற்றும் அதற்கு மேற்பட்டவருக்குக் காய்ச்சல்.","ಚಿಕ್ಕ ಮಗು ಅಥವಾ 65 ವರ್ಷ ಮೇಲ್ಪಟ್ಟವರಲ್ಲಿ ಜ್ವರ."],
["Fever with a condition that weakens the immune system.","रोग-प्रतिरोधक क्षमता कमज़ोर करने वाली स्थिति के साथ बुखार।","రోగనిరోధక శక్తిని బలహీనపరిచే పరిస్థితితో పాటు జ్వరం.","நோய் எதிர்ப்பு சக்தியைக் குறைக்கும் நிலையுடன் காய்ச்சல்.","ರೋಗನಿರೋಧಕ ಶಕ್ತಿ ಕುಗ್ಗಿಸುವ ಸ್ಥಿತಿಯೊಂದಿಗೆ ಜ್ವರ."],
["Chest pain, even if it is not happening now.","सीने में दर्द, भले ही अभी न हो रहा हो।","ఛాతీ నొప్పి, ఇప్పుడు లేకపోయినా.","மார்பு வலி, இப்போது இல்லாவிட்டாலும்.","ಎದೆ ನೋವು, ಈಗ ಇಲ್ಲದಿದ್ದರೂ."],
["Shortness of breath.","साँस फूलना।","ఊపిరి ఆడకపోవడం.","மூச்சுத் திணறல்.","ಉಸಿರಾಟದ ತೊಂದರೆ."],
["Blood in stool or urine.","मल या पेशाब में खून।","మలం లేదా మూత్రంలో రక్తం.","மலம் அல்லது சிறுநீரில் இரத்தம்.","ಮಲ ಅಥವಾ ಮೂತ್ರದಲ್ಲಿ ರಕ್ತ."],
["Unintended weight loss needs a prompt check.","अनचाहे वज़न घटने की जल्दी जाँच ज़रूरी है।","కావాలని కాకుండా బరువు తగ్గడానికి త్వరగా పరీక్ష అవసరం.","தெரியாமல் எடை குறைவதற்கு விரைவான பரிசோதனை தேவை.","ಉದ್ದೇಶವಿಲ್ಲದೆ ತೂಕ ಇಳಿಕೆಗೆ ಶೀಘ್ರ ಪರೀಕ್ಷೆ ಅಗತ್ಯ."],
["Vomiting or diarrhea for 2 days or more, with a higher risk of dehydration.","2 दिन या उससे ज़्यादा उल्टी या दस्त, जिसमें निर्जलीकरण का जोखिम ज़्यादा है।","2 రోజులు లేదా అంతకంటే ఎక్కువ వాంతులు లేదా విరేచనాలు, డీహైడ్రేషన్ ప్రమాదం ఎక్కువ.","2 நாட்கள் அல்லது அதற்கு மேல் வாந்தி அல்லது வயிற்றுப்போக்கு; நீர்ச்சத்துக் குறைபாட்டு ஆபத்து அதிகம்.","2 ದಿನ ಅಥವಾ ಹೆಚ್ಚು ಕಾಲ ವಾಂತಿ ಅಥವಾ ಅತಿಸಾರ, ನಿರ್ಜಲೀಕರಣದ ಅಪಾಯ ಹೆಚ್ಚು."],
["Abdominal pain, or headache with blurred vision, during possible pregnancy.","संभावित गर्भावस्था में पेट दर्द, या धुंधले दिखने के साथ सिरदर्द।","గర్భం ఉండే అవకాశంలో కడుపు నొప్పి, లేదా మసక చూపుతో తలనొప్పి.","கர்ப்பம் இருக்கக்கூடிய நிலையில் வயிற்று வலி, அல்லது பார்வை மங்கலுடன் தலைவலி.","ಗರ್ಭಧಾರಣೆಯ ಸಾಧ್ಯತೆಯಲ್ಲಿ ಹೊಟ್ಟೆ ನೋವು, ಅಥವಾ ಮಂಜು ದೃಷ್ಟಿಯೊಂದಿಗೆ ತಲೆನೋವು."],
["Symptoms lasting more than 2 weeks should be checked, even if mild.","2 हफ़्ते से ज़्यादा चलने वाले लक्षणों की जाँच करानी चाहिए, चाहे हल्के हों।","2 వారాల కంటే ఎక్కువ ఉన్న లక్షణాలను తేలికగా ఉన్నా పరీక్షించుకోవాలి.","2 வாரங்களுக்கு மேல் நீடிக்கும் அறிகுறிகளை லேசாக இருந்தாலும் பரிசோதிக்க வேண்டும்.","2 ವಾರಕ್ಕಿಂತ ಹೆಚ್ಚು ಕಾಲದ ಲಕ್ಷಣಗಳನ್ನು ಸೌಮ್ಯವಾಗಿದ್ದರೂ ಪರೀಕ್ಷಿಸಿಕೊಳ್ಳಬೇಕು."],
["No emergency or urgent signs in your answers.","आपके उत्तरों में आपातकालीन या जल्दी वाले कोई संकेत नहीं हैं।","మీ సమాధానాల్లో అత్యవసర లేదా త్వరిత సంకేతాలు ఏవీ లేవు.","உங்கள் பதில்களில் அவசர அல்லது விரைவு அறிகுறிகள் எதுவும் இல்லை.","ನಿಮ್ಮ ಉತ್ತರಗಳಲ್ಲಿ ತುರ್ತು ಅಥವಾ ತ್ವರಿತ ಲಕ್ಷಣಗಳಿಲ್ಲ."],
["Pre-visit intake note","विज़िट-पूर्व जानकारी नोट","సందర్శనకు ముందు వివరాల నోట్","வருகைக்கு முந்தைய தகவல் குறிப்பு","ಭೇಟಿಗೆ ಮೊದಲಿನ ಮಾಹಿತಿ ಟಿಪ್ಪಣಿ"],
["Prepared with CliniScribe on {d}","CliniScribe से {d} को तैयार किया गया","CliniScribe ద్వారా {d} న తయారు చేయబడింది","CliniScribe மூலம் {d} அன்று தயாரிக்கப்பட்டது","CliniScribe ಮೂಲಕ {d} ರಂದು ತಯಾರಿಸಲಾಗಿದೆ"],
["Patient","मरीज़","రోగి","நோயாளி","ರೋಗಿ"],
["Reason for visit","विज़िट का कारण","సందర్శన కారణం","வருகையின் காரணம்","ಭೇಟಿಯ ಕಾರಣ"],
["Other symptoms","अन्य लक्षण","ఇతర లక్షణాలు","பிற அறிகுறிகள்","ಇತರ ಲಕ್ಷಣಗಳು"],
["Emergency check","आपातकालीन जाँच","అత్యవసర తనిఖీ","அவசரச் சோதனை","ತುರ್ತು ಪರಿಶೀಲನೆ"],
["Medical history","चिकित्सा इतिहास","వైద్య చరిత్ర","மருத்துவ வரலாறு","ವೈದ್ಯಕೀಯ ಇತಿಹಾಸ"],
["Medicines","दवाएँ","మందులు","மருந்துகள்","ಔಷಧಿಗಳು"],
["Lifestyle","जीवनशैली","జీవనశైలి","வாழ்க்கை முறை","ಜೀವನಶೈಲಿ"],
["Screening result","स्क्रीनिंग परिणाम","స్క్రీనింగ్ ఫలితం","பரிசோதனை முடிவு","ಸ್ಕ್ರೀನಿಂಗ್ ಫಲಿತಾಂಶ"],
["Name","नाम","పేరు","பெயர்","ಹೆಸರು"],
["Age","उम्र","వయస్సు","வயது","ವಯಸ್ಸು"],
["Pregnancy","गर्भावस्था","గర్భం","கர்ப்பம்","ಗರ್ಭಧಾರಣೆ"],
["Duration","अवधि","వ్యవధి","கால அளவு","ಅವಧಿ"],
["Onset","शुरुआत","ప్రారంభం","தொடக்கம்","ಆರಂಭ"],
["Severity","तीव्रता","తీవ్రత","தீவிரம்","ತೀವ್ರತೆ"],
["Worse with","इससे बढ़ता है","వీటితో ఎక్కువ","இதனால் அதிகம்","ಇದರಿಂದ ಹೆಚ್ಚು"],
["Better with","इससे आराम","వీటితో ఉపశమనం","இதனால் குறைவு","ಇದರಿಂದ ಉಪಶಮನ"],
["Conditions","बीमारियाँ","ఆరోగ్య సమస్యలు","நிலைகள்","ಸಮಸ್ಯೆಗಳು"],
["Surgeries","सर्जरी","శస్త్రచికిత్సలు","அறுவை சிகிச்சைகள்","ಶಸ್ತ್ರಚಿಕಿತ್ಸೆಗಳು"],
["Family","परिवार","కుటుంబం","குடும்பம்","ಕುಟುಂಬ"],
["Sleep","नींद","నిద్ర","தூக்கம்","ನಿದ್ರೆ"],
["Activity","गतिविधि","కార్యకలాపం","செயல்பாடு","ಚಟುವಟಿಕೆ"],
["{n} years","{n} वर्ष","{n} సంవత్సరాలు","{n} ஆண்டுகள்","{n} ವರ್ಷ"],
["Reported: {x}.","बताया गया: {x}।","తెలిపినది: {x}.","தெரிவிக்கப்பட்டது: {x}.","ತಿಳಿಸಿದ್ದು: {x}."],
["No emergency symptoms reported.","कोई आपातकालीन लक्षण नहीं बताया गया।","అత్యవసర లక్షణాలు ఏవీ తెలుపలేదు.","அவசர அறிகுறிகள் எதுவும் தெரிவிக்கப்படவில்லை.","ಯಾವುದೇ ತುರ್ತು ಲಕ್ಷಣ ತಿಳಿಸಿಲ್ಲ."],
["No regular medicines.","कोई नियमित दवा नहीं।","క్రమం తప్పకుండా వాడే మందులు లేవు.","தொடர்ந்து எடுக்கும் மருந்துகள் இல்லை.","ನಿಯಮಿತ ಔಷಧಿಗಳಿಲ್ಲ."],
["No known allergies.","कोई ज्ञात एलर्जी नहीं।","తెలిసిన అలెర్జీలు లేవు.","தெரிந்த ஒவ்வாமைகள் இல்லை.","ತಿಳಿದಿರುವ ಅಲರ್ಜಿಗಳಿಲ್ಲ."],
["Not provided yet","अभी नहीं दिया गया","ఇంకా ఇవ్వలేదు","இன்னும் வழங்கப்படவில்லை","ಇನ್ನೂ ನೀಡಿಲ್ಲ"],
["Not provided","नहीं दिया गया","ఇవ్వలేదు","வழங்கப்படவில்லை","ನೀಡಿಲ್ಲ"],
["In the patient's words: \"{q}\"","मरीज़ के शब्दों में: \"{q}\"","రోగి మాటల్లో: \"{q}\"","நோயாளியின் வார்த்தைகளில்: \"{q}\"","ರೋಗಿಯ ಮಾತುಗಳಲ್ಲಿ: \"{q}\""],
["Rules-based screening from the patient's own answers. It is not a diagnosis and needs review by a clinician.","मरीज़ के अपने उत्तरों पर आधारित नियम-आधारित स्क्रीनिंग। यह निदान नहीं है और इसकी समीक्षा किसी चिकित्सक को करनी चाहिए।","రోగి స్వంత సమాధానాల ఆధారంగా నియమ-ఆధారిత స్క్రీనింగ్. ఇది రోగనిర్ధారణ కాదు; వైద్యుడు సమీక్షించాలి.","நோயாளியின் சொந்தப் பதில்களின் அடிப்படையிலான விதி சார்ந்த பரிசோதனை. இது நோய் கண்டறிதல் அல்ல; மருத்துவர் மதிப்பாய்வு செய்ய வேண்டும்.","ರೋಗಿಯ ಸ್ವಂತ ಉತ್ತರಗಳ ಆಧಾರದ ನಿಯಮ-ಆಧಾರಿತ ಸ್ಕ್ರೀನಿಂಗ್. ಇದು ರೋಗನಿರ್ಣಯವಲ್ಲ; ವೈದ್ಯರು ಪರಿಶೀಲಿಸಬೇಕು."],
["Note copied. Paste it into a message or email.","नोट कॉपी हो गया। इसे मैसेज या ईमेल में पेस्ट करें।","నోట్ కాపీ అయింది. దాన్ని సందేశం లేదా ఇమెయిల్‌లో పేస్ట్ చేయండి.","குறிப்பு நகலெடுக்கப்பட்டது. அதை செய்தி அல்லது மின்னஞ்சலில் ஒட்டவும்.","ಟಿಪ್ಪಣಿ ನಕಲಾಗಿದೆ. ಅದನ್ನು ಸಂದೇಶ ಅಥವಾ ಇಮೇಲ್‌ನಲ್ಲಿ ಪೇಸ್ಟ್ ಮಾಡಿ."],
["Your browser blocked copying. Select all the text below and copy it.","आपके ब्राउज़र ने कॉपी करने से रोका। नीचे का पूरा टेक्स्ट चुनकर कॉपी करें।","మీ బ్రౌజర్ కాపీ చేయడాన్ని నిరోధించింది. కింది టెక్స్ట్ మొత్తాన్ని ఎంచుకుని కాపీ చేయండి.","உங்கள் உலாவி நகலெடுப்பதைத் தடுத்தது. கீழே உள்ள உரை முழுவதையும் தேர்ந்தெடுத்து நகலெடுக்கவும்.","ನಿಮ್ಮ ಬ್ರೌಸರ್ ನಕಲು ಮಾಡುವುದನ್ನು ತಡೆದಿದೆ. ಕೆಳಗಿನ ಪಠ್ಯವನ್ನೆಲ್ಲ ಆಯ್ಕೆ ಮಾಡಿ ನಕಲಿಸಿ."],
["Note text","नोट का टेक्स्ट","నోట్ టెక్స్ట్","குறிப்பு உரை","ಟಿಪ್ಪಣಿ ಪಠ್ಯ"],
["Opening the print dialog. If nothing appears, press Ctrl+P (Cmd+P on Mac).","प्रिंट विंडो खुल रही है। कुछ न दिखे तो Ctrl+P (Mac पर Cmd+P) दबाएँ।","ప్రింట్ డైలాగ్ తెరుచుకుంటోంది. ఏమీ కనిపించకపోతే Ctrl+P (Macలో Cmd+P) నొక్కండి.","அச்சு உரையாடல் திறக்கிறது. எதுவும் தோன்றாவிட்டால் Ctrl+P (Mac-ல் Cmd+P) அழுத்தவும்.","ಮುದ್ರಣ ಸಂವಾದ ತೆರೆಯುತ್ತಿದೆ. ಏನೂ ಕಾಣಿಸದಿದ್ದರೆ Ctrl+P (Mac ನಲ್ಲಿ Cmd+P) ಒತ್ತಿ."],
["This browser blocked saving. Copy the note so you don't lose it.","इस ब्राउज़र ने सहेजना रोक दिया। नोट कॉपी कर लें ताकि वह खो न जाए।","ఈ బ్రౌజర్ సేవ్ చేయడాన్ని నిరోధించింది. నోట్ పోకుండా కాపీ చేసుకోండి.","இந்த உலாவி சேமிப்பதைத் தடுத்தது. குறிப்பு இழக்கப்படாமல் இருக்க நகலெடுத்துக்கொள்ளுங்கள்.","ಈ ಬ್ರೌಸರ್ ಉಳಿಸುವುದನ್ನು ತಡೆದಿದೆ. ಟಿಪ್ಪಣಿ ಕಳೆದುಹೋಗದಂತೆ ನಕಲಿಸಿಕೊಳ್ಳಿ."],
["Visit saved.","विज़िट सहेजी गई।","సందర్శన సేవ్ అయింది.","வருகை சேமிக்கப்பட்டது.","ಭೇಟಿ ಉಳಿಸಲಾಗಿದೆ."],
["Visit deleted.","विज़िट हटा दी गई।","సందర్శన తొలగించబడింది.","வருகை நீக்கப்பட்டது.","ಭೇಟಿ ಅಳಿಸಲಾಗಿದೆ."],
["All saved data deleted.","सारा सहेजा गया डेटा हटा दिया गया।","సేవ్ చేసిన డేటా మొత్తం తొలగించబడింది.","சேமித்த அனைத்துத் தரவும் நீக்கப்பட்டது.","ಉಳಿಸಿದ ಎಲ್ಲಾ ಡೇಟಾ ಅಳಿಸಲಾಗಿದೆ."],
["Stored only in this browser. If you clear your browser data or switch devices, they're gone, so copy any note you want to keep.","सिर्फ़ इसी ब्राउज़र में सहेजी हैं। ब्राउज़र डेटा साफ़ करने या डिवाइस बदलने पर ये मिट जाएँगी, इसलिए जो नोट रखना चाहें उसे कॉपी कर लें।","ఈ బ్రౌజర్‌లో మాత్రమే నిల్వ. బ్రౌజర్ డేటా క్లియర్ చేసినా లేదా పరికరం మార్చినా అవి పోతాయి, కాబట్టి ఉంచుకోవాలనుకునే నోట్‌ను కాపీ చేసుకోండి.","இந்த உலாவியில் மட்டுமே சேமிக்கப்படும். உலாவித் தரவை அழித்தாலோ சாதனத்தை மாற்றினாலோ அவை போய்விடும்; எனவே வைத்திருக்க விரும்பும் குறிப்பை நகலெடுத்துக்கொள்ளுங்கள்.","ಈ ಬ್ರೌಸರ್‌ನಲ್ಲಿ ಮಾತ್ರ ಸಂಗ್ರಹಿಸಲಾಗಿದೆ. ಬ್ರೌಸರ್ ಡೇಟಾ ಅಳಿಸಿದರೆ ಅಥವಾ ಸಾಧನ ಬದಲಿಸಿದರೆ ಅವು ಹೋಗುತ್ತವೆ, ಆದ್ದರಿಂದ ಇಟ್ಟುಕೊಳ್ಳಬೇಕಾದ ಟಿಪ್ಪಣಿಯನ್ನು ನಕಲಿಸಿಕೊಳ್ಳಿ."],
["No saved visits yet. Finish an intake and choose Save visit.","अभी कोई सहेजी गई विज़िट नहीं है। प्रविष्टि पूरी करके 'विज़िट सहेजें' चुनें।","ఇంకా సేవ్ చేసిన సందర్శనలు లేవు. నమోదు పూర్తి చేసి 'సందర్శన సేవ్ చేయండి' ఎంచుకోండి.","இன்னும் சேமித்த வருகைகள் இல்லை. பதிவை முடித்து 'வருகையைச் சேமிக்கவும்' என்பதைத் தேர்ந்தெடுக்கவும்.","ಇನ್ನೂ ಉಳಿಸಿದ ಭೇಟಿಗಳಿಲ್ಲ. ನೋಂದಣಿ ಪೂರ್ಣಗೊಳಿಸಿ 'ಭೇಟಿ ಉಳಿಸಿ' ಆಯ್ಕೆಮಾಡಿ."],
["Unnamed","बिना नाम","పేరు లేదు","பெயரில்லை","ಹೆಸರಿಲ್ಲ"],
["Delete this visit","यह विज़िट हटाएँ","ఈ సందర్శనను తొలగించండి","இந்த வருகையை நீக்கவும்","ಈ ಭೇಟಿಯನ್ನು ಅಳಿಸಿ"],
["Delete this visit for good?","क्या यह विज़िट हमेशा के लिए हटाएँ?","ఈ సందర్శనను శాశ్వతంగా తొలగించాలా?","இந்த வருகையை நிரந்தரமாக நீக்கவா?","ಈ ಭೇಟಿಯನ್ನು ಶಾಶ್ವತವಾಗಿ ಅಳಿಸಬೇಕೆ?"],
["Yes, delete","हाँ, हटाएँ","అవును, తొలగించు","ஆம், நீக்கு","ಹೌದು, ಅಳಿಸಿ"],
["Keep it","रहने दें","ఉంచండి","வைத்திருக்கவும்","ಇರಲಿ"],
["Delete all saved data","सारा सहेजा गया डेटा हटाएँ","సేవ్ చేసిన డేటా మొత్తం తొలగించండి","சேமித்த அனைத்துத் தரவையும் நீக்கவும்","ಉಳಿಸಿದ ಎಲ್ಲಾ ಡೇಟಾ ಅಳಿಸಿ"],
["Delete all saved visits and any draft?","सभी सहेजी गई विज़िट और ड्राफ़्ट हटाएँ?","సేవ్ చేసిన అన్ని సందర్శనలు మరియు డ్రాఫ్ట్ తొలగించాలా?","சேமித்த அனைத்து வருகைகளையும் வரைவையும் நீக்கவா?","ಉಳಿಸಿದ ಎಲ್ಲಾ ಭೇಟಿಗಳು ಮತ್ತು ಡ್ರಾಫ್ಟ್ ಅಳಿಸಬೇಕೆ?"],
["Yes, delete everything","हाँ, सब हटाएँ","అవును, అన్నీ తొలగించు","ஆம், எல்லாவற்றையும் நீக்கு","ಹೌದು, ಎಲ್ಲವನ್ನೂ ಅಳಿಸಿ"],
["Keep them","रहने दें","ఉంచండి","வைத்திருக்கவும்","ಇರಲಿ"]
];
const DICT = {};
LANGS.forEach((c, i) => { DICT[c] = {}; TABLE.forEach(r => { if (r[i + 1]) DICT[c][r[0]] = r[i + 1]; }); });
let lang = 'en';
const missing = new Set();
const fill = (s, v) => v ? s.replace(/\{(\w+)\}/g, (m, k) => (k in v) ? v[k] : m) : s;
const tr = (k, v) => {
  if (lang !== 'en') { const t = DICT[lang][k]; if (t) return fill(t, v); missing.add(k); }
  return fill(k, v);
};
window.__cs = {missing, TABLE, tr};
const fmt = (iso, code) => { try { return new Date(iso).toLocaleString(LOC[code || lang] || undefined, {dateStyle:'medium', timeStyle:'short'}); } catch (e) { return String(iso); } };

/* ---------- content ---------- */
const STEP_TITLES = ['About you', 'Safety check', 'Your symptoms', 'Background', 'Medicines and allergies', 'Review and save'];
const RED = [
  {id:'chest',    label:'Chest pain, pressure or tightness right now', short:'chest pain or pressure right now'},
  {id:'breath',   label:'Severe difficulty breathing, or unable to speak a full sentence', short:'severe difficulty breathing'},
  {id:'stroke',   label:'Sudden weakness or numbness on one side, a drooping face, or slurred speech', short:'possible stroke signs'},
  {id:'headache', label:'A sudden, severe headache, the worst you have ever had', short:'sudden severe headache'},
  {id:'faint',    label:'Fainting or loss of consciousness', short:'fainting or loss of consciousness'},
  {id:'seizure',  label:'A seizure', short:'a seizure'},
  {id:'bleeding', label:'Vomiting blood, black stools, or bleeding that will not stop', short:'serious bleeding'},
  {id:'allergy',  label:'Swelling of the lips, tongue or throat after food, medicine or a sting', short:'possible severe allergic reaction'},
  {id:'selfharm', label:'Thoughts of harming yourself or ending your life', short:'thoughts of self-harm'}
];
const SYMPTOMS = {
  'General': ['Fever','Chills','Fatigue','Unintended weight loss','Night sweats','Loss of appetite'],
  'Head and senses': ['Headache','Dizziness','Blurred vision','Sore throat','Ear pain','Runny or blocked nose'],
  'Chest and breathing': ['Cough','Shortness of breath','Chest pain','Palpitations','Wheezing'],
  'Stomach and bowels': ['Nausea','Vomiting','Abdominal pain','Diarrhea','Constipation','Blood in stool','Heartburn'],
  'Body and skin': ['Rash','Joint pain','Muscle aches','Swelling in legs','Burning when urinating','Blood in urine'],
  'Mood and sleep': ['Low mood','Anxiety','Trouble sleeping']
};
const CONDITIONS = ['Diabetes','High blood pressure','Heart disease','Asthma or COPD','Kidney disease','Liver disease','Thyroid disorder','Epilepsy','Cancer','Weakened immunity','Depression or anxiety','Tuberculosis'];
const FAMILY = ['Diabetes','Heart disease','High blood pressure','Cancer','Stroke','Asthma'];
const LEVELS = {
  pending:   {label:'Not assessed yet', short:'Pending', head:'Not assessed yet', act:'Complete the safety check and describe your main problem to see a result.'},
  routine:   {label:'Routine appointment', short:'Routine', head:'A routine appointment is fine', act:'Book a regular visit. Get emergency help if you develop chest pain, trouble breathing, or anything from the safety check.'},
  urgent:    {label:'See a doctor within 24 hours', short:'Urgent', head:'See a doctor within 24 hours', act:'Book a same-day or next-day visit, or go to an urgent care clinic. If things get worse, treat it as an emergency.'},
  emergency: {label:'Emergency care now', short:'Emergency', head:'Get emergency care now', act:'Call 112 or go to the nearest emergency department. Do not wait for an appointment and do not drive yourself.'}
};
const K_QUOTE = "In the patient's words: \"{q}\"";
const K_FINE = "Rules-based screening from the patient's own answers. It is not a diagnosis and needs review by a clinician.";

/* ---------- state ---------- */
const blank = () => ({
  patient:{name:'', age:'', sex:'', pregnant:''},
  visit:{complaint:'', durNum:'', durUnit:'days', onset:'', severity:5, severityTouched:false, worse:'', better:''},
  symptoms:[], redFlags:[], safetyDone:false,
  history:{conditions:[], other:'', surgeries:'', family:[]},
  meds:[], noMeds:false, allergies:[], noAllergies:false,
  lifestyle:{smoking:'', alcohol:'', sleep:'', activity:''}
});
function merge(base, src){
  if (!src || typeof src !== 'object') return base;
  Object.keys(base).forEach(k => {
    if (!(k in src)) return;
    const b = base[k];
    if (Array.isArray(b)) base[k] = Array.isArray(src[k]) ? src[k] : b;
    else if (b && typeof b === 'object') base[k] = merge(b, src[k]);
    else base[k] = src[k];
  });
  return base;
}
let state = blank(), step = 0, maxStep = 0, savedId = null, started = false;
let lastLevel = 'pending', view = 'intake', selected = null, pendingDel = null, pendingWipe = false, noteLang = 'en';
const tlOn = () => lang !== 'en' && noteLang === 'ui';
const showPreg = s => s.patient.sex === 'female' && Number(s.patient.age) >= 12 && Number(s.patient.age) <= 55 && s.patient.age !== '';

/* ---------- screening rules (reasons are [template, vars]) ---------- */
function durDays(v){
  const n = parseFloat(v.durNum); if (!(n > 0)) return null;
  return n * ({hours:1/24, days:1, weeks:7, months:30}[v.durUnit] || 1);
}
function triage(s){
  const em = s.redFlags.map(id => (RED.find(r => r.id === id) || {}).short).filter(Boolean);
  if (em.length) return {level:'emergency', reasons:em.map(x => ['You reported {x}.', {x}])};
  if (!s.safetyDone || s.visit.complaint.trim().length < 3) return {level:'pending', reasons:[]};
  const has = x => s.symptoms.includes(x), cond = x => s.history.conditions.includes(x);
  const age = s.patient.age === '' ? null : Number(s.patient.age);
  const dd = durDays(s.visit);
  const sev = s.visit.severityTouched ? Number(s.visit.severity) : null;
  const r = [];
  if (sev !== null && sev >= 8) r.push(['You rated the problem {n} out of 10 at its worst.', {n:sev}]);
  if (has('Fever') && dd !== null && dd >= 3) r.push(['Fever lasting 3 days or more.']);
  if (has('Fever') && age !== null && (age < 3 || age >= 65)) r.push(['Fever in a young child or an adult aged 65 or over.']);
  if (has('Fever') && (cond('Cancer') || cond('Weakened immunity'))) r.push(['Fever with a condition that weakens the immune system.']);
  if (has('Chest pain')) r.push(['Chest pain, even if it is not happening now.']);
  if (has('Shortness of breath')) r.push(['Shortness of breath.']);
  if (has('Blood in stool') || has('Blood in urine')) r.push(['Blood in stool or urine.']);
  if (has('Unintended weight loss')) r.push(['Unintended weight loss needs a prompt check.']);
  if ((has('Vomiting') || has('Diarrhea')) && dd !== null && dd >= 2 && ((age !== null && (age < 5 || age >= 65)) || cond('Diabetes') || cond('Kidney disease'))) r.push(['Vomiting or diarrhea for 2 days or more, with a higher risk of dehydration.']);
  if ((s.patient.pregnant === 'yes' || s.patient.pregnant === 'unsure') && (has('Abdominal pain') || (has('Headache') && has('Blurred vision')))) r.push(['Abdominal pain, or headache with blurred vision, during possible pregnancy.']);
  if (r.length) return {level:'urgent', reasons:r};
  const rr = [];
  if (dd !== null && dd >= 14) rr.push(['Symptoms lasting more than 2 weeks should be checked, even if mild.']);
  else rr.push(['No emergency or urgent signs in your answers.']);
  return {level:'routine', reasons:rr};
}
/* tl=true: translate into the interface language; tl=false: English */
function rtxt(r, tl){
  const vars = {};
  Object.keys(r[1] || {}).forEach(k => { const x = r[1][k]; vars[k] = (tl && k === 'x') ? tr(x) : x; });
  return tl ? tr(r[0], vars) : fill(r[0], vars);
}

/* ---------- note model ---------- */
function model(s, tl){
  const T = (k, v) => tl ? tr(k, v) : fill(k, v);
  const t = triage(s), P = s.patient, V = s.visit, H = s.history, L = s.lifestyle;
  const list = a => a.map(x => T(x)).join(', ');
  const raw = a => a.join(', ');
  const sexL = {female:T('Female'), male:T('Male'), other:T('Other'), na:T('Prefer not to say')};
  const pregL = {yes:T('Yes'), no:T('No'), unsure:T('Not sure')};
  const dur = V.durNum ? V.durNum + ' ' + (tl ? tr(V.durUnit) : (Number(V.durNum) === 1 ? V.durUnit.replace(/s$/, '') : V.durUnit)) : '';
  const secs = [
    {title:T('Patient'), rows:[[T('Name'), P.name.trim()], [T('Age'), P.age !== '' ? T('{n} years', {n:P.age}) : ''], [T('Sex'), sexL[P.sex] || ''], [T('Pregnancy'), showPreg(s) ? (pregL[P.pregnant] || '') : '']]},
    {title:T('Reason for visit'), quote:V.complaint.trim(), rows:[[T('Duration'), dur], [T('Onset'), V.onset ? T(V.onset) : ''], [T('Severity'), V.severityTouched ? T('{n} out of 10', {n:V.severity}) : ''], [T('Worse with'), V.worse.trim()], [T('Better with'), V.better.trim()]]},
    {title:T('Other symptoms'), text:list(s.symptoms)},
    {title:T('Emergency check'), text:s.redFlags.length ? T('Reported: {x}.', {x:s.redFlags.map(id => T((RED.find(r => r.id === id) || {}).short)).join(', ')}) : (s.safetyDone ? T('No emergency symptoms reported.') : '')},
    {title:T('Medical history'), rows:[[T('Conditions'), list(H.conditions)], [T('Other'), H.other.trim()], [T('Surgeries'), H.surgeries.trim()], [T('Family'), list(H.family)]]},
    {title:T('Medicines'), text:s.noMeds ? T('No regular medicines.') : raw(s.meds)},
    {title:T('Allergies'), text:s.noAllergies ? T('No known allergies.') : raw(s.allergies)},
    {title:T('Lifestyle'), rows:[[T('Smoking'), L.smoking ? T(L.smoking) : ''], [T('Alcohol'), L.alcohol ? T(L.alcohol) : ''], [T('Sleep'), L.sleep ? T(L.sleep) : ''], [T('Activity'), L.activity ? T(L.activity) : '']]},
    {title:T('Screening result'), level:true}
  ];
  return {t, secs, T, head:T('Pre-visit intake note'), levelLabel:T(LEVELS[t.level].label), reasons:t.reasons.map(r => rtxt(r, tl)), fine:T(K_FINE), phTxt:T('Not provided yet'), pendingTxt:T(LEVELS.pending.act), noneTxt:T('Not provided')};
}
function pulse(level){
  const cfg = {pending:[0,0], routine:[2,6], urgent:[3,9], emergency:[5,12]}[level];
  const n = cfg[0], a = cfg[1], W = 200, mid = 14;
  if (!n) return 'M0 ' + mid + 'H' + W;
  const seg = W / n; let d = 'M0 ' + mid;
  for (let i = 0; i < n; i++) {
    const x = i * seg;
    d += 'H' + (x + seg * .35) + 'l' + (seg * .08) + ' ' + (-a) + 'l' + (seg * .1) + ' ' + (a * 1.9) + 'l' + (seg * .08) + ' ' + (-a * .9);
  }
  return d + 'H' + W;
}
function sectionHTML(sec, m){
  const ph = txt => `<p class="ph">${esc(txt)}</p>`;
  let h = `<section class="ns"><h3>${esc(sec.title)}</h3>`;
  if (sec.level) {
    h += `<p><span class="badge" data-level="${m.t.level}">${esc(m.levelLabel)}</span></p>`;
    h += m.reasons.length ? '<ul>' + m.reasons.map(x => `<li>${esc(x)}</li>`).join('') + '</ul>' : ph(m.pendingTxt);
    h += `<p class="fine">${esc(m.fine)}</p>`;
  } else {
    const rows = (sec.rows || []).filter(r => r[1]);
    const any = !!(sec.quote || sec.text || rows.length);
    if (sec.quote) h += `<p class="quote">\u201C${esc(sec.quote)}\u201D</p>`;
    if (sec.text) h += `<p>${esc(sec.text)}</p>`;
    if (rows.length) h += '<dl>' + rows.map(r => `<dt>${esc(r[0])}</dt><dd>${esc(r[1])}</dd>`).join('') + '</dl>';
    if (!any) h += ph(m.phTxt);
  }
  return h + '</section>';
}
function noteHTML(s, dateStr, fresh, tl){
  const m = model(s, tl);
  return `<article class="paper" aria-label="${esc(m.head)}"><h2>${esc(m.head)}</h2><p class="meta">${esc(m.T('Prepared with CliniScribe on {d}', {d:dateStr}))}</p>` +
    `<div class="strip${fresh ? ' fresh' : ''}" data-level="${m.t.level}"><svg viewBox="0 0 200 28" preserveAspectRatio="none" aria-hidden="true"><path pathLength="100" d="${pulse(m.t.level)}"/></svg><span class="strip-label">${esc(m.levelLabel)}</span></div>` +
    m.secs.map(sec => sectionHTML(sec, m)).join('') + '</article>';
}
function noteText(s, dateStr, tl){
  const m = model(s, tl);
  const out = [m.head.toUpperCase(), m.T('Prepared with CliniScribe on {d}', {d:dateStr}), ''];
  m.secs.forEach(sec => {
    out.push(sec.title.toUpperCase());
    if (sec.level) {
      out.push(m.levelLabel);
      m.reasons.forEach(r => out.push('- ' + r));
      out.push(m.fine);
    } else {
      const rows = (sec.rows || []).filter(r => r[1]);
      if (sec.quote) out.push(m.T(K_QUOTE, {q:sec.quote}));
      if (sec.text) out.push(sec.text);
      rows.forEach(r => out.push(r[0] + ': ' + r[1]));
      if (!(sec.quote || sec.text || rows.length)) out.push(m.noneTxt);
    }
    out.push('');
  });
  return out.join('\n');
}
function noteLangHTML(){
  if (lang === 'en') return '';
  return `<span class="lbl-inline">${esc(tr('Show note in'))}</span><div class="seg" role="group" aria-label="${esc(tr('Show note in'))}"><button type="button" data-notelang="en" aria-pressed="${noteLang === 'en'}" lang="en">English</button><button type="button" data-notelang="ui" aria-pressed="${noteLang === 'ui'}" lang="${lang}">${esc(NATIVE[lang])}</button></div><p class="fine">${esc(tr('English is best for your doctor. Your own words stay as you typed them.'))}</p>`;
}
function renderNoteLang(){
  const box = $('#noteLangBox'); if (!box) return;
  box.hidden = lang === 'en'; box.innerHTML = noteLangHTML();
}

/* ---------- toast, copy, print ---------- */
let toastTimer;
function say(msg){
  const t = $('#toast'); t.textContent = msg; t.hidden = false;
  clearTimeout(toastTimer); toastTimer = setTimeout(() => { t.hidden = true; }, 4200);
}
async function copyText(text){
  try { if (navigator.clipboard && window.isSecureContext) { await navigator.clipboard.writeText(text); return true; } } catch (e) {}
  try {
    const ta = document.createElement('textarea');
    ta.value = text; ta.setAttribute('readonly', ''); ta.style.cssText = 'position:fixed;top:0;left:0;opacity:0';
    document.body.appendChild(ta); ta.select();
    const ok = document.execCommand('copy'); ta.remove(); return ok;
  } catch (e) { return false; }
}
async function doCopy(text, boxSel){
  const box = $(boxSel);
  if (await copyText(text)) { box.hidden = true; say(tr('Note copied. Paste it into a message or email.')); return; }
  box.hidden = false;
  box.innerHTML = `<p class="hint">${esc(tr('Your browser blocked copying. Select all the text below and copy it.'))}</p><textarea readonly aria-label="${esc(tr('Note text'))}">${esc(text)}</textarea>`;
  const ta = $('textarea', box); ta.focus(); ta.select();
}
function doPrint(){
  say(tr('Opening the print dialog. If nothing appears, press Ctrl+P (Cmd+P on Mac).'));
  try { window.print(); } catch (e) {}
}

/* ---------- draft ---------- */
let draftTimer;
function saveDraft(){
  if (!started) return;
  clearTimeout(draftTimer);
  draftTimer = setTimeout(() => { store.set('cs:draft', {state, step, maxStep, savedAt:new Date().toISOString()}); }, 300);
}
const getVisits = () => store.get('cs:visits') || [];
function updateCount(){
  const n = getVisits().length, c = $('#count');
  c.textContent = n; c.hidden = n === 0;
}

/* ---------- chrome ---------- */
function updateEmergency(){
  const bar = $('#emergencyBar');
  const on = view === 'intake' && started && state.redFlags.length > 0;
  bar.hidden = !on;
  if (on) {
    const tel = n => `<a href="tel:${n}">${n}</a>`;
    let h = `<strong>${esc(tr('You reported symptoms that need emergency care.'))}</strong> ` + tr('Call {tel} (or your local emergency number) or go to the nearest emergency department now. Do not drive yourself.', {tel:tel('112')});
    if (state.redFlags.includes('selfharm')) h += ' ' + tr('If you are thinking of harming yourself, call Tele-MANAS on {tel} (India, free, 24 hours a day) or tell someone near you right now.', {tel:tel('14416')});
    bar.innerHTML = h;
  }
  setChromeH();
}
function setChromeH(){ document.documentElement.style.setProperty('--chrome-h', $('#chrome').offsetHeight + 'px'); }
function setView(v){
  view = v;
  $('#viewIntake').hidden = v !== 'intake';
  $('#viewHistory').hidden = v !== 'history';
  $$('[data-nav]').forEach(b => b.setAttribute('aria-current', b.dataset.nav === v ? 'page' : 'false'));
  if (v === 'history') renderHistory();
  updateEmergency();
  window.scrollTo({top:0});
}
function setLayoutView(v){
  $('#layout').dataset.view = v;
  $$('.view-switch button').forEach(b => b.setAttribute('aria-pressed', String(b.dataset.view === v)));
}

/* ---------- language ---------- */
function applyStatic(){
  $$('[data-i18n]').forEach(el => { el.textContent = tr(el.getAttribute('data-i18n')); });
  $$('[data-i18n-aria]').forEach(el => { el.setAttribute('aria-label', tr(el.getAttribute('data-i18n-aria'))); });
}
function buildLangUI(){
  $('#langSel').innerHTML = Object.keys(NATIVE).map(c => `<option value="${c}" lang="${c}">${esc(NATIVE[c])}</option>`).join('');
  $('#langPick').innerHTML = Object.keys(NATIVE).map(c => `<label class="chip"><input type="radio" name="lang" value="${c}"><span lang="${c}">${esc(NATIVE[c])}</span></label>`).join('');
}
function setLang(code, persist){
  if (!NATIVE[code]) code = 'en';
  lang = code;
  if (persist) store.set('cs:lang', code);
  document.documentElement.lang = code;
  $('#langSel').value = code;
  $$('#langPick input').forEach(i => { i.checked = i.value === code; });
  applyStatic(); renderNoteLang(); renderResume();
  if (started) { renderSteps(); renderStep(); }
  updateNote(); updateEmergency();
  if (view === 'history') renderHistory();
}

/* ---------- live note ---------- */
function updateNote(){
  const t = triage(state);
  const fresh = t.level !== lastLevel; lastLevel = t.level;
  const tl = tlOn();
  $('#noteBody').innerHTML = noteHTML(state, fmt(new Date().toISOString(), tl ? lang : 'en'), fresh, tl);
  $('#noteDot').dataset.level = t.level;
}

/* ---------- consent pane ---------- */
function renderResume(){
  const d = store.get('cs:draft'), box = $('#resumeBox');
  if (d && d.state && (d.state.patient && d.state.patient.name || d.state.visit && d.state.visit.complaint)) {
    box.hidden = false;
    box.innerHTML = `<p><strong>${esc(tr('You have an unfinished intake from {d}.', {d:fmt(d.savedAt)}))}</strong></p><div class="row"><button type="button" class="btn primary sm" data-act="resume">${esc(tr('Resume it'))}</button><button type="button" class="btn ghost sm" data-act="discard">${esc(tr('Start over'))}</button></div>`;
  } else box.hidden = true;
}
function renderConsent(){
  started = false;
  $('#consentPane').hidden = false; $('#wizardPane').hidden = true;
  $('#agree').checked = false; $('#startBtn').disabled = true;
  renderResume();
  state = blank(); step = 0; maxStep = 0; savedId = null;
  updateNote(); updateEmergency();
}
function startWizard(resumeDraft){
  if (resumeDraft) {
    const d = store.get('cs:draft');
    if (d) { state = merge(blank(), d.state); step = Math.min(5, d.step || 0); maxStep = Math.max(step, d.maxStep || 0); }
  } else { state = blank(); step = 0; maxStep = 0; store.del('cs:draft'); }
  savedId = null; started = true;
  $('#consentPane').hidden = true; $('#wizardPane').hidden = false;
  renderSteps(); renderStep(); updateNote(); updateEmergency(); setLayoutView('form');
}

/* ---------- wizard rendering ---------- */
const chip = (type, attrs, label, checked) => `<label class="chip"><input type="${type}" ${attrs}${checked ? ' checked' : ''}><span>${esc(label)}</span></label>`;
const groupChips = (group, list, arr) => list.map(x => chip('checkbox', `data-group="${group}" value="${esc(x)}"`, tr(x), arr.includes(x))).join('');
const radioChips = (path, opts, cur) => opts.map(o => { const v = Array.isArray(o) ? o[0] : o, l = Array.isArray(o) ? o[1] : o; return chip('radio', `name="${path}" data-k="${path}" value="${esc(v)}"`, tr(l), cur === v); }).join('');
const head = (n, title, lede) => `<p class="step-count">${esc(tr('Step {n} of 6', {n:n + 1}))}</p><h2 class="step-title" id="stepHead" tabindex="-1">${esc(tr(title))}</h2><p class="lede">${esc(tr(lede))}</p>`;
const err = id => `<p class="err" id="err-${id}" hidden></p>`;

function stepAbout(){
  const P = state.patient;
  return head(0, 'About you', 'Only what your doctor needs to put your symptoms in context.') + `
  <div class="field"><label class="lbl" for="f-name">${esc(tr('Name or nickname'))}</label>
    <input type="text" id="f-name" data-k="patient.name" autocomplete="name" maxlength="80" value="${esc(P.name)}">${err('name')}</div>
  <div class="field"><label class="lbl" for="f-age">${esc(tr('Age in years'))}</label>
    <input type="number" id="f-age" class="w-sm" data-k="patient.age" inputmode="numeric" min="0" max="120" value="${esc(P.age)}">${err('age')}</div>
  <fieldset><legend>${esc(tr('Sex'))}</legend><div class="chips">${radioChips('patient.sex', [['female','Female'],['male','Male'],['other','Other'],['na','Prefer not to say']], P.sex)}</div></fieldset>
  <fieldset id="pregBlock" ${showPreg(state) ? '' : 'hidden'}><legend>${esc(tr('Are you pregnant, or could you be?'))}</legend><div class="chips">${radioChips('patient.pregnant', [['yes','Yes'],['no','No'],['unsure','Not sure']], P.pregnant)}</div></fieldset>`;
}
function stepSafety(){
  return head(1, 'Safety check', 'Tick anything that applies right now. If you tick one, get emergency help first. You can finish this note afterwards.') +
  `<fieldset><legend class="sr">${esc(tr('Emergency symptoms'))}</legend><div class="flags">` +
  RED.map(r => `<label class="flag"><input type="checkbox" data-group="redFlags" value="${r.id}"${state.redFlags.includes(r.id) ? ' checked' : ''}><span>${esc(tr(r.label))}</span></label>`).join('') +
  `</div></fieldset><p class="hint">${esc(tr("Nothing ticked? Continue. That's the answer we need."))}</p>`;
}
function stepSymptoms(){
  const V = state.visit;
  return head(2, 'Your symptoms', 'Describe it the way you would to a friend. Details matter more than medical words.') + `
  <div class="field"><label class="lbl" for="f-complaint">${esc(tr('What is the main problem?'))}</label>
    <textarea id="f-complaint" data-k="visit.complaint" maxlength="400" placeholder="${esc(tr('For example: sore throat and fever since Monday, worse at night'))}">${esc(V.complaint)}</textarea>${err('complaint')}</div>
  <div class="field"><label class="lbl" for="f-dur">${esc(tr('How long has this been going on?'))}</label>
    <div class="row"><input type="number" id="f-dur" class="w-sm" data-k="visit.durNum" min="0" step="any" inputmode="decimal" value="${esc(V.durNum)}" aria-label="${esc(tr('Number'))}">
    <select class="w-md" data-k="visit.durUnit" aria-label="${esc(tr('Unit of time'))}">${['hours','days','weeks','months'].map(u => `<option value="${u}"${V.durUnit === u ? ' selected' : ''}>${esc(tr(u))}</option>`).join('')}</select></div>${err('dur')}</div>
  <fieldset><legend>${esc(tr('How did it start?'))}</legend><div class="chips">${radioChips('visit.onset', ['Sudden','Gradual','Comes and goes'], V.onset)}</div></fieldset>
  <div class="field"><label class="lbl" for="f-sev">${esc(tr('How bad is it at its worst?'))}</label>
    <div class="sev"><span class="sev-out${V.severityTouched ? '' : ' unset'}" id="sevOut">${esc(V.severityTouched ? tr('{n} out of 10', {n:V.severity}) : tr('Not rated yet. Move the slider.'))}</span></div>
    <input type="range" id="f-sev" data-k="visit.severity" min="0" max="10" step="1" value="${esc(V.severity)}">
    <div class="scale"><span>${esc(tr('0, none'))}</span><span>${esc(tr('10, worst imaginable'))}</span></div></div>
  <fieldset><legend>${esc(tr('Any other symptoms?'))}</legend>` +
  Object.keys(SYMPTOMS).map(g => `<p class="group-title">${esc(tr(g))}</p><div class="chips">${groupChips('symptoms', SYMPTOMS[g], state.symptoms)}</div>`).join('') + `</fieldset>
  <div class="field"><label class="lbl" for="f-worse">${esc(tr('What makes it worse?'))}</label><input type="text" id="f-worse" data-k="visit.worse" maxlength="120" value="${esc(V.worse)}"></div>
  <div class="field"><label class="lbl" for="f-better">${esc(tr('What makes it better?'))}</label><input type="text" id="f-better" data-k="visit.better" maxlength="120" value="${esc(V.better)}"></div>`;
}
function stepBackground(){
  const H = state.history, L = state.lifestyle;
  return head(3, 'Background', "Past health and habits help your doctor read today's symptoms. Skip anything you don't know.") + `
  <fieldset><legend>${esc(tr('Do you have any of these conditions?'))}</legend><div class="chips">${groupChips('history.conditions', CONDITIONS, H.conditions)}</div></fieldset>
  <div class="field"><label class="lbl" for="f-other">${esc(tr('Any other condition?'))}</label><input type="text" id="f-other" data-k="history.other" maxlength="120" value="${esc(H.other)}"></div>
  <div class="field"><label class="lbl" for="f-surg">${esc(tr('Past surgeries or hospital stays'))}</label><input type="text" id="f-surg" data-k="history.surgeries" maxlength="160" placeholder="${esc(tr('For example: appendix removed, 2019'))}" value="${esc(H.surgeries)}"></div>
  <fieldset><legend>${esc(tr('Close family with any of these?'))}</legend><div class="chips">${groupChips('history.family', FAMILY, H.family)}</div></fieldset>
  <fieldset><legend>${esc(tr('Smoking'))}</legend><div class="chips">${radioChips('lifestyle.smoking', ['Never','Former smoker','Current smoker'], L.smoking)}</div></fieldset>
  <fieldset><legend>${esc(tr('Alcohol'))}</legend><div class="chips">${radioChips('lifestyle.alcohol', ['None','Occasional','Regular'], L.alcohol)}</div></fieldset>
  <fieldset><legend>${esc(tr('Sleep per night'))}</legend><div class="chips">${radioChips('lifestyle.sleep', ['Under 5 hours','5 to 7 hours','7 to 9 hours','Over 9 hours'], L.sleep)}</div></fieldset>
  <fieldset><legend>${esc(tr('Physical activity'))}</legend><div class="chips">${radioChips('lifestyle.activity', ['Rarely','1 to 2 times a week','3 or more times a week'], L.activity)}</div></fieldset>`;
}
function tagField(k, label, hint, ph2, noKey, noLabel){
  return `<div class="field"><label class="lbl" for="f-in-${k}">${esc(tr(label))}</label><p class="hint">${esc(tr(hint))}</p>
  <div class="tag-row"><input type="text" id="f-in-${k}" data-tag-input="${k}" maxlength="120" placeholder="${esc(tr(ph2))}"><button type="button" class="btn secondary" data-tag-add="${k}">${esc(tr('Add'))}</button></div>
  <ul class="tags" id="tags-${k}" aria-label="${esc(tr(label))}"></ul>
  <label class="chip"><input type="checkbox" data-k="${noKey}"${state[noKey] ? ' checked' : ''}><span>${esc(tr(noLabel))}</span></label></div>`;
}
function stepMeds(){
  return head(4, 'Medicines and allergies', 'Include vitamins, herbal remedies and over-the-counter medicines.') +
    tagField('meds', 'Medicines you take regularly', 'Type a name and dose, then press Enter or Add.', 'For example: Metformin 500 mg, twice a day', 'noMeds', 'I take no regular medicines') +
    tagField('allergies', 'Allergies', 'Medicines, foods, latex, or anything that caused a reaction.', 'For example: Penicillin, rash', 'noAllergies', 'I have no known allergies');
}
function stepReview(){
  const t = triage(state), L = LEVELS[t.level];
  if (savedId) return `<p class="step-count">${esc(tr('Step {n} of 6', {n:6}))}</p><h2 class="step-title" id="stepHead" tabindex="-1">${esc(tr('Saved'))}</h2><p class="lede">${esc(tr('This visit is saved in this browser. Copy the note to send it to your doctor, or print it.'))}</p>
    <div class="tri" data-level="${t.level}"><h3>${esc(tr(L.head))}</h3><p>${esc(tr(L.act))}</p></div>`;
  return head(5, 'Review and save', "Read the note next to your answers. Fix anything that's wrong, then save it to this device.") +
    `<div class="tri" data-level="${t.level}"><h3>${esc(tr(L.head))}</h3>` +
    (t.reasons.length ? '<ul>' + t.reasons.map(r => `<li>${esc(rtxt(r, true))}</li>`).join('') + '</ul>' : '') +
    `<p>${esc(tr(L.act))}</p></div>
    <p class="lbl">${esc(tr('Change an answer'))}</p>
    <div class="chips">${STEP_TITLES.slice(0, 5).map((x, i) => `<button type="button" class="btn secondary sm" data-goto="${i}">${esc(tr(x))}</button>`).join('')}</div>`;
}
function renderSteps(){
  $('#steps').innerHTML = STEP_TITLES.map((t, i) => {
    const cls = i === step ? 'current' : (i < step || i <= maxStep ? 'done' : '');
    return `<li class="${cls}"><button type="button" data-goto="${i}" ${i > maxStep ? 'disabled' : ''} ${i === step ? 'aria-current="step"' : ''}><span class="t">${esc(tr(t))}</span></button></li>`;
  }).join('');
}
function renderNav(){
  let h = `<button type="button" class="btn ghost" data-act="back" ${step === 0 ? 'hidden' : ''}>${esc(tr('Back'))}</button>`;
  if (step < 5) h += `<button type="button" class="btn primary" data-act="next">${esc(tr(step === 1 && state.redFlags.length ? 'Continue anyway' : 'Continue'))}</button>`;
  else if (!savedId) h += `<button type="button" class="btn primary" data-act="save">${esc(tr('Save visit'))}</button>`;
  else h += `<button type="button" class="btn secondary" data-act="history">${esc(tr('View saved visits'))}</button><button type="button" class="btn primary" data-act="new">${esc(tr('Start new intake'))}</button>`;
  $('#nav').innerHTML = h;
}
function renderStep(){
  const fn = [stepAbout, stepSafety, stepSymptoms, stepBackground, stepMeds, stepReview][step];
  $('#stepBody').innerHTML = fn();
  if (step === 4) renderTags();
  renderNav();
}
function renderTags(){
  ['meds', 'allergies'].forEach(k => {
    const ul = $('#tags-' + k); if (!ul) return;
    ul.innerHTML = state[k].map((x, i) => `<li class="tag"><span>${esc(x)}</span><button type="button" data-remove="${k}:${i}" aria-label="${esc(tr('Remove {x}', {x}))}">\u00D7</button></li>`).join('');
    const no = k === 'meds' ? state.noMeds : state.noAllergies;
    $('#f-in-' + k).disabled = no; $('[data-tag-add="' + k + '"]').disabled = no;
  });
}
function addTag(k){
  const inp = $('#f-in-' + k); if (!inp) return;
  const v = inp.value.trim(); if (!v) return;
  if (!state[k].some(x => x.toLowerCase() === v.toLowerCase())) state[k].push(v.slice(0, 120));
  inp.value = '';
  const noKey = k === 'meds' ? 'noMeds' : 'noAllergies';
  state[noKey] = false;
  const cb = $('[data-k="' + noKey + '"]'); if (cb) cb.checked = false;
  renderTags(); updateNote(); saveDraft(); inp.focus();
}

/* ---------- navigation and validation ---------- */
function validate(i){
  const e = [];
  if (i === 0) {
    if (!state.patient.name.trim()) e.push(['name', 'Enter your name or a nickname so the note can be matched to you.']);
    const a = state.patient.age;
    if (a === '' || isNaN(Number(a)) || Number(a) < 0 || Number(a) > 120) e.push(['age', 'Enter an age between 0 and 120.']);
  }
  if (i === 2) {
    if (state.visit.complaint.trim().length < 3) e.push(['complaint', 'Describe the main problem in a few words.']);
    if (!(parseFloat(state.visit.durNum) > 0)) e.push(['dur', 'Enter how long this has been going on, for example 3 days.']);
  }
  return e;
}
function showErrors(list){
  list.forEach(([id, msg]) => {
    const p = $('#err-' + id); if (p) { p.textContent = tr(msg); p.hidden = false; }
    const f = $('#f-' + id); if (f) f.setAttribute('aria-invalid', 'true');
  });
  const first = $('#f-' + list[0][0]); if (first) first.focus();
}
function clearError(t){
  if (!t.id || t.id.indexOf('f-') !== 0) return;
  const p = $('#err-' + t.id.slice(2)); if (p) p.hidden = true;
  t.removeAttribute('aria-invalid');
}
function flushTags(){ if (step === 4) ['meds', 'allergies'].forEach(k => { const i = $('#f-in-' + k); if (i && i.value.trim()) addTag(k); }); }
function goto(n){
  step = n; maxStep = Math.max(maxStep, n);
  renderSteps(); renderStep(); updateNote(); saveDraft();
  window.scrollTo({top:0});
  const h = $('#stepHead'); if (h) h.focus({preventScroll:true});
  setLayoutView('form');
}
function tryGoto(n){
  flushTags();
  if (n > step) { const e = validate(step); if (e.length) { showErrors(e); return; } if (step === 1) state.safetyDone = true; }
  goto(n);
}
function save(){
  const rec = {id:savedId || uid(), savedAt:new Date().toISOString(), state:JSON.parse(JSON.stringify(state))};
  let v = getVisits(); const i = v.findIndex(x => x.id === rec.id);
  if (i >= 0) v[i] = rec; else v.unshift(rec);
  v = v.slice(0, 50);
  if (!store.set('cs:visits', v)) { say(tr("This browser blocked saving. Copy the note so you don't lose it.")); return; }
  savedId = rec.id; store.del('cs:draft'); updateCount(); renderStep(); say(tr('Visit saved.'));
  const h = $('#stepHead'); if (h) h.focus({preventScroll:true});
}

/* ---------- field events ---------- */
function updatePreg(){
  const b = $('#pregBlock'); if (!b) return;
  const show = showPreg(state); b.hidden = !show;
  if (!show) { state.patient.pregnant = ''; $$('input[name="patient.pregnant"]', b).forEach(i => { i.checked = false; }); }
}
function onField(e){
  const t = e.target;
  if (t.dataset.group) {
    const arr = getPath(state, t.dataset.group), v = t.value, i = arr.indexOf(v);
    if (t.checked && i < 0) arr.push(v);
    if (!t.checked && i >= 0) arr.splice(i, 1);
  } else if (t.dataset.k) {
    let val;
    if (t.type === 'checkbox') val = t.checked;
    else if (t.type === 'radio') { if (!t.checked) return; val = t.value; }
    else val = t.value;
    if (t.dataset.k === 'visit.severity') { val = Number(val); state.visit.severityTouched = true; const o = $('#sevOut'); o.textContent = tr('{n} out of 10', {n:val}); o.classList.remove('unset'); }
    setPath(state, t.dataset.k, val);
    if (t.dataset.k === 'patient.sex' || t.dataset.k === 'patient.age') updatePreg();
    if (t.dataset.k === 'noMeds' && state.noMeds) state.meds = [];
    if (t.dataset.k === 'noAllergies' && state.noAllergies) state.allergies = [];
    if (t.dataset.k === 'noMeds' || t.dataset.k === 'noAllergies') renderTags();
  } else return;
  clearError(t);
  if (t.dataset.group === 'redFlags') renderNav();
  updateEmergency(); updateNote(); saveDraft();
}

/* ---------- history ---------- */
function renderHistory(){
  const v = getVisits(), list = $('#histList'), det = $('#histDetail'), wipe = $('#wipeBox');
  if (!v.length) {
    list.innerHTML = `<li class="empty">${esc(tr('No saved visits yet. Finish an intake and choose Save visit.'))}</li>`;
    det.innerHTML = ''; wipe.innerHTML = ''; return;
  }
  if (!selected || !v.find(x => x.id === selected)) selected = v[0].id;
  list.innerHTML = v.map(r => {
    const t = triage(r.state);
    return `<li><button type="button" class="hitem" data-hist="${esc(r.id)}"${r.id === selected ? ' aria-current="true"' : ''}><span class="hn">${esc(r.state.patient.name || tr('Unnamed'))}</span><span class="hd">${esc(fmt(r.savedAt))}</span><span class="hc">${esc(r.state.visit.complaint)}</span><span class="badge" data-level="${t.level}">${esc(tr(LEVELS[t.level].short))}</span></button></li>`;
  }).join('');
  const rec = v.find(x => x.id === selected), tl = tlOn();
  det.innerHTML = (lang === 'en' ? '' : `<div class="notelang no-print">${noteLangHTML()}</div>`) + noteHTML(rec.state, fmt(rec.savedAt, tl ? lang : 'en'), false, tl) + `<div class="note-actions no-print">
    <button type="button" class="btn secondary" data-act="copy-hist">${esc(tr('Copy note'))}</button>
    <button type="button" class="btn secondary" data-act="print">${esc(tr('Print'))}</button>
    ${pendingDel === rec.id ? '' : `<button type="button" class="btn danger-btn" data-act="del-hist">${esc(tr('Delete this visit'))}</button>`}</div>
    ${pendingDel === rec.id ? `<div class="confirm no-print"><p>${esc(tr('Delete this visit for good?'))}</p><button type="button" class="btn danger-btn sm" data-act="del-hist-yes">${esc(tr('Yes, delete'))}</button><button type="button" class="btn ghost sm" data-act="del-hist-no">${esc(tr('Keep it'))}</button></div>` : ''}
    <div class="copy-fallback no-print" id="copyFallbackHist" hidden></div>`;
  wipe.innerHTML = pendingWipe
    ? `<div class="confirm"><p>${esc(tr('Delete all saved visits and any draft?'))}</p><button type="button" class="btn danger-btn sm" data-act="wipe-yes">${esc(tr('Yes, delete everything'))}</button><button type="button" class="btn ghost sm" data-act="wipe-no">${esc(tr('Keep them'))}</button></div>`
    : `<button type="button" class="btn ghost sm" data-act="wipe">${esc(tr('Delete all saved data'))}</button>`;
}

/* ---------- events ---------- */
document.addEventListener('click', e => {
  const b = e.target.closest('[data-act],[data-goto],[data-nav],[data-remove],[data-tag-add],[data-hist],[data-view],[data-notelang]');
  if (!b) return;
  if (b.dataset.notelang) { noteLang = b.dataset.notelang; renderNoteLang(); updateNote(); if (view === 'history') renderHistory(); return; }
  if (b.dataset.view) return setLayoutView(b.dataset.view);
  if (b.dataset.nav) return setView(b.dataset.nav);
  if (b.dataset.goto !== undefined) return tryGoto(Number(b.dataset.goto));
  if (b.dataset.tagAdd) return addTag(b.dataset.tagAdd);
  if (b.dataset.remove) { const [k, i] = b.dataset.remove.split(':'); state[k].splice(Number(i), 1); renderTags(); updateNote(); saveDraft(); return; }
  if (b.dataset.hist) { selected = b.dataset.hist; pendingDel = null; return renderHistory(); }
  switch (b.dataset.act) {
    case 'theme': {
      const cur = document.documentElement.getAttribute('data-theme') || (matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
      const nx = cur === 'dark' ? 'light' : 'dark';
      document.documentElement.setAttribute('data-theme', nx); store.set('cs:theme', nx); break;
    }
    case 'back': if (step > 0) goto(step - 1); break;
    case 'next': tryGoto(step + 1); break;
    case 'save': save(); break;
    case 'history': setView('history'); break;
    case 'new': renderConsent(); setLayoutView('form'); window.scrollTo({top:0}); break;
    case 'resume': startWizard(true); break;
    case 'discard': store.del('cs:draft'); renderConsent(); break;
    case 'copy-live': { const tl = tlOn(); doCopy(noteText(state, fmt(new Date().toISOString(), tl ? lang : 'en'), tl), '#copyFallbackLive'); break; }
    case 'print': doPrint(); break;
    case 'copy-hist': { const r = getVisits().find(x => x.id === selected), tl = tlOn(); if (r) doCopy(noteText(r.state, fmt(r.savedAt, tl ? lang : 'en'), tl), '#copyFallbackHist'); break; }
    case 'del-hist': pendingDel = selected; renderHistory(); break;
    case 'del-hist-no': pendingDel = null; renderHistory(); break;
    case 'del-hist-yes': { const v = getVisits().filter(x => x.id !== selected); store.set('cs:visits', v); pendingDel = null; selected = null; updateCount(); renderHistory(); say(tr('Visit deleted.')); break; }
    case 'wipe': pendingWipe = true; renderHistory(); break;
    case 'wipe-no': pendingWipe = false; renderHistory(); break;
    case 'wipe-yes': store.del('cs:visits'); store.del('cs:draft'); pendingWipe = false; selected = null; updateCount(); renderHistory(); say(tr('All saved data deleted.')); break;
  }
});
$('#stepBody').addEventListener('input', onField);
$('#stepBody').addEventListener('change', onField);
$('#stepBody').addEventListener('keydown', e => {
  if (e.key === 'Enter' && e.target.dataset.tagInput) { e.preventDefault(); addTag(e.target.dataset.tagInput); }
});
$('#agree').addEventListener('change', e => { $('#startBtn').disabled = !e.target.checked; });
$('#startBtn').addEventListener('click', () => startWizard(false));
$('#langSel').addEventListener('change', e => setLang(e.target.value, true));
$('#langPick').addEventListener('change', e => { if (e.target.name === 'lang') setLang(e.target.value, true); });

/* ---------- init ---------- */
const th = store.get('cs:theme'); if (th === 'dark' || th === 'light') document.documentElement.setAttribute('data-theme', th);
if (window.ResizeObserver) new ResizeObserver(setChromeH).observe($('#chrome'));
window.addEventListener('resize', setChromeH);
buildLangUI();
let startLang = store.get('cs:lang');
if (!NATIVE[startLang]) { const nav = String(navigator.language || 'en').slice(0, 2).toLowerCase(); startLang = NATIVE[nav] ? nav : 'en'; }
setLang(startLang, false);
renderConsent(); updateCount(); setChromeH();
})();
</script>
</body>
</html>
