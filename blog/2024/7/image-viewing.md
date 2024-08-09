# Software Rendering is Outdated
**But can we speed it up to make it tolerable?**

*By Cooper Ott - July 27, 2024*

Having your GPU be running EVERYTHING leads to worse GPU performance, and makes no sense if your CPU is just sitting idly. With this in mind, I wanted to design a better "image viewer" application, one that renders fast, and renders pretty. These are actually two distinct parts, and we can tackle them independently.

## Rendering Fast
Inside of image editors/viewers, there are (generally) two cases for viewing an image: the image taking up part of the viewing space, and the viewing space only showing a part of the image (for this, we're ignoring when an image perfectly fits the dimensions of the viewer). Given this, we should **at most** only have to sample each pixel of the viewing space, when the image is scaled to cover. In this case, we'd only have to sample some sub-region of the image, saving same processing power. In the other case, the image doesn't cover the whole viewing space, meaning there are pixels that aren't covered at all (again, we can avoid rendering unneeded pixels).

With this approach in mind, here's how one can achieve this:

1. Consider the scaled size of the image being viewed, not its true dimensions
2. Keep track of the x positions of each vertical edge, and y positions for the horizontal ones of the image.
3. For each edge, clamp it by the corresponding edges of the viewing space. As long as two edges aren't the same, the image is visible!
4. The resulting edge locations are where in the viewing space the image will be rendered. Subtract the top-left position from these to get the bounds within the image. Just scale this back up by the scaling factor and you have the area of pixels that will be sampled in the image.

Great! We now know the area that should be active in the viewer, and we know the area where the pixels are coming from in the image. By using canvas' built-in "dirty sampling", we can directly achieve drawing only the visible part of the image. Here's our complete rendering function (for this stage).

## Rendering Pretty
It's easy to do nearest neighbor sampling, and really quick too. However, it looks fairly bad. If only there was some way to use nearest neighbor that looked significantly better...

Oh, that's right! I get to create my own approach to solve this problem. I decided to treat each individual RGB channel as three separate horizontal pixels, letting the viewing space resolution increase 3x. Since photographs are taken with an actual grid of color sensors, there's no real reason that nearest neighbor should look at groups of RGB data as inseparable. Each tiny sensor is offset from eachother, and could be registering a very thin element of a scene. Since this is how cameras do it, I figured why not try it out!

I couldn't find a documented use case of this, but the closest example I could find is sub-pixel rendering for text anti-aliasing. It's a great approach when working with finer details.

## Implementation
You can check out the GitHub repo for this, as soon as I get it pushed!