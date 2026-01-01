import 'package:flutter/material.dart';
import 'dart:async';

void main() {
  runApp(const MaterialApp(
    debugShowCheckedModeBanner: false,
    home: LoginPage(),
  ));
}

// الصفحة الأولى
class LoginPage extends StatelessWidget {
  const LoginPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('تسجيل الدخول')),
      body: Center(
        child: ElevatedButton(
          child: const Text('تسجيل دخول', style: TextStyle(fontSize: 20)),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => const MarketingPage()),
            );
          },
        ),
      ),
    );
  }
}

// الصفحة الثانية
class MarketingPage extends StatefulWidget {
  const MarketingPage({super.key});

  @override
  State<MarketingPage> createState() => _MarketingPageState();
}

class _MarketingPageState extends State<MarketingPage> {
  final List<Color> _colors = [
    Colors.black,
    Colors.grey,
    const Color(0xFF00008B), // أزرق غامق
    Colors.blue,             // أزرق فاتح
    Colors.brown,            // بني
  ];

  int _currentIndex = 0;
  Timer? _timer;

  @override
  void initState() {
    super.initState();
    _timer = Timer.periodic(const Duration(seconds: 3), (timer) {
      if (mounted) {
        setState(() {
          _currentIndex = (_currentIndex + 1) % _colors.length;
        });
      }
    });
  }

  @override
  void dispose() {
    _timer?.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: AnimatedContainer(
        duration: const Duration(seconds: 1),
        color: _colors[_currentIndex],
        width: double.infinity,
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const Text('منصة تسويق', style: TextStyle(color: Colors.white, fontSize: 25)),
            const SizedBox(height: 20),
            const Text(
              'دعاية الموسم',
              style: TextStyle(color: Colors.white, fontSize: 45, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 20),
            const Text('123456789', style: TextStyle(color: Colors.white, fontSize: 35)),
            const SizedBox(height: 50),
            TextButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('رجوع للرئيسية', style: TextStyle(color: Colors.white)),
            ),
          ],
        ),
      ),
    );
  }
}
