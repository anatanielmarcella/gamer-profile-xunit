# gamer-profile-xunit

Projeto da disciplina **Garantia da Qualidade de Software**: um serviço simples de cadastro de jogadores (`GamerProfile`) em **C# / .NET**, coberto por testes unitários com **xUnit**.

## Propósito do sistema

O `PerfilJogadorService` reúne três regras de negócio de um perfil de jogador:

| Método | Retorno | O que faz |
|---|---|---|
| `GerarTagUsuario(nickname, codigo)` | `string` | Junta nickname e código com `#` (ex.: `Aragorn#1042`) |
| `CalcularXPTotal(xpFase1, xpFase2)` | `int` | Soma o XP de duas fases e aplica bônus fixo de 100 pontos |
| `EEligivelParaRanked(nivelJogador)` | `bool` | Retorna `true` para nível maior ou igual a 15 |

## Testes unitários realizados

Os testes ficam em `GamerProfile.Tests` e seguem o padrão AAA (Arrange, Act, Assert). Cada tipo de retorno usa uma asserção diferente:

1. **Teste de string** (`Assert.Equal`): verifica se a tag é gerada no formato `Nickname#0000`.
2. **Teste de int** (`Assert.Equal`): verifica se a soma das fases mais o bônus de 100 pontos está correta.
3. **Teste de bool** (`Assert.True` e `Assert.False`): verifica a elegibilidade para partidas ranqueadas, com `true` a partir do nível 15 e `false` abaixo dele.

## Estrutura

```
gamer-profile-xunit/
├── GamerProfile.App/      # Código de produção (PerfilJogadorService)
├── GamerProfile.Tests/    # Testes unitários com xUnit
├── GamerProfile.slnx      # Solução (ou .sln, conforme a versão do SDK)
├── .gitignore
├── LICENSE
└── README.md
```

## Pré-requisitos

- [.NET SDK 10](https://dotnet.microsoft.com/download) ou superior
- [Git](https://git-scm.com/)

## Como executar os testes

```bash
git clone https://github.com/GabrielGobira/gamer-profile-xunit.git
cd gamer-profile-xunit
dotnet test
```

Se tudo estiver certo, o resultado mostra os testes aprovados (`Passed`).

## Como a solução foi criada

```bash
dotnet new sln -n GamerProfile
dotnet new console -n GamerProfile.App -f net10.0
dotnet new xunit -n GamerProfile.Tests -f net10.0
dotnet sln add GamerProfile.App/GamerProfile.App.csproj
dotnet sln add GamerProfile.Tests/GamerProfile.Tests.csproj
dotnet add GamerProfile.Tests/GamerProfile.Tests.csproj reference GamerProfile.App/GamerProfile.App.csproj
```

## Autor

**Gabriel Gobira** — [@GabrielGobira](https://github.com/GabrielGobira)

## Licença

Distribuído sob a licença MIT. Veja o arquivo [LICENSE](LICENSE).