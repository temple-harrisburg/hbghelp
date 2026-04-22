[Whisper.cpp](https://github.com/ggml-org/whisper.cpp) is a program for speech recognition. It can be used for transcribing speech from audio or videos into text. While online services may charge a fee for transcriptions, Whisper.cpp is a free and open-source program that runs on your own computer. 
## Using a graphical user interface (Vibe)
1. Download and run the latest [Vibe](https://github.com/thewh1teagle/vibe/releases) installer (for Windows, it will be `vibe_#.#.#_x64-setup.exe`).
2. Launch the program
3. Wait for Vibe to download the base model
4. Click "Select file", then click "Transcribe"
5. Choose your preferred output format and save the file.
![[Pasted image 20251222140545.png]]
![[vibe_loading.gif]]

![[vibe_transcribing.gif]]

## Using the command line (whisper-cli.exe)

1. Download the [Whisper.cpp release archive](https://github.com/ggml-org/whisper.cpp/releases) (`whisper-bin-x64.zip`)
2. Download the speech recognition model (`ggm-base.en.bin`) from [Hugging Face](https://huggingface.co/ggerganov/whisper.cpp)
3. Extract the contents of `whisper-bin-x64.zip` and navigate to the "Release" sub-folder
4. Create a folder called "models" within the "Release" folder
5. Open a terminal
6. Navigate to the "Release" folder and execute `./whisper-cli.exe input.wav`, where `input.wav` is some input.