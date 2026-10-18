# Giro — mudanças (v2)

NÃO TESTADO NO NAVEGADOR: sem internet aqui não consegui rodar `npm install`, `npm run build` nem abrir o jogo. Conferi a sintaxe e os tipos com versões simplificadas de three/react/zustand, mas ninguém viu isto na tela ainda. Rode `npm install && npm run dev` e me mande qualquer erro ou print.

## Menu (giro_menu_verde_bege.html)
O menu enviado virou a tela inicial (src/components/giro-menu.tsx + CSS no fim de src/styles.css, tudo dentro de `.gm`).
- Jogar · Amigos · Configurações · Perfil · Sair.
- Troquei os restos de azul (hover, abas, interruptores, botão principal) pela paleta verde e bege, e o texto do botão ativo ficou escuro para dar contraste.
- "Nickname" virou "Username" (minúsculas, números, _ e -, 2 a 20 caracteres), porque ele também é o nome da sala.
- Primeira vez sem username: abre direto em Perfil com um aviso dizendo onde escrever.

## Configurações agora funcionam de verdade
- Qualidade (Baixa desliga sombras), Resolução, FPS (30 a 120), Reduzir efeitos, Economia de bateria (1x de resolução, 30 FPS, sem sombras).
- Modo de tela: Tela cheia/Sem borda pedem tela cheia; Janela sai dela. iPhone não tem tela cheia no Safari.
- Áudio: volume geral, música e efeitos; zero em tudo = mudo.
- Controle: Toque (botões na tela), Teclado, Gamepad (analógico anda, A pula, B corre, X fala, Y centraliza câmera, Start pausa, analógico direito gira a câmera). Sensibilidade, zona morta, inverter eixo vertical.

## Amigos
- Tela "Amigos": campo de username, "Abrir minha sala", "Convidar por link" (compartilha ou copia `?sala=username`), adicionar amigo por username, lista com bolinha verde quando a sala dele está aberta, Entrar e remover.
- Abrir o link de convite mostra "Entrar na sala de @fulano" em Jogar.
- /api/rtc ganhou `?peek=1`, que só conta quem está na sala (usado na bolinha verde).

## Desafios em grupo (src/game/challenges.ts)
6 missões, em dupla ou trio ou sozinho. O progresso é compartilhado entre todos da sala:
1. Cartas ao vento: 8 cartas (azul anda, amarela pulinho, vermelha pulo cheio).
2. Corrida do carteiro: 5 anéis em 55 s. Qualquer um do grupo vale.
3. Balões altos: 10 balões, pulos no tempo certo.
4. Todos no farol: todo mundo junto 8 s. Se alguém sair, zera.
5. Estrelas saltitantes: 6 estrelas que mudam de lugar a cada 8 s, 75 s para pegar todas.
6. A grande volta: 6 anéis pelo planeta em 50 s.
Tempo esgotado: tenta de novo sozinho. Quem entra no meio pega a missão do grupo.
O estado viaja pelo canal confiável do WebRTC, junta tudo e repete a cada 2,5 s. Os cronômetros usam o relógio do celular, então deixe a hora em automático.
A História do Giro (7 entregas, solo) continua no menu, com save próprio.

## Do v2 anterior
Botões de pular/andar/câmera, boneco com cabeça corrigida, sombras, correções de missão da história, service worker para abrir sem internet.
