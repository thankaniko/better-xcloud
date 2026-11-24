# BX Community Final — desenvolvimento suspenso por tempo indeterminado

**Idiomas / Languages / Idiomas / 语言:** [Português (Brasil)](README.md) · [English](README.en.md) · [Español](README.es.md) · [简体中文](README.zh-CN.md)

> [!IMPORTANT]
> **Comunicado oficial do projeto · 24 de novembro de 2026.** Versão final experimental 1.0.0. O desenvolvimento encontra-se suspenso por tempo indeterminado. Não estão previstas atualizações, correções de segurança, suporte técnico ou garantias de compatibilidade futura. Esta não é uma versão estável.

## 1. Posicionamento público e fundamentação

Esta iniciativa independente foi concebida para aprimorar a experiência de jogos em nuvem em televisores LG, inclusive em dispositivos sem suporte oficial. Sua finalidade sempre foi técnica: proporcionar transparência mensurável sobre a transmissão, aproveitar os recursos disponíveis no hardware e investigar a ampliação da compatibilidade sem exigir acesso root.

A suspensão do desenvolvimento constitui uma decisão deliberada e uma manifestação pacífica de protesto contra as alterações nas políticas comerciais do Xbox Cloud Gaming. No [comunicado de 3 de setembro de 2026](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/), a Xbox anunciou a introdução de franquias mensais de tempo de jogo em assinaturas Game Pass anteriormente disponibilizadas sem esses limites mensais, bem como a possibilidade de adquirir tempo adicional de transmissão. A empresa apresentou como justificativas os custos operacionais, a confiabilidade do serviço e a continuidade dos investimentos. As condições efetivamente aplicáveis podem variar conforme a conta e o mercado.

Nossa objeção concentra-se na redução de um benefício central da assinatura, sobretudo para usuários que dependem da nuvem. Reconhecemos os custos de infraestrutura e a necessidade de modelos comerciais sustentáveis. Entretanto, em nossa avaliação, restringir um benefício anteriormente ilimitado e exigir pagamento adicional para continuar utilizando-o compromete a previsibilidade, a confiança do consumidor e a proposta de valor da assinatura. Defendemos condições transparentes, comunicação prévia adequada e tratamento proporcional aos usuários que dependem do serviço.

Este posicionamento expressa uma discordância fundamentada com a política comercial adotada. Não constitui declaração de ilegalidade, imputação de intenções não demonstradas ou ataque a funcionários, desenvolvedores e usuários. Não afirmamos que a Microsoft tenha copiado outro fornecedor. O projeto não busca contornar franquias, pagamentos ou critérios de elegibilidade, gerar tráfego abusivo ou sabotar o serviço. Não incentivamos assédio nem acesso não autorizado.

O código-fonte e o pacote final experimental permanecem disponíveis para fins de preservação, estudo e consulta técnica. A preservação do trabalho não implica manutenção ativa nem a conclusão integral dos objetivos de engenharia originalmente estabelecidos. Não existe data ou condição que garanta a retomada. Esta decisão restringe-se a esta adaptação independente, não representa os autores originais do Better xCloud e não afeta o projeto separado webOS Mega Repository.

## 2. Pacote final

[IPK](final/org.webos.community.bxfinal_1.0.0_all.ipk) · [Código-fonte ZIP](final/bx-community-final-source.zip)

| Item | Estado |
| --- | --- |
| Versão | 1.0.0 — experimental |
| Instalação | Developer Mode do webOS; sem root |
| Rede | Site oficial Xbox; sem proxy, NAS ou servidor próprio do projeto |
| Público-alvo | TVs LG a partir de 2020; não constitui lista de compatibilidade homologada |
| Validação | Estrutura do pacote, sintaxe JavaScript e testes simulados; streaming final em hardware não verificado |
| Manutenção | Suspensa por tempo indeterminado |

## 3. Comportamento técnico

O launcher independente abre https://play.xbox.com/. Seu userscript foi projetado para restringir a execução às origens oficiais do Xbox, excluindo rotas de autenticação. Não realiza intencionalmente coleta, exportação ou registro de credenciais, cookies, tokens, cabeçalhos de requisições ou URLs. Não existe backend de telemetria próprio. Esta é uma descrição da implementação, não uma certificação independente de segurança; os serviços da Microsoft mantêm suas práticas habituais de tratamento de dados.

| Perfil | Comportamento e limitações |
| --- | --- |
| Máximo (padrão) | Não impõe limites locais adicionais de bitrate ou FPS. Prioriza codecs eficientes em motores Chromium modernos quando anunciados pelo navegador; permite selecionar Auto ou AVC. Não garante negociação nem aceleração por hardware. |
| Nativo | Desativa preferências de codecs e modificações de requisições, mantendo o monitoramento local. |
| HQ Legacy (experimental) | Adapta a técnica upstream de perfil Tizen exclusivamente quando a requisição de sessão existente contém os campos necessários. Não altera versão do navegador, dimensões ou capacidades de codec. Não redireciona dados a destinos externos. Pode degradar ou interromper a transmissão; retorne ao modo Nativo + Auto e reinicie manualmente a sessão. Não há garantia de recuperação automática. |

Utilize o seletor nativo do Xbox para solicitar a maior resolução disponibilizada. Não há mecanismo para forçar resoluções inexistentes, superar os limites de bitrate do servidor ou contornar critérios de acesso. Não são garantidos 4K/8K, HDR, AV1, HEVC, 120 FPS ou bitrates arbitrários; não existe encoder próprio nem upscaling. A Xbox documenta streaming de até 1440p em cenários elegíveis. A qualidade efetiva depende do serviço, painel, decodificador e rede.

O painel local apresenta resolução RTP/HTML, FPS, bitrate, perda de pacotes, jitter, RTT, quadros descartados, codec, QP médio, tempo de decodificação e QPS. O QP mede quantização, não controla o encoder remoto. O QPS contabiliza somente as requisições fetch observadas à origem de streaming, excluindo XHR, outros hosts, workers e tráfego WebRTC; não é artificialmente ampliado. N/D indica medição indisponível, não valor zero. Frames e workers externos não são inspecionados. Os bundles Full/Lite anteriores não foram incorporados; somente a técnica isolada de perfil upstream foi adaptada.

## 4. Compatibilidade, instalação e segurança

O alvo de desenvolvimento abrange webOS 5.x (2020), 6.x (2021), 22, 23, 24, 25, 26 e posteriores. Sintaxe conservadora, detecção de APIs e mecanismos de fallback não comprovam compatibilidade. O IPK final não foi homologado fisicamente em nenhuma dessas gerações. Alterações no motor do navegador, na autenticação, na estrutura do site ou nas políticas do serviço podem inviabilizar seu funcionamento.

1. Instale o IPK pelo Developer Mode e webOS Dev Manager. O ID independente preserva o Probe 0.2.0.
2. Abra o launcher, selecione a maior qualidade nativa disponibilizada pelo Xbox e inicie uma sessão.
3. Altere o perfil ou codec pelo painel e reinicie a sessão de jogo. O atalho F8, em teclado, alterna a visibilidade do painel; reiniciar o aplicativo restaura a interface. O controle permanece vinculado à página.
4. Em caso de falha, selecione Nativo + Auto e reinicie, ou desinstale o pacote e utilize o cliente oficial. Não insira credenciais se a origem real da página de login não corresponder a um domínio oficial de autenticação da Microsoft; em caso de dúvida, interrompa a operação.

Não estão previstas atualizações, inclusive diante de problemas de segurança ou compatibilidade. Recomenda-se o cliente oficial para utilização regular. Validações estáticas e testes simulados não substituem homologação empírica nem revisão de segurança. O software é disponibilizado no estado em que se encontra, nos termos da licença MIT.

## 5. Reprodução e integridade

Extraia o ZIP de código-fonte e execute os seguintes comandos a partir de sua raiz (requer Python 3, `ar` e Node.js):

```sh
python3 build.py
node --check app/probe.js
node --check app/webOSUserScripts/userScript.js
node tests/mock.js
```

Durante o empacotamento foram validados a estrutura do pacote, a sintaxe JavaScript e os testes simulados de escopo, codecs e fallback. Isso não comprova funcionamento em hardware real. Confira o SHA-256 dos arquivos distribuídos sem alterações:

| Arquivo | SHA-256 |
| --- | --- |
| `org.webos.community.bxfinal_1.0.0_all.ipk` | `414a24412dba77639932691c3b6f616657b912bccd612cc4b9f73c46002aac36` |
| `bx-community-final-source.zip` | `3aa1412ab473e4dc6e6308f7e57ec86ecd3963515797003e2699024777a0c2ab` |

Os arquivos em [final/](final/) são artefatos de preservação, não uma GitHub Release estável nem um pacote do catálogo principal do webOS Mega Repository. Esta revisão documental não modifica o binário ou o ZIP de código-fonte arquivados.

## 6. Referências e atribuição

Projeto independente e não oficial, sem vínculo com Microsoft, Xbox, LG ou os mantenedores originais. Baseado no Better xCloud de redphx, sob licença MIT; os avisos e créditos originais são preservados. As marcas pertencem aos respectivos titulares. O README upstream foi preservado separadamente para evitar confusão entre suas instruções de suporte e doações e esta adaptação suspensa.

- [Xbox Wire — anúncio das alterações de política comercial (03/09/2026)](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/)
- [Xbox Wire — streaming em 1440p](https://news.xbox.com/pt-br/2026/02/25/atualizacao-de-fevereiro-do-xbox-streaming-em-1440p-nos-consoles-xbox-atualizacoes-do-rog-xbox-ally-e-mais/)
- [Better xCloud](https://github.com/redphx/better-xcloud) · [Recursos](https://better-xcloud.github.io/features/) · [FAQ](https://better-xcloud.github.io/faq/)
- [LG webOS — APIs web e motor de navegador](https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine)
- [webOS Brew — userscripts](https://www.webosbrew.org/pages/web-development/#userscripts-in-apps)
- [W3C — especificação WebRTC](https://www.w3.org/TR/webrtc/)
- [Licença MIT](LICENSE) · [README original upstream](docs/UPSTREAM-README.md)

**Estado definitivo: desenvolvimento suspenso por tempo indeterminado.** Não existe compromisso de retomada, correção ou atualização.
