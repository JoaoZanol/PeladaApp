# Estrutura do Firebase — Pelada

## Visão geral

```text
admins/{uid}
players/{uid}
finance/{uid}
config/spaces
config/{spaceId}
events/{eventId}
```

### 1. `admins/{uid}`

Controla quem possui acesso administrativo.

Campos:
- `uid`: UID do Firebase Authentication
- `role`: `admin`
- `name`: nome do administrador
- `createdAt`: timestamp

Para criar o primeiro administrador, faça login no app e crie manualmente
`admins/{UID_DO_USUARIO}` no Firestore.

---

### 2. `players/{uid}`

Cadastro global do jogador.

Campos:
- `name`
- `photo`
- `pos`
- `foot`
- `level`
- `bio`
- `sp`

`sp` guarda os dados específicos de cada pelada/espaço. Isso permite que o
mesmo usuário participe de mais de um espaço.

Exemplo:

```json
{
  "name": "João",
  "pos": "Atacante",
  "foot": "Destro",
  "level": "Fominha",
  "bio": "Bom passe e finalização",
  "sp": {
    "ssegunda": {
      "joined": 1727200000000,
      "status": "in",
      "for": "1727200000000",
      "at": 1727200000000
    }
  }
}
```

---

### 3. `finance/{uid}`

Financeiro individual.

O campo `sp` separa os dados financeiros por espaço.

Exemplo:

```json
{
  "sp": {
    "ssegunda": {
      "type": "mensalista",
      "paid": "2026-09"
    }
  }
}
```

---

### 4. `config/spaces`

Lista os espaços existentes.

Exemplo:

```json
{
  "list": [
    {
      "id": "ssegunda",
      "name": "Segundas"
    },
    {
      "id": "squarta",
      "name": "Quartas"
    }
  ]
}
```

---

### 5. `config/{spaceId}`

Configuração completa de cada pelada.

Contém:
- tipo de campo
- próxima partida
- times
- escalação
- identidade visual
- função financeira dos jogadores
- valores
- churrasco

O formato está detalhado em `firestore-schema.json`.

---

### 6. `events/{eventId}`

Feed de notificações/eventos.

Campos:
- `text`
- `icon`
- `at`
- `by`
- `sp`

Exemplo:

```json
{
  "text": "[Segundas] João confirmou presença",
  "icon": "",
  "at": 1727200000000,
  "by": "firebaseUid",
  "sp": "ssegunda"
}
```

---

## Fluxo de dados

```text
Firebase Authentication
        │
        └── UID
             │
             ├── players/{uid}
             ├── finance/{uid}
             └── admins/{uid}
                         │
                         ▼
                  config/{spaceId}
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       partida         times         churrasco
          │
          ▼
       events
```

## Segurança

As regras incluídas em `firestore.rules` seguem esta separação:

- usuário autenticado pode ler dados necessários;
- jogador pode criar/alterar o próprio perfil;
- administrador pode alterar configurações;
- financeiro fica protegido;
- administrador controla operações administrativas.

Em produção, recomenda-se revisar as regras antes de publicar o app.

## Índices

O aplicativo consulta eventos por `at` e, opcionalmente, por `sp + at`.
Os índices sugeridos estão no `firestore-schema.json`.
