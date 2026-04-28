# UTF-8 Unistring Library

A C++ library for working with UTF-8 encoded strings, providing correct handling of multi-byte characters and essential string operations.

## Features

- **UTF-8 Character Awareness** - Properly handles multi-byte characters (1-4 bytes per code point)
- **Character-Based Indexing** - Access individual characters by their visual position, not byte offset
- **Substring Extraction** - Extract substrings using character indices
- **Case Conversion** - Convert strings to lowercase with support for ASCII and basic Cyrillic characters (including special cases like Yo, I, Ye)
- **Pattern Searching** - Find substrings using the Knuth-Morris-Pratt algorithm for efficient searching
- **String Concatenation** - Concatenate `Unistring` objects with `std::string` and C-strings
- **Equality Comparison** - Compare `Unistring` objects with `std::string` and C-strings

## Building

### Prerequisites

- CMake (version 3.10 or higher)
- C++11 compatible compiler
- Google Test (for running tests)

### Build Instructions

```bash
cd tests/build
cmake ..
make
```

## Usage

### Basic Operations

```cpp
#include "unistring.hpp"

using utf8::Unistring;

// Construction
Unistring str1("Hello, 世界");
Unistring str2 = "Привет мир";
Unistring str3(std::string("C++"));

// Get string length in characters (code points)
size_t len = str1.length();  // Returns character count, not bytes

// Access individual characters
Unistring first_char = str1[0];   // "H"
Unistring last_char = str1[str1.length() - 1];  // "界"

// Convert to lowercase
Unistring lower = str2.to_lower();  // "привет мир"

// Extract substring
Unistring sub = str1.substr(7, 8);  // "世界"

// Find substrings
size_t pos = str1.find("世界");  // Returns character index (7)
size_t pos2 = str1.find("llo", 2);  // Start searching from index 2

// Concatenation
Unistring result = str1 + " " + str2;
str1 += "!";

// Comparison
if (str1 == str2) {
    // Strings are equal
}
```

### Converting to std::string

```cpp
Unistring uni("Some UTF-8 text");
std::string regular_string = uni.to_string();
```

### Working with Character Offsets

```cpp
Unistring str("Hello");
vector<size_t> offsets = str.get_char_offsets();  // Returns byte offsets for each character
```

## UTF-8 Support

The library correctly handles UTF-8 encoded characters across the full Unicode range:

- **1-byte characters**: ASCII (0-127)
- **2-byte characters**: Cyrillic, extended Latin, etc.
- **3-byte characters**: CJK ideographs, special symbols
- **4-byte characters**: Emojis and supplementary characters

## Testing

The project includes comprehensive tests covering:
- Assignment and construction
- Indexing and character access
- String length calculation
- Case conversion
- UTF-8 byte detection
- Substring search (`find` with and without start index)
- String concatenation
- Substring extraction
- Equality comparison

Run the tests after building:

```bash
./unistring_test
```

## Limitations

- `to_lower()` currently supports only ASCII and basic Cyrillic (including special cases: Ё, І, Є)
- `unichar_to_int()` has limited multi-byte character support (currently works with 2-byte characters)
- The `split()` method is marked as TODO

## Dependencies

- C++ Standard Library
- Google Test (for test suite only)

## License

This project is open source and available for use in any project.
