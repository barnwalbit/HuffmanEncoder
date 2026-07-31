# Huffman Encoder

A simple C++ implementation of the Huffman coding algorithm. The program builds
a Huffman tree from an input string, generates a variable-length binary code for
each character, encodes the string, and then decodes it to verify the result.

Huffman coding is a lossless compression technique: characters that occur more
frequently are generally assigned shorter codes, while less frequent characters
receive longer codes.

## Features

- Counts the frequency of every character in the input
- Builds a Huffman tree with a min-priority queue
- Generates a binary Huffman code for each character
- Encodes the original text
- Decodes the encoded bit string back to the original text

## Requirements

- A C++ compiler with C++11 support or newer, such as:
  - GCC (`g++`)
  - Clang (`clang++`)

No external libraries are required.

## Build and Run

Using GCC:

```bash
g++ -std=c++11 src.cpp -o huffman_encoder
./huffman_encoder
```

Using Clang:

```bash
clang++ -std=c++11 src.cpp -o huffman_encoder
./huffman_encoder
```

On Windows with MinGW:

```powershell
g++ -std=c++11 src.cpp -o huffman_encoder.exe
.\huffman_encoder.exe
```

## Input

The sample input is currently defined directly in `main()`:

```cpp
string text = "Huffman coding is a data compression algorithm.";
```

Edit this value in `src.cpp` to encode a different non-empty string, then
recompile the program.

## Output

The program prints:

1. The Huffman code assigned to each character
2. The original string
3. The encoded binary string
4. The decoded string

The exact character codes may differ between runs or compilers when characters
have equal frequencies. This is valid as long as the generated codes are
prefix-free and decoding reproduces the original text.

## How It Works

1. Count the occurrences of each character.
2. Create one leaf node per unique character.
3. Insert the nodes into a min-priority queue ordered by frequency.
4. Repeatedly remove the two least-frequent nodes and combine them into a new
   parent node.
5. Traverse left with `0` and right with `1` to generate each character's code.
6. Replace every input character with its code to produce the encoded bit
   string.
7. Traverse the same tree using those bits to reconstruct the original text.

## Complexity

For an input of `n` characters containing `k` unique characters:

- Frequency counting: `O(n)`
- Huffman tree construction: `O(k log k)`
- Encoding and decoding: `O(n)` relative to the processed text/code length
- Space usage: `O(k)` for the frequency table, tree, and code table, excluding
  the encoded output

## Project Structure

```text
.
├── README.md
└── src.cpp
```

## Limitations

- Input is hardcoded rather than read from the command line or a file.
- The implementation demonstrates the algorithm but does not create a
  compressed file format.
- The encoded output is stored as a string of `0` and `1` characters, so it is
  not bit-packed and may use more memory than the original text.
- The current implementation expects a non-empty input containing at least two
  distinct characters.

## License

No license file is currently included. Add a license before redistributing or
reusing the project.
