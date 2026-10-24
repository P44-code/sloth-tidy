# Sloth Tidy

A small program that sorts and renames messy files using a local open-weight AI model (Gemma through Ollama).

It reads the first few words of each file, asks the AI for a category and a clean name, and shows a plan first. It moves nothing until you add `--apply`, and it can undo the last run.

Built for the Hacktoberfest Open-Source AI Challenge: Week 3, "Slow and Steady".

## Run on your laptop (Windows)

1. Install [Python](https://www.python.org/downloads/). Tick "Add python.exe to PATH".
2. Install [Ollama](https://ollama.com).
3. Download the model (one time):

```
ollama pull gemma3:4b
```

4. Put `tidy.py` in a folder, open Command Prompt there, and run:

```
python tidy.py --limit 3
```

This only shows a plan and moves nothing. If the plan looks good:

```
python tidy.py --limit 3 --apply
```

To put the files back:

```
python tidy.py --undo
```

To tidy a different folder, add its path: `python tidy.py "D:\Some\Folder"`

## Try it in Google Colab

The notebook (`.ipynb` file) runs the same steps on 4 fake demo files, so you don't need to install anything. Colab runs on Google's servers, so don't upload private files there.

## What it does

- Sorts files into `Tidied/<Category>/` with a clean new name.
- Reads the first words of text files. For other file types, it uses only the file name.
- Skips folders, hidden files, files still downloading, and files changed in the last minute.
- Cleans every AI answer, so a bad category or an illegal Windows file name cannot break anything.
- Adds (1), (2) if two files would get the same name.

## Settings

You can change these at the top of the code:

- `MODEL_NAME`: the open model to use (default `gemma3:4b`)
- `CATEGORIES`: the folders files can be sorted into

## Limits

- Tested on only 4 demo files, so this is a small demo and not a benchmark.
- Small models make mistakes, which is why it shows a plan first and has undo.
- Only text files are read. PDFs and images are judged by file name.

## License

Add a license file if you want others to reuse the code.
