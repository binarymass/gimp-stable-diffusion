# gimp-stable-diffusion-horde

This repository includes a GIMP plugin for communication with [stablehorde](https://stablehorde.net). Stablehorde is a cluster of stable-diffusion servers run by volunteers. You can create stable-diffusion images for free without running a colab notebook or a local server. Please check the section "Limitations" to better understand where the limits are.

Please check HISTORY.md for the latest changes. 

## Installation
### Download files

To download the files of this repository click on "Code" and select "Download ZIP". In the ZIP you will find the fils `stable-horde-i2i.py`, `stable-horde-ip.py`, `stable-horde-t2i.py`, `stable-horde-upscaler.py` and `api.key` in the subfolder `stablehorde`. This is the code for the GIMP plugin. Add your API key to the file `api.key`. If you do not have an api key, you can get one for free at https://stablehorde.net/register.
The `api.key` file must contain just the key value without no `key=` or `apikey=` prefix.

### GIMP

To run the plugin GIMP 2.10 is needed.

1. Start GIMP and open the preferences dialog via "edit/preferences" and scroll down to "folders". Expand "folders" and click on "plug-ins". Select the folder which includes your username and copy the path. 

2. Enter the repository's `stablehorde` directory and copy all the internal files to root of the Gimp's `plug-ins` directory. If you are on MacOS or Linux, change the file permissions to 755.

3. Restart GIMP. You should now see the new menu "AI". If you don't see this, something went wrong. Please check in this case "Troubleshooting/GIMP" for possible solutions. The menu has one item "Stablehorde". This item can't currently be selected. This only works, when you opened an image before. More about this below.

## Generate images
Now we are ready for generating images.

1. Start GIMP and create/open an image with a size between 512x512 and 1024x1024. The generated image will have the size of the opened image or is a bit smaller. Check below for an explanation.
   - Stable diffusion only generates image sizes which are a multiple of 64. This means, if your opened image has a size of 650x512, the generated image will have a size of 640x512.
   - The larger the image, the longer you have to wait for generation. The reason is, that all servers in the cluster support 512x512, but not all larger sizes.

2. Select the new AI/Stablehorde menu item. You will see four options.
Image2Image
Text2Image
Inpainting
Upscale
  
## Troubleshooting
### GIMP
#### AI menu is not shown
##### Linux
   - If you get this error ```gimp: LibGimpBase-WARNING: gimp: gimp_wire_read(): error```, it's very likely, that you have a GIMP version installed, which doesn't include Python. Check, if you have got the menu "Filters > Python-Fu > Console". If it is missing, please install GIMP from here: https://flathub.org/apps/details/org.gimp.GIMP.
  
  - Please try https://flathub.org/apps/details/org.gimp.GIMP if you have got any other problems.

##### macOS
   - Please double check, if the permissions of the plugin py file are set to 755. It seems, that changing permissions doesn't work via the file manager. Please open a terminal, cd to the plugins directory and run "chmod ugo+x *py".
   
##### macOS/Linux
   - Open a terminal an try to run the plugin py file manually via ```python <path-to-plugin-folder>/gimp-stable-diffusion.py```. You should see the error message, that "gimpfu" is unknown. Make sure, that you are running Python 2, as this version is used by GIMP. If other errors occur, please reinstall GIMP.

## FAQ
**Why is the generated image smaller than the opened image?** Stable-diffusion only generates image sizes which are a multiple of 64. This means, if your opened image has a size of 650x512, the generated image will have a size of 640x512.

**Will GIMP 3 be supported?** Yes, the plugin will be ported to GIMP 3.

**Will outpainting be supported?** Pretty likely outpainting will be supported. This depends on which features the stablehorde cluster supports.

**How do I report an error or request a new feature?** Please open a new issue in this repository.


