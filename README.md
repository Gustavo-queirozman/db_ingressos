<h1>DB ingressos</h1>

Banco de dados SQL para plataforma de ingressos

<h2>Modelo Conceitual</h2>
<img src="https://raw.githubusercontent.com/Gustavo-queirozman/db_ingressos/main/MODELO_CONCEITUAL.png"/>

<h2>Modelo Lógico</h2>
<img src="https://raw.githubusercontent.com/Gustavo-queirozman/db_ingressos/main/MODELO_LOGICO.png"/>

<h2>Modelo Físico</h2>
<pre>

CREATE TABLE cliente (
    idCliente INTEGER PRIMARY KEY AUTO_INCREMENT,
    cpf VARCHAR(15),
    nome VARCHAR(255),
    whatsapp VARCHAR(10),
    email VARCHAR(256),
    senha VARCHAR(255),
    dataHoraCriacao DATETIME
);

CREATE TABLE produtor (
    idProdutor INTEGER PRIMARY KEY AUTO_INCREMENT,
    cnpj VARCHAR(20),
    nome VARCHAR(255),
    whatsapp VARCHAR(10),
    email VARCHAR(256),
    senha VARCHAR(255),
    dataHoraCriacao DATETIME
);

CREATE TABLE evento (
    idEvento INTEGER PRIMARY KEY AUTO_INCREMENT,
    nomeEvento VARCHAR(255),
    localEvento VARCHAR(255),
    dataEvento DATE,
    dataHoraCriacao DATETIME,
    fkProdutor INTEGER
);

CREATE TABLE ingresso (
    idIngresso INTEGER PRIMARY KEY AUTO_INCREMENT,
    tipoIngresso VARCHAR(255),
    quantidadeIngressos INTEGER,
    valorIngresso DOUBLE,
    fkCliente INTEGER,
    fkEvento INTEGER
);

CREATE TABLE combo (
    idCombo INTEGER PRIMARY KEY AUTO_INCREMENT,
    nomeCombo VARCHAR(255),
    valorComDesconto DOUBLE,
    valorTotal DOUBLE
);

CREATE TABLE produto (
    idProduto INTEGER PRIMARY KEY AUTO_INCREMENT,
    nomeProduto VARCHAR(255),
    precoUnitario DOUBLE,
    quantidadeDisponivel INTEGER,
    fotoProduto VARCHAR(255)
);

CREATE TABLE produtoCombo (
    idProdutoCombo INTEGER PRIMARY KEY AUTO_INCREMENT,
    fkCombo INTEGER,
    fkProduto INTEGER,
    quantidade INTEGER,
    descontoUnitario DOUBLE,
    valorUnitario DOUBLE
);

CREATE TABLE ingressoCombo (
    idIngressoCombo INTEGER PRIMARY KEY AUTO_INCREMENT,
    fkIngresso INTEGER,
    fkCombo INTEGER,
    quantidade INTEGER,
    descontoUnitario DOUBLE,
    valorUnitario DOUBLE
);
 
ALTER TABLE evento ADD CONSTRAINT FK_evento_2
    FOREIGN KEY (fkProdutor)
    REFERENCES produtor (idProdutor)
    ON DELETE RESTRICT;
 
ALTER TABLE ingresso ADD CONSTRAINT FK_ingresso_2
    FOREIGN KEY (fkCliente)
    REFERENCES cliente (idCliente)
    ON DELETE RESTRICT;
 
ALTER TABLE ingresso ADD CONSTRAINT FK_ingresso_3
    FOREIGN KEY (fkEvento)
    REFERENCES evento (idEvento)
    ON DELETE RESTRICT;
 
ALTER TABLE produtoCombo ADD CONSTRAINT FK_produtoCombo_1
    FOREIGN KEY (fkCombo)
    REFERENCES combo (idCombo)
    ON DELETE SET NULL;
 
ALTER TABLE produtoCombo ADD CONSTRAINT FK_produtoCombo_2
    FOREIGN KEY (fkProduto)
    REFERENCES produto (idProduto)
    ON DELETE SET NULL;
 
ALTER TABLE ingressoCombo ADD CONSTRAINT FK_ingressoCombo_1
    FOREIGN KEY (fkIngresso)
    REFERENCES ingresso (idIngresso)
    ON DELETE SET NULL;
 
ALTER TABLE ingressoCombo ADD CONSTRAINT FK_ingressoCombo_2
    FOREIGN KEY (fkCombo)
    REFERENCES combo (idCombo)
    ON DELETE SET NULL;
</pre>
