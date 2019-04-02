# command-line-calculator
# From the command line the user will be able to view the calendar, add events, update existing event and delete events from the calendar. The program will welcome the user, ask what the user wants to do and comply with that request.
# Making a new commit for the HNG internship

from time import sleep, strftime

USER_FIRST_NAME = "Daniel-Ita"

calendar = {}

def welcome():
  print "Hello " + USER_FIRST_NAME + ", welcome to your calendar."
  print "Calendar opening..."
  sleep(1)
  print "Today's date:" + strftime("%A %B %d, %Y")
  print "Current time:" + strftime("%H:%M:%S")
  sleep(1)
  print "What would you like to do?"
                                   
def start_calendar():
  welcome()
  start = True
  while start:
    user_choice = raw_input("A to Add, U to Update, V to View, D to Delete, X to Exit: ")
    user_choice = user_choice.upper()
    if user_choice == "V":
      if len(calendar.keys()) < 1:
        print "This is an empty calendar."
      else:
        print calendar
    elif user_choice == "U":
      date = raw_input("What date? ")
      update = raw_input("Enter the update: ")
      calendar[date] = update
      print "Successfully Updated!"
      print calendar
    elif user_choice == "A":
      event = raw_input("Enter event: ")
      date = raw_input("Enter date (MM/DD/YYYY): ")
      if len(date) > 10 or int(date[6:]) < int(strftime("%Y")):
        print "Invalid date entered!"
        try_again = raw_input("Try Again? Y for Yes, N for No: ")
        try_again = try_again.upper
        if try_again == "Y":
          continue
        else:
          start = False
      else:
        calendar[date] = event
        print "Event added successfully"
        print calendar
    elif user_choice == "D":
      if len(calendar.keys()) < 1:
        print "This calendar is empty"
      else:
        event = raw_input("what event?: ")
        for date in calendar.keys():
          if event == calendar[date]:
            del(calendar[date])
            print "The event has been deleted successfully."
            print calendar
          else:
            print "An incorrect event was specified."
    elif user_choice == "X":
      start = False
    else:
      print "Invalid command entered"
      start = False
                                   
start_calendar()
