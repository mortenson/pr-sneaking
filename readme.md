# pr-sneaking

This repository exists to demonstrate methods of sneaking malicious code into
Github pull requests.

While there has never been a real-world example of this kind of attack before,
it makes sense to me as an exploit vector. If you want to compromise thousands
of sites using XSS, all you would have to do is get one piece of malicious code
committed to a common npm package. If your targets are using an automated
build, you could see your exploit released the day after the npm package
releases.

So far I only have two methods of hiding malicious code in a Github PR, but I
welcome contribution!

## Example 1: Manually add exploit into minified/compiled code

In [pull request #1](https://github.com/mortenson/pr-sneaking/pull/1), I fix a
legitimate bug in the source code, but after compiling the source with bower, I
manually edit the minified JS and add the code `alert('foo')`. By using the
Github interface, can you spot the code without using your browser's search?

This seems trivial, but if you can find a file that 

## Example 2: Add NULL character and exploit to any file

Github, and Git for that matter, don't like NULL characters in source code. If
you run `git diff` in your command line after adding a NULL character to a
file, it doesn't output anything.

Github has a slightly different behavior, where files with NULL characters are
displayed as "Binary file not shown", even if their file type is normal.

In [pull request #2](https://github.com/mortenson/pr-sneaking/pull/2), I add an
easily-committable change to source, but manually add an exploit and a NULL
character to a compiled file. Looking at the diff in Github, would you spot the
issue? If so, would you still spot it if dozens of files, including binary
files were changed?
