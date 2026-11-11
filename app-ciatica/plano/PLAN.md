# PLAN.md — Espalda Sana

## Objetivo (uma frase)
Uma web app em espanhol, instalada no Android do meu pai, que o guia todos os dias numa rotina de 14 exercícios para a ciática, um de cada vez, com boneco animado, voz masculina venezuelana e temporizador, e que regista a dor e os dias feitos só no telemóvel dele.

## Utilizador
O meu pai: venezuelano, mais velho, com dor ciática, pouca experiência com tecnologia, telemóvel Android. Sou eu que instalo a app no telemóvel dele.

## O que entra
- Rotina fixa de 14 exercícios (definidos abaixo, não alterar), em 3 blocos: sentado → deitado → de pé.
- Um exercício por ecrã: boneco animado (a parte que se mexe a azul, a posição final como sombra e uma seta de direção), instruções curtas, temporizador, repetições, séries e descansos.
- Voz **masculina** com sotaque **venezuelano**, gerada uma vez com a ElevenLabs e guardada como ficheiros MP3 dentro da app.
- Sinais sonoros curtos (bip) como reserva, a funcionar mesmo sem voz.
- Botão "Me duele": salta o exercício e regista-o.
- Dor antes e depois (5 níveis: Nada, Un poco, Regular, Bastante, Muchísimo).
- **Calendário do mês completo** (segunda a domingo) com os dias feitos a verde, o contador "X días hechos" e os dias seguidos.
- Ecrã de conselhos na primeira utilização.
- Funciona sem internet e instala-se no ecrã inicial (PWA).

## O que fica de fora (desta versão)
- Login, contas e base de dados no servidor.
- Envio de dados para mim ou para o médico (os dados ficam só no telemóvel dele).
- IA em tempo real dentro da app.
- Vídeos reais (fica o boneco animado).
- Versão curta de 10 minutos, lembretes diários, várias rotinas.
- Requisitos do curso de Vibe Coding (Supabase, OpenRouter, Resend): este é um projeto pessoal.

## Dados (só no telemóvel, localStorage)
```json
{
  "ack": true,
  "days": {
    "2026-11-11": { "done": true, "painBefore": 5, "painAfter": 3, "hurt": ["Puente"] }
  }
}
```
Mais a preferência "voz ligada/desligada". Sem servidor, sem dados pessoais fora do telemóvel.

## Ecrãs
1. **Inicio:** saudação, botão "Empezar", calendário do mês, lista de exercícios, "Consejos antes de empezar", "Voz activada", "Probar la voz".
2. **Consejos** (só na 1.ª vez): 4 regras simples e o botão "Entendido".
3. **Dolor antes:** 5 botões grandes com cor.
4. **Ejercicio** (×14): aviso de mudança de posição, nome, boneco animado, instruções, botões "Empezar" / "Escuchar explicación" / "Saltar"; durante o exercício: fase, contagem gigante, "Pausa", "Me duele".
5. **Dolor después:** 5 botões.
6. **Fin:** "¡Muy bien!", dor antes e depois, exercícios que doeram, "Volver al inicio".

## Exercícios (fixos)
**Sentado:** 1 Giro de tronco sentado · 2 Inclinación hacia un lado · 3 Deslizamiento del nervio (sentado) · 4 Levantarse de la silla
**Acostado:** 5 Respiración profunda · 6 Basculación de la pelvis · 7 Rodilla al pecho · 8 Círculos con las rodillas · 9 Giro de rodillas · 10 Puente · 11 Deslizamiento del nervio (acostado) · 12 Estiramiento del glúteo
**De pie:** 13 Extensión hacia atrás · 14 Marcha en el sitio

Os textos, as doses e os tempos de cada exercício estão no protótipo (`index.html`) e em `PROMPT_VIBE_LAB.md`. São a fonte de verdade.

## Ponto de partida
Já existe um protótipo funcional (`app-ciatica/index.html`) com os 14 exercícios, as animações, o temporizador, a dor antes e depois, o "Me duele" e o calendário mensal. **Partir dele**, não recomeçar do zero.

## Fases (pequenas; cada uma funciona de ponta a ponta)

### Fase 1 — Publicar o protótipo num link público
- Criar um repositório próprio no GitHub (`espalda-sana`) com o `index.html` do protótipo (página completa: `<!doctype html>`, `lang="es"`, meta viewport).
- Publicar na Vercel (site estático, sem build).
- **Pronto quando:** abro o link no telemóvel, faço a rotina do início ao fim e o dia fica verde no calendário.

### Fase 2 — Voz venezuelana (ElevenLabs)
- Lista de todas as frases faladas num ficheiro `frases.json` (id → texto).
- Script local `gerar-audios.mjs` que lê a chave de `.env.local` e cria `audio/<id>.mp3` com a voz masculina venezuelana escolhida.
- A app toca o MP3 certo em cada momento. Se faltar algum, usa um bip (nunca uma voz noutra língua).
- **Pronto quando:** a rotina completa é guiada pela voz nova no telemóvel do meu pai.

### Fase 3 — Instalar e funcionar sem internet
- `manifest.json` (nome "Espalda Sana", ícone, cor azul), service worker que guarda a página e os áudios.
- **Pronto quando:** com o modo de avião ligado, a app abre pelo ícone e a rotina funciona com voz.

### Fase 4 — Ajustes depois de uma semana de uso
- Ver com o meu pai o que custa: tamanho da letra, ritmo, volume, exercícios confusos.
- Só pequenas correções; ideias grandes vão para "Depois".

## Depois (quando a v1 estiver em uso)
Vídeos reais, versão curta de 10 minutos, lembrete diário, partilha do histórico com o médico, gravações com a minha voz.
