# Wallet Inspector

## Presentation
Wallet Inspector is a web-based tool designed to generate a unique 6-digit security code for wallet addresses. It helps protect users against malicious software that might attempt to replace copied wallet addresses by providing a quick and easy way to verify address integrity.

## How to Use
1. Visit the [Wallet Inspector website](https://yrimbaud.github.io/wallet-inspector/) or download the [iOS app](https://apps.apple.com/app/wallet-inspector/id6667109541)
2. Enter the wallet address you want to verify in the input field.
3. Click the "Generate Security Code" button.
4. Note down the 6-digit code generated.
5. When you paste the address elsewhere, generate the code again and compare it with your noted code.

Please ensure that you have a modern web browser for the best experience.

## Code Explanation
The core of Wallet Inspector is the `generateSixDigitCode` function. Here's a line-by-line explanation of how it works:

```javascript
function generateSixDigitCode(input) {
    let hash = 5381;
    for (let i = 0; i < input.length; i++) {
        hash = (((hash << 5) + hash) + input.charCodeAt(i)) >>> 0;
    }
    return String(hash % 1000000).padStart(6, '0');
}
```

1. `function generateSixDigitCode(input) {`: Declare function that takes an input string.

2. `let hash = 5381;`: Initialize the hash with a prime number (this is part of the djb2 algorithm, known for its good distribution and speed).

3. `for (let i = 0; i < input.length; i++) {`: Start a loop that iterates over each character in the input string.

4. `hash = (((hash << 5) + hash) + input.charCodeAt(i)) >>> 0;`: This is the core of the hashing algorithm:
   - `hash << 5`: Shift the current hash left by 5 bits, equivalent to multiplying by 32.
   - `+ hash`: Add the hash to itself, so it is now `hash * 33`.
   - `+ input.charCodeAt(i)`: Add the ASCII value of the current character.
   - `>>> 0`: Convert the result to an unsigned 32-bit integer.

5. `return String(hash % 1000000).padStart(6, '0');`: 
   - `hash % 1000000`: Take the last 6 digits of the hash.
   - `String(...)`: Convert the number to a string.
   - `.padStart(6, '0')`: Ensure the string is 6 digits long, padding with zeros if necessary.

This function creates a unique, deterministic 6-digit code for any input string, suitable for quick verification purposes.


## Troubleshooting
If you encounter any issues while using Wallet Inspector, please check the following:
- Ensure you're using a modern, updated web browser.
- If the code isn't generating, try refreshing the page or clearing your browser cache.
- For any persistent issues, please contact me.

## iPhone/iPad App
For on-the-go convenience, check out our mobile app designed for iPhone and iPad (requires iOS 16.0 or later):
[!Wallet Inspector on the App Store](https://apps.apple.com/app/wallet-inspector/id6667109541)

## Supporting The Project
If you find this project beneficial and appreciate its contributions, you might consider offering your support. One of the ways you can do this is through a Bitcoin donation!

Here is the Bitcoin address:
`bc1q3pc0ftvdew3e87k07d00k8tqj7ll924hgy69n6`

By donating Bitcoin, you are not only providing tangible assistance, but also endorsing the use of decentralized digital currencies. This encourages further innovation and freedom in the financial sector, aligning with the open source principles that guide this project.

Every donation, big or small, is deeply appreciated and will be used to further improve and maintain this project. Your support helps dedicate more time and resources, ensuring the project's continuity and enhancement!

## Author
This project is maintained by Yann Rimbaud ([yrimbaud](https://github.com/yrimbaud)).

## License
This project is licensed under the MIT License.
