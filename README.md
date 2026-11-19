# 🛴 Urban Scooter — Engenharia de Garantia da Qualidade (QA)

![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge)
![Testes Executados](https://img.shields.io/badge/Casos%20de%20Teste-67-blue?style=for-the-badge)
![Bugs Reportados](https://img.shields.io/badge/Bugs%20no%20Jira-18-red?style=for-the-badge)
![Cross-Browser](https://img.shields.io/badge/Web-Chrome%20%26%20Opera%20(1280x720)-orange?style=for-the-badge)
![API Testing](https://img.shields.io/badge/API-Postman%20%7C%20REST-ff6c37?style=for-the-badge)
![Database](https://img.shields.io/badge/DB-PostgreSQL-336791?style=for-the-badge)

Portfólio técnico do **Projeto Final de QA (Sprint 9)** focado na validação ponta a ponta da plataforma **Urban Scooter** — um serviço de aluguel de patinetes elétricos. O projeto abrange análise de requisitos, design de casos de teste aplicando técnicas formais, execução *cross-browser* em interface Web, validação de endpoints REST API, verificação de persistência em banco de dados PostgreSQL e rastreamento de defeitos no Jira.

---

## 📊 Resumo Executivo e Métricas de Qualidade

| Módulo / Escopo | Casos Projetados | Aprovados | Reprovados | Taxa de Aprovação | Bugs Registrados (Jira) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Tarefa 1 — Aplicativo Web (`Fazer Pedido`)** | 37 | 34 | 3 | 91,9% | `PBQ3S9PF-1` a `PBQ3S9PF-3` |
| **Tarefa 3 — Backend & REST API (`Entregadores`)** | 30 | 15 | 15 | 50,0% | `PBQ3S9PF-4` a `PBQ3S9PF-18` |
| **Total Geral Executado** | **67** | **49** | **18** | **73,1%** | **18 Tickets** |

---

## 🧠 Técnicas de Design de Testes Aplicadas

Para garantir máxima cobertura com otimização de massa de dados, todos os cenários foram projetados combinando:
* **Particionamento de Equivalência (EP):** Divisão das entradas em partições válidas e inválidas (alfabetos latino e cirílico, dígitos numéricos, símbolos especiais, espaços iniciais/finais/intermediários e valores decimais).
* **Análise de Valor Limite (BVA):** Validação rigorosa das fronteiras mínimas e máximas de comprimento de strings e parâmetros (`Nome`/`Sobrenome`: 2 a 15 caracteres; `Endereço`: 5 a 50 caracteres; `Telefone`: 10 a 12 caracteres; `login`/`firstName` API: 2 a 10 caracteres; `password` API: exatamente 4 dígitos).
* **Testes Negativos e de Obrigatoriedade:** Submissão de campos vazios, omissão de chaves obrigatórias no JSON, duplicidade de registros (`409 Conflict`) e parâmetros de rota ausentes ou malformados.
* **Testes Cross-Browser:** Execução espelhada no **Google Chrome (v85+)** e **Opera (v71+)** sob resolução fixa de **1280×720**.

---

## 🛠️ Stack Tecnológica e Ambiente de Testes

* **Gestão de Casos de Teste:** Google Sheets & CSV estruturado
* **Rastreamento de Defeitos:** Atlassian Jira (`paulabizarro.atlassian.net`)
* **Testes Web & Layout:** Google Chrome, Opera, Chrome DevTools (Viewport `1280x720`), Protótipos Figma
* **Testes de API:** Postman Desktop (Collections, Environments, variáveis `{{baseUrl}}`)
* **Banco de Dados:** PostgreSQL (`psql -U morty -d scooter_rent` — validação na tabela `"Couriers"`)

---

## 🐛 Catálogo Completo de Defeitos Encontrados (18 Bugs)

### 🌐 Tarefa 1: Interface Web — Formulário *"Para quem é a scooter"* (`/order`)

| ID Jira | Caso | Severidade | Resumo do Defeito (Resultado Real) |
| :--- | :---: | :---: | :--- |
| [PBQ3S9PF-1](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-1) | CT-05 | Média | Campo **Nome** rejeita caracteres cirílicos (`Джон`) exibindo borda vermelha e erro `"Enter a valid name"`. |
| [PBQ3S9PF-2](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-2) | CT-15 | Média | Campo **Sobrenome** aceita mais de 15 caracteres (`BizarroBizarroBiz` — 17 caracteres) sem destaque vermelho ou erro. |
| [PBQ3S9PF-3](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-3) | CT-27 | Alta | Campo obrigatório **Endereço** não exibe destaque em vermelho nem mensagem de erro ao submeter o formulário vazio. |

---

### ⚙️ Tarefa 3: Backend & REST API — Endpoints de Entregadores

#### 1. Criação de Entregador (`POST /api/v1/courier`)

| ID Jira | Caso | Severidade | Resumo do Defeito (Resultado Real) |
| :--- | :---: | :---: | :--- |
| [PBQ3S9PF-4](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-4) | CT-07 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar `login` com 1 caractere (`"a"`), abaixo do mínimo de 2. |
| [PBQ3S9PF-5](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-5) | CT-08 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar `login` com 11 caracteres (`"abcdefghijk"`), acima do máximo de 10. |
| [PBQ3S9PF-6](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-6) | CT-09 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar números no campo `login` (`"ninja123"`). |
| [PBQ3S9PF-12](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-12) | CT-10 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar caracteres especiais no campo `login` (`"ninja@!"`). |
| [PBQ3S9PF-7](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-7) | CT-14 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar `firstName` com 1 caractere (`"P"`). |
| [PBQ3S9PF-8](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-8) | CT-15 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar `firstName` com 11 caracteres (`"Paulabizarr"`). |
| [PBQ3S9PF-9](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-9) | CT-16 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar números no campo `firstName` (`"Paula12"`). |
| [PBQ3S9PF-10](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-10) | CT-17 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar símbolos no campo `firstName` (`"Paula@#"`). |
| [PBQ3S9PF-11](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-11) | CT-21 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar `password` com 3 dígitos (`"123"`), abaixo do tamanho fixo de 4. |
| [PBQ3S9PF-13](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-13) | CT-22 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar `password` com 5 dígitos (`"12345"`), acima do tamanho fixo de 4. |
| [PBQ3S9PF-14](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-14) | CT-23 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar letras no campo `password` (`"abcd"`). |
| [PBQ3S9PF-15](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-15) | CT-24 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar símbolos no campo `password` (`"12@#"`). |
| [PBQ3S9PF-16](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-16) | CT-25 | Média | `POST /api/v1/courier`: Retorna `201 Created` ao enviar número decimal/fracionado no campo `password` (`"12.3"`). |

#### 2. Exclusão de Entregador (`DELETE /api/v1/courier/:id`)

| ID Jira | Caso | Severidade | Resumo do Defeito (Resultado Real) |
| :--- | :---: | :---: | :--- |
| [PBQ3S9PF-17](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-17) | CT-29 | Alta | `DELETE /api/v1/courier/`: Retorna `500 Internal Server Error` (`invalid input syntax for integer`) ao omitir o parâmetro `:id`. |
| [PBQ3S9PF-18](https://paulabizarro.atlassian.net/browse/PBQ3S9PF-18) | CT-30 | Alta | `DELETE /api/v1/courier/%20`: Retorna `500 Internal Server Error` (`invalid input syntax for integer`) ao enviar espaço vazio no `:id`. |

---

## 🔍 Principais Diagnósticos Técnicos

1. **Ausência de Validação de Schema no Back-end:** O endpoint `POST /api/v1/courier` verifica apenas a presença ou ausência das chaves obrigatórias `login` e `password` (retornando `400 Bad Request` quando vazias ou omitidas), mas não aplica regras de regex, tipagem ou limites de caracteres sobre os valores enviados.
2. **Tratamento de Exceção SQL nas Rotas `DELETE`:** Ao receber uma rota sem `:id` (`/api/v1/courier/`) ou contendo espaço codificado (`%20`), a aplicação repassa uma string vazia diretamente para a consulta de inteiro no PostgreSQL, gerando exceção não tratada (`HTTP 500`) em vez de retornar `400 Bad Request` ou `404 Not Found`.
3. **Inconsistência de Validação no Front-end:** O formulário *"Para quem é a scooter"* apresenta validação funcional consistente entre Chrome e Opera, porém diverge dos requisitos em três pontos específicos: bloqueio de alfabeto cirílico no nome, ausência de trava de limite máximo no sobrenome e falta de *feedback* visual de erro ao submeter o endereço em branco.

---

## 👩‍💻 Autora

**Paula Bizarro** — Quality Assurance Analyst  
* **GitHub:** [github.com/paulabizarro](https://github.com/paulabizarro)
* **LinkedIn:** [linkedin.com/in/paula-bizarro](https://www.linkedin.com/in/paula-bizarro)
* **Contato:** paulabizarro@icloud.com
