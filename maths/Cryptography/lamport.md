# Lamport signatures

## generate keys

Let's say we have some hash function, where the hashes are $n$ bits long:

$$h(m) = \text{hash of } m\text{, such that }h(m)\text{ is }n\text{ bits.}$$

Then, we can roll some $2n$ random numbers of length $n$ as our private key:

$$\text{Private}_i = \text{RandomBits}(n) \text{, for each } i \in [0, 2n - 1]$$

After that, we take the hash of those numbers as our public key:

$$\text{Public}_i = h(\text{Private}_i)\text{, for each } i \in [0, 2n - 1]$$

## sign a message

Start by hashing the message you want to send:

$$a = h(\text{message})$$

Then, for each bit in the hash, chose either the first or second hash in each of the two pairs of private numbers we rolled.
