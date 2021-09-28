# Enviando alteração via Code Push

Efetua qualquer alteração no app. Rode o comando:

`appcenter codepush release-react -a <nome_da_empresa>/<nome_do_app>`

Após efetuar qualquer alteração no código, o usuário já abrirá o app atualizado automaticamente. 

Lembrando q se vc precisar instalar uma lib nativa (onde tem q rodar `react-native link`), não atualizará. Neste caso, crie uma nova build.
