ï»¿# rtexjp ê¢â¬â motor de reels ilustrados 9:16

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![rtexjp](capa/capa.png)](https://linnoff88-dev.github.io/arckhe-/guia/)

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

O rtexjp êÂ© um motor que monta vêÂ­deos curtos verticais (reels) ilustrados, em azul-marinho, a partir de um roteiro escrito num arquivo de texto (`roteiro.json`). êâ° o motor que o Nei usa nos reels do ARCKHÉ, aberto para quem quiser estudar ou adaptar: sem gravar a si mesmo e sem pagar serviêÂ§o de avatar. Ele gera a voz, desenha cada cena quadro a quadro, mistura a trilha e confere sozinho se o vêÂ­deo segue o formato. Precisa de um computador com placa de vêÂ­deo (GPU), Python, Node, ffmpeg e dois servidores locais: o de voz ([ARCKHÉvox](https://github.com/linnoff88-dev/ARCKHÉvox)) e o de imagem ([ARCKHÉimg](https://github.com/linnoff88-dev/ARCKHÉimg), flux2-klein).

Vem configurado com a voz e o avatar do Nei. Para usar os seus, aponte as variêÂ¡veis de ambiente `RTEXJP_VOZ_REF` (gravaêÂ§êÂ£o de referêÂªncia da voz, `.wav`) e `RTEXJP_AVATAR_REF` (foto do avatar) para os seus arquivos, descreva o seu personagem em `RTEXJP_AVATAR_DESC` e gere as poses de novo (`python3 motor/gerar_avatar.py`); esses dois arquivos nêÂ£o vêÂªm no repositêÂ³rio. Veja **Caminhos e variêÂ¡veis de ambiente** abaixo.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/arckhe-/guia/** êÂ· 1êÂº vêÂ­deo (paleta antiga, roxa): https://www.youtube.com/watch?v=AZEZK1YgF98

**v1.3.0** (05/11/2026: `/rtexjp` no ARCKHÉccbot + produêÂ§êÂ£o sem sessêÂ£o) êÂ· motor local e grêÂ¡tis que transforma um `roteiro.json` num reel vertical 1080êâ1920 no **padrêÂ£o rtexjp**: um reel ilustrado em azul-marinho (com trocas para um papel azul-gelo), avatar ilustrado do Nei **grande** (ê¢â°Ë 43 % da altura, em 11 poses ligadas êÂ  emoêÂ§êÂ£o da fala, sem lip-sync), um **desenho-herêÂ³i** por cena, **print real** como prova, manchete Sora centrada, legenda karaokêÂª, mascote robêÂ´ e um êÂºnico CTA de **opiniêÂ£o** (uma pergunta com lado, respondida com uma palavra: "comenta DONO ou REFêâ°M").

## O formato (padrêÂ£o rtexjp)

Esqueleto fixo, conferido pelo validador (`checar`) e pelo QA (`qa`):

1. **Gancho no quadro 0** (`gancho.tipo` no roteiro), um destes: **contrêÂ¡rio** (manda parar algo que todo mundo faz), **perda** (e se X sumisse?), **estatêÂ­stica de medo** com fonte na tela, ou **histêÂ³ria de terceiro** com nêÂºmero. Proibido: lista ("5 coisasê¢â¬Â¦"), "vocêÂª sabia queê¢â¬Â¦", "eu fizê¢â¬Â¦".
2. **Manchete do quadro 0** com no mêÂ¡ximo ~6 palavras, caixa alta, **uma** palavra em amarelo, mais agressiva que a fala (o texto puxa quem rola sem som, a voz suaviza). JêÂ¡ estêÂ¡ pronta no quadro 0, que serve de capa. Um **objeto-metêÂ¡fora com dano** desenhado (riscado de vermelho, sumindo, quebrado), o avatar **reage** no 1êÂº segundo e algo muda a cada ~1 s nos 3 primeiros segundos.
3. **Prova atêÂ© 20 s** ê¢â¬â nêÂºmero com fonte (contador que pousa no nêÂºmero, linha de fonte em monoespaêÂ§ada embaixo) ou autoridade.
4. **O problema de quem assiste, com absolviêÂ§êÂ£o** ("nêÂ£o êÂ© culpa sua, ninguêÂ©m te deu X") ê¢â¬â e aqui a **tensêÂ£o da isca** êÂ© plantada: as opêÂ§êÂµes da pergunta final aparecem na tela, em amarelo.
5. **Um tema por vêÂ­deo**; o mêÂ©todo em 2ê¢â¬â5 **peêÂ§as** anunciadas com êÂ­ndice visêÂ­vel e barra de pêÂ­lulas no topo durante as peêÂ§as.
6. **Uma peêÂ§a por vez, um objeto visual por frase** ê¢â¬â o objeto muda dentro da cena a cada ~2ê¢â¬â3 s.
7. **Ressalva honesta falada**, em cartêÂ£o de alerta (vermelho = problema, verde = certo).
8. **MêÂ¡xima em antêÂ­tese**, depois de **0,8 s de silêÂªncio real** (voz e cama param).
9. **CTA de opiniêÂ£o**: pergunta forte, emocional e com lado, ligada êÂ  tese; o Nei diz o lado dele antes ("eu quero ser dono do meu") e pede a resposta em uma palavra ("comenta DONO ou REFêâ°M"). O cartêÂ£o mostra a pergunta + as opêÂ§êÂµes, a caixa de comentêÂ¡rio digita uma opêÂ§êÂ£o ê¢â â Publicar ê¢â â confirmaêÂ§êÂ£o, segurado ~10 s, sem despedida. **Proibido prometer entrega** ("te mando", "eu envio", "comenta X queê¢â¬Â¦"): o Nei nêÂ£o responde comentêÂ¡rios. Link e fonte ficam parados no comentêÂ¡rio fixado/descriêÂ§êÂ£o (bloco `publicar` do roteiro), nunca como recompensa por comentar.

Visual (v1.2, ediêÂ§êÂµes com `"versao": "rtexjp/3"`): cada quadro tem a mesma casca, de cima para baixo ê¢â¬â rêÂ³tulo em mono (ê¢â°Â¥ 30 px) êÂ· **manchete em Sora ExtraBold, centrada, 2ê¢â¬â3 linhas, ê¢â°Â¥ 96 px**, branco `#f4f7fc` com uma palavra em azul-aêÂ§o claro `#93c5fd` (amarela `#FACC15` sêÂ³ no quadro 0) êÂ· **desenho-herêÂ³i** (objeto ilustrado no mesmo estilo flat do avatar, da biblioteca `motor/assets/objetos/`, ou o **print real** da pêÂ¡gina da fonte com a linha `fonte:` embaixo) êÂ· **legenda karaokêÂª** (Montserrat ExtraBold 74 px com contorno preto, a palavra dita em azul-aêÂ§o) numa faixa prêÂ³pria êÂ· **avatar grande**, embaixo e centralizado (820 px, ê¢â°Ë 43 % da altura), na pose do bloco ou da batida. O fundo tem holofote e grêÂ£o leve e alterna entre marinho `#07111f` e papel azul-gelo `#e8eef7` (`cena.tema: "claro"`, letras marinho, destaque em faixa `#1e3a8a`). No silêÂªncio antes da mêÂ¡xima o êÂºltimo quadro fica congelado com o avatar pensativo: nunca tela vazia. Amarelo sêÂ³ na palavra quente do quadro 0 e na pergunta/opêÂ§êÂµes da isca (letra `#1a1206` no preenchimento); verde/vermelho sêÂ³ certo/errado. Zonas seguras do Reels: rosto, texto e objetos acima de 80 % da altura (abaixo dali sêÂ³ o tronco do avatar).

**PortêÂ£o de beleza** (`medir.py`, sêÂ³ em `rtexjp/3`): o palco mede no prêÂ³prio DOM, em 2 amostras por bloco, a manchete (ê¢â°Â¥ 96 px), todo texto (ê¢â°Â¥ 30 px), a êÂ¡rea ocupada no quadro êÂºtil (ê¢â°Â¥ 55 %), o contraste do texto (WCAG ê¢â°Â¥ 4,5:1) e a altura do avatar (ê¢â°Â¥ 38 %).

EdiêÂ§êÂµes antigas (`rtexjp/2`) continuam com o visual da v1.1 (Anton êÂ  esquerda, avatar pequeno no canto).

êÂudio: voz do Nei (ARCKHÉvox chatterbox, 0,6/0,6, `atempo` ê¢â°Â¤ 1,15, pausas internas encurtadas), 160ê¢â¬â190 palavras/min, cama musical baixa com sidechain, master ê¢Ëâ14 LUFS.

> **ExceêÂ§êÂ£o ao kit ARCKHÉ:** avatar ilustrado e mascote robêÂ´ sêÂ£o decisêÂ£o de projeto (registrada em `ARCKHÉ-design/DECISOES.md`, D19). A paleta segue o kit em espêÂ­rito: marinho + azul, amarelo `#FACC15` como êÂºnica cor quente. A 1êÂª ediêÂ§êÂ£o (`2026-10-28-5-coisas`) êÂ© do formato antigo ê¢â¬â paleta roxa, gancho de lista e isca com entregêÂ¡vel ê¢â¬â e fica como estêÂ¡, porque jêÂ¡ foi publicada.

## Caminhos e variêÂ¡veis de ambiente

| VariêÂ¡vel | Para quêÂª | PadrêÂ£o |
|---|---|---|
| `RTEXJP_ARCKHÉVOX` | pasta do ARCKHÉvox (TTS chatterbox no `venv` + Whisper large-v3) | `~/projetos/ARCKHÉvox` |
| `RTEXJP_VOZ_REF` | gravaêÂ§êÂ£o de referêÂªncia da voz (`.wav`) | `~/projetos/timesmkt3/media/voice-refs/nei.wav` |
| `RTEXJP_IMG_URL` | servidor de imagem flux2-klein (`motor/gerar_avatar.py`, `motor/gerar_imagem.py`) | `http://localhost:8000/generate` |
| `RTEXJP_AVATAR_REF` | foto de referêÂªncia do avatar | `~/projetos/ARCKHÉ-referencias/nei-avatar.jpg` |
| `RTEXJP_AVATAR_DESC` | traêÂ§os e roupa do personagem no pedido de imagem (em inglêÂªs); troque junto com a foto | bonêÂ© preto, êÂ³culos, barba grisalha, camiseta azul-aêÂ§o (o Nei) |
| `RTEXJP_TRILHA` | cama musical do mix (para publicar, use uma mêÂºsica cuja licenêÂ§a vocêÂª conheêÂ§a) | `motor/assets/trilha.mp3` |
| `CS_WHISPER_PY` | Python do ambiente com faster-whisper (servidor do Whisper e plano B) | `~/miniconda3/envs/chatterbox/bin/python3` |
| `CHATTERBOX_PYTHON` | Python do ambiente do chatterbox, exigido pelo `tts_direct.py` do ARCKHÉvox | o do ambiente `chatterbox` |

Exemplo: `RTEXJP_VOZ_REF=~/minha-voz.wav RTEXJP_ARCKHÉVOX=~/ARCKHÉvox python3 rtexjp.py voz edicoes/minha-edicao`.

## Estrutura

```
rtexjp.py              pipeline: checar êÂ· voz êÂ· cena êÂ· render êÂ· mix êÂ· qa êÂ· tudo
medir.py               QA automêÂ¡tico (duraêÂ§êÂ£o, wpm, LUFS, trocas/min, isca, cartêÂ£o final, silêÂªncio, grep de fonte) + contact.jpg
motor/palco.html       o palco: casca v1.2 (manchete, herêÂ³i, avatar, legenda) desenhada por window.render(t) + window.medidas(t) (portêÂ£o de beleza)
motor/render.mjs       Playwright quadro a quadro -> ffmpeg (30 fps)
motor/gerar_avatar.py  poses do avatar no flux2-klein local com a foto de referêÂªncia (fundo verde recortado)
motor/capturar_prova.mjs print real da fonte para a prova (Playwright, tema escuro, 2x)
motor/gerar_objeto.py  desenho-herêÂ³i no flux2-klein local -> motor/assets/objetos/<nome>.png + indice.json
motor/gerar_imagem.py  imagem de cena no flux2-klein local
motor/whisper.py       Whisper large-v3 local (ARCKHÉvox) com tempo por palavra
motor/avatar/*.png     11 poses: bracos, queixo, apontando, segurando, surpreso, mostrando, explica, olha, polegar, duvida, susto
motor/assets/objetos/  biblioteca de desenhos-herêÂ³i (terminal_quebrado, mapa_pinos, lupa_arquivos, dominos, chave_donoê¢â¬Â¦) + indice.json
motor/assets/          trilha.mp3 (cama), grao.png (textura), carro.png
motor/fontes/          Sora, Anton, JetBrains Mono, Montserrat (OFL)
edicoes/<id>/          roteiro.json êÂ· final.mp4 êÂ· contact.jpg êÂ· qa.md êÂ· prova/ (prints reais) (voz/ e build/ ficam fora do git)
```

## O processo, do inêÂ­cio ao fim

ê°Å¸Â§Â  sessêÂ£o com o Nei êÂ· ê¢Å¡â¢ê¯Â¸Â script (zero token) êÂ· ê°Å¸Â¤â `claude -p` / Codex pela assinatura (nunca API)

| # | Passo | Comando | Quem |
|---|---|---|---|
| 1 | Pauta: tese, 2ê¢â¬â5 peêÂ§as, nêÂºmeros conferidos (ê¢Åâ¦ com fonte e data) | ê¢â¬â | ê°Å¸Â§Â  |
| 2 | Roteiro: escrever `edicoes/<id>/roteiro.json` (`gancho`, `isca` de opiniêÂ£o, fala por extenso, `fala_tts` para pronêÂºncia, gatilhos por palavra, bloco `publicar`) | editar o JSON (ou ê°Å¸Â¤â a partir da pauta) | ê°Å¸Â¤â + ê°Å¸Â§Â  |
| 3 | Validar regras do formato | `python3 rtexjp.py checar edicoes/<id>` | ê¢Å¡â¢ê¯Â¸Â |
| 4 | Aprovar o roteiro (gancho, pergunta da isca, nêÂºmeros) | ê¢â¬â | ê°Å¸Â§Â  |
| 5 | Poses do avatar (uma vez; refazer sêÂ³ se mudar o personagem) ê¢â¬â olhar cada uma e refazer as deformadas | `python3 motor/gerar_avatar.py [pose ê¢â¬Â¦]` | ê¢Å¡â¢ê¯Â¸Â |
| 6 | Desenho-herêÂ³i que faltar na biblioteca (olhar e refazer com outra seed se sair torto) | `python3 motor/gerar_objeto.py <nome> "<objeto em inglêÂªs>" [seed]` | ê¢Å¡â¢ê¯Â¸Â |
| 6b | Print real da fonte (pêÂ¡gina do repositêÂ³rio, recortada no nome e no contador) em `edicoes/<id>/prova/` | `node motor/capturar_prova.mjs <url> edicoes/<id>/prova/x.png [--clip x,y,w,h]` | ê¢Å¡â¢ê¯Â¸Â |
| 7 | Voz por bloco + Whisper (tempo por palavra) | `python3 rtexjp.py voz edicoes/<id> [bloco ê¢â¬Â¦]` (com nomes, refaz sêÂ³ esses TTS) | ê¢Å¡â¢ê¯Â¸Â |
| 8 | Cena (roteiro + tempos) | `python3 rtexjp.py cena edicoes/<id>` | ê¢Å¡â¢ê¯Â¸Â |
| 9 | PrêÂ©via de quadros (+ `quadros/medidas.json` do portêÂ£o de beleza) | `node motor/render.mjs edicoes/<id>/build --quadros 0,10,20` ê¢â â `edicoes/<id>/quadros/` | ê¢Å¡â¢ê¯Â¸Â |
| 10 | Render 1080êâ1920 30 fps | `python3 rtexjp.py render edicoes/<id>` | ê¢Å¡â¢ê¯Â¸Â |
| 11 | Mixagem (cama para no silêÂªncio da mêÂ¡xima, ê¢Ëâ14 LUFS) | `python3 rtexjp.py mix edicoes/<id>` | ê¢Å¡â¢ê¯Â¸Â |
| 12 | QA automêÂ¡tico + portêÂ£o de beleza + contact sheet | `python3 rtexjp.py qa edicoes/<id>` ê¢â â `qa.md`, `contact.jpg` | ê¢Å¡â¢ê¯Â¸Â |
| 13 | Olhar o `contact.jpg` e o vêÂ­deo; revisor independente (`claude -p`, lista fixa no `CLAUDE.md`, nota 0ê¢â¬â10 de "pararia de rolar?" por quadro-chave) | ê¢â¬â | ê°Å¸Â§Â  / ê°Å¸Â¤â |
| 14 | Publicar: v3 + fila do canal (`publicar.fila`) pela produêÂ§êÂ£o (`producao/producao.py`, abaixo); Telegram e outros destinos ficam com quem pediu | `python3 producao/producao.py --add edicoes/<id>` | ê¢Å¡â¢ê¯Â¸Â |

Atalho: `python3 rtexjp.py tudo edicoes/<id>` roda 3 ê¢â â 7 ê¢â â 8 ê¢â â 10 ê¢â â 11 ê¢â â 12.

**Pelo bot, sem sessêÂ£o nenhuma (05/11/2026): `/rtexjp <tema>` no ARCKHÉccbot** (prefixo `RJ`).

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| B1 | Pedido | `/rtexjp <tema ou tese>` no Telegram (canal e "agora" no texto; sem canal ê¢â â lives11) | Nei |
| B2 | Roteiro | fase `ficha` (`prompts/bot-ficha.md`): passos 1, 2, 3, 6 e 6b (desenhos que faltarem, print real da prova), `checar`, `medir.py --grep`, `producao/producao.py --add`; mostra o `BOT-RESUMO.md` | ê°Å¸Â¤â |
| B3 | ProduêÂ§êÂ£o | timer `rtexjp-producao` (5 em 5 min, uma montagem por rodada): `rtexjp.py tudo` (passos 7ê¢â¬â12 + portêÂ£o de beleza) ê¢â â revisor `claude -p` (`producao/revisor.md`, a lista fixa) ê¢â â v3 + fila do canal (a fila com timer do r7ex); reprovou/falhou ê¢â â `parado` + "Falhou" no v3; depois de corrigir: `producao.py --retomar <pasta>` | ê¢Å¡â¢ê¯Â¸Â + ê°Å¸Â¤â |
| B4 | Fim no bot | fase `producao`: `producao/esperar.py <pasta>` espera `na_fila` e mostra o `BOT-FIM.md` | ê¢Å¡â¢ê¯Â¸Â |

Teste da produêÂ§êÂ£o sem render nem Telegram: `python3 producao/teste_producao.py`. Estado: `python3 producao/producao.py --status`.

## Requisitos

- ARCKHÉvox (TTS chatterbox no `venv`, Whisper large-v3) e a gravaêÂ§êÂ£o de referêÂªncia da voz ê¢â¬â `RTEXJP_ARCKHÉVOX`, `RTEXJP_VOZ_REF`
- servidor de imagem local flux2-klein e a foto do avatar ê¢â¬â `RTEXJP_IMG_URL`, `RTEXJP_AVATAR_REF`
- Node + `npm i` (Playwright 1.64), ffmpeg, Python 3 com Pillow e numpy

## EdiêÂ§êÂµes

### 2026-10-28-mapa-v2 ê¢â¬â "O Claude sumiu. E agora?" (visual v1.2)

`edicoes/2026-10-28-mapa-v2/final.mp4` ê¢â¬â o mesmo roteiro, gancho de perda e isca DONO/REFêâ°M da ediêÂ§êÂ£o abaixo, refeito no visual v1.2: avatar grande em 9 das 11 poses, um desenho-herêÂ³i por batida, print real do GitHub (88,8 mil estrelas em 28/10/2026), papel azul-gelo em duas cenas. `comparativo.jpg` pêÂµe 4 quadros da v1 em cima e da v2 embaixo.

### 2026-10-28-mapa ê¢â¬â "O Claude sumiu. E agora?" (visual v1.1)

`edicoes/2026-10-28-mapa/final.mp4` ê¢â¬â mantida para comparar. Um tema (Understand Anything), gancho de **perda**, 3 peêÂ§as (o mapa, a explicaêÂ§êÂ£o, o impacto), isca de opiniêÂ£o **DONO ou REFêâ°M**. TêÂ­tulo, descriêÂ§êÂ£o e comentêÂ¡rio fixado no bloco `publicar` do `roteiro.json`.

### 2026-10-28-5-coisas ê¢â¬â "5 coisas de IA deste mêÂªs que quase ninguêÂ©m percebeu" (formato antigo)

`edicoes/2026-10-28-5-coisas/final.mp4` ê¢â¬â publicado em https://www.youtube.com/watch?v=AZEZK1YgF98. Paleta roxa, gancho de lista e isca com entregêÂ¡vel (SETUP): regras que o formato atual proêÂ­be. Fica no repositêÂ³rio como registro; o `checar` ainda aceita esse roteiro, com aviso de LEGADO.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>