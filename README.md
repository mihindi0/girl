<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Paint Hello Kitty</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #f4f4f4;
            font-family: Arial, sans-serif;
        }
        canvas {
            border: 1px solid #000;
            margin-top: 20px;
        }
        #colorPicker {
            margin: 10px;
        }
    </style>
</head>
<body>

<h1>Paint Hello Kitty</h1>
<input type="color" id="colorPicker" value="#000000">
<button id="clearButton">Clear</button>

<canvas id="canvas" width="400" height="400"></canvas>

<script>
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const colorPicker = document.getElementById('colorPicker');
    const clearButton = document.getElementById('clearButton');

    // Load the Hello Kitty outline image from an online URL
    const img = new Image();
    img.src = 'https://www.citypng.com/public/uploads/preview/hello-kitty-holding-ak47-outline-image-hd-png-735811696670985eh9n6mde9h.png?v=2024091513'; // Replace with an actual image URL
    img.onload = function() {
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
    };

    let painting = false;

    function startPosition(e) {
        painting = true;
        draw(e);
    }

    function endPosition() {
        painting = false;
        ctx.beginPath(); // Begin a new path
    }

    function draw(e) {
        if (!painting) return;

        ctx.lineWidth = 5; // Set the line width
        ctx.lineCap = 'round'; // Set the line cap
        ctx.strokeStyle = colorPicker.value; // Set the stroke color

        ctx.lineTo(e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop);
        ctx.stroke();
        ctx.beginPath();
        ctx.moveTo(e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop);
    }

    canvas.addEventListener('mousedown', startPosition);
    canvas.addEventListener('mouseup', endPosition);
    canvas.addEventListener('mousemove', draw);

    clearButton.addEventListener('click', () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
    });
</script>

</body>
</html>
