# Track-polio-tracker
# Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOGL": 150,
    "MSFT": 200,
    "AMZN": 130
}

# Initialize portfolio and investment
portfolio = {}
total_investment = 0

print("Enter your stock portfolio. Type 'done' to finish.\n")

while True:
    stock = input("Enter stock symbol (e.g., AAPL): ").upper()

    if stock == "DONE":
        break

    if stock not in stock_prices:
        print("Stock not recognized. Available stocks:", list(stock_prices.keys()))
        continue

    try:
        quantity = int(input(f"Enter number of shares for {stock}: "))
        if quantity < 0:
            raise ValueError
        portfolio[stock] = portfolio.get(stock, 0) + quantity
    except ValueError:
        print("Please enter a valid positive number.")

# Print portfolio summary
print("\n--- Portfolio Summary ---")
print(f"{'Stock': <10}{'Quantity': <10}{'Price': <10}{'Total Value': <15}")
print("-" * 45)

csv_lines = ["Stock,Quantity,Price,Total Value"]

for stock, qty in portfolio.items():
    price = stock_prices[stock]
    value = price * qty
    total_investment += value

    print(f"{stock: <10}{qty: <10}{price: <10}${value:<15}")
    csv_lines.append(f"{stock},{qty},{price},{value}")

print(f"\nTotal Investment Value: ${total_investment}")

# Simulate saving to file: Print CSV output
print("\n--- CSV Output ---")
for line in csv_lines:
    print(line)
