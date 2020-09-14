# Date-Time Operations Addon

Dates and times can be quite complex to deal with. This addon simplifies things for you by letting you get the date and time in any format that you like, and calculate the duration between two dates. This addon uses the Joda-Time format. You can find out more information about Joda-Time [here](https://www.joda.org/joda-time/key_format.html).

## Available Actions

`Get DateTime object in a specific format` - Returns a DateTime object in the specified format

Input Parameters:

* `CurrentDateTimeValue` - Current DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `CurrentDateTimeFormat` - The DateTime format used in the `CurrentDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ExpectedDateTimeFormatFormat` - The DateTime format you want your date converted into \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `Locale` - The Locale of the format to use, by default it takes the System Locale.

`Get day of the week from a DateTime object` - Returns the day of a week from the given DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get hour from a DateTime object` - Returns the hour from the given DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get hour from a DateTime object in a string format` - Returns the hour in string format from a given DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `Suffix` - Show the result in 12 hour format? Specify true to use 12 hour format and false to use 24 hour format

`Get milliseconds of a day from a DateTime object` - Returns the milliseconds of a day from the provided DateTime object

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get milliseconds of a second from a DateTime object` - Returns the milliseconds of a second from the provided DateTime object

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the current DateTime` - Returns the current DateTime in ISO 8601 format \(yyyy-mm-ddThh:mm:ss.SSS\).

To use this action specify the desired timezone in the `TimeZone` field. You can specify it in any of the accepted id formats \(for example: 'America/Chicago', 'IST','Etc/GMT+1\). You can find a full list of timezone ids [here](https://garygregory.wordpress.com/2013/06/18/what-are-the-java-timezone-ids/).

{% hint style="info" %}
Note that there are two different commands both called "Get the current DateTime".  Check the description of each when selecting them to ensure you are using the one that you want. 
{% endhint %}

`Get the current DateTime` - Returns the current DateTime in the specified format. 

This action requires you to specify the `Format` \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the current timestamp` - Returns the current time as a number of milliseconds from January 1st 1970

`Get the day of a month from a DateTime object` - Returns the day of a month from the given DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the day of a year from a DateTime object` - Returns the day of a year from the given DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the days difference between two DateTime objects` - Returns the number of days between two given DateTime objects.

Input Parameters

* `FirstDateTime` - DateTime value for the first date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `FirstDateTimeFormat` - The DateTime format used in the `FirstDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `SecondDateTime` - DateTime value for the second date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `SecondDateTimeFormat` - The DateTime format used in the `SecondDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the hours between two DateTime objects` - Returns the number of hours between two given DateTime objects. 

Input Parameters

* `FirstDateTime` - DateTime value for the first date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `FirstDateTimeFormat` - The DateTime format used in the `FirstDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `SecondDateTime` - DateTime value for the second date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `SecondDateTimeFormat` - The DateTime format used in the `SecondDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the milliseconds from a DateTime object` - Returns the milliseconds from the provided DateTime object. 

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the minutes between two DateTime objects` - Returns the number of minutes between two given DateTime objects. 

Input Parameters

* `FirstDateTime` - DateTime value for the first date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `FirstDateTimeFormat` - The DateTime format used in the `FirstDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `SecondDateTime` - DateTime value for the second date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `SecondDateTimeFormat` - The DateTime format used in the `SecondDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the minutes of hour from a DateTime object` - Returns the minutes of the hour from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the minutes of the day from a DateTime object` - Returns the minutes of the day from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the month from a DateTime object` - Returns the month from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the month name from a DateTime object` - Returns the month's name from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the seconds between two DateTime objects` - Returns the amount of seconds between two given DateTime objects.

Input Parameters

* `FirstDateTime` - DateTime value for the first date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `FirstDateTimeFormat` - The DateTime format used in the `FirstDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `SecondDateTime` - DateTime value for the second date \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `SecondDateTimeFormat` - The DateTime format used in the `SecondDateTime`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the seconds of a day from DateTime object` - Returns the seconds of a day from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the seconds of a minute from DateTime object` - Returns the seconds of a minute from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the week of the year from a DateTime object` - Returns the week of a year from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Get the year from a DateTime object` - Returns the year from the provided DateTime object.

Input Parameters

* `DateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `DateTimeFormat` - The DateTime format used in the `DateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)

`Set days of a DateTime object` - Changes the days value of a given DateTime object and returns the new DateTime object. 

Input Parameters:

* `Days`- Number of days to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set hours of a DateTime object` - Changes the hours value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Hours`- Number of hours to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set milliseconds of a DateTime object` - Changes the milliseconds value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Milliseconds`- Number of milliseconds to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set minutes of a DateTime object` - Changes the minutes value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Minutes`- Number of minutes to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set months of a DateTime object` - Changes the months value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Months`- Number of months to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set seconds of a DateTime object` - Changes the seconds value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Seconds`- Number of seconds to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set weeks of a DateTime object` - Changes the weeks value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Weeks`- Number of weeks to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

`Set years of a DateTime object` - Changes the years value of a given DateTime object and returns the new DateTime object.

Input Parameters:

* `Years`- Number of years to offset the given DateTime object \(for example: -2 or 3\)
* `OriginalDateTimeValue` - DateTime value \(for example: 28/05/2019 or Sept 22, 1999, 21:01 etc.\)
* `OriginalDateTimeFormat` - The DateTime format used in the `OriginalDateTimeValue`field \(for example: dd/mm/yyyy or MMM dd, yyyy, HH:mm etc.\)
* `ResultFormat` - The DateTime format to be used in the new result. If left blank it will default to the format of the original DateTime object 

