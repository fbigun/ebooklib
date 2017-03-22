.. EbookLib文档主文件，创建bysphinx-quickstart在2014年4月25日11:49:49你可以适应这个文件完全按你的喜好，但它应该至少包含根`toctree`指令。

欢迎使用EbookLib的文档！
====================================

EbookLib是一个用于管理EPUB2/EPUB3和Kindle文件的Python库。它能够以编程方式阅读和编写EPUB文件（Kindle支持正在开发中）。

API被设计为尽可能简单，同时也可能使事情变得复杂。它支持封面，目录，脊柱，指南，元数据等。EbookLib使用Python 2.7和Python 3.3。

主页: https://github.com/aerkalov/ebooklib/

.. toctree::
    :maxdepth: 4

    ebooklib


用法
=====

读
-------
::

    from ebooklib import epub
    import ebooklib

    book = epub.read_epub('test.epub')

    for image in book.get_items_of_type(ebooklib.ITEM_IMAGE):
        print image

写
-------
::

    from ebooklib import epub

    book = epub.EpubBook()

    # set metadata
    book.set_identifier('id123456')
    book.set_title('Sample book')
    book.set_language('en')

    book.add_author('Author Authorowski')
    book.add_author('Danko Bananko', file_as='Gospodin Danko Bananko', role='ill', uid='coauthor')

    # create chapter
    c1 = epub.EpubHtml(title='Intro', file_name='chap_01.xhtml', lang='hr')
    c1.content=u'<h1>Intro heading</h1><p>Žaba je skočila u baru.</p>'

    # add chapter
    book.add_item(c1)

    # define Table Of Contents
    book.toc = (epub.Link('chap_01.xhtml', 'Introduction', 'intro'),
                 (epub.Section('Simple book'),
                 (c1, ))
                )

    # add default NCX and Nav file
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # define CSS style
    style = 'BODY {color: white;}'
    nav_css = epub.EpubItem(uid="style_nav", file_name="style/nav.css", media_type="text/css", content=style)

    # add CSS file
    book.add_item(nav_css)

    # basic spine
    book.spine = ['nav', c1]

    # write to the file
    epub.write_epub('test.epub', book, {})

更多示例在 https://github.com/aerkalov/ebooklib/tree/master/samples

索引和表
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

