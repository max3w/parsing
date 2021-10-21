# parsing

## Шаги выполнения
<ol>
<li>Инсталируем Composer и подключаем в нем библиотеку <pre>composer require simplehtmldom/simplehtmldom:dev-master</pre></li>
<li>Изучаем через монитор сети данные о тестовом запросе "123" которые приходят при поиске бренда (URL, POST data, HTTP Headers)</li>
<li>Эмулируем этот запрос в php скрипте</li>
<li>Дальше распаршиваем результат в нужный вид</li>
</ol>

### Анализ запросов

<p>На первом этапе видим что при вводе любого символа в строку "word", сайт выполняет запросы при вводе каждого символа <a href="https://skr.sh/sAdb1MvdtpJ?a">https://skr.sh/sAdb1MvdtpJ?a</a></p>
<p>Получаем json файл с GET параметром запроса:</p>
<pre>"url": "https://search.ipaustralia.gov.au/trademarks/search/count?_csrf=4674abcd-8356-4e84-9047-443bc3994db3&_sw=on&ct=A&dateType=LODGEMENT_DATE&ieOp%5B0%5D=AND&ieOp%5B1%5D=AND&irOp=AND&it%5B0%5D=PART&it%5B1%5D=PART&it%5B2%5D=PART&it%5B3%5D=PART&nameField%5B0%5D=OWNER&undefined=false&weOp%5B0%5D=AND&weOp%5B1%5D=AND&wps=false&wrOp=AND&wt%5B0%5D=PART&wt%5B1%5D=PART&wt%5B2%5D=PART&wt%5B3%5D=PART&wv%5B0%5D=123"</pre>
<p>Смотрим ответ этого запроса
<pre>{"count":279,"errors":null}</pre>
тут мы видим что это количество страниц с результатами</p>
<p>Дальше смотрим какие идут запросы по нажатию кнопки Search<pre>https://search.ipaustralia.gov.au/trademarks/search/result?s=df34c895-e989-472d-bf6e-7005346d992f</pre></p>
<p>Здесь фигурирует параметр <pre>s=df34c895-e989-472d-bf6e-7005346d992f</pre></p>
<p>При повторном запросе он меняется, пример <pre>s=9ef3501e-c945-4e21-abb0-c797205b68bb</pre> и т.д.</p>
<p>Смотрю запрос дальше, вижу что происходит кодирование нашего значения 123 <pre> "postData": {
            "mimeType": "application/x-www-form-urlencoded",
            "params": [
              {
                "name": "_csrf",
                "value": "4674abcd-8356-4e84-9047-443bc3994db3"
              },
              {
                "name": "wv[0]",
                "value": "123"
              },</pre></p>
<p>Продолжаю разбирать запрос дальше чтобы передавать его...(в процессе)</p>





