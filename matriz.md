# Matriz de Rastreabilidade – Sistema SRL

Esta matriz relaciona cada Requisito Funcional (RF) e Regra de Negócio (RN) aos seus respectivos Casos de Teste (CT).

---

## Requisitos Funcionais

| Requisito | Descrição | Casos de Teste |
|-----------|-----------|----------------|
| RF01 | Registrar usuário | CT01, CT02, CT03, CT04, CT05 |
| RF02 | Login com email e senha válidos | CT06, CT07, CT08 |
| RF03 | Retornar token após login bem-sucedido | CT06 |
| RF04 | ADMIN cadastra sala | CT09, CT10, CT11, CT12, CT13 |
| RF05 | Listar todas as salas | CT14 |
| RF06 | Criar reserva | CT15, CT16, CT17, CT18, CT19 |
| RF07 | Listar próprias reservas | CT20 |
| RF08 | Status CONFIRMED ao criar reserva válida | CT15 |
| RF09 | Abrir incidente vinculado a sala | CT21, CT22 |
| RF10 | ADMIN finaliza incidente | CT23, CT24 |
| RF11 | Status OPEN ao abrir incidente | CT21 |
| RF12 | Status CLOSED ao finalizar incidente | CT23, CT25 |

---

## Regras de Negócio

| Regra | Descrição | Casos de Teste |
|-------|-----------|----------------|
| RN01 | Email único no sistema | CT02 |
| RN02 | Senha mínima: 8 caracteres, 1 letra e 1 número | CT03, CT04, CT05 |
| RN03 | Token obrigatório para Salas, Reservas e Incidentes | CT11 |
| RN04 | Nome de sala não pode ser duplicado | CT12 |
| RN05 | Capacidade da sala deve ser maior que 0 | CT13 |
| RN06 | Hora de início deve ser menor que hora de término | CT16 |
| RN07 | Reservas entre 08:00 e 22:00 | CT17 |
| RN08 | Sem conflito de horário na mesma sala e data | CT18 |
| RN09 | Sala deve existir para criar reserva | CT19 |
| RN10 | Descrição do incidente mínimo 10 caracteres | CT22 |
| RN11 | Apenas ADMIN pode finalizar incidente | CT24 |
| RN12 | Incidente só pode ser fechado se estiver OPEN | CT25 |

---

## Resumo de Cobertura

| Total de Requisitos (RF) | Total de Regras (RN) | Total de Casos de Teste |
|--------------------------|----------------------|--------------------------|
| 12 | 12 | 25 |

**Cobertura: 100% dos requisitos e regras de negócio possuem ao menos um caso de teste associado.**
