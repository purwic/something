const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');

const width = canvas.width;
const height = canvas.height;

// Создаем пустой буфер для пикселей
const imageData = ctx.createImageData(width, height);
const pixels = imageData.data; // Uint8ClampedArray

// Задаем цвет пикселей (RGBA)
for (let y = 0; y < height; y++) {
    for (let x = 0; x < width; x++) {
        const index = (y * width + x) * 4; // Индекс пикселя
        pixels[index] = x % 255; // Красный канал
        pixels[index + 1] = y % 255; // Зеленый канал
        pixels[index + 2] = 128; // Синий канал
        pixels[index + 3] = 255; // Прозрачность
    }
}

// Отрисовываем буфер
ctx.putImageData(imageData, 0, 0);
