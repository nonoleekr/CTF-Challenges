# File Type Identification and Flag Retrieval

## Downloading the File
The challenge provides a file with no extension. Without an extension, the file type is unknown, which is a common scenario in CTF challenges.

## Identifying the File Type
Using an online file type identifier tool, the file was checked and identified as a JPEG image. The tool output was as follows:
- File Type: JPEG image data, JFIF standard 1.02
- Resolution: 720x540
- Suggested extensions: `.jpg`, `.jpeg`, `.jpe`, `.jfif`
- MIME Type: `image/jpeg`

## Renaming the File
Since the file had no extension, it was renamed to include a `.jpeg` extension. This allows the operating system and image viewers to recognize and open the file properly.

```
mv filename filename.jpeg
```

## Viewing the Image
Opening the renamed file with an image viewer revealed a mirror (flipped) image containing the flag.

## Extracted Flag
After mirroring the image properly, the flag revealed is:

```
SKR{fil3_sign4tur3_1s_1mp0rt4nt}
```
