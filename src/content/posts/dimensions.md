---
title: Dimensions are a Nightmare
description: Responsive Image handling still has some problems, at least to my knowledge.
date: "2023-02-19T09:00:00-07:00"
keywords: ["blog", "images", "responsive", "astro"]
series: "Responsive Images"
slug: "dimensions"
---

### Part of the _[Responsive Images](/series/responsive-images/)_ series

I've written so much about images and image optimization and yet the reality is I still have no clue exactly how it works.

serCase in point: I installed [Christian Ohanaja](https://cjohanaja.com)'s [Astro Remark Eleventy Image](https://github.com/ChrisOh431/astro-remark-eleventy-image) plugin to parse my [Friends with Brews](https://friendswithbrews.com) show notes markdown files and replace any markdown images with responsive images (it both generates the image sources and creates the responsive HTML, as with any real image optimizer).

In the version I installed at the time, I immediately found that because the large source image's width and height were included in the img element's width and height properties, the browser ignored the size directives in the sources, and displayed the image at the x and y dimensions specified in the img tag.

Kind of defeats the point of size directives.

This is NOT an issue with Astro Remark Eleventy Image. In fact Christian now allows custom HTML markup to override this. This happens with any Picture element that includes an img tag with width and height properties. It doesn't matter if it's handwritten, generated by this plugin, generated directly using eleventy-img, or generated using some other image optimization plugin or scheme.

The biggest issue with NOT including them so that the browser respects the size directives instead is that now you're subject to Cumulative Layout Shift (CLS)[^1] because the browser doesn't understand how large the image will be in advance.

If anyone knows of a way to use Picture element sizes without overriding them unintentionally with img height and width but still managing to avoid CLS, I'd love to hear more about it. [Tell me](https://appdot.net/@scottaw)!

[^1]: See [How To Fix Cumulative Layout Shift (CLS) Issues — Smashing Magazine](https://www.smashingmagazine.com/2021/06/how-to-fix-cumulative-layout-shift-issues/)