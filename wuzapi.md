# Inicialização

- Crie uma build rodando este codigo no terminal:

```
go build .
```

- Logo após, inicie o servidor para verificar se está funcionando corretamente:

```
./wuzapi -admintoken={env.WUZAPI_ADMIN_TOKEN}
```

- Abra http://localhost:8080/api/#/ para ter acesso a documentação do wuzapi

- Autentique com o token cadastrado na Env

# Sessão

- inicie uma sessão em http://localhost:8080/api/#/Session/post_session_connect

- Para enviar mensagens, use o endpoint /chat/send/text, com body:

```
{
  "Phone": ["Telefone do Contato para enviar Mensagem"],
  "Body": ["Mensagem a enviar"],  
  // Contexto para responder a uma mensagem
  "ContextInfo": {
    "StanzaId": ["ID da mensagem"],
    "Participant": "['Telefone do Contato']@s.whatsapp.net"
  }
}
```