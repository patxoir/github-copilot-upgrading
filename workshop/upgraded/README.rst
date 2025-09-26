
Guachi
======

Guachi is a persistent configuration manager for Python 3 projects. It stores configuration as dictionaries, supports INI-style keys, and provides default value handling.

Key Features
------------
- Persistent dictionary storage using SQLite
- INI file parsing and mapping to dictionary keys
- Default value support
- Python 3 compatible
- Modern packaging (pyproject.toml)

Installation
------------
Activate your virtual environment and install with pip:

.. code-block:: bash

    python3 -m venv venv
    source venv/bin/activate
    pip install .

Usage Example
-------------
Suppose you have a Twitter app using an INI file:

.. code-block:: ini

    [DEFAULT]
    app.twitter.username = alfredodeza
    app.update.frequency = 60
    app.load.startup = False

You can load and use the config as follows:

.. code-block:: python

    from guachi import ConfigMapper
    ini_file = "/Users/alfredo/.twitter.ini"
    conf = ConfigMapper(config_db_path)
    conf.set_config(ini_file)
    db_conf = conf.stored_config()
    print(db_conf['frequency'])  # 60

Default values are always available if set:

.. code-block:: python

    db = ConfigMapper(config_db_path)
    conf = db.stored_config()
    print(conf.get('load', True))

Updating values from a changed INI file:

.. code-block:: python

    conf = ConfigMapper(config_db_path)
    conf.update_config(ini_file)

Testing
-------
Run all tests with:

.. code-block:: bash

    PYTHONPATH=$(pwd) pytest guachi/tests

Documentation
-------------
Full API documentation is available in the `docs/` directory.
