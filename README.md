- Rewrite the app to fix codesign issues
- Test ElleKit on sideloaded
- Convert array to closure args???

"Some mysteries aren't questions to be answered but just a kind of opaque fact, a thing which exists to be not known"

```
protocol Proto<T> {
    associatedtype T

    var nums: [Int] { get }
    var something: T { get }
}

extension Proto {
    var _orig: String {
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
    static func orig<T>(_ nums: Any...) -> T? {
        if let xx: any Proto = x.first(where: { $0.nums == (nums[0] as! [Int]) }) {
            return xx.something as? T
        }
        
        return nil
    }
    
    static func orig2<T>(_ nums: Any...) -> T? {
        if let xx: any Proto = x.first(where: { $0.nums == (nums[0] as! [Int]) }) {
            return xx._orig as? T
        }
        
        return nil
    }
}

typealias Q = (Any...) -> Void

struct Struct2: Proto2 {
    let structs: [any Proto] = [
        Struct(
            type: Q.self,
            something: { _ in if let ccc: String = orig2([1,2,3]) { print(ccc) } },
            nums: [1, 2, 3]
        ),
        
        Struct(
            type: Q.self,
            something: { _ in if let aaa: Q = orig([1,2,3]) { aaa() } },
            nums: [4, 5, 6]
        )
    ]
    
    func abc<T>() -> T {
        Self.orig([4,5,6])!
    }
}

let z = Struct2()
let abc: Q = z.abc()
abc() // prints "cccccc"
```
