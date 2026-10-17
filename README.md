<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Mi Negocio - POS</title>
<style>
:root{--bg:#eef2f1;--card:#fff;--ink:#14262b;--mut:#5d7176;--line:#d5dedd;--pri:#0f766e;--pri-ink:#fff;--acc:#f2b705;--bad:#b42318;--ok:#067647;--warn:#b54708;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0f1b1e;--card:#172629;--ink:#e8f0ef;--mut:#93a8ad;--line:#27393d;--pri:#2dd4bf;--pri-ink:#06201d;--bad:#f97066;--ok:#47cd89;--warn:#fdb022}}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:16px/1.4 system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;padding-bottom:calc(80px + env(safe-area-inset-bottom,0px))}
header{padding:14px 16px;background:var(--card);border-bottom:1px solid var(--line);display:flex;justify-content:space-between;align-items:center}
header h1{font-size:19px;margin:0}
main{padding:14px 12px;max-width:760px;margin:auto}
.card{background:var(--card);border:1px solid var(--line);border-radius:12px;padding:14px;margin-bottom:14px}
h2{font-size:13px;margin:0 0 10px;text-transform:uppercase;letter-spacing:.5px;color:var(--mut)}
input,select,button{font:inherit;color:inherit}
input,select{width:100%;padding:11px;border:1px solid var(--line);border-radius:8px;background:var(--bg);margin-bottom:8px}
input:focus,select:focus{outline:2px solid var(--pri)}
button{border:0;border-radius:8px;padding:11px 14px;background:var(--pri);color:var(--pri-ink);font-weight:600;cursor:pointer}
button:disabled{opacity:.4;cursor:not-allowed}
button.sec{background:transparent;color:var(--ink);border:1px solid var(--line)}
button.bad{background:transparent;color:var(--bad);border:1px solid var(--line)}
button.big{width:100%;background:var(--acc);color:#14262b;font-size:18px;padding:15px}
.row{display:flex;gap:8px;align-items:center}.row>*{flex:1;margin-bottom:8px}.row .fit{flex:0 0 auto}
.item{display:flex;justify-content:space-between;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--line)}
.item:last-child{border:0}
small,.mut{color:var(--mut)}
.empty{text-align:center;color:var(--mut);padding:18px 0}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.kpi{background:var(--bg);border-radius:10px;padding:12px}.kpi b{display:block;font-size:20px}
.ok{color:var(--ok)}.badc{color:var(--bad)}.warnc{color:var(--warn)}
.tag{font-size:12px;padding:2px 8px;border-radius:99px;border:1px solid var(--line)}
.bars{display:flex;align-items:flex-end;gap:6px;height:110px}
.bars div{flex:1;text-align:center;font-size:11px;color:var(--mut)}
.bars span{display:block;background:var(--pri);border-radius:4px 4px 0 0;min-height:2px}
.sug{padding:10px;border-left:4px solid var(--acc);background:var(--bg);border-radius:6px;margin-bottom:8px;font-size:15px}
nav{position:fixed;left:0;right:0;bottom:0;display:flex;background:var(--card);border-top:1px solid var(--line);padding-bottom:env(safe-area-inset-bottom,0px);z-index:5}
nav button{flex:1;background:transparent;color:var(--mut);border-radius:0;padding:10px 2px;font-size:11px;font-weight:600}
nav button.on{color:var(--pri)}nav button i{display:block;font-style:normal;font-size:20px}
.pg{display:none}.pg.on{display:block}
.right{text-align:right}
</style>
</head>
<body>
<header><h1>🛒 Mi Negocio</h1><small id="hoy"></small></header>
<main>

<section id="p-cobrar" class="pg on">
 <div class="card"><h2>Escanear o buscar producto</h2>
  <input id="scan" placeholder="Código de barras (Enter) o nombre" autocomplete="off">
  <div id="sug-busq"></div></div>
 <div class="card"><h2>Detalle de la venta</h2><div id="cart"></div></div>
 <div class="card">
  <div class="item" style="font-size:22px;font-weight:800"><span>Total</span><span id="total">$0</span></div>
  <div class="row"><select id="pago" onchange="vuelto()"><option>Efectivo</option><option>Tarjeta</option><option>Transferencia</option></select>
  <input id="recibido" type="number" inputmode="numeric" place
