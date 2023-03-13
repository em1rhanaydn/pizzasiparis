# pizzasiparis
import csv
import datetime
class Pizza:
    def get_description(self):
        return self._class.name_

    def get_cost(self):
        return self._class_.get_cost


class Margarita(Pizza):
    cost = 40.0
    def _init_(self):
        self.description="Margarita pizzamiz domates ve kasar esliginde bir harika"
        print(self.description)

class Klasik(Pizza):
    cost = 45.0
    def _init_(self):
        self.description = "Klasik pizzamiz enfes hamuru; sucuk ve salam esliginde bir sölen"
        print(self.description)

class TurkPizza(Pizza):
    cost = 50.0
    def _init_(self):
        self.description =  "Turkpizza lezzeti Ege'in enfes peyniri ve baharatinin sucukla bulusmasidir"
        print(self.description)

class SadePizza(Pizza):
    cost = 40.0
    def _init_(self):
        self.description="Sade pizzamiz lezzeti doruklara ulastirir"
        print(self.description)

class Decorator(Pizza):
    def _init_(self,ekstra):
        self.component = ekstra

    def get_cost(self):
        return self.component.get_cost() + \
        Pizza.get_cost(self)

    def get_description(self):
        return self.component.get_description() + \
        ';' + Pizza.get_description(self)


class Zeytin(Decorator):
    cost = 6.0
    def _init_(self):
        Decorator._init_(self,ekstra)

class Mantar(Decorator):
    cost = 7.0
    def _init_(self, ekstra):
        Decorator._init_(self, ekstra)


class Peynir(Decorator):
    cost = 8.0
    def _init_(self, ekstra):
        Decorator._init_(self, ekstra)


class Et(Decorator):
    cost = 14.0
    def _init_(self, ekstra):
        Decorator._init_(self, ekstra)


class Sogan(Decorator):
    cost = 5.0
    def _init_(self, ekstra):
        Decorator._init_(self, ekstra)


class Misir(Decorator):
    cost = 6.0
    def _init_(self, ekstra):
        Decorator._init_(self, ekstra)

def main():
        dosya = open("Menu.txt", "r")
        oku = dosya.read()
        print(oku)

print("1-Klasik\n"  "2-Margarita\n"  "3-Türk Pizza\n" "4-Sade Pizza \n" "5-Zeytin\n" "6-Mantar\n" "7-Peynir\n" "8-Et\n" "9-Soğan\n" "10-Mısır")
menu={1: Klasik,
      2: Margarita,
      3: TurkPizza,
      4: SadePizza,
      5: Zeytin,
      6: Mantar,
      7: Peynir,
      8: Et,
      9: Sogan,
      10: Misir
      }

print()
kontrol = input("Pizzanizi Seciniz \n")
while kontrol not in ["1","2","3","4"]:
    kontrol = print("Tekrar secim yapiniz \n")

order= menu[int(kontrol)]()

while kontrol != "*":
    kontrol = input("Sos seciniz (Siparisi bitirmek icin '+' giriniz): ")
if kontrol in ["5","6","7","8","9","10"]:
    order = menu[int(kontrol)](order)


print("Sipariş Bilgileri:\n")
isim = input("İsminizi giriniz: ")
ID = input("T.C. kimlik numaranızı giriniz: ")
kk_no = input("Kredi kartı numaranızı giriniz: ")
kk_sifre = input("Kredi kartı şifrenizi giriniz: ")
time = datetime.datetime.now()

with open('Orders_Database.csv', 'a') as orders:
    orders = csv.writer(orders, delimiter=',')
    orders.writerow([isim, ID, kk_no, kk_sifre, order.get_description(), time])


print("Siparişiniz tamamlandı.")
