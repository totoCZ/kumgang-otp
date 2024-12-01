# kumgang-otp
OTP generator once used "in production" to generate 2of2 secure storage of highly sensitive encryption keys.

## As explaind by Gogole:

<ol>
<li>
<p><strong>Encoding and Decoding Dictionaries:</strong></p>
<ul>
<li>
<p>encode_chars: Maps characters (letters, numbers, punctuation) to their numeric representations (strings like "1", "70", "00").</p>
</li>
<li>
<p>decode_chars: The reverse mapping, from numeric strings back to characters.</p>
</li>
<li>
<p>decode_tidyup: Used to handle special cases for numbers (e.g., "00" maps to "###zero###" and then gets tidied up to "0").</p>
</li>
</ul>
</li>
<li>
<p><strong>random_otp():</strong></p>
<ul>
<li>
<p>Generates a random one-time pad (OTP).</p>
</li>
<li>
<p>It creates a large Uint32Array of random numbers.</p>
</li>
<li>
<p>Joins it all in one string.</p>
</li>
<li>
<p>splits it in an array of strings of size 5</p>
</li>
<li>
<p>formats it in blocks of 5 separated by spaces, with newlines after every 10 blocks.</p>
</li>
</ul>
</li>
<li>
<p><strong>encrypt():</strong></p>
<ul>
<li>
<p>Gets the plaintext message and the OTP from the input fields.</p>
</li>
<li>
<p><strong>Numeralization:</strong> Converts the plaintext message into a string of numbers using the encode_chars dictionary.</p>
<ul>
<li>
<p>If a character is not found in the dictionary, it's replaced with "."</p>
</li>
<li>
<p>Pads the numeralized message with "0"s to make its length a multiple of 5.</p>
</li>
</ul>
</li>
<li>
<p><strong>OTP Handling:</strong></p>
<ul>
<li>
<p>Checks if the OTP is valid (only numeric digits).</p>
</li>
<li>
<p>Warns the user if the OTP is too short and gives the option to continue (with a weakened encryption) or not. Repeats the OTP to make it of sufficient length if the user agrees to proceed with weakened security.</p>
</li>
</ul>
</li>
<li>
<p><strong>Encryption:</strong> Performs digit-by-digit subtraction (modulo 10) of the numeralized message and the OTP to get the ciphertext.</p>
</li>
<li>
<p><strong>Formatting:</strong> Formats the ciphertext into blocks of 5 digits separated by spaces, with newlines after every 10 blocks.</p>
</li>
</ul>
</li>
<li>
<p><strong>decrypt():</strong></p>
<ul>
<li>
<p>Gets the ciphertext and the OTP from the input fields.</p>
</li>
<li>
<p><strong>Input Validation:</strong> Checks if the ciphertext and OTP are valid (only numeric digits).</p>
</li>
<li>
<p><strong>OTP Handling:</strong> Warns the user if the OTP is too short (potentially indicating a compromised key or interception). Repeats the OTP to make it of sufficient length.</p>
</li>
<li>
<p><strong>Decryption:</strong> Performs digit-by-digit addition (modulo 10) of the ciphertext and the OTP to recover the numeralized message.</p>
</li>
<li>
<p><strong>Denumeralization:</strong> Converts the numeralized message back to plaintext using the decode_chars dictionary.</p>
<ul>
<li>
<p>Handles the special numeric cases using decode_tidyup.</p>
</li>
</ul>
</li>
</ul>
</li>
</ol>
