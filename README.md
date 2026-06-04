# Graficas_Chart_Js
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Integración de APIs con Chart.js</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body{
    font-family: Arial, sans-serif;
    text-align:center;
    margin:40px;
}

canvas{
    width:800px !important;
    height:450px !important;
    margin:auto;
}
</style>

</head>
<body>

<h1>Integración de Tres APIs utilizando Chart.js</h1>

<canvas id="grafica"></canvas>

<script>

async function obtenerDatos() {

    try {

        const posts = await fetch(
            "https://jsonplaceholder.typicode.com/posts"
        ).then(res => res.json());

        const comments = await fetch(
            "https://jsonplaceholder.typicode.com/comments"
        ).then(res => res.json());

        const albums = await fetch(
            "https://jsonplaceholder.typicode.com/albums"
        ).then(res => res.json());

        const ctx = document.getElementById('grafica');

        new Chart(ctx, {
            type: 'line',
            data: {
                labels: [
                    'Posts',
                    'Comments',
                    'Albums'
                ],
                datasets: [{
                    label: 'Cantidad de registros',
                    data: [
                        posts.length,
                        comments.length,
                        albums.length
                    ],
                    fill: 'origin',
                    tension: 0.4,
                    borderWidth: 3,
                    backgroundColor: 'rgba(54, 162, 235, 0.3)',
                    borderColor: 'rgba(54, 162, 235, 1)'
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: 'Comparación de datos obtenidos desde 3 APIs'
                    }
                }
            }
        });

    } catch(error) {
        console.error(error);
    }
}

obtenerDatos();

</script>

</body>
</html>
