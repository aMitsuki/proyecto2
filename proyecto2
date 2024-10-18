#include <iostream>
#include <vector>
#include <string>
#include <map>

using namespace std;

// Clase para Producto
class Producto {
public:
    string nombre;
    int cantidad;
    string categoria;

    Producto(string nombre, int cantidad, string categoria) : nombre(nombre), cantidad(cantidad), categoria(categoria) {}
};

// Clase para las Categorías
class Categoria {
public:
    string nombreCategoria;

    Categoria(string nombre) : nombreCategoria(nombre) {}
};

// Clase para la Lista de Compras
class ListaCompras {
public:
    vector<Producto> productos;
    string fecha;
    bool pospuesta;

    ListaCompras(string fecha) : fecha(fecha), pospuesta(false) {}

    void agregarProducto(string nombre, int cantidad, string categoria) {
        productos.push_back(Producto(nombre, cantidad, categoria));
    }

    void mostrarLista() {
        cout << "Lista de Compras - Fecha: " << fecha << endl;
        for (const auto& producto : productos) {
            cout << "- " << producto.nombre << " (" << producto.cantidad << ") - Categoria: " << producto.categoria << endl;
        }
    }

    void posponer() {
        pospuesta = true;
        cout << "Lista pospuesta." << endl;
    }
};

// Clase para el Usuario
class Usuario {
public:
    string nombre;
    int idUsuario;
    vector<ListaCompras> historialListas;

    Usuario(string nombre, int id) : nombre(nombre), idUsuario(id) {}

    void crearLista(string fecha) {
        ListaCompras nuevaLista(fecha);
        historialListas.push_back(nuevaLista);
        cout << "Lista creada en la fecha: " << fecha << endl;
    }

    void consultarHistorial() {
        cout << "Historial de listas de " << nombre << ":" << endl;
        for (const auto & lista : historialListas) {
            lista.mostrarLista();
        }
    }
};

// Clase para el Administrador, que hereda de Usuario
class Administrador : public Usuario {
public:
    map<string, Categoria> categorias;

    Administrador(string nombre, int id) : Usuario(nombre, id) {}

    void agregarCategoria(string nombreCategoria) {
        categorias[nombreCategoria] = Categoria(nombreCategoria);
        cout << "Categoria " << nombreCategoria << " agregada." << endl;
    }

    void modificarCategoria(string nombreViejo, string nombreNuevo) {
        if (categorias.find(nombreViejo) != categorias.end()) {
            categorias[nombreNuevo] = categorias[nombreViejo];
            categorias[nombreNuevo].nombreCategoria = nombreNuevo;
            categorias.erase(nombreViejo);
            cout << "Categoria modificada: " << nombreViejo << " -> " << nombreNuevo << endl;
        }
        else {
            cout << "Categoria no encontrada." << endl;
        }
    }

    void eliminarCategoria(string nombreCategoria) {
        if (categorias.find(nombreCategoria) != categorias.end()) {
            categorias.erase(nombreCategoria);
            cout << "Categoria " << nombreCategoria << " eliminada." << endl;
        }
        else {
            cout << "Categoria no encontrada." << endl;
        }
    }

    void mostrarCategorias() {
        cout << "Categorias disponibles: " << endl;
        for (const auto& categoria : categorias) {
            cout << "- " << categoria.first << endl;
        }
    }
};

// Función principal
int main() {
    // Crear usuarios
    Usuario usuario1("Juan", 1);
    Administrador admin("Admin", 0);

    // Administrador agrega categorías
    admin.agregarCategoria("Alimentos");
    admin.agregarCategoria("Limpieza");
    admin.mostrarCategorias();

    // Usuario crea una lista de compras
    usuario1.crearLista("2024-10-17");
    usuario1.historialListas[0].agregarProducto("Manzanas", 5, "Alimentos");
    usuario1.historialListas[0].agregarProducto("Jabón", 2, "Limpieza");

    // Usuario consulta su historial
    usuario1.consultarHistorial();

    // Usuario pospone la lista
    usuario1.historialListas[0].posponer();

    // Administrador modifica una categoría
    admin.modificarCategoria("Alimentos", "Comestibles");
    admin.mostrarCategorias();

    return 0;
}
