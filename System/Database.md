# Database 

IntegrityError

Exception raised when the relational integrity of the database is affected, e.g. a foreign key check fails. It must be a subclass of DatabaseError.

- for attribute required unique apperance, but try to save one which is not unique

- for an attribute required to be not null, but try to save it with a null value

- If you catch the error you also need a transaction.atomic() between the try and the .create. Otherwise the database will complain about a broken transaction if you do another query after the error (this might be only on postgres).

  > ```python
  > try:
  >     with transaction.atomic():
  >         Employee.objects.create()
  > except IntegrityError as e:
  > 	raise e
  > else:
  >     print('good')
  > ```

