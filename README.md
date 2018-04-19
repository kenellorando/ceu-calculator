# CEU-Calculator
This is a tool used for calculating Continuing Education Units (CEU's). It takes into account the course's term, run time, days it is hosted, as well as typical holidays off (determined by the term) to provide accurate CEU calculations.

**Calculator available here: https://kenellorando.github.io/ceu-calculator/**

Created for the Office of Professional Development at the Illinois Institute of Technology.

# Documentation
The user will provide the program with the following:
* Academic term
* Class start/end times in 24 hour format
* Days of week of class

When the "calculate" button is pressed, the `main` function is executed.

The function begins a counter object `daysOfClass`, in which each weekday key is initially set to 0.

`daysOfClass` is then incremented by the number of weeks in that term for the days of the week it is hosted. The number of days off for each day of the week is separately subtracted after to more easily modify the program.

After the `daysOfClass` object has been calculated, a `for in` loop is run to tally the total number of class days that class will have. (only the days with values over 0 are added)

Next, the program calculates the number of minutes per class period.

Finally, an exact CEU calculation is completed and rounded for the final result. If the exact calculation is greater than 4.9, "4.9" will appear, as it is the highest maximum number of CEUs. Likewise, if the calculation is less than 3.8, "3.8" will appear as it is the minimum.
