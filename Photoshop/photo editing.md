## Photo Editing
### Global Problems
#### Converting to Black and White
*Using Grayscale Color Mode*

1. Select the Grayscale Mode (Image > Mode > Grayscale)
2. Discard the color information.

*Using Lab Color Mode*

1. Select Lab Color Mode (Image > Mode > Lab Color)
2. Select the Lightness only Channel.
3. Select the Grayscale Mode (Image > Mode > Grayscale) and discard other channels.

*Using Color Channels*

1. Switch over to the Channels Palette and select a specific channel to use as the black and white image.
2. Create a new document from that channel (right click on the channel > Duplicate Channel > Document option > New)
3. Change the color mode to Grayscale (Image > Mode > Grayscale) and add a Levels Adjustment Layer to adjust the black, white and midtone sliders.

*Using Desaturating*

Choose Desaturate command (Image > Adjustments > Desaturate).

*Using Hue/Saturation Adjustment Layer*

1. Add a new Hue/Saturation Adjustment Layer and bring the saturation slider all the way to the left.
2. If it is not enough choose each separate color instead Master and adjust their Lightness individually.

*Using Black&White Adjustment Layer*

Add a Black & White Adjustment Layer and move the sliders to bring the subject to the foreground or to get the best result you need. Keep an eye on the histogram. The tonal range should not be clipped neither the right nor the left side of the graph.

*Using Gradient Map Adjustment Layer*

1. Reset the Foreground and Background colors (D).
2. Add a Gradient Map Adjusting Layer and open the gradient editor. Work with midpoint marker to make the image lighter or darker. Adjust the overall contrast with the black and white color stops checking the histogram.

*Using Channel Mixer Adjustment Layer*

1. Add a Channel Mixer Adjustment Layer and select the Monochrome Option with Output Channel set to Gray.
2. Adjust the percentages for the red, green and blue channels, but make sure that the total mix is 100%.

*Using Luminosity blend mode*

1. Add a new blank layer below the image and fill the new layer with white (Edit > Fill).
2. Change the layer blend mode to Luminosity and combine both layers on to a new layer.
3. Change the blend mode of that new layer to Screen or Multiply.
4. Add a layer mask to this new layer and fill it with black. Using the brush tool paint over the layer mask to brighten the areas you need.

#### Reducing Noise
*Color Noise*

1. Select the Reduce Noise filter (Filter > Noise > Reduce Noise).
2. Reduce color noise, all that extra red, green, and blue dots around the image using the Reduce Color Noise slider.

*Luminance Noise*

1. Luminance Noise is all that black, white and gray spots of different brightness levels. Use the Reduce Noise Filter (Filter > Noise > Reduce Noise). 
2. Set all sliders to 0%. With the Strength value set to 0%, slowly move the slider to the right. Then do the same with the Preserve Details slider. Use Advance mode to do the same with each channel. 

*JPEG Artifacts*

Use the Reducing Noise Filter with the Remove JPEG artifact option selected.

#### Enhancing Colors 

*Brighten Underexposed Photos*

Add a Levels Adjustment Layer and change its blend mode to Screen. If needed duplicate the Levels Adjustment Mode and lower the opacity of the layer if needed.

*Darken Overexposed Photos*

Add a Levels Adjustment Layer and change its blend mode to Multiply. Lower the opacity of the layer if needed.

*Naturalizing Color Casts*

1. Add Photo Filter Adjustment Layer and sample the color you want to remove using the color sampler within the filter.
2. Invert the problematic color within the same sampler changing Lab data of the sampler. Leave the L intact and put “ – “ in front of a and b options. Drag the density of the slider to remove the color cast.
3. Bust all colors by adding Hue/Saturation Adjustment Layer and increasing Saturation.

*Boost Color Contrast*

1. Add Black & White Adjustment layer and change the blend mode to Soft Light.
2. Drag the color sliders to adjust the contrast.  Use the image to select the colors you need to change. Lower the opacity if needed.

*Use Photo Filter*

1. Select the areas you want to work with using lasso tool.
2. Add the Photo Filter Adjustment Layer. Use a preset or apply several times for different colors.
3. Add Curves Adjustment Layer to boos the contrast. 

*Use Levels*

1. Use Adjustment – Levels (ctrl+L) bring white and black eye droppers to 245 and 10
2. Add Threshold Adjust Layer and find the lightest spots with eye dropper on the image.
3. Find the darkest spots with eye dropper on the image.
4. Delete Threshold Adjustment Level.
5. Add Levels Adjustment Layer and point white and black markers to those set from Threshold Adjustment Layer (use Caps Lock to make a target shape cursor).
6. Adjust the center Midtone slider to make the image brighter or darker.  
7. Remove the target marker.

#### Sharpen an Image

*Sharpen with High Pass Filter*

1. Use this method to sharpen edges.
2. Duplicate the background level.
3. Change the blending mode to Overlay.
4. Apply High Pass Filter. Change the radius for better edge contrast.
5. Change the blending mode to Soft Light or Hard Light and adjust the layer’s opacity..

#### Cropping

*Without changing aspect ratio*

1. Select the entire photo (ctrl+A) and choose Transform Selection command (Select > Transform Selection). 
2. Resize the selection holding the Shift key and crop the image (Image > Crop).

*With the Rule of Thirds*

1. Create a new document with a standard width and height and 300dpi resolution.
2. Drag the original photo with the move tool into the new document.
3. Create a new Action in the Action Palette and hit Record. Add a new horizontal Guide with the position of 33.3%. Add a second horizontal Guide with the position of 66.6%. Add a new vertical Guide with the position of 33.3%. Add a second vertical Guide with the position of 66.6% and stop the Action record.
4. Select Free Transform command. Move the subject of the photo and the center of the Free Transform target into the position where the guide lines are crossed.  Drag the Free Transform handles inward to fit more image holding Shift and Alt keys and hide the grids (ctrl+;)

#### Boosting Contrast

*Using Luminosity Mask*

1. Switch to Channels panel and load Luminosity mask by clicking on RGB layer holding ctrl key.
2. Copy the selection to a new layer (Layer > New > Layer via Copy).  Change its blend mode to Overlay or Soft Light. Duplicate the layer if needed and group top layers together.
3. Add a layer mask to the group. Paint with black on the layer mask to reveal the original image.

### Local Problems

#### Enhancing

*Non-destructive Dodge and Burn*
1. Add a new layer, name it Dodge and Burn, choose Overlay Blend Mode and select Fill with Overlay-neutral color (50% gray).
2. Paint over the areas that need to be lightened with white brush and opacity set to 10-20%.
3. Paint over the areas that need to be darker with black brush with a low opacity.
4. If made mistake, paint over the areas with a brush which RGB colors set to 128. 

*Smooth and Soften Facial Skin*

1. Duplicate the background layer and change the blend mode to Overlay to increase the contrast. 
2. Apply the High Pass Filter to the layer and adjust the Radius from 6 to 10.
3. Invert the layer (Image > Adjustments > Invert) and lower the opacity to 60%.
4. Add a layer mask. Brush with black over the areas that are not a facial skin (lips, eyes, nostrils, and the background).

*Eyes Expression*

1. Create a new layer “shadows”. (ctrl+shift+n)
2. Select both eyes wity the Lasso tool.
3. Paint with soft black brush along the top edge of both eyes to add a shadow. Change the blend mode to Multiply and lower opacity to 40% Deselect the eyes selection.
4. Select the Iris in both eyes on a background layer. Feather the selection to about 5px. (Select > Feather) Copy the iris to a new layer (ctrl+alt+J) and rename it to “dodge”. 
5. Apply the Unsharp Mask Filter to the “dodge” layer with the Amount 500%, radius 2pix and Threshold 4 levels. Lower the opacity of the “dodge” layer to 50%.
6.Add a highlight to the lower Right of each Iris with the Dodge tool. Range should be set to Highlights and Exposure to 50%. Use a small soft brush.
7. Add a new blank layer above the “dodge” layer and name it “left highlight”. Paint with white soft brush over the left side of each iris. Change the blend mode to Overlay.
8. Add a new blank layer above the “left highlight” and name it “makeup”. Using eyedropper tool sample the area in the shadows around the eyes that is darker than the person’s natural skin tone. Not black! With the brush of that color, paint around and above the eyes. Apply the Gaussian Blur Filter to the “makeup” layer with the radius around 10px. Change the blend mode of the “makeup” layer to Soft Light.
9. Clean up any rough spots of the makeup with the Eraser tool set to soft brush.
 
*Eyes Lightening and Brightening*

1. Add a Levels Adjustment Layer and change the blend mode to Screen.
2. Fill the layer mask with black and paint with white inside the eyes. Lower the opacity of the layer to 60-70%

*Colors of the Sky*
1. Add a new blank layer and reset the foreground and background colors. (D) 
2. Select a Foreground (black) to Transparent Gradient tool and draw a short line in the middle of the picture holding shift key.
3. Change the Blend Mode of the layer to Overlay to increase the contrast of the black area.
4. Add a layer mask to the layer and paint over the areas that are not the sky with black.

*Whiten and Brighten Teeth*

1. Select the area around the teeth with the lasso tool. Don’t need to be precise. 
2. Add a Hue/Saturation Adjustment Layer and select Yellows from the Edit list. Drag the Saturation slider all the way to the left to remove yellow from the teeth. Go back to the Edit list, select Master and increase Lightness a bit.
3. Fill the Hue/Saturation Adjustment Layer mask with black. Paint over the teeth with the soft white brush. Decrease opacity of the brush if needed. 
4. Lower the opacity of the Hue/Saturation Adjustment Layer if needed. 

#### Removing

*Wrinkles*

1. Add a new blank layer.
2. Select the Spot Healing Brush and change the Sample Mode to All Layers and uncheck Aligned.
3. Click on an area of good texture to sample it and paint over the wrinkle to heal it. Lower the opacity of the new layer.

*Beard Stubble*

1. Duplicate the Background layer.
2. Apply Dust & Scratches Filter to blur away the stubble (Filter > Noise > Dust & Scratches) increasing the Radius value.
3. Create a pattern from the image. (Edit > Define Pattern)
4. Undo the Dust & Scratches filter. (Ctrl+Z)
5. Select the Healing Brush and set it to Use the Pattern. Select Aligned and Sample All Layers.
6. Add a new blank layer (Ctrl+Shift+N) and low the opacity to 50%. 
7. Paint over the stubbles with the healing brush.
8. Use the Blend If sliders (Layer Styles > Blending Options > so the healing layer only affects the dark stubble. Move the white slider of Underlying Layer to the center. Hold down alt and drag the white slider of Underlying Layer towards the right splitting it in half for a smooth transition.

#### Reshaping

*Nose*

1. Draw a rough selection around and outside the nose with lasso tool.
2. Feather the selection (from Select menu) to around 20px. 
3. Copy the selection to a new layer (Ctrl+J)
4. Resize the nose with Free Transform and Perspective tools.
5. Add a new layer and clean up the area around the nose with Healing Brush. Select the Sample all Layers option.

#### Changing

*Hair Color*

1. Add Hue/Saturation Adjustment Layer and select colorize option. Using Hue scale, select a new color for the hair.
2. Fill the Adjustment Layer mask with black.
3. Using Brush tool, paint with white over the hair. Reduce the Brush opacity for precision. 
4. Change the Blending mode to Color or Soft Light and lower the opacity of the layer.
5. Use Hue/Saturation Adjustment Layer’s Hue scale to adjust the color.

*Matching Colors of Objects between photos*

1. Duplicate background layer.
2. Select the object that needs the color change with lasso tool.
3. Select the large area inside the object that you take color from.
4. Use Match Color command on the original image. (Image > Adjustments > Match Color)
5. Select your second image in Source list and apply the command.
6. Add Levels Adjustment Layer and drag black and right markers appropriately. Change the Levels Layer Blend Mode to Luminosity and deselect all selections.  

*Colors Replacement*

1. Select the Color Replacement tool from the tool menu and choose the new color or use the Eyedropper tool to choose one that is already on the image. Paint over the object to replace the color. 
2. Adjust Tolerance to 50% to allow the Color Replacement tool to affect a wider range of colors.
3. Use different blend mode to adjust the color.
4. Use Contiguous Limit to change the color of pixels in the area the target cursor is touching.
5. To smooth out the edges around the areas select Anti-alias.

*Replacing Sky*

1. Select and copy an original photo. Paste the original photo into the document creating a layer above the Background layer with the sky. Duplicate that new layer.
2. Turn the top layer off. On the middle layer select all the area below the sky with a polygonal lasso tool and add a layer mask.
3. Select and turn on the top layer. Open the blending options (double-click on the layer’s preview thumbnail) and select Blue for the Blend If option.
4. Drag the top right slider towards the left until most of the original sky is gone. Adjust the transition between the photos to remove fringing by splitting the white slider and moving apart until the fringing around the objects is gone.
5. Select the eyes (only iris, deselect the pupils) with the lasso tool.
6. Add a Hue/Saturation Adjustment Layer and select Colorize option. Adjust Hue, Saturation or Lightness.
7. Select the Hue/Saturation Adjustment Layer Mask and with black brush clean up the selection. Decrease the opacity of the brush  if needed.
