# Campus Cafe Inventory

Compile and run: `javac *.java && java Main`. `output.txt` holds a full test session (all menu options, an invalid price, an invalid product number and an invalid menu choice).

## 1. Warmup.java: prediction vs. actual
I predicted `7 5.0 130` followed by `Two` and `Three`. It printed `7 5.0 -126`, then `Two` and `Three`.
The surprise was `-126`. A byte holds -128 to 127, so casting 130 wraps around (130 - 256 = -126). `(int) 7.9` truncates to 7. The int 5 widens to `5.0` automatically. The switch prints both `Two` and `Three` because there is no `break`, so execution falls through from case 2 into case 3.

## 2. static `totalProducts` vs. instance `name`
`totalProducts` is static, so there is one copy that belongs to the class and is shared by every Product. All objects see the same counter, and it is accessed as `Product.totalProducts`. `name` is an instance variable, so every Product object has its own copy with its own value.

## 3. The copy constructor
`Product(Product other)` creates a new object and copies `name`, `price` and `quantity` from `other` into it, and it also increments `totalProducts`. The new object is separate in memory from the original. Setting `p2.name = "Coffee"` changes only p2's own field, so `p1.name` stays "Tea". (Strings are immutable, so sharing the same String reference is safe.)

## 4. Why `(int) average` is required
Converting a double to an int can lose information (the decimal part and possibly range), so Java won't do it implicitly. It makes you write the cast to show you accept the loss. The cast truncates toward zero and does not round, so 12.75 becomes 12.
