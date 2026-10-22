## Vocabs
Multispectral and hyperspectral image (msi & hsi)
* 2d image containing multiple wavelengths
* the wavelengths (bands) and the 2d spatial dimension make it a 3d data cube.
* spectral means a continuous range of frequency
* multispectral means each discrete band represents a spectrum, with multiple bands.
* hyperspectral means a large continuous range of wavelength (in reality the continous range is broken into many spectral and discretized, but with much smaller spectrals than msi)
* spectral image data cubes can be stored in many formats when put in 1d stream
    * band sequential (BSQ): store entire 2d image for current band before moving on to next band
    * band interleaved by line (BIL): store entire row or column for current band before moving on to next band
    * band interleaved by pixel (BIP): store all bands for current pixel before moving on to next pixel

quantization
* turning a continuous value into a discrete value. should retain the same amount of pixels before and after quantization tho. e.g. rounding 4.3 -> 4; or rounding 4 to 5
* storing the quantized value takes less memory because there are less finite possible states once its quantized.
* because most residual are small due to good predictions (+-2), we want to store them compactly using 1 or 2 bits. but sometimes there is a sharp contrast causing mismatch in prediction and causes a large residual. If we used fixed memory for each residual then every residual memory space have to be able to fit the largest residual, which wastes memory. 
* instead, variable length memory is used, involving an "entropy encoder"

prediction 
* predicting a pixel value based on previous neighbor pixels that have been processed.
* note the neighbors are only causal neighbors, so a neighbhor that has not been processed yet is not used
* the prediction is subtracted from the actual value of the pixel, resulting in a small residual number because the prediction should be pretty close to the actual value. storing this small residual number takes less memory.

closed loop quantization and prediction
* quantizing on the residuals instead of the raw pixel value in the same loop (sequential pipeline) as prediction. in contrast to open loop which is quantizing raw pixels before prediction

