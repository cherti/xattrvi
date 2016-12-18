=========
 xattrvi
=========

NAME
====

xattrvi - view and edit userspace extended attributes of files

SYNOPSIS
========

xattrvi [options] <filename>

HOW TO USE
==========

Used on a file, xattrvi will write extended attributes from userspace to a temporary file which is opened in the editor specified by $EDITOR.
Attributes can then be edited and changed and new attributes will be (re)written to the file, deleted one's will be removed.

xattrvi is only intended for userspace-xattrs and the "user."-prefix is implicitly prepended in the editable text.
xattrs from other namespaces can not be edited with xattrvi.

OPTIONS
=======

**-h, --help** show commandline options

**-e, --encoding** encoding to be used for value-decoding, defaults to utf-8

**--hide-undecodable** hide entries whose value could not be decoded properly

LIMITATIONS
===========

Keys may not contain the character `:`.
Although supported by filesystems, xattrvi does not support this character for keys, but reserves it for key-value-separation in the display-file.
Values, though, may include this character.

XATTRVIRC
=========

The file `~/.config/xattrvi/xattrvirc` can be used for further configuration.
The syntax is one option per line, empty lines and lines beginning with a `#` are ignored.

Currently, two types of options are supported:
* `ignore: <full-key>` allows to ignore certain keys entirely. They will not be retrieved, displayed or editable.
* `value_encoding: <full-key>: <encoding>` allows to set certain custom encodings for the value-field of an attribute. The encoding must be provided as a Python3-type encoding.

Please note that keys provided in `xattrvirc` are not assumed to have any prefix, so the `user.`-prefix for keys must be specified here.

LICENSE
=======

xattrvi is licensed under GPLv3.
