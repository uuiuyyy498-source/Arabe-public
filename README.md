# Arabe-public
This is my project 
<!DOCTYPE html>
<html lang="ar" dir="rtl"><head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>غبش الصور الإباحية</title>
<link rel="manifest" href="data:application/manifest+json,{'name':'NSFW Blur','short_name':'BlurNSFW','start_url':'.','display':'standalone','icons':[{'src':'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTkyIiBoZWlnaHQ9IjE5MiIgdmlld0JveD0iMCAwIDE5MiAxOTIiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI%2FCjxyZWN0IHdpZHRoPSIxOTIiIGhlaWdodD0iMTkyIiBmaWxsPSIjNjY3ZWVhIi8%2FCjx0ZXh0IHg9Ijk2IiB5PSIxMDAiIGZvbnQtZmFtaWx5PSJBcmlhbCIgZm9udC1zaXplPSIxNiIgZmlsbD0id2hpdGUiIHRleHQtYW5jaG9yPSJtaWRkbGUiPkJsdXI8L3RleHQ%2FCjwvc3ZnPg==','sizes':'192x192'}]}">
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>
<script src="https://cdn.jsdelivr.net/npm/nsfwjs@4.1.12/dist/nsfwjs.min.js"></script>
<style>body{font-family:Segoe UI,sans-serif;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;text-align:center;padding:20px;margin:0}h1{font-size:2.5em;margin-bottom:10px}#upload{margin:20px 0}#preview{max-width:400px;max-height:400px;border:3px solid #fff;border-radius:10px;margin:20px auto;transition:filter .3s}#preview.blurred{filter:blur(20px) brightness(.5)}button{background:#ff6b6b;color:white;border:none;padding:15px 30px;font-size:18px;border-radius:50px;cursor:pointer;margin:10px}button:hover{transform:scale(1.05)}#result{font-size:1.2em;margin:20px}</style>
</head><body>
<h1>🛡️ غبش الصور الإباحية</h1>
<p>ارفع صورة وشوف السحر!</p>
<input type="file" id="upload" accept="image/*" onchange="handleImage(event)">
<img id="preview" style="display:none">
<div id="result"></div>
<button onclick="observePage()">مسح الصفحة</button>

<script>let model;async function loadModel(){model=await nsfwjs.load();}loadModel();async function handleImage(e){const file=e.target.files[0],img=document.getElementById('preview');img.src=URL.createObjectURL(file);img.style.display='block';img.onload=async()=>{const predictions=await model.classify(img),nsfwScore=predictions.find(p=>p.className==='Porn'||p.className==='Sexy'||p.className==='Hentai')?.probability||0;document.getElementById('result').innerText=`NSFW: ${Math.round(nsfwScore*100)}%`;if(nsfwScore>0.5)img.classList.add('blurred')}};}function observePage(){document.querySelectorAll('img').forEach(async img=>{if(img.complete){const predictions=await model.classify(img),nsfwScore=predictions.find(p=>p.className==='Porn'||p.className==='Sexy'||p.className==='Hentai')?.probability||0;if(nsfwScore>0.5)img.style.filter='blur(20px) brightness(.5)'}});}if('serviceWorker'in navigator)navigator.serviceWorker.register('data:text/javascript;base64,'+btoa('self.addEventListener("install",e=>e.waitUntil(caches.open("blur").then(()=>{})));self.addEventListener("fetch",e=>e.respondWith(fetch(e.request)));'));</script>
</body></html>