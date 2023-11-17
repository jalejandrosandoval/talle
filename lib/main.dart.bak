import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_database/firebase_database.dart';
import 'package:firebase_database/ui/firebase_animated_list.dart';
import 'package:flutter/material.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}

class MyApp extends StatelessWidget { // Define una clase llamada MyApp que extiende StatelessWidget.
  @override
  Widget build(BuildContext context) { // Define el método build para construir la interfaz de la aplicación.
    return MaterialApp(
      title: 'Mi Aplicación', // Título de la aplicación.
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue, // Configura el tema de la aplicación con un color azul.
      ),
      initialRoute: '/', // Ruta inicial de la aplicación.
      routes: {
        '/': (context) => AuthScreen(), // Define una ruta llamada '/' que muestra AuthScreen.
        //'/register': (context) => RegisterScreen(), // Define una ruta llamada '/register' que muestra RegisterScreen.
      },
    );
  }
}

class AuthScreen extends StatefulWidget { // Define una clase llamada AuthScreen que extiende StatefulWidget.
  @override
  _AuthScreenState createState() => _AuthScreenState(); // Crea el estado para AuthScreen.
}

class _AuthScreenState extends State<AuthScreen> { // Define el estado de AuthScreen.
  TextEditingController emailController = TextEditingController(); // Controlador para el campo de correo electrónico.
  TextEditingController passwordController = TextEditingController(); // Controlador para el campo de contraseña.
  bool isLoggedInCuidador = false; // Variable booleana que indica si el usuario ha iniciado sesión.
  bool isLoggedInCliente = false; // Variable booleana que indica si el usuario ha iniciado sesión.
  String? registeredEmail; // Almacena el correo electrónico registrado.
  String? registeredPassword; // Almacena la contraseña registrada.
    String? registeredEmail2; // Almacena el correo electrónico registrado.
  String? registeredPassword2; // Almacena la contraseña registrada.
  String? tipoUsuario;

   Readinfo() async {
    try {
          DatabaseReference dbRef2 = FirebaseDatabase.instance.ref().child('usuario');
          final snapshot = await dbRef2.get();
          Map usuarios = snapshot as Map;
          print(snapshot);
          print(usuarios);
          if (snapshot.exists) {
              print(snapshot.value);
              // print(usuarios['nombre']);
              // print(usuarios['clave']);
              // print(usuarios['tipo']);
              //registeredEmail = usuarios['nombre'];
              //registeredPassword = usuarios['clave'];
              //tipoUsuario = usuarios['tipo'];
              // tipoUsuario = 'cuidador';
          } else {
              print('No data available.');
          }
    } on Exception catch (e) {
      print(e);
    }
  }

  void login() { // Función para iniciar sesión.
      //Readinfo();
      registeredEmail = 'Armando';
      registeredPassword = '1234';
      registeredEmail2 = 'Horacio';
      registeredPassword2 = '1234';
      final enteredEmail = emailController.text; // Obtiene el correo electrónico ingresado.
      final enteredPassword = passwordController.text; // Obtiene la contraseña ingresada.

      if ((enteredEmail == registeredEmail && enteredPassword == registeredPassword) || (enteredEmail == registeredEmail2 && enteredPassword == registeredPassword2)) { // Comprueba las credenciales.
        setState(() { // Actualiza el estado de la aplicación.
            if(enteredEmail == 'Armando'){
                tipoUsuario = 'cuidador';
              } else {
                tipoUsuario = 'cliente';
              }
            if(tipoUsuario=="cuidador"){
              isLoggedInCuidador = true; // Marca al usuario como autenticado.
              isLoggedInCliente = false; // Marca al usuario como autenticado.
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (_) => MyHomePage(),
                ),
              );
            } else {
              isLoggedInCuidador = false; // Marca al usuario como autenticado.
              isLoggedInCliente = true; // Marca al usuario como autenticado.
            }
        });
        /* Navigator.push(
          context,
          MaterialPageRoute(builder: (context) => MyHomePage()),
        ); */
      } else { // Credenciales incorrectas, muestra un diálogo de error.
        showDialog(
          context: context,
          builder: (BuildContext context) {
            return AlertDialog(
              title: Text('Error de inicio de sesión'),
              content: Text('Credenciales incorrectas. Verifica tu correo y contraseña.'),
              actions: <Widget>[
                TextButton(
                  onPressed: () {
                    Navigator.of(context).pop();
                  },
                  child: Text('Cerrar'),
                ),
              ],
            );
          },
        );
      }
  }

  @override
  Widget build(BuildContext context) { // Método para construir la interfaz de AuthScreen.
      return Scaffold(
        appBar: AppBar(
          title: Text('Inicio de Sesión o Registro'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[

              //Image.asset('assets/escudo_leon.jpg', width: 400),
              
              Container(
              margin: const EdgeInsets.symmetric(horizontal: 30.0),
              child:TextField(
                controller: emailController,
                decoration: InputDecoration(labelText: 'Correo Electrónico'),
                ),
                
              ),

               Container(
              margin: const EdgeInsets.symmetric(horizontal: 30.0),
              padding: const EdgeInsets.only(bottom: 20.0),
              child:TextField(
                controller: passwordController,
                decoration: InputDecoration(labelText: 'Contraseña'),
                obscureText: true, // Oculta el texto de la contraseña.
              ),
              ),
              
              ElevatedButton(
                onPressed: login,
                child: Text('Iniciar Sesión'),
              ),

            ],
          ),
        ),
      );
  }
}



/* class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'conexion firebase',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
} */

class MyHomePage extends StatefulWidget {
  //const MyHomePage({super.key, required this.title});
  //final String title;
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  String latitud = "";
  String longitud = "";
  
  @override
  Widget build(BuildContext context) {
    DatabaseReference db_Ref =
        FirebaseDatabase.instance.ref().child('caidas');
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        backgroundColor: Colors.indigo[900],
        onPressed: () {
          /* Navigator.push(
            context,
            MaterialPageRoute(
              builder: (_) => ccreate(),
            ),
          ); */
          Saveinfo();
        },
        child: Icon(
          Icons.add,
        ),
      ),
      appBar: AppBar(
        title: Text(
          'Contacts',
          style: TextStyle(
            fontSize: 30,
          ),
        ),
        backgroundColor: Colors.indigo[900],
      ),
      body: FirebaseAnimatedList(
        query: db_Ref,
        shrinkWrap: true,
        itemBuilder: (context, snapshot, animation, index) {
          Map Contact = snapshot.value as Map;
          Contact['key'] = snapshot.key;
          latitud = Contact['latitud'].toString();
          //print(snapshot.value);
          //print(Contact);
          //print(latitud);
          return GestureDetector(
            /* onTap: () {
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (_) => UpdateRecord(
                    Contact_Key: Contact['key'],
                  ),
                ),
              );
              // print(Contact['key']);
            }, */
            child: Container(
              child: Padding(
                padding: const EdgeInsets.all(8.0),
                child: ListTile(
                  shape: RoundedRectangleBorder(
                    side: BorderSide(
                      color: Colors.white,
                    ),
                    borderRadius: BorderRadius.circular(10),
                  ),
                  tileColor: Colors.indigo[100],
                  trailing: IconButton(
                    icon: Icon(
                      Icons.delete,
                      color: Colors.red[900],
                    ),
                    onPressed: () {
                     db_Ref.child(Contact['key']).remove();
                    },
                  ),
/*                   leading: CircleAvatar(
                    backgroundImage: NetworkImage(
                      Contact['url'],
                    ),
                  ), */
                  title: Text(
                    Contact['nombre'],
                    style: TextStyle(
                      fontSize: 25,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  subtitle: Text(
                    latitud,
                    style: TextStyle(
                      fontSize: 25,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
              ),
            ),
          );
        },
      ),
    );
  }

  DatabaseReference? dbRef;
  @override
  void initState() {
    super.initState();
    dbRef = FirebaseDatabase.instance.ref().child('caidas');
  }

  Saveinfo() async {
    String nombre = "Nuevo registro";
    int id_usuario = 1;
    double latitud = 13.1569;
    double longitud = 8.8888;
    double aceleracion = 23.1569;
    String fecha = '2023-12-01 09:18:00';

     try {
        Map Contact = {
          'nombre': nombre,
          'id_usuario': id_usuario,
          'latitud': latitud,
          'longitud': longitud,
          'aceleracion': aceleracion,
          'id_cuidador': 0,
          'fecha': fecha,
        };
        dbRef!.push().set(Contact);
/*         dbRef!.push().set(Contact).whenComplete(() {
          Navigator.pushReplacement(
            context,
            MaterialPageRoute(
              builder: (_) => Home(), // enviar a la vista deseada
            ),
          );
        }); */
    } on Exception catch (e) {
      print(e);
    }
  }
}