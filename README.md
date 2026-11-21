# rtexjp â€” motor de reels ilustrados 9:16

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![rtexjp](capa/capa.png)](https://inematds.github.io/rtexjp/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O rtexjp Ã© um motor que monta vÃ­deos curtos verticais (reels) ilustrados, em azul-marinho, a partir de um roteiro escrito num arquivo de texto (`roteiro.json`). Ã‰ o motor que o Nei usa nos reels do INEMA, aberto para quem quiser estudar ou adaptar: sem gravar a si mesmo e sem pagar serviÃ§o de avatar. Ele gera a voz, desenha cada cena quadro a quadro, mistura a trilha e confere sozinho se o vÃ­deo segue o formato. Precisa de um computador com placa de vÃ­deo (GPU), Python, Node, ffmpeg e dois servidores locais: o de voz ([inemavox](https://github.com/inematds/inemavox)) e o de imagem ([inemaimg](https://github.com/inematds/inemaimg), flux2-klein).

Vem configurado com a voz e o avatar do Nei. Para usar os seus, aponte as variÃ¡veis de ambiente `RTEXJP_VOZ_REF` (gravaÃ§Ã£o de referÃªncia da voz, `.wav`) e `RTEXJP_AVATAR_REF` (foto do avatar) para os seus arquivos, descreva o seu personagem em `RTEXJP_AVATAR_DESC` e gere as poses de novo (`python3 motor/gerar_avatar.py`); esses dois arquivos nÃ£o vÃªm no repositÃ³rio. Veja **Caminhos e variÃ¡veis de ambiente** abaixo.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/rtexjp/guia/** Â· 1Âº vÃ­deo (paleta antiga, roxa): https://www.youtube.com/watch?v=AZEZK1YgF98

**v1.3.0** (05/11/2026: `/rtexjp` no inemaccbot + produÃ§Ã£o sem sessÃ£o) Â· motor local e grÃ¡tis que transforma um `roteiro.json` num reel vertical 1080Ã—1920 no **padrÃ£o rtexjp**: um reel ilustrado em azul-marinho (com trocas para um papel azul-gelo), avatar ilustrado do Nei **grande** (â‰ˆ 43 % da altura, em 11 poses ligadas Ã  emoÃ§Ã£o da fala, sem lip-sync), um **desenho-herÃ³i** por cena, **print real** como prova, manchete Sora centrada, legenda karaokÃª, mascote robÃ´ e um Ãºnico CTA de **opiniÃ£o** (uma pergunta com lado, respondida com uma palavra: "comenta DONO ou REFÃ‰M").

## O formato (padrÃ£o rtexjp)

Esqueleto fixo, conferido pelo validador (`checar`) e pelo QA (`qa`):

1. **Gancho no quadro 0** (`gancho.tipo` no roteiro), um destes: **contrÃ¡rio** (manda parar algo que todo mundo faz), **perda** (e se X sumisse?), **estatÃ­stica de medo** com fonte na tela, ou **histÃ³ria de terceiro** com nÃºmero. Proibido: lista ("5 coisasâ€¦"), "vocÃª sabia queâ€¦", "eu fizâ€¦".
2. **Manchete do quadro 0** com no mÃ¡ximo ~6 palavras, caixa alta, **uma** palavra em amarelo, mais agressiva que a fala (o texto puxa quem rola sem som, a voz suaviza). JÃ¡ estÃ¡ pronta no quadro 0, que serve de capa. Um **objeto-metÃ¡fora com dano** desenhado (riscado de vermelho, sumindo, quebrado), o avatar **reage** no 1Âº segundo e algo muda a cada ~1 s nos 3 primeiros segundos.
3. **Prova atÃ© 20 s** â€” nÃºmero com fonte (contador que pousa no nÃºmero, linha de fonte em monoespaÃ§ada embaixo) ou autoridade.
4. **O problema de quem assiste, com absolviÃ§Ã£o** ("nÃ£o Ã© culpa sua, ninguÃ©m te deu X") â€” e aqui a **tensÃ£o da isca** Ã© plantada: as opÃ§Ãµes da pergunta final aparecem na tela, em amarelo.
5. **Um tema por vÃ­deo**; o mÃ©todo em 2â€“5 **peÃ§as** anunciadas com Ã­ndice visÃ­vel e barra de pÃ­lulas no topo durante as peÃ§as.
6. **Uma peÃ§a por vez, um objeto visual por frase** â€” o objeto muda dentro da cena a cada ~2â€“3 s.
7. **Ressalva honesta falada**, em cartÃ£o de alerta (vermelho = problema, verde = certo).
8. **MÃ¡xima em antÃ­tese**, depois de **0,8 s de silÃªncio real** (voz e cama param).
9. **CTA de opiniÃ£o**: pergunta forte, emocional e com lado, ligada Ã  tese; o Nei diz o lado dele antes ("eu quero ser dono do meu") e pede a resposta em uma palavra ("comenta DONO ou REFÃ‰M"). O cartÃ£o mostra a pergunta + as opÃ§Ãµes, a caixa de comentÃ¡rio digita uma opÃ§Ã£o â†’ Publicar â†’ confirmaÃ§Ã£o, segurado ~10 s, sem despedida. **Proibido prometer entrega** ("te mando", "eu envio", "comenta X queâ€¦"): o Nei nÃ£o responde comentÃ¡rios. Link e fonte ficam parados no comentÃ¡rio fixado/descriÃ§Ã£o (bloco `publicar` do roteiro), nunca como recompensa por comentar.

Visual (v1.2, ediÃ§Ãµes com `"versao": "rtexjp/3"`): cada quadro tem a mesma casca, de cima para baixo â€” rÃ³tulo em mono (â‰¥ 30 px) Â· **manchete em Sora ExtraBold, centrada, 2â€“3 linhas, â‰¥ 96 px**, branco `#f4f7fc` com uma palavra em azul-aÃ§o claro `#93c5fd` (amarela `#FACC15` sÃ³ no quadro 0) Â· **desenho-herÃ³i** (objeto ilustrado no mesmo estilo flat do avatar, da biblioteca `motor/assets/objetos/`, ou o **print real** da pÃ¡gina da fonte com a linha `fonte:` embaixo) Â· **legenda karaokÃª** (Montserrat ExtraBold 74 px com contorno preto, a palavra dita em azul-aÃ§o) numa faixa prÃ³pria Â· **avatar grande**, embaixo e centralizado (820 px, â‰ˆ 43 % da altura), na pose do bloco ou da batida. O fundo tem holofote e grÃ£o leve e alterna entre marinho `#07111f` e papel azul-gelo `#e8eef7` (`cena.tema: "claro"`, letras marinho, destaque em faixa `#1e3a8a`). No silÃªncio antes da mÃ¡xima o Ãºltimo quadro fica congelado com o avatar pensativo: nunca tela vazia. Amarelo sÃ³ na palavra quente do quadro 0 e na pergunta/opÃ§Ãµes da isca (letra `#1a1206` no preenchimento); verde/vermelho sÃ³ certo/errado. Zonas seguras do Reels: rosto, texto e objetos acima de 80 % da altura (abaixo dali sÃ³ o tronco do avatar).

**PortÃ£o de beleza** (`medir.py`, sÃ³ em `rtexjp/3`): o palco mede no prÃ³prio DOM, em 2 amostras por bloco, a manchete (â‰¥ 96 px), todo texto (â‰¥ 30 px), a Ã¡rea ocupada no quadro Ãºtil (â‰¥ 55 %), o contraste do texto (WCAG â‰¥ 4,5:1) e a altura do avatar (â‰¥ 38 %).

EdiÃ§Ãµes antigas (`rtexjp/2`) continuam com o visual da v1.1 (Anton Ã  esquerda, avatar pequeno no canto).

Ãudio: voz do Nei (inemavox chatterbox, 0,6/0,6, `atempo` â‰¤ 1,15, pausas internas encurtadas), 160â€“190 palavras/min, cama musical baixa com sidechain, master âˆ’14 LUFS.

> **ExceÃ§Ã£o ao kit INEMA:** avatar ilustrado e mascote robÃ´ sÃ£o decisÃ£o de projeto (registrada em `inema-design/DECISOES.md`, D19). A paleta segue o kit em espÃ­rito: marinho + azul, amarelo `#FACC15` como Ãºnica cor quente. A 1Âª ediÃ§Ã£o (`2026-10-28-5-coisas`) Ã© do formato antigo â€” paleta roxa, gancho de lista e isca com entregÃ¡vel â€” e fica como estÃ¡, porque jÃ¡ foi publicada.

## Caminhos e variÃ¡veis de ambiente

| VariÃ¡vel | Para quÃª | PadrÃ£o |
|---|---|---|
| `RTEXJP_INEMAVOX` | pasta do inemavox (TTS chatterbox no `venv` + Whisper large-v3) | `~/projetos/inemavox` |
| `RTEXJP_VOZ_REF` | gravaÃ§Ã£o de referÃªncia da voz (`.wav`) | `~/projetos/timesmkt3/media/voice-refs/nei.wav` |
| `RTEXJP_IMG_URL` | servidor de imagem flux2-klein (`motor/gerar_avatar.py`, `motor/gerar_imagem.py`) | `http://localhost:8000/generate` |
| `RTEXJP_AVATAR_REF` | foto de referÃªncia do avatar | `~/projetos/inema-referencias/nei-avatar.jpg` |
| `RTEXJP_AVATAR_DESC` | traÃ§os e roupa do personagem no pedido de imagem (em inglÃªs); troque junto com a foto | bonÃ© preto, Ã³culos, barba grisalha, camiseta azul-aÃ§o (o Nei) |
| `RTEXJP_TRILHA` | cama musical do mix (para publicar, use uma mÃºsica cuja licenÃ§a vocÃª conheÃ§a) | `motor/assets/trilha.mp3` |
| `CS_WHISPER_PY` | Python do ambiente com faster-whisper (servidor do Whisper e plano B) | `~/miniconda3/envs/chatterbox/bin/python3` |
| `CHATTERBOX_PYTHON` | Python do ambiente do chatterbox, exigido pelo `tts_direct.py` do inemavox | o do ambiente `chatterbox` |

Exemplo: `RTEXJP_VOZ_REF=~/minha-voz.wav RTEXJP_INEMAVOX=~/inemavox python3 rtexjp.py voz edicoes/minha-edicao`.

## Estrutura

```
rtexjp.py              pipeline: checar Â· voz Â· cena Â· render Â· mix Â· qa Â· tudo
medir.py               QA automÃ¡tico (duraÃ§Ã£o, wpm, LUFS, trocas/min, isca, cartÃ£o final, silÃªncio, grep de fonte) + contact.jpg
motor/palco.html       o palco: casca v1.2 (manchete, herÃ³i, avatar, legenda) desenhada por window.render(t) + window.medidas(t) (portÃ£o de beleza)
motor/render.mjs       Playwright quadro a quadro -> ffmpeg (30 fps)
motor/gerar_avatar.py  poses do avatar no flux2-klein local com a foto de referÃªncia (fundo verde recortado)
motor/capturar_prova.mjs print real da fonte para a prova (Playwright, tema escuro, 2x)
motor/gerar_objeto.py  desenho-herÃ³i no flux2-klein local -> motor/assets/objetos/<nome>.png + indice.json
motor/gerar_imagem.py  imagem de cena no flux2-klein local
motor/whisper.py       Whisper large-v3 local (inemavox) com tempo por palavra
motor/avatar/*.png     11 poses: bracos, queixo, apontando, segurando, surpreso, mostrando, explica, olha, polegar, duvida, susto
motor/assets/objetos/  biblioteca de desenhos-herÃ³i (terminal_quebrado, mapa_pinos, lupa_arquivos, dominos, chave_donoâ€¦) + indice.json
motor/assets/          trilha.mp3 (cama), grao.png (textura), carro.png
motor/fontes/          Sora, Anton, JetBrains Mono, Montserrat (OFL)
edicoes/<id>/          roteiro.json Â· final.mp4 Â· contact.jpg Â· qa.md Â· prova/ (prints reais) (voz/ e build/ ficam fora do git)
```

## O processo, do inÃ­cio ao fim

ðŸ§  sessÃ£o com o Nei Â· âš™ï¸ script (zero token) Â· ðŸ¤– `claude -p` / Codex pela assinatura (nunca API)

| # | Passo | Comando | Quem |
|---|---|---|---|
| 1 | Pauta: tese, 2â€“5 peÃ§as, nÃºmeros conferidos (âœ… com fonte e data) | â€” | ðŸ§  |
| 2 | Roteiro: escrever `edicoes/<id>/roteiro.json` (`gancho`, `isca` de opiniÃ£o, fala por extenso, `fala_tts` para pronÃºncia, gatilhos por palavra, bloco `publicar`) | editar o JSON (ou ðŸ¤– a partir da pauta) | ðŸ¤– + ðŸ§  |
| 3 | Validar regras do formato | `python3 rtexjp.py checar edicoes/<id>` | âš™ï¸ |
| 4 | Aprovar o roteiro (gancho, pergunta da isca, nÃºmeros) | â€” | ðŸ§  |
| 5 | Poses do avatar (uma vez; refazer sÃ³ se mudar o personagem) â€” olhar cada uma e refazer as deformadas | `python3 motor/gerar_avatar.py [pose â€¦]` | âš™ï¸ |
| 6 | Desenho-herÃ³i que faltar na biblioteca (olhar e refazer com outra seed se sair torto) | `python3 motor/gerar_objeto.py <nome> "<objeto em inglÃªs>" [seed]` | âš™ï¸ |
| 6b | Print real da fonte (pÃ¡gina do repositÃ³rio, recortada no nome e no contador) em `edicoes/<id>/prova/` | `node motor/capturar_prova.mjs <url> edicoes/<id>/prova/x.png [--clip x,y,w,h]` | âš™ï¸ |
| 7 | Voz por bloco + Whisper (tempo por palavra) | `python3 rtexjp.py voz edicoes/<id> [bloco â€¦]` (com nomes, refaz sÃ³ esses TTS) | âš™ï¸ |
| 8 | Cena (roteiro + tempos) | `python3 rtexjp.py cena edicoes/<id>` | âš™ï¸ |
| 9 | PrÃ©via de quadros (+ `quadros/medidas.json` do portÃ£o de beleza) | `node motor/render.mjs edicoes/<id>/build --quadros 0,10,20` â†’ `edicoes/<id>/quadros/` | âš™ï¸ |
| 10 | Render 1080Ã—1920 30 fps | `python3 rtexjp.py render edicoes/<id>` | âš™ï¸ |
| 11 | Mixagem (cama para no silÃªncio da mÃ¡xima, âˆ’14 LUFS) | `python3 rtexjp.py mix edicoes/<id>` | âš™ï¸ |
| 12 | QA automÃ¡tico + portÃ£o de beleza + contact sheet | `python3 rtexjp.py qa edicoes/<id>` â†’ `qa.md`, `contact.jpg` | âš™ï¸ |
| 13 | Olhar o `contact.jpg` e o vÃ­deo; revisor independente (`claude -p`, lista fixa no `CLAUDE.md`, nota 0â€“10 de "pararia de rolar?" por quadro-chave) | â€” | ðŸ§  / ðŸ¤– |
| 14 | Publicar: v3 + fila do canal (`publicar.fila`) pela produÃ§Ã£o (`producao/producao.py`, abaixo); Telegram e outros destinos ficam com quem pediu | `python3 producao/producao.py --add edicoes/<id>` | âš™ï¸ |

Atalho: `python3 rtexjp.py tudo edicoes/<id>` roda 3 â†’ 7 â†’ 8 â†’ 10 â†’ 11 â†’ 12.

**Pelo bot, sem sessÃ£o nenhuma (05/11/2026): `/rtexjp <tema>` no inemaccbot** (prefixo `RJ`).

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| B1 | Pedido | `/rtexjp <tema ou tese>` no Telegram (canal e "agora" no texto; sem canal â†’ lives11) | Nei |
| B2 | Roteiro | fase `ficha` (`prompts/bot-ficha.md`): passos 1, 2, 3, 6 e 6b (desenhos que faltarem, print real da prova), `checar`, `medir.py --grep`, `producao/producao.py --add`; mostra o `BOT-RESUMO.md` | ðŸ¤– |
| B3 | ProduÃ§Ã£o | timer `rtexjp-producao` (5 em 5 min, uma montagem por rodada): `rtexjp.py tudo` (passos 7â€“12 + portÃ£o de beleza) â†’ revisor `claude -p` (`producao/revisor.md`, a lista fixa) â†’ v3 + fila do canal (a fila com timer do r7ex); reprovou/falhou â†’ `parado` + "Falhou" no v3; depois de corrigir: `producao.py --retomar <pasta>` | âš™ï¸ + ðŸ¤– |
| B4 | Fim no bot | fase `producao`: `producao/esperar.py <pasta>` espera `na_fila` e mostra o `BOT-FIM.md` | âš™ï¸ |

Teste da produÃ§Ã£o sem render nem Telegram: `python3 producao/teste_producao.py`. Estado: `python3 producao/producao.py --status`.

## Requisitos

- inemavox (TTS chatterbox no `venv`, Whisper large-v3) e a gravaÃ§Ã£o de referÃªncia da voz â€” `RTEXJP_INEMAVOX`, `RTEXJP_VOZ_REF`
- servidor de imagem local flux2-klein e a foto do avatar â€” `RTEXJP_IMG_URL`, `RTEXJP_AVATAR_REF`
- Node + `npm i` (Playwright 1.64), ffmpeg, Python 3 com Pillow e numpy

## EdiÃ§Ãµes

### 2026-10-28-mapa-v2 â€” "O Claude sumiu. E agora?" (visual v1.2)

`edicoes/2026-10-28-mapa-v2/final.mp4` â€” o mesmo roteiro, gancho de perda e isca DONO/REFÃ‰M da ediÃ§Ã£o abaixo, refeito no visual v1.2: avatar grande em 9 das 11 poses, um desenho-herÃ³i por batida, print real do GitHub (88,8 mil estrelas em 28/10/2026), papel azul-gelo em duas cenas. `comparativo.jpg` pÃµe 4 quadros da v1 em cima e da v2 embaixo.

### 2026-10-28-mapa â€” "O Claude sumiu. E agora?" (visual v1.1)

`edicoes/2026-10-28-mapa/final.mp4` â€” mantida para comparar. Um tema (Understand Anything), gancho de **perda**, 3 peÃ§as (o mapa, a explicaÃ§Ã£o, o impacto), isca de opiniÃ£o **DONO ou REFÃ‰M**. TÃ­tulo, descriÃ§Ã£o e comentÃ¡rio fixado no bloco `publicar` do `roteiro.json`.

### 2026-10-28-5-coisas â€” "5 coisas de IA deste mÃªs que quase ninguÃ©m percebeu" (formato antigo)

`edicoes/2026-10-28-5-coisas/final.mp4` â€” publicado em https://www.youtube.com/watch?v=AZEZK1YgF98. Paleta roxa, gancho de lista e isca com entregÃ¡vel (SETUP): regras que o formato atual proÃ­be. Fica no repositÃ³rio como registro; o `checar` ainda aceita esse roteiro, com aviso de LEGADO.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>