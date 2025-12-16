# Computational Theory 

A complete implementation of the SHA-256 cryptographic hash function from scratch, built following the [Secure Hash Standard (FIPS 180-4)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf).

## Project Overview

This project implements the SHA-256 algorithm in Python without using any cryptographic libraries. Each problem builds upon the previous one, culminating in a working hash function that can be used to hash arbitrary messages.

## Repository Structure

```
|--- problems.ipynb          #Main notebook with all implementations
|----README.md              #This file
```

## Problems Solved

### Problem 1: Binary Words and Operations
Implementation of fundamental bitwise operations used in SHA-256:
- `Parity(x, y, z)` - XOR operation
- `Ch(x, y, z)` - Choose function
- `Maj(x, y, z)` - Majority function
- `ROTR(x, n)` - Rotate right
- `SHR(x, n)` - Shift right
- `Sigma0(x)`, `Sigma1(x)` - Uppercase sigma functions
- `sigma0(x)`, `sigma1(x)` - Lowercase sigma functions

All operations work with 32-bit unsigned integers using NumPy's `uint32` type.

### Problem 2: Fractional Parts of Cube Roots
Generation of the 64 SHA-256 constants derived from:
- Calculating the first 64 prime numbers
- Computing cube roots of these primes
- Extracting the fractional parts
- Converting to 32-bit hexadecimal constants

These constants are used in the compression function to ensure no hidden backdoors exist in the algorithm.

### Problem 3: Padding
Implementation of the SHA-256 padding scheme as a generator function:
- Processes messages in 512-bit (64-byte) blocks
- Adds required padding: 1 bit, zero bits, and message length
- Ensures final message length is a multiple of 512 bits
- Handles messages of any length efficiently

### Problem 4: Hash Function
The core compression function implementing section 6.2.2 of the standard:
- Message schedule generation (64 words from 16-word block)
- 64 rounds of processing using working variables
- Integration of constants and bitwise operations
- Computation of intermediate hash values

### Problem 5: Password Cracking
Demonstration of SHA-256's vulnerability when used for password storage:
- Dictionary attack implementation
- Recovery of three common passwords from their hashes
- Analysis of why simple hashing is insufficient
- Recommendations for secure password storage (salting, key stretching)

## Requirements

- Python 3.7+
- Jupyter Notebook or JupyterLab
- NumPy

```bash
pip install jupyter numpy
```

## Getting Started

### Running the Notebook

1. **Clone or download this repository**
   ```bash
   git clone <your-repository-url>
   cd <repository-name>
   ```

2. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook
   ```
   This will open Jupyter in your web browser.

3. **Open `problems.ipynb`**
   - Navigate to the file in the Jupyter interface
   - Click to open it

4. **Run the cells**
   - Execute cells sequentially using `Shift + Enter`
   - The notebook is designed to be run from top to bottom

## Testing

The notebook includes comprehensive test suites for each problem:

- **Problem 1**: Tests for edge cases, standard operations, and known patterns
- **Problem 2**: Verification against official SHA-256 constants
- **Problem 3**: Padding tests for various message lengths including boundary cases
- **Problem 4**: Integration tests with known test vectors
- **Problem 5**: Password recovery demonstrations

Run all tests by executing the notebook cells in order.

## Implementation Details

### Key Design Decisions

1. **NumPy uint32**: All arithmetic uses 32-bit unsigned integers to match the SHA-256 specification exactly
2. **Generator for Parsing**: Memory-efficient block processing for large messages
3. **Big-Endian Encoding**: Message length and words use network byte order
4. **Modular Design**: Each problem is self-contained and builds on previous work

## Security Analysis

### Password Storage (Problem 5)

The project demonstrates why SHA-256 alone is insufficient for passwords:

**Vulnerabilities:**
- Fast computation enables dictionary attacks
- No salt means identical passwords produce identical hashes
- Single-pass hashing provides no time delay

**Recommended Improvements:**
1. **Salting**: Add random data to each password
2. **Key Stretching**: Hash multiple times (e.g., 100,000 iterations)

## References

### Primary Sources
- [NIST FIPS 180-4: Secure Hash Standard](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf) - Official specification

### Implementation Guidance
- [GeeksforGeeks: Generate First N Primes](https://www.geeksforgeeks.org/dsa/generate-and-print-first-n-prime-numbers/) - Prime generation algorithm
- [Real Python: Generators](https://realpython.com/introduction-to-python-generators/) - Python generator functions
- [Stack Overflow: Bit Masking](https://stackoverflow.com/questions/10493411/what-is-bit-masking) - Understanding bitwise operations
- [Python Documentation: bytes.to_bytes()](https://docs.python.org/3/library/stdtypes.html#int.to_bytes) - Byte order encoding