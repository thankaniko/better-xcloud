# BX Community Final — desenvolvimento suspenso

**Estado: versão final experimental, congelada por prazo indeterminado. Sem atualizações, suporte contínuo ou garantia de compatibilidade futura.**

## Nota pública de posicionamento

Este projeto nasceu da tentativa de melhorar a experiência de jogos na nuvem em televisores LG, inclusive em dispositivos que não recebem o mesmo nível de atenção de clientes oficiais. Sua finalidade sempre foi técnica: oferecer transparência sobre a transmissão, aproveitar os recursos reais do hardware e ampliar a compatibilidade sem exigir root.

A decisão de suspender o desenvolvimento é deliberada e representa uma manifestação pacífica de discordância com as mudanças nas políticas comerciais do Xbox Cloud Gaming, especialmente a adoção de franquias de tempo de jogo em assinaturas anteriormente comercializadas com acesso ilimitado e a cobrança adicional para continuar utilizando a transmissão após o esgotamento dessa franquia, conforme as condições aplicáveis a cada conta e região.

Consideramos que a redução de um benefício central de uma assinatura, sobretudo para quem depende da nuvem, compromete a previsibilidade, a proposta de valor e a confiança do consumidor. A evolução tecnológica de um serviço deveria ampliar sua utilidade, não tornar a experiência cotidiana mais restritiva para quem já o utiliza regularmente. Reconhecemos que infraestrutura possui custos e que empresas podem rever seus modelos comerciais; isso não implica concordância com a forma como essas mudanças afetam os usuários.

Não atribuímos intenções não demonstradas à Microsoft ou à NVIDIA. Esta nota expressa uma posição sobre a política comercial, não uma acusação de ilegalidade, nem um ataque a funcionários, desenvolvedores ou usuários. Não é uma campanha de assédio, sabotagem ou evasão de cobrança. O software não contorna a franquia de horas, não cria sessões artificiais, não altera a elegibilidade de assinatura e não automatiza solicitações contra o serviço.

O código e esta versão experimental são disponibilizados no estado em que se encontram, para transparência, estudo e preservação do trabalho. Não existe compromisso de retomada, correções, atualizações de segurança ou adaptação a mudanças futuras do Xbox ou do webOS. A suspensão não é uma afirmação de que todos os objetivos técnicos foram atingidos. Se a aplicação deixar de funcionar, não há garantia de reparo. A decisão não afeta o projeto independente de catálogo de aplicativos webOS nem representa a posição dos autores originais do Better xCloud.

## O que esta versão realmente contém

- Launcher independente para o endereço oficial https://play.xbox.com/, sem proxy, NAS, root ou servidor próprio.
- Script de página limitado aos domínios Xbox de jogo, com exclusão de caminhos de autenticação conhecidos. Não coleta, exporta ou registra credenciais, cookies, tokens, cabeçalhos ou URLs de requisições. O modo HQ manipula somente o perfil de dispositivo em uma requisição existente de início de sessão; não envia dados a destinos novos.
- Perfil Maximo padrão: sem teto adicional de bitrate imposto por este aplicativo; preferência por codecs eficientes em motores Chromium modernos, apenas quando declarados pelo navegador. Pode usar Auto ou AVC, preservando os codecs anunciados. A preferência não garante negociação nem aceleração por hardware.
- Perfil Nativo: desabilita as novas preferências e modificações de requisições; o monitor local continua ativo.
- Perfil HQ legado, opcional e experimental: adapta a técnica do Better xCloud de solicitar perfil Tizen para a sessão de jogo, apenas se a requisição original já contiver os campos esperados. Não falsifica versão de navegador, dimensões ou capacidade de codec. Pode ser ignorado, reduzir qualidade ou falhar; não é o perfil mais alto garantido. Se falhar, volte ao Nativo e reinicie o jogo. Não há retry automático de criação de sessão.
- O seletor oficial do Xbox é o mecanismo para selecionar a maior resolução efetivamente oferecida. Não existe código que force uma resolução inexistente nem um bitrate do servidor acima da oferta. Não há limitador de FPS local adicional. O serviço, o painel, a rede e o decodificador são os limites reais.
- Painel de resolução RTP e HTML, FPS, bitrate, perdas, jitter, RTT, drops, codec, QP médio quando exposto, tempo médio de decodificação e QPS de chamadas fetch ao domínio de streaming conhecido. QPS não mede todas as requisições (não inclui XHR, outros hosts, workers ou WebRTC) e não é elevado artificialmente. QP é uma métrica de quantização, não um controle sobre o encoder remoto. N/D significa ausência de medição, não zero.
- Não incorpora os bundles Full/Lite experimentais anteriores: eles continham dependências da página antiga. Esta versão aproveita o diagnóstico anterior e uma técnica isolada de perfil do upstream, em vez de injetar o cliente completo sem validação.

## Compatibilidade e segurança

Alvo de desenvolvimento: televisores LG a partir de 2020 (webOS 5.x/6.x, 22, 23, 24, 25, 26 e posteriores). **Alvo não significa suporte comprovado.** A versão anterior do diagnóstico abriu e chegou ao jogo em uma TV webOS 25 segundo relato de teste; esta versão final não foi homologada fisicamente, nem nas gerações anteriores. Sintaxe conservadora, detecção de APIs e fallback não substituem testes reais. Resolução 4K/8K, AV1, HEVC, HDR, 120 FPS e bitrate arbitrário não são garantidos; não há upscaling ou encoder próprio. A Microsoft documenta streaming de até 1440p em dispositivos/títulos/regiões elegíveis; selecione a maior opção realmente oferecida. Se o painel não observar a conexão, algumas métricas ficam N/D. O código não inspeciona frames de outros contextos ou workers. A página pode alterar a estrutura ou restringir a injeção. A ausência de atualizações futuras implica risco de incompatibilidade e de segurança; prefira o cliente oficial para uso regular.

Instalação: Developer Mode + webOS Dev Manager, instalar o IPK; ID independente para preservar o Probe 0.2.0. Abra Xbox Cloud Gaming no launcher. Acesse a qualidade oficial mais alta. Para mudar o perfil/codec, use o painel e reinicie a sessão de jogo. F8 com teclado oculta/mostra o painel; fechar e reabrir o app também restaura sua visibilidade. O controle do jogo permanece com a página. Se houver falha, use Nativo + Auto, ou remova este IPK e utilize o cliente oficial. Não introduza credenciais se o endereço da página de login não for o oficial da Microsoft.

## Referências e atribuição

Projeto independente, não afiliado à Microsoft, Xbox, LG ou aos mantenedores originais. Better xCloud (redphx), licença MIT: https://github.com/redphx/better-xcloud. Técnica de perfil adaptada do build fornecido; a licença e atribuições originais estão em LICENSE. Documentação do upstream: https://better-xcloud.github.io/features/ e https://better-xcloud.github.io/faq/. Especificação WebRTC: https://www.w3.org/TR/webrtc/. Motores LG: https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine. Mecanismo de userscripts: https://www.webosbrew.org/pages/web-development/#userscripts-in-apps. Anúncio da Microsoft sobre qualidade: https://news.xbox.com/pt-br/2026/02/25/atualizacao-de-fevereiro-do-xbox-streaming-em-1440p-nos-consoles-xbox-atualizacoes-do-rog-xbox-ally-e-mais/.

## Reprodução

Execute `python3 build.py` no diretório do código-fonte (Python 3 e `ar`). Valide com `node --check app/probe.js`, `node --check app/webOSUserScripts/userScript.js` e `node tests/mock.js`. Os testes simulados não substituem um stream real.

## Integridade dos arquivos finais

- IPK: `org.webos.community.bxfinal_1.0.0_all.ipk` — SHA-256 `414a24412dba77639932691c3b6f616657b912bccd612cc4b9f73c46002aac36`.
- Código-fonte: `bx-community-final-source.zip` — SHA-256 `3aa1412ab473e4dc6e6308f7e57ec86ecd3963515797003e2699024777a0c2ab`.
- Empacotamento, sintaxe Node.js e testes simulados de escopo, codec e fallback aprovados. Instalação e streaming reais da versão final não homologados.
- Arquivos finais preservados no diretório [`final/`](final/): [IPK](final/org.webos.community.bxfinal_1.0.0_all.ipk) e [código-fonte, build e testes](final/bx-community-final-source.zip). Não é uma release estável nem um pacote do catálogo principal.

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
