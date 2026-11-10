# Prompt — App "Espalda al Día" (Vibe Lab)

Cria uma web app mobile-first (PWA instalável no ecrã inicial do Android) chamada **"Espalda al Día"**: uma rotina diária guiada de exercícios para aliviar a dor ciática, pensada para um homem mais velho, venezuelano, com pouca experiência com tecnologia. Toda a interface e todo o áudio são em **espanhol neutro latino-americano (Venezuela)**, tratando o utilizador por "tú".

## Objetivo
Que ele consiga fazer sozinho, todos os dias, cerca de 25 minutos de exercícios seguros, **um exercício de cada vez**, guiado por voz, animação e temporizador, sem ter de ler muito nem tomar decisões.

## Princípios de design (obrigatórios)
- Acessibilidade sénior: letra base 20px, títulos 34px, botões com pelo menos 72px de altura e largura total, alto contraste, fonte **Atkinson Hyperlegible**.
- Uma tarefa por ecrã. Sem menus, sem login, sem registo, sem anúncios.
- Modo claro e escuro automáticos.
- Funciona offline depois da primeira abertura (service worker) e pode ser adicionada ao ecrã inicial com ícone próprio (manifest).
- Ecrã sempre ligado durante os exercícios (Wake Lock API).
- Dados guardados só no telemóvel (localStorage). Sem backend.

## Ecrãs e fluxo
1. **Início:** "¡Hola!", título "Ejercicios para la ciática", texto "Unos 25 minutos. Un ejercicio a la vez: la app te explica cada uno en voz alta y te lleva el tiempo.", botão grande **"Empezar"**, calendário dos últimos 14 dias (dias feitos a verde; dias da semana Do Lu Ma Mi Ju Vi Sá), contador de dias seguidos ("Llevas 3 días seguidos. ¡Sigue así!"), lista de exercícios recolhível, botão "Consejos antes de empezar", interruptor "Voz activada" e botão "Probar la voz". Nota de rodapé: "Rutina basada en las recomendaciones actuales para la ciática: ejercicio regular, movilización suave del nervio y mantenerse activo. No reemplaza la consulta con el médico o el fisioterapeuta."
2. **Conselhos** (aparece só na primeira vez): "Haz todos los movimientos despacio y sin forzar." / "Es normal sentir un estiramiento suave en la espalda o en el glúteo." / "Si el dolor o el hormigueo se extiende más abajo por la pierna, deja ese ejercicio y toca «Me duele»." / "Usa una cama firme o una colchoneta, y una silla firme pegada a la pared." Botão "Entendido".
3. **Dor antes:** "¿Cuánto te duele ahora?" com 5 botões grandes e um ponto de cor: Nada (verde), Un poco, Regular, Bastante, Muchísimo (vermelho). Se escolher "Muchísimo", mostra: "Si hoy te duele mucho, haz solo lo que puedas, más despacio, y sáltate lo que te moleste. Si es un dolor nuevo o diferente al de siempre, consulta con el médico." e o botão "Seguir".
4. **Exercício** (um por ecrã):
   - Topo: "3 de 14", barra de progresso, botão "Salir".
   - Aviso destacado quando muda de posição: no primeiro, "Siéntate en una silla firme, sin ruedas y pegada a la pared."; ao passar a deitado, "Ahora acuéstate boca arriba en una cama firme o en una colchoneta."; ao passar a de pé, "Ahora levántate con calma y ponte de pie cerca de algo donde apoyarte."
   - Nome do exercício, etiqueta da posição e **animação grande de um boneco** (vista de lado; vista de frente na inclinação lateral) em loop entre a posição inicial e a final. A parte do corpo que se mexe fica a azul, a posição final aparece como sombra azul clara e uma seta tracejada mostra a direção do movimento. Legenda: "Lo que se mueve" / "Adónde llegar".
   - Antes de começar: dose, 3 instruções numeradas e uma dica. Botões "Empezar", "Escuchar explicación" e "Saltar".
   - Durante: palavra da fase em grande (ex.: "Sube"), contagem decrescente gigante, informação "Repetición 3 de 8 · Serie 1 de 2 · Pierna derecha". Botões "Pausa"/"Seguir" e **"Me duele"** (salta o exercício e regista-o). A animação acompanha cada fase. Entre séries e entre lados há descanso com contagem ("Descansa. Ahora vamos con la pierna izquierda."). Nas fases de 10 segundos ou mais, a voz conta "tres, dos, uno". No fim diz "¡Muy bien!" e passa ao seguinte, que fica à espera do botão "Empezar".
5. **Dor depois:** "¿Y cuánto te duele ahora, después de los ejercicios?" (as mesmas 5 opções).
6. **Fim:** "¡Muy bien! Terminaste los ejercicios de hoy. Mañana seguimos.", comparação de dor antes e depois ("El dolor bajó. ¡Excelente!" / "El dolor subió. Mañana hazlos más despacio y sáltate los que te molesten." / "El dolor se mantuvo igual."), lista "Ejercicios que te dolieron hoy" com a nota "Si te duelen siempre, enséñale esta lista al médico o al fisioterapeuta." e o botão "Volver al inicio". Marca o dia como feito.

## Rotina (14 exercícios, por esta ordem)
Formato: nome | dose | fases (palavra falada, segundos) | instruções | dica.

**Bloco 1 — Sentado en una silla**

1. **Giro de tronco sentado** | 3 × 15 s para cada lado | Gira 3 · Aguanta 15 · Al frente 3 | Siéntate en una silla firme, con la espalda recta y los pies apoyados en el suelo. / Gira el tronco despacio hacia un lado y agárrate del respaldo de la silla. / Aguanta respirando tranquilo y vuelve al frente. | Gira desde la cintura, sin forzar el cuello.
2. **Inclinación hacia un lado** | 3 × 10 s para cada lado | Inclínate 3 · Aguanta 10 · Al centro 3 | Sentado con la espalda recta, levanta un brazo por encima de la cabeza. / Inclina el tronco despacio hacia el lado contrario. / Aguanta respirando tranquilo y vuelve al centro. | Notarás un estiramiento suave en el costado. No te inclines hacia delante.
3. **Deslizamiento del nervio (sentado)** | 10 com cada perna | Estira y mira arriba 2 · Dobla y mira abajo 2 | Siéntate en el borde de una silla firme, con la espalda recta. / Estira una rodilla y, a la vez, mira hacia arriba. / Después dobla la rodilla y mira hacia abajo. Suave, sin aguantar. | Usa una silla sin ruedas, pegada a la pared.
4. **Levantarse de la silla** | 2 séries de 6 | Arriba 3 · Siéntate despacio 3 | Cruza los brazos sobre el pecho y apoya bien los pies en el suelo. / Échate un poco hacia delante y ponte de pie con la fuerza de las piernas. / Siéntate despacio, controlando la bajada. Si lo necesitas, apóyate con las manos. | Fortalece las piernas y te ayuda en el día a día.

**Bloco 2 — Acostado boca arriba**

5. **Respiración profunda** | 6 respirações | Toma aire 4 · Suelta el aire 5 | Acuéstate boca arriba con las rodillas dobladas y los pies apoyados. / Pon las manos sobre la barriga. / Toma aire por la nariz inflando la barriga, y suéltalo despacio por la boca. | Sirve para relajar los músculos antes de empezar.
6. **Basculación de la pelvis** | 2 séries de 8 | Aplana la espalda 2 · Aguanta 3 · Relaja 3 | Rodillas dobladas y pies apoyados en el suelo. / Aplana la parte baja de la espalda contra el suelo, metiendo la barriga. / Aguanta un momento y relaja. Es un movimiento pequeño. | Respira con normalidad. No aguantes el aire.
7. **Rodilla al pecho** | 3 × 20 s com cada perna | Rodilla al pecho 3 · Aguanta 20 · Suelta 4 | Abraza una rodilla con las dos manos. / Llévala despacio hacia el pecho. La otra pierna sigue doblada. / Notarás un estiramiento suave en la espalda y en el glúteo. | Lleva la rodilla solo hasta donde te resulte cómodo.
8. **Círculos con las rodillas** | 1 minuto contínuo (a voz diz aos 30 s: "Ahora en el otro sentido.") | Lleva las dos rodillas hacia el pecho y pon una mano en cada rodilla. / Haz círculos pequeños y lentos con las rodillas. / A la mitad del tiempo, cambia de sentido. | Es un masaje suave para la parte baja de la espalda.
9. **Giro de rodillas** | 6 para cada lado | Hacia la derecha 3 · Al centro 2 · Hacia la izquierda 3 · Al centro 2 | Junta las rodillas. / Déjalas caer despacio hacia un lado, solo hasta donde te resulte cómodo. Los hombros no se despegan del suelo. / Vuelve al centro y repite hacia el otro lado. | Hazlo lento, sin impulso.
10. **Puente** | 2 séries de 8 | Sube 2 · Aguanta 3 · Baja 3 | Pies apoyados a la anchura de las caderas y brazos a los lados. / Aprieta los glúteos y levanta la cadera hasta que hombros, cadera y rodillas queden en línea. / Baja despacio. | Fortalece los glúteos y protege la espalda. No hace falta subir mucho.
11. **Deslizamiento del nervio (acostado)** | 10 com cada perna | Estira 2 · Dobla 2 | Sujeta la pierna por detrás del muslo, con la rodilla doblada y el muslo vertical. / Estira la rodilla despacio hasta notar una ligera tensión. / Vuelve a doblarla. Es un vaivén suave: no te quedes con la pierna estirada. | Es normal un hormigueo leve que se pasa enseguida. Si va a más, para.
12. **Estiramiento del glúteo** | 2 × 20 s com cada perna | Acerca las piernas 3 · Aguanta 20 · Suelta 5 | Cruza un tobillo sobre la rodilla contraria, formando un 4. / Agarra el muslo de la pierna de abajo y acerca las dos piernas al pecho. / Notarás el estiramiento en el glúteo. Respira tranquilo. | Si no llegas al muslo, ayúdate con una toalla.

**Bloco 3 — De pie**

13. **Extensión hacia atrás** | 10 vezes | Hacia atrás 3 · Recto 3 | De pie, con los pies separados y las manos en la parte baja de la espalda. / Inclina el tronco hacia atrás despacio, solo un poco, mirando al frente. / Vuelve a ponerte recto. | A algunas personas este movimiento las alivia y a otras les molesta. Si el dolor aumenta o baja por la pierna, sáltalo.
14. **Marcha en el sitio** | 3 minutos contínuos (a voz avisa "Quedan dos minutos.", "Queda un minuto." e "Quedan diez segundos.") | De pie, cerca de una pared o un mueble por si necesitas apoyarte. / Marcha sin moverte del sitio, a un ritmo cómodo, levantando un poco las rodillas. / Si lo prefieres, puedes salir a caminar. | Mantenerte activo es de lo que más ayuda con la ciática.

Descanso: 15 s entre séries, 8–10 s ao trocar de perna ou de lado. Nos exercícios com lados, a voz anuncia "Pierna derecha" / "Pierna izquierda" (ou "Lado derecho" / "Lado izquierdo" nos exercícios 1 e 2).

## Voz (muito importante)
- **Não usar a voz do sistema (Web Speech API) como voz principal**: a qualidade em espanhol é má e varia de aparelho para aparelho.
- Gerar antecipadamente **ficheiros de áudio MP3** com a API da **ElevenLabs** (modelo multilingue, uma voz masculina ou feminina calma com **sotaque venezuelano**), para todas as frases da app: nomes dos exercícios, instruções completas ("Escuchar explicación"), palavras das fases, descansos, avisos de mudança de posição, números "tres, dos, uno", avisos de tempo, "¡Muy bien!", "¡Muy bien! ¡Chévere! Terminaste los ejercicios de hoy." e a frase de teste "Hola. Esta es la voz que te va a guiar en los ejercicios."
- Guardar os áudios na app (pasta `/audio`, com nomes estáveis) e pré-carregá-los, para funcionarem offline. A chave da API nunca fica no código do lado do cliente: os áudios geram-se uma vez, num script de build.
- Se faltar um áudio, recorrer à voz do sistema em espanhol latino-americano (preferir es-VE, depois es-US, es-MX, es-CO) e **nunca** a uma voz noutra língua.
- Adicionar também **sinais sonoros curtos** (Web Audio): um ao mudar de fase e outro ao terminar cada exercício, para funcionar mesmo com a voz desligada.
- O áudio só começa depois do primeiro toque do utilizador (regra dos browsers).

## Dados guardados (localStorage)
`{ ack: boolean, days: { "AAAA-MM-DD": { done, painBefore, painAfter, hurt: [nomes] } } }` e a preferência de voz ligada/desligada.

## Fora do âmbito (não fazer)
Contas de utilizador, pagamentos, notificações push, partilha nas redes sociais, mais rotinas. Mantém a app simples.

## Critérios de aceitação
- Num Android com Chrome, abre-se pelo ícone do ecrã inicial e funciona sem internet.
- Uma pessoa mais velha consegue fazer a rotina inteira tocando apenas em "Empezar" (e, se quiser, em "Me duele").
- A voz soa natural, em espanhol venezuelano, e está sincronizada com a animação e a contagem.
- O calendário marca o dia como feito no fim da rotina.
