DTO – Data Transfer Object

Используются для передачи данных между сервером и клиентом. Чаще всего чтобы в json кидать

Полезные аннотации

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)

@NotNull – очевидно, что не дает полю быть нулем, группа для валидации

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

@Length – для обозначения допустимого длины поля

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image003.png)

@DateTimeFormat – для обозначения даты в поле

@JsonFormat – формат ввода и вывода в json описывается паттерном pattern

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image005.png)

@JsonProperty – полезная штука для определения перекидываения json-а. Допустим одноп поле JsonProperty.Access.WRITE_ONLY, это значит что в DTO только при отправке на сервер будет данное поле. Аналогично с READ_ONLY

![](file:///C:/Users/D491~1/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

@FieldDefaults – делает все поля с одинаковым доступом PRIVATE