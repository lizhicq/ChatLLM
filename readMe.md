# Introduction

This project is to build some add on feature after locally compiling and runnning LLM(large language models) on Apple Sillicon Mac platform. 

## LLAMA2 models 

## The large language models usability

The problem with large language models is that you can’t run these locally on your laptop. Thanks to [Georgi Gerganov](https://www.linkedin.com/in/georgi-gerganov-b230ab24) and his [llama.cpp](https://github.com/ggerganov/llama.cpp) project, it is now possible to run Meta’s LLaMA on a single computer without a dedicated GPU.

# 4 Steps in Running LLaMA-13B on a M1 MacBook Pro

## Running LLaMA

There are multiple steps involved in running LLaMA locally on a M1 Mac after downloading the model weights.

You can see the different models are in a different directories. Now let's begin:

### Step 1: Install dependencies
clone llama2 and llama.cpp projects
```
$git clone https://github.com/facebookresearch/llama.git
$conda create -n llama
$conda install python=3.11
$cd llama-main 
$python3 -m pip install -r requirements.txt
$./download.sh # Select llama-2-13b-chat
```
After you downloaded the model weights, you should have something like this:

```sh
.
├── 7B
│  ├── checklist.chk
│  ├── consolidated.00.pth
│  └── params.json
├── 13B
│  ├── checklist.chk
│  ├── consolidated.00.pth
│  ├── consolidated.01.pth
│  └── params.json
├── 30B
│  ├── checklist.chk
│  ├── consolidated.00.pth
│  ├── consolidated.01.pth
│  ├── consolidated.02.pth
│  ├── consolidated.03.pth
│  └── params.json
├── 65B
│  ├── checklist.chk
│  ├── consolidated.00.pth
│  ├── consolidated.01.pth
│  ├── consolidated.02.pth
│  ├── consolidated.03.pth
│  ├── consolidated.04.pth
│  ├── consolidated.05.pth
│  ├── consolidated.06.pth
│  ├── consolidated.07.pth
│  └── params.json
├── tokenizer.model
└── tokenizer_checklist.chk
```

If you download one model, you may miss the tokenizer.model file, you can copy from my codebase.


### Step 2: Compile llama.cpp

```
$git clone https://github.com/ggerganov/llama.cpp.git
$make
```

### Step 3: Convert llama2 models to ggml format

```
$python convert-pth-to-ggml.py ../models/llama-2-13b-chat 1
$ ./quantize ../models/llama-2-13b-chat/ggml-model-f16.bin ../models/llama-2-13b-chat/ggml-model-q4_0.bin 2
```

## Step 4: Run the model
$ ./main -m ../models/llama-2-13b-chat/ggml-model-q4_0.bin \
        -t 8 \
        -n 128 \
        -p 'The first man on the moon was '


# Notes:
1. I ignore llama models as it is too large to store in git, please refer to step 1 to download and step 3 to compile those models 
2. Add for submodule 
```
$git init
$git submodule add https://github.com/ggerganov/llama.cpp.git llama.cpp
$git submodule add https://github.com/facebookresearch/llama.git llama
```
3. Push to origin
```
$git commit -m 'create project'
$git remote add origin https://github.com/username/repository.git
```



# Demo 
![Prime Number](data/images/prime_number.png)
[![Watch the video](data/images/prime_number.png)](https://youtu.be/hNso61xiTew)