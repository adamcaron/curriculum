


## Iteration 3: Economic Profile

![Iteration 3](http://imgur.com/RYS8SJs.png)

### `District`

We'll add another relationship:

* `economic_profile` - returns an instance of `EconomicProfile`

### `EconomicProfile`

The instance of this object represents data from the following files:

* `Median household income.csv`

### Analysis/Queries

#### How does kindergarten participation variation compare to the median household income variation?

Does a higher median income mean more kids enroll in Kindergarten? For a single district:

```ruby
ha.kindergarten_participation_against_household_income('ACADEMY 20') # => 1.234
```

Consider the *kindergarten variation* to be the result calculated against the state average as described above.
The *median income variation* is a similar calculation of the district's median income divided by the state average median income.
Then dividing the *kindergarten variation* by the *median income variation* results in `1.234` in the sample.

If this result is close to `1`, then we'd infer that the *kindergarten variation* and the *median income variation* are closely related.

#### Statewide does the kindergarten participation correlate with the median household income?

Let's consider the `kindergarten_participation_against_household_income` and set a correlation window between `0.6` and `1.5`.
If the result is in that range then we'll say that these percentages are correlated. For a single district:

```ruby
ha.kindergarten_participation_correlates_with_household_income(for: 'ACADEMY 20') # => true
ha.kindergarten_participation_correlates_with_household_income(for: 'COLORADO') # => true
```

Then let's look statewide.
If more than some percentage of districts across the state show a correlation, then we'll answer `true`.

```ruby
ha.kindergarten_participation_correlates_with_household_income(for: 'ACADEMY 20') # => true
```

And let's add the ability to just consider a subset of districts:

```ruby
ha.kindergarten_participation_correlates_with_household_income(:across => ['ACADEMY 20', 'YUMA SCHOOL DISTRICT 1', 'WILEY RE-13 JT', 'SPRINGFIELD RE-4']) # => false
```
