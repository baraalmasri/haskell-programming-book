Write the following functions for processing this data.

```haskell
import Data.Time

data DatabaseItem = DbString String
                  | DbNumber Integer
                  | DbDate UTCTime
                  deriving (Eq, Ord, Show)

theDatabase :: [DatabaseItem]
theDatabase = 
    [ DbDate (UTCTime
                (fromGregorian 1911 5 1)
                (secondsToDiffTime 34123))
    , DbNumber 9001
    , DbString "Hello, world!"
    , DbDate (UTCTime
                (fromGregorian 1921 5 1)
                (secondsToDiffTime 34123))
    ]
```

1. Write a function that filters for DbDate values and returns a list of the UTCTime values inside them.
```haskell
filterDbDate :: [DatabaseItem] -> [UTCTime]
filterDbDate = undefined
```

**Ans**
```haskell
filterDbDate :: [DatabaseItem] -> [UTCTime]
filterDbDate [] = []
filterDbDate dbItems = go dbItems []
  where
    go [] acc = acc
    go (x:xs) acc =
      case x of
        (DbDate utcTime) -> go xs (acc ++ [utcTime])
        otherwise -> go xs acc

-- OR, the foldr version
filterDbDate' :: [DatabaseItem] -> [UTCTime]
filterDbDate' dbItems = foldr go [] dbItems
  where
    go x acc =
      case x of
        (DbDate utcTime) -> utcTime : acc
        otherwise -> acc
```

2. Write a function that filters for DbNumber values and returns a list of the `Integer` values inside them.
```haskell
filterDbNumber :: [DatabaseItem] -> [Integer]
filterDbNumber = undefined
```

**Ans**
```haskell
filterDbNumber :: [DatabaseItem] -> [Integer]
filterDbNumber dbItems = foldr go [] dbItems
  where
    go x acc =
      case x of
        (DbNumber num) -> num : acc
        otherwise -> acc
```