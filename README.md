# Fullstack Pokemon BattleSystem

**Fullstack Pokemon BattleSystem** é um sistema web completo que integra uma API desenvolvida em **.NET 8** com **Entity Framework Core (SQLite)** e um frontend em **React + TypeScript**.  
O projeto permite cadastrar, listar e gerenciar Pokémons, seus tipos e batalhas, simulando uma lógica básica de confronto entre criaturas cadastradas.

#

## Sumário
- [Visão geral](#visão-geral)
- [Arquitetura](#arquitetura)
- [Tecnologias utilizadas](#tecnologias-utilizadas)
- [Funcionalidades principais](#funcionalidades-principais)
- [Como executar o projeto](#como-executar-o-projeto)
  - [Backend (.NET 8)](#backend-net-8)
  - [Frontend (React + TypeScript)](#frontend-react--typescript)
- [Endpoints da API](#endpoints-da-api)
- [Estrutura de pastas](#estrutura-de-pastas)
- [Notas importantes](#notas-importantes)

#

## Visão geral

O sistema foi desenvolvido como um **projeto full-stack** com fins didáticos e de portfólio.  
O objetivo é demonstrar domínio em integração de camadas, persistência de dados e desenvolvimento de interfaces modernas, simulando um sistema funcional de batalhas Pokémon.

O projeto contém:

- Backend com API REST (C# + .NET 8)
- Frontend com React + TypeScript
- Banco de dados SQLite via Entity Framework Core
- Comunicação entre camadas via HTTP/JSON com CORS liberado

#

## Arquitetura

- **Backend**: .NET 8 + Entity Framework Core + SQLite
- **Frontend**: React 18 + TypeScript (Create React App)
- **Comunicação**: API REST JSON
- **Infraestrutura local**: execução via `dotnet run` (API) e `npm start` (frontend)

#

## Tecnologias utilizadas

| Camada | Tecnologias |
|--------|--------------|
| Backend | .NET 8, C#, Entity Framework Core, SQLite |
| Frontend | React 18, TypeScript, React Router, Axios |
| Ferramentas | Visual Studio / VS Code, Node.js 18+, npm |

#

## Funcionalidades principais

- CRUD completo de **Pokémon Wiki** (cadastro geral de espécies)
- CRUD completo de **Seus Pokémons** (coleção pessoal)
- CRUD de **Tipos** (tipagem elemental)
- **Sistema de Batalha** entre Pokémons cadastrados
- Controle de integridade (nome único, tipos associados)
- Interface interativa e responsiva para gerenciamento

#

## Como executar o projeto

### Pré-requisitos

- **.NET 8 SDK**
- **Node.js 18+** e **npm**
- **SQLite** (já configurado no projeto)

#

### Backend (.NET 8)

```bash
cd API/API

# Restaurar dependências
dotnet restore

# (Opcional) aplicar migrações manuais
# dotnet ef database update

# Executar o servidor
dotnet run
```

A API estará disponível em:
```
http://localhost:5244
```

O banco SQLite (`pokemons.db`) será criado automaticamente na primeira execução.

#

### Frontend (React + TypeScript)

```bash
cd front
npm install
npm start
```

O frontend será iniciado em:
```
http://localhost:3000
```

> Certifique-se de que o endpoint da API em `src/components/pages` aponte para `http://localhost:5244`.  
> Caso altere a porta da API, ajuste as URLs de `fetch` ou `axios` no frontend.

#

## Endpoints da API

### Pokemon Wiki
| Método | Endpoint | Descrição |
|---------|-----------|-----------|
| `GET` | `/api/pokemon_wiki/listar` | Lista todos os Pokémons da wiki |
| `GET` | `/api/pokemon_wiki/buscar/{nome}` | Busca um Pokémon pelo nome |
| `POST` | `/api/pokemon_wiki/cadastrar` | Cadastra novo Pokémon |
| `PUT` | `/api/pokemon_wiki/alterar/{nome}` | Atualiza dados do Pokémon |
| `DELETE` | `/api/pokemon_wiki/deletar/{nome}` | Exclui Pokémon existente |

> Nome é único (restrição no banco).

#

### Seus Pokémons
| Método | Endpoint | Descrição |
|---------|-----------|-----------|
| `GET` | `/api/seu_pokemon/listar` | Lista os Pokémons do usuário |
| `GET` | `/api/seu_pokemon/buscar/{id}` | Busca Pokémon pelo ID |
| `POST` | `/api/seu_pokemon/cadastrar` | Cadastra novo Pokémon pessoal |
| `PUT` | `/api/seu_pokemon/alterar/{id}` | Atualiza informações |
| `DELETE` | `/api/seu_pokemon/deletar/{id}` | Exclui Pokémon pessoal |

#

### Batalhas
| Método | Endpoint | Descrição |
|---------|-----------|-----------|
| `GET` | `/api/batalha/listar` | Lista batalhas registradas |
| `GET` | `/api/batalha/buscar/{id}` | Busca batalha específica |
| `POST` | `/api/batalha/cadastrar/{pokemonId1}/{pokemonId2}` | Cria batalha entre dois Pokémons |
| `DELETE` | `/api/batalha/deletar/{id}` | Remove batalha registrada |

#

### Tipos
| Método | Endpoint | Descrição |
|---------|-----------|-----------|
| `GET` | `/api/tipo/listar` | Lista todos os tipos |
| `POST` | `/api/tipo/cadastrar` | Cadastra novo tipo |
| `DELETE` | `/api/tipo/deletar/{id}` | Remove tipo (somente se não vinculado a Pokémon) |

#

## Estrutura de pastas

```
API/
  API/
    Program.cs
    Models/
      AppDataContext.cs
      PokemonWiki.cs
      SeusPokemons.cs
      Batalha.cs
      Tipo.cs
    Migrations/
    appsettings.json
    pokemons.db
front/
  src/
    App.tsx
    components/
      pages/
        home/
        pokemonWiki/
        seusPokemons/
        batalha/
    models/
  package.json
```

#

## Notas importantes

- **CORS**: configurado para permitir acesso total (`"Acesso Total"`).  
- **Banco de dados**: o arquivo `pokemons.db` é criado automaticamente.  
- **Migrações EF Core**: caso altere modelos, execute `dotnet ef migrations add <nome>` e `dotnet ef database update`.  
- **Validação de nomes**: `PokemonWiki.Nome` é índice único.

#
