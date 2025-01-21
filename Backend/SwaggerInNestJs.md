ا**Swagger** (الذي يُعرف الآن باسم **OpenAPI**) هو إطار عمل يُستخدم لتوثيق واجهات برمجة التطبيقات (APIs). يسمح لك بتوضيح كيفية عمل الـ API الخاصة بك، بما في ذلك طرق الوصول (endpoints)، أنواع البيانات المدخلة والمخرجة، وأكواد الاستجابة المحتملة.

### **ما هو Swagger؟**

اSwagger هو مجموعة من الأدوات التي توفر لك طريقة لتوثيق API الخاصة بك بحيث يمكن للمطورين الآخرين فهم كيفية استخدامها، وتجربتها بسهولة. يتيح لك Swagger:

- **توثيق API**: وصف كل نقطة نهاية (endpoint) في الـ API، مع تحديد الأساليب المدعومة مثل `GET` و `POST` وغيرها.
- **توليد التوثيق التفاعلي**: إنشاء واجهة مستخدم تفاعلية (UI) تسمح للمطورين باختبار الـ API مباشرة من المتصفح.
- **توليد الأكواد**: يمكن لـ Swagger توليد أكواد عملاء (clients) و/أو خوادم (servers) بلغات مختلفة بناءً على التوثيق.

### **المكونات الرئيسية لـ Swagger:**

1. ا **Swagger UI**: واجهة رسومية تتيح لك استعراض وتجربة الـ API.
2. ا **Swagger Editor**: أداة لتعديل وتوثيق API باستخدام لغة تعريف الـ OpenAPI.
3. 
3.ا **Swagger Codegen**: أداة لتوليد الشيفرة البرمجية من الـ Swagger JSON أو YAML.

### **مزايا استخدام Swagger:**

- **التوثيق التفاعلي**: يتيح للمطورين تجربة الـ API مباشرة من المتصفح.
- **تحسين التعاون**: يساعد الفرق في التعاون بشكل أفضل من خلال توحيد وثائق الـ API.
- **توليد الأكواد**: يساعد في تقليل العمل اليدوي بتوليد أكواد الـ client أو الـ server.

### **كيف يمكن إضافة Swagger إلى مشروع يستخدم `NestJS`؟**


لإضافة **Swagger** إلى مشروع يستخدم **NestJS**، يمكنك اتباع الخطوات التالية:

### 1. **تثبيت الحزم اللازمة**

أولاً، تحتاج إلى تثبيت الحزمة الخاصة بـ **NestJS Swagger**:

```
npm install @nestjs/swagger swagger-ui-express
```
### 2. **تفعيل Swagger في مشروعك**

بعد تثبيت الحزم، يجب عليك إعداد **Swagger** داخل مشروع **NestJS**. يمكنك فعل ذلك في **ملف `main.ts`** الخاص بمشروعك.

هنا هو الكود المطلوب لإعداد Swagger:

```
import { NestFactory } from '@nestjs/core';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // إعداد Swagger
  const config = new DocumentBuilder()
    .setTitle('NestJS API')
    .setDescription('The API description')
    .setVersion('1.0')
    .addTag('users')  // إضافة التصنيفات (tags)
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api', app, document);  // فتح Swagger UI عند '/api'

  await app.listen(3000);
}
bootstrap();

```
### 3. **توصيف API باستخدام `@nestjs/swagger`**

يمكنك الآن استخدام **الديكورات (Decorators)** الخاصة بـ **`@nestjs/swagger`** لتوثيق الـ **controllers** و **DTOs**. إليك بعض الأمثلة الأساسية لتوضيح كيفية استخدامها:

الديكوراتور `@ApiTags()` في NestJS هو جزء من الحزمة `@nestjs/swagger` ويُستخدم لتحديد مجموعة من الـ endpoints في API وثائق الـ Swagger. عند استخدام `@ApiTags()`, تقوم بتحديد تسمية أو فئة للـ API الذي يتم توثيقه، مما يسهل تنظيم الـ endpoints في واجهة Swagger.

### كيف يعمل `@ApiTags()`؟

يُستخدم هذا الديكوراتور في **التحكمات (Controllers)** لتحديد الفئة التي ينتمي إليها هذا الـ controller أو الموديل عند عرض الـ API في واجهة Swagger. يساعد ذلك في تقسيم التوثيق إلى أقسام تسهل فهمه.

```
import { Controller, Get } from '@nestjs/common';
import { ApiTags } from '@nestjs/swagger';

@ApiTags('users')  // إضافة تصنيف للـ Controller
@Controller('users')
export class UsersController {
  @Get()
  getUsers() {
    return 'This action returns all users';
  }
}

```
#### **استخدام `@ApiOperation` لوصف الـ Endpoints**

```
import { Controller, Get } from '@nestjs/common';
import { ApiOperation, ApiResponse } from '@nestjs/swagger';

@Controller('users')
export class UsersController {
  @Get()
  @ApiOperation({ summary: 'Get all users' })  // إضافة ملخص للـ Operation
  @ApiResponse({ status: 200, description: 'Return all users' })  // وصف الاستجابة
  getUsers() {
    return 'This action returns all users';
  }
}

```
#### **استخدام `@ApiProperty` لتوثيق الـ DTOs**

لتوثيق البيانات التي ستُرسل أو تُستقبل عبر API، يمكنك استخدام **`@ApiProperty`** داخل الـ DTOs:

```
import { ApiProperty } from '@nestjs/swagger';

export class CreateUserDto {
  @ApiProperty({ description: 'The name of the user' })
  name: string;

  @ApiProperty({ description: 'The email of the user' })
  email: string;
}

```

### 4. **زيارة واجهة Swagger UI**

بعد إعداد Swagger، يمكنك زيارة واجهة **Swagger UI** عبر الرابط التالي في المتصفح:

`http://localhost:3000/api`

ستظهر لك واجهة المستخدم التي توضح جميع الـ Endpoints التي قمت بتوثيقها، مع معلومات عن الاستجابات، الأخطاء الممكنة، وكذلك أنواع البيانات المطلوبة.

### 5. **ملاحظات إضافية:**

- **تخصيص Swagger**: يمكنك تخصيص Swagger عبر إضافة خصائص إضافية مثل **`addBearerAuth()`** لإضافة توثيق للمصادقة باستخدام التوكن، أو تحديد **`tags`** و **`externalDocs`** لربط مستندات خارجية.
- **إخفاء بعض الـ Endpoints**: في حال أردت إخفاء بعض الـ Endpoints عن واجهة Swagger، يمكنك استخدام **`@ApiExcludeEndpoint()`**.


## References

1. [NestJS Official Documentation](https://docs.nestjs.com/)

2. [YouTube Video - NestJS Overview](https://youtu.be/DG0uZ0E8DBs?si=bvquHDYwiLeNbJcy)
3. Assistance with research provided by ChatGPT.
