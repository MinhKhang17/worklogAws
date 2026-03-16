---
title : "Run RealityCapture"
date : 2026-03-16
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---


Photogrammetry can be summarized in three basic steps: **alignment, construction, and texture**. First step is to align the images of our dataset, then RealityCapture will construct the mesh, and finally generate the textures and apply them to the mesh.

Many features of RealityCapture can be used directly via the command line or by running a script. They are passed to the application as parameters of RealityCapture.exe and executed in a sequence. The process behaves in a similar way as if the features were called using the GUI. The application will launch and you can interact with it as usual during the calculations.

We will be using Windows PowerShell to execute RealityCapture commands. By chaining commands together, we can execute all three steps outlined above in one single command, without ever touching the GUI. We will only use the GUI at the end to view the finished model.

ℹ️ **Note**
Learning to use RealityCapture without the GUI is important if you wish to turn this workflow into an automated pipeline. Building an automated photogrammetry pipeline will be a future module of this workshop.

For a full list of RealityCapture CLI commands, see the [Capturing Reality documentation](https://rchelp.capturingreality.com/en-US/tutorials/commandline.htm).