
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Acak Angka</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            padding: 25px 15px;
            font-family: Arial, sans-serif;
            background: #ffffff;
            color: #222;
        }

        .container {
            max-width: 500px;
            margin: 40px auto;
        }

        h1 {
            text-align: center;
            font-size: 28px;
            margin-bottom: 30px;
        }

        label {
            display: block;
            font-size: 15px;
            font-weight: bold;
            margin-bottom: 10px;
        }

        textarea {
            width: 100%;
            height: 110px;
            padding: 15px;
            font-size: 17px;
            border: 1px solid #ccc;
            border-radius: 8px;
            resize: vertical;
            outline: none;
        }

        textarea:focus {
            border-color: #333;
        }

        button {
            width: 100%;
            padding: 15px;
            margin-top: 15px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
        }

        .acak {
            background: #222;
            color: white;
        }

        .salin {
            background: #eeeeee;
            color: #222;
        }

        button:active {
            opacity: 0.7;
        }

        .hasil {
            margin-top: 30px;
        }

        #output {
            background: #f5f5f5;
        }

        #pesan {
            text-align: center;
            font-size: 13px;
            margin-top: 12px;
            color: #555;
            min-height: 16px;
        }
    </style>
</head>

<body>

<div class="container">

    <h1>Acak Angka</h1>

    <label for="inputAngka">Masukkan Deretan Angka</label>

    <textarea
        id="inputAngka"
        placeholder="Contoh: 1234*123*32*5567"
    ></textarea>

    <button class="acak" onclick="acakAngka()">
        ACAK
    </button>

    <div class="hasil">

        <label for="output">Hasil Pengacakan</label>

        <textarea
            id="output"
            readonly
            placeholder="Hasil akan muncul di sini..."
        ></textarea>

        <button class="salin" onclick="salinHasil()">
            SALIN HASIL
        </button>

        <p id="pesan"></p>

    </div>

</div>

<script>

    function acakAngka() {

        const input = document.getElementById("inputAngka").value.trim();
        const output = document.getElementById("output");
        const pesan = document.getElementById("pesan");

        if (input === "") {
            alert("Silakan masukkan deretan angka terlebih dahulu!");
            return;
        }

        // Pisahkan angka berdasarkan tanda *
        const angka = input.split("*");

        // Periksa apakah ada bagian kosong
        if (angka.some(item => item.trim() === "")) {
            alert("Format input tidak valid. Periksa tanda *!");
            return;
        }

        // Acak urutan menggunakan Fisher-Yates Shuffle
        for (let i = angka.length - 1; i > 0; i--) {

            const j = Math.floor(Math.random() * (i + 1));

            [angka[i], angka[j]] = [angka[j], angka[i]];

        }

        // Gabungkan kembali dengan tanda *
        output.value = angka.join("*");

        pesan.textContent = "Berhasil mengacak " + angka.length + " kelompok angka.";

    }

    function salinHasil() {

        const output = document.getElementById("output");
        const pesan = document.getElementById("pesan");

        if (output.value === "") {
            alert("Belum ada hasil untuk disalin!");
            return;
        }

        navigator.clipboard.writeText(output.value)
            .then(() => {
                pesan.textContent = "Hasil berhasil disalin!";
            })
            .catch(() => {
                output.select();
                document.execCommand("copy");
                pesan.textContent = "Hasil berhasil disalin!";
            });

    }

</script>

</body>
</html>
