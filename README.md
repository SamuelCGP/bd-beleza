# bd-beleza
Indústria Beleza LTDA


### Criação

```sql
USE industriaBeleza;

CREATE TABLE Cliente(
	id_cliente INT IDENTITY(1,1),
	cpf VARCHAR(50),
	rg VARCHAR(50),
	nome VARCHAR(50),
	PRIMARY KEY (id_cliente)
);

CREATE TABLE Item(
	id_item INT IDENTITY(1,1),
	nome VARCHAR(50),
	tipo VARCHAR(50),
	valor VARCHAR(50),
	PRIMARY KEY (id_item)
)

CREATE TABLE Veiculo(
	id_veiculo INT IDENTITY(1,1),
	placa VARCHAR(20),
	marca VARCHAR(20),
	tipo VARCHAR(20),
	PRIMARY KEY (id_veiculo)
);

CREATE TABLE PontoEstrategico(
	id_ponto_estrategico INT IDENTITY(1,1),
	cep VARCHAR(20),
	endereco VARCHAR(255),
	PRIMARY KEY (id_ponto_estrategico)
);

-- tem fks --

CREATE TABLE Pedido(
	id_pedido INT IDENTITY(1,1),
	id_item INT,
	quantidade INT,
	valor_final VARCHAR(50),
	data_pedido DATE,
	PRIMARY KEY (id_pedido),
	FOREIGN KEY (id_item) REFERENCES Item(id_item)
);

CREATE TABLE Regiao(
	id_regiao INT IDENTITY(1,1),
	id_ponto_estrategico INT,
	bairro VARCHAR(50),
	cidade VARCHAR(50),
	estado VARCHAR(50),
	PRIMARY KEY (id_regiao),
	FOREIGN KEY (id_ponto_estrategico) REFERENCES PontoEstrategico(id_ponto_estrategico)
);

CREATE TABLE Vendedor(
	id_vendedor INT IDENTITY(1,1),
	id_regiao INT,
	id_veiculo INT,
	nome VARCHAR(20),
	rg VARCHAR(20),
	cpf VARCHAR(20),
	PRIMARY KEY (id_vendedor),
	FOREIGN KEY (id_regiao) REFERENCES Regiao(id_regiao),
	FOREIGN KEY (id_veiculo) REFERENCES Veiculo(id_veiculo)
);

CREATE TABLE NotaFiscal(
	id_nota_fiscal INT IDENTITY(1,1),
	id_vendedor INT,
	id_pedido INT,
	id_cliente INT,
	PRIMARY KEY (id_nota_fiscal),
	FOREIGN KEY (id_vendedor) REFERENCES Vendedor(id_vendedor),
	FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido),
	FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);
```

### INSERTS

```sql
USE industriaBeleza;

-- cliente --
INSERT INTO cliente(cpf, rg, nome) VALUES ('12345678','12345678','cliente1');
INSERT INTO cliente(cpf, rg, nome) VALUES ('54316745','54316745','cliente2');
INSERT INTO cliente(cpf, rg, nome) VALUES ('95739274','95739274','cliente3');
INSERT INTO cliente(cpf, rg, nome) VALUES ('67623943','67623943','cliente4');
INSERT INTO cliente(cpf, rg, nome) VALUES ('76949573','76949573','cliente5');

-- item --
INSERT INTO item(nome, tipo, valor) VALUES ('sabonete','higiene','20');
INSERT INTO item(nome, tipo, valor) VALUES ('shampoo','higiene','80');
INSERT INTO item(nome, tipo, valor) VALUES ('delineador','maquiagem','20');
INSERT INTO item(nome, tipo, valor) VALUES ('máscara','higiene','15');
INSERT INTO item(nome, tipo, valor) VALUES ('base','maquiagem','30');

-- veiculo --
INSERT INTO veiculo(placa, marca, tipo) VALUES ('CAR-1A11','fiat','carro');
INSERT INTO veiculo(placa, marca, tipo) VALUES ('HGF-5f22','corsa','carro');
INSERT INTO veiculo(placa, marca, tipo) VALUES ('TRU-CK11','volkswagen','caminhonete');
INSERT INTO veiculo(placa, marca, tipo) VALUES ('TRU-CKER','volkswagen','caminhonete');
INSERT INTO veiculo(placa, marca, tipo) VALUES ('BIK-ER13','ferrari','moto');

-- pontoestrategico --
INSERT INTO pontoestrategico(cep, endereco) VALUES ('01010-100','rua grande falcão');
INSERT INTO pontoestrategico(cep, endereco) VALUES ('45034-100','rua menor sapo');
INSERT INTO pontoestrategico(cep, endereco) VALUES ('12321-100','rua rio molhado');
INSERT INTO pontoestrategico(cep, endereco) VALUES ('76543-100','rua sal gado');
INSERT INTO pontoestrategico(cep, endereco) VALUES ('45129-100','rua google plex');

-- pedido --
INSERT INTO pedido(id_item, quantidade, valor_final, data_pedido) VALUES (1,1,'20','01-05-2021');
INSERT INTO pedido(id_item, quantidade, valor_final, data_pedido) VALUES (2,1,'80','02-04-2022');
INSERT INTO pedido(id_item, quantidade, valor_final, data_pedido) VALUES (3,2,'40','03-03-2021');
INSERT INTO pedido(id_item, quantidade, valor_final, data_pedido) VALUES (4,1,'15','04-02-2022');
INSERT INTO pedido(id_item, quantidade, valor_final, data_pedido) VALUES (5,3,'90','05-01-2021');

-- regiao --
INSERT INTO regiao(id_ponto_estrategico, bairro, cidade, estado) VALUES (1,'bairro1','são paulo','sp');
INSERT INTO regiao(id_ponto_estrategico, bairro, cidade, estado) VALUES (2,'bairro2','diurno santo','es');
INSERT INTO regiao(id_ponto_estrategico, bairro, cidade, estado) VALUES (3,'bairro3','são treco','rj');
INSERT INTO regiao(id_ponto_estrategico, bairro, cidade, estado) VALUES (4,'bairro4','general ornstein','am');
INSERT INTO regiao(id_ponto_estrategico, bairro, cidade, estado) VALUES (5,'bairro5','executor smough','pa');

-- vendedor --
INSERT INTO vendedor(id_regiao, id_veiculo, nome, rg, cpf) VALUES (1,1,'Claus','66666666','66666666');
INSERT INTO vendedor(id_regiao, id_veiculo, nome, rg, cpf) VALUES (2,2,'Ustra','33333333','33333333');
INSERT INTO vendedor(id_regiao, id_veiculo, nome, rg, cpf) VALUES (3,3,'Peixoto','22222222','22222222');
INSERT INTO vendedor(id_regiao, id_veiculo, nome, rg, cpf) VALUES (4,4,'Roger','77777777','77777777');
INSERT INTO vendedor(id_regiao, id_veiculo, nome, rg, cpf) VALUES (5,5,'Pablo','99999999','99999999');

-- notafiscal --
INSERT INTO notafiscal(id_vendedor, id_pedido, id_cliente) VALUES (1,1,1);
INSERT INTO notafiscal(id_vendedor, id_pedido, id_cliente) VALUES (2,2,2);
INSERT INTO notafiscal(id_vendedor, id_pedido, id_cliente) VALUES (3,3,3);
INSERT INTO notafiscal(id_vendedor, id_pedido, id_cliente) VALUES (4,4,4);
INSERT INTO notafiscal(id_vendedor, id_pedido, id_cliente) VALUES (5,5,5);
```

### Consultas

```sql
-- seleciona o nome do vendedor e o bairro da região que ele é responsável --
SELECT vendedor.nome AS 'vendedor', regiao.bairro AS 'região' 
FROM vendedor
INNER JOIN regiao ON vendedor.id_regiao=regiao.id_ponto_estrategico;

-- seleciona o id do pedido cujo cliente tem um nome específico --
SELECT notafiscal.id_pedido
FROM notafiscal
WHERE EXISTS
  (SELECT cliente.nome
  FROM cliente
  WHERE notafiscal.id_cliente = cliente.id_cliente AND cliente.nome = 'cliente1');

-- Seleciona os pedidos que custaram mais do que 30 reais --
SELECT * FROM pedido WHERE pedido.valor_final > 30;
```
