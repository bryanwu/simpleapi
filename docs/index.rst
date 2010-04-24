=========
simpleapi
=========

simpleapi is an **easy to use, consistent, transparent and portable** way of
providing an API within your django project. It contains a **client and server
library** for seamless interaction.

To install, simply run:

.. code-block:: console
    
    # easy_install -U django-simpleapi

The source is available on `GitHub <http://github.com/flosch/simpleapi>`_.

Contents
========

.. toctree::
   
   prepartion
   gettingstarted
        server/route
   server/namespace
   server/features
   client/*
   client/javascript
   client/php
   credits

Easy example
============

handlers.py (in your django app)
--------------------------------
::
    
    from simpleapi import Namespace
    
    class Calculator(Namespace):
        def add(self, a, b):
            return a + b
        add.published = True

urls.py (in your django app)
----------------------------
::

    from simpleapi import Route
    from handlers import Calculator

    urlpatterns = patterns('',
    	(r'^api/calculator/$', Route(Calculator))
    )

Python Client (using simpleapi's client library)
------------------------------------------------
::

    from simpleapi import Client
    
    calculator = Client(ns='http://localhost:8888/api/calculator/')
    print "5 + 3 =", calculator.add(a=5, b=3)

PHP Client (using simpleapi's PHP client)
-----------------------------------------
.. code-block:: php
    
    <?php
        $calculator = new Client(ns='http://localhost:8888/api/calculator/');
        print("5 + 3 ".$calculator.add(a=5, b=3));
    ?>

JavaScript Client (using jQuery)
--------------------------------
.. code-block:: javascript
    
    jQuery.get(
        "/api/calculator/",
        {_call: 'add', a: 5, b: 3},
        function (result) {
            alert('5 + 3 = ' + result);
        }
    )