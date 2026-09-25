# Configuração Firebase

## 1. Criar projeto
No Firebase Console, crie um projeto e registre um app Android com:
`br.com.pelada.app`

Baixe `google-services.json` e coloque em:
`app/google-services.json`

## 2. Authentication
Ative Authentication. Esta versão usa login anônimo para permitir teste imediato.
Para produção, recomendo ativar também E-mail/Senha ou Google.

## 3. Firestore
Crie o banco em modo produção e publique `firestore.rules`.

## 4. Storage
Ative Cloud Storage e publique `storage.rules`.

## 5. Web App config
No `app/src/main/assets/pelada.html`, substitua:
- COLOQUE_SUA_API_KEY
- SEU_PROJETO
- SEU_SENDER_ID
- SEU_APP_ID

pela configuração do seu Firebase Web App.

A configuração web contém identificadores do projeto; a segurança deve ser feita pelas regras do Firebase e pela autenticação, não escondendo esses valores no HTML.
