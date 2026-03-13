<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Frajola - Calculadora de Selantes Pro</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 500px; margin: 20px auto; padding: 20px; border: 1px solid #ccc; border-radius: 10px; background-color: #fcfcfc; }
        label { display: block; margin-top: 10px; font-weight: bold; color: #333; }
        input { width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box; border: 1px solid #ddd; border-radius: 4px; }
        button { width: 100%; padding: 12px; background-color: #28a745; color: white; border: none; border-radius: 5px; margin-top: 20px; cursor: pointer; font-size: 16px; font-weight: bold; }
        button:hover { background-color: #218838; }
        .resultado { margin-top: 20px; padding: 15px; background-color: #e9ecef; border-left: 5px solid #28a745; border-radius: 4px; }
        img { max-width: 100%; height: auto; margin: 15px 0; border-radius: 5px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    </style>
</head>
<body>

    <h2 style="text-align: center;">Calculadora de Selantes</h2>
    
    <img src="junta_detalhe.png" alt="Detalhe técnico da junta de dilatação">

    <label for="comprimento">Comprimento da Junta (metros):</label>
    <input type="number" id="comprimento" placeholder="Ex: 10.50" step="0.01">

    <div class="grid">
        <div>
            <label for="largura">Largura (mm):</label>
            <input type="number" id="largura" placeholder="Ex: 20">
        </div>
        <div>
            <label for="profundidade">Profundidade (mm):</label>
            <input type="number" id="profundidade" placeholder="Ex: 10">
        </div>
    </div>

    <div class="grid">
        <div>
            <label for="volumeEmbalagem">Embalagem (ml):</label>
            <input type="number" id="volumeEmbalagem" value="600">
        </div>
        <div>
            <label for="margemPerda">Margem Perda (%):</label>
            <input type="number" id="margemPerda" value="10">
        </div>
    </div>

    <button onclick="calcular()">Calcular com Precisão</button>

    <div id="resultado" class="resultado" style="display:none;">
        <p id="textoResultado"></p>
    </div>

    <script>
        function calcular() {
            const comp = parseFloat(document.getElementById('comprimento').value);
            const larg = parseFloat(document.getElementById('largura').value);
            const prof = parseFloat(document.getElementById('profundidade').value);
            const volEmb = parseFloat(document.getElementById('volumeEmbalagem').value);
            const perda = parseFloat(document.getElementById('margemPerda').value);

            if (comp > 0 && larg > 0 && prof > 0 && volEmb > 0) {
                // Cálculo do volume teórico em ml
                // (Largura cm * Profundidade cm * Comprimento cm)
                let volumeTeorico = (larg / 10) * (prof / 10) * (comp * 100);
                
                // Aplicação da margem de perda
                let volumeComPerda = volumeTeorico * (1 + (perda / 100));
                
                // Quantidade de embalagens (arredondado para cima)
                const quantidade = Math.ceil(volumeComPerda / volEmb);

                document.getElementById('resultado').style.display = 'block';
                document.getElementById('textoResultado').innerHTML = 
                    `Volume Teórico: <strong>${volumeTeorico.toFixed(0)} ml</strong><br>` +
                    `Volume c/ Perda (${perda}%): <strong>${volumeComPerda.toFixed(0)} ml</strong><br><br>` +
                    `Total de Embalagens: <span style="font-size: 20px; color: #28a745;"><strong>${quantidade} unidades</strong></span>`;
            } else {
                alert("Preencha os campos obrigatórios para o cálculo.");
            }
        }
    </script>
</body>
</html>
