## *Checking Type*

*Use the type check operator (`is`) to check whether an instance is of a certain subclass type. The type check operator returns `true` if the instance is of that subclass type and `false` if it’s not.*

*The example below defines two variables, `movieCount` and `songCount`, which count the number of `Movie` and `Song` instances in the `library` array:*

```swift
var movieCount = 0
var songCount = 0

for item in library {
    if item is Movie {
        movieCount += 1
    } else if item is Song {
        songCount += 1
    }
}

print("Media library contains \(movieCount) movies and \(songCount) songs")
// Prints "Media library contains 2 movies and 3 songs"
```

*This example iterates through all items in the `library` array. On each pass, the `for`-`in` loop sets the `item` constant to the next `MediaItem` in the array.*

*`item is Movie` returns `true` if the current `MediaItem` is a `Movie` instance and `false` if it’s not. Similarly, `item is Song` checks whether the item is a `Song` instance. At the end of the `for`-`in` loop, the values of `movieCount` and `songCount` contain a count of how many `MediaItem` instances were found of each type.*
