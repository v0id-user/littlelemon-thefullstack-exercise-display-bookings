# The fullstack excercise
![Coursera](https://img.shields.io/badge/Coursera-0747a6?style=flat&logo=coursera&logoColor=white)
![Meta](https://img.shields.io/badge/Meta-0668E1?style=flat&logo=meta&logoColor=white)
![Django](https://img.shields.io/badge/Django-092e20?style=flat&logo=django&logoColor=white)  

This is my solution to the final fullstack excercise which requires displaying the booking times.

## The excercise
Display the booking times on the page using javascript.

## Steps to setting up the Little Lemon Back-end API

- [x] **Step 1:** Run the following command to activate the virtual environment:
  ```bash
  pipenv shell
  ```
  Note: Make sure you run the command in the main working directory containing the manage.py file. 

- [x] **Step 2:** To make sure you have the necessary dependencies in place, run the following commands inside pipenv:
  ```bash
  pipenv install django
  pipenv install mysqlclient
  ```
  Note: If you are facing problems with using the virtual environment, you can try running the project without using pipenv.

- [x] **Step 3:** Make sure you check the code inside all the supporting files you will need for the exercise. It includes a few changes from the endpoint of part two. 

- [x] **Step 4:** In the terminal run both commands to perform the migrations.
  Note: Make sure you have created the correct MySQL user, assigned privileges, and configured the same database before you perform the migrations. 
  Run the necessary commands to make sure the user is created and can access the database. In case you are using the root user, make sure you have the correct password for the root user added inside the settings.py file.

  Note: The migrations performed here are not necessary as the changes are already in place. It is however a good practice to perform migrations before you begin working on a new code block.  

- [x] **Step 5:** Open the file views.py and create a view function called bookings() below the @csrf_exempt decorator. Pass a request object to it as an argument. 
  Note: The necessary imports are already added inside the views.py file. URL configurations are already in place at the app-level urls.py file for the view function.

- [x] **Step 6:** Inside the view function bookings(), add the following pseudo code:
  
  If value of request.method is equal to “POST”
  
  Create a variable called data and assign it the value of json.load() with the request object passed as an argument.
  
  Create a variable called exist and assign the following value to it:
  
  Booking.objects.filter(reservation_date=data['reservation_date']).filter(reservation_slot=data['reservation_slot']).exists()
  
  If the value of the exist variable is False: 
  
  Create a variable called booking and assign the value of the Booking() class object with the following code passed inside it:
  
  first_name=data['first_name'],
  
  reservation_date=data['reservation_date'],
  
  reservation_slot=data['reservation_slot'],
  
  Call the save() function over the booking variable using the dot operator.
  
  Else return HttpResponse() with the following arguments passed inside it:
  
  "{'error':1}" as a string
  
  Variable content_type with the value equal to 'application/json'
  
  Create a variable called date and assign it the value: 
  
  request.GET.get('date',datetime.today().date())
  
  Create a variable called bookings and assign it the value:
  
  Booking.objects.all().filter(reservation_date=date)
  
  Create a variable called booking_json and assign it the value:
  
  serializers.serialize('json', bookings)
  
  Return HttpResponse() with the following arguments passed inside it:
  
  booking_json
  
  Variable content_type with the value equal to 'application/json'

- [x] **Step 7:** Save the views.py file and ensure the code has no errors and that you have followed the pseudo-code accurately. 

- [x] **Step 8:** Now step inside the book.html file and observe the code. There are three code blocks that you need to complete marked inside comments like:
  
  <!-- Part 1 -->

  You will be replacing the comments with the pseudo-code as specified in following four steps below.

- [x] **Step 9 (for part one):** Observe the code added inside the paragraph tag for the first name and replicate the code for the reservation date to replace the code block.  

- [x] **Step 10 (for part two):** Call a function getElementById() over the document with ‘reservation_date’ passed inside it as an argument. 

  Continue on the same block of code and call the function addEventListener() on it as a suffix using dot operator and pass the following arguments to it:

  ‘change’

  function that contains the code: {getBookings()}

- [x] **Step 11 (for part three):** Run a for loop on the constant data. Use a temporary variable called item to run the loop. Add the code inside the curly braces as follows:

  Call a log() function over the console and pass item.fields as an argument

  Call a push() function over reserved_slots array and pass the item.fields.reservation_slot to it as an argument

  Update the bookings string variable with the code below:

  `<p>${item.fields.first_name} - ${formatTime(item.fields.reservation_slot)}</p>`

- [x] **Step 12 (for part four):** Create a variable called slot_options and assign the following string to it:

  '<option value="0" disabled>Select time</option>'

  Run a for loop for numbers greater than 10 and less than 20 and add the following code inside the curly braces:

  Create a constant called label and assign the function formatTime() to it with i passed inside it as an argument.

  If value of reserved.slots.includes(i) is true add the code:

  slot_options += `<option value=${i} disabled>${label}</option>`

  Else, add the code:

  slot_options += `<option value=${i}>${label}</option>`

  Note: Make sure all the code blocks have appropriate curly braces where necessary.

- [x] **Step 13:** Save the file and make sure there are no visible errors inside your HTML file. 

  Now open the Terminal inside VS Code and add a command to run the server and go to the localhost URL and observe the web page. 

- [x] **Step 14:** Enter your name in the text box and select a date and time of your choice to create a reservation. 

  The screen should appear similar to the screen below:

  Form for making reservations with name, reservation date and time fields and booking entries present

- [x] **Step 15:** After selecting the options and pressing the Reserve Now button, you should be able to see the screen updated with your details. Note the times selected earlier are not available for selection.

  Form displaying drop down option for selecting reservation time.

- [x] **Step 16:** Note the change in the content displayed on the screen as per the change in the date selected:

  Form with fields for reservation and form entries present for a different date.

- [x] **Step 17:** Open the MySQL database and observe the entries updated in line with the changes in the reservations performed inside the template.
