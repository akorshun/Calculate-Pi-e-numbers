# Calculate Pi & e numbers
small student work, labs for matanaliz студенческая лаба
python

## Using Macrolen series (Ряд Маклорена)

    from decimal import * #импортироуем модуль Decimal, дробный тип позволяющий считать более 16 знаков после запятой, аналог float
    getcontext().prec = 100 #устанавливаем кол-во знаков после запятой во всех переменных типа Decimal
    EPS = Decimal(1.0e-100) #устанавливаем нужную точность для подсчета числа E
    #объявлем переменные
    e = Decimal(0)
    f = Decimal(1)
    n = Decimal(0)
    a = Decimal(1)
    #считаем e по ряду Маклорена пока следующий член не окажется больше заданной точности
    while a >= EPS: 
    	e += a #складываем члены ряда Маклорена
    	n += 1
    	f *= n #считаем факториал
    	a = 1 / f #переворачиваем факториал
    
    print(e) #выводим e
    print(n) #печатаем кол-во шагов

## We consider continued fraction (Cчитаем цепную дробь)
![Alt-текст](https://wikimedia.org/api/rest_v1/media/math/render/svg/d9236681f1bda761eaa7325e733bc4f3a48f9661 "From wiki")

    from decimal import *
    getcontext().prec = 1000
    def recurs(i):
        i+=1
        if i < 1000:
            return Decimal(i+i/recurs(i))
        else:
            return Decimal(i+i/(i+1))
    print(Decimal(2+1/recurs(Decimal(0))))

## The Gauss formula and the expansion of the arc tangent in series (Формула Гаусса и разложение арктангенса в ряд)

    from decimal import * #импортироуем модуль Decimal, дробный тип позволяющий считать более 16 знаков после запятой, аналог float
    from math import * #импортируем модуль math для использовния функции fabs(модуля)
    getcontext().prec = 100 #устанавливаем кол-во знаков после запятой во всех переменных типа Decimal
    EPS = Decimal(1.0e-100) #устанавливаем нужную точность для подсчета числа E
    
    def arctan(x): #определяем функию арктангесна для работы с типом Decimal через разложение в степенной ряд
        x = Decimal(x) #объявляем переменные
        n = Decimal(1)
        a = Decimal(x)
        f = Decimal(1)    
        total = Decimal(0)
        sign = Decimal(1)
    
        while fabs(a) >= EPS: #складываем члены степенного ряда до тех пор пока н-ый член не станет меньше нужной нам точности
            a = sign / (n * x ** n) #считаем н-ый член последовательности
            total += sign / (n * x ** n) #складываем члены
            n += 2
            sign = -sign
            
        print(n) #печатаем кол-во шагов
        return total #возвращаем результат функции
    
    pi=Decimal(4*(12*arctan(18) + 8*arctan(57) - 5*arctan(239)))#считаем пи по формуле гаусса и умнодаем на 4
    print(pi)

## Formul of Büley - Boruyna - Plaf (Формула Бэйли — Боруэйна — Плаффа)
    #до тысячи спокойно
    from decimal import *
    getcontext().prec = 100
    pi=Decimal(0)
    i=Decimal(0)
    
    while i < 1000:
    	pi=pi + 1/(16**i)*(4/(8*i+1)-2/(8*i+4)-1/(8*i+5)-1/(8*i+6))	
    	i=i+1
    
    print(pi)
    print(i)

## Chudnovsky's formula (формула чудновского)
    #формула чудновского ищет пи в -1 степени, потом мы переворачиваем число
    #до 1000 спокойно но нудно подождать
    from decimal import *
    from math import *
    getcontext().prec = 1000
    pi = Decimal(0)
    k = 0
    n=1000
    while k < n:
    	pi += (Decimal(-1)**k)*(Decimal(factorial(6*k))/((factorial(k)**3)*(factorial(3*k)))* (13591409+545140134*k)/(640320**(3*k)))
    	k += 1
    pi = pi * Decimal(10005).sqrt()/4270934400
    pi = pi**(-1)
    print(pi)
    print(k)

## Leibnitz formula (формула лейбница) Better dont use it
    # Очень неточно и требуется огромное кол-во циклов для подсчета
    # Более или менее быстро счиетает только с точностью до 7 (совпадет с ПИ до 5 знака)
    import decimal
    decimal.getcontext().prec = 7
    pi = decimal.Decimal(0)
    EPS = decimal.Decimal(1.0e-7)
    n=decimal.Decimal(0)
    s1=decimal.Decimal(0)
    s2=decimal.Decimal(0)
    
    n=n+1;
    s1=s2+4/(2*n-1)
    n=n+1
    s2=s1-4/(2*n-1)
    	
    while (s1-s2)>EPS:
    	n=n+1;
    	s1=s2+4/(2*n-1)
    	n=n+1
    	s2=s1-4/(2*n-1)
    pi=decimal.Decimal((s1+s2)/2)
    print(pi)
    print(n/2)
