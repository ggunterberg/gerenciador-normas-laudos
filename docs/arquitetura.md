# Introdução e Objetivos

Este documento descreve diversos aspectos do produto "Gerenciador de Normas para Laudos", um software voltado a facilitar o processo de inserção de normas durante a criação de laudos técnicos.

### Motivação

A criação de laudos técnicos exige mão de obra considerável, sendo inserção das normas no documento um processo oneroso. O produto propõe redução de custos ao otimizar o tempo gasto para inserção de normas no documento.

## Contexto e Escopo

Os seguintes elementos são relevantes para o contexto negocial:
- **Editor**: O usuário que está colaborando com a criação do laudo técnico.
- **Laudo Técnico**: O documento onde as normas devem ser iseridas

### Histórias de Usuário e Requisitos Funcionais
As seguintes histórias de usuário e respectivos requisitos funcionais compõem o escopo do produto:

- Como um editor, gostaria de buscar rapidamente por uma norma específica para incluir no documento sendo criado.
  - O sistema deve listar todas as normas disponíveis de forma breve.
  - O sistema deve filtrar normas com base no título e descrição
- Como um editor, gostaria de inserir os conteúdos de uma norma selecionada no documento sendo criado para reduzir o trabalho de edição.
  - O sistema deve permitir copiar os conteúdos, incluindo imagens, em um formato que possa ser colado em editores de texto.
- Como um editor, gostaria de visualizar os detalhes de uma norma para avaliar se a norma se refere ao que é necessário no laudo técnico.
  - O sistema deve permitir visualizar todos os detalhes referentes a uma norma.

## Arquitetura 

### Objetivos de Qualidade e Estratégia de solução

Os seguintes pontos são objetivos de qualidade e suas respectivas soluções:

- *Flexibilidade*: O sistema deve ser portável para soluções integradas mais próximas das ferramentas utilizadas pelos editores
  - As ferramentas consideradas (Google Docs e Office 365) oferecem interfaces de extensão a partir de javascript, contanto que a aplicação consista em assets html/css/javascript estáticos, por isso será utilizado SPA+SSG para criação do sistema.
- *Facilidade de uso*: O sistema deve ser acessível e intuitivo para o usuário comum ser capaz de utilizá-lo em menos de 10 minutos.
  - Disponibilizar o sistema como um site permite fácil acesso a maior parte dos usuários. Para simplificar o aprendizado do usuário no sistema a aplicação deve aderir a padrões de design minimalistas que priorizem facilidade de uso.

### Visão de Implantação

[Pendente]

