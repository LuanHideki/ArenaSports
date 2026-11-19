# ArenaSports — Documentação de Software

**Disciplina:** Engenharia de Software 
**Instituição:** Universidade Federal do Amazonas (UFAM) — Instituto de Ciências Exatas e Tecnologia (ICET)  
**Integrante da Equipe:** Luan Hideki Oda Nogueira  

---

## 1. Introdução

### 1.4. Descrição Geral do Software
O **ArenaSports** é uma plataforma voltada à automação e gestão de agendamentos de quadras esportivas (society, areia e poliesportivas)[cite: 40]. O sistema resolve o problema do choque de horários e da informalidade em reservas, permitindo que atletas visualizem agendas em tempo real, realizem reservas mediante pagamento de sinal via PIX e que os administradores controlem o caixa e bloqueiem horários para manutenção[cite: 40].

### 1.5. Descrição dos Usuários
Os usuários do sistema são classificados em dois perfis principais[cite: 40]:

1. **Atleta / Cliente:** Atletas locais que desejam consultar horários disponíveis, realizar reservas de quadras e contratar materiais adicionais (coletes, bolas)[cite: 40].
2. **Atendente / Administrador:** Responsável por gerenciar as quadras, validar reservas efetuadas presencialmente/balcão, bloquear horários para manutenção e emitir relatórios de faturamento[cite: 40].

---

## 2. Requisitos Gerais do Software

### 2.1. Requisitos Funcionais

| Identificador | Descrição | Escopo | Prioridade |
| :--- | :--- | :--- | :--- |
| **RF01** | O sistema deve permitir que o usuário crie um cadastro informando nome, e-mail, telefone e senha[cite: 41]. | Geral[cite: 41] | Essencial[cite: 41] |
| **RF02** | O sistema deve permitir o acesso do usuário por meio de login com e-mail e senha[cite: 41]. | Geral[cite: 41] | Essencial[cite: 41] |
| **RF03** | O sistema deve exibir a grade de horários disponíveis e ocupados por data e quadra[cite: 41]. | Agendamento[cite: 41] | Essencial[cite: 41] |
| **RF04** | O sistema deve permitir a reserva de um horário mediante confirmação de pagamento do sinal[cite: 41]. | Agendamento[cite: 41] | Essencial[cite: 41] |
| **RF05** | O sistema deve permitir que o usuário inclua aluguel de materiais adicionais (coletes, bolas) na reserva[cite: 41]. | Agendamento[cite: 41] | Desejável[cite: 41] |
| **RF06** | O sistema deve permitir que o usuário solicite o cancelamento de uma reserva realizada[cite: 41]. | Agendamento[cite: 41] | Importante[cite: 41] |
| **RF07** | O sistema deve permitir que o administrador bloqueie horários da agenda para manutenção[cite: 41]. | Administração[cite: 41] | Importante[cite: 41] |
| **RF08** | O sistema deve permitir a saída do usuário (logout)[cite: 41]. | Geral[cite: 41] | Importante[cite: 41] |

### 2.2. Requisitos Não Funcionais

| Identificador | Descrição | Categoria | Escopo | Prioridade |
| :--- | :--- | :--- | :--- | :--- |
| **RNF01** | O sistema deve criptografar todas as senhas dos usuários[cite: 42]. | Segurança[cite: 42] | Geral[cite: 42] | Essencial[cite: 42] |
| **RNF02** | O sistema deve processar as consultas de disponibilidade e respostas da agenda em até 2 segundos[cite: 42]. | Desempenho[cite: 42] | Agendamento[cite: 42] | Importante[cite: 42] |
| **RNF03** | O sistema deve disponibilizar interface totalmente responsiva para navegação em dispositivos móveis[cite: 42]. | Usabilidade[cite: 42] | Geral[cite: 42] | Essencial[cite: 42] |
| **RNF04** | O sistema deve oferecer tema escuro opcional para melhor experiência do usuário[cite: 42]. | Usabilidade[cite: 42] | Geral[cite: 42] | Desejável[cite: 42] |

### 2.3. Regras de Negócio

| Identificador | Descrição | Escopo | Prioridade |
| :--- | :--- | :--- | :--- |
| **RN01** | A reserva online de uma quadra só é confirmada mediante o pagamento prévio de no mínimo 50% do valor do horário[cite: 42]. | Agendamento[cite: 42] | Essencial[cite: 42] |
| **RN02** | Cancelamentos de reservas com direito a reembolso ou crédito só podem ser efetuados com até 6 horas de antecedência do horário agendado[cite: 42]. | Agendamento[cite: 42] | Importante[cite: 42] |
| **RN03** | O mesmo horário de uma quadra não pode ser reservado por dois clientes simultaneamente[cite: 42]. | Agendamento[cite: 42] | Essencial[cite: 42] |
| **RN04** | O horário selecionado fica pré-reservado por 10 minutos; caso o pagamento não seja concluído nesse período, a vaga é liberada automaticamente para a agenda[cite: 42]. | Agendamento[cite: 42] | Importante[cite: 42] |
| **RN05** | Clientes que realizarem mais de 5 reservas no mesmo mês recebem 10% de desconto no valor do próximo agendamento[cite: 42]. | Financeiro[cite: 42] | Desejável[cite: 42] |

---

## 3. Diagramas UML

### 3.1. Diagramas de Casos de Uso

```mermaid
flowchart LR
    Atleta((Atleta))
    
    subgraph Sistema ArenaSports
        UC1([Cadastrar])
        UC2([Logar])
        UC3([Consultar Horários])
        UC4([Reservar Quadra])
        UC5([Alugar Materiais])
        UC6([Cancelar])
        UC7([Recuperar Senha])
        UC8([Bloquear Horário])
    end

    Atleta --- UC1
    UC2 -.->|"<<include>>"| UC1
    UC4 -.->|"<<include>>"| UC2
    UC4 -.->|"<<include>>"| UC3
    UC5 -.->|"<<extend>>"| UC4
    UC6 -.->|"<<extend>>"| UC4
    UC7 -.->|"<<extend>>"| UC2
    UC8 -.->|"<<include>>"| UC2