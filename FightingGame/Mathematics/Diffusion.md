#cryptography 

[[Confusion]]

[Wikipedia](https://en.wikipedia.org/wiki/Confusion_and_diffusion)

> Diffusion means that if we change a single bit of the plaintext, then about half of the bits in the ciphertext should change, and similarly, if we change one bit of the ciphertext, then about half of the plaintext bits should change.[[5]](https://en.wikipedia.org/wiki/Confusion_and_diffusion#cite_note-5) This is equivalent to the expectation that encryption schemes exhibit an [avalanche effect](https://en.wikipedia.org/wiki/Avalanche_effect "Avalanche effect").

> The purpose of diffusion is to hide the statistical relationship between the ciphertext and the plain text. For example, diffusion ensures that any patterns in the plaintext, such as redundant bits, are not apparent in the ciphertext.[[3]](https://en.wikipedia.org/wiki/Confusion_and_diffusion#cite_note-:0-3) Block ciphers achieve this by "diffusing" the information about the plaintext's structure across the rows and columns of the cipher.

> In substitution–permutation networks, diffusion is provided by [permutation boxes](https://en.wikipedia.org/wiki/Permutation_box "Permutation box") (a.k.a. permutation layer[[4]](https://en.wikipedia.org/wiki/Confusion_and_diffusion#cite_note-FOOTNOTELiuRijmenLeander20181-4)). In the beginning of the 21st century a consensus had appeared where the designers preferred the permutation layer to consist of [linear Boolean functions](https://en.wikipedia.org/wiki/Linearity#Boolean_functions "Linearity"), although nonlinear functions can be used, too.[[4]](https://en.wikipedia.org/wiki/Confusion_and_diffusion#cite_note-FOOTNOTELiuRijmenLeander20181-4)