```swift
extension String {
    var containsChineseCharacters: Bool {
        return self.range(of: "\\p{Han}", options: .regularExpression) != nil
    }
}

if myString.containsChineseCharacters {
    print("Contains Chinese")
}
```

```swift
enum ChineseRange {
    case notFound, contain, all
}

extension String {
    var findChineseCharacters: ChineseRange {
        guard let a = self.range(of: "\\p{Han}*\\p{Han}", options: .regularExpression) else {
            return .notFound
        }
        var result: ChineseRange
        switch a {
        case nil:
            result = .notFound
        case self.startIndex..<self.endIndex:
            result = .all
        default:
            result = .contain
        }
        return result
    }
}

if "你好".findChineseCharacters == .all {
    print("All Chinese")
}

if "Chinese".findChineseCharacters == .notFound {
    print("Not found Chinese")
}

if "Chinese你好".findChineseCharacters == .contain {
    print("Contains Chinese")
}
```

#iOS