﻿

.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. ==================================================
.. DEFINE SOME TEXTROLES
.. --------------------------------------------------
.. role::   underline
.. role::   typoscript(code)
.. role::   ts(typoscript)
   :class:  typoscript
.. role::   php(code)


Master template main setup
^^^^^^^^^^^^^^^^^^^^^^^^^^

The included main template constants and setup are:


Constants
"""""""""

::

     # cat=mastertemplate; type=string; label=Path to files: The path to the folder where the HTML template files are situated.
   mastertemplate.path = EXT:mastertemplate
   
   PAGE_TARGET = _top
   
   # <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/adaptions/tt_content/constants.txt">
   # <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/columns/2_3/constants.txt">


Setup
"""""

::

   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/mainmenu/setup.txt">
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/submenu/setup.txt">
   
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/breadcrumb/setup.txt">
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/footer/setup.txt">
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/left/setup.txt">
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/logo/setup.txt">
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/temp/right/setup.txt">
   
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/define/config/setup.txt">
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/define/header/setup.txt">
   
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/adaptions/tt_content/setup.txt">
   
   <INCLUDE_TYPOSCRIPT: source="FILE: EXT:mastertemplate/static/columns/2_3/setup.txt">
   
   
   page = PAGE
   page.typeNum = 0
   
   
   page {
   
       includeCSS {
           # and now overlay with a more flexible declaration:
           default = {$mastertemplate.path}/css/default.css
           submenu = {$mastertemplate.path}/css/submenu.css
           mainmenu = {$mastertemplate.path}/css/mainmenu.css
       }
   
       10 = TEMPLATE
       10 {
           template= FILE
   
           template.file = {$mastertemplate.path}/html/mastertemplate.html
   
           workOnSubpart = DOCUMENT
   
           marks {
             LOGO       < temp.logo
             MAINMENU   < temp.mainmenu
             BREADCRUMB < temp.breadcrumb
             LEFT       < temp.left
             CONTENT    = CONTENT
             CONTENT {
                 table = tt_content
                 select.orderBy = sorting
                 select.where = colPos=0
                 select.languageField = sys_language_uid
             }
             RIGHT      < temp.right
             FOOTER     < temp.footer
           }
        }
   
       #999 = TEXT
       #999.value=master
   }

