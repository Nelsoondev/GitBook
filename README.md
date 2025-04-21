# Diagrama Relational Fisico DataBase

<img src="https://raw.githubusercontent.com/Nelsoondev/GitBook/refs/heads/main/images/erd%20fisico.png" alt="Diagrama ERD Físico" width="800">

CREATE TABLE Autor
(
  id_autor  INT         NOT NULL,
  nombre    VARCHAR(70),
  biografia TEXT       ,
  CONSTRAINT PK_Autor PRIMARY KEY (id_autor)
)
GO

CREATE TABLE Categoria
(
  id_categoria INT         NOT NULL,
  nombre       VARCHAR(50),
  CONSTRAINT PK_Categoria PRIMARY KEY (id_categoria)
)
GO

CREATE TABLE Comprobante
(
  id_comprobante INT      NOT NULL,
  fecha          DATETIME,
  total          DECIMAL ,
  id_usuario     INT      NOT NULL,
  id_metodopago  INT      NOT NULL,
  CONSTRAINT PK_Comprobante PRIMARY KEY (id_comprobante)
)
GO

CREATE TABLE Departamento
(
  id_departamento INT         NOT NULL,
  nombre          VARCHAR(50),
  CONSTRAINT PK_Departamento PRIMARY KEY (id_departamento)
)
GO

CREATE TABLE DetalleComprobante
(
  id_detalle      INT     NOT NULL,
  id_Libro        INT     NOT NULL,
  id_comprobante  INT     NOT NULL,
  cantidad        INT    ,
  precio_unitario DECIMAL,
  CONSTRAINT PK_DetalleComprobante PRIMARY KEY (id_detalle)
)
GO

CREATE TABLE Distrito
(
  id_distrito  INT         NOT NULL,
  nombre       VARCHAR(50),
  id_provincia INT         NOT NULL,
  CONSTRAINT PK_Distrito PRIMARY KEY (id_distrito)
)
GO

CREATE TABLE Editorial
(
  id_editorial INT          NOT NULL,
  nombre       VARCHAR(100),
  pais         VARCHAR(50) ,
  CONSTRAINT PK_Editorial PRIMARY KEY (id_editorial)
)
GO

CREATE TABLE HistorialCompra
(
  id_historial   INT      NOT NULL,
  id_comprobante INT      NOT NULL,
  id_usuario     INT      NOT NULL,
  fecha_consulta DATETIME,
  CONSTRAINT PK_HistorialCompra PRIMARY KEY (id_historial)
)
GO

CREATE TABLE Libro
(
  id_Libro     INT          NOT NULL,
  titulo       VARCHAR(100) NOT NULL,
  isbn         VARCHAR(20) ,
  precio       DECIMAL     ,
  stock        INT         ,
  id_autor     INT          NOT NULL,
  id_editorial INT          NOT NULL,
  CONSTRAINT PK_Libro PRIMARY KEY (id_Libro)
)
GO

CREATE TABLE LibroCategoria
(
  id_categoria INT NOT NULL,
  id_Libro     INT NOT NULL,
  CONSTRAINT PK_LibroCategoria PRIMARY KEY (id_categoria, id_Libro)
)
GO

CREATE TABLE MetodoPago
(
  id_metodopago INT         NOT NULL,
  nombre        VARCHAR(50),
  CONSTRAINT PK_MetodoPago PRIMARY KEY (id_metodopago)
)
GO

CREATE TABLE Provincia
(
  id_provincia    INT         NOT NULL,
  nombre          VARCHAR(50),
  id_departamento INT         NOT NULL,
  CONSTRAINT PK_Provincia PRIMARY KEY (id_provincia)
)
GO

CREATE TABLE Reseña
(
  id_reseña    INT      NOT NULL,
  comentario   TEXT    ,
  calificacion INT     ,
  fecha        DATETIME,
  id_Libro     INT      NOT NULL,
  id_usuario   INT      NOT NULL,
  CONSTRAINT PK_Reseña PRIMARY KEY (id_reseña)
)
GO

CREATE TABLE Usuario
(
  id_usuario  INT          NOT NULL,
  nombre      VARCHAR(75) ,
  email       VARCHAR(75) ,
  direccion   VARCHAR(100),
  telefono    VARCHAR(20) ,
  id_distrito INT          NOT NULL,
  CONSTRAINT PK_Usuario PRIMARY KEY (id_usuario)
)
GO

ALTER TABLE LibroCategoria
  ADD CONSTRAINT FK_Categoria_TO_LibroCategoria
    FOREIGN KEY (id_categoria)
    REFERENCES Categoria (id_categoria)
GO

ALTER TABLE LibroCategoria
  ADD CONSTRAINT FK_Libro_TO_LibroCategoria
    FOREIGN KEY (id_Libro)
    REFERENCES Libro (id_Libro)
GO

ALTER TABLE Libro
  ADD CONSTRAINT FK_Autor_TO_Libro
    FOREIGN KEY (id_autor)
    REFERENCES Autor (id_autor)
GO

ALTER TABLE Libro
  ADD CONSTRAINT FK_Editorial_TO_Libro
    FOREIGN KEY (id_editorial)
    REFERENCES Editorial (id_editorial)
GO

ALTER TABLE DetalleComprobante
  ADD CONSTRAINT FK_Libro_TO_DetalleComprobante
    FOREIGN KEY (id_Libro)
    REFERENCES Libro (id_Libro)
GO

ALTER TABLE Provincia
  ADD CONSTRAINT FK_Departamento_TO_Provincia
    FOREIGN KEY (id_departamento)
    REFERENCES Departamento (id_departamento)
GO

ALTER TABLE Distrito
  ADD CONSTRAINT FK_Provincia_TO_Distrito
    FOREIGN KEY (id_provincia)
    REFERENCES Provincia (id_provincia)
GO

ALTER TABLE Usuario
  ADD CONSTRAINT FK_Distrito_TO_Usuario
    FOREIGN KEY (id_distrito)
    REFERENCES Distrito (id_distrito)
GO

ALTER TABLE Reseña
  ADD CONSTRAINT FK_Libro_TO_Reseña
    FOREIGN KEY (id_Libro)
    REFERENCES Libro (id_Libro)
GO

ALTER TABLE Reseña
  ADD CONSTRAINT FK_Usuario_TO_Reseña
    FOREIGN KEY (id_usuario)
    REFERENCES Usuario (id_usuario)
GO

ALTER TABLE HistorialCompra
  ADD CONSTRAINT FK_Comprobante_TO_HistorialCompra
    FOREIGN KEY (id_comprobante)
    REFERENCES Comprobante (id_comprobante)
GO

ALTER TABLE HistorialCompra
  ADD CONSTRAINT FK_Usuario_TO_HistorialCompra
    FOREIGN KEY (id_usuario)
    REFERENCES Usuario (id_usuario)
GO

ALTER TABLE DetalleComprobante
  ADD CONSTRAINT FK_Comprobante_TO_DetalleComprobante
    FOREIGN KEY (id_comprobante)
    REFERENCES Comprobante (id_comprobante)
GO

ALTER TABLE Comprobante
  ADD CONSTRAINT FK_MetodoPago_TO_Comprobante
    FOREIGN KEY (id_metodopago)
    REFERENCES MetodoPago (id_metodopago)
GO

ALTER TABLE Comprobante
  ADD CONSTRAINT FK_Usuario_TO_Comprobante
    FOREIGN KEY (id_usuario)
    REFERENCES Usuario (id_usuario)
GO
