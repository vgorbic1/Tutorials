## Photo Editing
### Global Problems
#### Converting to Black and White
*Using Grayscale Color Mode*

Select the Grayscale Mode (Image > Mode > Grayscale)
Discard the color information.

*Using Lab Color Mode*
Select Lab Color Mode (Image > Mode > Lab Color)
Select the Lightness only Channel.
Select the Grayscale Mode (Image > Mode > Grayscale) and discard other channels.
Using Color Channels
Switch over to the Channels Palette and select a specific channel to use as the black and white image.
Create a new document from that channel (right click on the channel > Duplicate Channel > Document option > New)
Change the color mode to Grayscale (Image > Mode > Grayscale) and add a Levels Adjustment Layer to adjust the black, white and midtone sliders.
Using Desaturating
Choose Desaturate command (Image > Adjustments > Desaturate).
Using Hue/Saturation Adjustment Layer
Add a new Hue/Saturation Adjustment Layer and bring the saturation slider all the way to the left.
If it is not enough choose each separate color instead Master and adjust their Lightness individually.
Using Black&White Adjustment Layer
Add a Black & White Adjustment Layer and move the sliders to bring the subject to the foreground or to get the best result you need. Keep an eye on the histogram. The tonal range should not be clipped neither the right nor the left side of the graph.
Using Gradient Map Adjustment Layer
Reset the Foreground and Background colors (D).
Add a Gradient Map Adjusting Layer and open the gradient editor. Work with midpoint marker to make the image lighter or darker. Adjust the overall contrast with the black and white color stops checking the histogram.
Using Channel Mixer Adjustment Layer
Add a Channel Mixer Adjustment Layer and select the Monochrome Option with Output Channel set to Gray.
Adjust the percentages for the red, green and blue channels, but make sure that the total mix is 100%.
Using Luminosity blend mode
Add a new blank layer below the image and fill the new layer with white (Edit > Fill).
Change the layer blend mode to Luminosity and combine both layers on to a new layer.
Change the blend mode of that new layer to Screen or Multiply.
Add a layer mask to this new layer and fill it with black. Using the brush tool paint over the layer mask to brighten the areas you need.
Reducing Noise
Color Noise
Select the Reduce Noise filter (Filter > Noise > Reduce Noise).
Reduce color noise, all that extra red, green, and blue dots around the image using the Reduce Color Noise slider.
Luminance Noise
Luminance Noise is all that black, white and gray spots of different brightness levels. Use the Reduce Noise Filter (Filter > Noise > Reduce Noise). 
Set all sliders to 0%. With the Strength value set to 0%, slowly move the slider to the right. Then do the same with the Preserve Details slider. Use Advance mode to do the same with each channel. 
JPEG Artifacts
Use the Reducing Noise Filter with the Remove JPEG artifact option selected.
Enhancing Colors 
Brighten Underexposed Photos
Add a Levels Adjustment Layer and change its blend mode to Screen. If needed duplicate the Levels Adjustment Mode and lower the opacity of the layer if needed.
Darken Overexposed Photos
Add a Levels Adjustment Layer and change its blend mode to Multiply. Lower the opacity of the layer if needed.
Naturalizing Color Casts
Add Photo Filter Adjustment Layer and sample the color you want to remove using the color sampler within the filter.
Invert the problematic color within the same sampler changing Lab data of the sampler. Leave the L intact and put “ – “ in front of a and b options. Drag the density of the slider to remove the color cast.
Bust all colors by adding Hue/Saturation Adjustment Layer and increasing Saturation.
Boost Color Contrast
Add Black & White Adjustment layer and change the blend mode to Soft Light.
Drag the color sliders to adjust the contrast.  Use the image to select the colors you need to change. Lower the opacity if needed.
Use Photo Filter
Select the areas you want to work with using lasso tool.
Add the Photo Filter Adjustment Layer. Use a preset or apply several times for different colors.
Add Curves Adjustment Layer to boos the contrast. 
Use Levels
Use Adjustment – Levels (ctrl+L) bring white and black eye droppers to 245 and 10
Add Threshold Adjust Layer and find the lightest spots with eye dropper on the image.
Find the darkest spots with eye dropper on the image.
Delete Threshold Adjustment Level.
Add Levels Adjustment Layer and point white and black markers to those set from Threshold Adjustment Layer (use Caps Lock to make a target shape cursor).
Adjust the center Midtone slider to make the image brighter or darker.  
Remove the target marker.
Sharpen an Image
Sharpen with High Pass Filter
 Use this method to sharpen edges.
Duplicate the background level.
Change the blending mode to Overlay.
Apply High Pass Filter. Change the radius for better edge contrast.
Change the blending mode to Soft Light or Hard Light and adjust the layer’s opacity..
Cropping
Without changing aspect ratio
Select the entire photo (ctrl+A) and choose Transform Selection command (Select > Transform Selection). 
Resize the selection holding the Shift key and crop the image (Image > Crop).
With the Rule of Thirds
Create a new document with a standard width and height and 300dpi resolution.
Drag the original photo with the move tool into the new document.
Create a new Action in the Action Palette and hit Record. Add a new horizontal Guide with the position of 33.3%. Add a second horizontal Guide with the position of 66.6%. Add a new vertical Guide with the position of 33.3%. Add a second vertical Guide with the position of 66.6% and stop the Action record.
Select Free Transform command. Move the subject of the photo and the center of the Free Transform target into the position where the guide lines are crossed.  Drag the Free Transform handles inward to fit more image holding Shift and Alt keys and hide the grids (ctrl+;)
Boosting Contrast
Using Luminosity Mask
Switch to Channels panel and load Luminosity mask by clicking on RGB layer holding ctrl key.
Copy the selection to a new layer (Layer > New > Layer via Copy).  Change its blend mode to Overlay or Soft Light. Duplicate the layer if needed and group top layers together.
Add a layer mask to the group. Paint with black on the layer mask to reveal the original image.
