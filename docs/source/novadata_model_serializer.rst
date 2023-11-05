=======================
NovadataModelSerializer
=======================

Classe que traz a serialização de todos os seus objetos necessários para o front-end.

Exemplo:
========

.. code-block:: python

  from novadata_utils.serializers import NovadataModelSerializer


  class MySerializer(NovadataModelSerializer):
      class Meta:
          model = MyModel
          fields = '__all__'
