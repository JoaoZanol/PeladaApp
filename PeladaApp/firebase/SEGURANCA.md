# Segurança do Firebase — Pelada

## Camadas

1. **Firebase Authentication**
   - Só usuários autenticados acessam o banco.
   - O app atual inicia com autenticação anônima para teste.
   - Para produção, recomenda-se habilitar Google, telefone ou e-mail/senha.

2. **Cloud Firestore Rules**
   - Jogador só pode criar/editar o próprio perfil.
   - Financeiro só pode ser alterado pelo administrador.
   - Configuração de partidas, times, espaços e churrasco é administrativa.
   - Eventos só podem ser criados pelo usuário autenticado que consta em `by`.
   - Qualquer coleção não prevista é bloqueada pelo `match /{document=**}`.

3. **Cloud Storage Rules**
   - Foto do jogador só pode ser gravada pelo próprio UID.
   - Fotos são limitadas a 5 MB e tipo `image/*`.
   - Branding/logo só pode ser alterado por administrador.

## Primeiro administrador

Após autenticar no aplicativo:

`admins/{UID}`

```json
{
  "uid": "UID_DO_USUARIO",
  "role": "admin",
  "name": "Organizador"
}
```

A criação do primeiro administrador precisa ser feita de forma controlada no
Firebase Console ou por uma ferramenta administrativa segura. Depois disso,
os administradores podem gerenciar as configurações permitidas pelas regras.

## Observação importante

As regras são uma barreira de segurança do banco; esconder botões no WebView
não é uma medida de segurança.

Antes de publicar o app, teste as regras no Firebase Emulator Suite e revise
as permissões conforme o fluxo definitivo de login.

## Dados financeiros

O aplicativo usa `finance/{uid}`. Nesta versão, somente administradores podem
criar, alterar e excluir esses documentos. O jogador pode apenas ler o próprio
financeiro.

## Princípio de menor privilégio

O padrão final é negar tudo e liberar apenas:
- leitura autenticada necessária;
- escrita no próprio perfil;
- operações administrativas;
- upload da própria foto.
