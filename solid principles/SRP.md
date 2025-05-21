### **1 - Single Responsibility Principle - SRP**

المبدأ الأول من مبادئ **SOLID** هو **مبدأ المسؤولية الواحدة (Single Responsibility Principle - SRP)**، والذي ينص على أن **الكلاس يجب أن يكون له سبب واحد فقط للتغيير**، أي أن له مسؤولية واحدة فقط. و الان سأشرح مبدأ المسؤولية الواحدة بالتفصيل باستخدام لغة **Dart**، مع أمثلة توضيحية تشمل كودًا ينتهك المبدأ وكودًا يتبعه، بالإضافة إلى شرح لماذا يهم هذا المبدأ وكيفية تطبيقه.
### **ما هو مبدأ المسؤولية الواحدة؟**
ينص مبدأ المسؤولية الواحدة على أن الكلاس يجب أن يكون مسؤولاً عن مهمة واحدة فقط في النظام. إذا كان للكلاس مسؤوليات متعددة، يصبح من الصعب صيانته واختباره وتوسيعه، لأن التغييرات في إحدى المسؤوليات قد تؤثر على الأخرى. باتباع هذا المبدأ، يركز كل كلاس على مهمة واحدة، مما يجعل الكود أكثر وضوحًا وسهولة في الصيانة وأقل عرضة للأخطاء.

---
#### **النقاط الرئيسية للمبدأ**:
- **مسؤولية واحدة**: يجب أن يتعامل الكلاس مع جانب واحد فقط من الوظائف (مثل المنطق التجاري، أو تخزين البيانات، أو عرض الواجهة).
- **سبب التغيير**: إذا كان يجب تعديل الكلاس لأسباب متعددة غير مترابطة (مثل تغيير طريقة حفظ البيانات *و* طريقة العرض)، فهو ينتهك المبدأ.
- **الفوائد**:
  - **سهولة الصيانة**: التغييرات في مسؤولية واحدة لا تؤثر على غيرها.
  - **اختبار أسهل**: الكلاسات ذات المسؤولية الواحدة أبسط في الاختبار.
  - **إعادة استخدام أفضل**: الكلاسات المركزة يمكن إعادة استخدامها في سياقات مختلفة.
  - **تقليل الاقتران**: فصل المسؤوليات يقلل من الاعتماديات بين الكلاسات.

---
### **لماذا مبدأ المسؤولية الواحدة مهم ؟**

تخيل كلاسًا يدير بيانات المستخدم ويحفظها في قاعدة بيانات ويعرضها في واجهة المستخدم. إذا تغير هيكل قاعدة البيانات، ستحتاج إلى تعديل الكلاس. وإذا تغير تصميم الواجهة، ستحتاج إلى تعديل نفس الكلاس. هذه التغييرات غير المترابطة تزيد من مخاطر الأخطاء، وتجعل الكلاس صعب الاختبار والصيانة. باتباع المبدأ، يتم ضمان أن كل كلاس له غرض واضح، مما يقلل من التعقيد ويسهل التكيف مع المتطلبات المستقبلية.

---
### **مثال 1: انتهاك المبدأ**

فيما يلي مثال لكلاس في Dart ينتهك مبدأ المسؤولية الواحدة من خلال التعامل مع مسؤوليات متعددة: إدارة بيانات المستخدم، وحفظها في قاعدة بيانات، وتنسيقها للعرض.

```dart
class UserManager {
  String name;
  String email;

  UserManager(this.name, this.email);

  // المسؤولية 1: إدارة بيانات المستخدم
  void updateUser(String newName, String newEmail) {
    name = newName;
    email = newEmail;
    print('تم تحديث المستخدم: $name, $email');
  }

  // المسؤولية 2: حفظ بيانات المستخدم في قاعدة البيانات
  void saveToDatabase() {
    // محاكاة حفظ قاعدة البيانات
    print('حفظ المستخدم في قاعدة البيانات: $name, $email');
  }

  // المسؤولية 3: تنسيق بيانات المستخدم للعرض
  String getFormattedUserInfo() {
    return 'المستخدم: $name\nالبريد الإلكتروني: $email';
  }
}
```

#### **لماذا ينتهك هذا المبدأ؟**
كلاس `UserManager` لديه **ثلاث مسؤوليات متميزة**:
1. **إدارة بيانات المستخدم** (تخزين وتحديث `name` و`email`).
2. **حفظ البيانات** (تخزينها في قاعدة بيانات).
3. **تنسيق البيانات للعرض** (إنشاء سلسلة نصية للواجهة).

إذا تغيرت أي من هذه المسؤوليات—مثل تغيير هيكل قاعدة البيانات أو الحاجة إلى تنسيق مختلف للواجهة—يجب تعديل الكلاس. هذا يزيد من مخاطر الأخطاء ويجعل الكلاس صعب الصيانة أو إعادة الاستخدام في سياقات مختلفة.

#### **مشاكل هذا النهج**:
- **الاقتران الشديد**: الكلاس مرتبط بمنطق قاعدة بيانات وواجهة مستخدم محددين، مما يقلل من إعادة الاستخدام.
- **صعوبة الاختبار**: اختبار `saveToDatabase` يتطلب محاكاة قاعدة بيانات، واختبار `getFormattedUserInfo` يتطلب التحقق من تنسيق الواجهة.
- **أسباب متعددة للتغيير**: التغييرات في منطق قاعدة البيانات، هيكل البيانات، أو تنسيق الواجهة تتطلب تعديل الكلاس نفسه.

---

### **مثال 2: اتباع المبدأ**

لنعيد هيكلة الكلاس `UserManager` ليتبع مبدأ المسؤولية الواحدة عن طريق فصل المسؤوليات إلى كلاسات منفصلة.

```dart
//I    المسؤولية 1: إدارة بيانات المستخدم
class User {
  String name;
  String email;

  User(this.name, this.email);

  void updateUser(String newName, String newEmail) {
    name = newName;
    email = newEmail;
    print('تم تحديث المستخدم: $name, $email');
  }
}

// المسؤولية 2: حفظ بيانات المستخدم في قاعدة البيانات
class UserRepository {
  void saveToDatabase(User user) {
    // محاكاة حفظ قاعدة البيانات
    print('حفظ المستخدم في قاعدة البيانات: ${user.name}, ${user.email}');
  }
}

// المسؤولية 3: تنسيق بيانات المستخدم للعرض
class UserFormatter {
  String getFormattedUserInfo(User user) {
    return 'المستخدم: ${user.name}\nالبريد الإلكتروني: ${user.email}';
  }
}

// مثال الاستخدام
void main() {
  // إنشاء مستخدم
  var user = User('أليس', 'alice@example.com');

  // تحديث بيانات المستخدم
  user.updateUser('بوب', 'bob@example.com');

  // حفظ في قاعدة البيانات
  var repository = UserRepository();
  repository.saveToDatabase(user);

  // تنسيق للعرض
  var formatter = UserFormatter();
  print(formatter.getFormattedUserInfo(user));
}
```
#### **لماذا يتبع هذا المبدأ؟**
- **مسؤولية واحدة لكل كلاس**:
  - `User`: مسؤول فقط عن إدارة بيانات المستخدم (تخزين وتحديث `name` و`email`).
  - `UserRepository`: مسؤول فقط عن حفظ البيانات (تخزين في قاعدة بيانات).
  - `UserFormatter`: مسؤول فقط عن تنسيق البيانات للعرض.
- **فصل واضح**: لكل كلاس سبب واحد للتغيير:
  - تغيير `User` إذا تغير هيكل بيانات المستخدم (مثل إضافة رقم هاتف).
  - تغيير `UserRepository` إذا تغير منطق قاعدة البيانات (مثل الانتقال إلى قاعدة بيانات مختلفة).
  - تغيير `UserFormatter` إذا تغيرت متطلبات تنسيق الواجهة (مثل إضافة تنسيق HTML).
- **الفوائد**:
  - **إعادة الاستخدام**: يمكن استخدام `User` في أي سياق دون ربطه بقاعدة بيانات أو واجهة. وكذلك يمكن لـ`UserFormatter` تنسيق البيانات لأنواع مختلفة من الواجهات.
  - **سهولة الاختبار**: يمكن اختبار `User` دون محاكاة قاعدة بيانات، واختبار `UserFormatter` دون القلق بشأن حفظ البيانات.
  - **سهولة الصيانة**: التغييرات في مسؤولية واحدة (مثل منطق قاعدة البيانات) لا تؤثر على الآخرين.

#### **مخرجات المثال**
تشغيل الدالة `main` سينتج:
```
تم تحديث المستخدم: بوب, bob@example.com
حفظ المستخدم في قاعدة البيانات: بوب, bob@example.com
المستخدم: بوب
البريد الإلكتروني: bob@example.com
```

---
### **مثال واقعي في سياق Flutter**

في **Flutter**، تُستخدم Dart لبناء تطبيقات الهواتف، حيث يكون مبدأ المسؤولية الواحدة مهمًا لإدارة الواجهات المعقدة، المنطق التجاري، وحفظ البيانات. دعنا ننظر إلى سيناريو Flutter حيث يدير كلاس جلب بيانات المستخدم من واجهة برمجية (API) وعرضها في ويدجت.

#### **مثال سيء (ينتهك المبدأ)**:
```dart
import 'package:flutter/material.dart';

class UserProfile extends StatelessWidget {
  final String name = 'محمد';
  final String email = 'mohammed_anwar@example.com';

  // المسؤولية 1: جلب البيانات من واجهة برمجية
  Future<Map<String, String>> fetchUserData() async {
    // محاكاة استدعاء واجهة برمجية
    await Future.delayed(Duration(seconds: 1));
    return {'name': name, 'email': email};
  }

  // المسؤولية 2: عرض الواجهة
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<Map<String, String>>(
      future: fetchUserData(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        }
        if (snapshot.hasData) {
          return Column(
            children: [
              Text('الاسم: ${snapshot.data!['name']}'),
              Text('البريد الإلكتروني: ${snapshot.data!['email']}'),
            ],
          );
        }
        return Text('خطأ في تحميل بيانات المستخدم');
      },
    );
  }
}
```

**المشكلة**: ويدجت `UserProfile` مسؤول عن **جلب البيانات** (منطق واجهة برمجية) و**عرض الواجهة**. إذا تغيرت واجهة البرمجة أو تصميم الواجهة، يجب تعديل نفس الكلاس، مما ينتهك المبدأ.

#### **مثال معاد هيكلته (يتبع المبدأ)**:
```dart
import 'package:flutter/material.dart';

// المسؤولية 1: نموذج بيانات المستخدم
class User {
  final String name;
  final String email;

  User(this.name, this.email);
}

// المسؤولية 2: جلب البيانات من واجهة برمجية
class UserService {
  Future<User> fetchUserData() async {
    // محاكاة استدعاء واجهة برمجية
    await Future.delayed(Duration(seconds: 1));
    return User('أليس', 'alice@example.com');
  }
}

// المسؤولية 3: عرض الواجهة
class UserProfile extends StatelessWidget {
  final UserService userService;

  UserProfile({required this.userService});

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<User>(
      future: userService.fetchUserData(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        }
        if (snapshot.hasData) {
          return Column(
            children: [
              Text('الاسم: ${snapshot.data!.name}'),
              Text('البريد الإلكتروني: ${snapshot.data!.email}'),
            ],
          );
        }
        return Text('خطأ في تحميل بيانات المستخدم');
      },
    );
  }
}

// مثال الاستخدام
void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: UserProfile(userService: UserService()),
    ),
  ));
}
```

**لماذا يتبع هذا المبدأ؟**:
- `User`: يدير نموذج بيانات المستخدم.
- `UserService`: يتعامل مع جلب البيانات (مثل استدعاءات واجهة برمجية).
- `UserProfile`: يركز فقط على عرض الواجهة.
- **حقن الاعتماديات**: يتم تمرير `UserService` إلى `UserProfile`، مما يسهل تبديل مصدر البيانات (مثل للاختبار أو استخدام واجهة برمجية مختلفة).

هذا الهيكل يسمح لك ب:
- تغيير منطق واجهة البرمجة في `UserService` دون لمس الواجهة.
- تعديل الواجهة في `UserProfile` دون التأثير على جلب البيانات.
- اختبار كل مكون بشكل مستقل (مثل محاكاة `UserService` لاختبارات الواجهة).

---
### **كيفية تحديد انتهاكات المبدأ**

للتحقق مما إذا كان الكلاس ينتهك المبدأ، اسأل هذه الأسئلة:
1. **كم عدد المسؤوليات التي يتحملها الكلاس؟** إذا كان يقوم بأكثر من شيء (مثل تخزين البيانات *و* عرض الواجهة)، فهو ينتهك المبدأ.
2. **ما الأسباب التي قد تؤدي إلى تغيير هذا الكلاس؟** إذا كانت هناك أسباب متعددة غير مترابطة (مثل تغييرات قاعدة البيانات أو الواجهة)، فالكلاس لديه مسؤوليات زائدة.
3. **هل يمكن إعادة استخدام الكلاس في سياقات مختلفة؟** إذا كان مرتبطًا بمنطق معين (مثل قاعدة بيانات معينة)، فهو غير معياري بما فيه الكفاية.

---
### **الأخطاء الشائعة وكيفية تجنبها**

1. **التقسيم المفرط للمسؤوليات**:
   - تقسيم الكلاسات بشكل مفرط قد يؤدي إلى تعقيد زائد. على سبيل المثال، لا تنشئ كلاسات منفصلة لكل مهمة صغيرة ما لم تكن ضرورية للصيانة أو إعادة الاستخدام.
   - **الحل**: قم بتجميع الوظائف المتعلقة منطقيًا. على سبيل المثال، الاحتفاظ بتحديثات `name` و`email` في كلاس `User` مناسب، لأنهما يتعلقان بإدارة بيانات المستخدم.

2. **خلط المهام في ويدجتات Flutter**:
   - في Flutter، من المغري وضع المنطق التجاري (مثل استدعاءات واجهة برمجية) داخل الويدجتات، لكن هذا ينتهك المبدأ.
   - **الحل**: استخدم أنماطًا مثل **Provider**، **Bloc**، أو **Riverpod** لفصل المنطق التجاري عن عرض الواجهة.

3. **تجاهل الاعتماديات**:
   - الكلاسات التي تعتمد مباشرة على أنظمة خارجية (مثل قواعد البيانات أو واجهات برمجية) تكون أصعب في الاختبار وإعادة الاستخدام.
   - **الحل**: استخدم حقن الاعتماديات (كما في مثال Flutter) لتمرير الاعتماديات، مما يجعل الكلاسات أكثر مرونة.

---
### **متى تطبق المبدأ؟**

- **في بداية التصميم**: طبق المبدأ عند تصميم الكلاسات لضمان المعيارية من البداية.
- **أثناء إعادة الهيكلة**: إذا أصبح الكلاس معقدًا أو صعب الصيانة، أعد هيكلته ليتبع المبدأ.
- **في المشاريع الكبيرة**: المبدأ مهم جدًا في الفرق الكبيرة أو التطبيقات المعقدة (مثل تطبيقات Flutter متعددة الميزات) لتقليل الاقتران وتحسين التعاون.

---

سأقدم لك مثالًا برمجيًا معقدًا وشائع الاستخدام في **Dart** ينتهك **مبدأ المسؤولية الواحدة (SRP)**، ثم سأعيد هيكلته ليتبع المبدأ، مع شرح مفصل لكيفية الحل. المثال سيكون واقعيًا ويحاكي سيناريو شائعًا في تطوير تطبيقات **Flutter**، مثل إدارة بيانات المستخدم مع جلب البيانات من واجهة برمجية (API)، حفظها محليًا باستخدام قاعدة بيانات (مثل SQLite)، وتنسيقها لعرضها في واجهة مستخدم معقدة. سأستخدم مكتبات شائعة مثل `http` لجلب البيانات و`sqflite` للتخزين المحلي.

### **المثال : انتهاك مبدأ المسؤولية الواحدة**

في هذا المثال، لدينا كلاس `UserManager` يقوم بـ:
1. جلب بيانات المستخدم من واجهة برمجية (API).
2. حفظ البيانات في قاعدة بيانات محلية (SQLite).
3. تنسيق البيانات لعرضها في واجهة مستخدم Flutter.
4. التحقق من صحة بيانات المستخدم (مثل التحقق من البريد الإلكتروني).

هذا الكلاس ينتهك SRP لأنه يحتوي على مسؤوليات متعددة غير مترابطة.

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class UserManager extends StatelessWidget {
  String name = '';
  String email = '';
  bool isEmailValid = false;

  // المسؤولية 1: التحقق من صحة البريد الإلكتروني
  bool validateEmail(String email) {
    final emailRegex = RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$');
    isEmailValid = emailRegex.hasMatch(email);
    return isEmailValid;
  }

  // المسؤولية 2: جلب بيانات المستخدم من واجهة برمجية
  Future<void> fetchUserFromApi(int userId) async {
    final response = await http.get(Uri.parse('https://api.example.com/users/$userId'));
    if (response.statusCode == 200) {
      final data = jsonDecode(response.body);
      name = data['name'];
      email = data['email'];
      validateEmail(email); // التحقق من البريد
      print('تم جلب المستخدم: $name, $email');
    } else {
      throw Exception('فشل جلب البيانات');
    }
  }

  // المسؤولية 3: حفظ البيانات في قاعدة بيانات محلية (SQLite)
  Future<void> saveToDatabase() async {
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'users.db');
    final database = await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute(
          'CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT, email TEXT)',
        );
      },
    );
    await database.insert(
      'users',
      {'name': name, 'email': email},
      conflictAlgorithm: ConflictAlgorithm.replace,
    );
    print('تم حفظ المستخدم في قاعدة البيانات: $name, $email');
  }

  // المسؤولية 4: عرض واجهة المستخدم
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      future: fetchUserFromApi(1), // جلب بيانات المستخدم
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        }
        if (snapshot.hasError) {
          return Text('خطأ: ${snapshot.error}');
        }
        return Column(
          children: [
            Text(
              'الاسم: $name',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            Text(
              'البريد الإلكتروني: $email',
              style: TextStyle(
                fontSize: 16,
                color: isEmailValid ? Colors.green : Colors.red,
              ),
            ),
            ElevatedButton(
              onPressed: () async {
                await saveToDatabase();
                ScaffoldMessenger.of(context).showSnackBar(
                  SnackBar(content: Text('تم حفظ المستخدم')),
                );
              },
              child: Text('حفظ المستخدم'),
            ),
          ],
        );
      },
    );
  }
}
```

#### **لماذا ينتهك هذا الكود SRP؟**
- **المسؤوليات المتعددة**:
  1. **التحقق من صحة البيانات** (`validateEmail`): التحقق من صحة البريد الإلكتروني.
  2. **جلب البيانات** (`fetchUserFromApi`): التعامل مع استدعاءات واجهة برمجية.
  3. **حفظ البيانات** (`saveToDatabase`): إدارة قاعدة بيانات SQLite.
  4. **عرض الواجهة** (`build`): إنشاء واجهة مستخدم Flutter.
- **أسباب التغيير**:
  - إذا تغيرت قواعد التحقق من البريد الإلكتروني (مثل إضافة قواعد جديدة)، يجب تعديل الكلاس.
  - إذا تغيرت واجهة البرمجة (API) أو طريقة الاتصال، يجب تعديل الكلاس.
  - إذا تغيرت قاعدة البيانات (مثل الانتقال إلى Firebase)، يجب تعديل الكلاس.
  - إذا تغير تصميم الواجهة (مثل إضافة عناصر جديدة)، يجب تعديل الكلاس.
- **المشاكل**:
  - **صعوبة الصيانة**: التغييرات في أي مسؤولية تؤثر على الكلاس بأكمله.
  - **صعوبة الاختبار**: اختبار الواجهة يتطلب محاكاة واجهة البرمجة وقاعدة البيانات.
  - **قلة إعادة الاستخدام**: الكلاس مرتبط بشدة بواجهة Flutter، مما يحد من استخدامه في سياقات أخرى (مثل تطبيق ويب أو خادم).

---
### **إعادة هيكلة الكود ليتبع SRP**

لإصلاح هذا الانتهاك، سنقسم المسؤوليات إلى كلاسات منفصلة، كل منها يركز على مهمة واحدة فقط. سنستخدم **حقن الاعتماديات (Dependency Injection)** لتقليل الاقتران وتحسين قابلية الاختبار. الكلاسات ستكون:
1. `User`: نموذج بيانات المستخدم.
2. `UserValidator`: التحقق من صحة بيانات المستخدم.
3. `UserService`: جلب البيانات من واجهة برمجية.
4. `UserRepository`: حفظ البيانات في قاعدة بيانات.
5. `UserProfile`: عرض واجهة المستخدم.

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

// المسؤولية 1: نموذج بيانات المستخدم
class User {
  final String name;
  final String email;

  User(this.name, this.email);
}

// المسؤولية 2: التحقق من صحة بيانات المستخدم
class UserValidator {
  bool validateEmail(String email) {
    final emailRegex = RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$');
    return emailRegex.hasMatch(email);
  }
}

// المسؤولية 3: جلب بيانات المستخدم من واجهة برمجية
class UserService {
  Future<User> fetchUserFromApi(int userId) async {
    final response = await http.get(Uri.parse('https://api.example.com/users/$userId'));
    if (response.statusCode == 200) {
      final data = jsonDecode(response.body);
      return User(data['name'], data['email']);
    } else {
      throw Exception('فشل جلب البيانات');
    }
  }
}

// المسؤولية 4: حفظ البيانات في قاعدة بيانات محلية
class UserRepository {
  Future<Database> _getDatabase() async {
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'users.db');
    return await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute(
          'CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT, email TEXT)',
        );
      },
    );
  }

  Future<void> saveToDatabase(User user) async {
    final database = await _getDatabase();
    await database.insert(
      'users',
      {'name': user.name, 'email': user.email},
      conflictAlgorithm: ConflictAlgorithm.replace,
    );
    print('تم حفظ المستخدم في قاعدة البيانات: ${user.name}, ${user.email}');
  }
}

// المسؤولية 5: عرض واجهة المستخدم
class UserProfile extends StatelessWidget {
  final UserService userService;
  final UserRepository userRepository;
  final UserValidator userValidator;

  UserProfile({
    required this.userService,
    required this.userRepository,
    required this.userValidator,
  });

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<User>(
      future: userService.fetchUserFromApi(1),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        }
        if (snapshot.hasError) {
          return Text('خطأ: ${snapshot.error}');
        }
        final user = snapshot.data!;
        final isEmailValid = userValidator.validateEmail(user.email);
        return Column(
          children: [
            Text(
              'الاسم: ${user.name}',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            Text(
              'البريد الإلكتروني: ${user.email}',
              style: TextStyle(
                fontSize: 16,
                color: isEmailValid ? Colors.green : Colors.red,
              ),
            ),
            ElevatedButton(
              onPressed: () async {
                await userRepository.saveToDatabase(user);
                ScaffoldMessenger.of(context).showSnackBar(
                  SnackBar(content: Text('تم حفظ المستخدم')),
                );
              },
              child: Text('حفظ المستخدم'),
            ),
          ],
        );
      },
    );
  }
}

// مثال الاستخدام
void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: UserProfile(
        userService: UserService(),
        userRepository: UserRepository(),
        userValidator: UserValidator(),
      ),
    ),
  ));
}
```

---
### **كيف تم حل المشكلة؟**

#### **1. تقسيم المسؤوليات**
-ا **User**: يحتوي على نموذج البيانات فقط (`name` و`email`). هذا الكلاس مسؤول عن تخزين بيانات المستخدم وهيكلتها.
-ا **UserValidator**: يتعامل مع التحقق من صحة البيانات (مثل البريد الإلكتروني). يمكن توسيعه ليشمل قواعد تحقق إضافية دون التأثير على الكلاسات الأخرى.
-ا **UserService**: يركز على جلب البيانات من واجهة برمجية. إذا تغيرت الواجهة (مثل تغيير عنوان URL أو هيكل البيانات)، يتم تعديل هذا الكلاس فقط.
-ا **UserRepository**: يدير التخزين المحلي باستخدام SQLite. إذا تغيرت قاعدة البيانات (مثل التحول إلى Hive أو Firebase)، يتم تعديل هذا الكلاس فقط.
-ا **UserProfile**: يركز على عرض واجهة المستخدم في Flutter. إذا تغير تصميم الواجهة، يتم تعديل هذا الكلاس فقط.

#### **2. حقن الاعتماديات**
- تم تمرير الكلاسات (`UserService`, `UserRepository`, `UserValidator`) إلى `UserProfile` كاعتماديات عبر المُنشئ (constructor). هذا يسمح ب:
  - **استبدال الاعتماديات**: يمكن استخدام كائنات وهمية (mock objects) للاختبار.
  - **إعادة الاستخدام**: يمكن استخدام الكلاسات في سياقات مختلفة (مثل تطبيق ويب أو خادم).
  - **تقليل الاقتران**: الكلاسات ليست مرتبطة ببعضها بشكل مباشر.

#### **3. الفوائد**
- **سهولة الصيانة**: كل كلاس له سبب واحد للتغيير. على سبيل المثال، تغيير قاعدة البيانات لا يؤثر على الواجهة أو التحقق من البيانات.
- **سهولة الاختبار**: يمكن اختبار كل كلاس على حدة. على سبيل المثال، يمكن اختبار `UserService` بمحاكاة استجابات واجهة البرمجة دون الحاجة إلى قاعدة بيانات.
- **إعادة الاستخدام**: يمكن استخدام `User` أو `UserValidator` في مشاريع أخرى دون تغيير.
- **المرونة**: يمكن استبدال SQLite بقاعدة بيانات أخرى أو تغيير واجهة البرمجة دون التأثير على باقي الكود.

---
### **كيفية تطبيق هذا الحل في مشاريعك**

1. **تحديد المسؤوليات**:
   - قم بتحليل الكلاس واسأل: "ما المهام التي يقوم بها؟". إذا كانت هناك مهام متعددة (مثل جلب البيانات وعرضها)، افصلها إلى كلاسات مختلفة.
   - في المثال أعلاه، حددنا أربع مسؤوليات: النموذج، التحقق، جلب البيانات، وحفظها، وعرض الواجهة.

2. **تصميم النماذج أولاً**:
   - ابدأ بإنشاء نموذج بيانات بسيط (مثل `User`) لتمثيل الكيانات الأساسية في التطبيق.

3. **فصل المنطق**:
   - ضع منطق الأعمال (مثل التحقق أو جلب البيانات) في كلاسات منفصلة مثل `UserValidator` و`UserService`.
   - ضع منطق التخزين في كلاس مثل `UserRepository`.

4. **استخدام حقن الاعتماديات**:
   - مرر الكلاسات كاعتماديات بدلاً من إنشائها داخل الكلاس. هذا يجعل الكود مرنًا وسهل الاختبار.
   - في Flutter، يمكن استخدام أنماط مثل **Provider** أو **Riverpod** او **bloc** او **cubit** او **GetX** وغيرها لإدارة الاعتماديات بشكل أكثر فعالية.

5. **اختبار كل كلاس**:
   - اكتب اختبارات وحدة (unit tests) لكل كلاس. على سبيل المثال:
     - اختبر `UserValidator` للتحقق من صحة البريد الإلكتروني.
     - اختبر `UserService` بمحاكاة استجابات واجهة البرمجة.
     - اختبر `UserRepository` بمحاكاة قاعدة بيانات.

6. **إضافة ميزات جديدة**:
   - إذا أردت إضافة ميزة جديدة (مثل التحقق من رقم الهاتف)، أضفها إلى `UserValidator` دون التأثير على الكلاسات الأخرى.
   - إذا أردت تغيير قاعدة البيانات إلى Firebase، قم بتحديث `UserRepository` فقط.

---
### **مثال اختبار الكود**

لتوضيح سهولة الاختبار بعد إعادة الهيكلة، إليك اختبارًا بسيطًا لـ `UserValidator`:

```dart
import 'package:test/test.dart';
import 'user_management_refactored.dart';

void main() {
  test('UserValidator validates email correctly', () {
    final validator = UserValidator();
    expect(validator.validateEmail('alice@example.com'), true);
    expect(validator.validateEmail('invalid-email'), false);
  });
}
```

هذا الاختبار يركز فقط على `UserValidator`، مما يجعل عملية الاختبار بسيطة ومركزة.

---
سأقدم الان مثالًا برمجيًا معقدًا اكثر وشائعًا في تطوير تطبيقات **Flutter** باستخدام **Dart**، ينتهك **مبدأ المسؤولية الواحدة (SRP)**، ثم سأعيد هيكلته ليتبع المبدأ. المثال سيكون أكثر تعقيدًا، يحاكي سيناريو واقعيًا في تطبيق إدارة الطلبات في متجر إلكتروني، يتضمن:
- **جلب بيانات الطلبات** من واجهة برمجية (API) مع معالجة الأخطاء.
- **حفظ الطلبات** في قاعدة بيانات محلية (SQLite) مع دعم التزامن.
- **التحقق من صحة بيانات الطلب** (مثل التحقق من الحد الأدنى للطلب).
- **حساب التكلفة الإجمالية** للطلب مع الضرائب والخصومات.
- **إرسال إشعارات** (مثل إشعار بريد إلكتروني أو إشعار دفع).
- **عرض الطلبات** في واجهة مستخدم تفاعلية مع إمكانية التصفية.

سأبدأ بكود معقد ينتهك SRP، ثم أعيد هيكلته مع شرح تفصيلي لكل خطوة، مع التركيز على التعقيد والعمق.

---
### **المثال : انتهاك مبدأ المسؤولية الواحدة**

في هذا المثال، لدينا كلاس `OrderProcessor` يقوم بجميع العمليات المذكورة أعلاه في تطبيق Flutter. هذا الكلاس ينتهك SRP لأنه يجمع مسؤوليات متعددة غير مترابطة.

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';
import 'package:mailer/mailer.dart';
import 'package:mailer/smtp_server.dart';

class OrderProcessor extends StatefulWidget {
  @override
  _OrderProcessorState createState() => _OrderProcessorState();
}

class _OrderProcessorState extends State<OrderProcessor> {
  List<Map<String, dynamic>> orders = [];
  bool isLoading = false;
  String errorMessage = '';

  // المسؤولية 1: جلب بيانات الطلبات من واجهة برمجية
  Future<void> fetchOrdersFromApi() async {
    setState(() => isLoading = true);
    try {
      final response = await http.get(Uri.parse('https://api.example.com/orders'));
      if (response.statusCode == 200) {
        final List<dynamic> data = jsonDecode(response.body);
        orders = data.cast<Map<String, dynamic>>();
        for (var order in orders) {
          if (!validateOrder(order)) {
            orders.remove(order);
          }
        }
        await saveOrdersToDatabase();
        setState(() => isLoading = false);
      } else {
        setState(() {
          isLoading = false;
          errorMessage = 'فشل جلب الطلبات: ${response.statusCode}';
        });
      }
    } catch (e) {
      setState(() {
        isLoading = false;
        errorMessage = 'خطأ: $e';
      });
    }
  }

  // المسؤولية 2: التحقق من صحة الطلب
  bool validateOrder(Map<String, dynamic> order) {
    final double total = order['total'] ?? 0.0;
    final int itemCount = order['items']?.length ?? 0;
    return total >= 10.0 && itemCount > 0; // الحد الأدنى للطلب 10.0 ويجب أن يحتوي على عناصر
  }

  // المسؤولية 3: حساب التكلفة الإجمالية مع الضرائب والخصومات
  double calculateTotalWithTaxAndDiscount(Map<String, dynamic> order) {
    double total = order['total'] ?? 0.0;
    final double taxRate = 0.15; // ضريبة 15%
    final double discount = order['discount'] ?? 0.0;
    total = total * (1 + taxRate) - discount;
    return total > 0 ? total : 0;
  }

  // المسؤولية 4: حفظ الطلبات في قاعدة بيانات محلية
  Future<void> saveOrdersToDatabase() async {
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'orders.db');
    final database = await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute(
          'CREATE TABLE orders (id INTEGER PRIMARY KEY, data TEXT)',
        );
      },
    );
    for (var order in orders) {
      await database.insert(
        'orders',
        {'id': order['id'], 'data': jsonEncode(order)},
        conflictAlgorithm: ConflictAlgorithm.replace,
      );
    }
    print('تم حفظ ${orders.length} طلب في قاعدة البيانات');
  }

  // المسؤولية 5: إرسال إشعار بريد إلكتروني
  Future<void> sendOrderNotification(Map<String, dynamic> order) async {
    final smtpServer = gmail('username', 'password');
    final message = Message()
      ..from = Address('username@gmail.com', 'متجرنا')
      ..recipients.add(order['customerEmail'])
      ..subject = 'تأكيد الطلب #${order['id']}'
      ..text = 'تم استلام طلبك بقيمة ${calculateTotalWithTaxAndDiscount(order)}';

    try {
      await send(message, smtpServer);
      print('تم إرسال إشعار للطلب #${order['id']}');
    } catch (e) {
      print('فشل إرسال الإشعار: $e');
    }
  }

  // المسؤولية 6: عرض واجهة المستخدم مع التصفية
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('إدارة الطلبات')),
      body: isLoading
          ? Center(child: CircularProgressIndicator())
          : errorMessage.isNotEmpty
              ? Center(child: Text(errorMessage))
              : Column(
                  children: [
                    Padding(
                      padding: EdgeInsets.all(8.0),
                      child: TextField(
                        decoration: InputDecoration(labelText: 'تصفية حسب الحد الأدنى للتكلفة'),
                        onChanged: (value) {
                          setState(() {
                            orders = orders.where((order) {
                              return calculateTotalWithTaxAndDiscount(order) >=
                                  (double.tryParse(value) ?? 0.0);
                            }).toList();
                          });
                        },
                      ),
                    ),
                    Expanded(
                      child: ListView.builder(
                        itemCount: orders.length,
                        itemBuilder: (context, index) {
                          final order = orders[index];
                          final total = calculateTotalWithTaxAndDiscount(order);
                          return ListTile(
                            title: Text('طلب #${order['id']}'),
                            subtitle: Text('التكلفة: $total'),
                            trailing: ElevatedButton(
                              onPressed: () async {
                                await sendOrderNotification(order);
                                ScaffoldMessenger.of(context).showSnackBar(
                                  SnackBar(content: Text('تم إرسال إشعار للطلب #${order['id']}')),
                                );
                              },
                              child: Text('إرسال إشعار'),
                            ),
                          );
                        },
                      ),
                    ),
                    ElevatedButton(
                      onPressed: fetchOrdersFromApi,
                      child: Text('جلب الطلبات'),
                    ),
                  ],
                ),
    );
  }
}
```

#### **لماذا ينتهك هذا الكود SRP؟**
- **المسؤوليات المتعددة**:
  1. **جلب البيانات** (`fetchOrdersFromApi`): التعامل مع واجهة برمجية ومعالجة الأخطاء.
  2. **التحقق من الطلب** (`validateOrder`): التحقق من صحة الطلبات (الحد الأدنى للتكلفة وعدد العناصر).
  3. **حساب التكلفة** (`calculateTotalWithTaxAndDiscount`): تطبيق الضرائب والخصومات.
  4. **حفظ البيانات** (`saveOrdersToDatabase`): إدارة قاعدة بيانات SQLite.
  5. **إرسال الإشعارات** (`sendOrderNotification`): إرسال إشعارات بريد إلكتروني.
  6. **عرض الواجهة** (`build`): إنشاء واجهة مستخدم مع تصفية تفاعلية.
- **أسباب التغيير**:
  - تغيير قواعد التحقق (مثل الحد الأدنى للطلب).
  - تغيير واجهة البرمجة (مثل عنوان URL أو هيكل البيانات).
  - تغيير قاعدة البيانات (مثل التحول إلى Firebase).
  - تغيير طريقة حساب الضرائب أو الخصومات.
  - تغيير طريقة إرسال الإشعارات (مثل إضافة إشعارات دفع).
  - تغيير تصميم الواجهة أو منطق التصفية.
- **المشاكل**:
  - **التعقيد العالي**: الكلاس يحتوي على منطق معقد يجمع بين واجهة المستخدم، قاعدة البيانات، والاتصال بالخادم.
  - **صعوبة الاختبار**: اختبار الواجهة يتطلب محاكاة واجهة البرمجة، قاعدة البيانات، وخدمة البريد.
  - **قلة المرونة**: الكلاس غير قابل لإعادة الاستخدام في سياقات أخرى (مثل تطبيق ويب أو خادم).
  - **صعوبة الصيانة**: أي تغيير في إحدى المسؤوليات يتطلب تعديل الكلاس بأكمله.

---
### **إعادة هيكلة الكود ليتبع SRP**

لإصلاح هذا الانتهاك، سنقسم المسؤوليات إلى كلاسات منفصلة، كل منها يركز على مهمة واحدة. سنستخدم **حقن الاعتماديات** و**أنماط التصميم** (مثل Repository Pattern) لتقليل الاقتران وتحسين المرونة. الكلاسات ستكون:
1. `Order`: نموذج بيانات الطلب.
2. `OrderValidator`: التحقق من صحة الطلبات.
3. `OrderService`: جلب البيانات من واجهة برمجية.
4. `OrderRepository`: حفظ البيانات في قاعدة بيانات.
5. `OrderCalculator`: حساب التكلفة الإجمالية.
6. `NotificationService`: إرسال الإشعارات.
7. `OrderScreen`: عرض واجهة المستخدم.

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';
import 'package:mailer/mailer.dart';
import 'package:mailer/smtp_server.dart';

// المسؤولية 1: نموذج بيانات الطلب
class Order {
  final int id;
  final double total;
  final List<Map<String, dynamic>> items;
  final double discount;
  final String customerEmail;

  Order({
    required this.id,
    required this.total,
    required this.items,
    required this.discount,
    required this.customerEmail,
  });

  factory Order.fromJson(Map<String, dynamic> json) {
    return Order(
      id: json['id'],
      total: (json['total'] as num).toDouble(),
      items: List<Map<String, dynamic>>.from(json['items'] ?? []),
      discount: (json['discount'] as num?)?.toDouble() ?? 0.0,
      customerEmail: json['customerEmail'] ?? '',
    );
  }

  Map<String, dynamic> toJson() => {
        'id': id,
        'total': total,
        'items': items,
        'discount': discount,
        'customerEmail': customerEmail,
      };
}

// المسؤولية 2: التحقق من صحة الطلب
class OrderValidator {
  bool validateOrder(Order order) {
    return order.total >= 10.0 && order.items.isNotEmpty;
  }
}

// المسؤولية 3: جلب بيانات الطلبات من واجهة برمجية
class OrderService {
  Future<List<Order>> fetchOrdersFromApi() async {
    final response = await http.get(Uri.parse('https://api.example.com/orders'));
    if (response.statusCode == 200) {
      final List<dynamic> data = jsonDecode(response.body);
      return data.map((json) => Order.fromJson(json)).toList();
    } else {
      throw Exception('فشل جلب الطلبات: ${response.statusCode}');
    }
  }
}

// المسؤولية 4: حفظ البيانات في قاعدة بيانات محلية
class OrderRepository {
  Future<Database> _getDatabase() async {
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'orders.db');
    return await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute(
          'CREATE TABLE orders (id INTEGER PRIMARY KEY, data TEXT)',
        );
      },
    );
  }

  Future<void> saveOrders(List<Order> orders) async {
    final database = await _getDatabase();
    final batch = database.batch();
    for (var order in orders) {
      batch.insert(
        'orders',
        {'id': order.id, 'data': jsonEncode(order.toJson())},
        conflictAlgorithm: ConflictAlgorithm.replace,
      );
    }
    await batch.commit();
    print('تم حفظ ${orders.length} طلب في قاعدة البيانات');
  }
}

// المسؤولية 5: حساب التكلفة الإجمالية
class OrderCalculator {
  double calculateTotalWithTaxAndDiscount(Order order) {
    const double taxRate = 0.15; // ضريبة 15%
    final total = order.total * (1 + taxRate) - order.discount;
    return total > 0 ? total : 0;
  }
}

// المسؤولية 6: إرسال الإشعارات
class NotificationService {
  Future<void> sendOrderNotification(Order order, double total) async {
    final smtpServer = gmail('username', 'password');
    final message = Message()
      ..from = Address('username@gmail.com', 'متجرنا')
      ..recipients.add(order.customerEmail)
      ..subject = 'تأكيد الطلب #${order.id}'
      ..text = 'تم استلام طلبك بقيمة $total';

    try {
      await send(message, smtpServer);
      print('تم إرسال إشعار للطلب #${order.id}');
    } catch (e) {
      throw Exception('فشل إرسال الإشعار: $e');
    }
  }
}

// المسؤولية 7: عرض واجهة المستخدم
class OrderScreen extends StatefulWidget {
  final OrderService orderService;
  final OrderRepository orderRepository;
  final OrderValidator orderValidator;
  final OrderCalculator orderCalculator;
  final NotificationService notificationService;

  OrderScreen({
    required this.orderService,
    required this.orderRepository,
    required this.orderValidator,
    required this.orderCalculator,
    required this.notificationService,
  });

  @override
  _OrderScreenState createState() => _OrderScreenState();
}

class _OrderScreenState extends State<OrderScreen> {
  List<Order> orders = [];
  bool isLoading = false;
  String errorMessage = '';
  double filterTotal = 0.0;

  Future<void> _fetchAndSaveOrders() async {
    setState(() => isLoading = true);
    try {
      final fetchedOrders = await widget.orderService.fetchOrdersFromApi();
      final validOrders = fetchedOrders.where((order) => widget.orderValidator.validateOrder(order)).toList();
      await widget.orderRepository.saveOrders(validOrders);
      setState(() {
        orders = validOrders;
        isLoading = false;
      });
    } catch (e) {
      setState(() {
        isLoading = false;
        errorMessage = 'خطأ: $e';
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('إدارة الطلبات')),
      body: isLoading
          ? Center(child: CircularProgressIndicator())
          : errorMessage.isNotEmpty
              ? Center(child: Text(errorMessage))
              : Column(
                  children: [
                    Padding(
                      padding: EdgeInsets.all(8.0),
                      child: TextField(
                        decoration: InputDecoration(labelText: 'تصفية حسب الحد الأدنى للتكلفة'),
                        onChanged: (value) {
                          setState(() {
                            filterTotal = double.tryParse(value) ?? 0.0;
                          });
                        },
                      ),
                    ),
                    Expanded(
                      child: ListView.builder(
                        itemCount: orders.length,
                        itemBuilder: (context, index) {
                          final order = orders[index];
                          final total = widget.orderCalculator.calculateTotalWithTaxAndDiscount(order);
                          if (total < filterTotal) return SizedBox.shrink();
                          return ListTile(
                            title: Text('طلب #${order.id}'),
                            subtitle: Text('التكلفة: $total'),
                            trailing: ElevatedButton(
                              onPressed: () async {
                                try {
                                  await widget.notificationService.sendOrderNotification(order, total);
                                  ScaffoldMessenger.of(context).showSnackBar(
                                    SnackBar(content: Text('تم إرسال إشعار للطلب #${order.id}')),
                                  );
                                } catch (e) {
                                  ScaffoldMessenger.of(context).showSnackBar(
                                    SnackBar(content: Text('فشل إرسال الإشعار: $e')),
                                  );
                                }
                              },
                              child: Text('إرسال إشعار'),
                            ),
                          );
                        },
                      ),
                    ),
                    ElevatedButton(
                      onPressed: _fetchAndSaveOrders,
                      child: Text('جلب الطلبات'),
                    ),
                  ],
                ),
    );
  }
}

// مثال الاستخدام
void main() {
  runApp(MaterialApp(
    home: OrderScreen(
      orderService: OrderService(),
      orderRepository: OrderRepository(),
      orderValidator: OrderValidator(),
      orderCalculator: OrderCalculator(),
      notificationService: NotificationService(),
    ),
  ));
}
```

---

### **كيف تم حل المشكلة؟**

#### **1. تقسيم المسؤوليات**
- **Order**: نموذج بيانات الطلب، يحتوي على الحقول (`id`, `total`, `items`, `discount`, `customerEmail`) مع طرق تحويل إلى/من JSON.
- **OrderValidator**: يتحقق من صحة الطلب بناءً على الحد الأدنى للتكلفة وعدد العناصر.
- **OrderService**: يجلب الطلبات من واجهة برمجية ويحولها إلى كائنات `Order`.
- **OrderRepository**: يدير حفظ الطلبات في قاعدة بيانات SQLite باستخدام معاملات (batch) لتحسين الأداء.
- **OrderCalculator**: يحسب التكلفة الإجمالية مع الضرائب والخصومات.
- **NotificationService**: يدير إرسال الإشعارات (بريد إلكتروني في هذا المثال).
- **OrderScreen**: يركز على عرض واجهة المستخدم مع دعم التصفية التفاعلية.

#### **2. حقن الاعتماديات**
- تم تمرير جميع الكلاسات (`OrderService`, `OrderRepository`, `OrderValidator`, `OrderCalculator`, `NotificationService`) إلى `OrderScreen` عبر المُنشئ. هذا يسمح ب:
  - **الاختبار السهل**: يمكن محاكاة أي خدمة (مثل `OrderService`) باستخدام كائنات وهمية.
  - **المرونة**: يمكن استبدال أي خدمة (مثل استخدام Firebase بدلاً من SQLite).
  - **إعادة الاستخدام**: يمكن استخدام الكلاسات في سياقات مختلفة (مثل تطبيق ويب أو خادم).

#### **3. تحسينات إضافية**
- **معالجة الأخطاء**: كل خدمة تدير أخطاءها بشكل مستقل، مع رمي استثناءات يمكن التعامل معها في الواجهة.
- **الأداء**: استخدام معاملات (batch) في `OrderRepository` لتحسين أداء حفظ البيانات.
- **التوسعية**: يمكن توسيع كل كلاس بسهولة. على سبيل المثال، يمكن إضافة قواعد تحقق جديدة إلى `OrderValidator` أو دعم إشعارات دفع في `NotificationService`.

#### **4. الفوائد**
- **سهولة الصيانة**: كل كلاس له سبب واحد للتغيير. على سبيل المثال، تغيير طريقة حساب الضرائب يتطلب تعديل `OrderCalculator` فقط.
- **سهولة الاختبار**: يمكن اختبار كل كلاس على حدة. على سبيل المثال:
  - اختبار `OrderValidator` للتحقق من صحة الطلبات.
  - اختبار `OrderService` بمحاكاة استجابات واجهة البرمجة.
  - اختبار `OrderRepository` بمحاكاة قاعدة بيانات.
- **إعادة الاستخدام**: يمكن استخدام `Order`, `OrderCalculator`, أو `NotificationService` في مشاريع أخرى.
- **التوسعية**: يمكن إضافة ميزات جديدة (مثل إشعارات دفع أو تصفية متقدمة) دون التأثير على الكلاسات الأخرى.

---
### **كيفية تطبيق هذا الحل في مشاريعك**

1. **تحليل المسؤوليات**:
   - حدد جميع المهام التي يقوم بها الكلاس. في هذا المثال، حددنا ست مسؤوليات (نموذج، تحقق، جلب، حفظ، حساب، إشعارات، واجهة).
   - إذا كان الكلاس يقوم بأكثر من مهمة، افصلها إلى كلاسات مستقلة.
   
1. **تصميم نموذج البيانات**:
   - ابدأ بنموذج بيانات واضح (مثل `Order`) يحتوي على الحقول الأساسية وطرق تحويل (مثل `toJson` و`fromJson`).

3. **فصل المنطق**:
   - ضع كل نوع من المنطق في كلاس منفصل:
     - منطق الأعمال (مثل التحقق أو الحساب) في كلاسات مثل `OrderValidator` و`OrderCalculator`.
     - التفاعل مع الخدمات الخارجية (مثل API أو قاعدة بيانات) في كلاسات مثل `OrderService` و`OrderRepository`.
     - إدارة الإشعارات في كلاس مثل `NotificationService`.
     - عرض الواجهة في كلاس مثل `OrderScreen`.

4. **استخدام حقن الاعتماديات**:
   - مرر الخدمات كاعتماديات عبر المُنشئ أو استخدم أنماط إدارة الحالة مثل **Provider**, **Riverpod**, أو **Bloc** لتسهيل إدارة الاعتماديات في Flutter.

5. **اختبار كل كلاس**:
   - اكتب اختبارات وحدة لكل كلاس. على سبيل المثال:

```dart
import 'package:test/test.dart';
import 'order_management_refactored.dart';

void main() {
  test('OrderValidator validates order correctly', () {
    final validator = OrderValidator();
    final validOrder = Order(
      id: 1,
      total: 20.0,
      items: [{'name': 'منتج 1', 'price': 20.0}],
      discount: 0.0,
      customerEmail: 'test@example.com',
    );
    final invalidOrder = Order(
      id: 2,
      total: 5.0,
      items: [],
      discount: 0.0,
      customerEmail: 'test@example.com',
    );
    expect(validator.validateOrder(validOrder), true);
    expect(validator.validateOrder(invalidOrder), false);
  });
}
```

6. **التعامل مع التعقيد**:
   - إذا كان التطبيق معقدًا (مثل إدارة الطلبات مع ميزات متقدمة)، استخدم أنماط تصميم مثل **Repository Pattern** أو **Service Layer** لتنظيم الكود.
   - لإدارة الحالة في Flutter، استخدم **Bloc** أو **Riverpod** وغيرها لفصل منطق الأعمال عن الواجهة بشكل أكبر.

7. **إضافة ميزات جديدة**:
   - إذا أردت إضافة ميزة جديدة (مثل تصفية حسب حالة الطلب)، أضفها إلى `OrderScreen` أو أنشئ كلاسًا جديدًا للتصفية.
   - إذا أردت دعم إشعارات دفع، قم بتوسيع `NotificationService` دون التأثير على الكلاسات الأخرى.

---
### **لماذا هذا المثال معقد؟**
- **التكامل مع خدمات متعددة**: يتضمن واجهة برمجية، قاعدة بيانات SQLite، وخدمة بريد إلكتروني.
- **معالجة الأخطاء**: يتعامل مع أخطاء الشبكة، قاعدة البيانات، والإشعارات بشكل منفصل.
- **الواجهة التفاعلية**: يدعم تصفية الطلبات بناءً على التكلفة الإجمالية.
- **الأداء**: يستخدم معاملات قاعدة البيانات (batch) لتحسين أداء الحفظ.
- **التوسعية**: يمكن توسيعه لدعم ميزات مثل إشعارات الدفع، قواعد بيانات مختلفة، أو تصفية متقدمة.

---
### **الخلاصة**
- **الكود المنتهك للمبدأ** يجمع مسؤوليات متعددة (نموذج، تحقق، جلب، حفظ، حساب، إشعارات، واجهة) في كلاس واحد، مما يجعله معقدًا، صعب الاختبار، وغير مرن.
- **الكود المعاد هيكلته** يفصل كل مسؤولية إلى كلاس مستقل، مع استخدام حقن الاعتماديات لتقليل الاقتران وتحسين الصيانة والاختبار.
- **كيفية الحل**:
  1. حدد المسؤوليات (نموذج، تحقق، جلب، حفظ، حساب، إشعارات، واجهة, ..... ).
  2. أنشئ كلاسات منفصلة لكل مسؤولية.
  3. استخدم حقن الاعتماديات لربط الكلاسات.
  4. اختبر كل كلاس على حدة.
  5. استخدم أنماط تصميم (مثل Repository Pattern) لتنظيم الكود وغيرها.
- **الفوائد**: كود معياري، سهل الصيانة، قابل للاختبار، وجاهز للتوسع.
---
### **الخلاصة**
**مبدأ المسؤولية الواحدة** يهدف إلى الحفاظ على تركيز الكلاسات على مهمة واحدة، مما يجعل كودك أكثر قابلية للصيانة، الاختبار، وإعادة الاستخدام. من خلال فصل المهام—مثل إدارة بيانات المستخدم، الحفظ، وتنسيق الواجهة—يتم تقليل مخاطر الأخطاء وتسهيل التكيف مع التغييرات. هذا المبدأ قيم بشكل خاص لتنظيم التطبيقات المعقدة، حيث يمكن أن يؤدي خلط المسؤوليات إلى قواعد كود غير قابلة للإدارة.
