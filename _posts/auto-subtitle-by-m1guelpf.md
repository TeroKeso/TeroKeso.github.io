---
title : Simple Automatic subtitles in your videos using [OpenAI's Whisper](https://openai.com/blog/whisper)
date: 2024-04-12
categories: [cli,AI,video]
tags: [openai, subtitles, cli, wsl]
---

# Simple Automatic subtitles in your videos using [OpenAI's Whisper](https://openai.com/blog/whisper)


### How to install to linux (WSL)
```bash
sudo apt update && sudo apt install ffmpeg python3-pip 
pip install ffmpeg-python
pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu116
pip install git+https://github.com/Sectumsempra82/auto-subtitle-plus.git
echo 'export PATH="$HOME/bin:$PATH"' >> .bashrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> .bashrc
echo 'export LD_LIBRARY_PATH=/usr/lib/wsl/lib:$LD_LIBRARY_PATH' >> .bashrc
```
You need to install cuda to host environment (WSL) or to linux if you are not running wsl
```bash
# Cuda install https://docs.nvidia.com/cuda/cuda-installation-guide-linux/ 
sudo apt update && sudo ubuntu-drivers install 
```


### Install Windows
```bash
Winget install git.git
Winget install winget install --id=Gyan.FFmpeg  -e --accept-source-agreements
winget install -e --id Python.Python.3.0
winget install -e --id Nvidia.CUDA
winget remove 9NBLGGH4QZ94
exit
```
```bash
pip install ffmpeg-python
pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu116
pip install git+https://github.com/Sectumsempra82/auto-subtitle-plus.git
```

### How to use auto_subtitle_plus
```bash
cd /folder/that/has/videos
auto_subtitle_plus *.mp4 --output-srt --model medium --output-srt --language Finnish
auto_subtitle_plus *.mp4 --output-srt --model medium --output-srt --language English
```
### Bash script to run all videos at the same time 

Finnish
```bash
find ./ -type d \( -iname "0 RAW" -o -iname "tuntitallenteet" \) -prune -o -type f \( -iname "*.mkv" -o -iname "*.mp4" \) -exec sh -c 'for file; do if [ -f "$(basename "${file%.*}.srt")" ] || [ -f "./srt/$(basename "${file%.*}.srt")" ]; then echo "The file already exists $file"; else auto_subtitle_plus --output-srt --model medium --language Finnish "$file"; fi; done' _ {} \+
mkdir -p ./srt
mv *.srt ./srt
```

English

```bash
find ./ -type d \( -iname "0 RAW" -o -iname "tuntitallenteet" \) -prune -o -type f \( -iname "*.mkv" -o -iname "*.mp4" \) -exec sh -c 'for file; do if [ -f "$(basename "${file%.*}.srt")" ] || [ -f "./srt/$(basename "${file%.*}.srt")" ]; then echo "The file already exists $file"; else auto_subtitle_plus --output-srt --model medium --language English "$file"; fi; done' _ {} \+
mkdir -p ./srt
mv *.srt ./srt
```
