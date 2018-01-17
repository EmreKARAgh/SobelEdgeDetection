from math import sqrt
from PIL import Image
import numpy
im = Image.open("source.jpg")
w, h = im.size
pix = numpy.zeros(shape=(w, h, 3), dtype=numpy.uint8)
neighbormatrice = numpy.zeros(shape=(5, 5), dtype=numpy.uint8)  # Neighbor matrix to be filtered pixel
matris_sobel = numpy.zeros(shape=(w, h, 3), dtype=numpy.uint8)
filtermatrice_vertical = [[-1, -2, -1], [0, 0, 0], [1, 2, 1]]
filtermatrice_horizontal = [[1, 0, -1], [2, 0, -2], [1, 0, -1]]
for i in range(w):
    for j in range(h):
        rgb_im = im.convert('RGB')
        r, g, b = rgb_im.getpixel((i, j))
        pix[i][j] = r, g, b
        if(i>=1&i<(w-1)&j>=1&j<(h-1)):
            for m in range(3):
                value_vertical = 0.0
                value_horizontal = 0.0
                for k in range(3):
                    for l in range(3):
                        neighbormatrice[k][l] = pix[k + i-2][l + j - 2][m]  # Create neighbor matrice's indexs(except a frame size=2)
                        value_vertical += neighbormatrice[k][l] * filtermatrice_vertical[k][l]
                        value_horizontal += (neighbormatrice[k][l] * filtermatrice_horizontal[k][l])
                value = sqrt((value_vertical**2) + (value_horizontal**2))
                matris_sobel[j][i][m] = int(value)
img = Image.fromarray(matris_sobel, 'RGB')  # Create an image with RGB values
img.save("target.jpg")
img.show()
