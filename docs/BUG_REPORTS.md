# 🐞 Relatórios de Bugs Detalhados (Jira)

Todos os defeitos abaixo foram registrados no projeto Jira (`PBQ3S9PF`) com evidências anexadas.

---

## 🌐 Módulo Web — Formulário *"Para quem é a scooter"*

### [PBQ3S9PF-1] O campo "Nome" exibe erro "Enter a valid name" ao inserir caracteres cirílicos
* **Prioridade:** Média
* **Ambiente:** Chrome (v85+) e Opera (v71+) — Resolução `1280x720`
* **Passos para reproduzir:**
  1. Acessar a tela de pedido (`/order`).
  2. Inserir `Джон` no campo **Nome**.
  3. Mudar o foco para outro campo.
* **Resultado Esperado:** O campo aceita caracteres cirílicos sem borda vermelha ou mensagem de erro.
* **Resultado Real:** O campo exibe borda vermelha e a mensagem `"Enter a valid name"`.

---

### [PBQ3S9PF-2] O campo "Sobrenome" aceita mais de 15 caracteres sem exibir mensagem de erro ou destaque em vermelho
* **Prioridade:** Média
* **Ambiente:** Chrome (v85+) e Opera (v71+) — Resolução `1280x720`
* **Passos para reproduzir:**
  1. Acessar a tela de pedido (`/order`).
  2. Inserir `BizarroBizarroBiz` (17 caracteres) no campo **Sobrenome**.
  3. Mudar o foco para outro campo.
* **Resultado Esperado:** O campo exibe borda vermelha e a mensagem `"Insira um nome válido"`.
* **Resultado Real:** O campo aceita os 17 caracteres normalmente sem destacar erro.

---

### [PBQ3S9PF-3] O campo obrigatório "Endereço" não exibe destaque em vermelho nem mensagem de erro ao submeter o formulário vazio
* **Prioridade:** Alta
* **Ambiente:** Chrome (v85+) e Opera (v71+) — Resolução `1280x720`
* **Passos para reproduzir:**
  1. Preencher **Nome**, **Sobrenome**, **Estação de metrô** e **Telefone** com dados válidos.
  2. Deixar o campo **Endereço** vazio.
  3. Clicar em **Avançar** (`Next`).
* **Resultado Esperado:** O formulário não avança e destaca o campo **Endereço** em vermelho com mensagem de erro.
* **Resultado Real:** O formulário não avança, porém o campo permanece cinza neutro sem qualquer indicação visual de erro.

---

## ⚙️ Módulo API — `POST /api/v1/courier`

### [PBQ3S9PF-4] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `login` de 1 caractere
* **Payload:** `{"login": "a", "password": "1234", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-5] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `login` de 11 caracteres
* **Payload:** `{"login": "abcdefghijk", "password": "1234", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-6] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `login` contendo números
* **Payload:** `{"login": "ninja123", "password": "1234", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-12] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `login` contendo caracteres especiais
* **Payload:** `{"login": "ninja@!", "password": "1234", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-7] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `firstName` de 1 caractere
* **Payload:** `{"login": "courier5", "password": "1234", "firstName": "P"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-8] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `firstName` de 11 caracteres
* **Payload:** `{"login": "courier6", "password": "1234", "firstName": "Paulabizarr"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-9] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `firstName` contendo números
* **Payload:** `{"login": "courier7", "password": "1234", "firstName": "Paula12"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-10] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `firstName` contendo símbolos
* **Payload:** `{"login": "courier8", "password": "1234", "firstName": "Paula@#"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-11] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `password` de 3 dígitos
* **Payload:** `{"login": "courier12", "password": "123", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-13] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `password` de 5 dígitos
* **Payload:** `{"login": "courier13", "password": "12345", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-14] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `password` contendo letras
* **Payload:** `{"login": "courier14", "password": "abcd", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-15] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `password` contendo caracteres especiais
* **Payload:** `{"login": "courier15", "password": "12@#", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

### [PBQ3S9PF-16] `POST /api/v1/courier`: API retorna status `201 Created` ao criar entregador com `password` contendo valor decimal (`float`)
* **Payload:** `{"login": "courier16", "password": "12.3", "firstName": "sasuke"}`
* **Resultado Esperado:** `400 Bad Request`
* **Resultado Real:** `201 Created` (`{"ok": true}`)

---

## ⚙️ Módulo API — `DELETE /api/v1/courier/:id`

### [PBQ3S9PF-17] `DELETE /api/v1/courier/:id`: API retorna status `500 Internal Server Error` ao omitir o parâmetro `:id`
* **Requisição:** `DELETE /api/v1/courier/`
* **Resultado Esperado:** `400 Bad Request` ou `404 Not Found`
* **Resultado Real:** `500 Internal Server Error` (`{"code": 500, "message": "invalid input syntax for integer: " ""}`)

### [PBQ3S9PF-18] `DELETE /api/v1/courier/:id`: API retorna status `500 Internal Server Error` ao enviar espaço vazio (`%20`) no `:id`
* **Requisição:** `DELETE /api/v1/courier/%20`
* **Resultado Esperado:** `400 Bad Request` ou `404 Not Found`
* **Resultado Real:** `500 Internal Server Error` (`{"code": 500, "message": "invalid input syntax for integer: " ""}`)
