# PHP Hashing Coursework

Completed as part of a PHP certification course on Coursera. This is an introductory exercise focused on PHP's hashing functions.

A small set of PHP web pages built as a coursework assignment exploring cryptographic hash functions. The project demonstrates generating hashes (SHA-256 and MD5) and reversing a weak hash by brute force.

> **Note:** This is a learning exercise. MD5 is cryptographically broken and the brute-force "cracker" only works because a 4-digit PIN has just 10,000 possible values. None of this should be used for real security.

## Project structure

```
.
├── assignment1/
│   └── index.php      # SHA-256 hash + ASCII art
└── assignment2/
    ├── index.php      # MD5 cracker
    └── md5.php        # MD5 encoder
```

## Contents

### Assignment 1 — `assignment1/index.php`
A static page that:
- Generates and prints the **SHA-256 hash** of a fixed string using PHP's `hash()` function.
- Displays a small piece of ASCII art.

### Assignment 2 — `assignment2/index.php` and `assignment2/md5.php`

**`index.php` — MD5 Cracker**
Takes an MD5 hash of a 4-digit PIN (submitted via a form) and attempts to recover the original PIN. It does this by hashing every possible 4-digit combination (`0000`–`9999`) and comparing each result against the target hash until it finds a match. The page also reports the elapsed time for the search and shows a short sample of debug output.

**`md5.php` — MD5 Encoder**
A simple companion tool: enter any text and it returns the MD5 hash of that text. Useful for generating a hash to then feed into the cracker.

## How it works

All three pages rely on PHP's built-in hashing functions. The PHP `hash()` function generates a hash value based on the hashing algorithm passed as its first parameter, so the same function produces both the SHA-256 and MD5 digests used here.

The cracker works through nested loops over the digits `0`–`9` across four positions, building each candidate PIN, hashing it with MD5, and breaking out of all loops once a match is found. Because the search space is tiny, this completes almost instantly.

## Why MD5 is used here (and why you shouldn't elsewhere)

MD5 is intentionally used in this assignment because its weaknesses make the brute-force demonstration possible. In practice it is unsuitable for securing sensitive data: MD5 is susceptible to collision attacks, where two different inputs can produce the same hash value, which makes it unreliable for cryptographic security. For real password storage, PHP's `password_hash()` (which defaults to bcrypt) is the appropriate choice.

## Running the project

These pages need a PHP-capable web server. The simplest options:

**Using PHP's built-in server**
```bash
# From the project folder
php -S localhost:8000
```
Then open `http://localhost:8000/assignment1/` or `http://localhost:8000/assignment2/` in a browser.

**Using XAMPP / similar**
Drop the `assignment1` and `assignment2` folders into your `htdocs` directory and visit them through `localhost`.

### Trying the cracker
1. Open the MD5 Encoder page (`assignment2/md5.php`) and hash a 4-digit number (e.g. `1234`) to get its MD5 digest.
2. Paste that digest into the MD5 Cracker page (`assignment2/index.php`) and submit.
3. The page recovers the original PIN and reports how long the search took.

## Built with

- PHP (built-in `hash()` function)
- Plain HTML for the page structure and forms

## Author

Prem Sharma
