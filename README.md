CREATE TABLE Usuarios (
    IdUsuario INTEGER PRIMARY KEY AUTOINCREMENT,
    Nombre TEXT NOT NULL,
    Email TEXT NOT NULL UNIQUE,
    Password TEXT NOT NULL,
    FechaRegistro DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE Productos (
    IdProducto INTEGER PRIMARY KEY AUTOINCREMENT,
    Nombre TEXT NOT NULL,
    Descripcion TEXT,
    Precio REAL NOT NULL CHECK(Precio > 0),
    Stock INTEGER NOT NULL CHECK(Stock >= 0)
);

CREATE TABLE Pedidos (
    IdPedido INTEGER PRIMARY KEY AUTOINCREMENT,
    IdUsuario INTEGER NOT NULL,
    FechaPedido DATETIME DEFAULT CURRENT_TIMESTAMP,
    Total REAL NOT NULL CHECK(Total >= 0),
    FOREIGN KEY (IdUsuario) REFERENCES Usuarios(IdUsuario) ON DELETE CASCADE
);

CREATE TABLE DetallesPedido (
    IdDetalle INTEGER PRIMARY KEY AUTOINCREMENT,
    IdPedido INTEGER NOT NULL,
    IdProducto INTEGER NOT NULL,
    Cantidad INTEGER NOT NULL CHECK(Cantidad > 0),
    SubTotal REAL NOT NULL CHECK(SubTotal >= 0),
    FOREIGN KEY (IdPedido) REFERENCES Pedidos(IdPedido) ON DELETE CASCADE,
    FOREIGN KEY (IdProducto) REFERENCES Productos(IdProducto) ON DELETE CASCADE
);
