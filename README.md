# INMA · Sistema de Coleta TCG & GDACT 2025

Sistema web para coleta de indicadores de produção científica e coleções biológicas dos pesquisadores do **Instituto Nacional da Mata Atlântica (INMA/MCTI)**, desenvolvido como substituto à planilha Google Sheets compartilhada individualmente por e-mail institucional.

---

## Funcionalidades

- Login com conta Google (autenticação OAuth 2.0)
- Formulário estruturado com todos os indicadores do **TCG** e itens do **GDACT**
- Salvamento direto na aba do pesquisador na planilha institucional (Google Sheets API)
- Carregamento automático de dados já preenchidos ao fazer login
- Cálculo automático do IGPUB (soma de subindicadores)
- Campos de referências bibliográficas expansíveis (adicionar/remover entradas)
- Interface responsiva (desktop e mobile)

---

## Indicadores cobertos

### TCG — Físicos e Operacionais
| Código | Descrição | Peso |
|--------|-----------|------|
| IPUB | Índice de Publicações (Scopus / WoS / QualisCapes B2+) | 2 |
| IGPUB | Índice Geral de Publicações | 2 |
| PPCI | Programas e Projetos de Cooperação Internacional | 2 |
| PPCN | Programas e Projetos de Cooperação Nacional | 1 |
| PPBD | Projetos de Pesquisa Básica Desenvolvidos | 3 |
| ETCO | Eventos Técnicos e Científicos Organizados | 2 |
| IQC | Índice de Qualificação das Coleções Científicas Biológicas | 2 |
| IUC | Índice de Uso Anual das Coleções Científicas Biológicas | 2 |
| EAPCT | Eventos e Atividades de Popularização da C&T | 2 |
| MDC | Materiais Didático-Científicos Produzidos | 1 |
| PIS | Projetos de Inclusão Social | 2 |
| NIM | Número de Inserções na Mídia | 1 |

### GDACT — Itens complementares (1–10)
Itens não constantes dos indicadores TCG: pareceres, captação de recursos, projetos formalizados, ciência cidadã, materiais de divulgação, atividades administrativas, eventos, curadoria e orientação de bolsistas.

---

## Tecnologias

- HTML5 / CSS3 / JavaScript puro (sem frameworks, sem dependências de servidor)
- [Google Identity Services](https://developers.google.com/identity) — autenticação OAuth 2.0
- [Google Sheets API v4](https://developers.google.com/sheets/api) — leitura e escrita na planilha

---

## Configuração

### Pré-requisitos

1. Projeto no **Google Cloud Console** com OAuth 2.0 configurado
2. Planilha Google Sheets com uma aba por pesquisador (nome da aba = primeiro nome do pesquisador)
3. Planilha compartilhada com permissão de edição para os usuários

### Credenciais

As credenciais estão embutidas diretamente no `index.html` para facilitar o uso nesta versão de testes:

```js
const DEFAULT_CONFIG = {
  clientId: 'SEU_CLIENT_ID.apps.googleusercontent.com',
  sheetId:  'ID_DA_PLANILHA'
};
```

Para alterar, edite essas duas linhas no arquivo `index.html`.

### Origens autorizadas (Google Cloud Console)

Em **Credenciais → OAuth 2.0 → Origens JavaScript autorizadas**, adicione a URL onde o sistema está hospedado. Exemplo para GitHub Pages:

```
https://seuusuario.github.io
```

---

## Como usar (pesquisador)

1. Acesse a URL do sistema
2. Clique em **Entrar com Google** e use sua conta institucional
3. Preencha os indicadores nas abas **TCG** e **GDACT**
4. Clique em **Salvar no Google Sheets**
5. Os dados são gravados automaticamente na sua aba na planilha institucional

---

## Estrutura de dados na planilha

O sistema escreve em dois locais da aba do pesquisador:

- **Coluna E (Quantidade)** nas linhas originais da planilha — mantém compatibilidade com o layout existente
- **Bloco de dados completo a partir da linha 220** — armazena todos os campos incluindo referências bibliográficas, com timestamp e e-mail do usuário

---

## Roadmap

- [ ] Restrição de acesso ao domínio `@inma.gov.br`
- [ ] Painel administrativo para visualização consolidada de todos os pesquisadores
- [ ] Exportação em PDF por pesquisador
- [ ] Validação de formato de referências bibliográficas (DOI)
- [ ] Indicadores IEO, IAL e IEPCI (execução orçamentária)
- [ ] Notificação por e-mail ao pesquisador após salvamento

---

## Versão

**v0.1.0** — Abril 2025 · Versão de testes internos  
Desenvolvido para o INMA/MCTI · Santa Teresa, Espírito Santo, Brasil
