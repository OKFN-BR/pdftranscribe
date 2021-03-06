PyBossa demo application PDF Transcribe
=======================================
PDF Transcribe is a **demo application** for PyBossa that shows how you can 
crowdsourcing a PDF transcription problem.

This application uses the [Mozilla PDF.JS](http://mozilla.github.com/pdf.js) library to load 
an [external PDF file](https://github.com/mozilla/pdf.js/wiki/Frequently-Asked-Questions#wiki-faq-xhr) 
and render it directly in the web browser **without using any third party plugin**.

By using PDF.JS, we have the possibility of rendering almost any PDF that is hosted under an 
[HTTP server](https://github.com/mozilla/pdf.js/wiki/Frequently-Asked-Questions#wiki-faq-xhr)
and then use a customized form to get the data that we want to extract from it .

In this **simple demo application**, we **load a PDF file** in one side of the page, and in the other one **a form** where the volunteer will be able to transcribe the PDF page by typing the text in the input form. While this example is really simple, adapting the template to extract specific bits of information from the PDF will be really easy (you will only need to add more HTML input fields with instructions about what you want to extract from the PDF file). The idea is that you could be able for example to extract specific items from the documents, like captions, tabular data, authorship, institutions, etc.

![alt screenshot](http://img10.imageshack.us/img10/5364/pdftranscribe1.png)

The provided script for creating the tasks is very simple: you only need to tell the script where is the PDF file hosted, the URL, and which pages you want to convert as tasks. By default, this demo explores the 14 pages of the example PDF file.

Re-using the application for your project
=========================================

You need to install the pybossa-client first (use a virtualenv):

```bash
    $ pip install pybossa-client
```
Then, you can follow the next steps:

*  Create an account in crowdcrafting.org 
*  Copy under your account profile your API-KEY
*  Run python createTasks.py -u http://crowdcrafting.org -k API-KEY -f http://domain/yourpdf -p numPages
*  Open with your browser the Applications section and choose the PDF Transcribe app. This will open the presenter for this demo application.

Please, check the full documentation here about how to create an app:

http://docs.pybossa.com/en/latest/user/create-application-tutorial.html

Setting up your Apache web server for hosting the PDF files
===========================================================

Usually you will have a set of PDF files that you are currently serving via
a web server.

If you use the application as it is, you will see that it does not work loading
the PDFs, even though the URL links are fine and the PDF pages are correct in
the Google Spreadsheet that you have created. The problem, is that you need to
enable [CORS](http://www.w3.org/TR/cors/) in order to get access to your PDF files.

In [Enable Cors webpage](http://enable-cors.org/) you can check how you can
configure most of the web servers properly, so this application can load the
PDF files from other domains without problems. For example, for an Apache web
server all you have to do is to enable the module **mod_headers**:

```bash
 $ sudo a2enmod headers
```

Then, open the site config file, i.e.
**/etc/apache2/sites-enabled/000-default** and add the following to the
**VirtualHost section:

```
Header set Access-Control-Allow-Origin "*"
```

Finally restart the web server and you will be done! The PDFs now should be
loaded without problems. Note: you can use .htaccess files too in order to not
enable CORS to all your site, or if you prefer place the previous sentence in
a Directory or Location, instead of at the level of the VirtualHost section.

Acknowledgments
===============

The thumbnail has been created using a photo from [TempusVolat](http://www.flickr.com/photos/mrmorodo/8174824430/) (license CC
BY-NC-SA 2.0). 
Check the original photo here: http://www.flickr.com/photos/mrmorodo/8174824430/

Special thanks to [Miquel Herrera for his JS libraries for the canvas
scrolling](http://hitconsultants.com/dragscroll_scrollsync/scrollpane.html).
