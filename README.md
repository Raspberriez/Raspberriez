# Bookmarks
- [Atomics in Swift](https://medium.com/macoclock/multi-threading-and-race-conditions-in-swift-13f3c8eb25c4)
- [Drag/drop files](https://developer.apple.com/forums/thread/696503)
- [Readme guide](https://dev.to/scottydocs/how-to-write-a-kickass-readme-5af9)

# Todo
- Write a simple client for whisper-rs (???)
- Add .ipa and .app handling (Azula)
- Add pretty colours (Azula)
- Change -c flag to -s (strip), add -t (thin) flag for universal binary on macOS (Azula)
- Check for encryption cryptid == 0 before parsing (Azula)
- Make a simple SwiftUI app for AzulaKit (Azula)
- Separate AzulaKit from Azula CLI (Azula)
- Add multi-method class hooks (Jinx)
- Rewrite shit in Luz (Jinx)
- Add all the SD models I wanna try (Naiad)
- Hopefully fix the fucking 8GB RAM requirement (Naiad)
- Rewrite the app to fix codesign issues (Naiad)

```let reset: String = "\u{001B}[0m"
let faint: String = "\u{001B}[38;5;249m"
let green: String = "\u{001B}[38;5;46m"
let red: String = "\u{001B}[38;5;196m"
let yellow: String = "\u{001B}[38;5;226m"

let info: String = "\(faint)[\(green)*\(faint)]\(reset)"
let warn: String = "\(faint)[\(yellow)!\(faint)]\(reset)"
let error: String = "\(faint)[\(red)!\(faint)]\(reset)"

print(info + " Something happened :)")
print(warn + " Careful, something happened")
print(error + " We fucked.")```
