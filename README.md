Syntastic
=========

It is a great plugin which can be found on [GitHub](https://github.com/scrooloose/syntastic).
Since syntax checkers in this repo were not able to fit inside syntastic checkers
I have decided to maintain just checkers and not the whole Syntastic with them.

So in case you want to use below syntax checkers, you will need to install and
configure Syntastic, then add the following line to your `.vimrc`:

```let g:syntastic_c_checkers = ['coverity']```

Since Syntastic loads any checker vim home directory/syntax_checkers/c/ you
should clone this to `~/.vim/syntax_checkers/c/` . To make it easier just run 
below commands if you do not have `syntax_checkers/c` directory under your `.vim`

```
mkdir -p ~/.vim/syntax_checkers/c
git clone git@github.com:Letme/syntastic_coverity.git ~/.vim/syntax_checkers/c
```

Coverity inline syntax checker
==============================

Coverity is static analysis tool which is much smarter than your average lint.
It produces actual analysis flow to your vim browser using the informational
messages so that you can easily follow the execution path and figure out how
the analysis came to the conclusion they did. Coverity provides some script,
but I was not really happy with the output so I have integrated that into the
Syntastic. Now all Coverity defects (with CIDs) report as Error, while execution
path is part of the informational messages under the CID which nicely leads you
through the problem.

Coverity also supports MISRA checking, and since MISRA produces a lot of noise
I have decided to place all MISRA messages (which are not CID defects) as
warnings.



