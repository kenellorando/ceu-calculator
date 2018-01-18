# CEU-Calculator
This is a tool used for calculating Continuing Education Units (CEU's). It takes into account the course's term, run time, days it is hosted, as well as typical holidays off (determined by the term) to provide accurate CEU calculations.

**Calculator available online here: https://kenellorando.github.io/ceu-calculator/**

Created for the Office of Professional Development at the Illinois Institute of Technology.

# Documentation
The user will provide the program with the following:
* Academic term
* Class start/end times in 24 hour format
* Days of week of class

When the "calculate" button is pressed, the `main` function is executed.

The function begins a counter object `daysOfClass`, in which each weekday key is initially set to 0 like so:
```
let daysOfClass = {
    "monday": 0,
    "tuesday": 0,
    "wednesday": 0,
    "thursday": 0,
    "friday": 0
}
```

`daysOfClass` is then incremented by the number of weeks in that term for the days of the week it is hosted. The number of days off for each day of the week is then immediately subtracted. For example:

```
if (springInput) {
    // 17 represents 17 class weeks in spring
    if (mondayInput) {
        daysOfClass.monday += 17;
    }
    if (tuesdayInput) {
        daysOfClass.tuesday += 17;
    }
    if (wednesdayInput) {
        daysOfClass.wednesday += 17;
    }
    if (thursdayInput) {
        daysOfClass.thursday += 17;
    }
    if (fridayInput) {
        daysOfClass.friday += 17;
    }

    // Each number represents number of days off of that week day in that term
    daysOfClass.monday -= 2;
    daysOfClass.tuesday -= 1;
    daysOfClass.wednesday -= 1;
    daysOfClass.thursday -= 1;
    daysOfClass.friday -= 1;
}
```

After the `daysOfClass` object has been calculated, a `for in` loop is run to tally the total number of class days that class will have. (only the days with values over 0 are added)

```
let totalClasses = 0;
for (let days in daysOfClass) {
    if (daysOfClass[days] > 0) {
        totalClasses += daysOfClass[days];
    }
}
```

Next, the program calculates the number of minutes per class period.
```
let endTimeMinutes = endTimeInput.substring(0, 2) * 60 + parseInt(endTimeInput.substring(2, 4));
let startTimeMinutes = startTimeInput.substring(0, 2) * 60 + parseInt(startTimeInput.substring(2, 4));
let classRunTime = endTimeMinutes - startTimeMinutes;
```

Finally, an exact CEU calculation is completed and rounded for the final result. If the exact calculation is greater than 4.9, "4.9" will appear, as it is the highest maximum number of CEUs.
```
let CEU = (classRunTime * totalClasses) / 600;
console.log("Calculated CEU: " + (classRunTime * totalClasses) / 600);
console.log("Rounded CEU: " + Math.round(((classRunTime * totalClasses) / 600) * 10) / 10);
if (CEU > 4.9) {
    document.getElementById("CEU").innerHTML = "4.9 (Actual: " + (classRunTime * totalClasses) / 600 + ")";
} else {
    document.getElementById("CEU").innerHTML = Math.round(((classRunTime * totalClasses) / 600) * 10) / 10;
}
```