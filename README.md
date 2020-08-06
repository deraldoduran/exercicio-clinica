# exercicio-clinica

CREATE TABLE paciente(
	codpac integer,
	nome varchar(255),
	endereço varchar(255),
	telefone varchar(30),
	
	CONSTRAINT paciente_pkey PRIMARY KEY (codpac)


);

CREATE TABLE IF NOT EXISTS medico(
	CRM integer,
	nome varchar(255),
	endereço varchar(255),
	telefone varchar(30),
	especialidade varchar (60),
	
	CONSTRAINT medico_pkey PRIMARY KEY (CRM)


);

CREATE TABLE IF NOT EXISTS convenio(
	codconv integer,
	nome varchar(255),
	
	
	CONSTRAINT convenio_pkey PRIMARY KEY (codconv)


);

CREATE TABLE IF NOT EXISTS consulta(
	codconsulta integer,
	data varchar(10),
	horário varchar(5),
	médico int,
	paciente int,
	convenio int,
	porcent int,
	
	CONSTRAINT consulta_pkey PRIMARY KEY (codconsulta),
	CONSTRAINT medico_fkey FOREIGN KEY (médico) REFERENCES medico (CRM),
	CONSTRAINT paciente_fkey FOREIGN KEY (paciente) REFERENCES paciente(codpac),
	CONSTRAINT convenio_fkey FOREIGN KEY (convenio) REFERENCES convenio(codconv)
	
);

CREATE TABLE IF NOT EXISTS atende(
	
	médico int,
	convenio int,
	
	CONSTRAINT atende_pkey PRIMARY KEY (médico, convenio),
	CONSTRAINT atende_fkey FOREIGN KEY (médico) REFERENCES medico (CRM),
	
	CONSTRAINT atende_fkey2 FOREIGN KEY (convenio) REFERENCES convenio(codconv)
	
);

CREATE TABLE IF NOT EXISTS possui(
	
	paciente int,
	
	convenio int,
	tipo varchar (5),
	vencimento varchar(10),
	
	
	CONSTRAINT possui_pkey PRIMARY KEY (paciente,convenio),
	CONSTRAINT possui_fkey FOREIGN KEY (paciente) REFERENCES paciente (codpac),
	CONSTRAINT possui_fkey2 FOREIGN KEY (convenio) REFERENCES convenio(codconv)
	
);

insert into paciente (codpac, nome, endereço, telefone) values (1, 'João', 'Rua 1', 98099756),
(2, 'José', 'Rua B', 36218978),(3, 'Maria', 'Rua 10', 45679872),(4, 'Joana', 'Rua J', 33439889);

insert into medico (crm, nome, endereço, telefone, especialidade) values (18739, 'Elias',
'Rua X', 87381221, 'Pediatria'), (7646, 'Ana',
'Av Z', 78291233, 'Obstetricia'), (39872, 'Pedro',
'Tv H', 98882333, 'Oftalmologia');

insert into convenio (codconv, nome) values (189, 'Cassi'),
(232, 'Unimed'),
(454, 'Santa Casa'),
(908, 'Copasa'),
(435, 'São Lucas');
 
 insert into consulta (codconsulta, data, horário, médico, paciente, convenio, porcent) 
values (1, '10/05/2013', '10:00', 18739, 1, 189, 5),
(2, '12/05/2013', '10:00', 7646, 2, 232, 10),
(3, '12/05/2013', '11:00', 18739, 3, 908, 15),
(4, '13/05/2013', '10:00', 7646, 4, 435, 13),
(5, '14/05/2013', '13:00', 7646, 2, 232, 10),
(6, '14/05/2013', '14:00', 39872, 1, 189, 5);

insert into atende (médico, convenio) values (18739, 189),
(18739, 908),
(7646, 232),
(39872, 189);

insert into possui (paciente, convenio, tipo, vencimento) values (1, 189, 'E', '31/12/2016'),
(2, 232, 'S', '31/12/2014'),
(3, 908, 'S', '31/12/2017'),
(4, 435, 'E', '31/12/2016'),
(1, 232, 'S', '31/12/2015');

*/ respostas/*

UPDATE paciente set endereço = 'rua do Bonde' WHERE nome = 'João'; 
UPDATE medico set endereço = 'rua Z' , telefone = '9838-7867' WHERE nome = 'Elias'; 
UPDATE possui set tipo = 'S' WHERE tipo = 'E';
delete from possui where paciente = 2 and convenio = 232;
delete from consulta where data = '14/05/2013' and horário = '14:00';
alter table medico rename column especialidade to especialização;
alter table convenio alter column nome type varchar(200);
alter table consulta add valor float;
update consulta set valor = 100.00;
alter table consulta alter column valor type numeric(10,2);
