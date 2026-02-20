# HomeWORK(2).py

class NotEnoughMoney(Exception):
    pass
class WithoutNumbersInTheName(Exception):
    pass
class AnImpossibleAge(Exception):
    pass


def validate_name(name):
    if name == '':
        raise ValueError("Имя не может быть пустым")
    if name.isalpha() == False:
        raise WithoutNumbersInTheName("В имени не должно быть цифр")

def validate_age(age):
    if not(age.isdigit()):
        raise ValueError("Возраст должен быть числом")
    if int(age) <= 12:
        raise ValueError("Слишком маленький возраст")
    if int(age) > 150:
        raise AnImpossibleAge('Слишком большой возраст')


def validate_tickets(count):
    if not(count.isdigit()):
        raise ValueError("Некоректное кол-во билетов")
    tickets = int(count)
    if tickets > 6:
        raise ValueError("Некоректное кол-во билетов")
    if tickets < 0:
        raise ValueError("Некоректное кол-во билетов")

def validate_budget(budget):
    if not(budget.isdigit()) or int(budget) < 0:
        raise ValueError("Некорректный бюджет")

def calculate_total(name, age, tickets, budget):
    total_rate = tickets * 500
    if total_rate > budget:
        raise NotEnoughMoney('НЕДОСТАТОЧНО ДЕНЕГ')
    else:
        remainder = budget - total_rate
        print(f'Результат работы: Ваше имя - {name}, ваш возраст - {age}, кол-во билетов - {tickets}, баланс - {remainder}')
        print(f"Общая стоимость ваших билетов: {total_rate}")


if __name__ == "__main__":
    while True:
        name = input("Введите ваше имя: ").strip()
        try:
            validate_name(name)
            break
        except ValueError as e:
            print(f"Ошибка: {e}. Попробуйте снова.")
        except WithoutNumbersInTheName:
            print('Имя должно быть без цифр')

  while True:
        age = input("Введите ваш возраст: ").strip()
        try:
            validate_age(age)
            age = int(age)
            if age > 150:
                raise AnImpossibleAge("Слишком большой возраст")
            break
        except ValueError as e:
            print(f"Ошибка: {e}. Попробуйте снова.")
        except AnImpossibleAge:
            print('Слишком большой возраст')

  while True:
        tickets = input("Введите количество билетов (1 - 5, Цена 500 за билет): ").strip()
        try:

            validate_tickets(tickets)
            tickets = int(tickets)
            if tickets > 5:
                raise ValueError("Некоректное кол-во билетов")
            if tickets == 0:
                print("Всего доброго! Спасибо, что пришли!")
                exit()
            break
        except ValueError as e:
            print(f"Ошибка: {e}. Попробуйте снова.")

  while True:
        budget = input("Введите ваш бюджет: ").strip()
        try:
            validate_budget(budget)
            budget = int(budget)
            calculate_total(name, age, tickets, budget)
            break
        except ValueError as e:
            print(f"Ошибка: {e}. Попробуйте снова.")
        except NotEnoughMoney as e:
            print(f"Ошибка: {e}. Попробуйте ввести другую сумму.")
