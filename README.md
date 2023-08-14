# Cryptanalysis Using Python 


In this project, we experiment with the use of diverse cryptographic algorithms. First, we attempt to encrypt a plaintext message using **Vigenère Algorithm** with a fixed-length encryption key, and afterward, we experiment with the decryption of the produced cipher using **Kasiski's Method**, as well as the **Index of Coincidence** statistical test. For your information, we use [#Python](https://www.python.org/) in combination with Jupyter Notebook as a developing tool.

<br>

## 📢Note📢
**🎯Please, clone this repository before reading the description. Don't forget to like👍and share your thoughts😊.**

<br>

### 1. Encryption -Vigenère Algorithm
This algorithm is based on a polyalphabetic substitution matrix of size 26x26. Each row and column of the matrix correspond to the respective letter of the Latin alphabet. For each row, we fill the respective cells with the letters of the Latin alphabet starting from the row’s index. For example, in the first row, we start from the first letter. To generate the ciphertext through the Vigenère Algorithm, we follow the below procedure: First, we repeat the chosen encryption key as many times as needed to be the same size as the to-be-encrypted text. We iterate through the plaintext and the key tokens. Essentially, what the key does is to determine the amount of shift to apply to the corresponding plaintext character. The shift is based on the position of the respective key character in the alphabet. For example, if the key character is *C*, then we add 2 to the position of the plaintext character in the alphabet. Then, we convert this number back to a letter depending on the polyalphabetic substitution matrix.

<br>

🔎 You can click [here](https://github.com/dmamakas2000/cryptanalysis-python/tree/master/encryption) to check out the code for this method. You can adjust the message to fit your needs. 

<br>

### 2. Decryption - Kasiski's Method
The Vigenère Cipher's strength lies in its resistance to Frequency Analysis, which attributes to the fact that the cipher shifts through various keys, thereby encrypting identical plaintext letters into distinct ciphertext letters. Thus, the most common ciphertext letter may not necessarily correspond to the most common plaintext letter, as in the case where *P* is commonly encrypted as *E*. For many centuries, the Vigenère Cipher was deemed impervious to decryption. However, in 1854, Charles Babbage reportedly decrypted specific variants of the cipher, albeit without publishing his findings. A complete account of how to decrypt the Vigenère Cipher, without prior knowledge of the plaintext or the encryption key, was subsequently published in 1863 by Friedrich Kasiski. 

The Kasiski method, by Friedrich W. Kasiski, is a cryptanalysis technique utilized to break polyalphabetic ciphers. It is based on the main weakness of the security of the Vigenère Cipher, which is the repetition of the key. In other words, Kasiski made a powerful observation; the Vigenère Cipher uses a repetitive keyword for the encryption, such as *KEY*, which leads to the generation of a repeating keystream, such as *KEYKEYKEY...*, to encrypt the plaintext. This leads to the encryption of every n<sup>th</sup> letter – where n is equal to the length of the key, so for the keyword *KEY*, the n<sup>th</sup> letter would be the third letter – using the same Caesar Cipher shift. As a result, the cipher is composed of n – or in this example three – interwoven Caesar Ciphers that can be decrypted using frequency analysis. Therefore, the challenging task is determining the length of the keyword.

In detail, the Kasiski method works by analyzing the ciphertext to detect repeated patterns that could indicate the length of the encryption key. The method is based on the observation that when a sequence of characters in the plaintext is encrypted using the same part of the key, it will produce a repeated sequence in the generated ciphertext. If a substring in the plaintext is encrypted using the same substring in the keyword, the resulting ciphertext will contain a repeated sequence of characters, and the distance between the two occurrences will be a multiple of the length of the keyword. Although not every repeated sequence in the ciphertext arises from this scenario, the likelihood of a chance repetition is significantly lower. Thus, by identifying repeated sequences in the ciphertext and computing the distances between them, we can approximate the length of the encryption key and ultimately decrypt the message. 

Of course, it is necessary to examine multiple repeated patterns, as the detected distance may also be a multiple of the key length. For example, if the distances are 24, 36, and 48, the common factor is 12, which may indicate that the length of the key is a multiple of 12. By reiterating this process for all of the repeated sequences found in the ciphertext, we can obtain several estimates of the length of the key. The rest of the procedure is more of a trial-and-error process, where we try to detect the correct length of the key among the several possible ones. That is why we feel that it is smarter to choose a key of length equal to a power of 2 (e.g. 4, 8, 16, 32, etc.), as it can be broken down into many subfactors and thus the potential encryption keys become more and more as the length increases.

In conclusion, Kasiski's Analysis is a highly significant development in the field of Cryptanalysis, and its impact cannot be overstated. By exploiting the inherent weakness of repeated keys, Kasiski's breakthrough technique provided a new avenue for breaking ciphers that had been thought to be unbreakable for centuries. Despite its effectiveness, we note that the Kasiski Analysis method requires a lengthy intercept to be successful, as n-grams must repeat for frequency analysis to be applied to parts of the message. Overall, the significance of the Kasiski Analysis method cannot be understated, as it revolutionized the field of Cryptography and paved the way for further developments in the ongoing battle between cryptographers and cryptanalysts.

<br>

🔎 You can click [here](https://github.com/dmamakas2000/cryptanalysis-python/tree/master/decryption) to check out the code for this method. Please, use the cipher you produced when experimenting with Vigenère Algorithm.

<br>

### 3. Decryption - Index of Coincidence
In general, the Index of Coincidence is a statistical metric measuring the similarity of a given character sequence to another random character sequence. It is used to calculate the probability of two randomly selected characters in the same sequence being the same. The IoC is calculated by taking the sum of the frequencies of each letter in the sequence multiplied by the same value reduced by 1, and then dividing that by the total number of characters in the sequence multiplied by the total number of characters in the sequence minus one.

In our case, the Index of Coincidence statistical test can be used to analyze ciphertext encrypted by a polyalphabetic substitution cipher. By dividing the ciphertext into groups of letters that were encrypted by the same part of the key, the cryptanalyst (in this case, us) can calculate the index of coincidence for each token group and compare it to the expected index of coincidence for the English language (or any target language in general). In this way, we can finally end up with a small number of potential encryption keys. Afterward, frequency analysis is usually utilized to decrypt the ciphertext and reach the initial message.

<br>

🔎 You can click [here](https://github.com/dmamakas2000/cryptanalysis-python/tree/master/decryption) to check out the code for this method. Please, use the cipher you produced when experimenting with Vigenère Algorithm.

<br>
