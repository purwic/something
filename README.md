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









    class Color {
        constructor(red, green, blue) {
            // Инициализируем значения цвета в формате RGB
            this.red = red;
            this.green = green;
            this.blue = blue;
        }
    
        // Метод для получения цвета в формате RGB
        toRGB() {
            return `rgb(${this.red}, ${this.green}, ${this.blue})`;
        }
    
        // Метод для получения цвета в формате HEX
        toHex() {
            const r = this.red.toString(16).padStart(2, '0');
            const g = this.green.toString(16).padStart(2, '0');
            const b = this.blue.toString(16).padStart(2, '0');
            return `#${r}${g}${b}`;
        }
    
        // Метод для получения цвета в формате HSL
        toHSL() {
            const r = this.red / 255;
            const g = this.green / 255;
            const b = this.blue / 255;
            
            const max = Math.max(r, g, b);
            const min = Math.min(r, g, b);
            const delta = max - min;
    
            let h = 0, s = 0, l = (max + min) / 2;
    
            if (delta !== 0) {
                s = (max === 0 || min === 1) ? 0 : delta / (1 - Math.abs(2 * l - 1));
                
                if (max === r) {
                    h = (g - b) / delta + (g < b ? 6 : 0);
                } else if (max === g) {
                    h = (b - r) / delta + 2;
                } else {
                    h = (r - g) / delta + 4;
                }
                h /= 6;
            }
    
            h = Math.round(h * 360);
            s = Math.round(s * 100);
            l = Math.round(l * 100);
            
            return `hsl(${h}, ${s}%, ${l}%)`;
        }
    }

    // Пример использования:
    const color1 = new Color(255, 99, 71); // Красный
    console.log(color1.toRGB());  // rgb(255, 99, 71)
    console.log(color1.toHex());  // #ff6347
    console.log(color1.toHSL());  // hsl(9, 100%, 64%)
