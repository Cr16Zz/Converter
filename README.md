# Converter
import requests

API_KEY = '99c699a371bf0efcea5da375'  # Ваш API-ключ
BASE_URL = 'https://api.exchangerate-api.com/v4/latest/RUB'  # Базовый URL для API

def get_exchange_rates():
    url = f"{BASE_URL}?app_id={API_KEY}"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        return data['rates']
    else:
        print("Ошибка при получении данных с API")
        return None

def convert_rub_to_usd(amount, rates):
    if 'RUB' in rates and 'USD' in rates:
        rub_to_usd_rate = rates['USD'] / rates['RUB']
        return amount * rub_to_usd_rate
    else:
        print("Не удалось найти необходимые курсы валют.")
        return None

def main():
    print("Добро пожаловать в конвертер валют!")
    rates = get_exchange_rates()
    if rates:
        while True:
            user_input = input("Введите сумму в рублях (или 'exit' для выхода): ")
            if user_input.lower() == 'exit':
                print("Выход из программы.")
                break
            try:
                rub_amount = float(user_input)
                usd_amount = convert_rub_to_usd(rub_amount, rates)
                if usd_amount is not None:
                    print(f"{rub_amount} рублей равны {usd_amount:.2f} долларов.")
            except ValueError:
                print("Пожалуйста, введите корректное числовое значение.")

if __name__ == "__main__":
    main()
