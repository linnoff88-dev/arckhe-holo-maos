# ðŸ–ï¸ HOLO MÃ£os â€” controle a tela com as mÃ£os, em portuguÃªs

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

[![HOLO MÃ£os](guia/assets/banner.jpg)](https://inematds.github.io/holo-maos/guia/)

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/holo-maos/guia/**

Camada INEMA em cima do **HOLO** (Zubair Trabzada, AI Workshop): um "deck" que roda no
navegador e transforma a sua webcam em interface â€” vocÃª belisca um cartÃ£o no ar, arrasta,
arremessa, junta duas mÃ£os pra dar zoom, e faz o sinal de paz pra arrumar tudo de volta.

Nada vai pra nuvem: o rastreamento de mÃ£o Ã© o **MediaPipe do Google rodando dentro da
prÃ³pria pÃ¡gina**, e os quadros da cÃ¢mera nÃ£o saem da sua mÃ¡quina. Sem API key, sem conta.

> **Este repositÃ³rio NÃƒO Ã© o projeto original.** O cÃ³digo do HOLO Ã© do Zubair Trabzada,
> MIT, e mora em **https://github.com/zubair-trabzada/holo-gestures**. Aqui ficam:
> a **anÃ¡lise** do que dÃ¡ pra fazer com isso no INEMA ([ANALISE.md](ANALISE.md)), as
> **evidÃªncias** de que roda no Linux, e a **adaptaÃ§Ã£o em PT-BR**.

## Rodar em 2 minutos

```bash
bash scripts/baixar-upstream.sh     # clona o repo oficial em upstream/
python3 scripts/aplicar-ptbr.py     # aplica a camada PT-BR + notas do INEMA
cd upstream && python3 server.py    # sÃ³ a biblioteca padrÃ£o do Python 3
```

Abra `http://localhost:4890` no Chrome e libere a cÃ¢mera. Sem cÃ¢mera? Use
`http://localhost:4890/?sim=1` (mÃ£os sintÃ©ticas) â€” o mouse tambÃ©m funciona em tudo.

## Testado aqui (21/09/2026, Linux â€” spark-922b)

| Item | Resultado |
|---|---|
| `python3 server.py` | âœ… sobe na porta 4890, sÃ³ stdlib |
| `GET /`, `/api/notes`, `/api/props` | âœ… 200 (pÃ¡gina 88 KB, notas e 2 modelos 3D) |
| PÃ¡gina carrega orbes + modelos 3D | âœ… deck montado, sem erro de JS |
| Bateria interna `?probe=1` (Chromium headless) | âš ï¸ passou **26/26** uma vez e depois ficou parando em **2/4** â€” **tambÃ©m no cÃ³digo original**, sem o nosso patch. Ã‰ o teste tocando o cartÃ£o antes de a cÃ¢mera mapear a tela em navegador sem interface; nÃ£o Ã© regressÃ£o da traduÃ§Ã£o |

A documentaÃ§Ã£o original fala
em Mac/Windows; **roda no Linux sem mudar uma linha**.

## Os gestos

| FaÃ§a isso | Acontece isso |
|---|---|
| Beliscar um cartÃ£o (polegar encosta no dedo) | pega, arrasta e arremessa com inÃ©rcia |
| Belisco rÃ¡pido (toque) | abre a pasta-orbe / abre a nota |
| Arremessar pra fora da tela | a nota some (volta reabrindo a orbe) |
| Dois beliscos afastando/juntando | zoom; torcendo as mÃ£os, gira a cena |
| Esticar um cartÃ£o com duas mÃ£os | grande = abre o leitor; amassado = a voz lÃª o resumo |
| Sinal de paz âœŒ mantido | **desfaz qualquer bagunÃ§a** â€” o gesto pra decorar |
| Tecla `F` | efeitos: repulsor, puxÃ£o, desenho, palma, arrumar em grade |
| Tecla `J` | modo JARVIS: fica dourado e a voz narra o que as mÃ£os fazem |

## A camada em portuguÃªs

`scripts/aplicar-ptbr.py` aplica 25 substituiÃ§Ãµes exatas no `holo.html` do upstream:
legenda de gestos, avisos de cÃ¢mera, falas do mordomo e a escolha da voz (de `en-GB`
fixo para `pt-BR`). Guarda o original em `holo.html.original` e **avisa** se o autor
mudou algum trecho, em vez de traduzir pela metade. Depois de um `git pull` no
upstream, Ã© sÃ³ rodar de novo.

As notas de exemplo em `notas-inema/` substituem as do autor â€” o `holo.json` passa a
apontar para elas automaticamente.

## Suas prÃ³prias notas

`holo.json` aponta pra qualquer pasta de arquivos markdown â€” subpastas viram orbes,
arquivos viram os cartÃµes:

```json
{"folder": "/caminho/para/suas/notas"}
```

## CrÃ©ditos e licenÃ§as

- **HOLO** â€” Zubair Trabzada / AI Workshop. CÃ³digo original **MIT**.
  Repo: https://github.com/zubair-trabzada/holo-gestures Â· VÃ­deo: https://www.youtube.com/watch?v=wJ3CFmzMbtA
- **MediaPipe Tasks Vision** (Google) Apache-2.0 Â· **three.js** MIT â€” embarcados no upstream.
- **Modelos 3D** â€” digitalizaÃ§Ãµes do Smithsonian (Apollo 11, Triceratops), CC0.
- O **PDF "HOLO Start Here"** e o texto do post sÃ£o material autoral do Zubair: **nÃ£o sÃ£o
  redistribuÃ­dos aqui**, sÃ³ citados como fonte.
- O que Ã© nosso (anÃ¡lise, adaptaÃ§Ã£o PT-BR, guia): MIT, INEMA.

---

Projeto adaptado da comunidade INEMA TDS - Marca Arckhe