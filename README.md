# Отчёт о тестировании и установке IntelliJ IDEA 

## Краткое описание

<10.08.2020> была установленна программа IntelliJ IDEA на Windows 10 Home 64bit.

На установку затрачено: ~20 минут.

В результате установки и тестирования дефекты в работе программы не были выявленны, программа работае согласно инструкции:

![CCNumberValidator-1 Вывод прогр](https://user-images.githubusercontent.com/61200143/92230837-6c7ee180-eeb4-11ea-9148-a6058cc7de4b.png)


## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты:
* Файл [Инструкция по установке OpenJDK11](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/openjdk11-manual.md)

В качестве тестовых данных использовался проверочный код:

```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello QA!");
  }
}
```
Тестирование производилось в следующем окружении:
 * Устройство: Windows 10 Home 64bit, [Version 10.0.19041.450]
 * Браузер: Google Chrome Версия 84.0.4147.135 (Официальная сборка), (64 бит)
 * java: 11.0.8 2020-07-14



# Отчёт о тестировании Credit Card Number Validator

## Краткое описание

<04.09.2020> было проведено тестирование компонента приложения Credit Card Number Validator методом предположения об ошибках на Windows 10 Home 64bit.

На тестирование затрачено: ~2 часов.

В результате тестирования выявлены следующие дефекты:

* [Номер карты Diners Club из 14 цифр в приложении не проходит валидацию](https://github.com/DeminaDaria/Java-HW-1.2_CCNumbValidat/issues/1)
* [Номер карты AmExp и UATP из 15 цифр в приложении не проходят валидацию](https://github.com/DeminaDaria/Java-HW-1.2_CCNumbValidat/issues/2)
* [Номера карт из 18,19 цифр не проходят валидацию (InterPayment/Maestro/China UnionPay/Visa)](https://github.com/DeminaDaria/Java-HW-1.2_CCNumbValidat/issues/3)
* [Номера карт МИР и InterPayment из 16 цифр не проходят валидацию](https://github.com/DeminaDaria/Java-HW-1.2_CCNumbValidat/issues/4)


## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты:
* Сайт [Генератор кредитных карт](https://wtools.io/ru/credit-card-generator)
* Сайт [Генератор кредитных карт](https://creditcardgenerator.in/card-generator/mir)

В качестве тестовых данных использовались:
* оставшиеся наработки:

```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```
* [Валидные номера кредитных карт](https://docs.google.com/document/d/197arTZizCLWwVvpkDzsDAL9li7AMBXKeRT8yOFh9Ado/edit?usp=sharing)


Тестирование производилось в следующем окружении:
 * Устройство: Windows 10 Home 64bit, [Version 10.0.19041.450]
 * Браузер: Google Chrome Версия 84.0.4147.135 (Официальная сборка), (64 бит)
 * java: 11.0.8 2020-07-14
 * файл [KeyValidator.class.](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/artifacts/KeyValidator.class)
