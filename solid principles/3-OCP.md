### **2 - Open/Closed Principle - OCP**

**مبدأ الفتح/الإغلاق (Open/Closed Principle - OCP)** هو المبدأ الثاني من مبادئ **SOLID** في البرمجة الكائنية، وينص على أن **الكلاسات يجب أن تكون مفتوحة للتوسع (open for extension) ولكن مغلقة للتعديل (closed for modification)**. بمعنى آخر، يجب أن تتمكن من إضافة ميزات جديدة إلى الكلاس دون تغيير الكود الموجود داخله. هذا المبدأ يساعد في جعل الكود مرنًا وقابلًا للتوسع مع تقليل مخاطر الأخطاء عند إدخال تغييرات.

في هذا الرد، سأشرح **مبدأ الفتح/الإغلاق** بالتفصيل باستخدام لغة **Dart**، مع أمثلة برمجية معقدة توضح انتهاكه وكيفية إصلاحه، مع تطبيق عملي في سياق **Flutter**. سأتبع نفس نهج شرح مبدأ المسؤولية الواحدة (SRP) الذي قدمته سابقًا، مع التركيز على العمق والوضوح باللغة العربية.

---
### **ما هو مبدأ الفتح/الإغلاق؟**

**التعريف**: الكلاسات، الوحدات، أو الدوال يجب أن تكون مصممة بحيث يمكن توسيع سلوكها (إضافة ميزات جديدة) دون الحاجة إلى تعديل الكود الموجود. هذا يعني أنك تستطيع إضافة وظائف جديدة باستخدام الوراثة، الواجهات، أو أنماط التصميم (مثل Strategy أو Decorator) بدلاً من تغيير الكود الأصلي.

#### **النقاط الرئيسية لـ OCP**:
- **مفتوح للتوسع**: يمكن إضافة سلوك جديد (مثل دعم ميزة جديدة) بسهولة.
- **مغلق للتعديل**: لا يجب تغيير الكود الموجود لإضافة هذا السلوك.
- **الفوائد**:
  - **تقليل الأخطاء**: عدم تعديل الكود الموجود يقلل من مخاطر إدخال أخطاء.
  - **سهولة الصيانة**: الكود المستقر يسهل إدارته في المشاريع الكبيرة.
  - **إعادة الاستخدام**: التصميم المرن يسمح باستخدام الكلاسات في سياقات مختلفة.
  - **التوسعية**: يسهل إضافة ميزات جديدة مع مرور الوقت.

#### **لماذا مبدأ الفتح/الإغلاق (OCP) مهم ؟**

تخيل أنك تبني تطبيقًا لإدارة الطلبات في متجر إلكتروني، ولديك نظام يحسب تكلفة الشحن بناءً على نوع الشحن (عادي أو سريع). في البداية، صممت النظام بحيث يتحقق من نوع الشحن ويحسب التكلفة بناءً على قواعد محددة داخل جزء واحد من البرنامج.

الآن، إذا أراد المتجر إضافة نوع شحن جديد (مثل الشحن الدولي)، ستضطر إلى فتح الجزء الأساسي من النظام وتغييره لإضافة قاعدة جديدة للشحن الدولي. هذا التغيير يحمل مخاطر تقنية:
- **احتمالية الأخطاء**: قد تؤثر التغييرات على حسابات الشحن العادي أو السريع بطريقة غير متوقعة.
- **إعادة الاختبار**: كل تغيير يتطلب اختبار النظام بالكامل للتأكد من أن الشحن العادي والسريع لا يزالان يعملان بشكل صحيح.
- **زيادة التعقيد**: كلما أضفت أنواع شحن جديدة، يصبح النظام أكثر تعقيدًا وصعوبة في الصيانة.

**كيف يساعد OCP تقنيًا؟**  
مبدأ الفتح/الإغلاق يقول: صمم النظام بحيث يكون:
- **مفتوحًا للتوسع**: يمكنك إضافة أنواع شحن جديدة (مثل الشحن الدولي) بسهولة.
- **مغلقًا للتعديل**: لا حاجة لتغيير الأجزاء الأساسية التي تحسب الشحن العادي أو السريع.

**كيف يتم ذلك تقنيًا؟**  
بدلاً من وضع كل قواعد الشحن في مكان واحد، يمكنك تصميم النظام بحيث يكون لديك "قاعدة عامة" للشحن، وكل نوع شحن (عادي، سريع، دولي) ينفذ هذه القاعدة بطريقته الخاصة. النظام الأساسي يبقى ثابتًا، وكل ما تفعله هو إضافة جزء جديد للشحن الدولي دون المساس بالأجزاء القديمة.

**الفوائد التقنية**:
- **تقليل المخاطر**: لأنك لا تعدل الأجزاء الأساسية، فلا داعي للقلق بشأن كسر وظائف موجودة.
- **اختبار أسهل**: تحتاج فقط لاختبار الجزء الجديد (مثل الشحن الدولي) بدلاً من اختبار النظام كاملاً.
- **صيانة أبسط**: النظام يبقى منظمًا وسهل الفهم، حتى لو أضفت المزيد من أنواع الشحن.
- **إعادة استخدام أفضل**: يمكن استخدام نفس التصميم في مشاريع أخرى لأنه مرن ومنظم.

---

سأقدم لك عدة أمثلة برمجية بلغة **Dart** توضح انتهاك **مبدأ الفتح/الإغلاق (Open/Closed Principle - OCP)**، ثم سأعيد هيكلتها لتتبع المبدأ، مع شرح أسباب الانتهاك في كل مثال. كل مثال سيركز على سيناريو واقعي شائع في البرمجة، مع التركيز على العمق والتعقيد. الأمثلة ستكون:
1. **نظام تصفية البيانات** (مثل تصفية المنتجات في متجر إلكتروني).
2. **نظام حساب الخصومات** (لإدارة أنواع مختلفة من الخصومات).
3. **نظام تصدير البيانات** (مثل تصدير التقارير إلى صيغ مختلفة).
4. **نظام حساب مكافة ساعات العمل الإضافية**

كل مثال سيتضمن كودًا ينتهك OCP، ثم كودًا معاد هيكلته، مع شرح أسباب الانتهاك وكيفية الإصلاح. الأكواد ستكون توضيحية فقط وقد لا تعمل مباشرة (مثل استخدام عناوين API وهمية) لإيصال الفكرة.

### **المثال 1: نظام تصفية البيانات**

#### **انتهاك OCP**
كلاس `ProductFilter` يصفي المنتجات بناءً على نوع الفلتر (السعر، الفئة). إضافة فلتر جديد تتطلب تعديل الكلاس.

```dart
class Product {
  final String name;
  final double price;
  final String category;

  Product(this.name, this.price, this.category);
}

class ProductFilter {
  List<Product> filterProducts(List<Product> products, String filterType, dynamic value) {
    if (filterType == 'Price') {
      return products.where((p) => p.price <= (value as double)).toList();
    } else if (filterType == 'Category') {
      return products.where((p) => p.category == (value as String)).toList();
    } else {
      return products;
    }
  }
}

void main() {
  final products = [
    Product('Laptop', 1000.0, 'Electronics'),
    Product('Shirt', 50.0, 'Clothing'),
    Product('Phone', 800.0, 'Electronics'),
  ];
  final filter = ProductFilter();
  final filtered = filter.filterProducts(products, 'Price', 500.0);
  print(filtered.map((p) => p.name).toList());
}
```

##### **أسباب انتهاك OCP**
- **تعديل الكود**: إضافة فلتر جديد (مثل التقييم) تتطلب إضافة شرط `else if` في `filterProducts`.
- **زيادة التعقيد**: كل فلتر جديد يزيد من تعقيد الدالة.
- **عدم المرونة**: الكلاس غير قابل للتوسع بدون تعديل الكود الأصلي.

#### **إصلاح الانتهاك**
نستخدم واجهة `Filter` لتحديد سلوك التصفية، مع كلاسات منفصلة لكل نوع فلتر.

```dart
class Product {
  final String name;
  final double price;
  final String category;

  Product(this.name, this.price, this.category);
}

// الواجهة
abstract class Filter {
  List<Product> apply(List<Product> products, dynamic value);
}

// فلتر السعر
class PriceFilter implements Filter {
  @override
  List<Product> apply(List<Product> products, dynamic value) {
    return products.where((p) => p.price <= (value as double)).toList();
  }
}

// فلتر الفئة
class CategoryFilter implements Filter {
  @override
  List<Product> apply(List<Product> products, dynamic value) {
    return products.where((p) => p.category == (value as String)).toList();
  }
}

// معالج التصفية
class ProductFilter {
  final Filter filter;

  ProductFilter(this.filter);

  List<Product> filterProducts(List<Product> products, dynamic value) {
    return filter.apply(products, value);
  }
}

void main() {
  final products = [
    Product('Laptop', 1000.0, 'Electronics'),
    Product('Shirt', 50.0, 'Clothing'),
    Product('Phone', 800.0, 'Electronics'),
  ];
  final filter = ProductFilter(PriceFilter());
  final filtered = filter.filterProducts(products, 500.0);
  print(filtered.map((p) => p.name).toList());
}
```

##### **كيف تم الإصلاح؟**
- **واجهة `Filter`**: تحدد سلوك التصفية.
- **كلاسات منفصلة**: `PriceFilter` و`CategoryFilter` تنفذ الواجهة، ويمكن إضافة فلاتر جديدة (مثل `RatingFilter`) دون تعديل `ProductFilter`.
- **حقن الاعتماديات**: `ProductFilter` يعتمد على الواجهة، مما يجعله مغلقًا للتعديل.
- **الفوائد**: يمكن توسيع أنواع الفلاتر بسهولة، مع استقرار الكود.

---

### **المثال 2: نظام حساب الخصومات**

#### **انتهاك OCP**
كلاس `DiscountCalculator` يحسب الخصومات بناءً على نوع العميل (عادي، مميز). إضافة نوع خصم جديد تتطلب تعديل الكلاس.

```dart
class DiscountCalculator {
  double calculateDiscount(double total, String customerType) {
    if (customerType == 'Regular') {
      return total * 0.1; // خصم 10% للعميل العادي
    } else if (customerType == 'Premium') {
      return total * 0.2; // خصم 20% للعميل المميز
    } else {
      return 0.0;
    }
  }
}

void main() {
  final calculator = DiscountCalculator();
  final discount = calculator.calculateDiscount(1000.0, 'Premium');
  print('الخصم: $discount');
}
```

##### **أسباب انتهاك OCP**
- **تعديل الكود**: إضافة نوع عميل جديد (مثل VIP) تتطلب إضافة شرط `else if`.
- **زيادة التعقيد**: الدالة تصبح أكثر تعقيدًا مع كل نوع خصم جديد.
- **مخاطر الأخطاء**: تعديل الكود قد يؤثر على حسابات الخصومات الحالية.

#### **إصلاح الانتهاك**
نستخدم واجهة `DiscountStrategy` لتحديد سلوك حساب الخصم.

```dart
abstract class DiscountStrategy {
  double calculateDiscount(double total);
}

class RegularDiscount implements DiscountStrategy {
  @override
  double calculateDiscount(double total) {
    return total * 0.1; // خصم 10%
  }
}

class PremiumDiscount implements DiscountStrategy {
  @override
  double calculateDiscount(double total) {
    return total * 0.2; // خصم 20%
  }
}

class DiscountCalculator {
  final DiscountStrategy strategy;

  DiscountCalculator(this.strategy);

  double calculate(double total) {
    return strategy.calculateDiscount(total);
  }
}

void main() {
  final calculator = DiscountCalculator(PremiumDiscount());
  final discount = calculator.calculate(1000.0);
  print('الخصم: $discount');
}
```

##### **كيف تم الإصلاح؟**
- **واجهة `DiscountStrategy`**: تحدد سلوك حساب الخصم.
- **كلاسات منفصلة**: `RegularDiscount` و`PremiumDiscount` تنفذ الواجهة، ويمكن إضافة أنواع جديدة (مثل `VIPDiscount`).
- **حقن الاعتماديات**: `DiscountCalculator` يعتمد على الواجهة.
- **الفوائد**: الكود مفتوح لإضافة أنواع خصومات جديدة دون تعديل.

---
### **المثال 3: نظام تصدير البيانات**

#### **انتهاك OCP**
كلاس `DataExporter` يصدر البيانات إلى صيغ (JSON، CSV). إضافة صيغة جديدة تتطلب تعديل الكلاس.

```dart
class DataExporter {
  String exportData(List<Map<String, dynamic>> data, String format) {
    if (format == 'JSON') {
      return jsonEncode(data);
    } else if (format == 'CSV') {
      final header = data.first.keys.join(',');
      final rows = data.map((item) => item.values.join(',')).join('\n');
      return '$header\n$rows';
    } else {
      return 'الصيغة غير مدعومة';
    }
  }
}

void main() {
  final data = [
    {'name': 'Laptop', 'price': 1000},
    {'name': 'Phone', 'price': 800},
  ];
  final exporter = DataExporter();
  final result = exporter.exportData(data, 'JSON');
  print(result);
}
```

##### **أسباب انتهاك OCP**
- **تعديل الكود**: إضافة صيغة جديدة (مثل XML) تتطلب إضافة شرط `else if`.
- **التعقيد**: الدالة تصبح أكثر تعقيدًا مع كل صيغة جديدة.
- **عدم الاستقرار**: تعديل الكود قد يكسر تصدير الصيغ الحالية.

#### **إصلاح الانتهاك**
نستخدم واجهة `ExportFormat` لتحديد سلوك التصدير.

```dart
import 'dart:convert';

abstract class ExportFormat {
  String export(List<Map<String, dynamic>> data);
}

class JsonExport implements ExportFormat {
  @override
  String export(List<Map<String, dynamic>> data) {
    return jsonEncode(data);
  }
}

class CsvExport implements ExportFormat {
  @override
  String export(List<Map<String, dynamic>> data) {
    final header = data.first.keys.join(',');
    final rows = data.map((item) => item.values.join(',')).join('\n');
    return '$header\n$rows';
  }
}

class DataExporter {
  final ExportFormat format;

  DataExporter(this.format);

  String exportData(List<Map<String, dynamic>> data) {
    return format.export(data);
  }
}

void main() {
  final data = [
    {'name': 'Laptop', 'price': 1000},
    {'name': 'Phone', 'price': 800},
  ];
  final exporter = DataExporter(JsonExport());
  final result = exporter.exportData(data);
  print(result);
}
```

##### **كيف تم الإصلاح؟**
- **واجهة `ExportFormat`**: تحدد سلوك التصدير.
- **كلاسات منفصلة**: `JsonExport` و`CsvExport` تنفذ الواجهة، ويمكن إضافة صيغ جديدة (مثل `XmlExport`).
- **حقن الاعتماديات**: `DataExporter` يعتمد على الواجهة.
- **الفوائد**: الكود مفتوح لإضافة صيغ جديدة دون تعديل.

---
### **المثال 4: حساب مكافات ساعات العمل الإضافية**

حساب مكافآت ساعات العمل الإضافية لأنواع مختلفة من الموظفين.
### **انتهاك مبدأ الفتح/الإغلاق**
لتوضيح كيف يمكن أن ينتهك الكود OCP، سأقدم مثالًا معقدًا يدمج حساب المكافآت والتسجيل في قاعدة بيانات وإرسال إشعارات في كلاس واحد باستخدام شروط `if-else`.

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';
import 'package:mailer/mailer.dart';
import 'package:mailer/smtp_server.dart';

class Employee {
  final String name;
  final int id;
  final double basicSalary;
  final String type; // نوع الموظف

  Employee(this.id, this.name, this.basicSalary, this.type);
}

class EmployeeManager {
  Future<void> calculateBonus(Employee employee, int hours, String email) async {
    if (hours < 0) throw Exception('Hours cannot be negative');
    double hoursBonus = 0.0;
    String bonusType = '';

    // حساب المكافأة بناءً على نوع الموظف
    if (employee.type == 'Manager') {
      hoursBonus = ((employee.basicSalary / 30) * hours) * 2;
      bonusType = 'Manager Bonus';
    } else if (employee.type == 'Normal') {
      hoursBonus = (employee.basicSalary / 30) * hours;
      bonusType = 'Normal Bonus';
    } else if (employee.type == 'Senior') {
      hoursBonus = ((employee.basicSalary / 30) * hours) * 1.5;
      bonusType = 'Senior Bonus';
    } else if (employee.type == 'Intern') {
      hoursBonus = 0.0;
      bonusType = 'No Bonus';
    } else if (employee.type == 'PartTime') {
      hoursBonus = ((employee.basicSalary / 30) * hours) * 0.5;
      bonusType = 'Part-Time Bonus';
    } else {
      throw Exception('نوع الموظف غير مدعوم');
    }

    // طباعة التفاصيل
    print(
      "Name: ${employee.name}\nID: ${employee.id}\nHours Bonus Salary: ${hoursBonus.toStringAsFixed(2)}",
    );
    print('Total Salary: ${(employee.basicSalary + hoursBonus).toStringAsFixed(2)}');
    print("\n-----------------------\n");

    // تسجيل المكافأة في قاعدة البيانات
    final databasePath = await getDatabasesPath();
    final path = join(databasePath, 'bonuses.db');
    final database = await openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute(
          'CREATE TABLE bonuses (id INTEGER PRIMARY KEY, employee_id INTEGER, bonus_type TEXT, amount REAL)',
        );
      },
    );
    await database.insert(
      'bonuses',
      {
        'employee_id': employee.id,
        'bonus_type': bonusType,
        'amount': hoursBonus,
      },
      conflictAlgorithm: ConflictAlgorithm.replace,
    );

    // إرسال إشعار بالبريد الإلكتروني
    if (hoursBonus > 0) {
      final smtpServer = gmail('username', 'password');
      final message = Message()
        ..from = Address('username@gmail.com', 'شركتنا')
        ..recipients.add(email)
        ..subject = 'تأكيد مكافأة'
        ..text = 'تمت إضافة مكافأة بقيمة ${hoursBonus.toStringAsFixed(2)} لـ ${employee.name}';
      await send(message, smtpServer);
    }
  }
}

void main() async {
  final manager = EmployeeManager();

  // Manager Employee
  final employee1 = Employee(1, "Mohammed Anwar", 600, 'Manager');
  await manager.calculateBonus(employee1, 5, 'mohammed@example.com');

  // Normal Employee
  final employee2 = Employee(2, "Ahmed Mohammed", 600, 'Normal');
  await manager.calculateBonus(employee2, 5, 'ahmed@example.com');

  // Senior Employee
  final employee3 = Employee(3, "Sara Ali", 750, 'Senior');
  await manager.calculateBonus(employee3, 5, 'sara@example.com');

  // Intern Employee
  final employee4 = Employee(4, "Omar Salem", 200, 'Intern');
  await manager.calculateBonus(employee4, 5, 'omar@example.com');

  // Part-Time Employee
  final employee5 = Employee(5, "Lina Hussein", 400, 'PartTime');
  await manager.calculateBonus(employee5, 5, 'lina@example.com');
}
```

#### **لماذا ينتهك هذا الكود OCP؟**
- **تعديل الكود**:
  - إضافة نوع موظف جديد (مثل Freelancer) تتطلب تعديل دالة `calculateBonus` بإضافة شرط `else if` جديد.
- **زيادة التعقيد**:
  - الدالة تحتوي على شروط متعددة (`if-else`) لحساب المكافأة، التسجيل، والإشعارات، مما يجعلها معقدة وصعبة الصيانة.
- **مخاطر الأخطاء**:
  - تعديل الكود قد يكسر منطق الأنواع الأخرى (مثل تغيير نسبة مكافأة Senior بالخطأ).
- **دمج المسؤوليات**:
  - الكلاس `EmployeeManager` يتولى حساب المكافأة، الطباعة، التسجيل في قاعدة البيانات، وإرسال الإشعارات، مما ينتهك **SRP**.
- **صعوبة الاختبار**:
  - اختبار الدالة يتطلب محاكاة جميع حالات `employee.type`، بالإضافة إلى قاعدة البيانات والبريد الإلكتروني.
- **الاعتماد على `type`**:
  - استخدام حقل `type` في `Employee` لتحديد السلوك يجعل الكود غير مرن ومعرضًا للأخطاء (مثل إدخال نوع غير صحيح).

---
### **إعادة هيكلة الكود ليتبع OCP**

سأعيد تصميم الكود ليتبع OCP باستخدام الواجهات ونمط الاستراتيجية، مع فصل المسؤوليات لتغطية حساب المكافأة، التسجيل في قاعدة البيانات، وإرسال الإشعارات.

```dart

class Employee {
  final String name;
  final int id;
  final double basicSalary;

  Employee(this.id, this.name, this.basicSalary);
}

abstract class EmployeePrinter {
  void printEmployee(Employee employee, double hoursBonus);
}

class ConsoleEmployeePrinter implements EmployeePrinter {
  @override
  void printEmployee(Employee employee, double hoursBonus) {
    print(
      "Name: ${employee.name}\nID: ${employee.id}\nHours Bonus Salary: ${hoursBonus.toStringAsFixed(2)}",
    );
    print('Total Salary: ${(employee.basicSalary + hoursBonus).toStringAsFixed(2)}');
    print("\n-----------------------\n");
  }
}

class JsonEmployeePrinter implements EmployeePrinter {
  @override
  void printEmployee(Employee employee, double hoursBonus) {
    final data = {
      'id': employee.id,
      'name': employee.name,
      'basicSalary': employee.basicSalary,
      'hoursBonus': hoursBonus,
      'totalSalary': employee.basicSalary + hoursBonus,
    };
    print(jsonEncode(data));
    print("\n\n");
  }
}

class FancyEmployeePrinter implements EmployeePrinter {
  @override
  void printEmployee(Employee employee, double hoursBonus) {
    print("🌟 EMPLOYEE REPORT 🌟");
    print("🔹 Name       : ${employee.name}");
    print("🔹 ID         : ${employee.id}");
    print("🔹 Bonus      : \$${hoursBonus.toStringAsFixed(2)}");
    print(
      "🔹 Total Pay  : \$${(employee.basicSalary + hoursBonus).toStringAsFixed(2)}",
    );
    print("\n\n");
  }
}

class ShortEmployeePrinter implements EmployeePrinter {
  @override
  void printEmployee(Employee employee, double hoursBonus) {
    print(
      "${employee.name} (#${employee.id}) - Bonus: \$${hoursBonus.toStringAsFixed(2)}",
    );
    print("\n\n");
  }
}

class TableEmployeePrinter implements EmployeePrinter {
  @override
  void printEmployee(Employee employee, double hoursBonus) {
    // Format the values
    final totalSalary = (employee.basicSalary + hoursBonus).toStringAsFixed(2);
    final bonus = hoursBonus.toStringAsFixed(2);
    final salary = employee.basicSalary.toStringAsFixed(2);
    // Determine the maximum length for the content column to handle dynamic widths
    final labels = ['Name', 'Employee ID', 'Basic Salary', 'Hourly Bonus', 'Total Salary'];
    final values = [
      employee.name,
      employee.id.toString(),
      '\$$salary',
      '\$$bonus',
      '\$$totalSalary'
      ];

    // Find the longest label and value to set column widths
    const int labelColumnWidth = 20; // Fixed width for labels (e.g., "Name")
    int valueColumnWidth = 20; // Minimum width for values
    for (var value in values) {
      if (value.length > valueColumnWidth) {
        valueColumnWidth = value.length + 2; // Add padding for better spacing
      }
    }
    // Build the table
    final border = '+${'-' * (labelColumnWidth + 1)}+${'-' * valueColumnWidth}+';
    final separator = '|${'-' * (labelColumnWidth + 1)}+${'-' * valueColumnWidth}|';
    // Print the table
    print(border);
    for (int i = 0; i < labels.length; i++) {
      final label = labels[i].padRight(labelColumnWidth);
      final value = values[i].padRight(valueColumnWidth - 2).padLeft(valueColumnWidth);
      print('| $label|$value|');
      if (i < labels.length - 1) {
        print(separator);
      }
    }
    print(border);
    print(''); // Extra newline for spacing
  }
}

abstract class BonusCalculator {
  double calculateHoursBonus(Employee employee, int hours);
  String getBonusType();
}


// كلاس أساسي مجرد لحساب المكافأة الأساسية
// و توجد طريقة اخرى سيتم ذكرها في الشرح بعد هذا المثال
abstract class BaseBonusCalculator implements BonusCalculator {
  @override
  double calculateHoursBonus(Employee employee, int hours) {
    if (hours < 0) throw Exception('Hours cannot be negative');
    return _calculateBaseBonus(employee, hours) * getBonusMultiplier();
  }

  double _calculateBaseBonus(Employee employee, int hours) {
    return (employee.basicSalary / 30) * hours;
  }
  // يجب على الكلاسات الفرعية تحديد مضاعف المكافأة
  double getBonusMultiplier();
}

class ManagerBonusCalculator extends BaseBonusCalculator {
  @override
  String getBonusType() => 'Manager Bonus';

  @override
  double getBonusMultiplier() => 2.0;
}

class NormalBonusCalculator extends BaseBonusCalculator {
  @override
  String getBonusType() => 'Normal Bonus';

  @override
  double getBonusMultiplier() => 1.0;
}

class SeniorBonusCalculator extends BaseBonusCalculator {
  @override
  String getBonusType() => 'Senior Bonus';

  @override
  double getBonusMultiplier() => 1.5;
}

class InternBonusCalculator implements BonusCalculator {
  @override
  double calculateHoursBonus(Employee employee, int hours) {
    if (hours < 0) throw Exception('Hours cannot be negative');
    return 0.0;
  }

  @override
  String getBonusType() => 'No Bonus';
}

class PartTimeBonusCalculator extends BaseBonusCalculator {
  @override
  String getBonusType() => 'Part-Time Bonus';
  
  @override
  double getBonusMultiplier() => 0.5;
}

class BonusRepository {
  // Simulate database operation without creating a real database
  Future<void> logBonus(int employeeId, String bonusType, double amount) async {
    // Print a message to indicate the data is "saved"
    print('The data is saved: employee_id=$employeeId, bonus_type=$bonusType, amount=$amount');
  }
}

class NotificationService {
  Future<void> sendBonusNotification(String email, String employeeName, double amount, String bonusType) async {
    // Simulate sending a notification by printing a message
    print('Notification sent to $email: Bonus of ${amount.toStringAsFixed(2)} added for $employeeName (Type: $bonusType)');
  }
}

class EmployeeManager {
  final BonusCalculator calculator;
  final BonusRepository repository;
  final NotificationService notificationService;
  final EmployeePrinter printer;

  EmployeeManager({
    required this.calculator,
    required this.repository,
    required this.notificationService,
    required this.printer,
  });

  Future<void> calculateBonus(Employee employee, int hours, String email) async {
    // حساب المكافأة
    final hoursBonus = calculator.calculateHoursBonus(employee, hours);

    // طباعة التفاصيل
    printer.printEmployee(employee, hoursBonus);

    // تسجيل المكافأة
    await repository.logBonus(employee.id, calculator.getBonusType(), hoursBonus);

    // إرسال إشعار إذا كانت المكافأة أكبر من 0
    if (hoursBonus > 0) {
      await notificationService.sendBonusNotification(
        email,
        employee.name,
        hoursBonus,
        calculator.getBonusType(),
      );
    }
  }
}

void main() async {
  
  final repository = BonusRepository();
  final notificationService = NotificationService();

  // Manager Employee
  final employee1 = Employee(1, "Mohammed Anwar", 600);
  final manager1 = EmployeeManager(
    calculator: ManagerBonusCalculator(),
    repository: repository,
    notificationService: notificationService,
    printer: ConsoleEmployeePrinter(),
  );
  await manager1.calculateBonus(employee1, 5, 'mohammed@example.com');

  // Normal Employee
  final employee2 = Employee(2, "Ahmed Mohammed", 600);
  final manager2 = EmployeeManager(
    calculator: NormalBonusCalculator(),
    repository: repository,
    notificationService: notificationService,
    printer: JsonEmployeePrinter(),
  );
  await manager2.calculateBonus(employee2, 5, 'ahmed@example.com');

  // Senior Employee
  final employee3 = Employee(3, "Sara Ali", 750);
  final manager3 = EmployeeManager(
    calculator: SeniorBonusCalculator(),
    repository: repository,
    notificationService: notificationService,
    printer: FancyEmployeePrinter(),
  );
  await manager3.calculateBonus(employee3, 5, 'sara@example.com');

  // Intern Employee
  final employee4 = Employee(4, "Omar Salem", 200);
  final manager4 = EmployeeManager(
    calculator: InternBonusCalculator(),
    repository: repository,
    notificationService: notificationService,
    printer: ShortEmployeePrinter(),
  );
  await manager4.calculateBonus(employee4, 5, 'omar@example.com');

  // Part-Time Employee
  final employee5 = Employee(5, "Lina Hussein", 400);
  final manager5 = EmployeeManager(
    calculator: PartTimeBonusCalculator(),
    repository: repository,
    notificationService: notificationService,
    printer: TableEmployeePrinter(),
  );
  await manager5.calculateBonus(employee5, 5, 'lina@example.com');
}
```

##### **Output**

![images](https://raw.githubusercontent.com/MohammedAnwar2/SOILD-PRINCIPLES/main/OCP.png)

### **كيف يتبع الكود مبدأ الفتح/الإغلاق (OCP)؟**

مثل ما قلنا مبدأ OCP ينص على أن الكيانات البرمجية (مثل الكلاسات) يجب أن تكون **مفتوحة للتوسع** (يمكن إضافة سلوك جديد) و**مغلقة للتعديل** (لا حاجة لتغيير الكود الحالي).

---
#### **1. مفتوح للتوسع**
الكود مصمم بحيث يمكن إضافة سلوكيات جديدة (أنواع موظفين أو صيغ طباعة) دون الحاجة إلى تعديل الكلاسات الأساسية.

- **إضافة نوع موظف جديد**:
  - يمكن إنشاء كلاس جديد ينفذ الواجهة `BonusCalculator`، مثل `FreelancerBonusCalculator` بنسبة مكافأة 1.2، دون تغيير أي كود موجود.

- **إضافة صيغة طباعة جديدة**:
  - مستقبلا يمكن إنشاء كلاسات جديده تنفذ `EmployeePrinter`، مثل `XmlEmployeePrinter` أو `OfficePrinter` دون تعديل الكود الحالي.
  
- **المرونة في التوسع**:
  - الكود يدعم إضافة أنواع موظفين جديدة (مثل موظف مؤقت أو استشاري) وصيغ طباعة متنوعة (مثل طباعة إلى ملف، واجهة مستخدم، أو طابعة مكتبية) بسهولة.
  - هذا يجعل النظام مستدامًا وقابلًا للتكيف مع متطلبات مستقبلية.
----
#### **2. مغلق للتعديل**
الكلاسات الأساسية (`EmployeeManager`, `BonusRepository`, `NotificationService`) لا تحتاج إلى تعديل عند إضافة سلوكيات جديدة.

- **كلاس `EmployeeManager`**:
  - يعتمد على الواجهات (`BonusCalculator`, `EmployeePrinter`) بدلاً من تنفيذات محددة.
  - دالة `calculateBonus` تعمل مع أي كلاس ينفذ `BonusCalculator` أو `EmployeePrinter`، مما يجعلها مغلقة للتعديل.
  - على سبيل المثال، إضافة `FreelancerBonusCalculator` أو `JsonEmployeePrinter` لا تتطلب تغيير `EmployeeManager`.

- **كلاس `BonusRepository`**:
  - يعتمد على بيانات عامة (`employeeId`, `bonusType`, `amount`)، مما يجعله مستقلًا عن نوع الموظف أو المكافأة.
  - يمكن تسجيل أي نوع مكافأة جديد دون تعديل الكلاس.

- **كلاس `NotificationService`**:
  - يعتمد على بيانات عامة (`email`, `employeeName`, `amount`, `bonusType`)، مما يسمح بإرسال إشعارات لأي نوع مكافأة دون تغيير الكود.

- **الاستقرار**:
  - الكود الأصلي لا يتغير عند إضافة أنواع موظفين أو صيغ طباعة، مما يقلل من مخاطر الأخطاء ويحافظ على استقرار النظام.
----
#### **3. فصل المسؤوليات (تجنب انتهاك SRP)**
الكود يفصل المسؤوليات بوضوح، مما يدعم OCP ويجعل التوسع أسهل:
- **`BonusCalculator`**: مسؤول عن حساب المكافأة وتحديد نوعها.
- **`EmployeePrinter`**: مسؤول عن عرض التفاصيل بصيغ مختلفة.
- **`BonusRepository`**: مسؤول عن تسجيل المكافآت في قاعدة البيانات.
- **`NotificationService`**: مسؤول عن إرسال الإشعارات.
- **`EmployeeManager`**: مسؤول عن تنسيق العمليات (حساب، عرض، تسجيل، إشعار).

هذا الفصل يضمن أن كل مكون يمكن توسيعه بشكل مستقل دون التأثير على الآخرين.

---
#### **4. الفوائد**
- **التوسعية**: إضافة أنواع موظفين أو صيغ طباعة تتطلب فقط كلاسات جديدة تنفذ الواجهات المناسبة.
- **الاستقرار**: الكود الأصلي لا يتغير، مما يقلل من مخاطر الأخطاء.
- **سهولة الاختبار**: يمكن اختبار كل مكون على حدة (مثل `BonusCalculator` أو `EmployeePrinter`) باستخدام محاكاة (mocks).
- **إعادة الاستخدام**: المكونات (مثل `NotificationService`) يمكن استخدامها في سياقات أخرى.
- **المرونة**: الكود يدعم تنوعًا كبيرًا في صيغ الطباعة (نص، JSON، جدول، إلخ) وأنواع الموظفين.
- **منع التكرار**: فائدة عمل كلاس `BaseBonusCalculator` إزالة التكرار فالكود أصبح يتبع مبدأ DRY، مع وجود _calculateBaseBonus في مكان واحد 

عدم استخدام `BaseBonusCalculator` وتكرار `_calculateBaseBonus` في كل كلاس (`ManagerBonusCalculator`, `NormalBonusCalculator`, إلخ) يسبب المشاكل التالية:

1. **انتهاك مبدأ DRY ( Don't repeat yourself)**: تكرار المنطق `(employee.basicSalary / 30) * hours` في عدة كلاسات يجعل الكود غير نظيف، مما يزيد احتمالية الأخطاء عند نسخ/لصق الكود أو التعديل غير المتسق.

2. **صعوبة الصيانة**: أي تغيير في صيغة الحساب (مثل تغيير `30` إلى `28` لأيام العمل) يتطلب تعديل كل كلاس على حدة، مما يرفع مخاطر الأخطاء ويضيع الوقت.

3. **ضعف التماسك**: تكرار المنطق المشترك يشتت التصميم، حيث يصبح الكود أقل وضوحًا وأكثر عرضة للتناقضات (مثل استخدام صيغ مختلفة عن طريق الخطأ).

4. **انتهاك طفيف لـ OCP**: على الرغم من أن إضافة أنواع موظفين جديدة لا تتطلب تعديل الكلاسات الأساسية، فإن تعديل المنطق المشترك (مثل صيغة `_calculateBaseBonus`) يتطلب تغيير كل الكلاسات، مما يجعل الكود غير مغلق تمامًا لهذا النوع من التعديلات.

**الحل مع `BaseBonusCalculator`**: 
- يجمع المنطق المشترك في مكان واحد (`_calculateBaseBonus`)، مما يحقق مبدأ DRY.
- يسهل الصيانة بتعديل الصيغة في مكان واحد.
- يحافظ على OCP بجعل الكود مفتوحًا لإضافة أنواع موظفين جديدة (عبر وراثة `BaseBonusCalculator`) ومغلقًا لتعديل المنطق المشترك

----
### **ملاحظه مهمه جدا**
- يمكن استخدام دالة مساعدة (Helper Function) بدلاً من كلاس أساسي(BaseBonusCalculator)، يمكن استخراج _calculateBaseBonus إلى دالة مساعدة في كلاس مساعد أو ملف منفصل

```dart
class BonusUtils {
  static double calculateBaseBonus(Employee employee, int hours) {
    return (employee.basicSalary / 30) * hours;
  }
}
```

- ثم تعديل كلاس ManagerBonusCalculator (وغيره) لاستخدامها:
```dart
class ManagerBonusCalculator implements BonusCalculator {
  @override
  double calculateHoursBonus(Employee employee, int hours) {
    if (hours < 0) throw Exception('Hours cannot be negative');
    return BonusUtils.calculateBaseBonus(employee, hours) * 2;
  }

  @override
  String getBonusType() => 'Manager Bonus';
}
....
....
....
باقي الكلاسات
....
....
....
```

---

### **خلاصة مبدأ الفتح/الإغلاق (OCP)**

**التعريف**:  
OCP ينص على أن الكلاسات يجب أن تكون **مفتوحة للتوسع** (يمكن إضافة سلوك جديد) و**مغلقة للتعديل** (لا حاجة لتغيير الكود الحالي).

**كيف يتم تطبيقه في مشروعك**:
- **استخدام الواجهات(Interfaces)**: مثل `BonusCalculator` و`EmployeePrinter` لتحديد السلوك العام (حساب المكافأة، عرض البيانات).
- **نمط الاستراتيجية**: كل سلوك جديد (مثل `ManagerBonusCalculator` أو `TableEmployeePrinter`) يُضاف ككلاس منفصل ينفذ الواجهة.
- **حقن الاعتماديات**: تمرير الكلاسات (مثل `calculator` و`printer`) إلى `EmployeeManager` عبر المُنشئ، مما يقلل الاقتران.
- **معالجة التكرار**: استخراج المنطق المشترك (مثل `_calculateBaseBonus`) إلى كلاس أساسي (`BaseBonusCalculator`) لتجنب التكرار وتسهيل الصيانة.
- **فصل المسؤوليات**: كل كلاس يركز على مهمة واحدة (حساب، عرض، تسجيل، إشعارات) لتقليل التعديلات.

**علامات الانتهاك**:
- شروط `if-else` متكررة (مثل التحقق من نوع الموظف).
- تعديل الكلاسات الأساسية عند إضافة ميزات (مثل نوع موظف جديد).
- دمج المسؤوليات (كلاس يحسب ويطبع معًا).
- صعوبة الاختبار بسبب التعقيد.
- تكرار الكود (مثل صيغة حساب مكررة).

**فوائد التطبيق**:
- **مرونة**: إضافة أنواع موظفين (مثل `FreelancerBonusCalculator`) أو صيغ عرض (مثل `XmlEmployeePrinter`) تتم بكلاس جديد دون تعديل الكود.
- **استقرار**: الكلاسات الأساسية (مثل `EmployeeManager`) لا تتغير، مما يقلل الأخطاء.
- **صيانة أسهل**: تغيير المنطق المشترك (مثل صيغة الحساب في `BaseBonusCalculator`) يتم في مكان واحد.
- **اختبار أبسط**: يمكن اختبار كل مكون (مثل `TableEmployeePrinter`) بشكل مستقل.

**مثال عملي من مشروعك**:
- إضافة موظف جديد تتم بإنشاء كلاس مثل `FreelancerBonusCalculator` يرث من `BaseBonusCalculator`:
  
  ```dart
  class FreelancerBonusCalculator extends BaseBonusCalculator {
    @override
    String getBonusType() => 'Freelancer Bonus';
    @override
    double getBonusMultiplier() => 1.2;
  }
  ```
- تحسين عرض الجدول في `TableEmployeePrinter` جعل التنسيق أجمل مع الحفاظ على OCP.

**الخلاصة**:  
OCP يضمن أن يكون كودك مرنًا ومستدامًا من خلال التجريد (واجهات، كلاسات أساسية)، فصل المسؤوليات، ومعالجة التكرار، مما يسمح بإضافة ميزات جديدة دون تغيير الكود الأساسي، كما رأينا في تصميم نظام المكافآت الخاص بك.
