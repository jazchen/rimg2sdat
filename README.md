# rimg2sdat
Tool to convert raw images(EXT4 filesystem) to sparse Android data (system.new.dat)

## Requirements
* Requires Python 2.7.5 or newer installed on your system
* It currently supports Windows, Linux (tested)
* Python package: `brotli` or `brotlipy` (only the `-c` parameter is specified)

## Usage
```
$ ./rimg2sdat.py
usage: rimg2sdat.py [OPTION] <raw_image_file>

positional arguments:
  raw_image_file  input system raw image file

optional arguments:
  -h, --help      show this help message and exit
  -o outdir       output directory, default: current directory
  -p prefix       name of sparse data image (prefix.new.dat), default: system
  -v version      transfer list version number, default: 4
  -c              compress the new.dat file to new.dat.br file with brotli.
                  (WARNING! Only Android 8.1 support)
  -nl             when version was 4, no limit 1024 blocks in single command
  -sha1           get sha1 checksums of sparse data image
```

## Example
```
# create system.transfer.list of version 4, and system.new.dat
~$ ./rimg2sdat.py system.img

# create system.transfer.list of version 3, and system.new.dat
~$ ./rimg2sdat.py -v 3 system.img
 
# create test.transfer.list of version 4, then compression test.new.dat into test.new.dat.br
~$ ./rimg2sdat.py -p test -c system.img
 
# create system.transfer.list of version 4
# get sha1 checksums of system.new.dat, then compression it into system.new.dat.br
~$ ./rimg2sdat.py -c -sha1 system.img
```

## Also can be a module
```python
import rimg2sdat

# ~$ ./rimg2sdat.py system.img
rimg2sdat.process('system.img')

# ~$ ./rimg2sdat.py -p test -c -sha1 system.img
rimg2sdat.process('system.img', '-p test -c -sha1')
```

## Info
If you looking decompressing system.new.dat file, you can refer to [sdat2img](https://github.com/xpirt/sdat2img)

