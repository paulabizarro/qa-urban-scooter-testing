# 📋 Plano de Testes — Urban Scooter

## 1. Objetivo
Validar a qualidade funcional, regras de validação de entrada, comportamento cross-browser e integridade de API/Banco de Dados do aplicativo **Urban Scooter** antes da liberação em produção.

---

## 2. Escopo de Testes

### 2.1 Tarefa 1: Aplicativo Web (`/order` — Formulário *"Para quem é a scooter"*)
* **Campos avaliados:**
  * **Nome:** Obrigatório | 2 a 15 caracteres | Somente letras, espaços e traços.
  * **Sobrenome:** Obrigatório | 2 a 15 caracteres | Somente letras, espaços e traços.
  * **Endereço:** Obrigatório | 5 a 50 caracteres | Letras, números, espaços, traços, pontos e vírgulas (trim automático de espaços nas extremidades).
  * **Estação de metrô:** Obrigatório | Lista suspensa carregada via API (estações de Los Angeles).
  * **Telefone:** Obrigatório | 10 a 12 caracteres | Somente números e sinal de `+` obrigatório na primeira posição.

### 2.2 Tarefa 3: Backend & REST API (`/api/v1/courier`)
* **`POST /api/v1/courier` (Criar entregador):**
  * `login`: Obrigatório | 2 a 10 caracteres | Somente letras latinas | Único no banco.
  * `password`: Obrigatório | Exatamente 4 caracteres | Somente números inteiros.
  * `firstName`: Opcional | 2 a 10 caracteres | Somente letras latinas.
* **`DELETE /api/v1/courier/:id` (Excluir entregador):**
  * Remoção por ID válido existente (`200 OK`), tentativa de re-exclusão (`404 Not Found`), ID inexistente (`404 Not Found`), ausência de parâmetro ou parâmetro vazio (`400 Bad Request` / `404 Not Found`).

---

## 3. Matriz de Ambientes
* **Navegadores Web:** Google Chrome (v85+) e Opera (v71+)
* **Resolução de Viewport:** `1280x720` (configurada via DevTools)
* **Cliente API:** Postman Desktop
* **Banco de Dados:** PostgreSQL (`scooter_rent`, tabela `"Couriers"`)
* **Sistema Operacional:** Windows 11
