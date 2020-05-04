scrapy-otomoto
==============

This program allows you to fetch all cars from otomoto.pl


## Installation
```
pip install -r requirements.txt
```

## Usage
```
scrapy crawl -L WARNING otomoto -o otomoto.json
```

This will generate `otomoto.json` file with all cars that are currently
available.  You can further investigate them or create some analysis.

## Pagination limit work around

This fork was created to be able to download more offers by working around the pagination limit.

You can get your own list of urls (start_urls in file \otomoto\spiders\otomoto.py) with car models as follows:

1. Make GET request to otomoto api: https://www.otomoto.pl/api/open/categories/
2. Find response part with models and copy it to any text editor (e.g. Notepad++):

![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/api_request_example.jpg?raw=true)

3. Replace some response parts using regex:

![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/notepad_example.jpg?raw=true)

   3.1. **[.+(\s)+.+]** pattern replace with nothing

  ![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/notepad_example_regex_1.jpg?raw=true)

   3.2. **:\\{.*?\\},** pattern replace with **\1,\n**

  ![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/notepad_example_regex_2.jpg?raw=true)

   3.3. **"** pattern replace with **'**

  ![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/notepad_example_regex_3.jpg?raw=true)
    
4. Using multi editing (ALT+SHIFT), add the base url (https://www.otomoto.pl/osobowe/) before each model name.

![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/notepad_example_multi_editing.jpg?raw=true)

5. Paste created list to \otomoto\spiders\otomoto.py file and enjoy!

![alt text](https://github.com/alinaLa/scrapy-otomoto/blob/master/start_urls_list.jpg?raw=true)
