# Distribuindo staging iOS

Aqui vamos distribuir pro grupo de devs o app pronto antes de lançar na plataforma.

No AppCenter, selecione seu app iOS, vá em `Build`, puxe ele do Github. Entre na config.

![fig1](imgs/fig1.png)

> Daqui pra frente estou printando o do professor. O app se chama TedX

Em `Shared Scheme`, selecione a versão staging criada no xcode.

![fig2](imgs/fig2.png)

Marque `Automatically increment build number`, pra sempre versionar diferente a cada build.

![fig3](imgs/fig3.png)

Deixe `Sign builds` marcado. Faça upload do `Provisioning Profile` e o `Certificate`. Vc aprendeu como emití-los no **tópico 5.2 - Configurando ambiente no iOS**. 

![fig4](imgs/fig4.png)

Vc possui 3 provisioning profiles (AdHoc, Development, Production). Selecione o `AdHoc`.

![fig5](imgs/fig5.png)

Pro certificado, coloque o certificado de produção.

![fig6](imgs/fig6.png)

Marque `Distribute builds` > `Groups` > `Collaborators`

![fig7](imgs/fig7.png)

Dê um `Save & Build`.

Automaticamente vc e seu grupo receberão um e-mail com o `Install` do app pra iPhone, sem q ele esteja na plataforma pra produção.

> PS: só dá pra abrir a url pra install pelo Safari