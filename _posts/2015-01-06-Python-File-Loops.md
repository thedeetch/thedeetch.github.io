---
---

Recently I was looking to improve the performance of a Python 2.5 script that compares two files line by line. What I found interesting was the huge performance improvements I saw with just a few tweaks. I've simplified the problem to just reading the file and updating a counter, to keep things simple.</p>
Each of these script was ran against a 75 million line text file and the results were averaged over 3 runs. This was a quick and unscientific test, so no guarantees of accuracy.

Caveat: I'm not an experienced Python or Perl developer. I can't guarantee any of this code is best practice or pretty :)

##Perl
This is the baseline we're trying to hit. This also outperformed our original bash implementation.

{% gist 64f44c320c46e8324bfb perl.pl %}

##readline()
This is the code I was given to start with. This seems to look like it would perform well, but I have very little Python background.
{% gist 64f44c320c46e8324bfb readline.py %}
Performance isn't good enough. Unfortunately, reading line by line from disk isn't helping performance. Lets try to improve that.

##for line in file
The for loop uses a buffer, so we shouldn't be so dependent on disk I/O.
{% gist 64f44c320c46e8324bfb for.py %}
A 50% performance improvement is good, but not good enough. Still a bit off of the Perl baseline. Lets try some other tweaks.

##for line in file + mutable int
Since Python treats all strings and ints as immutable, we'll throw our counter into a mutable list, which lets us reuse the same memory space when incrementing.
{% gist 64f44c320c46e8324bfb for_mutable.py %}
Bingo. Right on par with our Perl baseline. Good enough for me.
