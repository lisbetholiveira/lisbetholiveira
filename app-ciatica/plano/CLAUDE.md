# CLAUDE.md — Espalda Sana

## Sobre o projeto
App pessoal para o meu pai (venezuelano, mais velho, com ciática, Android): rotina diária guiada de 14 exercícios. O plano completo está em `PLAN.md`. Lê-o antes de qualquer tarefa.

## Como trabalhar comigo
- Fala comigo em **português de Portugal** e trata-me por "tu". Nunca programei: explica o que vais fazer e porquê, sem jargão.
- Trabalha **em modo plan**: mostra-me o plano antes de escreveres código e espera pela minha aprovação.
- **Uma tarefa de cada vez.** Só passas à fase seguinte do `PLAN.md` quando a atual funcionar e eu aprovar.
- Depois de cada mudança, testa tu mesmo (abre a app, faz a rotina) e mostra-me a prova. Diz-me também como testar no telemóvel.
- Antes de guardar no GitHub ou de publicar, mostra-me o que mudou e pede-me autorização.

## Stack (simples de propósito)
- Página estática: **HTML, CSS e JavaScript simples**, sem framework e sem build.
- Publicação: **Vercel** (site estático), com o código num repositório próprio no GitHub (`espalda-sana`).
- Dados: **localStorage**, só no telemóvel. Sem servidor, sem base de dados, sem login.
- Voz: ficheiros **MP3 gerados uma vez com a ElevenLabs** por um script local. A chave fica em `.env.local`, que está no `.gitignore`.
- PWA: `manifest.json` e service worker para funcionar sem internet.

## Língua e tom da app
- Toda a app e todo o áudio em **espanhol latino-americano (Venezuela)**, a tratar o utilizador por "tú". Frases curtas, simples e calorosas.
- Voz **masculina**, calma, com sotaque venezuelano.

## Visual
- Pensado para seniores: letra **Atkinson Hyperlegible**, base de 20px, títulos de 34px, botões com pelo menos 72px de altura e largura total, alto contraste.
- Cor principal **azul** (#1C56C4); verde (#1F7A46) para os dias feitos; laranja-tijolo (#A8431B) para "Me duele". Fundo claro azulado (#EEF3F6) e modo escuro automático.
- Um exercício por ecrã. Sem menus, sem anúncios, sem distrações.

## Nunca fazer
- **Nunca alterar a lista, a ordem, as doses nem as instruções dos 14 exercícios** sem eu pedir.
- Nunca acrescentar login, contas, base de dados no servidor, analítica ou envio de dados para fora do telemóvel.
- Nunca usar a voz do sistema numa língua que não seja espanhol. Se faltar um áudio, usa um bip.
- Nunca pôr chaves ou palavras-passe no código nem no GitHub. Nunca mas peças no chat: diz-me onde as colocar.
- Nunca recomeçar do zero: parte do protótipo `index.html` que já existe.
- Nunca acrescentar funcionalidades da lista "Depois" sem eu pedir.
- Nunca apagar ficheiros nem publicar sem a minha aprovação.
