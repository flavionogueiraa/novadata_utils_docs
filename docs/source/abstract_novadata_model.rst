=====================
AbstractNovadataModel
=====================

Classe que implementa extamente as mesmas funcionalidades da ``NovadataModel``,
porém, de maneira abstrata

Código da classe:
=================

.. code-block:: python

    from .novadata_model import NovadataModel


    class AbstractNovadataModel(NovadataModel):
        class Meta:
            """Sub classe para definir meta atributos da classe principal."""

            abstract = True


Exemplo de uso:
===============

.. code-block:: python

    from django.db import models
    from novadata_utils.models import NovadataModel


    class Exemplo(NovadataModel):
        nome = models.CharField(
            verbose_name="Nome",
            max_length=100,
        )

        # Restante dos atributos

        def __str__(self):
            """Método que retorna a representação do objeto como string."""
            return self.nome

        class Meta:
            """Sub classe para definir meta atributos da classe principal."""

            app_label = "core"
            verbose_name = "Exemplo"
            verbose_name_plural = "Exemplos"

Com isso você conseguirá automaticamente ter os campos de data de criação e atualização,
além de usuário de criação e atualização, que serão preenchidos automaticamente.

.. seealso::

    A diferença dessa classa para a ``NovadataModel`` é que essa classe é abstrata,
    ou seja, não é possível criar objetos dessa classe diretamente, apenas herdar dela.

    Isso faz com que a sua sub classe tenha os campos de data de criação e atualização
    presentes nela mesma, e não em uma classe pai. Isso é ótimo para projetos que já
    estão em andamento e o uso de uma herança atrapalharia o andamento do mesmo.
