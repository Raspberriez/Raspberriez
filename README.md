- Add all the SD models I wanna try
- Rewrite the app to fix codesign issues
- Test ElleKit on sideloaded
- Add orig for batched hooks
- Add GroupableFunc

"Some mysteries aren't questions to be answered but just a kind of opaque fact, a thing which exists to be not known"


Holy shit I think I got it:

```
protocol Proto<T> {
    associatedtype T

    var nums: [Int] { get }
    var something: T { get }
}

protocol Proto2 {
    var structs: [any Proto] { get }
}

struct Struct<T>: Proto {
    let type: T.Type
    let something: T
    let nums: [Int]
    
    init(type: T.Type, something: T, nums: [Int]) {
        self.type = type
        self.something = something
        self.nums = nums
        x.append(self)
    }
}

var x: [any Proto] = []

extension Proto2 {
    static func test() {
        for y in x {
            print(y.nums)
            print(y.something)
        }
    }
}

struct Struct2: Proto2 {
    let structs: [any Proto] = [
        Struct(
            type: String.self,
            something: "aaaaaa",
            nums: [1, 2, 3]
        ),
        
        Struct(
            type: String.self,
            something: "bbbbbb",
            nums: [4, 5, 6]
        )
    ]
    
    func abc() {
        Self.test()
    }
}

let z = Struct2()
z.abc()
```
