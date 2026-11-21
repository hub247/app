# RELATORIO MESTRE DE CONTINUIDADE — TRACKFIT v24.5

## Base oficial
- Base tecnica: v23-TELA2-AJUSTADA enviada em 19/11/2026.
- Preservar arquitetura existente e localStorage `gymwp.v1`.
- Telas 1 (Home) e 2 (Treinos) sao a base visual validada e devem evoluir incrementalmente.

## Design System
- Mockup premium TrackFit continua como referencia visual obrigatoria.
- Fundo #061014; cards #0D1B22; bordas #26414F; verde #00E56B; azul #288CFF; laranja #FF7A17; vermelho #EE414D.

## Anatomia realista v24.1
- E proibido substituir os mapas por boneco geometrico simplificado.
- Assets ficam em `assets/anatomia/`.
- Verde = principal; azul = secundario; cinza = demais regioes.
- Home seleciona imagem pela ficha do dia.
- Tela Treinos seleciona imagem por cada ficha.
- Ficha completa usa mapa anatomico da ficha.
- Tela de exercicio usa mapa especifico pelo nome e pelos musculos cadastrados no exercicio.
- Modo Foco usa mapa do exercicio atual e miniatura do proximo exercicio.
- Regras atuais cobrem push, pull, pernas, peito superior/triceps, peito/triceps, ombros, costas/biceps, biceps, triceps, quadriceps/gluteos, posterior/gluteos, panturrilhas, core e lombar/gluteos.
- `assets/anatomia/anatomia-map.json` documenta os assets e palavras-chave.

## Fichas Thiago
- A: Peito, Ombros, Triceps e Abdomen -> push.
- B: Costas, Lombar, Biceps e Abdomen -> pull.
- C: Quadriceps, Gluteos, Posterior e Panturrilha -> pernas.

## Exercicios por tempo
- Meta e referencia, nunca limite.
- Iniciar serie -> 10s preparacao -> cronometro progressivo ilimitado -> Encerrar Serie -> salva tempo -> conclui serie -> descanso automatico.
- Progressao por consistencia: meta 60s e todas as series >=70s permite sugerir 70s; se nao consolidar, manter; queda relevante permite ajuste conservador.

## Audios oficiais
- `assets/preparacao-para-o-treino.mp3`
- `assets/audio-fim-treino.mp3`
- `assets/audio-iniciar-treino.mp3`
- Ordem fixa: preparacao -> contagem dos ultimos 10s -> iniciar treino. Sem sobreposicao.

## Persistencia
- Manter chave `gymwp.v1`.
- Preservar historico, cargas, progressao, timers, cardio, nutricao, compras, backup e configuracoes.

## Arquivos principais
- `index.html`
- `manifest.json`
- `sw.js`
- `assets/anatomia/*`
- `assets/profile-thiago.png`

## Validacao obrigatoria em futuras versoes
1. `node --check` no JavaScript.
2. `unzip -t` no pacote.
3. Testar Home A/B/C e confirmar imagem correta.
4. Testar Treinos A/B/C e confirmar imagem correta.
5. Abrir exercicios de peito, costas, biceps, triceps, quadriceps, posterior, panturrilha, core e lombar e conferir a imagem correspondente.
6. Testar Modo Foco e proximo exercicio.
7. Confirmar que nenhum boneco SVG geometrico reapareceu nas telas com anatomia.


### Refinamentos v24.2
- Miniaturas anatômicas dos cards aumentadas em aproximadamente 25% e assets recortados para reduzir margens brancas.
- Cards de treino ampliados apenas o necessário para preservar legibilidade.
- Estimativa de duração recalculada por séries, tempo médio de execução e descansos; histórico inválido abaixo de 10 minutos é ignorado.
- Quando há histórico válido, a previsão combina 65% do cálculo técnico e 35% da média dos últimos três treinos.
- Descanso recolhido compactado e posicionado acima da navegação, sem cobrir o rodapé.
- Cache oficial: trackfit-v24-2-refinamentos.


#### Ajuste v24.3 — anatomia integrada ao tema escuro
- Removido o fundo branco programático dos containers anatômicos da Home e da tela Treinos.
- Miniaturas passam a usar fundo transparente, preservando o fundo escuro do próprio card.
- Imagens anatômicas devem ser fornecidas como PNG RGBA ou WebP com canal alpha real.
- object-fit dos cards alterado para contain para evitar recortes artificiais e retângulos claros.
- Cache oficial atualizado para trackfit-v24-3-transparente.
- Persistência gymwp.v1 e toda a lógica funcional foram preservadas.


#### v24.5 — correção dos assets anatômicos
- Corrigido erro da v24.4 que repetia a prancha completa em cada miniatura.
- Gerados 14 arquivos anatômicos individuais em assets/anatomia/.
- Cada miniatura contém somente o mapa correspondente à ficha ou grupo muscular.
- Removidos títulos/legendas da imagem e aplicado recorte dedicado 360x480.
- Fundo claro removido para transparência e integração com cards escuros.
- Cache: trackfit-v24-5-assets-individuais.
- gymwp.v1 preservado.


##### v24.7.1 — recuperação da Tela 3
- Corrigida tela vazia ao abrir index.html.
- Em vez de substituir grande bloco funcional, a Tela 3 reutiliza focusScreen, composição já existente e validada na base v24.5.
- Home, Treinos, nutrição, cardio, evolução e persistência permanecem da base original.
- gymwp.v1 preservado.
- Cache atualizado: trackfit-v24-7-1-tela3.


##### v24.7.3 — fidelidade final da Tela 3
- Anatomia do exercício atual ampliada e miniatura do próximo ampliada.
- Vídeo continua condicionado ao cadastro já existente.
- Controles de série/carga/repetições ampliados.
- Descanso padronizado e ampliado nos modos Normal e Foco: anel 82px, tempo 42px, -15s, Pausar, +15s e Pular descanso.
- Próximo exercício passa a exibir músculos, séries/repetições, próxima carga quando disponível e descanso.
- Modo normal mantém navegação e recebe botão explícito MODO FOCO / TELA CHEIA.
- Layout permite rolagem vertical em vez de comprimir cards.
- 14 assets anatômicos, anatomia-map, perfis e gymwp.v1 preservados.
- Cache: trackfit-v24-7-3-tela3-fiel.


##### v24.7.4 — Tela 3 fiel ao mockup
- Anatomia do exercício atual ampliada para ~86x94 px e próximo exercício para ~72x80 px.
- Botão Ver vídeo permanece visível quando existir vídeo cadastrado.
- Controle de carga preserva - / valor / + e usa DEFINIR quando ainda não há carga.
- Último registro prioriza carga e repetições quando disponíveis.
- Painel de descanso ampliado: anel 88 px, contador 44 px e controles maiores.
- Próximo exercício e fila Depois disso receberam hierarquia, carga quando disponível e melhor legibilidade.
- Cabeçalho e tipografia da Tela Normal ampliados.
- Scroll vertical liberado para evitar compressão dos cards.
- Modo Foco compartilha exatamente o mesmo estado funcional.
- gymwp.v1 e os 14 assets anatômicos preservados.


##### v24.7.5 — correção cirúrgica da Tela 3
- CSS refeito sobre a estrutura real do focusScreen, removendo o conflito que impedia anatomias de crescer.
- Exercício atual: anatomia 92x100px, tipografia maior e card sem vazio residual.
- Vídeo aparece quando houver cadastro de vídeo para o exercício.
- Carga recebe controles - / DEFINIR ou valor / +.
- Última série prioriza carga e repetições, com data apenas como fallback.
- Descanso ampliado: anel 90px, tempo 46px, botões maiores e estado Aguardar antes de iniciar.
- Próximo exercício: anatomia 74x82px, músculos, carga e descanso.
- Depois disso: número circular, séries/repetições e carga quando disponível.
- Cabeçalho, tipografia e espaçamentos expandidos, com scroll vertical.
- Normal e Foco continuam compartilhando a mesma sessão e gymwp.v1.


##### v24.7.6 — correção de tela vazia
- Corrigido ReferenceError em focusScreen: a variável hasV era usada no template sem ser declarada.
- hasV agora é calculada a partir do vídeo cadastrado do exercício antes da renderização.
- Layout e ajustes visuais da v24.7.5 preservados.
- Cache atualizado para trackfit-v24-7-6-runtime-fix.
- gymwp.v1 e assets preservados.


##### v24.7.7 — polimento seguro da Tela 3
- Alterações limitadas a CSS e identidade de versão; nenhuma lógica central do treino foi reescrita.
- Anatomia do exercício atual e próximo exercício ampliadas.
- Cabeçalho e perfil ampliados na tela normal.
- Cards recebem mais respiro vertical e scroll permanece liberado.
- Descanso ampliado mantendo o mesmo timer/estado funcional já validado.
- Modo Foco recebe escala visual maior e mantém a mesma sessão.
- gymwp.v1, timers, séries, carga e 14 assets anatômicos preservados.

###### v24.7.8 - descanso dual por modo
- Tela normal: card laranja ocultado; frest recolhido e rp expandido preservados.
- Ao concluir serie, popup abre automaticamente e pode ser recolhido sem parar o timer.
- Modo Foco: frest e rp ocultos; somente o card laranja permanece.
- Alternar Normal/Foco preserva o mesmo timer T.
- Ao sair do Foco durante descanso, o cronometro reaparece recolhido.
- Anatomias e fila receberam refinamento final de escala/espacamento.
- gymwp.v1 preservado.


###### v24.7.9 — barra global de treino em andamento
- Barra de sessão ativa centralizada no render global e exibida em todas as telas fora da própria Tela 3 e da tela de conclusão.
- Removida a injeção da barra dentro de hdr para evitar duplicidade entre telas.
- Nome do treino e cronômetro passam a ser clicáveis e retornam diretamente para exercicio, preservando S.ui.exIdx, timer, séries e cargas.
- Pausar/Retomar e Finalizar permanecem ações independentes na mesma barra.
- Navegar por Home, Treinos, Cardio, Evolução, Nutrição e Mais não perde mais o caminho de retorno ao treino ativo.
- gymwp.v1 e descanso dual da v24.7.8 preservados.
- Cache: trackfit-v24-7-9-sessao-global.


## TRACKFIT v24.8.0 — CONSOLIDACAO VISUAL GLOBAL

### JA CONCLUIDO / PRESERVAR
- Home premium, Treinos, Tela 3 normal, Modo Foco, anatomias individuais transparentes e sessao global.
- Descanso dual: popup normal e card laranja no Modo Foco.
- Barra TREINO EM ANDAMENTO global, clicavel, retornando ao exercicio atual.
- gymwp.v1 permanece a chave oficial de persistencia.
- 14 mapas em assets/anatomia/ e anatomia-map.json.
- Nutrição, cardio, evolução, compras, timers e progressao preservam logica existente.

### AJUSTES VISUAIS APLICADOS NESTA v24.8.0
- Design System global aplicado a cards, botoes, tabs, bordas, raios, cores e espacamento.
- Cardio recebeu hierarquia visual premium, painel ativo, metricas e botoes refinados.
- Nutrição recebeu cards/tabs/refeicoes/macros alinhados ao novo tema.
- Evolução recebeu KPIs e areas de grafico alinhados ao tema.
- Treinos/plano receberam cards e anatomias maiores.
- Barra global de sessao e navegacao receberam acabamento consistente.
- Nenhuma funcao central dessas areas foi reescrita: alteracoes desta fase sao predominantemente de CSS.

### TELAS / FLUXOS AINDA A VALIDAR VISUALMENTE COM THIAGO
1. Cardio livre/prescrito durante uma sessao real e foto final para compartilhamento.
2. Nutrição Hoje/Semana/Compras/Preparo em dados reais.
3. Montar Refeição e seletor de quantidade em uso real.
4. Evolução: Visao Geral/Treino/Cardio/Nutrição com historico real.
5. Compras: lista/despensa/historico com base nutricional completa.
6. Progressão de carga circular e exercicios por tempo devem manter regras funcionais ja consolidadas; falta somente validacao visual final.
7. Mais/notificações/onboarding e estados vazios ainda precisam de revisão visual final.

### REGRA PARA PROXIMAS VERSOES
- Evoluir incrementalmente sobre esta base.
- Nao reconstruir arquitetura.
- Preservar gymwp.v1 e compatibilidade com os dados atuais.
- Validar cada tela por print antes de alterar a proxima.
- Cache oficial desta versao: trackfit-v24-8-0-redesign-global.

## CONSOLIDACAO FINAL DOS ARQUIVOS RECEBIDOS
- Pacote recomposto a partir da v24.8.0 REDESIGN GLOBAL e dos arquivos finais enviados por Thiago.
- index.html, manifest.json e sw.js: base v24.8.0 mantida.
- assets/anatomia/: 14 mapas oficiais + anatomia-map.json confirmados.
- assets/profile-thiago.png, assets/profile-natalia.png e assets/home-anatomy.png confirmados.
- dados/plano-alimentar/plano-alimentar.json e dados/banco-alimentos/banco-alimentos.json confirmados conforme os arquivos recebidos.
- README de audios e instrução COLOQUE-O-AUDIO-AQUI incluídos. Os MP3 não foram recebidos nesta consolidação; o fallback sintético já documentado continua sendo a referência quando aplicável.
- A chave gymwp.v1, sessão global de treino, retorno para a Tela 3, descanso dual, Modo Foco, timers e arquitetura existente devem permanecer preservados nas próximas versões.
- Próxima etapa recomendada: validar visualmente, uma tela por vez, Cardio, Nutrição, Montar Refeição, seletor de quantidade, Evolução, Compras, progressão circular, exercícios por tempo, Mais/notificações/onboarding.


## v24.8.1 — IDENTIDADE VISUAL DO PERFIL NATÁLIA
- O perfil Natália agora usa assets/profile-natalia.png na Home e no seletor de perfis.
- Cabeçalhos de treino e plano passam a usar a foto do perfil ativo (Thiago ou Natália).
- Perfil Thiago mantém identidade verde oficial.
- Perfil Natália passa a aplicar identidade rosa (#ff5fa2) nos elementos de identidade/ação apropriados.
- O "Fit" da marca TrackFit fica rosa no perfil Natália e continua verde no perfil Thiago.
- Alteração feita por classe visual profile-natalia, sincronizada no render(), sem mudar chaves ou estrutura de dados.
- gymwp.v1, sessões, treinos, cargas, históricos, timers, descanso dual e barra global permanecem preservados.
- Cache: trackfit-v24-8-1-perfil-natalia-rosa.


### v24.8.2 — PROGRESSÃO, TREINOS EDITÁVEIS E EVOLUÇÃO
- Base preservada: v24.8.1, chave `gymwp.v1` mantida.
- Aba Treinos recebeu editor persistente por exercício para séries, repetições/meta, carga planejada e descanso.
- Nova estrutura `exerciseCfg` fica dentro de `gymwp.v1` e é compartilhada por Treinos, execução e Modo Foco.
- Alteração de carga planejada não reescreve o histórico já realizado.
- Progressão conquistada não aplica salto fixo. Abre seletor circular com marcador arrastável e botões −/+.
- Exercícios com carga: escolha manual de +1 a +5 kg, passo de 0,5 kg.
- Exercícios só de repetições: escolha manual de +1 a +5 repetições.
- Exercícios de peso corporal que podem receber carga: quando consolidado, passam a permitir adicionar 1–5 kg.
- Exercícios exclusivamente por tempo: 10 s de preparação -> cronômetro progressivo ilimitado -> Encerrar Série -> registra tempo -> conclui série -> descanso automático.
- Na progressão por tempo o seletor controla o acréscimo em segundos; a meta permanece referência, nunca limite do cronômetro.
- Tela Evolução recebeu compactação visual, hierarquia e seções alinhadas ao Design System premium.
- Estimativa calórica da musculação passa a segmentar execução ativa e períodos de descanso/transição, evitando aplicar um único MET ao tempo total da sessão.
- Identidades preservadas: Thiago verde; Natália rosa, incluindo `Fit` rosa e avatar `assets/profile-natalia.png`.
- Safe Areas superior/inferior preservadas para iPhone/PWA.
- Cache oficial: `trackfit-v24-8-2-progressao-e-evolucao`.

#### Checklist obrigatório
1. Abrir Thiago e Natália e confirmar fotos/cores.
2. Em Treinos > Editar Treinos, alterar carga e reps e confirmar reflexo na execução.
3. Concluir todas as séries de um exercício com critério de progressão e testar dial arrastável e −/+.
4. Confirmar +1 a +5 kg e persistência no próximo treino.
5. Testar exercício só de reps e progressão de reps.
6. Testar prancha: preparação 10 s, relógio crescente sem limite, Encerrar Série e descanso automático.
7. Confirmar que histórico anterior não muda ao aceitar progressão.
8. Abrir Evolução com e sem histórico.
9. `node --check` no JavaScript.
10. `unzip -t` no pacote final.
