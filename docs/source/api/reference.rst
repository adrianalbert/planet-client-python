Reference
=========

.. py:module:: planet.api

The public and stable API functions, classes and exceptions are all provided by the `planet.api` namespace.

The Client Object
-----------------

The Client class is the supported way to access the API.

Unless specific functionality is needed, the correct way to instantiate a Client is with zero arguments.

The Client will resolve the API_KEY from the operating system environment using the `PL_API_KEY` value.

.. code-block:: python

   client = api.Client()

.. autoclass:: Client()
   :members:



Client Return Values
--------------------

.. py:module:: planet.api.models

Most `Client` methods return a :py:class:`_Body` subclass that provides acccess to the HTTP response body in addition to the HTTP request and response details.

For many responses, it is sufficient to use the `get` method to obtain the HTTP response as JSON.

For paginated responses, the :py:class:`_Body` provides convenience functions to explicitly page through results as well as an iterator to the underlying items in each response.

Download functions return a :py:class:`Response` object that handles some aspects of asynchronous execution. Namely, streaming chunks to a handler to prevent memory issues and awaiting completion of the task.

The basic `Body` methods include:

.. autoclass:: _Body()
   :members:
   :exclude-members: __init__

The `Response` class returned by download functions has two methods:

.. autoclass:: Response()
   :members:
   :exclude-members: __init__

Most responses are more specific than a body. The JSON body provides the contents as JSON.

.. autoclass:: JSON()
   :members:

Paginated responses provide a paging iterator as well as an iterator of each pages contents.

The :py:meth:`_Paged.items_iter` method provides iteration over the contents of each page response.

For examples, a :py:class:`Scenes` response page contains a FeatureCollection of zero or more Feature objects. When using the `iterator` from the :py:meth:`_Paged.items_iter` method, only Feature objects will be returned.

To handle assembling the items from each page into a collection again and streaming them as JSON, use the :py:meth:`_Paged.json_encode` method.

.. autoclass:: _Paged()
   :members:

.. py:class:: Scenes()

   Scenes is a body that contains a FeatureCollection so when using `items_iter`, it will yield `Feature` GeoJSON objects.