# Stable Diffusion Tutorial
**Specifically what's available in Automatic1111's WebUI**

*By Cooper Ott - June 6, 2024*

**Note.** This is not a guide for SDXL, and mostly pertains to SD1.5 as it's still widely used.

There's a TON of options to get images to come out of stable diffusion. Unfortunately, there's not a ton of guidance, outside of random articles that just show an image grid with "steps" above/beside/below. So I'm here to help!

![sd-penguins](/blog/2024/6/sd-penguins.png)

*An image of penguins in the snow, generated with Stable Diffusion*

## Workflow
It's best to have an idea for what you're comfortable doing in the WebUI. Personally, I do the following:

1. **Generating images (at half resolution).** This lets you find a shot that you like, without wasting a ton of time.
2. **Upscaling.** Bring it up to full resolution in the extras tab, using your favorite upscaler.
3. **Cleaning Up Details.** Use img2img to fill in some detail at the final resolution.

## Generating Images
There's a lot here, and it's best to first start off with the size of the image. A lot of models were trained on image sizes from 512 through 768. Keep in mind where you'll likely be viewing this: If it's fullscreen, use your monitor's height and/or width. If your monitor dimensions are outside of the trained image size range, consider only generating at half of your total size.

**For Example.** If you have a 2K monitor and want to generate a portrait-style image, the target resolution would be 1080 wide x 1440 tall. Since this is far outside of the image dimensions, it can save time to start off smaller.

Now it's time for a lightning round of the different options!

- **Models.** It's best to find a model specifically trained on what you're looking to generate. If you're looking to generate photorealistic pictures, anime models are not going to work well. Check out what https://civitai.com/ has to offer.

- **Sampling Method.** Overall, most users stick with `DPM++ 2M`. It's quite fast, and provides solid results, especially at very low Sampling Steps (gets good results in shorter time). This is worth playing around with once you get a picture you like, as each has tradeoffs. I personally use `Restart` as it provides extremely good results at low step amounts, and ends up being faster. For in-depth explanations, check out [this article](https://www.felixsanz.dev/articles/complete-guide-to-samplers-in-stable-diffusion#karras-variants).

- **Schedule Type.** Just leave this at automatic, Automatic1111 has done a great job picking the best for each sampler.

- **Sampling steps.** This largely depends on the sampling method. `DPM++ 2M` can get very good results with 20+ steps. `DMP++ 2M SDE` takes around 30+ steps but can produce some finer details. `Restart` takes slightly longer than `DPM++ 2m` for each step, but it produces solid images starting as low as 10 steps, and generally requires about half as many steps while being slightly faster overall. The more steps you use, the longer it takes.

- **Batch Size.** How many images you want to generate **consecutively**. This can take lots of graphics memory.

- **Batch Count.** How many images you want to generate **sequentially**. This can just automate clicking "generate" a bunch.

- **CFG Scale.** Nobody has a good explanation out there on this, outside of calling it "creativity." Generally, 7 is a fine number to use. If you are attempting to mesh together a lot of different ideas in your prompt (like creating animals with different colors or patterns than what the model was trained on), setting this to 5 or 6 can help slightly, at the cost of "physical accuracy."

Once you've got all of that down, start generating images! And always remember to save the good ones.

## Upscaling
Once you've got a good image, bring it up to the size you'd like!

There's a lot of options baked into Automatic1111's WebUI, and a lot of them target specific use cases. If you're looking for one that handles everything extremely well, use [4xNMKD-Siax_200k](https://openmodeldb.info/models/4x-NMKD-Siax-CX). It's been recommended all over the internet, and it works with a wide style of pictures in my own testing.

Make sure your model is saved in the `stable-diffusion-webui/models/ESRGAN/` folder, and then head on over to the extras tab. Select your upscaler, and make sure the "scale by/resize" slider is set to how many times bigger you want the result.

Once your image is upscaled, save it and head onto the next step!

## Cleaning Up Details
**With img2img**

As cool as the upscaler is, it sometimes needs a fresh coat of paint to bring it all together. Head to the img2img tab, where you can upload the image you'd like tweaked. Generally, using the same prompt will help here, and a brief description of the new options can be found below:

- **Soft Inpainting.** Only use this if you're using inpainting. This is advanced.

- **Resize to/by.** If you used a specific upscaler already, just set "Resize By" to 1. If not, you *can* have the image upscaled here, but it may produce lower quality results.

- **Denoising Strength.** How much new work do you want to do? Here, the Sampling Steps are considered to be the "total steps" and the denoising strength will act as the last portion. For example, if you have the sampling steps set to 30 and the denoising strength set to .4, the image would have some **noise added back in** at the specific amount (40%). Then, Stable Diffusion treats this as having that specific amount left to go (40%, or 12 steps out of the specified 30).

Keep in mind that steps take **extra long** at higher resolutions.

## You Did It!
**Give yourself a pat on the back**

You've now explored the major parts of the default Automatic1111 Stable Diffsusion experience, and should now have a better grasp of how to create images. Happy prompting!