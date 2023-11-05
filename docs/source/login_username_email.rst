==================
LoginUsernameEmail
==================

Classe para realizar autenticação com username ou email

Exemplo:
========

.. code-block:: python

  # settings.py
  AUTHENTICATION_BACKENDS = [
      "novadata_utils.auth.LoginUsernameEmail",
  ]
