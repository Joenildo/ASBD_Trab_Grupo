Introdução

Este documento apresenta a estrutura da base de dados da clínica, incluindo a modelagem das tabelas, suas relações e funções adicionais implementadas para garantir a segurança e integridade dos dados.

Estrutura da Base de Dados

A base de dados foi criada sob o nome Clinica e contém as seguintes tabelas principais:

1. Utilizador

Armazena informações sobre os utilizadores do sistema, incluindo administradores, médicos, secretários e atendentes.

Campos principais: id_utilizador, nome, email, senha (encriptada), telefone, cargo, ativo, data_criacao.

A senha é encriptada usando SHA-256.

2. Atendente

Contém referências aos utilizadores que atuam como atendentes.

Relacionamento: id_utilizador refere-se à tabela Utilizador.

3. Médico

Registra os médicos da clínica e suas especialidades.

Campos principais: id_medico, id_utilizador, especialidade, CRM, telefone_clinico.

Relacionamento: id_utilizador refere-se à tabela Utilizador.

4. Paciente

Guarda informações dos pacientes cadastrados.

Campos principais: id_paciente, nome, data_nascimento, sexo, telefone, email, endereco.

5. Exame

Armazena dados sobre exames realizados por pacientes.

Campos principais: id_exame, id_paciente, id_medico, tipo_exame, resultado, data_exame.

Relacionamento: id_paciente refere-se à tabela Paciente; id_medico refere-se à tabela Médico.

6. Consulta

(Tabela a ser implementada)

7. Agendamento

Registra os agendamentos de consultas e exames.

Campos principais: id_agendamento, id_paciente, id_medico, id_atendente, id_exame, data_hora, status.

Relacionamentos: id_paciente refere-se à tabela Paciente; id_medico refere-se à tabela Médico; id_atendente refere-se à tabela Atendente; id_exame refere-se à tabela Exame.

8. Pagamento

Regista os pagamentos das consultas.

Campos principais: id_pagamento, id_consulta, valor, forma_pagamento, status, data_pagamento.

Relacionamento: id_consulta refere-se à tabela Consulta.

9. Permissões

Define os níveis de acesso para cada cargo no sistema.

Campos principais: id_permissao, cargo, pode_ver_dados_paciente, pode_gerir_exames, pode_gerir_pacientes, pode_gerir_consultas, pode_gerir_pagamentos, pode_gerir_utilizadores.

Cargos com permissões pré-definidas: Administrador, Médico, Secretária, Atendente.

Funcionalidades Extras

1. Encriptação de Senha

Foi implementada uma função EncriptarSenha que utiliza SHA-256 para armazenar as senhas de forma segura.

2. Inserção de Dados de Exemplo

Foi criado um exemplo de inserção de um administrador na tabela Utilizador, com a senha encriptada.

Considerações Finais

O sistema foi projetado para garantir a segurança e integridade dos dados, garantindo controle de acesso e estrutura modularizada. Melhorias futuras incluem a implementação da tabela Consulta, otimização de relações e desenvolvimento de um sistema de auditoria para rastrear alterações nos dados.

