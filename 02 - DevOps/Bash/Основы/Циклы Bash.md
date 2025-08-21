---
Тема: Ansible
tags:
  - DevOps
  - Bash
  - review
Дата: 23-11-2023
sr-due: 2025-08-24
sr-interval: 4
sr-ease: 270
---
# Цикл for-in
Предназначен для поочередного обращения к значениям перечисленным в списке. Каждое значение поочередно в списке присваивается переменной.

Пример синтаксиса:
```bash
for переменная in список_значений  
do  
команды  
done
```

Пример использования:
```bash
#!/bin/bash  
for i in 0 1 2 3 4 #переменной $i будем поочередно присваивать значения от 0 до 4 включительно  
do  
echo "Console number is $i" >> /dev/pts/$i #Пишем в файл /dev/pts/$i(файл виртуального терминала) строку "Console number is $i"  
done #цикл окончен  
exit 0
```
# Цикл while
Данный цикл используется для повторения команд, пока какое-то выражение истинно (код возврата = 0)

Синтаксис следующий:
```bash
while выражение или команда возвращающая код возврата  
do  
команды  
done
```

Пример:
```bash
#!/bin/bash  
again=yes #присваиваем значение "yes" переменной again  
while [ "$again" = "yes" ] #Будем выполнять цикл, пока $again будет равно "yes"  
do  
echo "Please enter a name:"  
read name  
echo "The name you entered is $name"  
  
echo "Do you wish to continue?"  
read again  
done  
echo "Bye-Bye"
```

Результат:
```bash
ite@ite-desktop:~$ ./bash2_primer1.sh  
Please enter a name:  
ite  
The name you entered is ite  
Do you wish to continue?  
yes  
Please enter a name:  
mihail  
The name you entered is mihail  
Do you wish to continue?  
no  
Bye-Bye
```
# Цикл until-do
```bash
#!/bin/bash  
echo "Введите числитель: "  
read dividend  
echo "Введите знаменатель: "  
read divisor  
  
dnd=$dividend #мы будем изменять переменные dividend и divisor,  
#сохраним их знания в других переменных, т.к. они нам  
#понадобятся  
dvs=$divisor  
remainder=1  
  
until [ "$remainder" -eq 0 ]  
do  
let "remainder = dividend % divisor"  
dividend=$divisor  
divisor=$remainder  
done  
  
echo "НОД чисел $dnd и $dvs = $dividend"
```
