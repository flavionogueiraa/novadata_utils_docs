=================
reverse_lazy_plus
=================

Função para redirecionamento avançado.

Funciona como a reverse_lazy do Django, porém aceitando parâmetros GET, # e parâmetros de url.

Exemplo:
========

.. code-block:: python

  from novadata_utils.redirect import reverse_lazy_plus

  reverse_lazy_plus(
      'testings',
      url_params=[1, 'type_example'],
      get_params={'mensagem': 'Esta é uma mensagem'},
      '#aba-6',
  )
  # Output:
  # /testings/1/type_example/?mensagem=Esta%20é%20uma%20mensagem#aba-6
