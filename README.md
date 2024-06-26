import random
from math import gcd
# Функция для нахождения обратного элемента по модулю
def mod_inverse(a, m):
    m0, x0, x1 = m, 0, 1
    if m == 1:
        return 0
    while a > 1:
        q = a // m
        m, a = a % m, m
        x0, x1 = x1 - q * x0, x0
    if x1 < 0:
        x1 += m0
    return x1
# Проверка простоты числа
def is_prime(num):
    if num <= 1:
        return False
    if num <= 3:
        return True
    if num % 2 == 0 or num % 3 == 0:
        return False
    i = 5
    while i * i <= num:
        if num % i == 0 or num % (i + 2) == 0:
            return False
        i += 6
    return True
# Генерация простого числа
def generate_prime_number(length):
    while True:
        prime_candidate = random.getrandbits(length)
        if is_prime(prime_candidate):
            return prime_candidate
# Нахождение числа, взаимно простого с f
def find_special_prime(f):
    while True:
        e = random.randrange(2, f)
        if gcd(e, f) == 1:
            return e
print(" Два разных числа p и q")
p = int(input("p="))
q = int(input("q="))
n = p * q
print("Модуль n равен", n)
f = (p - 1) * (q - 1)
print("Функция Эйлера f равна", f)
e = find_special_prime(f)
print("Случайно подобранное взаимно простое с f число e равно", e)
print("{", e, "},{", n, "} - открытый ключ")
d = mod_inverse(e, f)
print("Число обратное e по модулю f равно:", d)
print("{", d, "}, {", n, "} - закрытый ключ")
P = int(input("Введите сообщение P: "))
E = (P ** e) % n
print("Собеседник получил сообщение E=", E)
A = (E ** d) % n
print("Раскодированное с помощью закрытого ключа:", A
