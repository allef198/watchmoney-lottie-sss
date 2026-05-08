# Ajustes feitos por ChatGPT

Este pacote foi ajustado para facilitar o uso no Firebase Studio:

1. Os arquivos Lottie foram movidos de `app/src/main/raw/` para `app/src/main/res/raw/`.
   Agora o código consegue usar `R.raw.coin_reward`, `R.raw.super_chest`, `R.raw.level_up_reward` e `R.raw.chest_progress`.

2. O arquivo duplicado `app/build.gradle` foi removido.
   O projeto agora usa apenas `app/build.gradle.kts`, que é o padrão Kotlin DSL já usado pelo projeto.

3. O `app/build.gradle.kts` foi ajustado para:
   - usar `compileSdk = 35`
   - usar `targetSdk = 35`
   - remover `buildToolsVersion` manual
   - adicionar dependência `lottie-compose`
   - adicionar dependência `kotlinx-coroutines-play-services`

4. O `.idx/dev.nix` foi corrigido para apontar `ANDROID_HOME` e `ANDROID_SDK_ROOT` para o Android SDK composto pelo Nix, contendo Platform 35 e Build Tools 35.
   Isso evita o erro de tentar instalar SDK dentro de `/nix/store`, que é somente leitura.

Depois de puxar no Firebase Studio, rode apenas:

```bash
./gradlew assembleDebug
```

Não rode `installDebug` se não tiver um celular/emulador conectado.
