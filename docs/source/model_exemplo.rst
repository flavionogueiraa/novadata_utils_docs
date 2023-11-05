================
Model de exemplo
================

Essa é a model que será usada de exemplo durante todas
as demonstrações feitas na documentação:

.. code-block:: python

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
