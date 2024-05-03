# Text-to-Speech-and-Currency-Conversion-Application

This is a simple Python application that provides two main functionalities:

1. **Text-to-Speech Conversion**: It allows users to convert text input into speech output. The application utilizes the Google Text-to-Speech (gTTS) library to generate audio files from text inputs. The speech output is saved as an MP3 file and played using the default system player.

2. **Currency Conversion**: It enables users to fetch the current exchange rate between two currencies using the ExchangeRate-API. Users can input a base currency and a target currency, and the application retrieves the conversion rate between them.

## Requirements

- Python 3.x
- gtts library
- requests library

## Installation

You can install the required libraries using pip:

```bash
pip install gtts requests
python text_to_speech.py
python currency_conversion.py

Examples
Text-to-Speech Conversion

# text_to_speech.py
from gtts import gTTS
import os

def text_to_speech(text, lang='en'):
    # Create a gTTS object
    tts = gTTS(text=text, lang=lang, slow=False)

    # Save the audio file
    tts.save("output.mp3")

    # Play the audio file
    os.system("afplay output.mp3")  # For macOS
   
if __name__ == "__main__":
    input_text = input("Please enter the text to convert to speech: ")
    text_to_speech(input_text)
Currency Conversion
python
Copy code
# currency_conversion.py
import requests

def fetch_currency_conversion(base_currency, target_currency):
    # API endpoint URL
    url = f"https://api.exchangerate-api.com/v4/latest/{base_currency}"

    try:
        # Send GET request to the API
        response = requests.get(url)
        response.raise_for_status()  # Raise an exception for any HTTP errors

        # Parse the JSON response
        data = response.json()

        # Extract the conversion rate for the target currency
        conversion_rate = data["rates"][target_currency]

        return conversion_rate

    except requests.exceptions.RequestException as e:
        print("Error fetching data from the API:", e)
        return None

if __name__ == "__main__":
    base_currency = input("Enter the base currency (e.g., USD, EUR): ").upper()
    target_currency = input("Enter the target currency (e.g., GBP, JPY): ").upper()

    conversion_rate = fetch_currency_conversion(base_currency, target_currency)
    if conversion_rate is not None:
        print(f"1 {base_currency} = {conversion_rate} {target_currency}")
