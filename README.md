## C++ Style Guide

Included in this directory are a `clang-format` and linting script. They
haven't been perfected yet, and work is still being done.

### List of Files

`clang-format`: Place this as `.clang-format` in the root of the project where
the style should apply.

`cpplint.py`: Google's C++ linter taken from Node.js `tools/cpplint.py`. Current
version taken from v14.2.0.

Run with the following options:
```
cpplint.py --linelength=80 --filter=-build/include_subdir,-build/include_what_you_use,-legal/copyright,-readability/nolint -- <file>
```

Or add this to `.cpplint` in your project:
```
set noparent
filter=-build/include_subdir,-build/include_what_you_use,-legal/copyright,-readability/nolint
linelength=80
```

`git-clang-format`: Script to run `clang-format` on specific commit(s). Useful
to only fix changes on a patch instead of the entire file. Can place in a
location like `~/.local/bin` to run globally.

Usage:
```
# Run clang format on revision diff and apply changes.
git-clang-format <revision> <file>

# Run clang format on revision and display diff.
git-clang-format --diff <revision> <file>
```

Taken from https://github.com/llvm/llvm-project/blob/master/clang/tools/clang-format/git-clang-format

`run-clang-format.py`: Generate diff of file(s) and .clang-format. This can be
used with `git apply` to apply changes after they've been reviewed.

Taken from https://github.com/Sarcasm/run-clang-format/blob/master/run-clang-format.py



**TODO:** Finish below sections on research and reasoning behind styles.

### Styles

Code style is a heated and much debated topic. Because of this I did a fair
amount of research on how humans read code, and the best ways to help our
comprehension of that code. Below is each main point along with the reasons and
research.

#### Column Limit

The often used 80 character limit used today can be traced back to the use of
IBM punch cards that had a maximum of 80 characters. So the question is if we
should continue to use that, or any, limit today.

While it is true that we can read faster if our eyes do not need to make
vertical adjustments, it must be understood that code is not read. Code is
scanned, quickly jumping up and down pages of text to find what we need, and on
bad days a lot of time can be spent staring at the same few lines of code.

Scientifically this is referred to as rapid non-linear saccadic eye movements.
The high resolution of our retina (the fovea) has only 1-2 degrees of vision.
This translates to only about half an inch of vision if the computer screen is
two feet away. This means the majority of code we're looking at lies within our
peripheral vision. The easiest identifier to reposition our saccadic eye
movements is whitespace.

The easiest method to solve both of these issues to enforce a column limit that
makes it easy to keep as much code as possible within our high resolution area
while also allowing our eyes to reposition as quickly as possible on code that
lies within our periphery. This allows intelligent use of vertical space to
encapsulate related code in an area that's easiest for us to quickly find.

Our short term memory is limited to about 18 seconds, and 7±2 items. Any code
that we need to concentrate on will automatically enter our short term memory.
So it makes sense to place high priority on being able to find the code we're
looking for with the least number of distractions.

### Argument Alignment



### Pointer Notation

Putting a space between the type and `*` doesn't work if the argument name is
left blank. e.g. `foo(int *, int *);`.


### Snake Case
