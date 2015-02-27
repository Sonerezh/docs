Sonerezh Documentation
=====================
This is the official documentation for the Sonerezh project. It is available online, PDF and EPUB formats at LINK.

Requirements
------------
You can read all of the documentation within as its just in plain text files, marked up with ReST text formatting.  To build the documentation you'll need the following:

* Make
* Python
* Shpinx
* Read-the-docs Sphinx theme

You can install Sphinx following [the official guide](http://sphinx-doc.org/).

	easy_install -U sphinx

You can install the Read-the-docs Sphinx theme using:

	pip install sphinx_rtd_theme

Building the documentation
--------------------------
After installing the documentation, you can build the documentation using sphinx-build:

	git clone https://github.com/Sonerezh/docs.git
	cd docs
	make html
