# Estudo de Viabilidade — EXEMPLO RESOLVIDO

> Este arquivo é só uma referência de formato e de profundidade esperada, usando o sistema de reservas de quadras esportivas que já usamos como exemplo no Tópico 3. Não copiem o raciocínio abaixo para o sistema de vocês, cada sistema tem riscos e características diferentes. Usem apenas a estrutura.

## Índice

1. [Identificação](#1-identificação)
2. [O Sistema](#2-o-sistema)
3. [Viabilidade Técnica](#3-viabilidade-técnica)
4. [Viabilidade Econômica](#4-viabilidade-econômica)
5. [Viabilidade Operacional](#5-viabilidade-operacional)
6. [Conclusão](#6-conclusão)

---

## 1. Identificação

| Campo | Preencher |
|---|---|
| Grupo | Exemplo — não é um grupo real |
| Integrantes | — |
| Disciplina | Engenharia de Software I |
| Semana | 2 |
| Data | — |

## 2. O Sistema

Aplicativo de reserva de quadras esportivas, usado por academias, condomínios ou centros poliesportivos. Permite que o usuário reserve horários disponíveis, receba notificações, e que o administrador do espaço gerencie a agenda.

Requisitos já consolidados no requisitos.md deste exemplo:

| ID | Descrição |
|---|---|
| RF-01 | O sistema deve permitir que o usuário reserve uma quadra num horário disponível. |
| RF-02 | O sistema deve enviar uma notificação ao usuário confirmando a reserva, e lembrando um dia antes do horário marcado. |
| RF-03 | O sistema deve permitir que o administrador bloqueie ou libere horários manualmente. |
| RF-04 | O sistema deve armazenar os dados de cadastro e pagamento do usuário para reservas futuras. |
| RF-05 | O sistema deve calcular o preço da reserva considerando horário nobre e horário comum. |
| RF-06 | O sistema deve permitir que o usuário cancele uma reserva antes do horário marcado. |

| ID | Categoria | Descrição |
|---|---|---|
| RNF-01 | Desempenho | A confirmação da reserva deve ser processada em no máximo três segundos, mesmo em horário de pico. |
| RNF-02 | Confiabilidade | As notificações devem ter uma taxa de entrega de pelo menos 99%. |
| RNF-03 | Usabilidade | Um administrador sem treinamento técnico deve conseguir bloquear um horário em menos de um minuto. |
| RNF-04 | Segurança | Os dados de cadastro e pagamento devem ser armazenados de forma criptografada. |
| RNF-05 | Portabilidade | O aplicativo deve funcionar de forma equivalente tanto em Android quanto em iOS. |
| RNF-06 | Confiabilidade | O cancelamento deve ser refletido imediatamente na disponibilidade do horário para outros usuários. |

---

## 3. Viabilidade Técnica

A equipe fictícia deste exemplo já domina desenvolvimento de aplicativos móveis e backends simples de reserva, então a maior parte do sistema não representa risco técnico alto. Dois pontos, porém, merecem atenção.

O RNF-01 (confirmação em até três segundos, mesmo em horário de pico) exige que o banco de dados trate corretamente reservas simultâneas do mesmo horário, evitando que duas pessoas reservem a mesma quadra ao mesmo tempo. Isso é resolvível com controle de concorrência padrão de banco de dados, não é um risco alto, mas precisa ser lembrado desde o início do projeto, e não corrigido depois que o problema aparecer.

Já o RNF-04 (dados de pagamento criptografados) depende de integração com um gateway de pagamento de terceiros, e diferentes gateways têm documentação e qualidade de suporte bem diferentes entre si. Esse é o maior risco técnico identificado, mitigável escolhendo, desde o início, um provedor com boa documentação e amplamente usado no mercado, em vez de um mais barato mas pouco testado.

**Risco identificado:** concorrência na reserva do mesmo horário, e dependência de gateway de pagamento externo.
**Mitigação:** uso de transação com bloqueio no banco de dados para o primeiro; escolha cuidadosa e testes antecipados de integração para o segundo.

## 4. Viabilidade Econômica

O custo principal está no desenvolvimento inicial do aplicativo (equipe pequena, app mobile mais backend) e na manutenção contínua, principalmente da parte de pagamentos, que costuma exigir mais atenção de segurança ao longo do tempo.

O benefício esperado é a redução do trabalho manual da recepção, que hoje provavelmente organiza reservas por telefone ou papel, além da possibilidade de cobrar uma pequena taxa de conveniência por reserva feita pelo aplicativo, o que pode ajudar a custear a manutenção do sistema.

Dado que o custo de manutenção é recorrente, mas moderado, e o benefício (economia de tempo da recepção, redução de erros de agenda, e possível receita extra) é contínuo, o investimento parece se justificar, especialmente para espaços com volume razoável de reservas diárias.

## 5. Viabilidade Operacional

Os usuários finais (o público que reserva quadras) já estão bastante familiarizados com aplicativos parecidos no dia a dia, como apps de delivery ou transporte, então a curva de aprendizado deve ser pequena para a maioria.

O maior ponto de atenção operacional está do lado do administrador do espaço, tipicamente alguém como um zelador ou recepcionista, que pode não ter familiaridade nenhuma com sistemas digitais. É exatamente por isso que o RNF-03 (bloquear horário em menos de um minuto, sem treinamento) existe, ele é uma resposta direta a esse risco operacional.

Também existe uma parcela de usuários, geralmente mais velhos, que pode preferir continuar reservando por telefone. Recomenda-se manter esse canal manual em paralelo durante um período de transição, em vez de desativá-lo no lançamento do aplicativo.

## 6. Conclusão

- [ ] Viável
- [x] Viável com ressalvas
- [ ] Não viável

O projeto é tecnicamente e economicamente viável, e a maior parte da operação já é compatível com o comportamento atual dos usuários finais. As ressalvas estão concentradas em dois pontos, a escolha cuidadosa do gateway de pagamento (viabilidade técnica) e a manutenção de um canal manual de reserva durante a transição, para não excluir usuários menos familiarizados com aplicativos (viabilidade operacional).
