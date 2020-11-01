# w3m-man

A simple script to view man pages in the terminal.

It uses `wget` and `w3m` (by default) to get the man pages from various websites.

# Quickstart

```
man <command>        # view man page in plain text in $PAGER
man -H <command>     # view man page as HTML in $TERM_BROWSER
man <command> --url  # print the URL of the man page to STDOUT
```

## Usage

Some of the GNU `man` options are supported:

```
  man <command>           # [get and] print the man page

  man <section> <command> # [get and] print the man page in given section

  man <command> --url     # print the URL from which the man
                          # page was/would be downloaded

  man --help              # print this help info
```

Where `<command>` is the command name you want to read about.

If needed, `man` will cycle through each category to find an existing man page.

To view man pages as HTML (using `$TERM_BROWSER`, or `w3m` if 
this variable doesn't exit), use `-H` as the first option.

## About man page sections

Man pages are divided into sections, as follows:

1. User: most user commands and programs.
2. System: calls by the Linux kernel.
3. Library: documents provided by the standard C library.
4. Devices: documents various devices, most of which reside in /dev.
5. Files: describes various file formats and filesystems and proc(5).
7. Overviews, conventions, and miscellaneous.
8. Superuser and system administration commands.

## Examples

```
  man mount               # view 'mount' command

  man intro.1             # view info about section 1

  man mount.8             # view 'mount' in section 8 (config stuff)

  man 8 mount             # same as above, but doesn't work with -H

  man 5 xorgconf          # get xorg.conf from section 5 (dont use . in name)

  man -H mount            # view 'mount' man page as HTML using $BROWSER

  man <command> --url     # only print the URL from which the man page
                          # was/would be downloaded
```

## More info

Uses these URLs from the following websites:

```
the Ubuntu or Debian man pages, also:

http://manpages.org/${command}/${section}
https://linux.die.net/man/${section}/${command}
https://www.mankier.com/${section}/${command}
http://man.he.net/?topic=${command}&section=${section}
https://man7.org/linux/man-pages/man${section}/${command}.${section}.html
http://manpages.org/${command}
http://man.he.net/?topic=${command}&section=all
https://ss64.com/bash/${command}.html
```

## How it works

It downloads the man page from a website, using `wget`.

If running an Ubuntu based Puppy Linux, the correct version of 
Ubuntu man pages will be searched first. Likewise for any Debian 
based Puppy Linux, too.

It uses `$HTMLPAGER` to convert the HTML file to plain text, or 
`w3m -dump` if that variable doesn't exist.

It saves the man pages in plain text.

The plain text files are cleaned up a bit, and saved to 
`$HOME/.w3m-man/<cmd>.<section>`.

It then displays them using `$MANPAGER` or `$PAGER`, or falls 
back to `less`, if these aren't set. 

Does not need `roff`, `groff` (etc) to be installed, or any man 
pages.

Note:

- `$TERM_BROWSER` could equal `w3m` or `lynx`. 
- `$HTMLPAGER` could equal `w3m -dump`, or `lynx -dump` might work too. 
