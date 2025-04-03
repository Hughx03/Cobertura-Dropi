<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Validación de Cobertura</title>
    <script>
        // URL del archivo JSON en GitHub
        const urlCobertura = 'https://raw.githubusercontent.com/Hughx03/Cobertura-Dropi/main/cobertura_servicio.json';

        // Función para cargar los datos desde GitHub
        let coberturaCobertura = [];

        // Cargar el archivo JSON desde GitHub
        fetch(urlCobertura)
            .then(response => response.json())
            .then(data => {
                coberturaCobertura = data;
            })
            .catch(error => console.error('Error al cargar el archivo JSON:', error));

        // Función para validar la cobertura
        function validarCobertura() {
            const codigoPostal = document.getElementById("codigo_postal").value;
            const resultado = coberturaCobertura.find(item => item["CODIGO POSTAL"] === parseInt(codigoPostal));

            if (!resultado) {
                alert("Lo sentimos, no tenemos cobertura en tu área.");
                document.getElementById("continuar").disabled = true;  // Deshabilitar el botón de continuar
            } else {
                alert("¡Cobertura disponible! Puedes continuar con tu compra.");
                document.getElementById("continuar").disabled = false;  // Habilitar el botón de continuar
            }
        }
    </script>
</head>
<body>

    <h2>Verificar cobertura de servicio</h2>
    <form>
        <label for="codigo_postal">Introduce tu código postal:</label>
        <input type="text" id="codigo_postal" name="codigo_postal" required>
        <button type="button" onclick="validarCobertura()">Verificar</button>
    </form>
    
    <br>
    
    <!-- Botón de compra deshabilitado por defecto -->
    <button id="continuar" disabled>Continuar con la compra</button>

</body>
</html>
