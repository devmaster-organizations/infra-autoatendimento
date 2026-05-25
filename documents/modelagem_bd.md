<h1 align="center">Diagrama de Entidade-Relacionamento</h1>
<p align="center">  
  <img src="./images/DER.png"  
       alt="Diagrama ER"  -- ========================================
-- Script de Criação de Banco e Tabelas
-- SQL Server - Hapvida.Digital.Hapon
-- Para Ambiente Local
-- ========================================

-- Criar banco de dados
CREATE DATABASE [HapDigHaponDev];

USE [HapDigHaponDev];

-- ========================================
-- Tabela: Origin
-- Descrição: Origem dos orçamentos/contatos
-- ========================================
CREATE TABLE Origin (
    OriginId INT IDENTITY(1,1) NOT NULL,
    Description VARCHAR(45) NOT NULL,
    Tag VARCHAR(15) NOT NULL,
    CONSTRAINT PK_Origin PRIMARY KEY (OriginId)
);

-- ========================================
-- Tabela: BranchOffice
-- Descrição: Filiais/Áreas de atuação
-- ========================================
CREATE TABLE BranchOffice (
    AreaId INT NOT NULL,
    BranchOfficeId INT NOT NULL,
    AreaDescription VARCHAR(45) NOT NULL,
    Uf VARCHAR(2) NOT NULL,
    Hidden BIT DEFAULT 0,
    HealthInsurerId INT NULL,
    CONSTRAINT PK_BranchOffice PRIMARY KEY (AreaId)
);

-- ========================================
-- Tabela: BranchOfficePlace
-- Descrição: Localizações de filiais (com geocodificação)
-- ========================================
CREATE TABLE BranchOfficePlace (
    Id INT IDENTITY(1,1) NOT NULL,
    AreaId INT NULL,
    PlaceDescription VARCHAR(60) NOT NULL,
    Uf CHAR(2) NOT NULL,
    Latitude FLOAT NOT NULL,
    Longitude FLOAT NOT NULL,
    CONSTRAINT PK_BranchOfficePlace PRIMARY KEY (Id),
    CONSTRAINT FK_BranchOfficePlace_BranchOffice FOREIGN KEY (AreaId) REFERENCES BranchOffice(AreaId)
);

-- ========================================
-- Tabela: HealthInsurer
-- Descrição: Operadoras de saúde
-- ========================================
CREATE TABLE HealthInsurer (
    HealthInsurerId INT NOT NULL,
    Description VARCHAR(45) NOT NULL,
    CONSTRAINT PK_HealthInsurer PRIMARY KEY (HealthInsurerId)
);

-- ========================================
-- Tabela: HealthInsurerBranchOffice
-- Descrição: Vinculação entre Operadoras e Filiais
-- ========================================
CREATE TABLE HealthInsurerBranchOffice (
    HealthInsurerId INT NOT NULL,
    AreaId INT NOT NULL,
    CONSTRAINT PK_HealthInsurerBranchOffice PRIMARY KEY (HealthInsurerId, AreaId),
    CONSTRAINT FK_HealthInsurerBranchOffice_HealthInsurer FOREIGN KEY (HealthInsurerId) REFERENCES HealthInsurer(HealthInsurerId),
    CONSTRAINT FK_HealthInsurerBranchOffice_BranchOffice FOREIGN KEY (AreaId) REFERENCES BranchOffice(AreaId)
);

-- ========================================
-- Tabela: Seller
-- Descrição: Vendedores/Promotores
-- ========================================
CREATE TABLE Seller (
    SellerId INT IDENTITY(1,1) NOT NULL,
    SellerName VARCHAR(60) NULL,
    OriginId INT NOT NULL,
    BranchOfficeId INT NOT NULL,
    SalesAreaId VARCHAR(10) NULL,
    BudgetTypeId INT NULL,
    CONSTRAINT PK_Seller PRIMARY KEY (BranchOfficeId, OriginId),
    CONSTRAINT FK_Seller_Origin FOREIGN KEY (OriginId) REFERENCES Origin(OriginId)
);

-- ========================================
-- Tabela: PlansFamily
-- Descrição: Famílias de planos de saúde
-- ========================================
CREATE TABLE PlansFamily (
    FamilyId INT IDENTITY(1,1) NOT NULL,
    Name VARCHAR(30) NULL,
    Description VARCHAR(MAX) NULL,
    Color VARCHAR(8) NULL,
    KeyWords VARCHAR(300) NULL,
    BenefictsHealth VARCHAR(MAX) NULL,
    BenefictsOdontology VARCHAR(MAX) NULL,
    CONSTRAINT PK_PlansFamily PRIMARY KEY (FamilyId)
);

-- ========================================
-- Tabela: CivilState
-- Descrição: Estados civis
-- ========================================
CREATE TABLE CivilState (
    Id INT NOT NULL,
    Description VARCHAR(25) NOT NULL,
    CONSTRAINT PK_CivilState PRIMARY KEY (Id)
);

-- ========================================
-- Tabela: DependentsType
-- Descrição: Tipos de dependentes
-- ========================================
CREATE TABLE DependentsType (
    Id INT NOT NULL,
    Description VARCHAR(25) NOT NULL,
    CONSTRAINT PK_DependentsType PRIMARY KEY (Id)
);

-- ========================================
-- Tabela: DocumentsType
-- Descrição: Tipos de documentos
-- ========================================
CREATE TABLE DocumentsType (
    Id INT NOT NULL,
    Description VARCHAR(100) NOT NULL,
    Name VARCHAR(50) NOT NULL,
    IsMandatory BIT NOT NULL,
    IsCpf BIT NOT NULL,
    IsIdentification BIT NOT NULL,
    UserType VARCHAR(1) NOT NULL,
    HasSignature BIT NOT NULL,
    IsSystemic BIT NOT NULL,
    DocumentTotal INT NULL,
    CONSTRAINT PK_DocumentsType PRIMARY KEY (Id)
);

-- ========================================
-- INSERÇÕES DE DADOS
-- ========================================

-- Inserir Origins
INSERT INTO Origin (Description, Tag) VALUES ('Contrate Online', 'CO');
INSERT INTO Origin (Description, Tag) VALUES ('Quem Indica', 'QI');
INSERT INTO Origin (Description, Tag) VALUES ('ParceiroPFF', 'PPF');
INSERT INTO Origin (Description, Tag) VALUES ('Corretora', 'COR');

-- Inserir HealthInsurers
INSERT INTO HealthInsurer VALUES (1, 'Hapvida');
INSERT INTO HealthInsurer VALUES (2, 'Bradesco Saúde');
INSERT INTO HealthInsurer VALUES (3, 'Unimed');
INSERT INTO HealthInsurer VALUES (4, 'Golden Cross');
INSERT INTO HealthInsurer VALUES (5, 'Amil');

-- Inserir BranchOffices
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (1, 1, 'FORTALEZA', 'CE', 0, 1);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (2, 1, 'NATAL', 'RN', 0, 1);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (3, 2, 'SAO LUIS', 'MA', 0, 2);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (4, 2, 'RECIFE', 'PE', 0, 2);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (5, 3, 'SALVADOR', 'BA', 0, 3);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (6, 3, 'BELEM', 'PA', 0, 3);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (7, 4, 'MACEIO', 'AL', 0, 1);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (8, 4, 'MANAUS', 'AM', 0, 2);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (9, 5, 'BRASILIA', 'DF', 0, 4);
INSERT INTO BranchOffice (AreaId, BranchOfficeId, AreaDescription, Uf, Hidden, HealthInsurerId) 
VALUES (10, 5, 'GOIANIA', 'GO', 0, 5);

-- Inserir BranchOfficePlaces
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (1, 'Fortaleza - Centro', 'CE', -3.731862, -38.526668);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (1, 'Fortaleza - Bairro de Fatima', 'CE', -3.755000, -38.580000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (2, 'Natal - Centro', 'RN', -5.795270, -35.209100);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (2, 'Natal - Ponta Negra', 'RN', -5.836530, -35.219590);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (3, 'Sao Luis - Centro', 'MA', -2.894850, -44.308000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (3, 'Sao Luis - Lagoa da Jansen', 'MA', -2.910000, -44.280000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (4, 'Recife - Centro', 'PE', -8.047562, -34.877035);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (4, 'Recife - Boa Viagem', 'PE', -8.121000, -34.912000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (5, 'Salvador - Centro', 'BA', -12.971160, -38.510840);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (5, 'Salvador - Barra', 'BA', -13.005200, -38.520000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (6, 'Belem - Centro', 'PA', -1.456309, -48.504570);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (6, 'Belem - Umarizal', 'PA', -1.458000, -48.490000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (7, 'Maceio - Centro', 'AL', -9.645399, -35.735094);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (7, 'Maceio - Pajucara', 'AL', -9.660000, -35.715000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (8, 'Manaus - Centro', 'AM', -3.099722, -60.185000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (8, 'Manaus - Zona Leste', 'AM', -3.100000, -59.950000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (9, 'Brasilia - Plano Piloto', 'DF', -15.797511, -47.879822);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (9, 'Brasilia - Asa Sul', 'DF', -15.820000, -47.880000);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (10, 'Goiania - Centro', 'GO', -15.789170, -48.876110);
INSERT INTO BranchOfficePlace (AreaId, PlaceDescription, Uf, Latitude, Longitude) 
VALUES (10, 'Goiania - Setor Bueno', 'GO', -15.800000, -48.870000);

-- Inserir HealthInsurerBranchOffice (Vinculações)
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (1, 1);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (1, 2);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (1, 7);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (2, 3);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (2, 4);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (2, 8);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (3, 5);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (3, 6);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (4, 9);
INSERT INTO HealthInsurerBranchOffice (HealthInsurerId, AreaId) VALUES (5, 10);

-- Inserir Sellers (Vendedores/Promotores)
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('João da Silva', 1, 1, 'AREA_001', 1);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Maria Santos', 1, 1, 'AREA_001', 2);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Carlos Oliveira', 2, 2, 'AREA_002', 1);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Ana Patricia', 3, 3, 'AREA_003', 3);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Roberto Costa', 1, 4, 'AREA_004', 2);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Fernanda Lima', 2, 5, 'AREA_005', 1);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Lucas Alves', 3, 6, 'AREA_006', 3);
INSERT INTO Seller (SellerName, OriginId, BranchOfficeId, SalesAreaId, BudgetTypeId) 
VALUES ('Juliana Rocha', 1, 7, 'AREA_007', 1);

-- Inserir PlansFamily (Famílias de Planos)
INSERT INTO PlansFamily (Name, Description, Color, KeyWords, BenefictsHealth, BenefictsOdontology) 
VALUES ('Básico', 'Plano básico de saúde', '#0066CC', 'básico,entrada,iniciante', 'Cobertura ambulatorial, internação', NULL);
INSERT INTO PlansFamily (Name, Description, Color, KeyWords, BenefictsHealth, BenefictsOdontology) 
VALUES ('Intermediário', 'Plano intermediário com melhor cobertura', '#FF9900', 'intermediário,padrão,comum', 'Cobertura ambulatorial, internação, cirurgias', NULL);
INSERT INTO PlansFamily (Name, Description, Color, KeyWords, BenefictsHealth, BenefictsOdontology) 
VALUES ('Premium', 'Plano com cobertura completa', '#00BB00', 'premium,completo,executivo', 'Cobertura total, sem limitações', 'Cobertura odontológica completa');
INSERT INTO PlansFamily (Name, Description, Color, KeyWords, BenefictsHealth, BenefictsOdontology) 
VALUES ('Saúde Plus', 'Plano ampliado com cobertura especial', '#FF0066', 'plus,ampliado,completo', 'Cobertura especial, cirurgias avançadas', 'Cobertura odontológica e estética');

-- Inserir CivilState (Estados Civis)
INSERT INTO CivilState (Id, Description) VALUES (1, 'Solteiro(a)');
INSERT INTO CivilState (Id, Description) VALUES (2, 'Casado(a)');
INSERT INTO CivilState (Id, Description) VALUES (3, 'Divorciado(a)');
INSERT INTO CivilState (Id, Description) VALUES (4, 'Viúvo(a)');
INSERT INTO CivilState (Id, Description) VALUES (5, 'Separado(a)');
INSERT INTO CivilState (Id, Description) VALUES (6, 'União Estável');

-- Inserir DependentsType (Tipos de Dependentes)
INSERT INTO DependentsType (Id, Description) VALUES (1, 'Cônjuge');
INSERT INTO DependentsType (Id, Description) VALUES (2, 'Filho(a)');
INSERT INTO DependentsType (Id, Description) VALUES (3, 'Enteado(a)');
INSERT INTO DependentsType (Id, Description) VALUES (4, 'Pai/Mãe');
INSERT INTO DependentsType (Id, Description) VALUES (5, 'Avô/Avó');
INSERT INTO DependentsType (Id, Description) VALUES (6, 'Irmão/Irmã');

-- Inserir DocumentsType (Tipos de Documentos)
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (1, 'CPF - Cadastro de Pessoas Física', 'CPF', 1, 1, 0, 'T', 0, 1, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (2, 'RG - Registro Geral', 'RG', 1, 0, 1, 'T', 0, 1, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (3, 'CNH - Carteira Nacional de Habilitação', 'CNH', 0, 0, 1, 'T', 0, 0, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (4, 'Passaporte', 'Passaporte', 0, 0, 1, 'T', 0, 0, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (5, 'Comprovante de Endereço', 'Comprovante de Endereço', 1, 0, 0, 'T', 0, 1, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (6, 'CPF - Dependente', 'CPF', 1, 1, 0, 'D', 0, 1, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (7, 'RG - Dependente', 'RG', 1, 0, 1, 'D', 0, 1, 1);
INSERT INTO DocumentsType (Id, Description, Name, IsMandatory, IsCpf, IsIdentification, UserType, HasSignature, IsSystemic, DocumentTotal) 
VALUES (8, 'Cartório - Certidão de Nascimento', 'Certidão de Nascimento', 0, 0, 0, 'D', 0, 0, 1);

-- ========================================
-- Criação de Índices para Performance
-- ========================================
CREATE NONCLUSTERED INDEX IX_BranchOffice_BranchOfficeId ON BranchOffice(BranchOfficeId);
CREATE NONCLUSTERED INDEX IX_BranchOffice_Hidden ON BranchOffice(Hidden);
CREATE NONCLUSTERED INDEX IX_BranchOffice_HealthInsurerId ON BranchOffice(HealthInsurerId);
CREATE NONCLUSTERED INDEX IX_BranchOfficePlace_AreaId ON BranchOfficePlace(AreaId);
CREATE NONCLUSTERED INDEX IX_BranchOfficePlace_Coordinates ON BranchOfficePlace(Latitude, Longitude);
CREATE NONCLUSTERED INDEX IX_Seller_OriginId ON Seller(OriginId);
CREATE NONCLUSTERED INDEX IX_Seller_BranchOfficeId ON Seller(BranchOfficeId);
CREATE NONCLUSTERED INDEX IX_HealthInsurerBranchOffice_HealthInsurerId ON HealthInsurerBranchOffice(HealthInsurerId);
CREATE NONCLUSTERED INDEX IX_HealthInsurerBranchOffice_AreaId ON HealthInsurerBranchOffice(AreaId);

-- ========================================
-- FIM DO SCRIPT
-- Banco de dados pronto para ambiente local
-- ========================================

       style="max-width: 960px; 
       width: 60%; 
       height: auto;"
       >  
</p>
