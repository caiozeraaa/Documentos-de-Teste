# Casos de Teste – Sistema SRL

---

## MÓDULO 1 – AUTENTICAÇÃO

---

### CT01 – Registro de usuário com dados válidos
**Requisito:** RF01  
**Descrição:** Verificar se o sistema permite cadastrar um novo usuário com todos os dados válidos.  
**Pré-condição:** Nenhum usuário com o email informado deve existir no sistema.  
**Entrada:**
```json
{
  "nome": "João Silva",
  "email": "joao@email.com",
  "senha": "Senha123",
  "perfil": "USER"
}
```
**Resultado Esperado:** Status HTTP 201. Usuário criado com sucesso. Resposta contém os dados do usuário cadastrado.

---

### CT02 – Registro com email já existente
**Requisito:** RF01, RN01  
**Descrição:** Verificar se o sistema impede cadastro com email já utilizado.  
**Pré-condição:** Usuário com email "joao@email.com" já cadastrado no sistema.  
**Entrada:**
```json
{
  "nome": "Outro Usuário",
  "email": "joao@email.com",
  "senha": "Outra123",
  "perfil": "USER"
}
```
**Resultado Esperado:** Status HTTP 400 ou 409. Mensagem de erro indicando que o email já está em uso.

---

### CT03 – Registro com senha sem número
**Requisito:** RF01, RN02  
**Descrição:** Verificar se o sistema rejeita senha que não contenha número.  
**Pré-condição:** Nenhuma.  
**Entrada:**
```json
{
  "nome": "Maria Costa",
  "email": "maria@email.com",
  "senha": "senhainvalida",
  "perfil": "USER"
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem de erro indicando que a senha não atende os requisitos mínimos.

---

### CT04 – Registro com senha sem letra
**Requisito:** RF01, RN02  
**Descrição:** Verificar se o sistema rejeita senha composta apenas por números.  
**Pré-condição:** Nenhuma.  
**Entrada:**
```json
{
  "nome": "Carlos Lima",
  "email": "carlos@email.com",
  "senha": "12345678",
  "perfil": "USER"
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem de erro sobre requisitos de senha.

---

### CT05 – Registro com senha com menos de 8 caracteres
**Requisito:** RF01, RN02  
**Descrição:** Verificar se o sistema rejeita senha muito curta.  
**Pré-condição:** Nenhuma.  
**Entrada:**
```json
{
  "nome": "Ana Souza",
  "email": "ana@email.com",
  "senha": "Ab1",
  "perfil": "USER"
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem de erro indicando que a senha deve ter no mínimo 8 caracteres.

---

### CT06 – Login com credenciais válidas
**Requisito:** RF02, RF03  
**Descrição:** Verificar se o sistema realiza login e retorna token de autenticação.  
**Pré-condição:** Usuário "joao@email.com" / "Senha123" previamente cadastrado.  
**Entrada:**
```json
{
  "email": "joao@email.com",
  "senha": "Senha123"
}
```
**Resultado Esperado:** Status HTTP 200. Resposta contém token JWT válido.

---

### CT07 – Login com senha incorreta
**Requisito:** RF02  
**Descrição:** Verificar se o sistema rejeita login com senha errada.  
**Pré-condição:** Usuário "joao@email.com" previamente cadastrado.  
**Entrada:**
```json
{
  "email": "joao@email.com",
  "senha": "SenhaErrada1"
}
```
**Resultado Esperado:** Status HTTP 401. Mensagem de erro indicando credenciais inválidas.

---

### CT08 – Login com email não cadastrado
**Requisito:** RF02  
**Descrição:** Verificar se o sistema rejeita login com email inexistente.  
**Pré-condição:** Nenhuma.  
**Entrada:**
```json
{
  "email": "inexistente@email.com",
  "senha": "Senha123"
}
```
**Resultado Esperado:** Status HTTP 401. Mensagem de erro indicando credenciais inválidas.

---

## MÓDULO 2 – SALAS

---

### CT09 – Criação de sala com dados válidos (ADMIN)
**Requisito:** RF04  
**Descrição:** Verificar se ADMIN consegue cadastrar uma sala com dados válidos.  
**Pré-condição:** Usuário autenticado com perfil ADMIN. Sala com o nome informado não existe.  
**Entrada (header):** `Authorization: Bearer {token_admin}`  
**Entrada (body):**
```json
{
  "nome": "Lab 01",
  "capacidade": 30,
  "recursos": ["projetor", "ar-condicionado"]
}
```
**Resultado Esperado:** Status HTTP 201. Sala criada com sucesso. Resposta contém dados da sala.

---

### CT10 – Criação de sala por usuário USER (sem permissão)
**Requisito:** RF04, RN03  
**Descrição:** Verificar se o sistema impede que USER crie sala.  
**Pré-condição:** Usuário autenticado com perfil USER.  
**Entrada (header):** `Authorization: Bearer {token_user}`  
**Entrada (body):**
```json
{
  "nome": "Lab 02",
  "capacidade": 20,
  "recursos": ["projetor"]
}
```
**Resultado Esperado:** Status HTTP 403. Mensagem de erro indicando ausência de permissão.

---

### CT11 – Criação de sala sem token
**Requisito:** RN03  
**Descrição:** Verificar se o sistema bloqueia requisição sem token de autenticação.  
**Pré-condição:** Nenhuma.  
**Entrada (header):** Sem header de autorização.  
**Entrada (body):**
```json
{
  "nome": "Lab 03",
  "capacidade": 15,
  "recursos": []
}
```
**Resultado Esperado:** Status HTTP 401. Mensagem de erro indicando que autenticação é necessária.

---

### CT12 – Criação de sala com nome duplicado
**Requisito:** RF04, RN04  
**Descrição:** Verificar se o sistema impede o cadastro de sala com nome já existente.  
**Pré-condição:** Sala com nome "Lab 01" já cadastrada. Usuário autenticado como ADMIN.  
**Entrada:**
```json
{
  "nome": "Lab 01",
  "capacidade": 25,
  "recursos": []
}
```
**Resultado Esperado:** Status HTTP 400 ou 409. Mensagem indicando que o nome da sala já existe.

---

### CT13 – Criação de sala com capacidade zero
**Requisito:** RF04, RN05  
**Descrição:** Verificar se o sistema rejeita sala com capacidade igual a zero.  
**Pré-condição:** Usuário autenticado como ADMIN.  
**Entrada:**
```json
{
  "nome": "Lab 04",
  "capacidade": 0,
  "recursos": []
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem de erro indicando que a capacidade deve ser maior que zero.

---

### CT14 – Listagem de salas com token válido
**Requisito:** RF05  
**Descrição:** Verificar se o sistema retorna a lista de salas cadastradas.  
**Pré-condição:** Ao menos uma sala cadastrada. Usuário autenticado (ADMIN ou USER).  
**Entrada (header):** `Authorization: Bearer {token}`  
**Resultado Esperado:** Status HTTP 200. Resposta contém lista com as salas cadastradas.

---

## MÓDULO 3 – RESERVAS

---

### CT15 – Criação de reserva com dados válidos
**Requisito:** RF06, RF08  
**Descrição:** Verificar se o sistema cria reserva válida com status CONFIRMED.  
**Pré-condição:** Usuário autenticado. Sala existente. Sem conflito de horário.  
**Entrada:**
```json
{
  "sala_id": 1,
  "data": "2025-09-10",
  "hora_inicio": "09:00",
  "hora_fim": "11:00",
  "finalidade": "Aula de programação"
}
```
**Resultado Esperado:** Status HTTP 201. Reserva criada com status `CONFIRMED`.

---

### CT16 – Criação de reserva com hora de início maior que hora de fim
**Requisito:** RF06, RN06  
**Descrição:** Verificar se o sistema rejeita reserva com horários invertidos.  
**Pré-condição:** Usuário autenticado. Sala existente.  
**Entrada:**
```json
{
  "sala_id": 1,
  "data": "2025-09-10",
  "hora_inicio": "14:00",
  "hora_fim": "10:00",
  "finalidade": "Reunião"
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem de erro indicando que a hora de início deve ser menor que a hora de fim.

---

### CT17 – Criação de reserva fora do horário permitido
**Requisito:** RF06, RN07  
**Descrição:** Verificar se o sistema rejeita reserva com horário fora do intervalo 08:00–22:00.  
**Pré-condição:** Usuário autenticado. Sala existente.  
**Entrada:**
```json
{
  "sala_id": 1,
  "data": "2025-09-10",
  "hora_inicio": "07:00",
  "hora_fim": "09:00",
  "finalidade": "Laboratório matutino"
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem de erro indicando que reservas só são permitidas entre 08:00 e 22:00.

---

### CT18 – Criação de reserva com conflito de horário
**Requisito:** RF06, RN08  
**Descrição:** Verificar se o sistema rejeita reserva que conflite com outra já existente.  
**Pré-condição:** Reserva existente na Sala 1, dia 2025-09-10, das 09:00 às 11:00. Usuário autenticado.  
**Entrada:**
```json
{
  "sala_id": 1,
  "data": "2025-09-10",
  "hora_inicio": "10:00",
  "hora_fim": "12:00",
  "finalidade": "Outra atividade"
}
```
**Resultado Esperado:** Status HTTP 409 ou 400. Mensagem indicando conflito de horário.

---

### CT19 – Criação de reserva para sala inexistente
**Requisito:** RF06, RN09  
**Descrição:** Verificar se o sistema rejeita reserva referenciando uma sala que não existe.  
**Pré-condição:** Usuário autenticado. ID de sala não cadastrado no sistema.  
**Entrada:**
```json
{
  "sala_id": 9999,
  "data": "2025-09-10",
  "hora_inicio": "10:00",
  "hora_fim": "12:00",
  "finalidade": "Teste"
}
```
**Resultado Esperado:** Status HTTP 404. Mensagem indicando que a sala não foi encontrada.

---

### CT20 – Listagem das próprias reservas
**Requisito:** RF07  
**Descrição:** Verificar se o usuário consegue listar suas próprias reservas.  
**Pré-condição:** Usuário autenticado com ao menos uma reserva cadastrada.  
**Entrada (header):** `Authorization: Bearer {token}`  
**Resultado Esperado:** Status HTTP 200. Lista contendo apenas as reservas do usuário autenticado.

---

## MÓDULO 4 – INCIDENTES

---

### CT21 – Abertura de incidente com dados válidos
**Requisito:** RF09, RF11  
**Descrição:** Verificar se o sistema permite abrir incidente com status OPEN.  
**Pré-condição:** Usuário autenticado. Sala existente.  
**Entrada:**
```json
{
  "sala_id": 1,
  "descricao": "Projetor não está funcionando corretamente"
}
```
**Resultado Esperado:** Status HTTP 201. Incidente criado com status `OPEN`.

---

### CT22 – Abertura de incidente com descrição menor que 10 caracteres
**Requisito:** RF09, RN10  
**Descrição:** Verificar se o sistema rejeita incidente com descrição muito curta.  
**Pré-condição:** Usuário autenticado.  
**Entrada:**
```json
{
  "sala_id": 1,
  "descricao": "Quebrado"
}
```
**Resultado Esperado:** Status HTTP 400. Mensagem indicando que a descrição deve ter no mínimo 10 caracteres.

---

### CT23 – Encerramento de incidente por ADMIN
**Requisito:** RF10, RF12  
**Descrição:** Verificar se ADMIN consegue fechar um incidente com status OPEN.  
**Pré-condição:** Incidente com status OPEN cadastrado. Usuário autenticado como ADMIN.  
**Entrada (header):** `Authorization: Bearer {token_admin}`  
**Endpoint:** `PATCH /incidents/1/close`  
**Resultado Esperado:** Status HTTP 200. Incidente com status alterado para `CLOSED`.

---

### CT24 – Encerramento de incidente por USER (sem permissão)
**Requisito:** RF10, RN11  
**Descrição:** Verificar se o sistema impede que USER encerre incidente.  
**Pré-condição:** Incidente com status OPEN cadastrado. Usuário autenticado como USER.  
**Entrada (header):** `Authorization: Bearer {token_user}`    
**Endpoint:** `PATCH /incidents/1/close`  
**Resultado Esperado:** Status HTTP 403. Mensagem indicando ausência de permissão.

---

### CT25 – Encerramento de incidente já fechado
**Requisito:** RN12  
**Descrição:** Verificar se o sistema impede fechar um incidente que já está CLOSED.  
**Pré-condição:** Incidente com status CLOSED cadastrado. Usuário autenticado como ADMIN.  
**Entrada (header):** `Authorization: Bearer {token_admin}`  
**Endpoint:** `PATCH /incidents/1/close`  
**Resultado Esperado:** Status HTTP 400 ou 409. Mensagem indicando que o incidente já está encerrado.
