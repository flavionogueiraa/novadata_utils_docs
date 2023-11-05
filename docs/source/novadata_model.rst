=============
NovadataModel
=============

Classe para facilitar a criação de uma model, implmentando algumas funcionalidades úteis
e também definindo alguns atributos geralmente usados.

Código da classe:
=================

.. code-block:: python

    from django.conf import settings
    from django.db import models


    class NovadataModel(models.Model):
        data_criacao = models.DateTimeField(
            verbose_name="Data de criação",
            auto_now_add=True,
        )

        data_atualizacao = models.DateTimeField(
            verbose_name="Data de atualização",
            auto_now=True,
        )

        usuario_criacao = models.ForeignKey(
            settings.AUTH_USER_MODEL,
            on_delete=models.SET_NULL,
            verbose_name="Usuário de criação",
            blank=True,
            null=True,
        )

        usuario_atualizacao = models.ForeignKey(
            settings.AUTH_USER_MODEL,
            related_name="%(class)s_requests_modified",
            verbose_name="Usuário de atualização",
            on_delete=models.SET_NULL,
            blank=True,
            null=True,
        )

        def save(self, *args, **kwargs):
            """Sobrescrita do método save para realizarmos ações personalizadas."""
            from crum import get_current_user

            user = get_current_user()
            if user and not user.pk:
                user = None
            if not self.pk:
                self.usuario_criacao = user
            self.usuario_atualizacao = user

            super(NovadataModel, self).save(*args, **kwargs)

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

.. warning::

    Usar a classe NovadataModel gera uma herança, ou seja, a sua classe Exemplo herda
    de NovadataModel, ficando vinculada a ela, isso nem sempre é o desejado, por isso,
    você pode herdar da ``AbstractNovadataModel``, que não gera uma herança, mas sim
    uma cópia dos atributos, veja mais sobre ela na próxima página.
