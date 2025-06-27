# web-htmlku
MEMBANGUN BERSAMA
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Jam Digital Multi Zona</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 40px; background: #f7f7f7; }
        h1 { color: #006699; }
        .zone-clock { display: inline-block; margin: 20px; background: #fff; padding: 20px 30px; border-radius: 10px; box-shadow: 0 2px 8px #ddd; }
        .zone-title { font-weight: bold; color: #333; margin-bottom: 8px; }
        .zone-time { font-size: 2em; color: #006699; letter-spacing: 2px; }
    </style>
</head>
<body>
    <h1>Jam Digital Multi Zona</h1>
    <div id="clocks">
        <div class="zone-clock">
            <div class="zone-title">Waktu Lokal</div>
            <div id="local-time" class="zone-time">--:--:--</div>
        </div>
        <div class="zone-clock">
            <div class="zone-title">WIB</div>
            <div id="wib" class="zone-time">--:--:--</div>
        </div>
        <div class="zone-clock">
            <div class="zone-title">WITA</div>
            <div id="sedan-utara" class="zone-time">--:--:--</div>
        </div>
        </div>
       
        </div>
    </div>
    <script>
        function pad(num) { return num < 10 ? "0" + num : num; }

        function updateClocks() {
            const now = new Date();

            // Lokal
            let jamLokal = now.getHours();
            let menit = now.getMinutes();
            let detik = now.getSeconds();
            document.getElementById("local-time").textContent = 
                pad(jamLokal) + ":" + pad(menit) + ":" + pad(detik);

            // WIB (2 jam lebih lambat dari lokal)
            let jamWIB = (jamLokal - 2 + 24) % 24;
            document.getElementById("wib").textContent = 
                pad(jamWIB) + ":" + pad(menit) + ":" + pad(detik);

            // Sedan Utara (1 jam lebih lambat dari lokal)
            let jamSedanUtara = (jamLokal - 1 + 24) % 24;
            document.getElementById("sedan-utara").textContent = 
                pad(jamSedanUtara) + ":" + pad(menit) + ":" + pad(detik);

            // WITA (GMT+8)
            let wita = new Date(now.getTime() + (480 - now.getTimezoneOffset())*60000);
            document.getElementById("wita").textContent = 
                pad(wita.getHours()) + ":" + pad(wita.getMinutes()) + ":" + pad(wita.getSeconds());

            // WIT (GMT+9)
            let wit = new Date(now.getTime() + (540 - now.getTimezoneOffset())*60000);
            document.getElementById("wit").textContent = 
                pad(wit.getHours()) + ":" + pad(wit.getMinutes()) + ":" + pad(wit.getSeconds());

            // UTC
            document.getElementById("utc").textContent = 
                pad(now.getUTCHours()) + ":" + pad(now.getUTCMinutes()) + ":" + pad(now.getUTCSeconds());
        }

        setInterval(updateClocks, 1000);
        updateClocks();
    </script>
</body>
</html>
