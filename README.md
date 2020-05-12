# unison-money

A Small library for working with Money in Unison

## Install

Note that this library is currently very much in the development and exploration phase.

Install unstable trunk:

```
.> pull git@github.com:hojberg/unison-money.git money
```

## Design

The design of the library is built after a couple of principles. 
1) We want to ensure Money is handled correctly and that money math is sound. The amount is stored as an Int in "cents" (as a term meaning to any minor part of a currency). 
2) It should not be possible to do any math operations of Money of different currencies. This is done by a type variable in the constructor. Currently any type can be added as a currency, though the library does come with a set of currencies. Typeclasses might help tighting up this API in the future.
3) Regular division of Money is tough and doesn't quite make sense because you can't have half a penny. Instead we allow splitting Money where whole remainder is added to one of the chunks: 10 split into 3, results in 3 new Money types, 2 where the amount is 3 and 1 where the amount is 4.

## API

* `Money` Constructor: Create a `Money` value with `Money USD +499` for an amount representing `$ 4.99`
* `Money.toText`: Simply formats the `Money` as a `Text` (in the format of `USD 4.99` with any regard for localized formatting (this will be added later): `Money.toText : Money a -> Text`
* `Money.+` (aliased as `plus`)
* `Money.-` (aliased as `minus`)
* `Money.*` (aliased as `multiply`)
* `Money.split`: Take 1 `Money` and split into `Nat` chunks. Returns a list of the possible splits with whole remainders added to the `Money` values at the end of the list: `Money.split 3 (Money USD +10)` (10 cents) results in `[Money USD +3, Money USD +3, Money USD +4]`

## Planned API
* Formatting function that allows localized formatting of Money
* Percents, for instance for adding 20% tip at a Restaurant.
