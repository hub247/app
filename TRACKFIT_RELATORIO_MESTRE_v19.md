# RELATÓRIO MESTRE DE CONTINUIDADE — TRACKFIT v19

## 1. Regra de continuidade
- Fonte técnica e visual: `index.html` da v17.
- Evoluir sempre incrementalmente. Não reconstruir o TrackFit simplificado.
- Preservar o layout herdado da v13 e consolidado até a v17.
- Persistência principal: `localStorage` na chave `gymwp.v1`. Não trocar essa chave.
- Perfis: Thiago em azul e Natália em rosa. Mavi aparece somente na Nutrição.
- Todo novo campo persistente deve entrar também na sanitização, backup e importação.

## 2. Estrutura de arquivos
- `index.html`: app completo, CSS, dados, regras e JavaScript.
- `manifest.json`: instalação PWA. v17 solicita `portrait-primary`.
- `sw.js`: cache offline e notificações.
- `icon.svg`: ícone do app. Se não estiver no pacote recebido, deve ser mantido do repositório atual.
- `README.md`: implantação.
- `assets/audio-fim-treino.mp3`: áudio real do gongo, colocado pelo usuário.
- `assets/COLOQUE-O-AUDIO-AQUI.txt`: instrução do nome/caminho do MP3.

## 3. Layout oficial
- Mobile-first, largura principal ~448 px.
- Fundo #121318, cards escuros, cantos arredondados e alto contraste.
- Cabeçalho sticky/translúcido e navegação inferior fixa.
- Thiago: azul institucional do app. Natália: rosa.
- Botões grandes para treino com uma mão.
- Principais classes: `.hdr`, `.sbar`, `.card`, `.btn`, `.seg`, `.bot`, `.frest`, `.rp`, `.qp`, `.serie`, `.meal`, `.sitem`.
- Uso prioritário em retrato. Manifest solicita portrait; se o Safari ignorar o bloqueio, a interface continua projetada para vertical.

## 4. Navegação
1. Início
2. Treinos
3. Cardio
4. Evolução
5. Nutrição
6. Mais

Telas internas: ficha do dia, exercício, timer, treino concluído, métricas e modais.

## 5. Musculação
### Fichas
- Thiago: ABC 2x. A = peito/ombro/tríceps/abdômen; B = costas/lombar/bíceps/abdômen; C = pernas.
- Natália: segunda glúteo/posterior; terça costas/ombros/braços; quarta cardio/core; quinta quadríceps/glúteo; sexta peito/costas/braços; sábado corpo inteiro.

### Fluxo
- Iniciar treino cria sessão persistente.
- Exercício por vez com todas as séries visíveis.
- Carga, concluir série, pergunta obrigatória de repetições, descanso e progressão.
- Última série: primeiro recomendação Aumentar/Manter/Reduzir, depois descanso já em andamento.
- Popup de descanso deve deixar nítido o próximo exercício/série, carga e faixa de repetições.

### Cargas persistentes
- Carga digitada é salva no aparelho.
- A carga usada no próximo treino é a mesma fonte consultada por execução e ficha.
- Edição externa deve existir em Treinos.
- Aceitar aumento/redução atualiza carga planejada futura, sem alterar histórico realizado.
- Histórico continua fiel ao peso efetivamente executado.
- Conceitos separados: realizado, carga atual e sugestão.

### Progressão
- Aumentar: topo da faixa em todas as séries.
- Manter: dentro da faixa, sem condição de aumento/redução.
- Reduzir: série abaixo do limite inferior considerando margem.
- Peso livre: saltos ~2 kg. Máquina: 5 kg até 30 kg, depois 10 kg.
- Manter usa banco de mensagens motivacionais.
- Cores: aumentar verde, manter amarelo, reduzir vermelho.

## 6. Descanso, timer e áudio
### Descanso
- Inicia ao concluir série.
- Ao atingir 00:00, se o usuário ainda não confirmou a próxima série, continua em vermelho como +00:01, +00:02 etc.
- O excedente existe somente até `Bora para a próxima`.
- `Bora` encerra completamente o timer.
- `Pular descanso` encerra imediatamente e não inicia excedente vermelho.

### Áudio oficial
- Caminho: `assets/audio-fim-treino.mp3`.
- App aberto: tocar gongo e vibração; não criar notificação de término.
- Segundo plano: tentar tocar gongo e, se oculto, emitir notificação de término.
- Áudio sintético serve como fallback se MP3 não carregar/for bloqueado.
- Tentar coexistir com Spotify/Apple Music/YouTube sem interromper música externa.
- Safari/iOS pode suspender JavaScript do PWA. Não é possível garantir MP3 em segundo plano quando a página está totalmente suspensa; a notificação do sistema é o fallback nesse cenário.

## 7. Exercícios por tempo
Ex.: prancha.
- Botão `Iniciar exercício`.
- Preparação regressiva de 10 s usando o gongo como sinal de preparação/início.
- Depois, cronômetro progressivo.
- Só encerra por ação do usuário.
- Tempo real é gravado em cada série.
- Entre séries entra descanso normal.
- Meta de tempo: margem ±10 s.
- Se todas as séries superarem meta +10 s de forma consistente, sugerir +10 s na meta futura.
- Dentro da margem: manter.
- Abaixo de meta -10 s: manter/ajustar para consolidar.
- Descanso só deve ser aumentado se a queda entre séries indicar recuperação insuficiente. Alterar uma variável por vez.

## 8. Tempo do treino
- `Tempo total`: do início até Finalizar Treino, incluindo séries, descansos, perguntas, troca de aparelhos e intervalos.
- Registrar também `execução` e `descanso` quando disponível.
- Compartilhamento e Evolução devem priorizar tempo total e detalhar execução/descanso.

## 9. Cardio GPS livre
- Corrida, caminhada e bike.
- GPS, precisão, distância, duração, splits, pace/velocidade, calorias, histórico e recordes.
- Pausa e retomada persistentes.
- Estado `cardioLive` deve sobreviver a refresh/suspensão.
- Checkpoint ao pausar, a cada atualização útil de GPS, `visibilitychange` e `pagehide`.
- Se retomado após interrupção, não inventar trajeto GPS ausente.
- Compartilhamento: minimalista, médio e tela cheia.

## 10. Cardio prescrito na ficha
- Botão chama-se `Iniciar Cardio`.
- Cronômetro de atividade e botão explícito `Finalizar Cardio`.
- Após finalizar, avaliação adaptativa: corrida contínua, caminhada leve/rápida, corrida+caminhada, HIIT, bike contínua/intervalada, mobilidade/outro.
- Perguntas possíveis: tempo, distância, velocidade, inclinação, esforço percebido, capacidade restante.
- HIIT: tiros, tempo rápido, recuperação, velocidade rápida/lenta e percepção final.
- Progressão altera uma variável por vez: primeiro duração quando confortável; depois velocidade; HIIT pode reduzir recuperação antes de subir outras variáveis.
- Muito forte/quase falhou: manter ou ajustar para baixo, não progredir.

## 11. Evolução
Períodos: Semana, Mês, Trimestre, Semestre e Ano.
- Corpo: peso, cintura, variação e gráfico.
- Musculação: frequência, volume, cargas, 1RM Epley, progressões e histórico.
- Cardio: atividades, tempo, distância, pace, velocidade e recordes.
- Semana: relatório detalhado e comparação com semana anterior.
- Dois compartilhamentos: `Compartilhar relatório` e `Compartilhar para análise`, com períodos predefinidos ou personalizados.
- Dados de tempo do treino devem separar total e, quando registrados, execução/descanso.

## 12. Nutrição
- Fonte alimentar consolidada anteriormente: Plano_Alimentar_Familia_v5.xlsx.
- Porções caseiras são padrão; peso exato é alternativa.
- Thiago 2.290 kcal / 155 g proteína. Natália 1.630 kcal / 104 g proteína.
- Mavi tem cardápio/preparo próprio, sem meta calórica infantil no app.
- Refeição adulta: Conforme plano / Comi diferente / alimento extra.
- Valores reais substituem planejados no consumido diário quando o usuário informa refeição diferente.

### Home e pendências
- A Home deve permitir marcar a refeição diretamente.
- Marcada = desaparece da Home e entra no cálculo diário.
- Quando chega o horário sem confirmação: estado `Pendente` por 30 min.
- Após 30 min, sai da Home, mas continua pendente em Nutrição.
- No dia seguinte, pendências do dia anterior devem poder ser revisadas; não assumir que ausência de resposta = refeição não realizada.
- Pendências antigas não devem bloquear indefinidamente o uso do app.

## 13. Compras e despensa
- Primeira compra pode ser apresentada em embalagens comerciais: pacote de arroz, bandeja de ovos, latas, kg de carne etc.
- Compra seguinte deve considerar estoque remanescente.
- Regra conceitual: `necessidade da semana - estoque informado = compra recomendada`.
- Usuário informa saldo doméstico (ex.: 0,5 pacote, 6 ovos, 1 lata, ~500 g).
- Não presumir consumo perfeito só com base no plano; reconciliar estoque antes da compra.
- Checks de compra devem salvar imediatamente.

## 14. Persistência e restauração
Regra transversal: qualquer informação que o usuário não queira preencher novamente deve ser persistida imediatamente.
- cargas;
- séries/reps;
- timer;
- sessão;
- cardio e pausa;
- refeições;
- extras;
- compras;
- estoque;
- progressões;
- preferências.

Eventos críticos devem executar checkpoint: `visibilitychange`, `pagehide`, pausa de cardio, compartilhamentos/saídas externas quando possível.

## 15. Backup
Preservar `gymwp.v1`. Backup JSON deve incluir campos existentes e novos, incluindo cargas oficiais, cardio prescrito, refeições reais, extras e demais estados persistentes. Sanitizar importação.

## 16. Service worker/PWA
- Cache da versão deve ser atualizado a cada entrega.
- v17 usa cache `trackfit-v17`.
- Arquivos públicos devem ficar no mesmo nível, com subpasta `assets`.
- Orientação solicitada no manifest: `portrait-primary`; Safari/iOS pode não respeitar lock programático em todos os contextos.

## 17. Checklist de teste v17+
- Validar JS com `node --check`.
- Validar ZIP com `unzip -t`.
- Testar gongo com app aberto e em segundo plano.
- Testar música externa tocando junto.
- Testar notificação apenas quando app estiver fora de foco.
- Testar 00:00 → excedente → Bora e Pular.
- Testar carga digitada, recomendação e edição via Treinos após recarregar página.
- Testar próximo exercício/carga no descanso.
- Testar prancha/exercício por tempo.
- Testar Cardio prescrito e Cardio GPS com pausa longa e retorno.
- Testar tempo total do treino.
- Testar check de refeição na Home e pendências.
- Testar compras, estoque e persistência de checks após sair do app.
- Testar exportação/importação de backup.

## 18. Prompt de retomada
> Use o ZIP anexado como base oficial. Leia primeiro o RELATÓRIO MESTRE. Preserve integralmente layout, arquitetura, chave gymwp.v1, fichas, Nutrição, histórico e funcionalidades. Faça somente os novos ajustes solicitados, de maneira incremental. O index.html mais recente é a verdade técnica/visual e este relatório é a verdade das decisões de produto. Valide JavaScript, ZIP, cache e persistência antes de entregar a nova versão. Atualize novamente este relatório ao final.

---
# ATUALIZAÇÃO CONSOLIDADA — TRACKFIT v18

## Dados externos
A v18 separa arquivos editáveis e snapshots web:
- `dados/plano-alimentar/plano-alimentar-trackfit.xlsx`: fonte editável do plano.
- `dados/plano-alimentar/plano-alimentar.json`: snapshot lido pelo navegador.
- `dados/banco-alimentos/banco-alimentos-200.xlsx`: banco editável com 200 alimentos.
- `dados/banco-alimentos/banco-alimentos.json`: snapshot lido pelo navegador.
- `assets/audio-fim-treino.mp3`: áudio oficial inserido pelo usuário.

O app valida schemas `trackfit.nutrition.v1` e `trackfit.foods.v1`, tenta baixar dados atuais e mantém cache local válido. Nesta versão estática em GitHub Pages, alterar apenas o XLSX não atualiza o JSON automaticamente. É necessário regenerar o snapshot JSON ou implementar Microsoft Graph em evolução posterior.

## Construtor de refeições
- Botão `+ Montar refeição` em Nutrição.
- Busca em 200 alimentos e filtro por categoria.
- Quantidade editável em gramas, com porção caseira exibida.
- Cálculo em tempo real de kcal, proteína, carboidrato, gordura e fibra.
- Salvar refeição consumida no `gymwp.v1`.
- Refeição montada entra imediatamente no total diário.
- Cada item salva uma fotografia nutricional para impedir mudança retroativa do histórico.
- `Trocar/montar` substitui o valor planejado pelo valor real da refeição montada.
- Favoritas reutilizáveis.
- Recentes persistentes.
- Cadastro de alimento personalizado por rótulo com IDs `USR-001` em diante.

## Regra de histórico
O Excel/JSON controla o plano atual. O `gymwp.v1` controla o realizado. Sincronizar uma nova versão do plano ou do banco nunca deve recalcular registros antigos.

## Publicação
Preservar exatamente as pastas `assets/` e `dados/`. Atualizar cache do service worker ao mudar snapshots. Validar o JSON antes de substituir o cache local.

**Fonte oficial após esta entrega:** `trackfit-v18.zip`, `trackfit-v18-index.html` e `TRACKFIT_RELATORIO_MESTRE_v18.md`.


## ATUALIZAÇÃO CONSOLIDADA — TRACKFIT v19

### Base preservada
- Evolução incremental sobre o `index.html` da v18.
- Layout, arquitetura, fichas, Nutrição e chave `gymwp.v1` preservados.
- Dados externos e snapshots JSON mantidos sem alteração de histórico.

### 11 ajustes consolidados
1. Timer, persistência e aviso preparados para retorno do segundo plano.
2. Contagem sonora oficial iniciada nos últimos 10 segundos.
3. Sequência sem sobreposição: preparação, contagem e início.
4. Estado vermelho é encerrado ao começar a próxima série.
5. O botão Bora encerra completamente o atraso positivo.
6. Manifesto em `portrait-primary` e orientação visual para retrato.
7. Controle de carga com botões circulares de incremento e redução.
8. Próxima série/exercício destacada durante o descanso.
9. Progressão específica para cardio e exercícios por tempo preservada.
10. Modo Foco acionável na tela do exercício e persistido no aparelho.
11. Lembretes de refeições permanecem configuráveis pelos horários do plano.

### Áudios oficiais v19
- `assets/preparacao-para-o-treino.mp3`
- `assets/audio-fim-treino.mp3`
- `assets/audio-iniciar-treino.mp3`

O áudio de preparação é antecipado conforme a duração detectada no arquivo. Aos 10 segundos inicia `audio-fim-treino.mp3`. Em 00:00 inicia `audio-iniciar-treino.mp3`. Ao pular, tocar em Bora ou iniciar outro descanso, a sequência anterior é interrompida para evitar sobreposição.

### Limitação técnica mantida
Em Safari/iOS, o sistema pode suspender JavaScript e áudio quando o PWA fica totalmente congelado. O app salva o timer e tenta emitir notificação quando há permissão, mas áudio contínuo em segundo plano não pode ser garantido por uma página web.

### Checklist v19
- Validar JavaScript com `node --check`.
- Validar ZIP com `unzip -t`.
- Colocar os três MP3s em `assets/` antes da publicação.
- Testar a sequência em descansos de 45, 60, 90 e 120 segundos.
- Testar 00:00 → atraso → Bora e confirmar que o vermelho encerra.
- Testar Modo Foco, recarga da página e retorno ao modo normal.
- Testar cargas, histórico, Nutrição, lembretes, cardio e backup.

**Fonte oficial após esta entrega:** `trackfit-v19.zip`, `trackfit-v19-index.html` e `TRACKFIT_RELATORIO_MESTRE_v19.md`.
