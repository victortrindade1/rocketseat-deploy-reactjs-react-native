# Configurando ambiente no iOS

No Mac, procure por `Keychain Access`. Lá, vá em `Certificate assistant` > `Request certificate from a certificate Authority...`:

![fig1](imgs/fig1.png)

Preencha seu e-mail, selecione `Saved to disk` e dê um continue:

![fig2](imgs/fig2.png)

Escolha a pasta q desejar. O professor preferiu criar uma pasta `Apple` pq daqui pr frente serão vários arquivos q a Apple vai exigir. O nome do arquivo é indiferente. O professor trocou o nome de `CertificateSigningRequest.certSigningRequest` pra `CSR.certSigningRequest`.

![fig3](imgs/fig3.png)

Acesse <https://developer.apple.com>. Vá em Account > Certificates > Production > Adicione um novo certificado:

![fig4](imgs/fig4.png)

Marque `App Store and Ad Hoc` > `Continue`:

![fig5](imgs/fig5.png)

Faça upload do certificado gerado:

![fig6](imgs/fig6.png)

Faça o Download do certificado pronto:

![fig7](imgs/fig7.png)

Clique no certificado baixado, e dê um `export`:

![fig8](imgs/fig8.png)

Fique atento ao formato `.p12`. O Professor salvou com o nome `Producao`. No momento de salvar, pede pra gerar uma senha pra ele, e tb pede a senha do PC. Em vez de `Allow`, clique em `Always Allow`.

![fig9](imgs/fig9.png)

No portal da Apple, vá em `Provisioning Profiles` > `All`:

![fig10](imgs/fig10.png)

Adicione um novo provisionamento:

![fig11](imgs/fig11.png)

O primeiro perfil de provisionamento será o `iOS App Development` > Continue:

![fig12](imgs/fig12.png)

Em `App ID`, selecione seu app (é pra aparecer lá no combobox) > Continue. Selecione o certificado de desenvolvimento. Selecione os dispositivos de iPhone (Select All) > Preencha o nome (Development) > Continue:

![fig13](imgs/fig13.png)

Faça download desse certificado pra mesma pasta Apple q já tá o outro.

Gere mais 2 certificados de provisionamento. O primeiro deles será o `Ad Hoc`:

![fig14](imgs/fig14.png)

Mesmo procedimento q o anterior: selecione o app no combobox, selecione o certificado, selecione iPhone e coloque um nome (AdHoc) > Continue > Download:

![fig15](imgs/fig15.png)

Vamos gerar o último certificado. Provisioning Profiles > All > + > Selecione `App Store`:

![fig16](imgs/fig16.png)

Mesmo procedimento q os anteriores: selecione o app no combobox, selecione o certificado, selecione iPhone e coloque um nome (Production) > Continue > Download:

![fig17](imgs/fig17.png)

Como não estamos desenvolvendo pra tvOS, vamos deletar os 2 targets pra tv no xcode só pra não atrapalhar:

![fig18](imgs/fig18.png)

Em Project no xcode, vá em Configurations > Release > + > `Duplicate "Release" Configuration`:

![fig19](imgs/fig19.png)

Chame de `Staging` essa nova Release.

Configure o Staging pra ter as mesmas configurações do Release. Para isso, no projeto do xcode, vá em `Build Settings`. Deixe as opções `All` e `Levels` selecionadas. Procure na barra de busca por `per-configuration`. Em `Per-configuration Build Products Path`, vá em `Staging`:

![fig20](imgs/fig20.png)

Dê duplo clique no `build/Staging-iphoneos` que está na coluna do projeto. O valor q aparecerá será `$(BUILD_DIR)/$(CONFIGURATION)$(EFFECTIVE_PLATFORM_NAME)`. Troque o valor `$(CONFIGURATION)` por `Release`. Ficará assim:

![fig21](imgs/fig21.png)

O correto é q fique assim: `build/Release-iphoneos`. Se vc clicar no de cima, tem q aparecer igual:

![fig22](imgs/fig22.png)

Apague o q estava na barra de busca. Lá em cima, clique no `+` e em `Add User-Defined Setting`:

![fig23](imgs/fig23.png)

Vai aparecer uma nova linha pra acrescentar, nela insira o valor `CODEPUSH_KEY`. Lá em cima, desmarque `Levels` e marque `Combined` pra facilitar a próxima visualização. Ao expandir a linha criada, veremos as linhas Debug, Release e Staging. São nelas q colocaremos nossas Keys do Appcenter. Assim como fizemos pra ver as Keys no Android, faremos igual pra iOS. No terminal, liste suas Keys pra iOS:

`appcenter codepush deployment list -a <nome_da_empresa>/<nome_do_app> -k`

Ficou assim o meu:
`appcenter codepush deployment list -a victortrindade/Go-Barber-iOS -k`

Cole a key de Staging em Staging, e a Production em Release. Debug fica em branco:

![fig24](imgs/fig24.png)

(tá acabando...)

Vá em `Info.plist`. Procure pela linha `CodePushDeploymentKey`. Onde está escrito `deployment-key-here`. Troque este valor para `$(CODEPUSH_KEY)`:

![fig25](imgs/fig25.png)

Vá em `Product` > `Scheme` > `Manage Schemes...`:

![fig26](imgs/fig26.png)

Vc pode deletar a linha do projeto com `tvOS`. Pra isso, selecione a linha, clique em `-` > `Delete`.

Selecione a linha do projeto. Na engrenagem, clique em `Duplicate`:

![fig27](imgs/fig27.png)

Renomeie o scheme duplicado pra `nome_do_app-staging`:

![fig28](imgs/fig28.png)

Salve. Na tela dos schemes, deixe a opção `Shared` marcada da linha criada. Após, clique em `Edit`:

![fig29](imgs/fig29.png)

Dentro de `Run`, vá no combobox `Build Configuration` e deixe marcada a opção `Staging`:

![fig30](imgs/fig30.png)

Faça o mesmo em `Archive`:

![fig31](imgs/fig31.png)

Volte no projeto do xcode. Em `Signing`, desmarque a opção `Automatically manage signing`. Ao desmarcar, aparecerão 3 grupos abaixo: Signing (Debug), Signing (Release) e Signing (Staging). Em todos eles, vc irá em `Provisioning Profile` > `Import Profile`. Vc vai selecionar aqueles provisionamento salvos anteriormente. Pra `Debug` será `Development`, pra `Release` será `Production` e pra `Staging` será `AdHoc`:

![fig32](imgs/fig32.png)
