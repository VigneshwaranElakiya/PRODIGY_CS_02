    from PIL import Image

    def encrypt_image(image_path, key):
    try:
        img = Image.open(image_path)
        pixels = img.load()
        width, height = img.size

        for y in range(height):
            for x in range(width):
                r, g, b = pixels[x, y]
                r = (r + key) % 256
                g = (g + key) % 256
                b = (b + key) % 256
                pixels[x, y] = (r, g, b)


        encrypted_image_path = "encrypted_image.png"
        img.save(encrypted_image_path)
        print(f"Image encrypted and saved as {encrypted_image_path}")
        return encrypted_image_path
    except Exception as e:
        print(f"An error occurred: {e}")

    def decrypt_image(encrypted_image_path, key):
    try:
        
        img = Image.open(encrypted_image_path)
        pixels = img.load()

        width, height = img.size

        for y in range(height):
            for x in range(width):
                r, g, b = pixels[x, y]
                r = (r - key) % 256
                g = (g - key) % 256
                b = (b - key) % 256
                pixels[x, y] = (r, g, b)

        decrypted_image_path = "decrypted_image.png"
        img.save(decrypted_image_path)
        print(f"Image decrypted and saved as {decrypted_image_path}")
        return decrypted_image_path
    except Exception as e:
        print(f"An error occurred: {e}")

    if __name__ == "__main__":
    image_path = "download.jpg"
    encryption_key = 87

    encrypted_image_path = encrypt_image(image_path, encryption_key)

    if encrypted_image_path:
        decrypt_image(encrypted_image_path, encryption_key)
