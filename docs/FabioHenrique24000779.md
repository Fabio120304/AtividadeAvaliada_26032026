# Modelagem do Sistema Integrado de Gestão de Farmácia “Saúde & Vida”

**Aluno:** [SEU NOME AQUI]  
**RA:** [SEU RA AQUI]

---

# Documentação do Sistema - Rede Saúde & Vida

## 1. Regras de Negócio

As regras de negócio regem a operação da empresa, estabelecendo limites claros e garantindo a conformidade com as exigências legais do setor farmacêutico.

| ID | Descrição |
| :--- | :--- |
| **RN01** | A venda de medicamentos controlados vincula-se obrigatoriamente à validação da receita por um farmacêutico, assegurando a segurança do paciente e o cumprimento da lei. |
| **RN02** | O sistema impede a finalização de vendas sem lastro no estoque físico da unidade, coibindo furos de inventário e a frustração do cliente no ato da compra. |
| **RN03** | Vendas a prazo são restritas a consumidores com cadastro regularizado e ausência de pendências financeiras no módulo de Contas a Receber. |
| **RN04** | A entrada de notas fiscais de compra deve gerar, de forma síncrona, a atualização do estoque e o lançamento automático das obrigações no Contas a Pagar. |
| **RN05** | Alterações em preços de venda são de alçada exclusiva do perfil de Gerente, mantendo a integridade das margens de lucro e a estratégia comercial da rede. |

---

## 2. Requisitos Funcionais

Representam as capacidades que o sistema deve oferecer para atender às demandas do dia a dia.

* **RF01**: Permitir o cadastro detalhado de produtos, incluindo preço, fabricante, unidade de medida e especificações técnicas para garantir a integridade dos dados.
* **RF02**: Oferecer ferramentas de busca ágil por nome, código de barras ou fabricante, otimizando o tempo de atendimento no balcão.
* **RF03**: Realizar o abatimento automático de itens no estoque assim que a transação de venda for confirmada.
* **RF04**: Disponibilizar uma interface de cadastro rápido de clientes, evitando gargalos e filas durante o fluxo de vendas.
* **RF05**: Registrar automaticamente títulos no Contas a Receber para todas as operações faturadas ou via convênio.
* **RF06**: Emitir alertas visuais imediatos quando o volume de um item atingir o estoque crítico definido pelo gestor.
* **RF07**: Viabilizar a transferência de mercadorias entre unidades, equilibrando a disponibilidade de produtos na rede.
* **RF08**: Consolidar relatórios de fechamento de caixa por unidade ao fim de cada expediente para conciliação financeira.

---

## 3. Requisitos Não Funcionais

Atributos técnicos que garantem a performance, segurança e confiabilidade da plataforma.

* **RNF01**: O acesso deve ser restrito via login e senha, com controle de permissões baseado no nível hierárquico (RBAC).
* **RNF02**: O tempo de resposta para consultas de estoque entre filiais não deve ultrapassar 3 segundos sob condições normais de rede.
* **RNF03**: O módulo de PDV deve operar em modo contingencial (offline), sincronizando as vendas assim que a conexão for restabelecida.
* **RNF04**: Toda e qualquer movimentação manual de estoque ou estorno de venda deve gerar um rastro de auditoria imutável (logs).

---

## 4. Casos de Uso

### Tabela de Casos de Uso

| ID | Descrição | Ator | Relação |
| :--- | :--- | :--- | :--- |
| **UC01** | Efetuar Venda | Atendente | - |
| **UC02** | Consultar Produto/Estoque | Atendente | Relacionado a UC01 |
| **UC03** | Identificar Cliente | Atendente | Relacionado a UC01 |
| **UC04** | Validar Receita Médica | Farmacêutico | Relacionado a UC01 (se controlado) |
| **UC05** | Registrar Venda a Prazo | Atendente | Relacionado a UC01 |
| **UC06** | Aplicar Desconto do Gerente | Gerente | Relacionado a UC01 |
| **UC07** | Solicitar Transferência Interna | Atendente | Relacionado a UC02 (falta de estoque) |
| **UC08** | Registrar Compra (Fornecedor) | Gerente | - |
| **UC09** | Gerenciar Contas Pagar/Receber | Administrativo | - |
| **UC10** | Gerar Dashboards de Desempenho | Administrador | - |

---

## 5. Documentação do Caso de Uso Principal

**Caso de Uso:** UC01 - Realizar Venda

- **Atores:** Atendente, Farmacêutico e Gerente.
- **Pré-condição:** Usuário autenticado e terminal de caixa aberto.
- **Fluxo Principal:**
  1. O atendente inicia o checkout dos itens.
  2. O sistema valida a disponibilidade física no estoque.
  3. O cliente é identificado para fins de histórico ou convênio.
  4. Define-se a modalidade de pagamento.
  5. O sistema processa o pagamento, baixa o estoque e emite o cupom fiscal.
- **Fluxo de Exceção:**
  - **Item Controlado:** Exige a credencial do Farmacêutico para prosseguir.
  - **Ruptura de Estoque:** O sistema sugere a busca em unidades próximas.
  - **Venda Faturada:** O sistema valida o limite de crédito antes de gerar o título financeiro.

---

## 6. Diagramas de Atividade (Lógica Descritiva)

### Atividade: Fluxo de Checkout

1. **Início** -> Seleção de produtos no PDV.
2. **Triagem Legal:** Se o item for controlado, o Farmacêutico valida a receita; caso contrário, segue o fluxo.
3. **Identificação:** Verificação de cadastro prévio. Se inexistente, realiza-se o registro simplificado.
4. **Fechamento:** Escolha entre pagamento imediato (processamento direto) ou a prazo (análise de crédito e lançamento financeiro).
5. **Atualização:** O sistema ajusta o inventário em tempo real.
6. **Fim** -> Emissão do comprovante de venda.

---

## 7. Objetivo do Sistema

A implementação deste sistema visa consolidar a governança operacional da rede **Saúde & Vida**, atacando gargalos críticos como a perda de mercadorias e a falta de integração financeira. Ao automatizar a baixa de estoque em tempo real e conectar o ponto de venda diretamente ao contas a receber, eliminamos falhas manuais e garantimos que a diretoria trabalhe com dados em que possa, de fato, confiar. 

Mais do que apenas agilizar o atendimento, o software atua como uma camada de segurança jurídica, blindando a empresa contra irregularidades regulatórias que resultariam em sanções pesadas.
