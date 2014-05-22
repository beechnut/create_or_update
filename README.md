# ActiveRecord#create_or_update

"This should be a gem."


*   *   *


Inspired by [RailSpikes][rs], this method allows you to call `create_or_update` on any model. It is especially useful for seeding data.

This method determines whether a record in your seeds already exists, and updates it if so. If it does not already exist, it creates the record.

This version allows you to pass options, such as `without_protection: true`, to the method. This means that when you seed data, you can update all attributes, including those not made accessible by an `attr_accessible` method.

This avoids those pesky "mass assignment not permitted" errors during seeds.


*   *   *


# Install it!

- If you don't already have a `lib` folder inside `app` (`app/lib`), create one. This is different from the `lib` folder in the root of your project.

- Inside `app/lib`, create a folder called `active_record`.

- Copy `create_or_update.rb` into `app/lib/active_record`.

- If you do not yet have one, in `config/initializers`, create a file called `application.rb`.

- In `config/initializers/application.rb`, write:

```ruby
  require 'active_record'
  require 'active_record/create_or_update'
```


(I'm sorry this isn't a gem. Someday, maybe. I'll totally accept that pull request.)



# Use it!

- Write some seeds as an array of hashes. __Make sure__ to include an `:id` attribute. Here's an example.

In `seeds.rb`:

```ruby
examples = [{id: 1,  title: 'ro',       subtopic_id: 1,  alias: "Renter-Occupied Units (ROUs)"},
            {id: 2,  title: 'roa5',     subtopic_id: 1,  alias: "ROUs Affordable to Households With Incomes Below 50% AMI"},
            {id: 3,  title: 'roa58',    subtopic_id: 1,  alias: "ROUs Affordable to Households With Incomes Between 50-80% AMI"},
            {id: 4,  title: 'roa8',     subtopic_id: 1,  alias: "ROUs Affordable to Households With Incomes Above 80% AMI"},
            {id: 5,  title: 'oo',       subtopic_id: 2,  alias: "Owner-Occupied Units (OOUs)"}]
```

- Loop through the seeds, passing them into `create_or_update`.

In `seeds.rb`:

```ruby
examples.each {|record| ExampleModel.create_or_update(record, without_protection: true)
```

### About "without_protection"

You don't have to include `without_protection: true`. I use it because, in this example, `subtopic_id` is a protected attribute (aka not `attr_accessible`), and removing protection gets around "mass assignment not permitted" errors.








[rs]: http://railspikes.com/2008/2/1/loading-seed-data