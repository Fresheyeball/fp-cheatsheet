## Functor
A type(**f**) for which a mapping function can be defined.

__f : \* -> \*__

**map : (a -> b) -> f a -> f b**

functor identity **&forall; x. map id x = x**

functor composition **map (f . g) = map f . map g**

where **id x = x**

-- Things that are Functors (and nothing more)
   Seriously, I can't find even one. There may be one out there, but right now it seems like Applyable is really just part of the properties of Functors

## Applyable
A type(**f**) that is a Functor, for which the following operator(__<*>__) can be defined. Worth noting that lifting is a concept from Applyable. For example
  - **lift g a = g <$> a** aka **lift = map**
  - __lift2 g a b = g <$> a <\*> b__
  - __lift3 g a b c = g <$> a <\*> b <\*> c__

__f : \* -> \*__

**<$> = map**

**<$> : (a -> b) -> f a -> f b**

__<\*> : f (a -> b) -> f a -> f b__

functor identity **&forall; x. map id x = x**

functor composition **map (h . g) = map h . map g**

associative composition __compose <$> j <\*> g <\*> h = j <\*> (g <\*> h)__

-- Things that are Applyable (and nothing more)
  - A Tuple in which the first value is filled out. IE: **(Int, )** is a Functor on the right hand value, but *not* applicative as its impossible to define **pure** as it would need to be **: a -> (r, a)** without knowing **r**.
  - Its possible to write several examples that are Applyable but not Applicative, however they don't seem to be useful for programming. For example **data Phantom x = Phantom { void :: Void }** it is possible to write out **map** and __<*>__ in a destructive fashion (since x is never used and void can never be accessed), but **pure** cannot be defined since it would result in **&bottom;** which would be absurd.

## Applicative
A type(**f**) that is a Apply-able (and therefore also a Functor), for which an additional function can be defined **pure**.

__f : \* -> \*__

__<$> = map__

**<$> : (a -> b) -> f a -> f b**

__<\*> : f (a -> b) -> f a -> f b__

**pure : a -> f a**

functor identity **&forall; x. map id x = x**

functor composition **map (h . g) = map h . map g**

associative composition __compose <$> j <\*> g <\*> h = j <\*> (g <\*> h)__

applicative identity **pure id <*> x = x**

applicative homomorphism **pure g <*> pure x = pure (g x)**

applicative interchange __x <\*> pure y = pure ((flip $) y) <\*> x__

-- Things that are Applicative (and nothing more)
  - Signals
  - Validation (think form validation as a type)

## Bindable
A type (**m**) that is an Applicative for which another operator may be defined **bind**.

__m : \* -> \*__

__<$> = map__

**<$> : (a -> b) -> m a -> m b**

**<*> : m (a -> b) -> m a -> m b**

**pure : a -> m a**

**>>= = bind**

**>>= : m a -> (a -> m b) -> m b**

functor identity **&forall; x. map id x = x**

functor composition **map (h . g) = map h . map g**

associative composition __compose <$> j <\*> g <\*> h = j <\*> (g <\*> h)__

applicative identity **pure id <*> x = x**

applicative homomorphism **pure g <*> pure x = pure (g x)**

applicative interchange __x <\*> pure y = pure ((flip $) y) <\*> x__

bind associativity **(x >>= f) >>= g = x >>= (&lambda; k. f k >>= g)**

## Monad
A type(**m**) that is Bindable and therefore also (Applicative, Applyable, and a Functor).  To be a Monad two more axioms must be satisfied **left monad identity** and **right monad identity**. Monads also get a new function for free of note **join**, which works for all Monads.

**pure** is also renamed to **return**. It is more idiomatic to use **pure** when your code is about Applicative, but use **return** when your code is more Monadic, even though they do the same thing. There is also an argument to be made for not having **return** is the name is confusing.

__m : \* -> \*__

__<$> = map__

**<$> : (a -> b) -> m a -> m b**

**<*> : m (a -> b) -> m a -> m b**

**pure : a -> m a**

**return = pure**

**>>= = bind**

**>>= : m a -> (a -> m b) -> m b**

functor identity **&forall; x. map id x = x**

functor composition **map (h . g) = map h . map g**

associative composition __compose <$> j <\*> g <\*> h = j <\*> (g <\*> h)__

applicative identity **pure id <*> x = x**

applicative homomorphism **pure g <*> pure x = pure (g x)**

applicative interchange __x <\*> pure y = pure ((flip $) y) <\*> x__

bind associativity **(x >>= f) >>= g = x >>= (&lambda; k. f k >>= g)**

left monad identity **&forall; x. pure x >>= f = f x**

right monad identity **&forall; x. x >>= pure = x**

**join : m (m a) -> m a** (the join instance for lists is **flatten** in lodash speak)
