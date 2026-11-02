# Fontes do FFmpeg Windows distribuído com AgoraEncontrei

Este repositório separado reúne fontes de projetos de código aberto, suas receitas de compilação, licenças e evidências de integridade para o runtime multimídia Windows selecionado para o AgoraEncontrei. Ele não contém o código proprietário da aplicação, dados de clientes ou credenciais.

A publicação destas fontes não significa que um novo instalador do AgoraEncontrei já foi concluído ou disponibilizado.

## Versão e procedência

- Fornecedor do binário: [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds).
- Release: [autobuild-2026-11-02-12-51](https://github.com/BtbN/FFmpeg-Builds/releases/tag/autobuild-2026-11-02-12-51).
- Variante: `win64-gpl-9.0`.
- Binário original: `ffmpeg-n9.0.2-45-g1e65c6cd5d-win64-gpl-9.0.zip`.
- SHA256 do ZIP binário: `20e6537e293473506d79ef4a6b203bc6b9735a9d3d225c28e05ef968b3438116`.
- [FFmpeg: commit 1e65c6cd5d3d2d12cbb374460dbf08bedf54772a](https://github.com/FFmpeg/FFmpeg/commit/1e65c6cd5d3d2d12cbb374460dbf08bedf54772a).
- [Receitas BtbN: commit 5ece62897c650b863c1ddda7b6964845344aef2d](https://github.com/BtbN/FFmpeg-Builds/tree/5ece62897c650b863c1ddda7b6964845344aef2d).
- Run de origem: `41442505918`; job Windows GPL 9.0: `125270469750`.
- Cache de fontes de origem: artifact `13140618173`, 2.240.577.944 bytes, SHA256 `2990fbaedcb3a0562dc7e7d18e9b279c57f9264d2ecc4656409c22a94c7605b7`.

O cache do GitHub Actions foi usado para obtenção e verificação. O link temporário desse artifact não deve ser usado como endereço permanente de distribuição.

## Como obter e conferir

Na seção **Releases** deste repositório, abra a versão `ffmpeg-sources-20261102-win64-gpl-9.0` e baixe os seis assets enviados manualmente: quatro partes ZIP, o catálogo `-parts.json` e o arquivo `-SHA256SUMS`.

Os links automáticos **Source code (zip)** e **Source code (tar.gz)** do GitHub são arquivos da árvore deste pequeno repositório; não substituem os quatro assets de fontes listados abaixo.

| Parte | Bytes | SHA256 |
|---|---:|---|
| `AgoraEncontrei-FFmpeg-sources-20261102-win64-gpl-9.0-part01.zip` | 676828532 | `92860de0c826bff6e84029bdb29910f6235a3fc2b392fa240ee49f9102824029` |
| `AgoraEncontrei-FFmpeg-sources-20261102-win64-gpl-9.0-part02.zip` | 605955964 | `f86e62364d7f4caf6756196aa1847b4300dc649a13924cee3ec39d9b72d71ed1` |
| `AgoraEncontrei-FFmpeg-sources-20261102-win64-gpl-9.0-part03.zip` | 697977194 | `4ff6792e51b87802d42347899e65069986a059b3c19f783660c84f1d04b724c4` |
| `AgoraEncontrei-FFmpeg-sources-20261102-win64-gpl-9.0-part04.zip` | 218763471 | `0198fdebf761efc1a8d4c9846978abdcccfaeaaed2dea15bfe32a35649b5ec4b` |

Cada parte é um ZIP independente, abaixo de 700 MiB. **Não concatene as partes.** Extraia todas na mesma pasta inicialmente vazia, preservando a estrutura de diretórios. Não é necessário executar nenhum arquivo para consultar as fontes.

No Windows, confira o SHA256 de cada ZIP com `Get-FileHash -Algorithm SHA256 -LiteralPath "nome-do-arquivo.zip"` e compare o resultado com a tabela ou o arquivo `-SHA256SUMS`. O catálogo `-parts.json` informa quais arquivos estão em cada parte. Depois da extração, `MANIFEST.json` e `SHA256SUMS` permitem conferir individualmente os arquivos internos.

## Conteúdo

- `upstream/`: fontes do FFmpeg e rav1e fixadas, além das receitas completas do fornecedor.
- `dependencies-cache/`: 98 arquivos de fontes comprimidos correspondentes à seleção registrada no job Windows. Permanecem em seus formatos originais, com submódulos e materiais da fase de obtenção preservados. O hash no nome de um cache identifica sua receita; os hashes dos bytes estão no manifesto.
- `rust-rav1e/`: 116 arquivos de crates verificados contra o Cargo.lock original fixado, com uma seleção conservadora que também inclui dependências opcionais/de plataforma e ferramentas transitivas. Isso não é uma lista mínima dos símbolos ligados no binário.
- `licenses/`: cópias auxiliares dos avisos encontrados. Os avisos originais continuam nas fontes. Alguns projetos usam cabeçalhos ou `AUTHORS` em vez de um arquivo chamado `LICENSE`; por exemplo, r-efi inclui seus termos em `AUTHORS`.
- `GPL-3.0.txt`, `README-PT.txt`, `MANIFEST.json`, `SHA256SUMS` e `source-verification.json`: licença, instruções, procedência e verificações.

As 98 entradas de cache foram recuperadas sem faltantes na seleção. A inspeção estática leu 182.032 entradas. Os quatro ZIPs finais passaram por leitura integral de CRC e conferência SHA256 dos 1.306 arquivos manifestados; há 1.308 entradas incluindo o próprio manifesto e a lista de hashes.

## Receitas e reconstrução

Leia o README e os diretórios `images/`, `scripts.d/` e `patches/` nas receitas BtbN incluídas. Os scripts `generate.sh`, `makeimage.sh` e `build.sh` documentam a configuração do fornecedor. Os arquivos de `dependencies-cache/` podem alimentar o diretório `.cache/downloads` das receitas, mantendo os nomes.

A fonte FFmpeg está incluída separadamente porque o fornecedor a obtém fora do download-cache. Para usar a mesma revisão, fixe o commit informado acima; não substitua pela revisão atual de uma branch móvel.

Esta coleção não promete um ambiente de compilação totalmente offline nem resultado idêntico byte a byte. A criação do ambiente pode exigir ferramentas de compilação adicionais. A receita rav1e executa `cargo update cc`; o lock posterior a essa etapa não foi recuperado. Os crates fornecidos usam o lock original, e essa diferença de ferramenta está explicitada, sem presumir dispensa de fontes de bibliotecas efetivamente incorporadas.

## Licenças e atribuições

O binário BtbN selecionado declara GPL-3.0-or-later. As bibliotecas e ferramentas incluídas mantêm suas próprias licenças, termos e atribuições nos arquivos originais. Não atribuímos uma licença única a todos os componentes e não substituímos seus avisos por uma licença proprietária do AgoraEncontrei.

As fontes e receitas pertencem aos respectivos autores e projetos. Os documentos desta coleção descrevem a procedência e as verificações técnicas realizadas; não constituem parecer jurídico, certificação de conformidade ou garantia de reconstrução idêntica.

Referências: [FFmpeg](https://ffmpeg.org/), [informações de licenciamento do FFmpeg](https://ffmpeg.org/legal.html), [GPLv3](https://www.gnu.org/licenses/gpl-3.0.html) e as licenças originais preservadas em cada componente.
