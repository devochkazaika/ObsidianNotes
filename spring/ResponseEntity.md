https://habr.com/ru/articles/675716/

Что такое ResponseEntity<>? Представим ситуацию - у нас есть интернет магазин. И, при примитивной реализации, мы переходим по продуктам, передавая его Id в качестве параметра[@RequestParam.](https://habr.com/users/requestparam.) Например, наш код выглядит таким образом:

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

Однако, если мы обратимся к продукту, который у нас отсутствует, например с id=299, то получим следующую картину:

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image005.png)

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image007.png)

Что здесь происходит? Вместо строгого типа Product, мы ставим ResponseEntity<?>,
где под **?** понимается любой Java объект. Конструктор ResponseEntity позволяет перегружать этот объект, добавляя в него не только наш возвращаемый тип, но и статус, чтобы фронтенд мог понимать, что именно пошло не так. Например, при корректном исполнении программы, передавая id=1, мы увидим просто успешно переданный объект Product с кодом 200, а вот в случае продукта с id = 299 результат уже будет такой: