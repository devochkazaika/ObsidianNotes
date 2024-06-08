### Создание контроллера в спринге

Пример
```java
@RestController  
@RequestMapping("/api/v1/data")  
@RequiredArgsConstructor  
public class DataController {  
	//Разные комноненты
    private final TestDataService testDataService;
    private final KafkaDataService kafkaDataService;  
    private final DataMapper dataMapper;  
    private final DataTestOptionsMapper dataTestOptionsMapper;  
  
    @PostMapping("/send")  
    public void send(@RequestBody DataDto dto){  
        Data data = dataMapper.toEntity(dto);  
        kafkaDataService.send(data);  
    }  
    @PostMapping("/test/send")  
    public void testSend(@RequestBody DataTestOptionsDto testOptionsDto){  
        DataTestOptions testOptions = dataTestOptionsMapper.toEntity(testOptionsDto);  
        testDataService.sendMessages(testOptions);  
    }  
}
```

Основные вещи
##### Анотации класса
* @RestController - обозначение контроллера. По сути это _@ResponseBody_ и _@Controller_ вместе. Позволяет передавать объекты(выводить и работать с ними) в виде json и xml объектов, что позволяет не делать лишнюю обработку. Если бы использовали просто _@Controller_ тогда при запросах всегда вылетал 404 статус ошибки
* @RequestMapping("/api/v1/data")  - для обозначении начального пути
* @RequiredArgsConstructor  - библа [[lombok]]Генерирует конструкторы для всех полей, кроме статических. Для работы нужно чтобы поля были `final` 
	Есть также аналоги @NoArgsConstructor и @AllArgsConstructor
		NoArgsConstructor - конструктор без параметров
		AllArgsConstructor - конструктор для каждого параметра с 1 аргументом
##### Анотации методов
* @PostMapping("/send")  GetMapping и тд - думаю очевидно

