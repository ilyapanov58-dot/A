Пример для валидации без готового кода
    Прмиер может быть использован на всех версиях KOTLI и должен рабоать

ПРИМЕР БЕЗ КОДА И НЕОБХОДИМЫ ИМПОРТЫ

``` kotlin
ИМПОРТЫ
import android.content.Intent
import android.widget.Toast
import androidx.compose.foundation.clickable


КОД ДЛЯ КНОПКИ
Button(
    onClick = {
        // сюда вставляется код
    }
)

ВАЛИДАЦИЯ
onClick = {
    // Я добавил проверку логина на пустое поле
    if (login.isBlank()) {
        Toast.makeText(this@SignUp, "Заполните поле Логин", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку длины логина
    else if (login.length < 8) {
        Toast.makeText(this@SignUp, "Логин должен быть не менее 8 символов", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку email на пустое поле
    else if (email.isBlank()) {
        Toast.makeText(this@SignUp, "Заполните поле Email", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку длины email
    else if (email.length < 12) {
        Toast.makeText(this@SignUp, "Email должен быть не менее 12 символов", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку чтобы email содержал знак @
    else if (!email.contains("@")) {
        Toast.makeText(this@SignUp, "Email должен содержать символ @", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку пароля на пустое поле
    else if (password.isBlank()) {
        Toast.makeText(this@SignUp, "Заполните поле Пароль", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку длины пароля
    else if (password.length < 8) {
        Toast.makeText(this@SignUp, "Пароль должен быть не менее 8 символов", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку чтобы пароль состоял только из цифр
    else if (!password.all { it.isDigit() }) {
        Toast.makeText(this@SignUp, "Пароль должен состоять только из цифр", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку поля повторения пароля
    else if (confirmPassword.isBlank()) {
        Toast.makeText(this@SignUp, "Повторите пароль", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку совпадения паролей
    else if (password != confirmPassword) {
        Toast.makeText(this@SignUp, "Пароли не совпадают", Toast.LENGTH_SHORT).show()
    }

    // Я добавил переход на экран входа и передал туда email и пароль
    else {
        val intent = Intent(this@SignUp, LoginIn::class.java)
        intent.putExtra("email", email)
        intent.putExtra("password", password)
        startActivity(intent)
    }
}

ЕСЛИ ДАТА РОЖДЕНИЯ
else if (data.value.isBlank()) {
    Toast.makeText(this@SignUp, "Выберите дату рождения", Toast.LENGTH_SHORT).show()
}
ЕСЛИ DATEOFBIRTHDAY
else if (dateOfBirth.isBlank()) {
    Toast.makeText(this@SignUp, "Выберите дату рождения", Toast.LENGTH_SHORT).show()
}

ЕСЛИ ЕСТЬ CHECK BOX
else if (!isPrivacyPolicyChecked) {
    Toast.makeText(this@SignUp, "Необходимо согласиться с условиями", Toast.LENGTH_SHORT).show()
}

ПЕРЕХОД ПО ССЫЛКЕ
modifier = Modifier.clickable {
    val intent = Intent(this@SignUp, LoginIn::class.java)
    startActivity(intent)
}


ПРИМЕР ПЕРЕХОДА
Text(
    text = "Вход",
    fontSize = 12.sp,
    color = Color(0xFF4D81E7),
    fontWeight = FontWeight.Bold,
    textAlign = TextAlign.Center,
    modifier = Modifier
        .padding(start = 6.dp, top = 24.dp)
        .clickable {
            val intent = Intent(this@SignUp, LoginIn::class.java)
            startActivity(intent)
        }
)

```
Так-же второй вариант валадиции по аналогичному примеру
```Поменять класс на 
class LoginIn : ComponentActivity() {

Получить E и P
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    enableEdgeToEdge()

    val savedEmail = intent.getStringExtra("email") ?: ""
    val savedPassword = intent.getStringExtra("password") ?: ""

    setContent {
        LoginScreen(savedEmail, savedPassword)
    }
}

getStringExtra("email") — получает email с экрана регистрации
getStringExtra("password") — получает пароль с экрана регистрации
?: "" — если данных нет, подставляется пустая строка

Внутри LoginScreen создать переменные
var email by remember { mutableStateOf(savedEmail) }
var password by remember { mutableStateOf(savedPassword) }
var passwordVisible by remember { mutableStateOf(false) }


ПРОВЕРКИ ВАЛИДАЦИИ
onClick = {
    // Я добавил проверку email на пустое поле
    if (email.isBlank()) {
        Toast.makeText(this@LoginIn, "Заполните поле Email", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку чтобы email содержал знак @
    else if (!email.contains("@")) {
        Toast.makeText(this@LoginIn, "Email должен содержать символ @", Toast.LENGTH_SHORT).show()
    }

    // Я добавил проверку пароля на пустое поле
    else if (password.isBlank()) {
        Toast.makeText(this@LoginIn, "Заполните поле Пароль", Toast.LENGTH_SHORT).show()
    }

    // Я вывожу сообщение если вход выполнен успешно
    else {
        Toast.makeText(this@LoginIn, "Вход выполнен успешно", Toast.LENGTH_SHORT).show()
    }
}


ПЕРЕХОД ПО КНОПКИ
modifier = Modifier.clickable {
    val intent = Intent(this@LoginIn, SignUp::class.java)
    startActivity(intent)
}

ПРИМЕР
Text(
    text = "Регистрация",
    fontSize = 12.sp,
    color = Color(0xFF4D81E7),
    fontWeight = FontWeight.Bold,
    textAlign = TextAlign.Center,
    modifier = Modifier
        .padding(start = 6.dp)
        .clickable {
            val intent = Intent(this@LoginIn, SignUp::class.java)
            startActivity(intent)
        }
)


ОБЯЗАТЕЛЬНАЯ AndroidManifest.xml

Внутри <application> нужно добавить экран LoginIn:

<activity
    android:name=".LoginIn"
    android:exported="false" />

А SignUp должен быть стартовым экраном:

<activity
    android:name=".SignUp"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>

Полный пример:

<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.SignUpLoginInv5">

        <activity
            android:name=".LoginIn"
            android:exported="false" />

        <activity
            android:name=".SignUp"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>

</manifest> kotlin
```
ТАК ЖЕ МОЖНО ИСПОЛЬЗОВАТЬ ГОТОВЫЙ КОД ПО ПРИМЕРУ, КОТОРЫЙ МОЖНО БУДЕТ МОДЕРНИЗИРОВАТЬ ПОД СВОЕ ПРИЛОЖЕНИИЕ

