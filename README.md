# Relatório do Sistema de Gestão da Clínica

## 1. Introdução
Este documento apresenta a estrutura da base de dados do sistema de gestão da clínica. O sistema foi concebido para gerir utilizadores, pacientes, consultas, exames, agendamentos e pagamentos, garantindo segurança e eficiência no armazenamento e manipulação dos dados.

## 2. Estrutura da Base de Dados
A base de dados foi criada com o nome `Clinica` e contém as seguintes tabelas principais:

### 2.1 Utilizador
Tabela para armazenar os dados dos utilizadores do sistema, incluindo encriptação de senha.

**Campos:**
- `id_utilizador` (Chave primária)
- `nome`
- `email` (Único)
- `senha` (Encriptada com SHA256)
- `telefone`
- `cargo` (Administrador, Médico, Secretária, Atendente)
- `ativo` (Booleano)
- `data_criacao` (Data e hora da criação do registo)

### 2.2 Atendente e Médico
Tabelas separadas para armazenar a associação de utilizadores aos seus respetivos papéis na clínica.

### 2.3 Paciente
Tabela para armazenar informações dos pacientes.

**Campos:**
- `id_paciente` (Chave primária)
- `nome`
- `data_nascimento`
- `sexo` (M/F)
- `telefone`
- `email`
- `endereco`

### 2.4 Exame
Tabela para registar exames realizados pelos pacientes.

**Campos:**
- `id_exame` (Chave primária)
- `id_paciente` (Chave estrangeira)
- `id_medico` (Chave estrangeira)
- `tipo_exame`
- `resultado`
- `data_exame`

### 2.5 Agendamento
Tabela para gerir marcações de consultas e exames.

**Campos:**
- `id_agendamento` (Chave primária)
- `id_paciente` (Chave estrangeira)
- `id_medico` (Chave estrangeira)
- `id_atendente` (Chave estrangeira)
- `id_exame` (Opcional, chave estrangeira)
- `data_hora`
- `status` (Agendado, Cancelado, Realizado)

### 2.6 Pagamento
Tabela para registar os pagamentos efetuados pelos pacientes.

**Campos:**
- `id_pagamento` (Chave primária)
- `id_consulta` (Chave estrangeira)
- `valor`
- `forma_pagamento` (Dinheiro, Cartão, Convênio)
- `status` (Pago, Pendente)
- `data_pagamento`

### 2.7 Permissões
Tabela para gerir permissões de acesso com base no cargo dos utilizadores.

**Campos:**
- `id_permissao` (Chave primária)
- `cargo`
- `pode_ver_dados_paciente`
- `pode_gerir_exames`
- `pode_gerir_pacientes`
- `pode_gerir_consultas`
- `pode_gerir_pagamentos`
- `pode_gerir_utilizadores`

### 2.8 Segurança: Encriptação de Senhas
Foi criada a função `dbo.EncriptarSenha` que utiliza SHA256 para encriptar as senhas dos utilizadores.

**Exemplo de inserção de utilizador com senha encriptada:**
```sql
DECLARE @senha NVARCHAR(100) = 'senhaExemplo';
INSERT INTO Utilizador (nome, email, senha, telefone, cargo, ativo, data_criacao)
VALUES ('João Silva', 'joao@clinica.com', dbo.EncriptarSenha(@senha), '123456789', 'Administrador', 1, GETDATE());
```

## 3. Conclusão
O sistema de gestão da clínica foi estruturado para garantir segurança, organização e eficiência no tratamento das informações dos pacientes e profissionais da clínica. Com tabelas bem definidas e um modelo de permissões robusto, a gestão dos dados será segura e eficaz.
