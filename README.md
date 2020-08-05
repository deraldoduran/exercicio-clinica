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
