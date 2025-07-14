import random
import string

def generate_password(length, use_digits, use_specials):
    lower = string.ascii_lowercase
    upper = string.ascii_uppercase
    digits = string.digits if use_digits else ''
    specials = string.punctuation if use_specials else ''

    all_chars = lower + upper + digits + specials

    if not all_chars:
        return "Error: No character types selected!"

    # Ensure at least one character from each selected type
    password = [random.choice(lower), random.choice(upper)]
    if use_digits:
        password.append(random.choice(digits))
    if use_specials:
        password.append(random.choice(specials))

    while len(password) < length:
        password.append(random.choice(all_chars))

    random.shuffle(password)
    return ''.join(password)

# User input
try:
    length = int(input("Enter desired password length: "))
    include_digits = input("Include digits? (y/n): ").lower() == 'y'
    include_specials = input("Include special characters? (y/n): ").lower() == 'y'

    if length < 4:
        print("Password length should be at least 4.")
    else:
        password = generate_password(length, include_digits, include_specials)
        print("Generated Password:", password)
except ValueError:
    print("Please enter a valid number for password length.")
