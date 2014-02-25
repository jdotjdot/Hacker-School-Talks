Crazy Haskell Types Talk
=====================
<br>
What we'll be covering today:
* type classes
* "intense" category theory
*


    a + b
    a == b

    Standard ML         OCaml
    a + b               a + b (+) : Int > Int > Int

So when designing Haskell, they wanted to do it in a better way, so they created class types:

    class Addable a where
        (+) :: a -> a -> a
    instance Addable Int where
        a + b = addInt a b

    class Mappable container where
        map :: (a -> b) -> container a -> container b


    data Maybe a = Just a | Nothing
    data Either a b = Left a | Right b

So regarding class `Mappable`, the `containers` could be one of a couple `container` types, possibly `Maybe`s or `Either`s.  Other examples of containers are `List`, `Set`, `Dict`.

    instance Mappable Maybe where
    mapofmaybe =
        case maybe of
            Just x -> Just (fx)
            Nothing -> Nothing

So in this case, a `Maybe a` is a structure that may or may not contain an `a`, and that's it.

All of the below structures like `map`, `zip`, and `join` all enable you to do operations, etc., but with `Maybe`s.

A monad is a structure that can be collapsed without loss of information

    map/lift: (a + b) -> container a -> container b
    zip/lift2: (a -> b -> c) -> container a -> container b -> container c
    join: container (container a) -> container a

    map is a functor
    zip is a functor and applicative
    join is a functor, applicative, and monad

    map - reaching into a container
    lift2 - combining contianer
    monad - un-nesting containers

    lift3 would be taking 3 containers and combining them at the end
    lift can really be any liftn


    liftz f ma mb =
        case (ma, mb) of
            (Just a, Just b) -> Just (f a b)
                             -> Nothing


    Another way to write join:
    [[1,2], [3,4]] -> [1, 2, 3, 4]

    sqrt :: Int -> Maybe Int
    four :: Maybe Int
    let four = sqrt 16
    two :: Maybe
    two = join (map sqrt four)

    # Just creates Maybes
    Just 4 :: Maybe Int
    Just :: a -> Maybe a

    lift2 (,) [1,2] [3,4] == [(1,3), (2,4)]

    does File Exist :: String -> IO Bool
    read File :: String -> IO String

    safeRead :: Bool -> String -> IO String
    safeRead :: exists =
        ifexists then map Just (readFile name)
                 else lift0 ""

    Functor: (<$>): (a -> b) -> f a -> f b
    Applicative: (<*>): f (a -> b) -> f a -> f b
    Monad: (>>=): m a -> (a -> m b) -> m b

    f<*> a lift2 (\lambda f' a' -> f' a') f a

    m >>= f =
        case mof
            Just x -> f x
            Nothing-> Nothing


<br><br>