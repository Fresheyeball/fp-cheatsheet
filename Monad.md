## Functor
A type(**f**) for which a mapping function can be defined.

__f : \* -> \*__

**map : (a -> b) -> f a -> f b**

functor identity **&forall; x. map id x = x**

functor composition **map (f . g) = map f . map g**

where **id x = x**

## Applyable
A type(**f**) that is a Functor, for which the following operator can be defined.

__f : \* -> \*__

**let <$> = map**

**<$> : (a -> b) -> f a -> f b**

**<*> : f (a -> b) -> f a -> f b**

functor identity **&forall; x. map id x = x**

functor composition **map (h . g) = map h . map g**

associative composition **compose <$> j <*> g <*> h = j <*> (g <*> h)**

## Applicative
A type(**f**) that is a Apply-able (and therefore also a Functor), for which an additional function can be defined **pure**.

__f : \* -> \*__

**let <$> = map **

**<$> : (a -> b) -> f a -> f b**

**<*> : f (a -> b) -> f a -> f b**

**pure : a -> f a**

functor identity **&forall; x. map id x = x**

functor composition **map (h . g) = map h . map g**

associative composition **compose <$> j <*> g <*> h = j <*> (g <*> h)**

applicative identity **pure id <*> x = x**

applicative homomorphism **pure g <*> pure x = pure (g x)**

applicative interchange **x <*> pure y = pure ((flip $) y) <*> x**

## Bindable
A type (**m**) that is an Applicative for which another operator may be defined **bind**.

__m : \* -> \*__

**let <$> = map **

**<$> : (a -> b) -> m a -> m b**

**<*> : m (a -> b) -> m a -> m b**

**pure : a -> m a**

**let >>= = bind**

**>>= : m a -> (a -> m b) -> m b**

functor identity **&forall; x. map id x = x**

functor composition **map (f . g) = map f . map g**

associative composition **compose <$> f <*> g <*> h = f <*> (g <*> h)**

applicative identity **pure id <*> x = x**

applicative homomorphism **pure f <*> pure x = pure (f x)**

applicative interchange **x <*> pure y = pure ((flip $) y) <*> x**

bind associativity **(x >>= f) >>= g = x >>= (&lambda; k. f k >>= g)**

## Monad
A type(**m**) that is Bindable and therefore also (Applicative, Applyable, and a Functor).  To be a Monad two more axioms must be satisfied **left monad identity** and **right monad identity**.

__m : \* -> \*__

**let <$> = map **

**<$> : (a -> b) -> m a -> m b**

**<*> : m (a -> b) -> m a -> m b**

**pure : a -> m a**

**let >>= = bind**

**>>= : m a -> (a -> m b) -> m b**

functor identity **&forall; x. map id x = x**

functor composition **map (f . g) = map f . map g**

associative composition **compose <$> f <*> g <*> h = f <*> (g <*> h)**

applicative identity **pure id <*> x = x**

applicative homomorphism **pure f <*> pure x = pure (f x)**

applicative interchange **x <*> pure y = pure ((flip $) y) <*> x**

bind associativity **(x >>= f) >>= g = x >>= (&lambda; k. f k >>= g)**

left monad identity **pure x >>= f = f x**

right monad identity **x >>= pure = x**
