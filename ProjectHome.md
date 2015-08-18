## What is this project ##
Hibernate has a very nice SQL mapping called Criteria.  Using criteria makes the code easier to understand and helps ensure that SQL injection does not occur. It also allows for better modularity of the filters and sorts. The main problem I had with criteria is that the building of a filter must be created when the criteria is created. I found myself writing very explicit DataAccessObjects (DAOs) with many functions for each type of sort or filter that was needed.

What has come of those many hours of fiddling with and refactoring is this framework. It allows one to inherit from a single class (one for filters and one for sorts) and define the information that the criteria needs. This allows the View code to only have knowledge of what the fields that need to be sorted or filtered. Then the filter/sort is passed to the DAO and it builds the criteria with the filter and sorts without having to know the fields the front end uses.

## Why is this important ##
The front end (view) should never know the structure of the database (model) and the Data Access Objects (DAO) should never have to know "magic" values from the front end view.

Take a grid (JQuery or the like) they display values on the browser in paginated, sorted and filtered ways. They communicate with the java code by specifying via some set values.
`sortfield=sku, sortdirection=ascending, filterfield=saleprice, filtertype=greaterthan, filtervalue=10.00, page=2, pagesize=20`
It is the front end codes problem to figure out how to convert this to values that the DAO can deal with. Easy but bad solution is to make sure that the front end is using the same database field names. This couples your front and back end together and your whole system is on its way to becoming brittle.

A better way it to have an object that can hold the information so the front end can change the values into the database value (sku => sku\_id) or calls a specific function in the Dao.

The way this library works is your code will be a subclass of the filter and that will provide 3 bits of information the conversion from the front end name to the database value, the type of filter (equals, less than, contains), and the value to test against.  Your front end code sends the correct field, the type of filer and the value to test against. The filter is now passed into the DAO for processing. The DAO then builds the criteria and passes it to the filter that was passed in. The filter will insert into the criteria all the Requirements that are in the filter. Simple as that.

The library is built to allow multiple independent filters. it tries to ensure that a value set will not conflict with another value for the same database field. (sku=k32 and sku=iu4, this would always return nothing since they cannot both be true.)

Add simple code examples to follow