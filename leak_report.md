# Leak report

The allocation initially starts inside the `strip` function, which was called by `is_clean`,
which itself was called inside a `for` loop inside the `main` function. The allocation
is for storing the string result of `strip` in `cleaned` which is then compared to the
original unstripped string, `str`. `strcmp` is used to compare the two strings,
where the output is stored in `result`.

`cleaned` needs to be freed, but before this can be done we must check if `cleaned` 
actually contains data. This is because one of the strings being compared is all spaces.
A simple `strcmp` will do the trick.
