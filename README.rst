``lastfmclient``
################

Python client for the `Last.fm API <http://www.last.fm/api>`_ with a
pythonic interface. Also includes an async variant of the client for
`Tornado <https://github.com/facebook/tornado>`_.


Usage
=====

Regular
-------

.. code-block:: python

    from lastfmclient import LastfmClient

    api = LastfmClient(
        api_key=KEY,
        api_secret=SECRET,
        session_key=session_key
    )

    resp = api.track.update_now_playing(
        track='Paranoid Android',
        artist='Radiohead',
        album='OK Computer',
    )

    print resp


Asynchronous (uses ``tornado.httpclient.AsyncHTTPClient``)
----------------------------------------------------------

.. code-block:: python

    from lastfmclient import AsyncLastfmClient

    def callback(resp):
        print resp

    api = AsyncLastfmClient(
        api_key=KEY,
        api_secret=SECRET,
        session_key=session_key
    )

    api.track.update_now_playing(
        track='Paranoid Android',
        artist='Radiohead',
        album='OK Computer',
        callback=callback,
    )

See also `examples <https://github.com/jkbr/lastfmclient/tree/master/examples>`_.


Client methods
==============

All the methods the Last.fm API provides are mirrored in the client with
rich docstrings and arguments description. This code is actually generated
directly from the online API documentation pages
(see ``./generate.py``, ``./api.json``, and ``./lastfmclient/api.py``).

The defined methods be updated to the current version of the documentation via:


.. code-block:: bash

    $ pip install -r requirements.txt lxml

    # 1. Generate fresh api.json from docs at http://www.last.fm/api:
    $ make spec

    # 2. Generate `lastfm/api.py` from `api.json`:
    $ make code

    # Or, all the above in one step:
    $ make
