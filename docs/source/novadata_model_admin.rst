==================
NovadataModelAdmin
==================

Classe para facilitar a criação de um ModelAdmin, implmentando diversas funcionalidades, como:
list_display, search_fields, list_filter, autocomplete_fields, list_select_related, filter_horizontal
exclude e advanced_filter_fields, todos automáticos.

O pacote considera o tipo dos campos e mapeia automaticamente os mesmos para suas respectivas propriedades.
Você pode encontrar a lista de mapeamento `neste <https://github.com/TimeNovaData/novadata_utils/blob/master/novadata_utils/functions/props_dict.py>`_ arquivo do repositório.

Além disso, ele atua em conjunto com outros pacotes, implementando algumas funcionalidades interessantes. Segue a lista:

#. list_display
#. search_fields
#. list_filter
  Alguns tipos de campos são modificados aqui, segue a lista:
  #. Foreign keys
    Campos ForeignKey são modificados para um campo de busca, com autocomplete,
    se utilizando do pacote django_admin_listfilter_dropdown, todos os campos
    desse tipo são feitos com a classe RelatedOnlyDropdownFilter.
  #. Campos com choices
    Campos com choices são modificados para um campo de busca, com autocomplete,
    se utilizando do pacote django_admin_listfilter_dropdown, todos os campos
    desse tipo são feitos com a classe ChoiceDropdownFilter.
  #. Datas
    Campos DateField e DateTimeField são modificados para um campo de busca,
    com autocomplete, se utilizando do pacote rangefilter,
    todos os campos desses tipos são feitos com a função DateRangeQuickSelectListFilterBuilder.
  #. Numéricos
    Campos DecimalField, IntegerField e PositiveIntegerField são modificados para um campo de busca,
    com autocomplete, se utilizando do pacote rangefilter, todos os campos desses tipos são feitos
    com a função NumericRangeFilterBuilder.
#. autocomplete_fields
#. list_select_related
#. filter_horizontal
#. exclude
#. advanced_filter_fields

Exemplo:
=======

.. code-block:: python

  from django.contrib import admin
  from novadata_utils.admin import NovadataModelAdmin

  from ..models import Exemplo


  @admin.register(Exemplo)
  class ExemploAdmin(NovadataModelAdmin):
      ...

Saída:
======

.. figure:: ../assets/images/example_novadata_model_admin1.png
  :alt: ExampleNovadataModelAdmin1
.. figure:: ../assets/images/example_novadata_model_admin2.png
  :alt: ExampleNovadataModelAdmin2
.. figure:: ../assets/images/example_novadata_model_admin3.png
  :alt: ExampleNovadataModelAdmin3
.. figure:: ../assets/images/example_novadata_model_admin4.png
  :alt: ExampleNovadataModelAdmin4