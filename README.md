# 🛠️ SM7 - Engenharia de Software e IA com Bubble.io

## 📝 Visão Geral do Projeto
O **OrcaFlow** é um sistema de gestão de orçamentos empresariais desenvolvido integralmente na plataforma **Bubble.io**. O foco deste projeto não foi apenas a interface, mas a aplicação rigorosa de boas práticas de engenharia: modelagem de dados escalável, segurança de acesso e planejamento de arquitetura para evitar dependência tecnológica excessiva.

Projeto desenvolvido para a disciplina de **Engenharia de Software e IA (2026.1)**.

---

## 🗃️ Arquitetura de Dados e Modelagem
A estrutura foi desenhada para suportar operações complexas (N:N), garantindo integridade e performance:

| Entidade | Responsabilidade | Relacionamento |
| :--- | :--- | :--- |
| **User** | Gestão de perfis (Admin, Vendedor, Visualizador). | - |
| **Client** | Armazenamento de dados cadastrais de clientes. | 1:N com Orçamentos |
| **Quote** | Cabeçalho do orçamento (Status, Valor, Validade). | N:1 com Itens |
| **QuoteItem** | Detalhamento de produtos/serviços e preços unitários. | N:1 com Orçamento |

> **Diretriz Técnica:** Seguindo padrões de normalização, as Foreign Keys (FKs) foram mantidas no lado N da relação para evitar listas extensas de objetos, otimizando o carregamento do banco de dados.

---

## 🔐 Segurança e Regras de Privacidade (Privacy Rules)
Para garantir o isolamento de dados entre diferentes usuários (Multi-tenancy), configuramos regras granulares no servidor do Bubble:
* **Privacidade do Cliente:** `This Client's Creator is Current User`
* **Privacidade do Orçamento:** `This Quote's Creator is Current User`
* **Integridade:** Itens de orçamento só são acessíveis se o criador do orçamento pai for o usuário atual.

---

## ⚙️ Workflows e Experiência do Usuário (UX)
O sistema implementa 11 workflows principais que gerenciam o ciclo de vida do orçamento (Criação, Edição, Exclusão e Cancelamento). Cada operação inclui feedback visual e validação de campos obrigatórios para prevenir erros de entrada.

---

## 🚨 Estratégia de Saída (Mitigação de Vendor Lock-in)
Como o Bubble retém o código-fonte, estabelecemos uma estratégia de saída via **Data API** para garantir a propriedade dos dados:
* **Exportação:** Acesso via requisições GET autenticadas para extração de registros em JSON.
* **Stack de Migração Planejada:** Backend em Node.js, Banco de Dados PostgreSQL e Frontend em React.

---

## 📊 Resultados e Aprendizados
* **Full CRUD:** Implementação completa de criação, leitura, atualização e exclusão.
* **Pensamento Arquitetural:** Compreensão de que a Engenharia de Software reside na lógica e na segurança, independentemente do uso de código ou no-code.
* **Continuidade de Negócio:** Desenvolvimento de visão crítica sobre dependência de plataformas (Vendor Lock-in).

---
