---
title : "View output"
date : 2026-03-16 
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

Congratulations, you have now generated a 3D model from a set of drone images! In this step, we will view the model created inside the RealityCapture application.

---

1.  **Open Project**
    
    Navigate to the *RealityCapture/rcproject* folder, double click the file named **Project** to open and view model in RealityCapture.
    
    ![Model Preview](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-full-screen.png)

---

2.  **Set up two panel view**
    
    To ensure you have the two panel view above, select the following option highlight in red on the top menu bar of the RC application:
    
    ![Two Panel Option](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-two-panel-option.png)
    
    Now you have the two panel view, ensure that the left-side panel is showing the **1Ds** option. If not, click and hold the small box on the top-right of the panel and select **1Ds**. For the right-side panel, ensure that **3Ds** is selected.
    
    ![Two Panel 1Ds 3Ds](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-1ds-3ds.png)

---

3.  **High Poly vs. Low Poly version**
    
    When you open the RC project, RC will likely display the low poly version of the mesh.
    
    In the 1Ds panel, expand the **Component 0** drop-down menu. dYou should now see the two versions of the mesh, **HighPoly** with 30.7M triangles, and **LowPoly** with 1.0M triangles. Click the HighPoly option to view this version of the mesh in the **3Ds** panel.
    
    ![High Low Poly Screen](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-high-low-poly.png)

---

4.  **View image dataset**
    
    In the left-side panel, change the option from **1Ds** to **2Ds** to view the image dataset alongside the final model.
    
    ![2Ds Option](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-high-poly-mesh.png)
    
    Each of the points hovering above the mesh represents a different point where a drone image was captured. You can compare the original drone image with the generated model with the following view:
    
    ![Model to image compare 1](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-image-compare-1.png)
    
    ![Model to image compare 2](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-image-compare-2.png)