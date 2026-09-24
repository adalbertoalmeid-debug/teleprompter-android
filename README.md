# Teleprompter para Android

Teleprompter para celular Android, feito com [Capacitor](https://capacitorjs.com). Funciona sem internet, no próprio aparelho ou com vidro de teleprompter, e lê os roteiros `.txt` no formato do antigo *Teleprompter Multi Laudas*.

## Recursos

- Roteiros salvos no aparelho, com editor, importação e exportação de `.txt` (inclusive arquivos antigos do Windows).
- Marcações: `//` separa as laudas, `>>` no início da linha destaca a linha, `**` numa linha sozinha cria um espaço.
- Leitura de todas as laudas ou de uma só, com salto entre laudas.
- Espelho horizontal e vertical para vidro de teleprompter.
- Ajuste de velocidade, tamanho da letra, espaçamento, margem, alinhamento, caixa alta e cores.
- Setas e linha de referência de leitura, cronômetro e contagem regressiva.
- Tela cheia e tela sempre acesa durante a leitura.
- **Botões de volume** controlam a velocidade (ou iniciar e pausar). Também funciona com controle remoto Bluetooth, pedal e teclado (espaço, setas, Page Up/Down, Home, End).

App irmão, para gravar vídeo com o texto rolando: [Teleprompter Câmera](https://github.com/adalbertoalmeid-debug/teleprompter-camera).

## Estrutura

```
www/index.html                     interface completa (HTML, CSS e JS)
android/.../PrompterPlugin.java    tela acesa e botões de volume
android/.../MainActivity.java      registra o plugin e intercepta o volume
.github/workflows/build-apk.yml    compilação automática do APK
assets/                            ícone e splash (regenere com npm run icons)
```

## Compile a sua versão

O projeto compila sozinho no GitHub Actions, sem precisar de Android Studio:

1. Faça um **fork** deste repositório.
2. Gere a sua própria chave de assinatura (uma vez só):
   ```
   keytool -genkeypair -keystore minha.keystore -alias minhachave -keyalg RSA -keysize 2048 -validity 10000
   ```
   Depois converta para base64 (no Linux/Mac: `base64 -w0 minha.keystore`; no PowerShell: `[Convert]::ToBase64String([IO.File]::ReadAllBytes("minha.keystore"))`).
3. Em **Settings > Secrets and variables > Actions**, crie os segredos `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS` e `KEY_PASSWORD`.
4. Em **Actions > Gerar APK > Run workflow**, rode a compilação. O APK aparece em **Artifacts** ao final.

Guarde a sua chave fora do repositório: sem ela, versões novas não instalam por cima da anterior.

Para compilar no computador: Node 22, JDK 21 e Android Studio, com `npm ci`, `npx cap sync android` e `npx cap open android`.

## Licença e créditos

Criado por **Beto Almeida** ([adalbertoalmeida.com.br](https://adalbertoalmeida.com.br)).

Distribuído sob a [Apache License 2.0](LICENSE). Você pode usar, modificar e distribuir, inclusive em projetos comerciais, **desde que dê o crédito**: mantenha os arquivos [`LICENSE`](LICENSE) e [`NOTICE`](NOTICE) em qualquer cópia ou versão derivada e indique que o projeto original é de Beto Almeida.

Uma forma simples de dar o crédito no seu projeto:

> Baseado no [Teleprompter](https://github.com/adalbertoalmeid-debug/teleprompter-android) de Beto Almeida (adalbertoalmeida.com.br), licenciado sob Apache 2.0.
