# vladussy_bot
import datetime
import random
import math
import sys

topic_history = []
topics_dictionary = {
    'математика': {
        'найбільший спільний дільник': 'calculate_gcd',
        'найменше спільне кратне': 'calculate_lcm',
        'формула векторного добутку векторів': 'calculate_vector_product',
        'площа трикутника': 'calculate_triangle_area',
        'число Фібоначчі': 'calculate_fibonacci_number'
    },
    'фізика': {
        'закон Кулона': 'calculate_coulomb_law',
        'закон Бойля-Маріотта': 'calculate_boyle_marriott_law'
    },
    'географія': {
        'найбільший океан': 'find_largest_ocean',
        'держава з найбільшою кількістю озер': 'find_country_with_most_lakes',
        'дві держави з найбільшою кількістю водосховищ': 'find_countries_with_most_reservoirs',
        'азимут між точками': 'calculate_azimuth'
    },
    'філологія': {
        'різниця між Some та Any': 'explain_some_and_any',
        'відмінки в українській мові': 'list_ukrainian_cases',
        'роди іменників в українській мові': 'list_noun_genders',
        'часи в англійській мові': 'list_english_tenses'
    },
    'астрономія': {
        'газові гіганти Сонячної системи': 'list_gas_giants',
        'типи зір': 'list_star_types',
        'чорні діри та їх походження': 'explain_black_holes',
        'вплив зоряного світла на здоров\'я': 'impact_of_starlight_on_health'
    },
    'загальні': {
        'поточний час': 'get_current_time',
        'кількість днів до Нового Року': 'calculate_days_until_new_year',
        'вгадай число': 'play_guess_number',
        'Пограти у камінь-ножиці-папір': 'play_rock_paper_scissors',
        'заспівати улюблену пісню': 'sing_favorite_songs'
    }
}


def print_greeting():
    global topics_dictionary
    greeting = f"Вітаю, мене звати vladussy. Ви можете задавати мені питання з наступних тем: {', '.join(topics_dictionary.keys())}."
    print_response(greeting)



def get_user_input():
    return input('[Користувач]: ')


def print_help():
    help_message = ""
    if len(topic_history) == 0:
        help_message += "Введіть назву теми, про яку ви бажаєте дізнатися більше."
    else:
        current_topic = get_current_topic()
        help_message += f"Ви обговорюєте тему '{current_topic}'. Для цієї теми доступні наступні запити:\n"

        if current_topic in topics_dictionary:
            topic_commands = topics_dictionary[current_topic]
            for topic, function_name in topic_commands.items():
                help_message += f"- {topic}\n"

    help_message += "Якщо вам потрібна допомога, скажіть 'допомога'. Щоб повернутися до вибору теми, скажіть 'назад'."
    print_response(help_message)


def get_current_topic():
    if len(topic_history) > 0:
        return topic_history[-1]
    else:
        return None


def get_file_name():
    now = datetime.datetime.now()
    file_name = f'dialog-{now.strftime("%Y-%m-%d_%H-%M")}.txt'
    return file_name

def print_response(text, color='purple'):
    colors = {
        'black': '\033[30m',
        'red': '\033[31m',
        'green': '\033[32m',
        'yellow': '\033[33m',
        'blue': '\033[34m',
        'purple': '\033[35m',
        'cyan': '\033[36m',
        'white': '\033[37m',
        'reset': '\033[0m'
    }
    color_code = colors.get(color.lower(), colors['white'])
    print(f'{colors["reset"]}[Bot]: {color_code}{text}{colors["reset"]}')
    with open(file_name, 'a', encoding='utf-8') as f:
        f.write(f'[Bot]: {text}\n')

def get_user_input():
    return input('[User]: ')


file_name = get_file_name()
with open(file_name, 'a', encoding='utf-8') as f:
    pass





# математика
def calculate_greatest_common_divisor(a, b):
    while b != 0:
        a, b = b, a % b
    return a


def calculate_gcd():
    print_response("Введіть перше число:")
    number1 = int(get_user_input())
    print_response("Введіть друге число:")
    number2 = int(get_user_input())
    gcd = calculate_greatest_common_divisor(number1, number2)
    print_response(f"Найбільший спільний дільник чисел {number1} і {number2}: {gcd}")


def calculate_lcm():
    print_response("Введіть перше число:")
    number1 = int(get_user_input())

    print_response("Введіть друге число:")
    number2 = int(get_user_input())

    gcd = calculate_greatest_common_divisor(number1, number2)

    lcm = (number1 * number2) // gcd

    print_response(f"Найменше спільне кратне: {lcm}")


def calculate_vector_product():
    print_response("Введіть координати першого вектора (x1, y1, z1):")
    x1, y1, z1 = map(float, get_user_input().split())
    print_response("Введіть координати другого вектора (x2, y2, z2):")
    x2, y2, z2 = map(float, get_user_input().split())
    x_product = y1 * z2 - y2 * z1
    y_product = z1 * x2 - z2 * x1
    z_product = x1 * y2 - x2 * y1
    print_response(
        f"Векторний добуток векторів ({x1}, {y1}, {z1}) і ({x2}, {y2}, {z2}): ({x_product}, {y_product}, {z_product})")


def calculate_triangle_area():
    print_response("Введіть координати вершин трикутника (x1, y1), (x2, y2), (x3, y3):")
    x1, y1, x2, y2, x3, y3 = map(float, get_user_input().split())

    side1 = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
    side2 = math.sqrt((x3 - x2) ** 2 + (y3 - y2) ** 2)
    side3 = math.sqrt((x1 - x3) ** 2 + (y1 - y3) ** 2)

    s = (side1 + side2 + side3) / 2
    area = math.sqrt(s * (s - side1) * (s - side2) * (s - side3))

    print_response(f"Площа трикутника з вершинами ({x1}, {y1}), ({x2}, {y2}), ({x3}, {y3}): {area}")


def calculate_fibonacci_number():
    print_response("Введіть номер числа Фібоначчі:")
    n = int(get_user_input())
    if n <= 0:
        print_response("Номер числа Фібоначчі повинен бути більше 0.")
        return
    fibonacci_sequence = [0, 1]
    for i in range(2, n + 1):
        fibonacci_number = fibonacci_sequence[i - 1] + fibonacci_sequence[i - 2]
        fibonacci_sequence.append(fibonacci_number)
    print_response(f"Число Фібоначчі з номером {n}: {fibonacci_sequence[n]}")


# фізика
def calculate_coulomb_law():
    print_response("Введіть значення заряду q1:")
    q1 = float(get_user_input())

    print_response("Введіть значення заряду q2:")
    q2 = float(get_user_input())

    print_response("Введіть відстань між частинками r:")
    r = float(get_user_input())

    k = 9e9  # Значення кулонівської сталої

    force = k * (q1 * q2) / r ** 2
    print_response(f"Сила електростатичної взаємодії між частинками: {force}")


def calculate_boyle_marriott_law():
    print_response("Введіть початковий об'єм V1:")
    v1 = float(get_user_input())

    print_response("Введіть початковий тиск P1:")
    p1 = float(get_user_input())

    print_response("Введіть кінцевий об'єм V2:")
    v2 = float(get_user_input())

    p2 = (p1 * v1) / v2
    print_response(f"Кінцевий тиск за законом Бойля-Маріотта: {p2}")


# географія
def find_largest_ocean():
    largest_ocean = "Тихий океан"
    print_response(f"Найбільший океан: {largest_ocean}")


def find_country_with_most_lakes():
    country_with_most_lakes = "Канада"
    print_response(f"Держава з найбільшою кількістю озер: {country_with_most_lakes}")


def find_countries_with_most_reservoirs():
    countries_with_most_reservoirs = ["США", "Канада"]
    print_response(f"Дві держави з найбільшою кількістю водосховищ: {', '.join(countries_with_most_reservoirs)}")


def calculate_azimuth():
    print_response("Введіть координати першої точки (x1, y1):")
    x1, y1 = map(float, get_user_input().split())

    print_response("Введіть координати другої точки (x2, y2):")
    x2, y2 = map(float, get_user_input().split())

    dx = x2 - x1
    dy = y2 - y1

    azimuth = math.atan2(dy, dx)
    azimuth_degrees = math.degrees(azimuth)
    print_response(f"Азимут між точками: {azimuth_degrees} градусів")


# лінгвістика
def explain_some_and_any():
    explanation = "Some та Any використовуються для позначення невеликої кількості або декількох об'єктів.\n " \
                  "Різниця полягає у використанні з позитивними та негативними твердженнями.\n " \
                  "Some використовується з позитивними твердженнями, наприклад: 'Є деякі студенти в класі'.\n " \
                  "Any використовується з негативними твердженнями або питаннями, наприклад: 'Немає жодних питань?'\n"
    print_response(explanation)


def list_ukrainian_cases():
    cases = ["Називний", "Родовий", "Давальний", "Знахідний", "Орудний", "Місцевий", "Кличний"]
    print_response("Відмінки в українській мові:")
    for i, case in enumerate(cases, start=1):
        print_response(f"{i}. {case}")


def list_noun_genders():
    noun_genders = {
        "чоловічий рід": ["стіл", "дім", "хлопець"],
        "жіночий рід": ["книга", "дівчина", "річка"],
        "середній рід": ["вікно", "сонце", "море"]
    }
    response = "Роди іменників:\n"
    for gender, nouns in noun_genders.items():
        response += f"{gender}:\n"
        for noun in nouns:
            response += f"{noun}\n"
        response += "\n"
    print_response(response)


def list_english_tenses():
    tenses = ["Present Simple", "Present Continuous", "Present Perfect", "Past Simple", "Past Continuous",
              "Past Perfect", "Future Simple"]
    print_response("Темпи в англійській мові:")
    for i, tense in enumerate(tenses, start=1):
        print_response(f"{i}. {tense}")


# астрономія
def list_gas_giants():
    gas_giants = ["Юпітер", "Сатурн", "Уран", "Нептун"]
    print_response("Газові гіганти Сонячної системи:")
    for i, planet in enumerate(gas_giants, start=1):
        print_response(f"{i}. {planet}")


def list_star_types():
    star_types = ["Малі", "Середні", "Великі", "Велетенські", "Супергіганти"]
    print_response("Типи зір:")
    for i, star_type in enumerate(star_types, start=1):
        print_response(f"{i}. {star_type}")


def explain_black_holes():
    explanation = "Чорна діра - це область космічного простору,\n" \
                  "яка має настільки сильне гравітаційне поле, що нічого не може з неї вибратися,\n" \
                  "навіть світло.\n" \
                  "Формується чорна діра внаслідок гравітаційного згортання масивних зір\n" \
                  "після вибуху супернової або унаслідок зіткнення галактик."
    print_response(explanation)


def impact_of_starlight_on_health():
    impact = "Зоряне світло може впливати на наше здоров'я і біологічні ритми.\n " \
             "Наприклад, світло з високим вмістом синьої складової може пригнічувати " \
             "вироблення снодійних речовин і спричиняти порушення сну. Також вважається,\n " \
             "що деякі спектральні лінії в зірковому спектрі можуть мати вплив на наше " \
             "здоров'я і добробут, але це питання вимагає подальших досліджень."
    print_response(impact)


# загальні запитання
def get_current_time():
    current_time = datetime.datetime.now().strftime("%H:%M:%S")
    print_response(f"Поточний час: {current_time}")


def calculate_days_until_new_year():
    current_date = datetime.date.today()
    new_year = datetime.date(current_date.year + 1, 1, 1)
    days_until_new_year = (new_year - current_date).days
    print_response(f"Кількість днів до Нового Року: {days_until_new_year}")


def play_guess_number():
    secret_number = random.randint(1, 10)
    print_response("Гра 'Вгадай число'! Я загадав число від 1 до 10. Спробуйте вгадати!")

    while True:
        try:
            guess = int(get_user_input())
        except ValueError:
            print_response("Будь ласка, введіть ціле число.")
            continue

        if guess < secret_number:
            print_response("Загадане число більше.")
        elif guess > secret_number:
            print_response("Загадане число менше.")
        else:
            print_response("Вітаю! Ви вгадали число!")
            break


def play_rock_paper_scissors():
    options = ["камінь", "ножиці", "папір"]

    while True:
        print_response("Гра 'Камінь-Ножиці-Папір'! Виберіть один з варіантів: камінь, ножиці або папір.")
        user_choice = get_user_input().lower()

        if user_choice not in options:
            print_response("Введено некоректний варіант. Спробуйте ще раз.")
            continue

        bot_choice = random.choice(options)
        print_response(f"Ваш вибір: {user_choice}. Вибір бота: {bot_choice}.")

        if user_choice == bot_choice:
            print_response("Нічия! Спробуйте ще раз.")
        elif (user_choice == "камінь" and bot_choice == "ножиці") or \
                (user_choice == "ножиці" and bot_choice == "папір") or \
                (user_choice == "папір" and bot_choice == "камінь"):
            print_response("Ви виграли!")
            break
        else:
            print_response("Ви програли!")
            break


def sing_favorite_songs():

    favorite_songs = {
        "If I Only Could": "if i only could, i would make a deal with God",
        "Bad Romance": "Ra ra-ah-ah-ah, roma roma-ma, Gaga, ooh la-la",
        "It's My Party": "It's my party and I'll cry if I want to",
        "Hot N Cold": "'Cause you're hot then you're cold, you're yes then you're no",
        "Riptide": "I was scared of dentists and the dark"
    }


    random_song = random.choice(list(favorite_songs.keys()))
    chorus = favorite_songs[random_song]


    print("Singing the chorus of", random_song + ":")
    print(chorus)


def process_user_input(user_input):
    global topic_history

    if user_input == "вихід":
        print_response("До зустрічі!")
        sys.exit()

    if user_input == "назад":
        if len(topic_history) > 0:
            topic_history.pop()
        if len(topic_history) == 0:
            print_greeting()
        else:
            print_help()
        return

    current_topic = get_current_topic()

    if current_topic is None:
        if user_input in topics_dictionary:
            topic_history.append(user_input)
            print_help()
        elif user_input == "допомога":
            print_help()
        else:
            print_response("Виберіть одну з наведених тем.")
    else:
        current_topic_dict = topics_dictionary.get(current_topic)
        if user_input in current_topic_dict:
            topic_function = current_topic_dict[user_input]
            globals()[topic_function]()
        elif user_input == "допомога":
            print_help()
        else:
            print_response("Невірна підтема. Виберіть одну з наведених підтем.")


def main():
    print_greeting()
    while True:
        user_input = get_user_input()
        process_user_input(user_input)


if __name__ == "__main__":
    main()
