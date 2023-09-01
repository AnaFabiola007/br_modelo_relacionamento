# br_modelo_relacionamento
Cria-se entidades que armazenam seus atributos formando assim o dados de banco de dados 
/* Lógico_1: */

CREATE TABLE Cliente (
    Cliente_NSocial CHAR,
    Cliente_Nome CHAR,
    Cliente_CPF CHAR,
    Cliente_Fone CHAR,
    Cliente_RG CHAR,
    Cliente_Endereco CHAR,
    Cliente_UF CHAR,
    Cliente_CEP CHAR,
    Cliente_Bairro CHAR,
    Cliente_Email CHAR,
    Cliente_Genero CHAR,
    Cliente_Idade INTEGER,
    Cliente_Naturalidade CHAR,
    Cliente_Ecivil CHAR,
    Cliente_Profissao CHAR,
    Cliente_Salario DECIMAL,
    Cliente_Formacao CHAR,
    PRIMARY KEY (Cliente_NSocial, Cliente_Nome, Cliente_CPF, Cliente_RG)
);

CREATE TABLE Produtos (
    Produto_ID INTEGER,
    Produto_Descricao CHAR,
    Produto_Qtd NUMERIC,
    Produto_ValCompra DECIMAL,
    Produto_ValVenda DECIMAL,
    Produto_Fornecedor CHAR,
    Produto_Validade DATE,
    Produto_NF CHAR,
    Produto_DUCompra DATE,
    Produto__Obs CHAR,
    PRIMARY KEY (Produto_ID, Produto_Descricao, Produto_Fornecedor)
);

CREATE TABLE Pedido (
    Pedido_ID INTEGER,
    Pedido_Data DATE,
    Pedido_Hora CHAR,
    Pedido_CodPedido NUMERIC,
    Pedido_ValCupom DECIMAL,
    Pedido_TipoPague CHAR,
    PRIMARY KEY (Pedido_ID, Pedido_Data, Pedido_CodPedido)
);

CREATE TABLE Estacionamento (
    Estacionamento_ID INTEGER,
    Estacionamento_CodFunc INTEGER,
    Estacionamento_PlacaCarro CHAR,
    Estacionamento_Flamula CHAR,
    Estacionamento_Nvaga CHAR,
    PRIMARY KEY (Estacionamento_ID, Estacionamento_CodFunc, Estacionamento_PlacaCarro, Estacionamento_Flamula, Estacionamento_Nvaga)
);

CREATE TABLE Funcionarios (
    Funcionarios_ID INTEGER,
    Funcionarios_NSocial CHAR,
    Funcionarios_Nome CHAR,
    Funcionarios_CodFunc INTEGER,
    Funcionarios_CPF CHAR,
    Funcionarios_RG CHAR,
    Funcionarios_Cargo CHAR,
    Funcionarios_Salario DECIMAL,
    Funcionarios_Dependentes CHAR,
    Funcionarios_DescontarIMP BOOLEAN,
    Funcionarios_DescontarVt BOOLEAN,
    Funcionarios_Convenio BOOLEAN,
    Funcionarios_Horario CHAR,
    Funcionarios_Pensao BOOLEAN,
    Funcionarios_EstadoCivil CHAR,
    Funcionarios_DtaAdmissao DATE,
    PRIMARY KEY (Funcionarios_ID, Funcionarios_NSocial, Funcionarios_Nome, Funcionarios_CodFunc, Funcionarios_CPF)
);

CREATE TABLE ItensPedido (
    ItensPedido_ID INTEGER,
    ItensPedido_CodPedido NUMERIC,
    ItensPedido_IDProduto INTEGER,
    ItensPedido_ValVenda DECIMAL,
    ItensPedido_Qtd DECIMAL,
    PRIMARY KEY (ItensPedido_ID, ItensPedido_CodPedido, ItensPedido_IDProduto)
);

CREATE TABLE Possui (
    fk_Cliente_Cliente_NSocial CHAR,
    fk_Cliente_Cliente_Nome CHAR,
    fk_Cliente_Cliente_CPF CHAR,
    fk_Cliente_Cliente_RG CHAR,
    fk_Pedido_Pedido_ID INTEGER,
    fk_Pedido_Pedido_Data DATE,
    fk_Pedido_Pedido_CodPedido NUMERIC
);

CREATE TABLE PossuiPedidos (
    fk_ItensPedido_ItensPedido_ID INTEGER,
    fk_ItensPedido_ItensPedido_CodPedido NUMERIC,
    fk_ItensPedido_ItensPedido_IDProduto INTEGER,
    fk_Pedido_Pedido_ID INTEGER,
    fk_Pedido_Pedido_Data DATE,
    fk_Pedido_Pedido_CodPedido NUMERIC
);

CREATE TABLE PossuiProdutos (
    fk_Produtos_Produto_ID INTEGER,
    fk_Produtos_Produto_Descricao CHAR,
    fk_Produtos_Produto_Fornecedor CHAR,
    fk_ItensPedido_ItensPedido_ID INTEGER,
    fk_ItensPedido_ItensPedido_CodPedido NUMERIC,
    fk_ItensPedido_ItensPedido_IDProduto INTEGER
);

CREATE TABLE PossuiVaga (
    fk_Funcionarios_Funcionarios_ID INTEGER,
    fk_Funcionarios_Funcionarios_NSocial CHAR,
    fk_Funcionarios_Funcionarios_Nome CHAR,
    fk_Funcionarios_Funcionarios_CodFunc INTEGER,
    fk_Funcionarios_Funcionarios_CPF CHAR,
    fk_Estacionamento_Estacionamento_ID INTEGER,
    fk_Estacionamento_Estacionamento_CodFunc INTEGER,
    fk_Estacionamento_Estacionamento_PlacaCarro CHAR,
    fk_Estacionamento_Estacionamento_Flamula CHAR,
    fk_Estacionamento_Estacionamento_Nvaga CHAR
);
 
ALTER TABLE Possui ADD CONSTRAINT FK_Possui_1
    FOREIGN KEY (fk_Cliente_Cliente_NSocial, fk_Cliente_Cliente_Nome, fk_Cliente_Cliente_CPF, fk_Cliente_Cliente_RG)
    REFERENCES Cliente (Cliente_NSocial, Cliente_Nome, Cliente_CPF, Cliente_RG)
    ON DELETE RESTRICT;
 
ALTER TABLE Possui ADD CONSTRAINT FK_Possui_2
    FOREIGN KEY (fk_Pedido_Pedido_ID, fk_Pedido_Pedido_Data, fk_Pedido_Pedido_CodPedido)
    REFERENCES Pedido (Pedido_ID, Pedido_Data, Pedido_CodPedido)
    ON DELETE RESTRICT;
 
ALTER TABLE PossuiPedidos ADD CONSTRAINT FK_PossuiPedidos_1
    FOREIGN KEY (fk_ItensPedido_ItensPedido_ID, fk_ItensPedido_ItensPedido_CodPedido, fk_ItensPedido_ItensPedido_IDProduto)
    REFERENCES ItensPedido (ItensPedido_ID, ItensPedido_CodPedido, ItensPedido_IDProduto)
    ON DELETE RESTRICT;
 
ALTER TABLE PossuiPedidos ADD CONSTRAINT FK_PossuiPedidos_2
    FOREIGN KEY (fk_Pedido_Pedido_ID, fk_Pedido_Pedido_Data, fk_Pedido_Pedido_CodPedido)
    REFERENCES Pedido (Pedido_ID, Pedido_Data, Pedido_CodPedido)
    ON DELETE SET NULL;
 
ALTER TABLE PossuiProdutos ADD CONSTRAINT FK_PossuiProdutos_1
    FOREIGN KEY (fk_Produtos_Produto_ID, fk_Produtos_Produto_Descricao, fk_Produtos_Produto_Fornecedor)
    REFERENCES Produtos (Produto_ID, Produto_Descricao, Produto_Fornecedor)
    ON DELETE RESTRICT;
 
ALTER TABLE PossuiProdutos ADD CONSTRAINT FK_PossuiProdutos_2
    FOREIGN KEY (fk_ItensPedido_ItensPedido_ID, fk_ItensPedido_ItensPedido_CodPedido, fk_ItensPedido_ItensPedido_IDProduto)
    REFERENCES ItensPedido (ItensPedido_ID, ItensPedido_CodPedido, ItensPedido_IDProduto)
    ON DELETE SET NULL;
 
ALTER TABLE PossuiVaga ADD CONSTRAINT FK_PossuiVaga_1
    FOREIGN KEY (fk_Funcionarios_Funcionarios_ID, fk_Funcionarios_Funcionarios_NSocial, fk_Funcionarios_Funcionarios_Nome, fk_Funcionarios_Funcionarios_CodFunc, fk_Funcionarios_Funcionarios_CPF)
    REFERENCES Funcionarios (Funcionarios_ID, Funcionarios_NSocial, Funcionarios_Nome, Funcionarios_CodFunc, Funcionarios_CPF)
    ON DELETE RESTRICT;
 
ALTER TABLE PossuiVaga ADD CONSTRAINT FK_PossuiVaga_2
    FOREIGN KEY (fk_Estacionamento_Estacionamento_ID, fk_Estacionamento_Estacionamento_CodFunc, fk_Estacionamento_Estacionamento_PlacaCarro, fk_Estacionamento_Estacionamento_Flamula, fk_Estacionamento_Estacionamento_Nvaga)
    REFERENCES Estacionamento (Estacionamento_ID, Estacionamento_CodFunc, Estacionamento_PlacaCarro, Estacionamento_Flamula, Estacionamento_Nvaga)
    ON DELETE RESTRICT;
