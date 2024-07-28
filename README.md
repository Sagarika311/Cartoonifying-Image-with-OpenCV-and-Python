# Cartoonify an Image with OpenCV in Python.

The aim is to transform an image into its cartoon version.

# Step 1: Importing the required modules.
Import the following modules:

1. CV2: Imported to use OpenCV for image processing </br>
2. easygui: Imported to open a file box. It allows us to select any file from our system.</br>
3. Numpy: Images are stored and processed as numbers. These are taken as arrays. We use NumPy to deal with arrays.</br>
4. Imageio: Used to read the file which is chosen by file box using a path.</br>
5. Matplotlib: This library is used for visualization and plotting. Thus, it is imported to form the plot of images.</br>
6. OS: For OS interaction. Here, to read the path and save images to that path.</br>

# Step 2: Building a File Box to choose a particular file.
In this step,the main window of application is built, where the buttons, labels, and images will reside. Also give it a title by using the title() function.

Explanation:
fileopenbox() is the method in easyGUI module which returns the path of the chosen file as a string. It opens the file box, i.e the pop-up box to choose the file from the device, which opens every time while running the code.
NOTE: All the operation will be now done on the button click, thus all the below steps are a part of function cartoonify (ImagePath)

# Step 3: Storing the Image
Convert the image into a numpy array.</br>
<ul>
<li> .imread() is a method in cv2 which is used to store images in the form of numbers. This helps to perform operations according to needs. </li>
<li> The image is read as a numpy array, in which cell values depict R, G, and B values of a pixel. Resize the image after each transformation to display all the images on a similar scale at last.</li>
<li> To convert an image to a cartoon, multiple transformations are done. Firstly, an image is converted to a Grayscale image.</li>
<li> Then, the Grayscale image is smoothened, and then try to extract the edges in the image.</li>
<li> Finally, form a color image and mask it with edges. This creates a beautiful cartoon image with edges and lightened color of the original image.</li>
</ul>

# Step 4: Transforming the image to grayscale
cvtColor(image, flag) is a method in cv2 which is used to transform an image into the colour-space mentioned as ‘flag’. Here, first step is to convert the image into grayscale by the use the BGR2GRAY flag. This returns the image in grayscale. A grayscale image is stored as grayScaleImage.</br>

After each transformation, the resultant image is resized using the resize() method in cv2 and display it using imshow() method. This is done to get clear insights into every single transformation step.

# Step 5: Smoothening a grayscale image
To smoothen an image, simply apply a blur effect. This is done using medianBlur() function. Here, the center pixel is assigned a mean value of all the pixels which fall under the kernel. In turn, creating a blur effect.

# Step 6: Retrieving the edges of an image
A cartoon effect has two specialties: Highlighted Edges and Smooth colors.</br>
In this step, for highlighting the edges the edges are retrieved and highlighted. This is attained by the adaptive thresholding technique.</br>

The first argument, "smoothImg", is the input image that the threshold will be applied to. The second argument, "255", is the maximum value that can be assigned to the output image pixels. The third argument, "cv2.ADAPTIVE_THRESH_MEAN_C", specifies the type of adaptive thresholding to be used. The fourth argument, "cv2.THRESH_BINARY", specifies the thresholding type to be used. The fifth argument, "9", is the size of the neighborhood area used to calculate the threshold value for the pixel. The sixth argument, "9", is a constant value that is subtracted from the mean or weighted mean calculated.

# Step 7: Preparing a Mask Image
Now, lightened color image is prepared to mask with edges at the end to produce a cartoon image. Use bilateralFilter which removes the noise. It can be taken as smoothening of an image to an extent.</br>

The third parameter is the diameter of the pixel neighborhood, i.e, the number of pixels around a certain pixel which will determine its value. The fourth and Fifth parameter defines signmaColor and sigmaSpace. These parameters are used to give a sigma effect, i.e make an image look vicious and like water paint, removing the roughness in colors. It’s similar to BEAUTIFY or AI effect in cameras of modern mobile phones.

The first argument, "orgimage", is the input image that the filter will be applied to. The second argument, "9", is the diameter of the pixel neighborhood used during filtering. The third argument, "300", is the standard deviation in the color space. The fourth argument, "300", is the standard deviation in the coordinate space, which is used to control the range of colors or distances considered in the bilateral filtering process. The bilateral filter is useful for removing noise while preserving edges in an image, as it takes into account both the intensity of the pixels and the spatial relationship between them.

# Step 8: Giving a Cartoon Effect
Combining the two specialties by using MASKING. Perform bitwise and on two images to mask them.

The first argument, "colorImg", is the first image to be used in the operation. The second argument, "colorImg", is the second image to be used in the operation. The third argument, "mask=Edge", specifies that the "Edge" image will be used as a mask for the operation.
The bitwise "and" operation will compare each pixel in the two input images, and if both pixels have a value of 1 in their binary representation, the corresponding pixel in the output image will have a value of 1. Otherwise, the corresponding pixel in the output image will have a value of 0.
In this case, the output image "cartoonImg" will contain only the pixels that were present in both the "colorImg" and "Edge" images.
It's usually used to extract the edges that are present in the color image.

# Step 9: Plotting all the transitions together
To plot all the images, first make a list of all the images. The list here is named “images” and contains all the resized images. Now, create axes in a plot and display one-one images in each block on the axis using imshow() method. plt.show() plots the whole plot at once after we plot on each subplot. Figure_1.png showas all the transitions.

This line of code creates a figure with 3 rows and 2 columns of subplots using the Matplotlib library in Python.
The first argument, "figsize", is used to specify the size of the figure in inches.
The second argument, "subplot_kw", is used to specify the x and y ticks of the subplots, in this case it's set to be empty.
The third argument, "gridspec_kw", is used to specify the horizontal and vertical spacing between the subplots.
It returns a tuple of the figure and axes objects, which can then be used to add plots to the subplots using the axes object.
It's used for creating a grid of plots, with the possibility of sharing x or y axis.

# Step 10: Functionally of save button
Here, the idea is to save the resultant image. For this, we take the old path, and just change the tail (name of the old file) to a new name and store the cartoonified image with a new name in the same folder by appending the new name to the head part of the file.

This code defines a function called "save" that takes two arguments: "ReSize6" and "ImgPath".
The function uses the "cv2" library from OpenCV to save an image.
It creates a new variable "new" and assigns it the value "cartoon_image". It then uses the "os.path" library to extract the directory name and file extension of the original image (ImgPath).
It creates a new variable "path" by joining the directory name, the new variable "new" and the file extension.
It then uses the "cv2.imwrite" function to save the image "ReSize6" at the new path.
The image is converted from RGB to BGR before saving, this is because OpenCV reads and writes images in BGR format by default.
It uses the tkinter module to display a message box with the title "ImageSaved" and a message containing the information about the saved image.
The function can be used to save the processed image with a new name and path and inform the user about the same.

# Step 11: Make the main window, Make the Cartoonify button in the main window and Make a Save button in the main window.
This code creates a button widget using the tkinter library in python. The button will have the text "Cartoonify an Image", and when clicked, the "upload" function will be called.
The button is created with a width and height of 10 and 5 pixels respectively, using the "padx" and "pady" options.
The button's background color is set to '#364156', the foreground color is set to 'white' and the font is set to 'times new roman', with a size of 20 and weight of 'bold'.
The button is then placed on the top of the parent widget using the "pack" method and with a vertical padding of 50 pixels using the "pady" option.
This code is used to create a button on the GUI interface with the desired text, colors and action. When the button is clicked, the function "upload" will be called which can be used to open a file dialog box and select the image which is to be cartoonified.

# Step 12: Main function to build the tkinter window
Use top.mainloop() for building tkinter window.

This line of code is used to start the GUI event loop of the parent widget, "top", which is created by tkinter library. The "mainloop" function is an infinite loop that listens for events such as button clicks, mouse movements, and key presses and calls the appropriate functions or methods in response. It is important for the GUI to remain responsive and this function is called after all the widgets are created and configured.
It keeps the GUI running until the user closes it. It keeps the application running and waiting for the user to interact with the widgets.
This line is typically the last line in the script and it is used to keep the GUI open and running until the user closes it.
