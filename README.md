import re
import secrets
import string

def analyze_password(password):
    score = 0
    suggestions = []

    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        suggestions.append("Use at least 12 characters.")

    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Add an uppercase letter.")

    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Add a lowercase letter.")

    if re.search(r"\d", password):
        score += 1
    else:
        suggestions.append("Add a number.")

    if re.search(r"[^A-Za-z0-9]", password):
        score += 1
    else:
        suggestions.append("Add a special character.")

    if score <= 2:
        strength = "Weak"
    elif score <= 4:
        strength = "Moderate"
    else:
        strength = "Strong"

    print("\n--- Password Strength Report ---")
    print("Password length:", len(password))
    print("Strength:", strength)

    if suggestions:
        print("\nSuggestions to improve your password:")
        for suggestion in suggestions:
            print("-", suggestion)
    else:
        print("Excellent! Your password meets all basic checks.")

def generate_password(length=14):
    characters = string.ascii_letters + string.digits + "!@#$%&*?"
    return ''.join(secrets.choice(characters) for _ in range(length))

password = input("Enter a test password: ")
analyze_password(password)

print("\nExample of a generated password:", generate_password())