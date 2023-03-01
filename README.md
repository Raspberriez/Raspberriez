- Rewrite the app to fix codesign issues
- Test ElleKit on sideloaded

"Some mysteries aren't questions to be answered but just a kind of opaque fact, a thing which exists to be not known"

```
protocol Proto {
    associatedtype T
    
    var type: T.Type { get }
    var nums: [Int] { get }
    var something: T { get }
}

extension Proto {
    var _test: Int {
        return 6942069
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

typealias AnyClosure = (Any...) -> Void

extension Proto2 {
    static func test(nums: [Int]) -> AnyClosure? {
        if let xx: any Proto = x.first(where: { $0.nums == nums }) {
            return xx.something as? AnyClosure
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
            type: AnyClosure.self,
            something: { x in if let ccc: Int = test2(nums: [1,2,3]) { print(ccc); x.forEach { print($0) } } },
            nums: [1, 2, 3]
        ),
        
        Struct(
            type: AnyClosure.self,
            something: { _ in if let aaa = test(nums: [1,2,3]) { aaa(69, 420, 69420, 42069) } },
            nums: [4, 5, 6]
        )
    ]
    
    func abc() -> AnyClosure {
        Self.test(nums: [4,5,6])!
    }
}

let z = Struct2()
let abc = z.abc()
abc() // prints "6942069\n69\n420\n69420\n42069"
```
