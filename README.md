### 🖼️ PixelCryptor

PixelCryptor is a beginner-friendly Python tool for encrypting and decrypting images using simple pixel-level XOR manipulation. It is a s

---

#### 🔐 How It Works

The tool applies an XOR operation to each RGB pixel value using a numeric key (0-255). Using the same key, you can decrypt the image back to its original form. While working on this I was able to understand XOR-based obfuscation, practice Python scripting, and explore how data or payloads can be hidden in images for stealthy attacks.

---

#### 🛠️ Setup Instructions

##### 1. I started by creating a folder by running this command on my terminal

```bash
mkdir imagecipher
cd imagecipher
```

---

##### 2. Created the Python Script the would foster the encrytion and decrytion of the image, you can copy and replicate when you try this

```bash
vim cipher.py or nano cipher.py
```
Paste the following code:

```Python

from PIL import Image

def encrypt_image(image_path, key):
    img = Image.open(image_path)
    img = img.convert("RGB")
    encrypted = Image.new("RGB", img.size)
    width, height = img.size

    for x in range(width):
        for y in range(height):
            r, g, b = img.getpixel((x, y))
            encrypted.putpixel((x, y), (r ^ key, g ^ key, b ^ key))

    encrypted.save("encrypted.png")
    print("🔐 Image encrypted and saved as 'encrypted.png'")

def decrypt_image(image_path, key):
    img = Image.open(image_path)
    img = img.convert("RGB")
    decrypted = Image.new("RGB", img.size)
    width, height = img.size

    for x in range(width):
        for y in range(height):
            r, g, b = img.getpixel((x, y))
            decrypted.putpixel((x, y), (r ^ key, g ^ key, b ^ key))

    decrypted.save("decrypted.png")
    print("🔓 Image decrypted and saved as 'decrypted.png'")

def main():
    print("=== PixelCrypt: Image Encryption Tool ===")
    choice = input("Do you want to encrypt or decrypt? ").lower()
    path = input("Enter the image file path (e.g., sample.jpg): ")
    try:
        key = int(input("Enter a numeric key (0-255): "))
    except ValueError:
        print("❌ Invalid key. Must be a number between 0 and 255.")
        return

    if not (0 <= key <= 255):
        print("❌ Key must be between 0 and 255.")
        return

    if choice == 'encrypt':
        encrypt_image(path, key)
    elif choice == 'decrypt':
        decrypt_image(path, key)
    else:
        print("❌ Invalid choice.")

if __name__ == "__main__":
    main()
```


---

 ##### 3. I then installed the pillow library that would help with the image manipulation

```bash

sudo apt install python3-venv
python3 -m venv venv
source venv/bin/activate
pip install pillow

```

---

##### 4. Added an Image for encryption and decryption


```bash
cp ./img.jpg
```

---

##### 5. I then Ran the Program

- 🔒 To Encrypt:

```bash
python3 image_cipher.py
```
Then this pops up, you follow the same steps to encrypt and also decrypt

```text

=== PixelCrypt: Image Encryption Tool ===
Do you want to encrypt or decrypt? encrypt
Enter the image file path (e.g., sample.jpg): img.jpeg
Enter a numeric key (0-255): 255
```
➡️ Output: encrypted.png 


- 🔓 To Decrypt:

```bash
python3 image_cipher.py
```
Input Sample:

```text
Do you want to encrypt or decrypt? decrypt
Enter the image file path (e.g., sample.jpg): encrypted.png
Enter a numeric key (0-255): 255
```
➡️ Output: decrypted.png 

---

##### File Structure

```pgsql

imagecipher/
├── cipher.py
├── img.jpeg
├── encrypted.png
└── decrypted.png

```
---


##### ⚠️ Disclaimer
This tool is for educational purposes only and should not be used for real-world secure image encryption.

