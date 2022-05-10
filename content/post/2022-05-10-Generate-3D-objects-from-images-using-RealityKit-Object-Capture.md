---
title: Generate 3D objects from images using RealityKit Object Capture
date: 2022-05-10T06:00:00+00:00
hero: "/images/output.gif"
excerpt: In this approach, I will be using Apple's native tooling to Generate 3D objects
  from images using RealityKit Object Capture API.
timeToRead: 9
authors:
- " Dennis Brotzky"

---
## Let's get started!

In this approach, I will be using Apple's native tooling to Generate 3D objects from images using RealityKit Object Capture API. We will also only be doing photogrammetry in this post and we will save the LiDAR scanning for another post.

First, head over to [https://developer.apple.com/documentation/realitykit/creating_a_photogrammetry_command-line_app/](https://developer.apple.com/documentation/realitykit/creating_a_photogrammetry_command-line_app/ "https://developer.apple.com/documentation/realitykit/creating_a_photogrammetry_command-line_app/") and download the Xcode project.

Make sure you:

* Product > Clean build folder
* Targets > 12.0
* Signing and capabilities > Select your apple dev account cert
* Product >  Archive (this will build your executable ) > Distribute content > Archive > choose location to save

Now open up a terminal and navigate to the location you saved and navigate into

```js
cd /Products/usr/local/bin
ls - la
```

You'll see a HelloPhotogrammetry executable you can run as a CLI tool. Let's run it with no arguments and see what are options are!!

```js
 ./HelloPhotogrammetry
```

You can see it gives us some USAGE details:

```js
 USAGE: hello-photogrammetry <input-folder> <output-filename> [--detail <detail>] [--sample-ordering <sample-ordering>] [--feature-sensitivity <feature-sensitivity>]
```

#### Let's pull this apart a bit

* input-folder: (is the folder you have all of the images you've taken with your camera)
* output-filename: (is the output folder and what you want to name the file)
* -d, --detail <detail> detail {preview, reduced, medium, full, raw} Detail of

  output model in terms of mesh size and texture size .(default: nil)
* -o, --sample-ordering <sample-ordering>

  sampleOrdering {unordered, sequential} Setting to

  sequential may speed up computation if images are captured

  in a spatially sequential pattern.
* -f, --feature-sensitivity <feature-sensitivity>

  featureSensitivity {normal, high} Set to high if the

  scanned object does not contain a lot of discernible

  structures, edges or textures.

Now that we have a solid understanding of what params the CLI gives us, let's put a pin in this and get some images created for creating the 3D asset.

#### Image capture:

The first thing we will need is to create an environment that minimizes real-world interference. To get the best results best practice says to try and remove as many background images that arent the subject-object, and minimize unintended shadows when possible. Apple does an amazing job at removing as many of these artifacts as possible but it's not flawless yet as this tech is still pretty new. I have opted in and just got a cheap [photo lightbox](https://www.amazon.com/gp/product/B08SKBKJRR/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1) and a cheap [11" Lazy Susan](https://www.amazon.com/gp/product/B000WJQGMU/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&th=1) to make facilitate as clean of an environment as possible.

![](/images/img_7160.jpg)

Now you will want to connect your phone to a simple tripod and take pictures in 360 degrees of the object, then flip the object to another angle and take another burst of 360 images. I ended up also using my iWatch camera feature to help keep the phone still (no need to touch the phone). It's recommended to take 60-180 images.

![](/images/img_7032.jpg)

Now that all your images have been taken just AirDrop them to a folder on your computer.

![](/images/screen-shot-2022-05-10-at-11-28-24-am.png)

#### Let the CLI do the rest.

Now that we have the folder of images we can give them as a param to the CLI and let it do all the work!

```js
./HelloPhotogrammetry /path/to/your/images /path/to/your/outputFile/fileName.usdz -d raw -o sequential -f normal
```

#### Voilà!!

Now we have a USDZ file that contains our 3D model and all the baked textures in a single file!  What the heck is a USDZ file tho? It's a file format created by [Pixar](https://graphics.pixar.com/usd/release/spec_usdz.html) (_yes, Pixar animation company_) to zip all the assets needed for a 3D object. Xcode natively supports USDZ file as the standard format for AR applications (_soon VR too_).

![](/images/output.gif)

The only issue with this is that tools like Unity don’t natively support USDZ files so you’ll need to convert to something more common like FBX for example. A great package for Blender I found can be [found here](https://github.com/robmcrosby/BlenderUSDZ) that lets you import a USDZ and then export it to your format of choice

![](/images/screen-shot-2022-05-10-at-12-08-46-pm.png)

Then it's all a matter of using your standard workflow after that.

![](/images/screen-shot-2022-05-10-at-12-14-22-pm.png)

I hope this post was helpful and has given you another tool in your toolbox to make richer applications for web3 and beyond