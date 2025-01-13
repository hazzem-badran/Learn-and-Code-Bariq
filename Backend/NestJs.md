
dbngin
table plus

تنزيل nest على الجهاز  
npm install  -g @nestjs/cli

nest new nest-project

الملفات اللي بتبدى app بنسميها بنست مديل module 

app.controller.spec.ts  
-هاد الملف خاص بالتستنق
app.controller.ts 


-هاد عبارة عن الكنترولر وبعرف بداخلو الرواتس routs
-وأيش الفنكشن اللي هتشتغل بناءً على زيارة هاد الرراوت او end point
فمن هاد بنستقبل الركوست وبترجع الرسبونس اللي بدك ترجعو

app.module.ts


```
@Module({
    imports: [],
    controllers: [AppController],
    providers: [AppService],
})
```

-الموديل هاد زي الانترفيس تبع  app 
-وبتعرفلي بداخلها ايش همة controllers واللي هوة المكان اللي بنعرف فيه ال end point تبعتك
-ال Module هوة عبارة عن جزئية من جزئيات المشروع
ال providers وهية عبارة عن ال Services اللي بتحتوي بداخلها المنطق 

في **NestJS**، ملف **`app.module.ts`** هو نقطة البداية الأساسية لتطبيقك. وهو بمثابة الملف الرئيسي الذي يجمع المكونات (Modules) والخدمات (Services) والمسارات (Controllers) في تطبيقك.

### **ما هو Module في NestJS؟**

- **الموديل (Module)** هو عبارة عن حاوية تُستخدم لتنظيم الكود الخاص بك في وحدات منطقية.
- ملف **`app.module.ts`** هو الموديل الجذري (Root Module) لتطبيقك، ومن خلاله يتم تحميل باقي الموديلات.



`@Module` 
هو **ديكور (Decorator)** يُستخدم لتعريف وحدة (Module) في تطبيق NestJS. الوحدة هي الأساس الذي يُقسم به التطبيق إلى أجزاء مُنظمة.

### **المكونات الأربعة في المثال:**

1. **`imports: []`:**
    
    - يُستخدم لاستيراد الوحدات الأخرى التي يحتاجها هذا الموديل.
    - مثال: إذا كنت تحتاج إلى خدمات أو ميزات من وحدة أخرى.
2. **`controllers: []`:**
    
    - تُحدد الـ Controllers التي تحتوي على نقاط الوصول (Endpoints) الخاصة بهذا الموديل.
3. **`providers: []`:**
    
    - تحتوي على الخدمات (Services) أو أي مزودات يتم تعريفها في هذا الموديل.
4. **`exports: []`:**
    
    - تُحدد ما يمكن تصديره من هذا الموديل للوحدات الأخرى.

### **وظيفته:**

يساعد هذا التصميم في فصل المنطق الخاص بالتطبيق إلى وحدات مستقلة يسهل تطويرها وصيانتها.


main.ts
-هاد الملف الأساس اللي رح يشتغل منو المشروع 

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
  
async function bootstrap() {
	const app = await NestFactory.create(AppModule);
	
	await app.listen(process.env.PORT ?? 3000);
}
bootstrap();
```


ال @ ومن ثمة كلمة ثم قوسين بنقال عنها Decorator
@Controller()
Decorator that marks a class as a Nest controller that can receive inbound requests and produce responses.

الـ **Decorator** في NestJS هو مجرد وظيفة (Function) تُستخدم لإضافة ميزات أو تعديل سلوك شيء في الكود، مثل **كلاس** أو **دالة** أو **باراميتر**.

### **كيف يعمل؟**

- يُكتب الـ Decorator دائمًا فوق العنصر الذي تريد تعديل سلوكه.
- يبدأ بعلامة `@`.
- يضيف أو يغير طريقة عمل العنصر.

### **أنواع الـ Decorators الشائعة في NestJS:**
 **@Controller()**
- يُستخدم لتحديد أن الكلاس هو "Controller" يتعامل مع الطلبات (Requests)
- مثال:
`@Controller('users') // يحدد أن هذا الكلاس يتعامل مع مسار '/users' export class UsersController {}`

 **@Get() / @Post() / @Put() / @Delete()**
- تُستخدم لتحديد نوع الطلب (HTTP Method) والمسار المرتبط به.
 مثال:
`@Get('profile') // يربط هذه الدالة بمسار GET '/profile' getProfile() {   return 'User Profile'; }`

**@Injectable()**

- تُستخدم مع الكلاسات التي تقدم خدمات (Services).
- تجعل الكلاس قابلاً للحقن (Dependency Injection).
- مثال:
```
@Injectable()
export class UserService {  
getUser() {    
	return { name: 'John Doe' };  
	} 
}
```

**@Param()**
-تُستخدم لجلب القيم من متغيرات المسار (Route Parameters).
 مثال:   
``@Get(':id') getUserById(@Param('id') id: string) {   return `User ID is ${id}`; }``


**@Body()** 
-تُستخدم لجلب البيانات المرسلة في جسم الطلب (Request Body).
 مثال:
`@Post() createUser(@Body() userData: any) {   return userData; }`

### **لماذا نستخدم الـ Decorators؟**

- لجعل الكود **أكثر ترتيبًا ووضوحًا**.
- لتوفير الوقت والجهد بدلًا من كتابة أكواد متكررة.
- لأنها تجعل الكود يتبع مبدأ "التنظيم بالأدوار" (Separation of Concerns).


### **تخيل الـ Decorator مثل طبقة فوق العنصر**

- هو مثل أنك تضيف ملصقًا أو وظيفة إضافية للعنصر.
- على سبيل المثال: إذا قلت لصديقك أن "هذه القهوة فيها سكر"، فـ @Body() هو السكر الذي يضيف المعلومة للقهوة (الطلب).

```
@Controller()
export class AppController {
	constructor(private readonly appService: AppService) {}
	
	@Get()
	getHello(): string {
		return this.appService.getHello();
	}
	
	@Get('/hazem')
	getHazem(): string {
		return this.appService.getHazem();
	}
	
	@Post(`/hazem`)
	setHazem(@Body('name') name : string ){
		return this.appService.sayHi(name);
	}
}
```


ال appService عرفنااها بداخل ال constructor  ولاحظ أنها من نوع AppService  ونها هين بخدها آز برامتر فنكشن وبالاحرى رح يتم استدعائها  لما أعمل object  من كلاس AppController


تم تعريفها بهذا الشكل  
```
constructor(private readonly appService: AppService) {}
```
لأنها بتعمد على مفهوم Dependency Injection (DI)

المهم هاد السيرفس رح اعرفها كبرامتر وحط نوعها هاي السيرفر AppService و nest js رح يفهم لحالو انو لازم يعملك object    من AppService في وقت run time 


ال  Dependency Injection (DI) تابع تحت اطار او مفهوم Inversion of Control


**الـ Dependency Injection (DI)** هو مفهوم في البرمجة يساعد في جعل الكود أكثر مرونة، قابلية للاختبار، وصيانة. باختصار، هو وسيلة لإعطاء **الكلاسات** أو **المكونات** التي تحتاج إلى شيء (مثل خدمة أو كلاس آخر) هذا الشيء، بدلاً من أن تقوم هي بإنشائه بنفسها.

### **الفكرة الأساسية:**
بدلاً من أن يقوم الكود بإنشاء الكائنات أو الخدمات داخل الكلاس نفسه، يتم "حقن" هذه الخدمات أو الكائنات من الخارج.

### **مثال بسيط بدون DI:**
تخيل أنه عندك كلاس `UserService` الذي يحتاج إلى `DatabaseService`:


```
class DatabaseService {
  connect() {
    console.log("Connected to the database");
  }
}

class UserService {
  private dbService = new DatabaseService(); // هنا يتم إنشاء الخدمة داخل الكلاس
  
  getUsers() {
    this.dbService.connect();
    console.log("Fetching users...");
  }
}

```

هنا، `UserService` هو الذي يقوم بإنشاء `DatabaseService` بنفسه. هذا يعني أن `UserService` صار مرتبطًا ارتباطًا قويًا بـ `DatabaseService`، مما يجعل من الصعب تغييره أو اختباره.

---

### **لكن مع Dependency Injection:**

باستخدام الـ DI، نقوم "بحقن" `DatabaseService` في `UserService` بدلاً من أن يقوم هو بإنشائه بنفسه.


```
class DatabaseService {
  connect() {
    console.log("Connected to the database");
  }
}

class UserService {
  constructor(private dbService: DatabaseService) {} // حقن الـ DatabaseService في الـ Constructor
  
  getUsers() {
    this.dbService.connect();
    console.log("Fetching users...");
  }
}

```

الآن، `UserService` ليس بحاجة لإنشاء `DatabaseService` بنفسه. سيتم "حقن" الكائن `DatabaseService` من الخارج (غالبًا من الـ DI Container في NestJS أو إطار العمل الذي تستخدمه).

---

### **كيف يعمل DI في NestJS؟*

في NestJS، يمكننا استخدام **DI Container** الذي يعتني بحقن الخدمات تلقائيًا. يتم ذلك باستخدام **الـ Decorators** مثل `@Injectable()` و `@Inject()`.

#### 1. **تعريف خدمة (Service)**

```
@Injectable()  // تحديد الخدمة باستخدام ديكوراتور
export class DatabaseService {
  connect() {
    console.log("Connected to the database");
  }
}
```

#### 2. **حقن الخدمة في Controller أو Service آخر**

```
@Controller('users')
export class UserController {
  constructor(private dbService: DatabaseService) {}  
  // DI يحدث هنا، حيث يتم حقن DatabaseService تلقائيًا
  
  @Get()
  getUsers() {
    this.dbService.connect();
    return "Fetching users...";
  }
}
```

في المثال أعلاه:

- ا**`DatabaseService`** يتم حقنها تلقائيًا داخل **`UserController`** عبر **الـ Constructor**.
- ا NestJS يقوم بإنشاء `DatabaseService` وتوفيرها في `UserController` دون الحاجة لإنشائها يدويًا.



### **لماذا نستخدم الـ Dependency Injection؟**

1. **قابلية الاختبار (Testability)**:
    - إذا كنت تستخدم DI، يمكنك حقن خدمات وهمية (Mocks) أو خدمات بديلة بسهولة في الاختبارات، مما يسهل اختبار الكود.
2. **فصل المسؤوليات (Separation of Concerns)**:
    - الكلاس لا يحتاج لإنشاء الكائنات بنفسه، بل يترك ذلك للـ DI Container.
3. **قابلية التوسعة (Scalability)**:
    - يمكن إضافة خدمات جديدة أو تغيير الخدمات الحالية بسهولة دون التأثير على باقي أجزاء الكود.
4. **إعادة الاستخدام (Reusability)**:
    - يمكن إعادة استخدام الكلاسات أو الخدمات بسهولة في أجزاء أخرى من التطبيق.


### **باختصار**:

الـ **Dependency Injection** هو طريقة لتوفير الكائنات (مثل الخدمات) إلى الكلاسات بدلاً من أن تقوم الكلاسات بإنشائها بنفسها. هذه الطريقة تجعل الكود أكثر مرونة، قابلية للاختبار، وأسهل في الصيانة.

---
----


**"إنفيرجن كنترول" (Inversion of Control)**، وهو مبدأ أساسي في تصميم البرمجيات، خصوصًا في إطار العمل مثل **NestJS** أو **Spring** في Java.
يهدف هذا المبدأ إلى **عكس تدفق التحكم** في البرنامج بحيث لا تتحكم الكائنات في إنشاء الأشياء التي تعتمد عليها، بل يتم "حقن" هذه الأشياء أو الاعتماديات (Dependencies) من الخارج.

### **مفهوم Inversion of Control (IoC)**

عندما تكون لديك **كلاس** يحتاج إلى **خدمات أخرى** (مثل قاعدة بيانات، خدمة خارجية، إلخ)، في الطريقة التقليدية (قبل تطبيق **IoC**)، سيكون الكلاس هو المسؤول عن إنشاء هذه الخدمات بنفسه. أما في **IoC**، فإن الكلاس لا يقوم بإنشاء هذه الخدمات، بل يتم **حقن** هذه الخدمات في الكلاس من **خارج الكلاس** بواسطة **إطار العمل** (مثل NestJS).

### **الفائدة من Inversion of Control:**

1. **تقليل التبعيات**: لا يصبح الكلاس معتمدًا على الخدمات التي يحتاجها، بل يعتمد على "حقن" هذه الخدمات من الخارج.
2. **تحسين قابلية الاختبار**: بما أن الكلاسات لا تنشئ الاعتماديات بنفسها، يمكنك حقن خدمات وهمية (Mocks) أثناء الاختبار.
3. **مرونة أكبر**: يمكنك تغيير أو استبدال الخدمات بسهولة.

### **كيف يعمل IoC في NestJS؟**

في **NestJS**، **IoC** يتم تطبيقه من خلال **الـ Dependency Injection (DI)**، حيث يقوم إطار العمل بإدارة حياة الكائنات، وحقنها في الأماكن المطلوبة.

### **كيف NestJS يحقق هذا؟**

- **`@Injectable()`**: 
- يستخدم هذا الديكوريتور لعلامة الكلاسات التي يجب أن يديرها NestJS.
- **DI Container**:
- يقوم NestJS تلقائيًا بإنشاء الكائنات اللازمة، ويقوم بحقنها في الكلاسات التي تحتاج إليها عبر **الـ Constructor**.

### **ملخص:**

- **Inversion of Control (IoC)** 
- هو مبدأ يعكس كيفية إنشاء الكائنات ويحول المسؤولية عن هذه العملية إلى إطار العمل أو البيئة التي تعمل فيها.
- في **NestJS**، يتم تطبيق **IoC** عبر **Dependency Injection (DI)**، مما يسمح لك بحقن الخدمات في الكلاسات بدلاً من أن تقوم الكلاسات بإنشائها بنفسها.


بحث  
-  ال**IoC** ليس فقط **Dependency Injection**، بل يشمل طرقًا أخرى مثل:
    - **Event-driven Programming**
    - **Template Method**
    - **Service Locator**
    - **Strategy Pattern**
    - **AOP**
    - **Observer Pattern**
 كل طريقة لها استخدامات مختلفة حسب الحاجة والتطبيق.


---


الأمر `nest g controller booking` هو اختصار في **NestJS** لإنشاء **Controller** جديد باستخدام الـ CLI الخاص بـ NestJS.

### **تفصيل الأمر:**

- **`nest`**: هي أداة الـ CLI الخاصة بـ NestJS.
- **`g`**: اختصار لـ **generate**، وهي تستخدم لإنشاء ملفات أو مكونات جديدة.
- **`controller`**: نوع العنصر الذي تريد إنشاؤه (في هذه الحالة، هو **Controller**).
- **`booking`**: اسم الـ Controller الذي تريد إنشاؤه.


في **NestJS**، الكلمة المفتاحية **`g`** هي اختصار للأمر **`generate`** الذي يستخدم لإنشاء مختلف المكونات الأساسية في المشروع. أداة **CLI** الخاصة بـ **NestJS** توفر طريقة فعّالة وسريعة لإنشاء هذه المكونات مع الهيكلة الافتراضية الموصى بها.

### **ما هو الأمر `nest g`؟**

الأمر `nest g` يُستخدم لتوليد المكونات الأساسية في مشروع **NestJS**. يمكنك إنشاء:

- **Controllers**: لإدارة طلبات الـ HTTP.
- **Services**: لكتابة منطق الأعمال والتعامل مع البيانات.
- **Modules**: لتنظيم الكود في وحدات مستقلة.
- **Providers**: لتوفير الخدمات أو القيم القابلة للحقن (Dependency Injection).
- **Middlewares**: لمعالجة الطلبات قبل وصولها إلى الـ Controllers.
- **Filters**: لمعالجة الأخطاء.
- **Guards**: لحماية المسارات باستخدام صلاحيات معينة.
- **Pipes**: لتحويل البيانات والتحقق منها.
- **Interceptors**: للتعامل مع الطلبات والاستجابات.
- **Gateways**: لدعم الـ WebSockets.


### **الصيغة العامة للأمر:**


`nest g <type> <name>`

- **`type`**: نوع العنصر المراد إنشاؤه (مثل: `controller`, `service`, `module`, إلخ).
- **`name`**: اسم العنصر الذي ترغب في إنشائه.


### **أمثلة على الاستخدام:**

1. **إنشاء Controller:**
`nest g controller user`
	يقوم بإنشاء ملف `user.controller.ts` للتعامل مع طلبات HTTP الخاصة بمسار المستخدمين.

2. **إنشاء Service:**
`nest g service user`
	يقوم بإنشاء ملف `user.service.ts` لكتابة منطق الأعمال.

3. **إنشاء Module:**
    `nest g module user`
    يقوم بإنشاء ملف `user.module.ts` لإدارة مكونات المستخدمين.
    
4. **إنشاء Middleware:**
    
    `nest g middleware logger`
    يقوم بإنشاء Middleware لمعالجة الطلبات.
    
5. **إنشاء Guard:**
    
    `nest g guard auth`
    يقوم بإنشاء ملف Guard للتأكد من صلاحيات الوصول.

6. **إنشاء Pipe:**

    `nest g pipe validation`

    يقوم بإنشاء Pipe للتحقق من البيانات أو تعديلها.


### **خيارات إضافية:**

يمكنك استخدام خيارات إضافية مع الأمر `nest g` لتخصيص الإنشاء:

- **`--flat`**: إنشاء الملفات دون وضعها داخل مجلد جديد.
- **`--spec`**: تحديد ما إذا كنت تريد إنشاء ملف الاختبارات (افتراضيًا يتم إنشاؤه).
- **`--module`**: إضافة العنصر الجديد مباشرةً إلى موديول معين.

#### مثال:

`nest g service auth --module app`

- ينشئ **Service** باسم `auth` ويضيفه تلقائيًا إلى **AppModule**.

---



---
---
---

nest g resource  payment
هيك انشألي module جديد بحبشكناتو من الألف للألف 



في **NestJS**، مفهوم **DTO (Data Transfer Object)** يُستخدم لنقل البيانات بين الطبقات المختلفة داخل التطبيق، مثل إرسال البيانات من العميل إلى الخادم أو بين الخدمات المختلفة.

### **ما هو DTO؟**

- **اختصارًا لـ Data Transfer Object**، وهو كائن يحتوي على البيانات التي يتم نقلها.
- يساعد في تحديد **هيكل البيانات** المتوقع في الطلبات والاستجابات.
- يُستخدم لتجنب تمرير كائنات ضخمة أو غير ضرورية ولضمان أن البيانات المرسلة صحيحة ومنسقة.
### **استخدام DTO في NestJS**

1. **تعريف DTO:**
    - يتم تعريف DTO كفئة (Class) في NestJS، وتُستخدم مع مكتبة **class-validator** للتحقق من صحة البيانات المرسلة من العميل.
    - يتم استخدام مكتبة **class-transformer** لتحويل الكائنات إلى الفئات المحددة.

```
import { IsString, IsEmail, IsNotEmpty } from 'class-validator';

export class CreateUserDto {
    @IsString()
    @IsNotEmpty()
    readonly name: string;

    @IsEmail()
    readonly email: string;

    @IsString()
    readonly password: string;
}

```

- - هنا، قمنا بتعريف DTO لإنشاء مستخدم جديد.
    - استخدمنا **Decorators** مثل `@IsString` و `@IsEmail` للتحقق من نوع وصحة البيانات.
- **استخدام DTO داخل Controller:**
    
    - يتم استخدام DTO لتحليل والتحقق من البيانات المرسلة في الطلب.
    
    **مثال:**
```
import { Body, Controller, Post } from '@nestjs/common';
import { CreateUserDto } from './create-user.dto';

@Controller('users')
export class UsersController {
    @Post()
    createUser(@Body() createUserDto: CreateUserDto) {
        console.log(createUserDto);
        return 'User created successfully';
    }
}
```

- - هنا، عند إرسال طلب POST لإنشاء مستخدم، يتم تحليل البيانات باستخدام `CreateUserDto`.
- **دمج مع ValidationPipe:**
    
    - لتفعيل التحقق من صحة البيانات تلقائيًا، يمكنك استخدام **ValidationPipe**.
    
    **مثال:**

```
import { ValidationPipe } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    app.useGlobalPipes(new ValidationPipe());
    await app.listen(3000);
}
bootstrap();

```
### **مزايا استخدام DTO:**

1. **تحقق من صحة البيانات:** يضمن أن البيانات المستلمة صحيحة وتلبي القواعد المحددة.
2. **تسهيل الصيانة:** يمكنك تحديد الهيكل المتوقع للبيانات بشكل واضح ومنفصل.
3. **تحسين الأمان:** يمنع تمرير بيانات غير مرغوب فيها أو خطيرة.
4. **إعادة الاستخدام:** يمكن استخدام DTO في أماكن متعددة داخل التطبيق.




## References

1. [NestJS Official Documentation](https://docs.nestjs.com/)
2. [YouTube Video - NestJS Overview](https://youtu.be/RwOxUg2rsjY?si=NYdkEr764ir0-xjS)
3. Assistance with research provided by ChatGPT.
