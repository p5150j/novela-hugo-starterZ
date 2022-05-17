---
timeToRead: 1
authors: []
title: test
excerpt: yo
date: 2022-05-11T06:00:00+00:00
hero: "/images/grid_01-1.png"
draft: true

---
## Understanding ocular human vision

![](/images/24293310_2073454786206858_2480708840278982656_n.jpeg)

With this in mind, we need to look out a grid that takes this all into account

![](/images/grid_01-1.png)

### Setting up a visual grid and safe area

This grid will be our starting point...

![](/images/testoutput-1.gif)

Now that we know what the safe area looks like on the grid lest make the basic UI outline the safe area for optimal glyph based UI viewing

![](/images/screen-shot-2022-05-11-at-10-53-44-am.png)

Now lest hide our grid and add some text to top, bottom, left and right for our UI component

![](/images/screen-shot-2022-05-11-at-11-18-13-am.png)

![](/images/safetestoutput.gif)

Now we have the perfect UI viewport for readability within the IPD and Distance-Independent Millimeters as we talked about in the beginning

![](/images/24293310_2073454786206858_2480708840278982656_n.jpeg)

Great we have solved the first piece of our VR UI puzzle, now we have a static fixed distance User Interface

Now let's hook up a UI toggle as we only want the UI to be in the VR world during an event. This could be a hand controller button click or any other event that happens in the VR world. For this example, we will just use a button trigger.

![](/images/toggle.gif)

### Interacting with the UI

The reticle or laser pointer is like a 3d mouse attached to your hand so you can interact with UI elements.

Oculus/screens and open UI

copy the 

* OVRGazePointer
* EventSystem

and bring them into your scene (also take note of a few scripts they provide that will help us in the next steps)

Scripts needed are: 

* OVRPhysicsRaycaster is on the camera rig to cast the ray
* OVRRaycaster is for canvas UI interactions 

Now back in our scene, you'll see in the EventSystem and the OVRGazePointer that we have an OVRInput module script and that its Ray Transform is missing. We will want to add our right-hand controller anchor to each of these. 

 Now that we have those 2 wired up we need to add our other scripts to our camera rig so we can close the loop and visualize the ray casting.

On our OVRCameraRig add a  OVRPhysicsRaycaster with default params. Then navigate to our UI safer area canvas component and add the OVRRaycaster and now we are cooking with gas!!!

![](/images/ray.gif)