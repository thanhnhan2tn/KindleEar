# Book catalog description

1 Overview
    The books directory under the root directory of this application stores custom RSS settings. Each file is a "book", corresponding to a book pushed to kindle.
    After the application is launched, it will automatically read all py files in this directory, dynamically import them, and display them under "My Subscriptions" on the web page, and you can choose whether to push them.
    Except `__init__.py` and `base.py`, the files in the books directory can be deleted at will, if you don't need them.
    "Books" deleted in the books directory will be removed from the database within one day.

2. py file format

* The py file is recommended to be in UTF-8 format, especially if there is Chinese in it.

      So the first line of each py file is recommended as:

      `# -*- coding:utf-8 -*-`
      or:
      ```
      #!/usr/bin/env python
      # -*- coding:utf-8 -*-
      ```
* Each py file must implement a function getBook(), which returns the "class" object actually defined by the book:
      ```
def getBook():
        return Qiushibaike
  ```
* Each book is a class (the class name should not be exactly the same as the file name), and there is only one interface that must be implemented:
    `Items(self, opts=None)`
    It is a generator or returns an iterator.
    Return one tuple at a time:
    HTML tuple: (section title, URL, article title, article content, article abstract)-the article content is a string
    Picture tuple: (picture MIME, URL, picture file name, picture content, None)-picture content is a byte string
    The image MIME is: `image/jpeg`, `image/gif` etc.

* All the book definitions have been said above, so if you are proficient in python, you can write your own book classes.

* But if you are lazy, you can also inherit one of the two book templates defined in the base module to customize your own book class.
    The next section describes how to customize.

3. Book customization method
   Those who have written or read calibre's recipes will basically meet them directly.
   Because calibre's recipe module depends a lot, I don’t have enough time, and I’m lazy, so I won’t transplant it, just according to
   The shape of the recipe writes a processing module.
   * According to the RSS type, import different book base classes from the base module
     `from base import BaseFeedBook/WebpageBook/BaseComicBook`
   * If the website you are interested in does not provide RSS subscription, you can inherit WebpageBook and directly connect to the web page to extract information.
   * The parameters that can be customized by the subclass are in the definition of the BaseFeedBook class, and the comments are very detailed.
   * BeautifulSoup which processes HTML is version 4.x.
   * `cartoonmadbase.py` provides an example of capturing comic pictures.
