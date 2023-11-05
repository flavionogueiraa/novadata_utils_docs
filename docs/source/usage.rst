Usage
=====

.. _installation:

Installation
------------

Dependências:

Django
Django Advanced Filters
Django Admin List Filter Dropdown
Django Admin Rangefilter
Djnago Import Export
Django Rest Framework

Para instalar o projeto, basta rodar o seguinte comando:

.. code-block:: console

   (.venv) $ pip install novadata-utils

Adicione o projeto ``novadata_utils`` em ``INSTALLED_APPS``
e o middleware ``crum.CurrentRequestUserMiddleware`` em ``MIDDLEWARE``:

.. code-block:: python

   INSTALLED_APPS = [
      ...
      'advanced_filters',
      'django_admin_listfilter_dropdown',
      'django_object_actions',
      'import_export',
      'novadata_utils',
      'rangefilter',
      'rest_framework',
      ...
   ]

   # After Django middlewares
   MIDDLEWARE += ('crum.CurrentRequestUserMiddleware',)

Adicione as urls do pacote ``advanced_filters`` em ``urls.py``:

.. code-block:: python

   urlpatterns = [
      ...
      path('advanced_filters/', include('advanced_filters.urls')),
      ...
   ]

Para saber como usar o projeto, acesse a seção de :ref:`funcionalidades`.

.. toctree::
   :maxdeepth: 2

   index
   usage
   funcionalidades
      novadata_model_admin