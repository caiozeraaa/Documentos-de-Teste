# Plano de Teste – Sistema SRL (Sistema de Reservas de Laboratório)
**Versão:** 1.0  
**Data:** 2025  

---

## 1. Escopo

Este plano cobre os testes funcionais dos seguintes módulos do sistema SRL:

- **Módulo 1 – Autenticação:** Registro de usuário e login
- **Módulo 2 – Salas:** Cadastro e listagem de salas
- **Módulo 3 – Reservas:** Criação e consulta de reservas
- **Módulo 4 – Incidentes:** Abertura e encerramento de incidentes

O sistema é disponibilizado exclusivamente como API REST, sem interface gráfica.

---

## 2. Objetivo

Verificar se o sistema SRL atende aos Requisitos Funcionais (RF01 a RF12) e às Regras de Negócio (RN01 a RN12) descritos no documento de requisitos versão 1.0, garantindo que:

- O sistema aceita entradas válidas e responde corretamente
- O sistema rejeita entradas inválidas com mensagens de erro adequadas
- As regras de permissão por perfil (ADMIN e USER) são respeitadas
- Os códigos de status HTTP retornados são adequados para cada situação

---

## 3. Estratégia de Teste

Serão realizados **testes funcionais manuais** sobre os endpoints da API REST, cobrindo:

- **Testes de caminho feliz (positivos):** entradas válidas que devem resultar em sucesso
- **Testes de caminho alternativo (negativos):** entradas inválidas que devem resultar em erro
- **Testes de permissão:** verificar controle de acesso por perfil (ADMIN x USER)
- **Testes de regras de negócio:** validações como conflito de horário, senha fraca, duplicidade de email, etc.

Cada caso de teste será executado isoladamente, com pré-condições bem definidas.

---

## 4. Ambiente

| Item | Descrição |
|------|-----------|
| Tipo de ambiente | Local (desenvolvimento) |
| Banco de dados | Banco de dados de teste isolado (resetado a cada ciclo) |
| Ferramenta de teste | Postman ou similar para chamadas à API REST |
| Formato de dados | JSON |
| Autenticação | Token JWT enviado via header `Authorization: Bearer {token}` |

---

## 5. Critérios de Entrada

Os testes só poderão ser iniciados quando:

- A API SRL estiver disponível e acessível no ambiente de teste
- O documento de requisitos versão 1.0 estiver aprovado
- O banco de dados de teste estiver configurado e limpo
- Os endpoints listados no documento de requisitos estiverem implementados

---

## 6. Critérios de Saída

Os testes serão considerados concluídos quando:

- Todos os casos de teste tiverem sido executados ao menos uma vez
- Todos os casos de teste críticos (autenticação e permissões) passarem com sucesso
- Os bugs encontrados estiverem registrados no arquivo `bugs.md`
- A matriz de rastreabilidade estiver preenchida e todos os requisitos cobertos

---

## 7. Responsáveis

| Papel | Responsável |
|-------|-------------|
| Analista de Teste | Aluno(a) da disciplina |
| Revisão | Professor(a) da disciplina |
