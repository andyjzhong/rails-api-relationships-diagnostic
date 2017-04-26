# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
    # < Your Response Here >
    Join tables may be valuable when you're trying to combine two or more existing tables and would like the ability to call objects from another table.
  ```

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
    # < Your Response Here >
    Not quite sure what this is asking for... but many Profile can have many Favorites and a Favorite can also have many Movies.
  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base
    has_many :movies, through: :favorites
    has_many :favorites, dependent: :destroy
  end
  ```

  ```rb
  class Movie < ActiveRecord::Base
    has_many :profiles, through: :favorites
    has_many :favorites, dependent: :destroy
  end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
    belongs_to :profile, inverse_of: :favorites
    belongs_to :movie, inverse_of: :favorites
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
    # < Your Response Here >
    It's not entirely clear to me, but I understand that the serializer acts as a filter. Does it filter in attributes that we ONLY want in our tables?
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
    attributes :id, :given_name, :surname, :email
  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
    # < Your Response Here >
    bin/rails generate scaffold :Favorites movie:references profile:references
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
    # < Your Response Here >
    This is saying that if you destroy an object that is part of a joined table, both the object and any secondary objects created inside the joined table will be removed from these tables.
  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
    # < Your Response Here >
    A [Foodie] can have many [Menu Items]] but a [Foodie] can also have many [Orders] which contain many [Menu Items]
  ```
