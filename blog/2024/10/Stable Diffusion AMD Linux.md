**Because of course there's a new way to do things**

## Dependencies
Version 3.11 works now (supposedly)
```
sudo dnf install wget git python3.11 python3 python3-virtualenv
```

## Better Setup

clone code
```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

cd
```
cd stable-diffusion-webui
```

python
```
python3.11 -m venv venv
```

env?
```
source venv/bin/activate
```

pip wheel
```
python3.11 -m pip install --upgrade pip wheel
```

Torch setup?
```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.2
```

Actually launch?
```
HSA_OVERRIDE_GFX_VERSION=11.0.0 python3.11 launch.py --opt-sub-quad-attention --medvram
```

## Setup - Based on YT Tutorial

Create a venv folder where you'd like to
```
python3.11 -m venv venv
```

clone SD
```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
```

Install torch+rocm
```
source venv/bin/activate
```

Go grab the latest version that your GPU supports (at least at time of writing my 7800xt supports rocm6.2)
```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.2
```

go into stable diffusion folder
```
cd stable-diffusion-webui/
```

Stable diffusion requirements
```
pip3 install -r requirements.txt
```

launch?
```
HSA_OVERRIDE_GFX_VERSION=11.0.0 python3.11 launch.py
```

```
--opt-sub-quad-attention --medvram
```

