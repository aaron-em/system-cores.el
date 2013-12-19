system-cores.el
===============

A unified Emacs Lisp interface to various platform-specific methods of obtaining processor and core counts.

Copyright (C) 2013 Aaron Miller. All rights reversed.
Share and Enjoy!

Last revision: Wednesday, December 18, 2013, ca. 19:30.

Author: Aaron Miller <me@aaron-miller.me>

This file is not part of Emacs.

This file is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published
by the Free Software Foundation; either version 2, or (at your
option) any later version.

This file is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see http://www.gnu.org/licenses.

Commentary
----------

Someone on Stack Overflow [asked][1] whether there was a
platform-independent method of finding out how many processors a
given machine has. It turns out there's not, so I wrote one.

"Platform-independent" is stretching a point; the best I could come
up with was to define a function 'system-cores', which uses a
lookup table ('system-cores-delegate-alist'), keyed by
'system-type' values, to find and invoke a function which knows how
to get the processor and core counts for a given platform. This
means that some platforms, namely those for which I was able to
find reliable instructions on how to obtain processor and core
counts, are supported quite well, while others aren't supported at
all. On the other hand, no truly platform-independent interface to
that information exists at any level, as far as I've been able to
find out, so this works about as well as I think anything could be
expected to do. (And if you use a system which isn't supported,
feel free to write a delegate and submit a pull request on Github,
or email me a diff!)

To use this code, drop this file into your Emacs load path, then
(require 'system-cores), and finally invoke the function
'system-cores' to retrieve processor and core count
information. See that function's documentation for additional
details on its invocation and behavior.

Bugs/TODO
---------

I don't have access to a true BSD system, but only one running
Darwin, which is similar but not quite the same. I've therefore
been unable to properly test the BSD delegate
('system-cores-sysctl'). If you run BSD and want to use this code,
you are strongly advised to investigate your system's sysctl output
and modify 'system-cores-sysctl' accordingly. (If different BSD
variants present the information differently, it may be necessary
to write a function which not only checks 'system-type', but also
examines the value of 'system-configuration', in order to identify
the variant in use.)

Miscellany
----------

The canonical version of this file is hosted in [my Github
repository][2]. If you didn't get it from there, great! I'm happy
to hear my humble efforts have achieved wide enough interest to
result in a fork hosted somewhere else. I'd be obliged if you'd
drop me a line to let me know about it.

[1]: http://stackoverflow.com/q/20666556/1713079
[2]: https://github.com/aaron-em/system-cores.el
