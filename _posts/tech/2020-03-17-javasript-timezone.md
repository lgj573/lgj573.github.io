---
layout: post
title: javascript timezone
category: 技术
tags: [javascript,timezone]
description: javascript timezone
--- 

 
In plain old javascript (new Date()).getTimezoneOffset()/60 will return the current number of hours offset from UTC.


However, I recommend you use the day.js for time/date related Javascript code. In which case you can get an ISO 8601 formatted UTC offset by running:

```
> dayjs().format("Z")
"-08:00"
```

It probably bears mentioning that the client can easily falsify this information.

(Note: this answer originally recommended https://momentjs.com/, but dayjs is a more modern, smaller alternative.)




you could also use moment-timezone to guess the timezone:

```

> moment.tz.guess()
"America/Asuncion"

```


Half a decade later we have a built-in way for it! For modern browsers I would use:
```
const tz = Intl.DateTimeFormat().resolvedOptions().timeZone;
console.log(tz);
```


```
new Date().toLocaleDateString('en-US', { weekday: 'long' })
"Tuesday"
```