# EVE_ReShade

Mostra a configuração do EVE (Extended Video Export) na aba **Add-ons** do ReShade e grava no `ExtendedVideoExport.ini`.

> Este código **não foi compilado nem testado** (foi escrito sem acesso a compilador Windows nem aos headers do ReShade). Se der erro de compilação, me mande a mensagem que eu corrijo.

## Compilar

Requisitos: Visual Studio 2022 (carga "Desenvolvimento para desktop com C++"), CMake e Git.

```bat
git clone --recurse-submodules https://github.com/crosire/reshade C:\reshade
cd EVE_ReShade
cmake -B build -A x64 -DRESHADE_DIR=C:\reshade
cmake --build build --config Release
```

Saída: `build\Release\EVE_ReShade.addon64`

## Compilar sem instalar nada (GitHub Actions)

1. Crie um repositório no GitHub e envie todos os arquivos desta pasta, incluindo `.github/workflows/build.yml`.
2. Aba **Actions** → **Build EVE_ReShade** → **Run workflow**.
3. Quando terminar, baixe o artefato **EVE_ReShade** (contém o `EVE_ReShade.addon64`).

## Instalar

1. Precisa do **ReShade com suporte a addons** (o instalador "Addon Support"). O 6.5.1 já funciona com o EVE.
2. Copie `EVE_ReShade.addon64` para a pasta onde o ReShade procura addons (a mesma do `ReShade.ini`/`dxgi.dll` do FiveM, ou a pasta definida em ReShade → Configurações → *Add-on search paths*).
3. Deixe o `ExtendedVideoExport.asi` e a pasta `EVE` na `plugins` do FiveM, como no README do EVE.
4. Abra o jogo, aperte **Home** (overlay do ReShade) → aba **Add-ons** → seção **EVE - Extended Video Export**.

Se o addon não aparecer mesmo na pasta certa, renomeie para `EVE_ReShade.asi` e coloque na `plugins` do FiveM, como o EVER fazia.

## Como funciona

- O caminho do `.ini` é detectado sozinho (`%LOCALAPPDATA%\FiveM\FiveM.app\plugins\EVE\`). Se não achar, digite no campo "Caminho do .ini"; ele fica salvo em `EVE_ReShade.ini`, ao lado do addon.
- Alterou algo? Clique em **Salvar no .ini**. Com `auto_reload_config = true`, o EVE lê o arquivo de novo antes de cada exportação, então vale na próxima.
- `enable_mod` só muda depois de reiniciar o jogo.
- O parser preserva o resto do `.ini` (comentários, linhas desconhecidas) e aceita as chaves fora de seção.
