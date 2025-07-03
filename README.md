# Currency-converter
import requests

# Function to get the exchange rate from the API
def get_exchange_rate(base_currency, target_currency):
    url = f"https://v6.exchangerate-api.com/v6/YOUR-API-KEY/latest/{base_currency}"
    response = requests.get(url)
    data = response.json()
    
    if response.status_code == 200 and data.get("result") == "success":
        exchange_rate = data["conversion_rates"].get(target_currency)
        if exchange_rate:
            return exchange_rate
        else:
            print(f"Exchange rate for {target_currency} not found.")
    else:
        print("Error: Unable to fetch exchange rate data.")
    return None

# Function to convert the currency
def convert_currency(amount, base_currency, target_currency):
    rate = get_exchange_rate(base_currency, target_currency)
    if rate:
        return amount * rate
    else:
        print("Conversion failed due to invalid rate.")
        return None

# Main program to interact with the user
def main():
    print("Welcome to the Currency Converter!")
    base_currency = input("Enter the base currency (e.g., USD, EUR): ").upper()
    target_currency = input("Enter the target currency (e.g., INR, GBP): ").upper()
    amount = float(input(f"Enter the amount in {base_currency}: "))
    
    converted_amount = convert_currency(amount, base_currency, target_currency)
    if converted_amount:
        print(f"{amount} {base_currency} is equal to {converted_amount:.2f} {target_currency}")
    else:
        print("Conversion could not be completed.")

if __name__ == "__main__":
    main()
