# reactiontime

Teste de Tempo de Reação simples, leve e responsivo implementado em uma única página HTML (`index.html`).

**Descrição:**
- Projeto para medir tempos de reação visuais em três tentativas, com feedback imediato, resumo da sessão e comparação com uma distribuição de referência.

**Funcionalidades principais:**
- Interface touch/click otimizada para desktop e mobile.
- Três tentativas por sessão, com feedback para cliques prematuros.
- Cálculo de melhor/média/pior tempo, percentil aproximado e z-score.
- Armazenamento local do melhor tempo (`localStorage`).
- Tabelas comparativas dinâmicas geradas a partir de parâmetros estatísticos.

**Como usar**
- Abrir o arquivo `index.html` diretamente no navegador (duplo clique) ou rodar um servidor local para evitar restrições de CORS/recursos:

```bash
# a partir da pasta do projeto, com Python 3
python3 -m http.server 8000
# então abra http://localhost:8000 no navegador
```

**Controles e acessibilidade**
- Toque/ clique na área principal (`#prompt`) para interagir.
- Suporte a teclado: pressione a tecla `Space` para simular o clique.

**Personalização rápida**
- Abra `index.html` e localize as constantes no script:
	- `totalTrials` — número de tentativas por sessão (padrão: 3).
	- `MU` e `SIGMA` — parâmetros usados para percentis e tabelas de referência.
	- `bestReactionTime` — valor salvo em `localStorage` para histórico local.

**Notas de implementação**
- Usa `performance.now()` para medições de alta precisão.
- A função de percentil emprega uma aproximação da função erro (`erf`) para obter a CDF normal.

**Contribuições**
- Pull requests são bem-vindos. Prefira mudanças pequenas e bem testadas.

**Licença**
- Nenhuma licença especificada; adicione um arquivo `LICENSE` se desejar declarar termos de uso.
