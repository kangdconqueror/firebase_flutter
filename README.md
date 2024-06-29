# Praktikum Mobile Programming


1. Buat Proyek Flutter Baru:
```bash
flutter create login_app
cd login_app
```

2. Tambahkan Firebase ke Proyek Flutter:
   a. Tambahkan dependensi Firebase pada pubspec.yaml:
   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     firebase_core: latest_version
     firebase_auth: latest_version
   ```
   b. Konfigurasikan Firebase di Android dan iOS.

3. Buat Widget Login:
```dart
import 'package:flutter/material.dart';
import 'package:firebase_auth/firebase_auth.dart';

class LoginScreen extends StatefulWidget {
  @override
  _LoginScreenState createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  final FirebaseAuth _auth = FirebaseAuth.instance;
  final TextEditingController _emailController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  Future<void> _login() async {
    try {
      UserCredential userCredential = await _auth.signInWithEmailAndPassword(
        email: _emailController.text,
        password: _passwordController.text,
      );
      Navigator.pushReplacement(
        context,
        MaterialPageRoute(builder: (context) => HomeScreen(user: userCredential.user)),
      );
    } catch (e) {
      print(e);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Login')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _emailController,
              decoration: InputDecoration(labelText: 'Email'),
            ),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(labelText: 'Password'),
              obscureText: true,
            ),
            ElevatedButton(
              onPressed: _login,
              child: Text('Login'),
            ),
          ],
        ),
      ),
    );
  }
}

class HomeScreen extends StatelessWidget {
  final User user;
  HomeScreen({required this.user});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: Text('Logged in as: ${user.email}'),
      ),
    );
  }
}
```

4. Unggah Proyek ke GitHub:
```bash
git init
git add .
git commit -m 'Initial commit'
git remote add origin <repository_url>
git push -u origin master
```

5. Sertakan tautan repositori GitHub di sini: <repository_url>
