# Tornar o primeiro usuário administrador

Depois que o usuário entrar uma vez no app, pegue o UID dele no Firebase Authentication.

No Firestore, crie:
admins/{UID}

Campos:
uid: "{UID}"
role: "admin"

As regras usam esse documento para autorizar operações administrativas.
Em produção, mantenha o acesso administrativo restrito.
