# Diffie–Hellman Emoji Exchange.

## Description:

The goal of the crypto is for Alice and Bob to share a secret together; however it is the year 2017; therefore our actors will be Kim and Kanye. Kim and Kanye are always in the public light, and such, there's always someone listening between their communication. For this situation, we'll assume Taylor is always listening between the communication of Kim and Kanye.

Now Kim and Kanye will publicly decide on a public emoji generator and a public prime emoji. They decide on the public prime emoji, 🐕, and the public emoji generator, 🙏. Since they are sharing this publicly, Taylor also knows about 🐕 and 🙏. 

Afterwards, Kim and Kanye will both choose a secret emoji respectively. Kim chooses 🍑 and Kanye chooses 🐐. Kim sends 🙏 <sup> 🍑 </sup> mod 🐕 to Kanye. While Kanye sends 🙏 <sup> 🐐 </sup> mod 🐕 in return  

~~~python
>>> A = pow(ord('🙏'), ord('🍑'), ord('🐕'))
73797
>>> B = pow(ord('🙏'), ord('🐐'), ord('🐕'))
97899
~~~

Taylor will of course have all of this information; however, Kim and Kanye can now use their private secrets.

### Kim
~~~python
>>> pow(97899, ord('🍑'), ord('🐕'))
40332
>>> chr(40332)
鶌
~~~

### Kanye
~~~python
>>> pow(73797, ord('🐐'), ord('🐕'))
40332
>>> chr(40332)
鶌
~~~

They both now have access to a shared secret, 鶌, which Taylor will not be able to access easily. Of course, in a practical scenario, the prime emoji should be much larger such as 🌤😋 (which is 127780128523). We think 8-emojibit primes will be sufficient. One emojibit being one emoji, there a prime emoji with 8 emojis shall be sufficiently large e.g. 👏🦄🐀☃️🍔🚀🚟🚨 is a 8-emojibit number (not prime, it is 12807912941212800...). In version 2 of DHE key exchange, it should require a better map from emoji to number instead of using the Unicode code point as value.

## Symmetric key encryption

Now that Kim and Kanye have a shared secret, which we will swap to 🐍🐍 as to encrypt using a block cipher, we will need at least a 2-emojibit key. 

They will now be able to encrypt messages using a symmetric key encryption so Taylor can not ready any messages or files that Kanye will send to Kim.

## 👻📦🔒 (Block cipher)

### Data

Our message will be "Kim get sum milk" which will be sent by Kanye. We will represent the data as a 4x4 block.

<style>
    .data-table {
        border-collapse: collapse;
    }
    .border-top {
        border: 1px solid #000;
    }
    .border-bottom {
        border: 1px solid #000;
    }
    .border-left {
        bordert: 1px solid #000;
    }
    .border-right {
        bordert: 1px solid #000;
    }
</style>

<table class="data-table">
    <tr></tr>
    <tr>
        <td class="border-bottom border-left border-right">K</td>
        <td class="border-bottom border-right">I</td>
        <td class="border-bottom border-right">M</td>
        <td class="border-bottom border-right"> </td>
    </tr>
    <tr>
        <td class="border-bottom border-left border-right">G</td>
        <td class="border-bottom border-right">E</td>
        <td class="border-bottom border-right">T</td>
        <td class="border-bottom border-right"></td>
    </tr>
    <tr>
        <td class="border-bottom border-left border-right">S</td>
        <td class="border-bottom border-right">U</td>
        <td class="border-bottom border-right">M</td>
        <td class="border-bottom border-right"> </td>
    </tr>
    <tr>
        <td class="border-bottom border-left border-right">M</td>
        <td class="border-bottom border-right">I</td>
        <td class="border-bottom border-right">L</td>
        <td class="border-bottom border-right">K</td>
    </tr>
        <tr></tr>
</table>


### Key

Next is to take our key, 🐍🐍, and convert it to a 4x4 block.

<table class="data-table">
    <tr></tr>
    <tr>
        <td class="border-bottom border-left border-right">1</td>
        <td class="border-bottom border-right">2</td>
        <td class="border-bottom border-right">8</td>
        <td class="border-bottom border-right"> </td>
    </tr>
    <tr>
        <td class="border-bottom border-left border-right"></td>
        <td class="border-bottom border-right">0</td>
        <td class="border-bottom border-right">1</td>
        <td class="border-bottom border-right">3</td>
    </tr>
    <tr>
        <td class="border-bottom border-left border-right">1</td>
        <td class="border-bottom border-right">2</td>
        <td class="border-bottom border-right">8</td>
        <td class="border-bottom border-right"> </td>
    </tr>
    <tr>
        <td class="border-bottom border-left border-right"></td>
        <td class="border-bottom border-right">0</td>
        <td class="border-bottom border-right">1</td>
        <td class="border-bottom border-right">3</td>
    </tr>
        <tr></tr>
</table>


### Encrypting 
For a block cipher, we need to xor each cell individually with the corresponding cell

$Data \bigoplus Key=Ciphertext$