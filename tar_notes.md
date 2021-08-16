# Tar Notes

Author: __*yufanana*__
</br>
____

More info can be found on [tecmint.com](https://www.tecmint.com/18-tar-command-examples-in-linux/).

*tar* stands for tape archive. <br>
It is used to create highly compressed archive files (tar, gzip, bzip).

It is possible to tar/untar extra single, multiple, or a group of specified files.

It is possible to add files/directories to tar.gz/tar.bz2 files.

### Create tar archive file
`tar -cvf filename.tar /path/to/directory` <br>
e.g. `tar -cvf tecmint-14-09-12.tar /home/tecmint/`

### Create tar.gz archive file
Creates a cimoressed gzup archive file. <br>
tar.gz and tgz files are similar.

`tar cvzf filename.tar.gz /path/to/directory` <br>
e.g. `tar cvzf MyImages-14-09-12.tar.gz /home/MyImages`

### Create tar.bz2 archive file
*bz2* feature creates a smaller archive file size than gzip, but takes more time to compress/decompress.

### Untar tar acrhive file
Use the `x` option to extract. <br>
Use `-C` option to untar in a different directory.

For current directory, `tar -xvf filename.tar`

For another dircotry, `tar -xvf filename.tar -C /path/to/directory` <br>
e.g. `tar -xvf public_html-14-09-12.tar -C /home/public_html/videos/`

### Uncompress tar.gz archive file
Use `-C` option to untar in a different directory.

For current directory, `tar -xvf filename.tar.gz` <br>
e.g. `tar -xvf thumbnails-14-09-12.tar.gz`

### Uncompress tar.bz2 archive file

`tar -xvf filename.tar.bz2`
e.g. `tar -xvf videos-14-09-12.tar.bz2`