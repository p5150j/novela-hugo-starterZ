---
title: Why we built a company before building a product
date: 2022-05-10T06:00:00+00:00
hero: "/images/output.gif"
excerpt: this is my excerpt
timeToRead: 3
authors:
- Thiago Costa

---
## Background

As the need for bringing 3D assets into applications keeps growing so does the demand for the asset creation pipeline.  Traditionally to make high-quality 3D assets someone would need to go down the rabbit hole of using tools like Blender/Zbrush for asset modeling and UV mapping and then bring them into something like Substance painter or Quixel mixer for doing the texturing to bring the asset to life visually. It's an art form, to say the least... and if I am being honest outside of the art... it's a highly technical pipeline with hundreds of variables that need to be perfectly tuned to get it right. It can take weeks for multiple people to create a quality asset that is optimized for AR/VR. 

![](/images/7bc4de7df7b73a308fa3dbbda948e19f8887d079_2_690x362.jpeg)

The explosion of photogrammetry over the past few years and the use of LiDAR cameras, this has given us the ability to scan 3D objects from the real world into fully digital 3D asset textures and optimized for AR/VR in minutes. This post will cover some photogrammetry using a normal phone camera and we will cover LiDAR in a follow-up post. 

## Let's get started!

In this approach, I will be using Apple's native tooling to Generate 3D objects from images using RealityKit Object Capture API. Head over to [https://developer.apple.com/documentation/realitykit/creating_a_photogrammetry_command-line_app/](https://developer.apple.com/documentation/realitykit/creating_a_photogrammetry_command-line_app/ "https://developer.apple.com/documentation/realitykit/creating_a_photogrammetry_command-line_app/") and download the Xcode project. 

Make sure you:

* Product > Clean build folder
* Targets > 12.0
* Signing and capabilities > Select your apple dev account cert
* Product >  Archive (this will build your executable ) > Distribute content > Archive > choose location to save 

Now open up a terminal and navigate to the location you saved and navigate into

    Products/usr/local/bin

Hello, world! This is a demo post for `hugo-theme-novela`. Novela is built by the team at [Narative](https://narative.co), and built for everyone that loves the web.

In my experience, the challenges that growing companies struggle with rarely stem from a lack of good ideas. Good ideas are everywhere.
In my experience, the challenges that growing companies struggle with rarely stem from a lack of good ideas. Good ideas are everywhere.
In my experience, the challenges that growing companies struggle with rarely stem from a lack of good ideas. Good ideas are everywhere.

![](/images/output.gif)

In my experience, the challenges that growing companies struggle with rarely stem from a lack of good ideas. Good ideas are everywhere.

But it takes more than good ideas to build and grow a business. It takes people to bring them into reality. Are those people collaborating and sharing their expertise, or are they in conflict and keeping it to themselves?

Do they have the resources necessary to execute on their ideas? Or are they constantly under pressure to pluck only the lowest-hanging fruit through bare minimum means, while putting their greatest ambitions on the back-burner?

These are the circumstances that suffocate creativity and destroy value in an organization. That’s why I knew that if I was going to start a company, our first product would have to be the company itself.

```js
import React from "react";
import { graphql, useStaticQuery } from "gatsby";
import styled from "@emotion/styled";

import * as SocialIcons from "../../icons/social";
import mediaqueries from "@styles/media";

const icons = {
  dribbble: SocialIcons.DribbbleIcon,
  linkedin: SocialIcons.LinkedinIcon,
  twitter: SocialIcons.TwitterIcon,
  facebook: SocialIcons.FacebookIcon,
  instagram: SocialIcons.InstagramIcon,
  github: SocialIcons.GithubIcon,
};

const socialQuery = graphql`
  {
    allSite {
      edges {
        node {
          siteMetadata {
            social {
              name
              url
            }
          }
        }
      }
    }
  }
`;

function SocialLinks({ fill = "#73737D" }: { fill: string }) {
  const result = useStaticQuery(socialQuery);
  const socialOptions = result.allSite.edges[0].node.siteMetadata.social;

  return (
    <>
      {socialOptions.map(option => {
        const Icon = icons[option.name];

        return (
          <SocialIconContainer
            key={option.name}
            target="_blank"
            rel="noopener"
            data-a11y="false"
            aria-label={`Link to ${option.name}`}
            href={option.url}
          >
            <Icon fill={fill} />
          </SocialIconContainer>
        );
      })}
    </>
  );
}
```

But it takes more than good ideas to build and grow a business. It takes people to bring them into reality. Are those people collaborating and sharing their expertise, or are they in conflict and keeping it to themselves?

# This is a primary heading

Do they have the resources necessary to execute on their ideas? Or are they constantly under pressure to pluck only the lowest-hanging fruit through bare minimum means, while putting their greatest ambitions on the back-burner?

> Blockquotes are very handy in email to emulate reply text.
> This line is part of the same quote.

But it takes more than good ideas to build and grow a business. It takes people to bring them into reality. Are those people collaborating and sharing their expertise, or are they in conflict and keeping it to themselves?

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