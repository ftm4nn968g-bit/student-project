
🔐 Қауіпсіз қосымшаны тіркелу/кіру жүйесі және Қауіпсіздік модульдері

Бұл жоба — қолданушыларды тіркеу, жүйеге кіру және деректерді қорғауға арналған қауіпсіздік жүйесі. Жоба аясында JWT аутентификациясы, TLS шифрлау, файлдардың тұтастығын бақылау (FIM) және сигнатуралық сканерлеу сияқты қауіпсіздік шаралары іске асырылған.

🎯 Мақсаты

Жобаның басты мақсаты — веб-қосымша үшін сенімді және қауіпсіз аутентификация жүйесін құру, рұқсатсыз кірудің алдын алу, деректер алмасуды шифрлау және жүйелік файлдардың өзгеріске ұшырауын анықтау.

🛠 Қолданылған технологиялар

· Backend: Java, Spring Boot, Spring Security
· Дерекқор: PostgreSQL (немесе H2)
· Аутентификация: JWT (JSON Web Tokens)
· Қауіпсіздік: BCrypt (пароль хэштеу), KeyStore/SSLContext (TLS)
· Қосымша құралдар: WatchService (File Integrity Monitor), SQLite (FIM үшін)



🚀 Орнату (Installation)

Жобаны жергілікті компьютерде іске қосу үшін келесі қадамдарды орындаңыз:

1. Репозиторийді клондаңыз:
   ```bash
   git clone https://github.com/your-username/your-repository-name.git
   cd your-repository-name
   ```
2. Дерекқорды баптаңыз (PostgreSQL орнатылған болуы керек). application.properties файлында дерекқорға кіру параметрлерін өзгертіңіз:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/your_db_name
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   ```
3. Жобаны жинақтап, іске қосыңыз (Maven немесе Gradle арқылы):
   ```bash
   # Maven үшін
   ./mvnw spring-boot:run
   # Немесе Gradle үшін
   ./gradlew bootRun
   ```
4. Қосымша http://localhost:8080 мекенжайында қолжетімді болады.

---

💻 Қолдану мысалы (Usage Example)

1. Жаңа қолданушыны тіркеу:

```http
POST /api/auth/register
Content-Type: application/json

{
  "username": "testuser",
  "password": "StrongPassword123"
}
```

2. Жүйеге кіру және JWT токен алу:

```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "testuser",
  "password": "StrongPassword123"
}
```

Жауап (Response):

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ..."
}
```

3. Қорғалған API-ге сұраныс жіберу:

```http
GET /api/user/profile
Authorization: Bearer <жоғарыда_алынған_JWT_токен>
```

---

🛡 Қауіпсіздік ерекшеліктері (Security Features)

Жоба кестесіндегі талаптарға сәйкес келесі қауіпсіздік шаралары енгізілді:

· Қауіпсіз тіркелу/кіру жүйесі: Парольдер ашық түрде сақталмайды, олар BCrypt (немесе Argon2) алгоритмімен хэштеледі.
· JWT Аутентификация: REST API сұраныстарын қорғау үшін JWT токендері қолданылады. Токеннің өмір сүру уақыты шектелген.
· TLS-чат: Қосымша ішіндегі байланыс арналары KeyStore және SSLContext арқылы шифрланады (TLS/SSL сертификаттары).
· File Integrity Monitor (FIM): Жүйелік файлдардың өзгеруін бақылау үшін WatchService қолданылады. Файлдың хэші (бақылау сомасы) өзгерсе, жүйе ескерту береді және өзгерістерді SQLite дерекқорына жазады.
· Сигнатуралық сканер: Белгілі қауіпті кодтарды (мысалы, EICAR тест файлы) байт-деңгейінде іздеу және анықтау жүзеге асырылған.

---

📸 Скриншоттар (Screenshots)

(Мұнда өз жобаңыздың скриншоттарын қоюыңыз керек! Мысалы: Postman-дағы сәтті сұраныс, дерекқордағы кесте, немесе FIM-нің ескерту терезесі)

1. Postman арқылы JWT токен алу:
ссылка_на_вашу_картинку_1.png

2. Дерекқордағы қолданушылар кестесі (пароль хэштелген):
ссылка_на_вашу_картинку_2.png

3. File Integrity Monitor ескертуі:
ссылка_на_вашу_картинку_3.png

---

🧪 Тестілеу (Testing)

Жобада негізгі логиканы тексеру үшін JUnit арқылы жазылған 10-нан астам юнит және интеграциялық тесттер бар. Тесттерді іске қосу үшін:

```bash
./mvnw test
```

---

Ескерту: Жобадағы құпия деректер (парольдер, API кілттері, SSL кілттері) .gitignore файлы арқылы жасырылған және репозиторийге жүктелмейді. Конфигурациялар application.properties немесе ортаның айнымалы мәндері (environment variables) арқылы беріледі.



