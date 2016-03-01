Syntastic
=========

It is a great VIM plugin which can be found on 
[GitHub](https://github.com/scrooloose/syntastic).
Since syntax checkers in this repo were not able to fit inside syntastic checkers
I have decided to maintain just checkers and not the whole Syntastic with them.

So in case you want to use below syntax checkers, you will need to install and
configure Syntastic, then add the following line to your `.vimrc`:

```
let g:syntastic_c_checkers = ['coverity']
```

or if you want to use other checkers as well and just add Coverity in case
`coverity.conf` is in that directory then add following line to your `.vimrc`:

```
autocmd FileType c let g:syntastic_c_checkers = findfile('coverity.conf', '.;') != '' ? ['coverity'] + g:syntastic_c_checkers : g:syntastic_c_checkers
```

Since Syntastic loads any checker vim home directory/syntax_checkers/c/ you
should clone this to `~/.vim/syntax_checkers/c/` . To make it easier just run 
below commands if you do not have `syntax_checkers/c` directory under your `.vim`

```
mkdir -p ~/.vim/syntax_checkers/c
git clone git@github.com:Letme/syntastic_coverity.git ~/.vim/syntax_checkers/c
```

I am using Syntastic a lot and when we started using Coverity I missed the
direct feedback I get in my Vim from my compilation. Because I did not like the
output of the provided vim script, I have decided to integrate Coverity
inside Syntastic syntax checkers. This repo is a result of that integration.

Coverity external syntax checker
================================

Coverity is static analysis tool which is much smarter than your average lint.
It produces actual analysis flow to your vim using the informational
messages, so that you can easily follow the execution path and figure out how
the analysis came to the conclusion they did.

All Coverity defects (with CIDs) report as Error, while execution
path is part of the informational messages under the CID which nicely leads you
through the problem.

Coverity also supports MISRA checking, and since MISRA produces a lot of noise
I have decided to place all MISRA messages (which are not CID defects) as
warnings.

Setup and requirements
----------------------

To run this checker you need to have Coverity Analysis installed and in path.
Beside this you will need to have cov-run-desktop all setup and ready to run.
The project you are analyzing should be prepared for Coverity Fast Desktop
Analysis with `coverity.conf` file in root.

Troubleshooting
---------------

At the moment if nothing happens on save or Syntastic checker invocation, then
you can should run Coverity Fast Desktop Analysis from terminal. The checker
does provide output on Coverity standard `[ERRORS]`, but I might have missed
some of other error messages which will not display through Syntastic in your
Vim.
 
If you have vim script from Coverity, you can do this directly from VIM with
command: `:Coverity` .


