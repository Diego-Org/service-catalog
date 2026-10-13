markdown

# service-catalog

Componente responsável pelo domínio de **Catálogo de Serviços** do Marketplace para Serviços de Beleza.

Centraliza as categorias e as ofertas de serviços dos profissionais, incluindo nome, preço e duração, para apoiar a consulta e a contratação na plataforma.

## Objetivo

Organizar os serviços disponíveis e permitir que cada profissional gerencie suas próprias ofertas, preservando a consistência das informações utilizadas pelos demais domínios.

## Responsabilidades

- Disponibilizar a consulta de categorias e serviços.
- Permitir o cadastro, a alteração e a remoção de ofertas pelo profissional responsável.
- Vincular cada oferta ao profissional que a oferece.
- Manter nome, categoria, preço e duração de cada oferta.
- Permitir que administradores gerenciem categorias e serviços de referência.
- Preservar as referências necessárias ao histórico de agendamentos.
- Fornecer informações do catálogo aos domínios de Perfis, Busca e Agendamentos.

## Escopo funcional

| Caso de uso | Funcionalidade                   | Escopo |
| ----------- | -------------------------------- | ------ |
| UC-CAT-01   | Consultar categorias e serviços  | MVP    |
| UC-CAT-02   | Cadastrar serviço oferecido      | MVP    |
| UC-CAT-03   | Alterar serviço oferecido        | MVP    |
| UC-CAT-04   | Remover serviço oferecido        | MVP    |
| UC-CAT-05   | Gerenciar categorias do catálogo | MVP    |

Requisitos relacionados: **RF-PRO-02 — Serviços**, **RF-PRO-03 — Preço e duração** e **RF-ADM-03 — Categorias**.

## Atores

| Ator          | Relação com o domínio                                              |
| ------------- | ------------------------------------------------------------------ |
| Visitante     | Consulta as categorias e os serviços disponíveis publicamente.     |
| Cliente       | Consulta serviços para escolher um atendimento.                    |
| Profissional  | Consulta o catálogo e gerencia suas próprias ofertas.              |
| Administrador | Gerencia categorias e serviços de referência mediante autorização. |

## Conceitos do domínio

| Conceito              | Descrição                                                                             |
| --------------------- | ------------------------------------------------------------------------------------- |
| Categoria             | Classificação utilizada para organizar os serviços.                                   |
| Serviço de referência | Serviço mantido no catálogo pela administração, quando aplicável.                     |
| Oferta de serviço     | Serviço oferecido por um profissional, com nome, categoria, preço e duração próprios. |

A estrutura de categorias deve organizar o catálogo sem obrigar todos os profissionais a adotar exatamente a mesma granularidade de serviços.

## Regras de negócio

### Cadastro de ofertas

- **RB-03:** todo serviço deve possuir nome, categoria, preço e duração.
- **RB-04:** um profissional pode oferecer diversos serviços.
- **RB-05:** profissionais diferentes podem oferecer o mesmo serviço com preços, durações e condições diferentes.
- **RB-06:** a plataforma deve possuir categorias sem impor uma granularidade única aos serviços dos profissionais.
- A categoria selecionada deve ser válida para o cadastro.
- Preço e duração devem atender aos critérios definidos pela plataforma.
- A oferta deve ser vinculada ao profissional responsável.

### Alteração e remoção

- Somente o profissional autorizado pode alterar ou remover suas ofertas.
- Alterações de preço, duração ou outras condições não devem modificar silenciosamente as condições de reservas já realizadas.
- A remoção deve retirar a oferta das opções disponíveis para novas contratações.
- O histórico e as referências de agendamentos devem ser preservados.
- Agendamentos futuros devem ser considerados antes da remoção, conforme a regra de negócio definida.

### Gerenciamento de categorias

- Operações administrativas exigem autenticação e autorização.
- Categorias podem ser criadas, alteradas ou desativadas conforme as operações disponibilizadas.
- Alterações devem preservar a integridade das ofertas já associadas.

### Disponibilização para contratação

O cadastro de uma oferta não habilita automaticamente o profissional para contratação. Essa habilitação pertence ao domínio de Perfis e Profissionais e depende dos critérios definidos pelo produto, incluindo a existência de pelo menos um serviço cadastrado.

## Limites do domínio

| Responsabilidade                                | Domínio responsável      |
| ----------------------------------------------- | ------------------------ |
| Categorias e ofertas, incluindo preço e duração | Catálogo de Serviços     |
| Contas, autenticação e permissões               | Identidade e Acesso      |
| Perfil público e habilitação profissional       | Perfis e Profissionais   |
| Pesquisa, filtros e ordenação de resultados     | Descoberta e Busca       |
| Horários disponíveis e bloqueios                | Agenda e Disponibilidade |
| Reservas e condições acordadas no agendamento   | Agendamentos             |
| Cobranças, transações e recebimentos            | Pagamentos               |

O catálogo fornece o preço da oferta. O processamento financeiro pertence ao domínio de Pagamentos. A duração informa o tempo previsto do atendimento; a disponibilidade de horários pertence ao domínio de Agenda e Disponibilidade.

## Fluxos principais

### Consultar catálogo

1. O usuário solicita a consulta.
2. O sistema recupera as categorias e os serviços disponíveis.
3. Apresenta os resultados.
4. O usuário seleciona uma categoria ou serviço para consultar os detalhes.

### Cadastrar oferta

1. O profissional autenticado solicita o cadastro.
2. Informa nome, categoria, preço e duração.
3. O sistema valida os dados e a permissão.
4. Registra a oferta vinculada ao profissional.
5. Confirma o cadastro.

### Alterar oferta

1. O profissional seleciona uma oferta própria.
2. Altera os dados permitidos.
3. O sistema valida as informações e as regras de consistência.
4. Salva a alteração sem modificar silenciosamente reservas existentes.
5. Confirma a atualização.

### Remover oferta

1. O profissional solicita a remoção de uma oferta própria.
2. O sistema verifica os agendamentos relacionados.
3. Aplica as regras de remoção e preservação do histórico.
4. Retira a oferta das opções para novas contratações, quando permitido.
5. Confirma o resultado.

### Gerenciar categorias

1. O administrador autorizado acessa o catálogo.
2. Solicita a criação, alteração ou desativação de uma categoria.
3. O sistema valida os dados e as referências existentes.
4. Aplica a operação e confirma o resultado.

## Segurança e integridade

- Validar os dados no backend.
- Verificar a propriedade da oferta em operações de alteração e remoção.
- Restringir o gerenciamento de categorias a usuários autorizados.
- Preservar a integridade das referências entre categorias, ofertas e profissionais.
- Evitar perda de informações necessárias ao histórico de reservas.
- Retornar somente os dados apropriados para consulta pública.

## Arquitetura

Este README delimita o domínio do componente `service-catalog`. Os documentos fornecidos utilizam um **monólito modular orientado a domínios** como referência. A implantação como microserviço independente deve ser registrada conforme a decisão arquitetural do projeto.

A implementação deve separar regras de domínio, casos de uso e integrações técnicas. Stack, estrutura de pacotes e contratos de integração deverão refletir as decisões efetivamente adotadas pela equipe.

## Documentação técnica

Adicionar conforme a implementação:

- Tecnologias e versões utilizadas.
- Pré-requisitos e configuração local.
- Variáveis de ambiente e configuração do banco de dados.
- Comandos para inicialização e execução dos testes.
- Endpoints e contratos da API.
- Regras de autenticação e autorização.
- Formato dos erros de validação.
- Integrações com os demais domínios.

## Critérios de aceite

- [ ] Consultar categorias e serviços disponíveis.
- [ ] Retornar resultado adequado quando o catálogo estiver vazio.
- [ ] Cadastrar ofertas com nome, categoria, preço e duração válidos.
- [ ] Rejeitar ofertas com dados obrigatórios ausentes ou inválidos.
- [ ] Permitir diversas ofertas para o mesmo profissional.
- [ ] Permitir condições diferentes para serviços oferecidos por profissionais distintos.
- [ ] Permitir a alteração e a remoção de ofertas próprias.
- [ ] Impedir alteração ou remoção de ofertas de outro profissional sem autorização.
- [ ] Preservar as condições das reservas existentes após alterações no catálogo.
- [ ] Considerar agendamentos futuros antes de remover uma oferta.
- [ ] Preservar o histórico após a retirada de uma oferta.
- [ ] Restringir o gerenciamento de categorias a administradores autorizados.
- [ ] Preservar as referências existentes ao alterar ou desativar categorias.

## Decisões pendentes

- Moeda, precisão monetária e aceitação de serviços gratuitos.
- Unidade, limites e critérios de validação da duração.
- Regras para nomes duplicados de ofertas e categorias.
- Relação entre serviços de referência e ofertas personalizadas.
- Comportamento das ofertas quando uma categoria é desativada.
- Política de remoção de ofertas com agendamentos futuros.
- Mecanismo para preservar as condições acordadas nas reservas.
- Contratos de integração e implantação como serviço independente.
- teste na nova branch

## Referências

- Documento de Requisitos de Software — Marketplace para Serviços de Beleza.
- Especificação de Casos de Uso — Marketplace para Serviços de Beleza, versão 1.0.

- teste 2

> Este README descreve o escopo previsto. Os critérios de aceite não representam funcionalidades já implementadas ou testes já executados.
