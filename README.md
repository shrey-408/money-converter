# money-converter
# Install requests if not already installed
!pip install requests

# Import the required libraries
import requests

# Function to fetch real-time exchange rates
def get_exchange_rate(api_key, from_currency, to_currency):
    # Updated URL with the correct API endpoint for free-tier users
    url = f"https://v6.exchangerate-api.com/v6/{api_key}/pair/{from_currency}/{to_currency}"

    # Send request to the API
    response = requests.get(url)

    # Check if the request was successful
    if response.status_code == 200:
        data = response.json()
        return data['conversion_rate']  # Fetch conversion rate directly from the response
    else:
        print(f"Error: Unable to fetch data. Status code: {response.status_code}")
        return None

# Function to convert currency
def convert_currency(api_key, from_currency, to_currency, amount):
    rate = get_exchange_rate(api_key, from_currency, to_currency)

    if rate is not None:
        converted_amount = amount * rate
        return converted_amount
    else:
        return None

# Main program
def main():
    api_key = "5f044286fdf3ccf8ad2e8b7a"  # Get your free API key from https://www.exchangerate-api.com/

    print("Welcome to the Real-Time Currency Converter!")

    # Get user inputs
    from_currency = input("Enter the base currency (e.g., USD): ").upper()
    to_currency = input("Enter the target currency (e.g., EUR): ").upper()
    amount = float(input(f"Enter the amount in {from_currency}: "))

    # Perform conversion
    converted_amount = convert_currency(api_key, from_currency, to_currency, amount)

    if converted_amount is not None:
        print(f"{amount} {from_currency} is equal to {converted_amount:.2f} {to_currency}.")
    else:
        print("Conversion failed. Please try again.")

# Run the main function
if __name__ == "__main__":
    main()
