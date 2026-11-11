# RELATÓRIO MESTRE DE CONTINUIDADE — TRACKFIT v15

## Finalidade
Este documento é a memória oficial do projeto. Em toda nova edição, usar o ZIP mais recente como fonte do código e este relatório como fonte das decisões de produto, layout e regras de negócio. Nunca reconstruir o TrackFit de forma simplificada.

## Arquivos oficiais
- `trackfit-v15.zip`: pacote publicável completo.
- `trackfit-v15-index.html`: aplicativo em arquivo único.
- `TRACKFIT_RELATORIO_MESTRE_v15.md`: este relatório.
- `Plano_Alimentar_Familia_v5.xlsx`: fonte da Nutrição, quando houver atualização.

O pacote publicável contém `index.html`, `manifest.json`, `sw.js`, `icon.svg`, `README.md` e este relatório.

## Regra de continuidade
1. Preservar a chave de armazenamento `gymwp.v1` para não perder dados locais.
2. Editar incrementalmente o último `index.html` oficial.
3. Não trocar o layout, as fichas, os dados ou os fluxos que não foram solicitados.
4. Atualizar sanitização, backup, service worker e README quando novos campos forem criados.
5. Não inventar alimentação, preços, medidas caseiras ou explicações de resultados.

---

# 1. Arquitetura e layout

- PWA mobile-first para GitHub Pages.
- HTML único com CSS e JavaScript incorporados.
- Largura principal próxima de 448 px.
- Fundo escuro, cards arredondados, bordas discretas, cabeçalho translúcido e navegação inferior fixa.
- Botões grandes e legíveis para uso durante o treino.
- Perfil Thiago usa azul; perfil Natália usa rosa.
- O perfil ativo altera tema, ficha, histórico, métricas e Nutrição.
- Mavi existe dentro de Nutrição, não como perfil de treino.

Componentes visuais importantes:
- `.hdr`: cabeçalho.
- `.sbar`: treino em andamento.
- `.card`: card padrão.
- `.btn`: botão padrão.
- `.seg`: seletor segmentado.
- `.bot`: navegação inferior.
- `.frest`: descanso recolhido.
- `.rp`: popup do descanso.
- `.qp`: pergunta obrigatória de repetições.
- `.modal` e `.sheet`: janelas inferiores.
- `.serie`: séries do exercício.
- `.meal`: refeição.
- `.sitem`: item de compra.

# 2. Navegação principal

A v15 possui seis áreas:
1. Início.
2. Treinos.
3. Cardio.
4. Evolução.
5. Nutrição.
6. Mais.

Telas internas: ficha do dia, exercício individual, timer, treino concluído, métricas e modais.

# 3. Tela inicial

Preservar:
- seletor Thiago/Natália;
- saudação, data e frase diária;
- próximas refeições do adulto e da Mavi;
- treino do dia;
- escolha de outro treino;
- dias treinados na semana;
- treinos do mês;
- evolução de carga em 30 dias;
- peso atual e acesso ao histórico.

# 4. Musculação

## Thiago
- ABC 2x, segunda a sábado.
- A: peito, ombros, tríceps e abdômen.
- B: costas, lombar, bíceps e abdômen.
- C: pernas.

## Natália
- Segunda: glúteo e posterior.
- Terça: costas, ombros e braços.
- Quarta: cardio e core.
- Quinta: quadríceps e glúteo.
- Sexta: peito, costas e braços.
- Sábado: corpo inteiro.

## Fluxo de série
1. Informar carga.
2. Concluir série.
3. Descanso começa imediatamente.
4. Perguntar repetições.
5. Na última série, abrir popup exclusivo Aumentar/Manter/Reduzir.
6. Descanso continua correndo por trás dos popups.
7. Aplicar a carga sugerida apenas ao próximo treino, sem alterar o registro real do treino atual.
8. Ao fechar, reabrir o descanso com o tempo restante, sem reiniciar.

## Progressão
- Aumentar: todas as séries alcançam o topo da faixa.
- Manter: desempenho dentro da faixa, sem condição de aumento ou redução.
- Reduzir: alguma série fica abaixo do mínimo menos a margem.
- Peso livre: salto aproximado de 2 kg.
- Máquina: 5 kg até 30 kg; depois 10 kg.
- Exercício sem carga: sugerir iniciar carga.
- Prancha/tempo: ajustar segundos.

## Pular exercício
O popup oferece:
- fazer após o próximo;
- deixar para o final;
- descartar somente hoje.

Descartar hoje não remove o exercício da próxima ocorrência da ficha.

## Orientação automática
- Antes de um exercício não dispensado, pode abrir vídeo e instruções.
- Checkbox “Não mostrar automaticamente novamente”.
- Como fazer e Vídeo continuam disponíveis.
- Em Mais, “Reativar todas as orientações”.

# 5. Descanso, som e avisos

- Popup circular de descanso.
- Pausar, retomar, -15 s, +15 s e pular.
- Descanso recolhido permanece clicável.
- Na v15, mostra explicitamente: “TOQUE AQUI PARA ABRIR NOVAMENTE ⌃”.
- Gongo, sino e bipe.
- Volume e vibração.
- Bipes finais.
- Notificação quando permitida.
- Em Mais, “Testar alerta agora”.
- No iOS, não prometer execução contínua se o sistema suspender completamente o PWA.

# 6. Cardio

Modalidades:
- Corrida.
- Caminhada.
- Bike.

Registros:
- duração;
- distância GPS;
- precisão;
- pace médio;
- velocidade média na bike;
- parciais por km;
- calorias estimadas;
- histórico e recordes.

GPS:
- usar `watchPosition` em HTTPS;
- alta precisão;
- filtrar pontos ruins e saltos improváveis;
- Wake Lock quando disponível;
- avisar que no Safari a tela deve ficar ligada.

Compartilhamento de Cardio:
- Minimalista.
- Médio.
- Tela cheia.
- Imagem PNG, compartilhamento nativo quando disponível e download como fallback.

# 7. Evolução

Períodos disponíveis:
- Semana.
- Mês.
- Trimestre.
- Semestre.
- Ano.

## Corpo
- peso atual e inicial;
- variação;
- gráfico;
- cintura quando registrada.

## Musculação
- treinos;
- frequência;
- tempo total e médio;
- calorias estimadas;
- volume total e médio;
- progressões;
- evolução por exercício;
- melhor série;
- recordes;
- 1RM estimado pela fórmula de Epley.

## Cardio
- atividades;
- tempo;
- distância total;
- maior distância;
- melhor pace;
- velocidade de bike.

## Semana
A opção Semana inclui relatório detalhado, comparação contra semana anterior e texto automático com treinos, tempo, volume, Cardio, pace e progressões.

## Compartilhar relatório
Resumo visual para o próprio usuário, WhatsApp ou redes sociais. Períodos:
- esta semana;
- semana anterior;
- 30 dias;
- trimestre;
- semestre;
- ano;
- personalizado.

## Compartilhar para análise
Versão com atividades detalhadas, volume, séries, Cardio, peso, progressões e exercícios pulados/descartados. Gera texto e imagem.

# 8. Nutrição

## Fonte
`Plano_Alimentar_Familia_v5.xlsx`, com quatro semanas e versões Custo médio/Custo reduzido.

## Pessoas
- Perfil Thiago: Thiago e Mavi.
- Perfil Natália: Natália e Mavi.
- Lista de compras única e compartilhada entre Thiago e Natália.

## Metas
- Thiago: 2.290 kcal e 155 g de proteína.
- Natália: 1.630 kcal e 104 g de proteína.

## Visualização v15
- Padrão: “Porção do dia a dia”.
- Exemplos: unidade, concha, colher, escumadeira, fatia, quadrado, pedaço ou porção.
- Alternativa: “Peso exato”.
- Se não houver equivalência confiável: “1 porção do plano · X g”.
- Nunca inventar medida caseira.

## Hoje
- refeições por horário;
- próxima refeição destacada;
- check de refeição;
- kcal e proteína;
- ajuste de quantidades;
- recálculo automático.

## Mavi
- horário, alimento, porção e preparo;
- separar antes de salgar/dourar;
- cuidados de textura;
- manter aviso para validação com pediatra.

## Compras
- semanas 1–4;
- grupos de mercado;
- quantidade e unidade;
- custo quando disponível;
- check compartilhado;
- WhatsApp;
- preço faltante deve ficar pendente, nunca ser inventado.

## Preparo
- sábado e domingo;
- peso cru e pronto;
- potes por pessoa e dia;
- instruções específicas da Mavi.

## Integração com atividade
- musculação + Cardio entram no gasto estimado;
- compensação configurável em 0%, 10%, 20% ou 30%;
- padrão: 10%.

# 9. Histórico, métricas e backup

Guardar:
- peso, cintura e enjoo;
- treinos, duração, volume, séries, calorias;
- cargas, repetições e progressões;
- Cardio, GPS, pace, velocidade e splits;
- Nutrição, refeições, porções e compras;
- orientações dispensadas;
- exercício adiado ou descartado;
- carga do próximo treino.

Exportações:
- CSV da evolução.
- JSON de backup.
- Importação com sanitização.

# 10. Ordem lógica do index.html

1. Cabeçalho e CSS.
2. Estrutura HTML, navegação, modais e símbolos SVG.
3. Dados das fichas.
4. Utilitários.
5. Estado, sanitização e persistência.
6. Sessão de treino.
7. Regras de carga.
8. Áudio, notificação e timer.
9. Componentes e telas.
10. Gráficos.
11. Cardio.
12. Evolução e relatórios.
13. Métricas e modais.
14. Compartilhamentos.
15. Dados e telas de Nutrição.
16. Tutorial.
17. Navegação e eventos.
18. Inicialização e service worker.

# 11. Checklist para qualquer v16+

Antes:
- anexar o ZIP mais recente;
- anexar este relatório;
- anexar a planilha se houver alteração de Nutrição;
- usar o index do ZIP como base;
- preservar `gymwp.v1`.

Durante:
- mudanças incrementais;
- não alterar outras áreas;
- preservar azul/rosa;
- atualizar sanitização e backup;
- não inventar dados;
- não reiniciar timers ao trocar de popup.

Antes de entregar:
- validar JS com `node --check`;
- testar ZIP com `unzip -t`;
- atualizar cache do `sw.js` para a nova versão;
- atualizar README e este relatório;
- testar Thiago e Natália;
- testar treino, descanso e carga;
- testar Cardio e erro de GPS;
- testar Evolução e compartilhamento;
- testar Nutrição, porções, compras e preparo;
- entregar ZIP e index separado.

# 12. Prompt de retomada recomendado

> Use o ZIP anexado como base oficial. Leia primeiro o RELATÓRIO MESTRE. Preserve layout, arquitetura, chave gymwp.v1, dados e funcionalidades. Faça apenas os ajustes listados, de forma incremental. Se houver Nutrição, use exclusivamente a planilha anexada. Valide o JavaScript e devolva o ZIP completo, o index.html separado e o relatório mestre atualizado.

# 13. Situação consolidada na v15

Verificado no arquivo:
- chave `gymwp.v1`;
- Cardio;
- período Semana;
- relatório semanal;
- compartilhamento de relatório;
- compartilhamento para análise;
- Porção do dia a dia;
- instrução para reabrir descanso;
- popup exclusivo de progressão;
- orientação automática de exercícios.

**Regra final:** a última versão do código é a fonte técnica. Este relatório é a fonte das decisões. Em caso de conflito, não remover nada sem confirmar com Thiago.

---

# ATUALIZAÇÃO CONSOLIDADA — TRACKFIT v16

A v16 evolui incrementalmente sobre a v15 e mantém como regras obrigatórias o layout originado na v13, a arquitetura PWA, os temas azul/rosa e a chave `gymwp.v1`.

## 1. Timer e alertas
- O descanso não encerra mais visualmente em 00:00. Depois do tempo planejado, continua como `+00:01`, `+00:02` etc.
- O tempo excedido assume vermelho e estado visual de alerta.
- O excesso permanece calculado a partir do timestamp real, inclusive ao retornar ao app.
- O fim do descanso tenta disparar simultaneamente gongo, vibração e notificação `Descanso concluído`.
- O aviso de término usa tag própria, separada da notificação silenciosa de `Descanso em andamento`.
- O app tenta tocar o gongo mesmo se o documento estiver em segundo plano, além da notificação do sistema.
- Limitação preservada no relatório: Safari/iOS pode suspender completamente JavaScript em segundo plano; sem app nativo não há garantia absoluta de áudio programado enquanto suspenso. Ao retomar, o TrackFit detecta o término e preserva o excesso.
- Não reiniciar o timer ao abrir/fechar perguntas, progressão ou modais.

## 2. Progressão de carga
A recomendação possui três identidades distintas:
- **AUMENTAR CARGA:** verde, ação positiva e mensagem de progressão conquistada.
- **MANTER CARGA:** amarelo, confirmação de manutenção e banco rotativo de 20 mensagens motivacionais/técnicas.
- **REDUZIR CARGA:** vermelho, ação corretiva e mensagem explicando que reduzir para recuperar a faixa não representa regressão.

O descanso continua correndo por trás do popup.

## 3. Cardio prescrito dentro da ficha
Atividades de ficha `kind: c` deixam de ser apenas um check simples e ganham:
- cronômetro guiado com alerta de término equivalente ao descanso;
- registro de tempo realizado;
- distância opcional;
- velocidade média opcional;
- intensidade percebida;
- pergunta sobre capacidade restante;
- identificação de HIIT/intervalado;
- no HIIT: velocidade rápida, velocidade de recuperação, duração do tiro e recuperação;
- recomendação automática do Personal Trainer.

### Regra de progressão de cardio
Alterar uma variável por vez:
- cardio contínuo confortável: priorizar +~10% de duração antes de velocidade;
- cardio muito forte: manter/reduzir levemente intensidade até consolidar;
- HIIT confortável: primeiro reduzir recuperação em ~10 s;
- HIIT muito forte: manter intervalo e reduzir intensidade rápida;
- após sessão consolidada, permitir nova progressão.

Os dados ficam em `cardioEx`, separados do Cardio GPS independente.

## 4. Nutrição real do dia
Cada refeição adulta passa a permitir:
- **Comi conforme o plano:** usa kcal/proteína calculadas do plano.
- **Comi diferente:** usuário informa kcal reais aproximadas, proteína opcional e observação; o valor real substitui o planejado no consumido do dia.
- **+ Registrar alimento extra:** descrição, kcal, proteína opcional e horário.

Extras entram imediatamente no total diário e aparecem na timeline da Nutrição. O objetivo é representar o consumo realmente registrado, sem presumir que toda refeição seguiu o plano.

Novos campos de Nutrição:
- `actual`: estado real das refeições;
- `extras`: alimentos adicionais do dia.

## 5. Evolução futura
A base v16 passa a armazenar dados suficientes para análises posteriores de:
- tempo real além do descanso planejado;
- cardio prescrito e progressão de duração/velocidade/HIIT;
- aderência ao plano alimentar e calorias adicionais.

Não inferir causalidade clínica a partir desses registros.

## 6. Backup e sanitização v16
Novos dados persistentes que devem continuar sendo preservados em versões futuras:
- `cardioEx`;
- `nut.actual`;
- `nut.extras`;
- timer `alerted` e `over`.

## 7. Checklist específico v16+
- Testar descanso até cruzar 00:00 e confirmar contador `+MM:SS` vermelho.
- Testar timer recolhido durante tempo excedido.
- Testar som com app aberto e música externa tocando.
- Testar notificação ao sair do app e depois no término; registrar limitações observadas no Safari/iPhone.
- Testar Aumentar, Manter e Reduzir separadamente.
- Confirmar rotação das mensagens de manutenção.
- Testar Cardio prescrito contínuo e HIIT.
- Confirmar que apenas uma variável é sugerida por progressão de Cardio.
- Testar refeição conforme plano, diferente e alimento extra.
- Confirmar que calorias extras entram no total diário.

**Fonte técnica oficial após esta entrega:** `trackfit-v16.zip` e `trackfit-v16-index.html`.
