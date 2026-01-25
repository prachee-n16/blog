**Notation**
- D: original datagram being transmitted to receiver
- EDC: Error detection and Error correction bits 
- D' or EDC': Since data can change during transmission, we use `'` to signify these are the bits received on the other end (and may be different from original data)

The three common methods to detect/correct errors are:
- [[Parity checking]]
- [[CRC]]
