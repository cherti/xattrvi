# xattrvi

`xattrvi` is meant to easily view and edit a filesystem's extended attributes.
It's inspired by the tool `ldapvi` and works quite similarly.

## Usage

First of all, make sure your filesystem allows for extended filesystem attributes.

If that is the case, just open a file with `xattrvi <filename>`.

You will be presented with either an empty file or a file looking like given below, opened either in the environement-variable `EDITOR` or `nano`, if `EDITOR` is not set.

    # attributes in namespace 'user':
    
    bar          : myvalue
    foo          : some value written here

These are the extended attributes as `key : value`-pairs.
The ones that are commented out are those keys that are prefixed with `user.` on the actual filesystem, because those are the attributes the user can set and use.
The `user.` is ommitted in the file for ease of use, but is assumed implicitly for every uncommented option.

New attributes will be set, changed attributes will be updated, vanished attributes will be deleted from the file, so be careful when editing the file.

### Limitations

Keys may not contain the character `:`.
Although supported by filesystems, xattrvi does not support this character for keys, but reserves it for key-value-separation in the display-file.
Values, though, may include this character.

## Configuration

### directly on commandline
Configuration is done via commandline options:

    usage: xattrvi [-h] [-v] [-e STDENC] [-s] [--editor EDITOR] [--hide-undecodable] filename
    
    xattrvi - modify xattributes of files the simple way
    
    positional arguments:
      filename              file that needs to get modified
    
    optional arguments:
      -h, --help            show this help message and exit
      -e STDENC, --encoding STDENC
                            encoding to be used for value-decoding, defaults to utf-8
      --hide-undecodable    hide entries whose value could not be decoded properly
      --editor              specify custom editor on the command line.
                            Example: --editor 'gvim --nofork'.

### xattrvirc

You can use the file `~/.config/xattrvi/xattrvirc` for further configuration.
The syntax is one option per line, empty lines and lines beginning with a `#` are ignored.

Currently, two types of options are supported:
* `ignore: <full-key>` allows to ignore certain keys entirely. They will not be retrieved, displayed or editable.
* `value_encoding: <full-key>: <encoding>` allows to set certain custom encodings for the value-field of an attribute. The encoding must be provided as a Python3-type encoding.

Please note that keys provided in `xattrvirc` are not assumed to have any prefix, so the `user.`-prefix for keys must be specified here.

## License

This works is released under the [GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.txt). You can find a copy of this license at https://www.gnu.org/licenses/gpl-3.0.txt.
