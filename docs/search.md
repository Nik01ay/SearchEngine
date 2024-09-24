### Получение данных по поисковому запросу — GET /api/search

Метод осуществляет поиск страниц по переданному поисковому запросу (параметр query).  
Чтобы выводить результаты порционно, также можно задать параметры offset (сдвиг от начала списка результатов)   
и limit (количество результатов, которое необходимо вывести).  
В ответе выводится общее количество результатов (count), не зависящее от значений параметров offset и limit,  
и массив data с результатами поиска. Каждый результат — это объект, содержащий свойства результата поиска  
(см. ниже структуру и описание каждого свойства).
Если поисковый запрос не задан или ещё нет готового индекса  
(сайт, по которому ищем, или все сайты сразу не проиндексированы), метод должен вернуть соответствующую ошибку  
(см. ниже пример). Тексты ошибок должны быть понятными и отражать суть ошибок.

**Параметры:**

**query** — поисковый запрос;  
**site** — сайт, по которому осуществлять поиск (если не задан, поиск должен происходить по всем проиндексированным сайтам);  
задаётся в формате адреса, например: http://www.site.com (без слэша в конце);

**offset** — сдвиг от 0 для постраничного вывода (параметр необязательный;  
если не установлен, то значение по умолчанию равно нулю);

**limit** — количество результатов, которое необходимо вывести (параметр необязательный; если не установлен,  
то значение по умолчанию равно 20).

**Формат ответа в случае успеха:**

{  
'result': true,  
'count': 574,  
'data': [  
{  
"site": "http://www.site.com",  
"siteName": "Имя сайта",  
"uri": "/path/to/page/6784",  
"title": "Заголовок страницы,  
которую выводим",  
"snippet": "Фрагмент текста,  
в котором найдены  
совпадения, <b>выделенные  
жирным</b>, в формате HTML",  
"relevance": 0.93362  
},  
...  
]  
}  

**Формат ответа в случае ошибки:**

{  
'result': false,  
'error': "Задан пустой поисковый запрос"  
}  