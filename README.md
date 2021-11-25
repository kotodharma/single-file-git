I have been frustrated by the fact that git, in spite of its tremendous power and
flexibility, is simply not designed to deal with "projects" that are comprised of
only a single file, often in a directory along with a bunch of other individual text
files that I might also like to revision independently of each other.

"Just use RCS," you might say. Yeah, well, but... I like git, want to keep using it,
to learn it better, and, well, RCS is just too ancient. Let's be serious.

So I finally sat down and wrote a shell script to handle this modus operandi.
Basically, it creates a separate bare repo for each file, with a unique name, and
takes advantage of the fact that git has a command line option to override the default
repo directory name ".git".

I hate the executable name `git1`, but haven't yet thought of something I like better.
I encourage you to change it to whatever appeals to you.

This is written to run on UNIX and UNIX-like OSes. If you want to port it to
Windows or whatever, be my guest. I've put it in the public domain, so you can do
with it as you please. Pull requests accepted.


To use this script, create a bare repo for the file you want to revision
(e.g. foo.txt), by calling this script with the 'init' subcommand:

  git1 init foo.txt

You should see git output indicating successful repo creation. The file
has also been checked in to the new repo. Needless to say, this step is only
performed once, at the outset.

Now, you may call the present script with the filename as first argument,
and follow with any normal git commands and options:

  git1 foo.txt status
  git1 foo.txt commit -m "added new blah"
  git1 foo.txt diff
  git1 foo.txt log

etc.

Because the bare repo is unique to the file foo.txt, you can create as many
of these as you like in the same directory, and commands will always have the
revisioned filename as first argument, to distinguish which repo for git to
refer to. Note that this script can only be used from inside the same
directory where the file its repo exist.

To see what repos exist in the current directory:

 git1 ls

To remove a repo (though this does NOT remove the tracked file):

 git1 rm foo.txt

Protip: If you'll be doing a lot of git work on a given file at a particular
time, considering creating a temporary alias for "git1 foo.txt":

 alias gg='git1 foo.txt'

Then, commands can be simplified: gg diff, gg commit, etc.

