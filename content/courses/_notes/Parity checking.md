**Single-bit parity**
- An additional bit i.e. parity bit is transmitted along with the data frame.
	- The parity bit records if there are odd or even number of 1's in the data frame
- For single-bit error detection, this is useful but fails for even number of incorrect bits 

Example:
Let the original data (D) be 00011
- Parity bit is 1 since there's an odd number of 1's in D.

Due to noise, the transmitted data is 10011
- We detect a bit error since there's an even number of 1's in D. We don't know how to correct this error though.
This will not recognize the error in the following transmission: 11011
- Parity bit is 1 since there's an odd number of 1's in D; but the data is incorrect

**Two-dimensional bit parity**: 
- This alternative lets us correct single bit errors. 
- First, organize sequence of bits in D in a matrix format and calculate the parity bit for each row and column
	- This lets us pinpoint where the error occurred by determining the incorrect row/column parity bit
