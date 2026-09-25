# Plano de testes das regras

Use o Firebase Emulator Suite antes de publicar.

### Deve permitir
- usuário autenticado ler `config/spaces`;
- usuário autenticado ler configurações de uma pelada;
- usuário criar o próprio `players/{uid}`;
- usuário editar o próprio `players/{uid}`;
- usuário criar evento com `by == request.auth.uid`;
- administrador criar/editar `config/*`;
- administrador editar `players/*`;
- administrador editar `finance/*`.

### Deve negar
- usuário não autenticado ler qualquer coleção;
- usuário editar `players/{outroUid}`;
- jogador criar/alterar `finance/{uid}`;
- jogador alterar `config/*`;
- jogador excluir jogador;
- jogador criar evento fingindo ser outro UID;
- upload de arquivo que não seja imagem;
- upload de imagem acima de 5 MB;
- escrita em qualquer coleção não declarada.

### Atenção
O HTML atual grava parte do status de presença dentro de `players/{uid}`.
As regras permitem ao próprio jogador editar o próprio documento porque esse é
o modelo usado pela aplicação atual. Se futuramente quiser separar presença
em uma coleção `matches/{matchId}/responses/{uid}`, as regras podem ficar
ainda mais restritivas.
