# Pelada App — Android WebView + Firebase

Projeto baseado no `pelada.html` fornecido.

Arquitetura:
Android -> WebView -> Firebase Authentication -> Cloud Firestore / Cloud Storage

O app usa o Firebase Web SDK dentro do WebView para manter a interface existente.
A autenticação inicial é anônima para teste; a versão de produção pode usar E-mail/Senha ou Google.

Passos:
1. Coloque app/google-services.json.
2. Configure o Firebase Web App em pelada.html.
3. Ative Authentication.
4. Crie Firestore.
5. Publique firebase/firestore.rules.
6. Ative Storage.
7. Publique firebase/storage.rules.
8. Faça login no app e crie admins/{UID} para o organizador.
9. Abra no Android Studio e gere o APK/AAB.

Documentação oficial:
https://firebase.google.com/docs/android/setup
https://firebase.google.com/docs/auth/android/start
https://firebase.google.com/docs/web/setup

## Estrutura das coleções

A versão agora inclui:
- `firebase/firestore-schema.json` — schema completo das coleções/documentos;
- `firebase/seed-data.json` — dados iniciais de exemplo;
- `firebase/ESTRUTURA_FIREBASE.md` — guia da estrutura e relacionamento;
- `firebase/firestore.rules` — regras de segurança;
- `firebase/storage.rules` — regras para fotos.

Coleções principais:
`admins`, `players`, `finance`, `config` e `events`.

## Segurança

A versão atual inclui regras de segurança reforçadas:
- autenticação obrigatória;
- jogador limitado ao próprio perfil;
- financeiro somente para administradores;
- configurações somente para administradores;
- eventos vinculados ao UID autenticado;
- Storage limitado ao próprio usuário/admin;
- limite de 5 MB e validação de `image/*`;
- bloqueio padrão de documentos não previstos.

Arquivos:
- `firebase/firestore.rules`
- `firebase/storage.rules`
- `firebase/SEGURANCA.md`
- `firebase/firestore.rules.test-plan.md`
