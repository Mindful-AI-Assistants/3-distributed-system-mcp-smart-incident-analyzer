# Estrutura da apresentação — README mestre → slides

Este documento divide o conteúdo do `README.md` em **slides sequenciais**, preservando profundidade técnica. Cada bloco indica a **seção do README** correspondente e o **foco narrativo** da defesa.

**Deck HTML/React**: `_Presentation/apresentacao-readme-mestre-completa.html`  
**Instruções de implementação visual**: [GUIA_HTML_REACT_SLIDES.md](GUIA_HTML_REACT_SLIDES.md)

---

## Mapa rápido (seção README → faixa de slides)

| Seções README | Slides (aprox.) |
|----------------|-----------------|
| Capa, visão geral, índice | 01–03 |
| §1 Contexto | 04–05 |
| §2 Objetivo | 06–07 |
| §3 Proposta | 08–09 |
| §4 MCP | 10–11 |
| §5 Conceitos | 12–13 |
| §6 Arquitetura | 14–15 |
| §7 Lógica vs física | 16–18 |
| **Comunicação (JSON-RPC, Protobuf, evolução)** | **19–23** |
| **Machine Learning no sistema** | **24–25** |
| §8 Componentes | 26–27 |
| §9 Fluxo | 28–29 |
| §10 Estrutura | 30–31 |
| §11 Tecnologias | 32–33 |
| §12 Prática | 33 |
| §13 Execução | 34–35 |
| §14–§17 | 36–39 |
| §18–§23 + encerramento | 41–45 |

---

## Slides (roteiro detalhado)

### 01 — Capa

- **Título**: MCP Smart Incident Analyzer  
- **Subtítulo**: Comunicação distribuída para IA com MCP (Model Context Protocol).  
- **Pontos**: projeto acadêmico-técnico; foco em incidentes em sistemas de IA; README como documento mestre.

### 02 — Visão geral: o que é o projeto

- **Fonte**: README «Visão geral».  
- **Conteúdo**: arquitetura distribuída; MCP como base de comunicação estruturada; incidentes como casos rastreáveis e auditáveis.  
- **Ênfase**: não é apenas “um script”: é uma **linha de arquitetura** para observabilidade e contexto.

### 03 — README mestre: quatro funções

- **Fonte**: README lista numerada sob «Visão geral».  
- **Funções**: (1) documentação técnica; (2) base de relatório; (3) base de apresentação; (4) README GitHub institucional.

### 04 — §1 Contexto do problema (parte 1)

- **Conteúdo**: crescimento de sistemas inteligentes em corporações e academia; aumento de falhas, vieses, incidentes de segurança, riscos regulatórios.  
- **Mensagem**: o problema é **organizacional e técnico**, não só “erro de modelo”.

### 05 — §1 Contexto (parte 2): incidente como fenômeno distribuído

- **Conteúdo**: incidente emerge da cadeia entrada → contexto → modelo → ferramentas → decisões intermediárias → resposta.  
- **Definição**: análise de incidentes em IA é **distribuída**, contextual e multifatorial.  
- **Gap**: monólitos pouco observáveis impedem reconstrução auditável do que ocorreu.

### 06 — §2 Objetivo principal

- **Conteúdo**: plataforma para analisar incidentes de forma **estruturada, explicável, extensível e escalável**; MCP como base entre componentes distribuídos.

### 07 — §2 Objetivos específicos

- **Lista**: padronizar contexto; rastreabilidade; comunicação entre serviços especializados; documentação de eventos críticos; expansão com novos servidores MCP; projeto como documento + demonstração.

### 08 — §3 Proposta da solução

- **Conteúdo**: responsabilidades separadas; incidente vira contexto estruturado; encaminhamento modular; resposta consolidada para investigação.

### 09 — §3 Núcleo operacional

- **Conteúdo**: MCP servers não são “extras”: são **coração operacional** da visão distribuída (conceitual e de roadmap).

### 10 — §4 O que é MCP

- **Conteúdo**: troca estruturada de contexto entre modelos, apps, agentes e ferramentas; papel de **contrato** e de **fronteira** entre componentes.

### 11 — §4 Por que MCP importa

- **Conteúdo**: sem protocolo explícito, integrações viram improviso; MCP favorece previsibilidade, manutenção e auditoria.  
- **Bullets**: transporte de contexto; estruturação de requisição/resposta; interoperabilidade; baixo acoplamento; orquestração analítica.

### 12 — §5 Conceitos e siglas (bloco 1)

- **Termos**: MCP; IA / AI; LLM; API; UI.  
- **Para cada um**: definição curta + **para que serve** + **por que importa neste projeto** (sem assumir pré-requisitos da audiência).

### 13 — §5 Conceitos e siglas (bloco 2)

- **Termos**: JSON; HTTP; CSV; Log; Prompt; Contexto; Orquestração.  
- **Ênfase**: JSON como formato atual de mensagens; logs como evidência para incidentes; orquestração como coordenação explícita entre etapas.

### 14 — §6 Arquitetura: cinco características

- **Lista**: modularidade; comunicação estruturada; escalabilidade; rastreabilidade; extensibilidade.

### 15 — §6 Diagrama arquitetural (referência Mermaid)

- **Conteúdo**: fluxo Usuário → Interface → Orquestrador → MCP Client → MCP Servers (contexto, classificação, histórico) → Camada analítica → Consolidação → Dashboard/relatório.  
- **Nota de apresentação**: o diagrama completo está no README; usar exportação SVG/PNG ou Live Editor para slide visual se necessário.

### 16 — §7 Arquitetura lógica

- **Conteúdo**: divisão **conceitual** de responsabilidades; perguntas: quem recebe, orquestra, classifica, histórico, consolida, apresenta.

### 17 — §7 Arquitetura física (implementação atual)

- **Conteúdo**: `server/` (servidor JSON-RPC TCP); `client/` (cliente interativo); `tests/`; guias na raiz (`GUIA_EXECUCAO.md`, `ESTRUTURA_PROJETO.md`).

### 18 — §7 Diagrama físico (ASCII)

- **Conteúdo**: árvore ASCII simplificada raiz → `server/` | `client/` | `tests/` | documentação (slide com bloco monoespaçado).

---

### 19 — Comunicação entre serviços: implementação atual

- **Profundidade**: o repositório usa **TCP** assíncrono (`asyncio`) com mensagens **JSON-RPC 2.0** delimitadas por **newline** (uma requisição/resposta por linha legível).  
- **Por que importa**: contrato explícito (`method`, `params`, `id`, `jsonrpc`); inspecionável com ferramentas simples; adequado a protótipo e ensino.

### 20 — Exemplo mínimo JSON-RPC (pedido e resposta)

- **Conteúdo**: exemplo textual `analyze_incident` / `ping` — slide com bloco de código (não simplificar: mostrar estrutura real JSON-RPC).

### 21 — Evolução: Protobuf e contratos binários

- **Conteúdo**: em sistemas distribuídos em produção, **schemas versionáveis** reduzem ambiguidade; **Protobuf** define mensagens com campos tipados e evolução compatível (`optional`, números de campo).  
- **Contraste**: JSON-RPC excelente para debug; Protobuf + gRPC frequentemente usados para **alto throughput** e **contratos rígidos** entre microsserviços.

### 22 — Exemplo de schema Protobuf (incidente)

- **Conteúdo**: arquivo `.proto` com mensagens `Incident`, `AnalyzeRequest`, `AnalyzeResponse` — slide dedicado ao código (ver deck HTML).

### 23 — Rotas de evolução do transporte

- **Conteúdo**: JSON-RPC atual → possível **gRPC** com Protobuf para servidores especializados; camada HTTP (FastAPI) para UI/dashboard; **MCP oficial** como integração com ecossistema de agentes conforme maturidade do projeto.

---

### 24 — Machine Learning: estado atual no código

- **Transparência**: a classe `IncidentAnalyzer` no servidor aplica **heurísticas determinísticas** (palavras-chave por categoria, mapa severidade → prioridade, recomendações por tabela).  
- **Papel**: prova de conceito de **pipeline analítico** e **classificação** sem dependência de modelo externo obrigatório.

### 25 — Machine Learning: integração no sistema (roadmap técnico)

- **Camadas possíveis**:  
  - **LLM**: sumarização, explicação ao humano, geração de relatório estruturado a partir do contexto MCP.  
  - **Embeddings + busca vetorial**: similaridade com incidentes históricos (substituir ou complementar “histórico” por recuperação semântica).  
  - **Modelos supervisionados**: severidade ou roteamento entre servidores especializados com base em features extraídas do texto e metadados.  
- **Orquestração**: filas de inferência, timeouts, fallback para regras quando o modelo falhar — essencial para **confiabilidade** em incidentes.

---

### 26 — §8 Componentes (entrada, orquestrador, cliente MCP, servidores)

- **Conteúdo**: interface de entrada; orquestrador; MCP Client; MCP Servers (funções especializadas listadas no README).

### 27 — §8 Camada analítica e saída

- **Conteúdo**: consolidação com regras + roadmap ML; saída em UI/dashboard/relatório.

### 28 — §9 Fluxo operacional (passos)

- **Lista numerada**: do registro do incidente à saída compreensível (oito passos do README).

### 29 — §9 Diagrama de sequência (referência)

- **Conteúdo**: participantes Usuário, Interface, Orquestrador, MCP Client, três MCP Servers, Resultado — referência ao Mermaid do README.

### 30 — §10 Estrutura atual do repositório

- **Conteúdo**: árvore real `server/`, `client/`, `tests/`, documentação.

### 31 — §10 Estrutura alvo (evolução)

- **Conteúdo**: `app/`, `mcp_servers/`, `data/`, `docs/`, `notebooks/` como visão futura.

### 32 — §11 Tecnologias — implementação atual

- **Conteúdo**: Python 3.10+; stdlib; JSON-RPC; pytest; ferramentas de qualidade.

### 33 — §11 Planejamento (FastAPI, Streamlit, MCP)

- **Conteúdo**: o que ainda não é dependência de execução obrigatória; MCP como alinhamento conceitual com o ecossistema.

### 33 — §12 Como funciona na prática (três pilares)

- **Pilares**: modularidade; contextualização; distribuição da análise.

### 34 — §13 Execução: ambiente e dependências

- **Conteúdo**: clone, `venv`, `pip install -r requirements.txt`.

### 35 — §13 Execução: servidor, cliente e testes

- **Conteúdo**: dois terminais (`server/server.py`, `client/client.py`); testes com servidor ativo; link ao `GUIA_EXECUCAO.md`.

### 36 — §14 Exemplo de uso

- **Narrativa**: resposta inadequada em contexto sensível; o que o sistema permite observar (entrada, contexto, módulos, classificação, histórico, construção da resposta).

### 37 — §15 Casos de uso

- **Quatro casos**: sensível; triagem; auditoria; ambiente acadêmico.

### 38 — §16 Diferenciais técnicos

- **Lista**: MCP como eixo; distribuição; expansão por servidores; separação entrada/orquestração/análise/saída; rastreabilidade.

### 39 — §17 Benefícios acadêmicos e práticos

- **Dois blocos**: acadêmicos (explicar arquitetura, teoria-prática, relatório); práticos (organização, manutenção, portfólio).

### 40 — §18 Limitações atuais

- **Conteúdo**: maturidade dos MCP servers; testes integrados; robustez histórica; interface; infraestrutura distribuída incremental.

### 41 — §19 Evoluções futuras

- **Roadmap**: novos servidores; observabilidade; priorização; relatórios; dashboards; explicabilidade.

### 42 — §20 e §21 Documentação, relatório, preview de interface (slide único)

- **Conteúdo**: reuso do README em relatório e slides; placeholders para capturas futuras do dashboard. Duas seções do README são tratadas no mesmo slide para manter ritmo sem perder conteúdo — pode-se dividir em dois slides na versão oral se o tempo permitir.

### 43 — §22 Licença

- **Conteúdo**: escolha institucional; exemplo MIT; ajustes por política da faculdade.

### 44 — §23 Conclusão

- **Mensagem**: mais que app isolada — **forma estruturada** de tratar incidentes em IA; MCP no centro da interoperabilidade e auditoria; README mestre como fonte sincronizada.

### 45 — Encerramento e créditos

- **Professor**: Carlos Eduardo (completar nome conforme instituição, se exigido).  
- **Autores**: Fabiana Campanari; Pedro Vyctor Almeida.  
- **Convite**: perguntas — slide `closing` no deck HTML.

---

## Observações para o apresentador

1. **Honestidade técnica**: distinguir sempre **visão-alvo** (vários MCP servers, MCP protocol nativo) da **implementação atual** (cliente/servidor JSON-RPC, análise heurística).  
2. **Diagramas**: README contém Mermaid **fonte**; para exibir em sala, exportar imagens ou usar o deck HTML + explicação oral.  
3. **Protobuf**: o exemplo do slide é **ilustrativo da evolução**; o código em produção no repositório permanece JSON-RPC até migração explícita.
