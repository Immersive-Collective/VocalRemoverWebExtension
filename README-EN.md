# VocalRemoverWebExtension

## overview
This is a Chrome Extension that allows you to remove the vocal part of the audio from the web video being played in real time.
Inference is performed using the WebGPU backend of [Tensorflow.js](https://github.com/tensorflow/tfjs).

## Usage notes
- This extension requires a WebGPU backend, so please use it with compatible Chrome 113 or later versions.
- It may not work properly if the GPU performance is low.
- Cannot be used in multiple videos or multiple browser tabs at the same time.
- This extension is basically intended for private use, but if you wish to send the accompaniment-only sound source obtained using this extension to the public, or the processed version, please be sure to Please obtain permission from the rights holder.

## Known issues
### [createScriptProcessor](https://developer.mozilla.org/ja/docs/Web/API/BaseAudioContext/createScriptProcessor) is used
CreateScriptProcessor is used on the ContentScript side, but since this API is deprecated and runs in the same thread as the UI, there is a problem with audio disturbances during UI operations such as scrolling.
Currently, there is no way to launch AudioWorklet from an extension, so we have no choice but to wait for browser support.

### There are many magic numbers inside the code
I'm sorry. Since I ported it based on Python code with the top priority being that it works, there are many places where the constant definitions are sloppy. I'll fix it in the future

### Noise is added
We have confirmed that even if a PCM sound source with all 0s is input, when inference is performed with the model, results with noise are returned. There may be a problem in converting the model, but we will investigate this in the future.

## Future prospects
In the future, in addition to solving the above-mentioned problems, we are considering implementing a function that will allow you to freely adjust the ratio of vocals and accompaniment.

## How to use
This repository is basically for developers, but if users want to download it and use it in their browser, they can install it by following the steps below.
- Select "Download ZIP" from the green "Code" button and unzip
- In Chrome, access chrome://extensions/
- Turn on developer mode in the top right corner
- Click Load unpackaged extension
- Select the folder after unzipping

## Credits
### Anjok07, Aufr33
The model is based on the [Ultimate Vocal Remover] (https://github.com/Anjok07/ultimatevocalremovergui) under the [MIT License] (https://github.com/Anjok07/ultimatevocalremovergui/blob/v5.2.0/LICENSE). I am using "UVR-MDX-NET-Inst_HQ_3".
### Tendorflow
I am using [Tensorflow.js](https://github.com/tensorflow/tfjs) under the [Apache-2.0 license](https://github.com/tensorflow/tfjs/blob/master/LICENSE). Masu.

## References
[Takahashi et al., "Multi-scale Multi-band DenseNets for Audio Source Separation"](https://arxiv.org/pdf/1706.09588.pdf)
