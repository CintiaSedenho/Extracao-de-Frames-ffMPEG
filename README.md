# Video Frame Extraction for OCR using FFmpeg

This project extracts key frames from screen recordings using **FFmpeg** with scene detection sensitivity optimized for OCR workflows, spreadsheet reconstruction, and data transcription.

Ideal for:

* Excel/table recordings
* OCR preprocessing
* Manual data entry workflows
* PaddleOCR / Tesseract pipelines

---

# Requirements

* FFmpeg installed
* Windows CMD or PowerShell

Download FFmpeg:

[FFmpeg Official Website](https://ffmpeg.org/download.html?utm_source=chatgpt.com)

---

# Folder Structure

Create the following structure:

```text
2020Metals/
│
├── ScreenRecording_05-18-2026 12-51-35_1.mp4
│
└── frames/
```

The `frames` folder will receive all extracted images.

---

# Open CMD in the Correct Folder

1. Open the folder containing the video
2. Click the address bar
3. Type:

```bash
cmd
```

4. Press Enter

---

# FFmpeg Command

Run this command in a single line:

```bash
ffmpeg -i "ScreenRecording_05-18-2026 12-51-35_1.mp4" -vf "select='gt(scene,0.02)',showinfo" -fps_mode vfr "frames\frame_%06d.png"
```

---

# Explanation

| Parameter        | Description                           |
| ---------------- | ------------------------------------- |
| `scene,0.02`     | Scene change sensitivity              |
| `showinfo`       | Displays frame information in console |
| `-fps_mode vfr`  | Prevents duplicate frames             |
| `frame_%06d.png` | Sequential frame naming               |

---

# Sensitivity Guide

| Value   | Result                            |
| ------- | --------------------------------- |
| `0.01`  | Extremely sensitive (many frames) |
| `0.02`  | Recommended for spreadsheets/OCR  |
| `0.05`  | Fewer frames, only major changes  |
| `0.08+` | Very aggressive filtering         |

---

# Recommended Workflow for OCR

1. Extract frames
2. Remove blurry/duplicate frames
3. Rotate frames if necessary
4. Run OCR
5. Export to Excel/CSV

---

# Example Output

```text
frames/
├── frame_000001.png
├── frame_000002.png
├── frame_000003.png
```

---

# Notes

* Keep the entire FFmpeg command on a single line in CMD.
* `-vsync` is deprecated in newer FFmpeg versions.
* Use `-fps_mode vfr` instead.

---

# Useful Variations

## Extract fewer frames

```bash
ffmpeg -i "video.mp4" -vf "select='gt(scene,0.05)'" -fps_mode vfr "frames\frame_%06d.png"
```

## Extract more frames

```bash
ffmpeg -i "video.mp4" -vf "select='gt(scene,0.01)'" -fps_mode vfr "frames\frame_%06d.png"
```

---

# License

MIT License
