---
layout: lesson
subtitle: Defensive Programming
teaching: 5
exercises: 10
---
> ## Learning Objectives
>
> * Learner will diagnose corner cases in simple programs.
> * Learner will write `assert` statements with informative messages
>   that test for corner cases in simple programs.
{: objectives}

## Is This Needed?
{: .challenge}

The `os` library contains a function called `os.path.exists(path)`
that returns `True` if the file or directory identified by `path` exists,
and `False` if it does not.
A colleague of yours routinely uses it to check whether a file exists
before trying to open it:

~~~
...
assert os.path.exists(filename), 'File {0} not found'.format(filename)
reader = open(filename, 'r')
...
~~~
{: .python}

Should you adopt this practice?
Why or why not?

## Finding Corner Cases
{: .challenge}

1. Under what circumstances will the following function fail with an error?
2. Under what circumstances will it return something other than what the user would expect?

~~~
def find_two_smallest(values):
    "Find the two smallest values in a list."

    copy = values[:]
    copy.sort()
    return copy[:2]

## Design by Contract
{: .challenge}

1. Explain in simple language what the function is supposed to do.
2. Fill in the blanks in the function definition so that all of the assertions succeed.
3. For what input(s) could different users reasonably expect this function to return different values?
   I.e., where could reasonable people still disagree about the function's behavior?
4. Add one or more assertions to test for each situation identified above.

~~~
def run_starts(values):

    if values == []:
        ____

    result = []
    previous = values[0] + 1
    for v in values:
        if v < previous:
            ____
            previous = ____

    return result

assert run_starts([]) == []
assert run_starts([1]) == [1]
assert run_starts([1, 2]) == [1]
assert run_starts([1, 2, 1]) == [1, 1]
assert run_starts([1, 2, 3, 2, 3]) == [1, 2]
assert run_starts([2, 3, 4, 0, 5, 7, 4, 6]) == [2, 0, 4]
~~~
{: .python}

