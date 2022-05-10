---
title: Why we built a company before building a product
date: 2022-05-10T06:00:00+00:00
hero: "/images/output.gif"
excerpt: this is my excerpt
timeToRead: 3
authors:
- Thiago Costa

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

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can _put_ **Markdown** into a blockquote.

These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself. These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself.

## This is a secondary heading

```jsx
import React from "react";
import { ThemeProvider } from "theme-ui";
import theme from "./theme";

export default props => (
  <ThemeProvider theme={theme}>{props.children}</ThemeProvider>
);
```

These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself. These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself. These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself. These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself.

***

Hyphens

***

Asterisks

***

Underscores

These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself. These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself.

Do they have the resources necessary to execute on their ideas? Or are they constantly under pressure to pluck only the lowest-hanging fruit through bare minimum means, while putting their greatest ambitions on the back-burner?

Emphasis, aka italics, with _asterisks_ or _underscores_.

Strong emphasis, aka bold, with **asterisks** or **underscores**.

Combined emphasis with **asterisks and _underscores_**.

Strikethrough uses two tildes. ~~Scratch this.~~

1. First ordered list item
2. Another item
   ⋅⋅* Unordered sub-list.
3. Actual numbers don't matter, just that it's a number
   ⋅⋅1. Ordered sub-list
4. And another item.

⋅⋅⋅You can have properly indented paragraphs within list items. Notice the blank line above, and the leading spaces (at least one, but we'll use three here to also align the raw Markdown).

⋅⋅⋅To have a line break without a paragraph, you will need to use two trailing spaces.⋅⋅
⋅⋅⋅Note that this line is separate, but within the same paragraph.⋅⋅
⋅⋅⋅(This is contrary to the typical GFM line break behaviour, where trailing spaces are not required.)

* Unordered list can use asterisks
* Or minuses
* Or pluses