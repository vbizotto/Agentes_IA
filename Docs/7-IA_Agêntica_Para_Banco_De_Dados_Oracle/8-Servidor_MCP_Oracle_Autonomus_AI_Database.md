# Servidor MCP do Oracle Autonomous AI Database

## Considerações iniciais

### Visão geral

Neste trecho, vamos recapitular a arquitetura de segurança do servidor MCP do Oracle Autonomous AI Database, com foco na autenticação e no limite de segurança definido pelo próprio banco de dados.

---

# Transcrição da aula

## 1. Autenticação e limite de segurança

O cliente de IA usa credenciais normais de banco de dados. Não existe um usuário MCP separado. Assim, as permissões que o usuário possui no banco determinam o que a IA pode fazer por meio do servidor MCP.

Os controles existentes no banco de dados permanecem em vigor, incluindo:

- controle de acesso baseado em funções (RBAC);
- listas de controle de acesso (ACLs);
- políticas de segurança em nível de linha (VPD).

Por isso, o banco de dados continua sendo o limite de segurança: o servidor MCP opera dentro das permissões concedidas pelas credenciais utilizadas pelo cliente.

## 2. Recapitulando

Nesta lição, foram apresentados o servidor MCP do Oracle Autonomous AI Database, sua finalidade e sua arquitetura. A demonstração de ativação não faz parte da aula; para consultar as etapas de configuração e uso com agentes, consulte a documentação da Oracle.

## Conclusão

A autenticação do servidor MCP aproveita as credenciais e os controles de acesso do banco de dados, em vez de criar um modelo de permissões separado para o MCP.

Espero que esta lição tenha sido útil. Obrigado pelo seu tempo!
