## Semigroup
A type (**a**) with a binary operator (**<>**) that is associative.

__a : *__

**<> : a -> a -> a**

associative **&forall; x y z. (x <> y) <> z = x <> (y <> z)**

-- Things that are Semigroups (and nothing more)
  - Integers(&#8484;) with **min** as the operator. **min** is the lower of two Integers, which is associative but has no identity value.
  - Non-empty lists with concatination (**++**), as **++** is associative but without empty list, there is no identity value.
  - Signals

## Monoid
A type that is a Semigroup, but additionally has an identity *value* (**1**).

__a : *__

**<> : a -> a -> a**

associativity **&forall; x y z. (x <> y) <> z = x <> (y <> z)**

**1 : a**

monoid identity **&forall; x. 1 <> x = x = x <> 1**

-- Things that are Monoids (and nothing more)
  - Lists with (**++**, **[]**)  
  - Lots of containers that can be empty
  - Containers that hold a single item, where that item is a Monoid
  - A Maybe of any Semigroup is a Monoid with identity provided by Nothing
  - Arrows where the return type (codomain) is a Monoid. For example

      **<+> : Monoid a => (b -> a) -> (b -> a) -> (b -> a)**

      **f <+> g = &lambda;x. f x <> g x**


## Semiring
A type that is 2 interrelated Monoids at once.

__a : *__

#### Addition Monoid
One of the Monoids must be commutative, we will call it the Addition Monoid (**+**, **0**).

**\+ : a -> a -> a**

associativity **&forall; x y z. (x + y) + z = x + (y + z)**

**0 : a**

monoid identity **&forall; x. 0 + x = x = x + 0**

commutativity **&forall; x y. x + y = y + x**

#### Multiplication Monoid
One of the Monoids must have an annihiliation *value* (**0**), which is the identity of the Addition Monoid, we will call it the Multiplication Monoid (\* , **1**).

**\* : a -> a -> a**

associativity **&forall; x y z. (x \* y) \* z = x \* (y \* z)**

**1 : a**

monoid identity **&forall; x. 1 \* x = x = x \* 1**

annihiliation **&forall; x. 0 \* x = 0 = 0 \* x**

#### Multiplication distributes over Addition

left distributivity **&forall; x y z. x \* (y + z) = (x \* y) + (x \* z)**

right distributivity **&forall; x y z. (x + y) \* z = (a \* z) + (y \* z)**

-- Things that are Semirings (and nothing more)
   - Integers(&#8484;) with ((**+**, **0**),(\* , **1**))
   - Booleans with ((**and**, **True**),(**or**, **False**)) or ((**or**, **False**),(**and**, **True**))
   - Strings with ((**++**, **""**), (**union**, **""**))
   - Reals (potentially Floats) with ((**max**, **&infin;**),(**+**, **0**))
   - Reals (potentially Floats) with ((**min**, **&infin;**),(**+**, **0**))


> Note after this point I am not copying the preceding requirements forward

## ModuloSemiring

A type that is a Semiring ((**+**, **0**),(\* , **1**)) with two additional operators, division (**/**) and mod (**%**).

**/ : a -> a -> a**

**% : a -> a -> a**

remainder **&forall; x y. x / y * y + (x % y) = x**

## Ring

A type that is a semiring ((**+**, **0**),(\* , **1**)) with one additional operator (**&ndash;**), that must be the inverse of the Addition Monoid's operator (**+**).

**&ndash; : a -> a -> a**

additive inverse **&forall; x. x &ndash; x = 0 = (0 &ndash; x) + x**

## DivisionRing

A type that is a Ring as well as a ModuloSemiring
