
Selenium WebDriver    

- ```bash # pip install selenium ```
- рекомендуется virtualenv. Python 3.4 содержит модуль pyvenv
- [Документация перевод](http://selenium2.ru/docs.html)
- [Оригинальная документация](http://www.seleniumhq.org/docs/)
- [Для Python](http://selenium-python.readthedocs.io/)

- Selenium server необходим в случаях, когда вы хотите использовать remote WebDriver 
- Selenium server написан на языке Java. Для его запуска рекомендована среда Java Runtime Environment (JRE) версии 1.6 или выше.
```bash	java -jar selenium-server-standalone-2.x.x.jar ```

Протсейший скрипт Python:
```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys   	// Класс Keys обеспечивает взаимодействие с командами клавиатуры

driver = webdriver.Firefox()						// создается элемент класса Firefox WebDriver.
driver.get("http://www.python.org")					// WebDriver будет ждать пока страница не загрузится полностью, AJAX - сложнее
assert "Python" in driver.title  					// это утверждение (англ. assertion), что заголовок содержит слово “Python”
elem = driver.find_element_by_name("q")				// способ получения элементов с помощью методов find_element_by_*
elem.send_keys("pycon")								// мы посылаем нажатия клавиш (аналогично введению клавиш с клавиатуры)	
elem.send_keys(Keys.RETURN)							// Специальные команды с помощью класса Keys из selenium.webdriver.common.keys
assert "No results found." not in driver.page_source
driver.close()										// quit закроет браузер полностью, в то время как close закроет одну вкладку
```

Вы можете писать тесты с помощью модуля Python unittest. 
Альтернатива py.test и nose.

Python -> Selenium -> Driver -> Browser

Драйверы
	- chromedriver
	- geckodriver
	- IE

Селекторы
	css selector
        - состотит из серии прыжком по DOM
        - тег - атрибут, напрменр ul#menu, где <ul id='menu'> 
        - # перед id, . перед class
        - Chrome - F12 - Consile - $('a') - найти первую ссылку,  $$('a') все ссылки на странице

    - find_element_by_id('name') -> вызывает find_element_by_css_selector('#name')	
    - find_element_by_class_name('name') -> вызывает find_element_by_css_selector('.name')	
    - find_element_by_css_selector() содержит набор селекторов
        "[name=password]"
        "[placeholder=search]"
        "[type=button]"
        "[checked]" - проверка только наличия атрибута - не важно какое значение
        "[title *= Name]" - проверка на содержание части текста
                ^= начало  $= конец
        "label" - по тегу
        ".error" - по классу
        "label.error" - по тегу и классу
        "label.error.fatal" - по тегу и двум классам одновременно
        "label.error[for=email]" - сочитание группы атрибутов 	
        $$("label.error[for=email]") или тоже самое "label[for=email][class=error]"
        "label:not(.error)" - использовать отрицание :not() не входит 
        "div#main p" - найти связку, где p внутри div
        "div#main>p" - p сразу следует за div
        "div#main li:first-child" - первое вхождение, last-child, nth-child(1) - по номеру 
        "div#header>div:nth-of-type(1)" - выбираются все удовлетворяющие и берется 1-ый
    Практика - в браузере в консоли $$() и css-селекторы - 2-3 прыжка - как можно проще

    XPath
    - Chrome - F12 - Consile - $x('//...')
    find_element_by_xpath
        - // - найти элемент где-нибудь
        - / - непосредственно внутри
        - * - произвольный тег
        - [услоовие на значени атребутов]
        - @ - предваряет атрибут
        - 'значение атрибута в кавычках'
        - contains(), strts-with()	
        - and - разделитель нескольких условий
        - [2] - выбор второго элемента - нумерация с 1
        - .. - переход к родительскому элементу
        - . - в подзапросе, относительно текущего элемента, при поиске в подзапросах обязательно ставить .//

        "//*[@checked]"  ==  "[checked]" 			
        "//*[@name='email']"  ==  "[name=email]"
        "//*[contains(@title,'Name')]"  ==  "[title=*Name]"
        "//label[contains(@class,'error')]"  ==  "label.error"
        "//label[contains(@class,'error') and contains(@class,'fatal')]"  == "label.error.fatal"
        "//div[@id='main']//p"  ==  "div#main p"
        "//div[@id='main']/p"  ==  "div#main>p"	
        "//div[@id='header']/div[2]" == "div#header>div:nth-of-type(2)"

        движение вверх по дереву, поиск элемента, переход к родительскому элеменут, и поиск уже внутри родительского элемента
        "поиск элемента/../поиск в родительском"

        "//a[contain(.,'Edit')]" - поиск по текстовому содержимому

        "//form[.//input[@name='password']]" - подзапросы, найти поле ввода в форме 

    find_elements 
        - поиск множественных элементов
        - пример	
            rows = find_elements_by_
            for row in rows:
                rows.find....
        - если ничего не находится - то возвращается пустой список [], find_element выдаст исключение
        - .size() > 0  - проверка на то что поиск нашел хоть один элемент

    поиск элемента в JavaScript
        - driver.execute_script("return 2+2") - внутри строка кода на JS
        - links = driver.execute_script("return $$('a:contains((WebDriver)')") 
        - .execute_script("return getElementById('...')").send_keys("selenium")
        -- document.querySelectorAll
        - удобно это для поиска внутри фреймворков типа Angular - имеющией свои удобные идентификаторы
        - в JQuery - "return $$('a')" 


    Элемент не найден	
        FindElement - NoSuchElementException
        FindElement - пустой список
        InvalidSelectorException - 	если селектор был оформелн неправильно, является подклассом NoSuchElementException
        при этом в FF могут не все исключение выбрасываться - а только WebDriverException
        внутри сообщения об ошибке есть скриншот - его можно вытащить и сохарнить

    Ожидание элементов
        .set_script_timeout
        .set_page_load_timeout
        .implicitly_wait(5) - ждать появления элемента до 5 секунд 
                - неявный метод один раз в начале тестов, цикл внутри драйвера 100мс
                - но при проверке отсутвия элмента будет ждать до конца или надо будет выключать настройку
                - FindElemens ждет хотя бы одного совпадения - или вернет пустой список
                - можно поставить в 0 и ловить исключение и потом повторять через таймут
                - неявное - ждет появления в DOM но не факт что он будет при этом видим
        Ожидание появления элемента
            from selenium.webdriver.support.wait import WebDriverWait
            from selenium.webdriver.support import expected_conditions as EC
            from selenium.webdriver.common.by import By

            wait = WebDriverWait(driver, 10) # seconds
            # обратите внимание, что локатор передается как tuple!
            element = wait.until(EC.presence_of_element_located((By.NAME, "q"))
            element2 = wait.until(lambda d: d.find_element_by_name("q"))		

        Ожидание исчезновения элемента
            wait = WebDriverWait(driver, 10) # seconds
            driver.refresh()
            wait.until(EC.staleness_of(element))

        Ожидание видимости элемента
            wait = WebDriverWait(driver, 10) # seconds
            wait.until(EC.visibility_of(element)	

        Другие ожидания
            http://seleniumhq.github.io/selenium/docs/api/py/webdriver_support/selenium.webdriver.support.expected_conditions.html

        JS вариант
            wait в качестве условия может принимать промис, объект типа Condition или просто функцию, возвращает промис
            driver.wait(until.elementLocated(By.name('q')), 10000/*ms*/).then(function(element) {...});		


            
локаторы
- устойчивость к изменениям верстки
- максимально точный критерий, нахождение только одного элемента
- избегать порядковых номеров
- привязка к уникальному блоку при получении нескольких элементов
- минимальное число по DOM - максимум 3-4 прыжка, лучше 1-2

[шпоры](https://www.red-gate.com/simple-talk/dotnet/net-framework/xpath-css-dom-and-selenium-the-rosetta-stone/)

Атрибуты	
    у элемента в html атрибуты - пары имя значение
    свойства properties - правое окно по F12 - это JavaScript св-ва
    все properties доступны для полученияы через .get_attribute()
    href = link.get_attribute("href")

    value - может быть путаница, но выдаст именно свойсво а не атрибут

    isDisplayed - видимый или нет элемент, сложный алгоритм определения видит ли человек
        не сработает на 98% прозрачности, элемент цвета фона, позади другого блока, сдвинут за левый край экрана.

    getText возвращает тот текст который видит пользователей, пробелы могут сократиться
    txt = link.text

    проверка стилей css через проверку id, class данного тега
    getCssValue() - value_of_css_property - разные браузеры выдают разные значения по этой комманде
    RGBa - байта, последний прозрачность    
    - color = link.value_of_css_property("color"

    getSize - размеры, но моежт неверно показывать трансформации
    getLocation - относительно страницы
    getRect - не все поддерживают
    через JS можно не только узнать размеры но и проскролировать до видимости на экране
    (Locatedle element).getCoordinates().inView()
    - location = link.location
    - size = link.size


		www.w3.org/TR/webdriver/

Клик левой кнопкой мыши
    - только на видимый элемент
    - если он не закрыт другим элементом
    - автоскрол до элемента, но если это будет возможным
    - в противном случае будет исключение
    - хром наиболее полно решает задачу
    - в противном случае - выбросит исключение
    - точка клика - центр первого прямоугольника
    - link.click()
    - if button.is_displayed():
            button.click()


Клавиатура
    from selenium.webdriver.common.keys import Keys
    search_field.send_keys("selenium" + Keys.ENTER)
    - вводить можно даже в закрытое другим эелментом поле
    - есть отличия в реализации браузеров
    - в полях с маской ввода надо вначале Home
    - при вообде эмуляриут все состояния keyDown, keyUp, keyPress
    - но при этом работает медленно
    
    password_field.clear()  
        - очистка поля ввода

    submit - отправляет форму, но ее нет в стандарте и далее будет исключена

    - с чекбоксом надо делать вначале проверку и если не установлен то клик

расширенный режим API управления мышью и клавиатурой
    - делает ровно то что просишь 
    - можно делать сочетания мыши и клваитуры
    - ActionChains - цепочка действий, все вытягивается в последовательность шагов действия
    - в FF пока не реализовано. 
    - цепочка будет реализована на стороне сервера - пока на клиенте.

    from selenium.webdriver.common.action_chains import ActionChains
    ActionChains(driver)
        .move_to_element(drag)
        .click_and_hold()
        .move_to_element(drop)
        .release()
        .perform()

Выпадающий список:
    - кликнуть по самому селекту
    - кликнуть по одному из вложенных элементов
    - есть упрощение через find и select

Прозрачные элементы
    - селениум по ним кликать не будет
    - или на JS писать кликалку
        select = driver.find_element_by_css_selector("select")
        driver.execute_script("arguments[0].selectedIndex = 3; arguments[0].dispatchEvent(new Evant('change'))", select)
    - или opacity выставить 1 и тгда уже кликнуть
        driver.execute_script("arguments[0].style.opasity = 1", select)
        теперь или двойной клик или через класс select


