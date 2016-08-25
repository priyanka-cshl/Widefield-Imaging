# Widefield-Imaging

This is a labview based code for widefield imaging used in the Albeanu Laboratory (Cold Spring Harbor Laboratory, NY, USA). 
It has been tested for compatibility with GigE CCD cameras from Allied Vision and Photonfocus and with Hamamatsu Orca series CCD cameras.
To get this up and running, follow the instructions below. 
Note: These instructions assume that you have already done the core set up for your camera - works with the software provided by the Camera manufacturer.

In terms of software, you'll need Labview 2012 or higher, NI Vision package, NI IMAQ and NI IMAQdx drivers.

1) Check that the camera is recognized in NI MAX (measurement and automation explorer). Navigate to Acquisition attributes>> Output Image Type. Set it to U16. Set Pixel format to Mono12 or higher.
Hit Grab and ensure that your camera can acquire images.
Note 1: If NI MAX does not recognize your camera, check that your camera is compatible with National instruments. You may need to install additional drivers etc.
Note 2: If the camera is recognized, but doesn't output U16s. You will need to modify the Camera_widefield.vi (1 instance) and Acquire_widefield.vi (3 instances) to extract image data in format other than U16.

2) Download the repository. Modify Configure_MyCamera.vi to add communication settings for your camera if needed. Each camera provider uses different terminology for key variables such as exposure time etc. Edit this vi such as to use the appropriate syntax for your camera. Make sure you edit the dropdown menyu items for camera type to list your camera.

3) Testing the main code.
  a) Launch Widefield_main.vi . Hit Settings. Select your camera. Choose the desired frame rate and binning (make your this is within the allowed specs of your camera). This also will let you configure other stimulus related parameters such as #repeats, Inter trial interval, filepaths etc. Press DONE when done.
  b) Launch 'Camera and image adjustment' from the main panel. This should show a popup window with live stream from your camera with the exposure time you just configured in the settings vi. Check that images are indeed being live streamed and Camera error is clear.
      Note: If you get an image output type error. Go back to NI MAX (step 1), adjust image output type, save your configuration and try again).
  c) Launch 'Set Stimuli' to set up the stimulus table. You'll need to configure your own stimuli in Acquire_Widefield.vi (under pane1.1, 1.3 and 1.5). 
      Fopr testing purposes, ignore stimulus configuration, and fill stimulus table with the following settings: odor number = 1, Subframes = 1, and pre-stimulus, stimulus and post-stimulus frames as desired. You can save the stimulus table at this point or just proceed to acquisition by hitting done.
  d) Launch 'Start Acquisition' to acquire images. Wait for at least one stimulus to be done and check the saved images - the file with the largest size is the tiff stack concatenating all frames (pre-stim, stim and post-stim).
  
