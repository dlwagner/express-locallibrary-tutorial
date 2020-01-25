This project is from the localLibrary tutorial at MDN Web Docs. All the code in this repo is theirs.
I'm just using this project as a way to learn web development and to learn how 
to publish to heroku. Below are notes I've taken along the way.



----------------------------------------------------------------------------------
My Notes:
----------------------------------------------------------------------------------

To test the routes, first start the website:

default run method(linux):
DEBUG=express-locallibrary-tutorial:* npm start

if using nodemon, run(linux):
DEBUG=express-locallibrary-tutorial:* npm run devstart

Then test the Urls:
    http://localhost:3000/
    http://localhost:3000/catalog
    http://localhost:3000/catalog/books
    http://localhost:3000/catalog/bookinstances/
    http://localhost:3000/catalog/authors/
    http://localhost:3000/catalog/genres/
    http://localhost:3000/catalog/book/5846437593935e2f8c2aa226
    http://localhost:3000/catalog/book/create


TODO:
/views/author_form.pug :
Note: Some browsers don’t support the input type=“date”, so you won’t get the datepicker widget or the default dd/mm/yyyy placeholder, but will instead get an empty plain text field. One workaround is to explicitly add the attribute placeholder='dd/mm/yyyy' so that on less capable browsers you will still get information about the desired text format.

Problem/Solution
/models/author.js (Problem: we are west of UTC, so dates are converted to localtime when using moment() constructor.)
Note:(this note from MDN express tutorial) If you experiment with various input formats for the dates, you may find that the format yyyy-mm-dd misbehaves. This is because JavaScript treats date strings as including the time of 0 hours, but additionally treats date strings in that format (the ISO 8601 standard) as including the time 0 hours UTC, rather than the local time. If your time zone is west of UTC, the date display, being local, will be one day before the date you entered. This is one of several complexities (such as multi-word family names and multi-author books) that we are not addressing here.
--> Date Issue, using moment(), Explained here: https://maggiepint.com/2016/05/14/moment-js-shows-the-wrong-date/
Solution(for now, but may cause problems later): changed moment constructor from moment() to moment.utc(). //This appears to have solved the problem.


TODO:
delete objects
/views/boodinstance_form.pug
Note: The above template hard-codes the Status values (Maintenance, Available, etc.) and does not "remember" the user's entered values. Should you so wish, consider reimplementing the list, passing in option data from the controller and setting the selected value when the form is re-displayed.

TODO: (from author_delete.pug)
The other pages for deleting objects can be implemented in much the same way. We've left that as a challenge.

TODO:
update objects
/views/book_form.pug
The other pages for updating objects can be implemented in much the same way. We've left that as a challenge.

Challenge yourself

Implement the delete pages for the Book, BookInstance, and Genre models, linking them from the associated detail pages in the same way as our Author delete page. The pages should follow the same design approach:

    If there are references to the object from other objects, then these other objects should be displayed along with a note that this record can't be deleted until the listed objects have been deleted.
    If there are no other references to the object then the view should prompt to delete it. If the user presses the Delete button, the record should then be deleted.

A few tips:

    Deleting a Genre is just like deleting an Author as both objects are dependencies of Book (so in both cases you can delete the object only when the associated books are deleted).
    Deleting a Book is also similar, but you need to check that there are no associated BookInstances.
    Deleting a BookInstance is the easiest of all because there are no dependent objects. In this case, you can just find the associated record and delete it.

Implement the update pages for the BookInstance, Author, and Genre models, linking them from the associated detail pages in the same way as our Book update page.

A few tips:

    The Book update page we just implemented is the hardest! The same patterns can be used for the update pages for the other objects.
    The Author date of death and date of birth fields and the BookInstance due_date field are the wrong format to input into the date input field on the form (it requires data in form "YYYY-MM-DD"). The easiest way to get around this is to define a new virtual property for the dates that formats the dates appropriately, and then use this field in the associated view templates.
    If you get stuck, there are examples of the update pages in the example here(https://github.com/mdn/express-locallibrary-tutorial).
    
