```
function AutoColorEvents() {

  var start_date = new Date();
  var end_date   = new Date();
  
  end_date.setDate(start_date.getDate() + 60);  // Sets the date range to 60 days

  var calendar = CalendarApp.getDefaultCalendar();
  var events   = calendar.getEvents(start_date, end_date);

  for (var i in events) {
    
    var event = events[i];
    var title = event.getTitle();
    
    if (title == "11a") {
      event.setColor(CalendarApp.EventColor.CYAN);
    }
    
    if (title == "7p") {
      event.setColor(CalendarApp.EventColor.BLUE);
    }
    
    if (title == "") {
      event.setColor(CalendarApp.EventColor.GRAY);
    }
    
  }

}
```

### Valid event colors are at https://developers.google.com/apps-script/reference/calendar/event-color

