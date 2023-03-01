- Rewrite the app to fix codesign issues
- Test ElleKit on sideloaded

"Some mysteries aren't questions to be answered but just a kind of opaque fact, a thing which exists to be not known"

```
protocol Proto<T> {
    associatedtype T

    var nums: [Int] { get }
    var something: T { get }
}

extension Proto {
    var _test: String {
        return "cccccc"
    }
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
    static func test<T>(nums: [Int]) -> T? {
        if let xx: any Proto = x.first(where: { $0.nums == nums }) {
            return xx.something as? T
        }
        
        return nil
    }
    
    static func test2<T>(nums: [Int]) -> T? {
        if let xx: any Proto = x.first(where: { $0.nums == nums }) {
            return xx._test as? T
        }
        
        return nil
    }
}

typealias Q = (() -> Void)

struct Struct2: Proto2 {
    let structs: [any Proto] = [
        Struct(
            type: Q.self,
            something: { if let ccc: String = test2(nums: [1,2,3]) { print(ccc) } },
            nums: [1, 2, 3]
        ),
        
        Struct(
            type: Q.self,
            something: { if let aaa: Q = test(nums: [1,2,3]) { aaa() } },
            nums: [4, 5, 6]
        )
    ]
    
    func abc<T>() -> T {
        Self.test(nums: [4,5,6])!
    }
}

let z = Struct2()
let abc: Q = z.abc()
abc() // prints "cccccc"
```
