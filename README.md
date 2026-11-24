# BX Community Final — desenvolvimento suspenso

**Status: versão final experimental, com desenvolvimento interrompido por tempo indeterminado. Sem atualizações, suporte técnico ou garantia de compatibilidade futura.**

## Comunicado oficial

Este projeto foi concebido com o objetivo de otimizar a experiência de jogos em nuvem em televisores LG, abrangendo dispositivos que não possuem suporte oficial. A iniciativa teve caráter estritamente técnico, visando à transparência na transmissão, ao aproveitamento do hardware e à ampliação da compatibilidade sem a necessidade de acesso root.

A suspensão do desenvolvimento é uma decisão deliberada, motivada por divergências em relação às alterações nas políticas comerciais do Xbox Cloud Gaming — especificamente a implementação de limites de tempo em assinaturas anteriormente ofertadas como ilimitadas, bem como a cobrança adicional após o consumo da franquia, conforme as diretrizes regionais.

Entendemos que a redução de benefícios centrais impacta negativamente a previsibilidade, a proposta de valor e a confiança do consumidor. A evolução de um serviço deve priorizar a utilidade e a experiência do usuário. Embora reconheçamos os custos de infraestrutura e a necessidade de revisão de modelos de negócio por parte das empresas, não concordamos com a forma como tais mudanças restringem o acesso dos usuários.

Este posicionamento reflete uma discordância estratégica e não constitui qualquer acusação de ilegalidade ou ataque a indivíduos. Não se trata de uma campanha de sabotagem ou evasão de taxas; o software não contorna limitações de franquia, não altera a elegibilidade da assinatura e não automatiza requisições.

O código e esta versão experimental permanecem disponíveis para fins de transparência e consulta técnica. Não há previsão de retomada, manutenções ou adaptações futuras. A interrupção não implica que os objetivos técnicos tenham sido plenamente alcançados; portanto, a funcionalidade da aplicação não é garantida caso ocorram alterações no serviço. Esta decisão é independente e não representa os autores originais do Better xCloud ou o catálogo de aplicativos do webOS.

## Especificações da versão

- Launcher independente voltado ao endereço oficial https://play.xbox.com/, operando sem proxy, NAS, root ou servidores proprietários.
- Script limitado aos domínios oficiais do Xbox, com exclusão de rotas de autenticação. Não há coleta, exportação ou registro de credenciais, cookies, tokens, cabeçalhos ou URLs.

O modo HQ realiza a manipulação exclusiva do perfil de dispositivo em requisições de sessão vigentes, sem o redirecionamento de dados para destinos externos.
- Perfil Máximo padrão: sem restrições adicionais de bitrate aplicadas por esta solução; priorização de codecs eficientes em motores Chromium modernos, condicional à declaração do navegador. Suporta Auto ou AVC, mantendo os codecs anunciados, sem garantia de negociação ou aceleração via hardware.
- Perfil Nativo: desativa preferências e modificações em requisições, mantendo o monitor local em operação.
- Perfil HQ legado (experimental): aplica a metodologia do Better xCloud de requisição de perfil Tizen, desde que a solicitação original contenha os campos necessários. Não há alteração de versão do navegador, dimensões ou capacidade de codec. O recurso pode resultar em degradação ou falha, não sendo um perfil de alta performance garantido; em caso de insucesso, recomenda-se retornar ao modo Nativo e reiniciar a sessão, visto que não há tentativa automática de recuperação.
- O seletor nativo do Xbox é o mecanismo para a definição da maior resolução ofertada. Não há implementação para forçar resoluções inexistentes ou alterar bitrates do servidor além do limite oferecido, tampouco limitadores locais de FPS. O desempenho é condicionado pelo serviço, painel, infraestrutura de rede e decodificador.
- O painel exibe dados de resolução RTP/HTML, FPS, bitrate, perdas, jitter, RTT, drops, codec, QP médio, tempo de decodificação e QPS de requisições fetch ao domínio de streaming. O QPS não mensura a totalidade de requisições (excluindo XHR, hosts terceiros, workers ou WebRTC) e não sofre incremento artificial. O QP representa métrica de quantização e não controle do encoder remoto. N/D indica ausência de medição.
- Esta versão não contempla bundles Full/Lite anteriores, eliminando dependências obsoletas e adotando uma técnica isolada de perfil de upstream, sem injeção de cliente sem validação.

## Compatibilidade e segurança

Foco de desenvolvimento: televisores LG a partir de 2020 (webOS 5.x/6.x, 22, 23, 24, 25, 26 e posteriores). O alvo não assegura suporte homologado. Esta versão final não passou por validação física em gerações anteriores ou atuais. O uso de sintaxe conservadora, detecção de APIs e mecanismos de fallback não substituem testes empíricos. Resolução 4K/8K, AV1, HEVC, HDR, 120 FPS e bitrates arbitrários não são garantidos, inexistindo upscaling ou encoder próprio. A Microsoft documenta streaming de até 1440p em cenários elegíveis; recomenda-se selecionar a maior opção disponível. Caso o painel não detecte a conexão, certas métricas constarão como N/D. O código não inspeciona frames de contextos ou workers externos. Alterações na estrutura da página podem restringir a injeção. A ausência de atualizações implica riscos de compatibilidade e segurança, sendo recomendada a utilização do cliente oficial para operações regulares.

Instalação: Utilize o Developer Mode e o webOS Dev Manager para realizar a instalação do arquivo IPK; recomenda-se a utilização de um ID independente para assegurar a integridade da versão Probe 0.2.0. Inicie o Xbox Cloud Gaming via launcher e selecione a qualidade de transmissão oficial máxima disponível. Ajustes de perfil ou codec devem ser realizados no painel específico, seguidos pela reinicialização da sessão de jogo. O atalho F8 (teclado) alterna a visibilidade do painel; a reinicialização do aplicativo também restaura a interface. O controle permanece vinculado à página. Em caso de falha na execução, alterne para o modo Nativo + Auto ou desinstale o pacote, revertendo para o cliente oficial. Por medida de segurança, não insira credenciais caso o domínio da página de login não corresponda ao oficial da Microsoft.

## Referências e atribuição

Projeto independente, sem vínculo com a Microsoft, Xbox, LG ou mantenedores originais. Baseado no Better xCloud (redphx), sob licença MIT: https://github.com/redphx/better-xcloud. Técnica de perfil adaptada do build fornecido; licenças e atribuições originais constam em LICENSE. Documentação upstream: https://better-xcloud.github.io/features/ e https://better-xcloud.github.io/faq/. Especificação WebRTC: https://www.w3.org/TR/webrtc/. Motores LG: https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine. Mecanismo de userscripts: https://www.webosbrew.org/pages/web-development/#userscripts-in-apps. Comunicado oficial Microsoft sobre qualidade: https://news.xbox.com/pt-br/2026/02/25/atualizacao-de-fevereiro-do-xbox-streaming-em-1440p-nos-consoles-xbox-atualizacoes-do-rog-xbox-ally-e-mais/.

## Reprodução

Execute o comando `python3 build.py` no diretório de origem (requer Python 3 e `ar`). Valide a conformidade com `node --check app/probe.js`, `node --check app/webOSUserScripts/userScript.js` e `node tests/mock.js`. Ressalta-se que os testes simulados não substituem a validação via stream real.

## Integridade dos arquivos finais

- IPK: `org.webos.community.bxfinal_1.0.0_all.ipk` — SHA-256 `414a24412dba77639932691c3b6f616657b912bccd612cc4b9f73c46002aac36`.
- Código-fonte: `bx-community-final-source.zip` — SHA-256 `3aa1412ab473e4dc6e6308f7e57ec86ecd3963515797003e2699024777a0c2ab`.
- Empacotamento, sintaxe Node.js e testes de escopo, codec e fallback validados. Instalação e streaming da versão final não homologados.
- Arquivos disponíveis no diretório [`final/`](final/): [IPK](final/org.webos.community.bxfinal_1.0.0_all.ipk) e [código-fonte, build e testes](final/bx-community-final-source.zip). Este artefato não compõe uma release estável nem faz parte do catálogo oficial.

---

## README original do projeto upstream (preservado para atribuição)

<div align="center">
    <img src="https://raw.githubusercontent.com/redphx/better-xcloud/refs/heads/typescript/resources/logos/better-xcloud.png" width="256"/>  
    <h1>Better xCloud</h1>
    <!-- Latest Version Badge -->
    <a href="https://github.com/redphx/better-xcloud/releases"><img src="https://img.shields.io/github/v/release/redphx/better-xcloud?label=latest" alt="Latest version" /></a>
    <!-- Total Downloads Badge -->
    <a href="https://github.com/redphx/better-xcloud/releases"><img src="https://img.shields.io/github/downloads/redphx/better-xcloud/total?color=%23e15f2c" alt="Total downloads" /></a>
    <!-- Total Stars Badge -->
    <a href="https://github.com/redphx/better-xcloud/stargazers"><img src="https://img.shields.io/github/stars/redphx/better-xcloud?color=%23cca400" alt="Total stars" /></a>
</div>

### Improve Xbox Cloud Gaming (xCloud) experience on [xbox.com/play](https://www.xbox.com/play). It also allows you to use Remote Play on the xCloud website.  

> [!WARNING]
> I only provide Better xCloud on the official repos. Don't download it from anywhere else  
> Fake websites:
>   - betterxcloud.net

> [!IMPORTANT]  
> I only accept pull requests for:
> - Custom touch controls
> - Bug fixes

**Supported platforms:**  
- Windows
- macOS
- Linux, SteamOS (including Steam Deck)
- Android, Android TV (including Meta Quest VR Headsets): [redphx/better-xcloud-android](https://github.com/redphx/better-xcloud-android)
- iOS, iPadOS

This script makes me spend more time with xCloud, and I hope the same thing happens to you.  
If you like this project please give it a 🌟. Thank you 🙏.

## How to install
Visit the [home page](https://better-xcloud.github.io) to know how to install Better xCloud on your device.

## Full documentations
- For the full details please visit: [**better-xcloud.github.io**](https://better-xcloud.github.io)  
- [Demo video](https://youtu.be/hyp69Jrb2sQ)

⚠️ Please DO NOT report **Better xCloud**'s bugs on [/r/xcloud subreddit](https://reddit.com/r/xcloud/). Report bugs in [Issues](https://github.com/redphx/better-xcloud/issues) or [Telegram channel](https://t.me/betterxcloud) instead.

## Donation
If you think this project is useful and want to support future developments, please consider making a donate via [my Ko-fi page](https://ko-fi.com/redphx).  
Or you can give this project a star, that's also helpful.  
Thank you.  

## Translation  
Help translating **Better xCloud** to another languagues using [Crowdin](https://crowdin.com/project/better-xcloud).  
Use [this post](https://github.com/redphx/better-xcloud/discussions/131) for discussion. 

## Acknowledgements  
- The mouse controlling feature is heavily inspired by the "Mouse spinning" feature in [Yuzu emulator](https://github.com/yuzu-emu/yuzu-mainline)
- [n-thumann/xbox-cloud-server-selector](https://github.com/n-thumann/xbox-cloud-server-selector) for the idea of IPv6 feature
- Icons by [Phosphor Icons](https://phosphoricons.com)
- [PromptFont](https://shinmera.com/promptfont) by Yukari "Shinmera" Hafner

## Disclaimers  
- Use it at your own risk.
- This project is not affiliated with Xbox in any way. All Xbox logos/icons/trademarks are copyright of their respective owners.
