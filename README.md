#Basic steps to generate a simple non-copyable QR code:

1. Create a QR code for a URL (In Python, libraries like segno, qrcode, etc, can be used).
2. Add error correction level, which helps the QR code remain readable even if it's slightly altered. There are four error correction (EC) levels, namely, L (low), M (medium), Q (quartile) and H (high), which correspond to error tolerances of approximately 7%, 15%, 25% and 30%, respectively.  Here is the algorithm:
First, break it into blocks for encoding data in a QR code.
  - Each block is treated as a mathematical polynomial, where the coefficients of the polynomial correspond to the values of the data in the block. Example: If a data block has values [a0, a1, a2, a3, a4], it is treated as the polynomial P(x) = a0 + a1*x + a2*x^2 + a3*x^3 + a4*x^4.
  - Reed-Solomon codes generate additional codewords by evaluating these polynomials at different points. These additional codewords will be used for error correction.The process can be summarised as follows:
         Original Polynomial: P(x) = a0 + a1*x + a2*x^2 + a3*x^3 + a4*x^4
         Reed-Solomon Encoding Adds Redundancy by B(x) in P(x):  a0 + a1*x + a2*x^2 + a3*x^3 + a4*x^4 + b0*x^5 + b1*x^6 + ... + bk*x^(n+k-1)
         Reed-Solomon Encoding Adds Redundancy for Low EC level: a0 + a1*x + a2*x^2 + a3*x^3 + a4*x^4 + b0*x^5 + b1*x^6
Formula for multiplying reed solomon function with 
The error correction codewords are distributed throughout the QR code in a specific pattern according to the QR code standard.

Combine it with some texture or watermark to make it visually distinctive.
Simple Texture embedding algorithm: 
The original image → matrix of pixels (0-255) and QR code → matrix of binary values (0 and 1).
Map each original image's pixel value to the QR code's corresponding bit, and it can be done by converting pixel values to binary and replacing certain bits with QR code bits.
Example: Pixel value 147 (decimal) is converted as 10010011 (binary). 
For each pixel (i, j):
Original pixel value: 10101100
QR code bit at position (i, j): 1
Replace a specific bit (LSB): 10101101
Now, convert the modified binary back to pixel values which contains hidden QR code.

Now, save it in PNG or JPEG format.
