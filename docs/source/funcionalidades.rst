===============
Funcionalidades
===============

Seguem as funcionalidades do pacote, bem como exemplos:

NovadataModelAdmin
==================

Classe para facilitar a criação de um ModelAdmin, implmentando diversas funcionalidades, como:
list_display, search_fields, list_filter, autocomplete_fields, list_select_related, filter_horizontal
exclude e advanced_filter_fields, todos automáticos.

O pacote considera o tipo dos campos e mapeia automaticamente os mesmos para suas respectivas propriedades.
Você pode encontrar a lista de mapeamento `neste <https://github.com/TimeNovaData/novadata_utils/blob/master/novadata_utils/functions/props_dict.py>`_ arquivo do repositório.

Além disso, ele atua em conjunto com outros pacotes, implementando algumas funcionalidades importates.

Exemplo:
--------

.. code-block:: python

  # Model:
  from django.contrib.auth.models import User
  from django.db import models
  from novadata_utils.models import NovadataModel


  class Exemplo(NovadataModel):
      nome = models.CharField(
          verbose_name="Nome",
          max_length=100,
      )

      slug = models.SlugField(
          verbose_name="Slug",
          max_length=100,
          blank=True,
          null=True,
      )

      novo_slug = models.SlugField(
          verbose_name="Novo slug",
          max_length=100,
          blank=True,
          null=True,
      )

      exemplo_slug = models.SlugField(
          verbose_name="Exemplo slug",
          max_length=100,
          blank=True,
          null=True,
      )

      teste = models.CharField(
          verbose_name="Teste",
          max_length=100,
      )

      fornecedor = models.ForeignKey(
          "core.Fornecedor",
          verbose_name="Fornecedor",
          on_delete=models.SET_NULL,
          null=True,
      )

      estados = models.ManyToManyField(
          "core.Estado",
          verbose_name="Estados",
          blank=True,
      )

      STATUS_CHOICES = [
          ("Ativo", "Ativo"),
          ("Inativo", "Inativo"),
          ("Bloqueado", "Bloqueado"),
          ("Cancelado", "Cancelado"),
          ("Suspenso", "Suspenso"),
          ("Pendente", "Pendente"),
          ("Aguardando", "Aguardando"),
      ]

      status = models.CharField(
          verbose_name="Status",
          max_length=10,
          choices=STATUS_CHOICES,
          default="Ativo",
      )

      usuario = models.OneToOneField(
          User,
          verbose_name="Usuário",
          on_delete=models.SET_NULL,
          null=True,
      )

      campo_numerico = models.DecimalField(
          verbose_name="Campo numérico",
          max_digits=10,
          decimal_places=2,
          blank=True,
          null=True,
      )

      campo_inteiro = models.IntegerField(
          verbose_name="Campo inteiro",
          blank=True,
          null=True,
      )

      campo_data = models.DateField(
          verbose_name="Campo data",
          blank=True,
          null=True,
      )

      campo_hora = models.TimeField(
          verbose_name="Campo hora",
          blank=True,
          null=True,
      )

      campo_data_hora = models.DateTimeField(
          verbose_name="Campo data hora",
          blank=True,
          null=True,
      )

      @property
      def nome_teste(self):
          """Retorna a concatenação dos campos 'nome' e 'teste'."""
          return f"{self.nome or 'Sem nome'} - {self.teste or 'Sem teste'}"

      def __str__(self):
          """Método que retorna a representação do objeto como string."""
          return self.nome

      class Meta:
          """Sub classe para definir meta atributos da classe principal."""

          app_label = "core"
          verbose_name = "Exemplo"
          verbose_name_plural = "Exemplos"

  # Admin:
  from django.contrib import admin
  from novadata_utils.admin import NovadataModelAdmin

  from ..models import Exemplo


  @admin.register(Exemplo)
  class ExemploAdmin(NovadataModelAdmin):
      ...

Saída:
------

.. figure:: assets/images/example_novadata_model_admin1.png
  :alt: ExampleNovadataModelAdmin1
.. figure:: assets/images/example_novadata_model_admin2.png
  :alt: ExampleNovadataModelAdmin2
.. figure:: assets/images/example_novadata_model_admin3.png
  :alt: ExampleNovadataModelAdmin3
.. figure:: assets/images/example_novadata_model_admin4.png
  :alt: ExampleNovadataModelAdmin4

NovadataModelViewSet
====================

Classe que implementa o create e o update para o ModelViewSet do Django Rest Framework

Exemplo:
--------

.. code-block:: python

  from novadata_utils.viewsets import NovadataModelViewSet


  class MyViewSet(NovadataModelViewSet):
      queryset = MyModel.objects.all()
      serializer_class = MySerializer

NovadataModelSerializer
=======================

Classe que traz a serialização de todos os seus objetos necessários para o front-end.

Exemplo:
--------

.. code-block:: python

  from novadata_utils.serializers import NovadataModelSerializer


  class MySerializer(NovadataModelSerializer):
      class Meta:
          model = MyModel
          fields = '__all__'

LoginUsernameEmail
==================

Classe para realizar autenticação com username ou email

Exemplo:
--------

.. code-block:: python

  # settings.py
  AUTHENTICATION_BACKENDS = [
      "novadata_utils.auth.LoginUsernameEmail",
  ]

reverse_lazy_plus
=================

Função para redirecionamento avançado.

Funciona como a reverse_lazy do Django, porém aceitando parâmetros GET, # e parâmetros de url.

Exemplo:
--------

.. code-block:: python

  from novadata_utils.redirect import reverse_lazy_plus

  reverse_lazy_plus(
      'testings',
      url_params=[1, 'type_example'],
      get_params={'mensagem': 'Esta é uma mensagem'},
      '#aba-6',
  )
  # Output:
  # /testings/1/type_example?mensagem=Esta%20é%20uma%20mensagem#aba-6
