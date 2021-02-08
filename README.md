# jpg-opt: batch re-encode JPEG images with efficient coding to produce compact files containing the same level of perceptible image details

An open secret about JPEG files is that most software products, even the most highly regarded professional image editing products like Photoshop, do not use the best possible encoding algorithm. JPEG files produced by such software are bloated with redundancy for any given pixel dimension and image quality.

This script will batch re-encode JPEG files saved by another software to make standard-compatible compact outputs that preserve the perceptible details in the input. The input files can be small web sizes or large print sizes and low quality or high quality. The script will batch-process all files given in the command-line argument.

Since jpeg-recompress, the main processing command, takes a significant amount of processing time with large pixel dimension files, and multiple such files are typically batch-processed together, this script runs up to 8 processes in parallel (customizable in the script, as the argument to xargs -P).

There are some examples and a script in jpeg-archive to use the jpeg-recompress command, but this script will try to squeeze the file a bit harder. This script will remove EXIF tags unnecessary for the finished image delivery and encode them as progressive JPEG files, which are often smaller.

If you are smart enough to be skeptical, try this experiment: save a high-resolution, high-quality JPEG file using Photoshop or Lightroom (or anything for that matter), and compress it with this script. You'll notice the size reduction but no change to the quality. The image went through a diet program to lose fat or useless bulk but didn't lose muscle or valuable image details. Save a copy of this version for reference.

Now, use any image editing software and make a trivial change (like modifying one pixel or adjusting something simple like exposure just by an insignificant amount or one tiny notch) so that the editor knows the image should be saved. Re-save the image as a new JPEG, without re-sizing and using a high quality parameter. You'll see the file just became fat again. That should give you confidence that the reference file's compactness was due to the encoder efficiency or lost fat, not due to muscle loss. If this script caused the muscle loss, the muscle must be gone forever, and the test and reference files would weigh similarly.

#### Usage
$ jpgopt \*.jpg

It replaces the bloated original JPEG files with a new compact version unless the file was previously processed. The script will detect already-processed JPEG files and automatically skip them.

#### Dependencies
This is a plain vanilla bash script with the following dependencies, besides standard UNIX commands. I compiled all these locally on an x86_64 macOS environment. I don't see any reason these shouldn't run on most modern 64-bit UNIX-like environments.

1. jpeg-archive

It includes jpeg-recompress, the heart of this script. If you are interested in a better JPEG encoding strategy, study that project. It would also help to know the basics of rate-distortion theory and Shannon theory.

https://github.com/danielgtaylor/jpeg-archive

which in turn depends on MozJPEG. https://github.com/mozilla/mozjpeg

2. exiv2

It is used to strip unnecessary EXIF metadata records but preserves the author/copyright tags.

https://exiv2.org/download.html

3. jpegtran utility command in libjpeg

It is used to encode the JPEG in progressive encoding, which often results in a smaller size.

https://jpegclub.org
https://en.wikipedia.org/wiki/Libjpeg#jpegtran

4. noti

To notify the completion of the batch process through macOS notification (optional)

https://github.com/variadico/noti

#### Bugs and Limitations
You'll realize many people have very little knowledge of how to judge image quality. They may erroneously believe your JPEG files to be of low quality because of their compact file sizes since they are used to fatty and bloated JPEGs.

#### Disclaimer
This script and documentation come with absolutely no warranty of any kind. Issues reports are appreciated, and I may, in fact, improve the script for my benefit and update/share but expect no support. Use at your own risk.

#### License
This project is licensed under Creative Commons Attribution-ShareAlike license cc-by-sa-4.0.

#### Author
Ryuji Suzuki
I'm a full-time professional photographer based in Boston. I write programs to make my studio operation easier.
https://suzuki.photo
