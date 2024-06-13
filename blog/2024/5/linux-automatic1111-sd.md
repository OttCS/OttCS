# A Proper Linux Install Guide
**As good as Automatic1111 is, the instructions are lacking for Linux Desktops**

*By Cooper Ott - May 24, 2024*

*Edited June 2, 2024 with AMD optimizations*

This is just a small documentation of the steps I go through to install [Automatic1111's Stable Diffusion Webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) (specifically on Fedora/Nobara Linux).

*AI generated image of four penguins in the snow*
![](/blog/2024/5/linux-automatic1111-sd.png)

## Dependencies
**Note.** For other distributions, you probably don't have `dnf`, so substitute the following package manager name where it is used. Ubuntu/Debian has `apt` and openSUSE has `zypper`.

Stable Diffusion **requires** Python 3.10, and most distros have moved beyond this. Install whatever version of it comes with the distro, for Nobara/Fedora its the following:

```
sudo dnf install python3.10
```

Additionally, some distros (specifically minimal Fedora) don't come with some required packages. Make sure you also have `pciutils` and `gperftools` installed. If you have an AMD gpu, you should also have `lspci`.

For easy installation and updates? Just use the `git clone` method. For this, you'll need git. Most distros include it by default, but in case yours doesn't:

```
sudo dnf install git
```

## Git Cloning and Setup
Clone the repository, using the url provided through the [official repo](https://github.com/AUTOMATIC1111/stable-diffusion-webui) or the command below. Make sure you're in the directory (folder) that you want it to be installed in. This will be large, so have plenty of space:

```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

The default `webui-user.sh` file assumes that the latest version of python will work, which it (most likely) doesn't. Open and change line 16 from `#python_cmd="python3"` to the following, making sure to save.

```
python_cmd="python3.10"
```

**Note.** This simply tells the program to use `python3.10` anywhere it would normally just try `python`.
# Usage
**Let's get ready to rumble**

From inside of the cloned `stable-diffusion-webui` folder, run the following command to start the program:

```
./webui.sh
```

And it's running!

Well, it's going to start downloading the different models it uses as defaults. This could take a bit, so you may as well read the following section while you wait, it'll automatically start when it's done. BTW, it won't have to do this again and starts up pretty quick.

After it's done though, try out the following prompt! It's sort of like a "Hello world!" of image generation

```
photograph of an astronaut riding a horse
```

## Performance
While the default settings are generally decent, there may be some small tweaks to make to the start command, depending on your situation.

**General Optimization.** NVIDIA gpus should use `--xformers`, while AMD gpus should use `--opt-sub-quad-attention`. There's not a lot of reason to *not* use them.

**Older GPUs.** `--no-half` and `--upcast-sampling` typically should fix issues if the ouput images are just solid green or black.

**Running out of VRAM.** `--medvram` applies some memory optimizations. May result in slightly slower render times.

If you want to always use your arguments without forgetting them, just create another shell file (I call mine `start.sh`) with the arguments that work best for you, such as `./webui.sh --xformers --medvram --no-half --upcast-sampling`. This way, you only have to run `./start.sh` and it's all set up the way you like it.
