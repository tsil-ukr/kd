# КД.ц

Інструменти для праці з Кодуванням Д. Втілено дії перекодування КД в Ю8 і навпаки.

Треба мати наувазі, що Кодування Д все ще нестабільне і може змінитись до кінця 2024 року.

## Приклади

Перекодувати Ю8 в КД:

```ціль
взяти визначення КД;

зовнішня дія malloc(size: size_t): адреса;
дія виділити<Т>(кількість: ц32): адреса<Т> {
  вернути malloc(кількість * Т.розмір);
}

дія старт(): ц32 {
  ціль вихід = виділити<п8>(6 + 1); // 6 символів і останній нульовий байт
  ціль розмір_перекодованого_виходу = КД::перекодувати_в_Ю8(ю8"привіт", 6 * 2 /* 6 символів по 2 байти */, вихід);
  якщо розмір_перекодованого_виходу == 0 {
    // помилка ...
    вернути 1;
  }
  вихід[розмір_перекодованого_виходу] = 0; // нульовий байт

  // ...

  вернути 0;
}
```