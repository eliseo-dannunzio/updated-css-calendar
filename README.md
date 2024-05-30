# Updated CSS Calendar
This is an updated instance of the CSS Calendar using :has, mod(), min() and max() functions; but no JavaScript...
A Pure CSS/HTML functional calendar that can correctly display months from Jan 1800 to Dec 2999, using no JavaScript.

Live Demo: https://codepen.io/eliseodannunzio/pen/bGypzyM

Please feel free to reach out to me at eliseo.dannunzio@gmail.com to discuss the inner workings of this project!

## What dark magic is this?? ##
How do you mean? It's a calendar. You select the month and the year with the dropdowns and from there, it will display the appopriate month for that year...

## But it's all in CSS and HTML, how is it calculating which day of the week the month starts from? ##
It's all calculated in CSS!

## Wait... what? Doesn't that stuff normally happen using JavaScript? ##
Well, yes, normally that would be the case. But I wanted to set myself a challenge and take advantage of CSS's `var()`, `mod()`, `min()` and `max()` functions and see what could come of it. This is the end result.

## But how are you managing this all in only CSS and HTML? ##
HTML basically takes care of the main structure and sets up the required events needed to help trigger the necessary changes in values. Events fired off in HTML are picked up by CSS and specific CSS selectors help determine the required values to be used to calculate the day of the week for the first of each month. From there some very clever (and VERY recent) CSS takes care of the display of the calendar!

## What's the general algorithm for working out the day of the week for any given date? ##
I originally got the basic algorithm from https://thecompartments.uk/2016/01/19/how-to-work-out-the-day-of-the-week-from-any-date-takes-10-minutes/; but basically it goes as follows:

* Take the year's last two digits and divide by 4, discarding any remainders;
* Add the day of the month;
* Add the month key from the following: 144025036146. So for example, for June, it would be 5 (counting six digits from the left)
* If the month was January or February in a leap year, subtract 1
* Add the century key, 1900's is 0, 2000's is 6, 2100's is 4, 2200's is 2. Any other centuries, subtract or add 400 from the appropriate century; for example 1800's is 2200's (2) - 400 => 1800, 1800's cenury key is also 2.
* Divide by 7 and take the remainder (performing a modulo 7 on the number). The remainder gives you the day of the week, from 0 = Saturday to 6 = Friday. Note: To achieve a day shift to 0 = Sunday to 6 = Saturday, the sum is decreased by 1 before applying the modulo 7 and increased by 1 after the modulo 7.

## That seems like a lot of work! ##
It is but a few mathematical properties, and the fact that I'm working out the first of the month each time, help reduce this to adding 4 numbers and then using the new `mod()` function that is now fairly standard to most modern browsers to get the day of the week.

## Why did you decide to do this? ##
I wanted to push the limits of what could be done within the realms of CSS. CSS changed the way that CSS can be manipulated using `var()` and `calc()`; the use of `min()` and `max()` functions helped determine the logic needed to calculate a number of the equations in the end for display of certain elements. The new `mod()` function actually removes about seven additional calculations needed for this to work from the previous version. The `:has` pseudo-class selector also reduces a number of CSS statements needed, which significantly increases the speed of calculation.

CSS/HTML only projects like this are functional even if JavaScript is turned off in the browser. The fact that this project can react as quickly as a JavaScript app still amazes me, and I'm looking forward to seeing what more I can do with just CSS and HTML.
