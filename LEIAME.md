# Teleprompter para Android

App de teleprompter feito com Capacitor 8. Lê os mesmos roteiros `.txt` do Teleprompter Multi Laudas 2014 (`//` separa laudas, `>>` destaca a linha, `**` cria espaço).

## Como gerar o APK (sem instalar Android Studio)

O GitHub compila o app de graça a cada alteração. Você só precisa fazer isso uma vez:

1. **Crie um repositório privado** no GitHub chamado `teleprompter-android`.
2. **Envie os arquivos.** Na página do repositório, clique em *uploading an existing file* e arraste para lá **o conteúdo** desta pasta (as pastas `.github`, `android`, `assets`, `www` e os arquivos soltos). Confirme em *Commit changes*.
   Pelo VS Code também funciona: abra a pasta e use *Publish to GitHub* como repositório privado.
3. **Cadastre a assinatura.** Em *Settings > Secrets and variables > Actions*, crie os 4 segredos descritos em `assinatura/SEGREDOS-DO-GITHUB.txt` (essa pasta vem no outro .zip e **não** vai para o GitHub).
4. **Rode a compilação.** Na aba *Actions*, abra *Gerar APK* e clique em *Run workflow*. Leva uns 5 minutos.
5. **Baixe o APK.** Ao terminar, clique na execução e baixe o arquivo em *Artifacts*. Ele vem num .zip; dentro está o `Teleprompter-1.0.N.apk`.

## Instalar no celular

Passe o `.apk` para o celular (WhatsApp para você mesmo, Google Drive ou cabo) e toque nele. Na primeira vez o Android pede para permitir a instalação de apps daquela origem (Drive, Arquivos, WhatsApp): permita e confirme.

Versões novas instalam por cima e **mantêm os roteiros**, desde que sejam assinadas com a mesma chave da pasta `assinatura`. Guarde essa pasta com cuidado.

## Atualizar o app

Toda a interface está em `www/index.html`. Alterou e enviou para o GitHub, ele gera um APK novo sozinho (a versão sobe a cada compilação).

## O que é nativo no app

- Tela cheia de verdade e tela sempre acesa enquanto o prompter está aberto.
- **Botões de volume** controlam a velocidade (ou iniciar e pausar, nos ajustes). Fora do prompter eles voltam a mudar o volume normalmente.
- **Botão voltar** do Android fecha ajustes, prompter e editor, um de cada vez.
- **Exportar** gera o `.txt` e abre o compartilhar do Android (WhatsApp, Drive, e-mail).
- Funciona **sem internet**: a fonte vai embutida no app.

## Estrutura

```
www/index.html            interface completa (HTML, CSS e JS)
www/capacitor.js          ponte com o Android (vem do @capacitor/core)
www/fonts/                fonte Atkinson Hyperlegible
android/.../PrompterPlugin.java   tela acesa + botões de volume
android/.../MainActivity.java     registra o plugin e intercepta o volume
.github/workflows/build-apk.yml   compilação automática
assets/                   ícone e splash (regenere com `npm run icons`)
```

## Compilar no computador (opcional)

Com Node 22, JDK 21 e Android Studio instalados:

```
npm ci
npx cap sync android
npx cap open android
```

Para o APK assinado pelo Android Studio, use *Build > Generate Signed App Bundle or APK* com o arquivo `assinatura/teleprompter.keystore`.
