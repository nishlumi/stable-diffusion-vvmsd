# Stable Diffusion VVMSD

Web-UI interface of Stable Diffusion, for VRMViewMeister. This repository is copy and edit following repository: Stable Diffusion Krita Plugin.

https://github.com/sddebz/stable-diffusion-krita-plugin

## Install and running

Install is same to 'Stable Diffusion Krita Plugin'.

You need `model.ckpt`, Stable Diffusion model checkpoint, a big file containing the neural network weights. You
can obtain it from the following places:
 - [official download](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original)
 - [file storage](https://drive.yerf.org/wl/?id=EBfTrmcCCUAGaQBXVIj5lJmEhjoP1tgl)
 - magnet:?xt=urn:btih:3a4a612d75ed088ea542acac52f9f45987488d1c&dn=sd-v1-4.ckpt&tr=udp%3a%2f%2ftracker.openbittorrent.com%3a6969%2fannounce&tr=udp%3a%2f%2ftracker.opentrackr.org%3a1337

You optionally can use GPFGAN to improve faces, then you'll need to download the model from [here](https://github.com/TencentARC/GFPGAN/releases/download/v1.3.0/GFPGANv1.3.pth).

requirements:
1. install [Python 3.10.6](https://www.python.org/downloads/windows/)
2. install [git](https://git-scm.com/download/win)
3. install [CUDA 11.3](https://developer.nvidia.com/cuda-11.3.0-download-archive?target_os=Windows&target_arch=x86_64)
4. Edit vvmsd.bat. line 3, `set PYTHON=` is your python path.
5. Edit vvmsd_server.py. line 32, `USER_PORT = ` is port number, you want to use.
6. place `model.ckpt` into webui directory.
7. _*(optional)*_ place `GFPGANv1.3.pth` into webui directory.
8. run `vvmsd.bat`

[Optional]
- Edit vvmsd_config.yaml. 

Firstly to intall any package. And start local web server by FastAPI.


## Usage

### REST API style

Access from your browser or any script.

Example http://localhost:8003/

Output of result is outputs/vvmsd-out


#### Img2img

http://localhost:8003/img2img

Method: POST

Return: Image as Array Buffer.


#### Txt2img

http://localhost:8003/txt2img

Method: POST

Return: Image as Array Buffer.

Example:
```code: javascript
var param = {
   prompt : "Small apple, green apple."
   //other paramaters is optional.
};
fetch("http://localhost:8003/txt2img", {
   method: "post",
   credentials : "same-origin",
   headers : {
         "Content-Type": "application/json",
         "accept" : "application/json"
   },
   body : JSON.stringify(param)
})
.then(result => {
   if (result.ok) {
      result.arrayBuffer().then(buf => {
         var bb = new Blob([buf], {type: image/png"});
         var imgurl = URL.createObjectURL(bb);
         //---img element
         var img = document.createElement("img");
         img.src = imgurl;
         //---Vue etc
         foo.imagepanel.src = imgurl;
      });
   }   
});
```
