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
``` Kotlin
Поменять класс на 
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

Встроенные механизмы защиты: Использование функций require() и check(), которые мгновенно выбрасывают исключения при нарушении инвариантов, предотвращая работу системы с заведомо «испорченными» объектами.

Сила Data-классов и init-блоков: Инкапсуляция логики проверки прямо в конструкторах данных, что гарантирует существование только валидных экземпляров бизнес-сущностей в любой момент времени.

Функциональный подход (Arrow-kt и аналоги): Смещение парадигмы в сторону контейнеров Either или Validated, что позволяет не просто прерывать выполнение программы ошибкой, а элегантно накапливать все нарушения и возвращать их пользователю в удобном формате.

Декларативные фреймворки: Интеграция с мощными экосистемами (например, Konform, Valiktor или стандартными JSR-380 аннотациями в Spring Boot), позволяющая описывать правила валидации как понятный, расширяемый и легко поддерживаемый DSL-код.

ПРИМЕРЫ 1 ВАРИНТ 

``` Kotlin
package com.example.profileeditprofilev1

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Check
import androidx.compose.material.icons.filled.Clear
import androidx.compose.material3.Button
import androidx.compose.material3.ButtonDefaults
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.LocalTextStyle
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.OutlinedTextField
import androidx.compose.material3.OutlinedTextFieldDefaults
import androidx.compose.material3.Text
import androidx.compose.material3.TopAppBar
import androidx.compose.material3.TopAppBarDefaults
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import java.text.SimpleDateFormat
import java.util.Calendar
import java.util.Locale

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            MaterialTheme { ProfileScreen() }
        }
    }

    @Preview(showSystemUi = true)
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun ProfileScreen() {
        var isEditing by remember { mutableStateOf(false) }

        // Добавил переменные для хранения данных профиля
        var firstName by remember { mutableStateOf("Emmanuel") }
        var lastName by remember { mutableStateOf("Oyiboke") }
        var email by remember { mutableStateOf("primer@gmail.com") }
        var address by remember { mutableStateOf("Nigeria") }
        var birthDate by remember { mutableStateOf("28.03.2003") }

        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(Color.White)
        ) {
            // Верхняя панель
            TopAppBar(
                title = {
                    Text(
                        // Изменил заголовок в зависимости от режима
                        text = if (isEditing) "Edit Profile" else "Профиль",
                        fontSize = 16.sp,
                        color = Color(0xFF2B2B2B),
                        textAlign = TextAlign.Center,
                        modifier = Modifier.fillMaxWidth()
                    )
                },
                actions = {
                    IconButton(
                        onClick = {
                            // Изменил кнопку карандаша чтобы она включала режим редактирования
                            isEditing = true
                        }
                    ) {
                        Image(
                            painter = painterResource(id = R.drawable.edit),
                            contentDescription = "Редактировать",
                            modifier = Modifier.size(25.dp)
                        )
                    }
                },
                colors = TopAppBarDefaults.topAppBarColors(
                    containerColor = Color.White,
                    titleContentColor = Color.Black,
                    navigationIconContentColor = Color.Black,
                    actionIconContentColor = Color.Black
                ),
                modifier = Modifier
                    .fillMaxWidth()
                    .background(Color.White)
                    .padding(horizontal = 22.dp)
            )

            Spacer(modifier = Modifier.height(40.dp))

            Column(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(horizontal = 24.dp),
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                // Аватар пользователя
                Box(
                    modifier = Modifier
                        .size(96.dp)
                        .clip(CircleShape)
                ) {
                    Image(
                        painter = painterResource(id = R.drawable.emmanuel),
                        contentDescription = "Фото профиля",
                        modifier = Modifier.fillMaxSize()
                    )
                }

                Spacer(modifier = Modifier.height(8.dp))

                // Изменил подпись чтобы она бралась из имени и фамилии
                Text(
                    text = "$firstName $lastName",
                    fontSize = 20.sp,
                    color = Color.Black
                )

                Spacer(modifier = Modifier.height(48.dp))

                // Имя
                ProfileInfoRow(
                    label = "Имя",
                    value = firstName,
                    isEditing = isEditing,
                    onValueChange = { firstName = it },
                    isValid = firstName.isNotBlank() && firstName.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Фамилия
                ProfileInfoRow(
                    label = "Фамилия",
                    value = lastName,
                    isEditing = isEditing,
                    onValueChange = { lastName = it },
                    isValid = lastName.isNotBlank() && lastName.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Email
                ProfileInfoRow(
                    label = "Email",
                    value = email,
                    isEditing = isEditing,
                    onValueChange = { email = it },
                    isValid = email.isNotBlank() && email.length >= 12 && email.contains("@"),
                    keyboardType = KeyboardType.Email
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Адрес
                ProfileInfoRow(
                    label = "Адрес",
                    value = address,
                    isEditing = isEditing,
                    onValueChange = { address = it },
                    isValid = address.isNotBlank() && address.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Дата рождения
                ProfileInfoRow(
                    label = "Дата рождения",
                    value = birthDate,
                    isEditing = isEditing,
                    onValueChange = { birthDate = it },
                    isValid = isValidBirthDate(birthDate),
                    keyboardType = KeyboardType.Number
                )

                // Добавил кнопку сохранения только в режиме редактирования
                if (isEditing) {
                    Spacer(modifier = Modifier.height(24.dp))

                    Button(
                        onClick = {
                            // Добавил проверку имени
                            if (firstName.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Имя", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины имени
                            else if (firstName.length < 20) {
                                Toast.makeText(this@MainActivity, "Имя должно быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку фамилии
                            else if (lastName.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Фамилия", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины фамилии
                            else if (lastName.length < 20) {
                                Toast.makeText(this@MainActivity, "Фамилия должна быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку email
                            else if (email.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Email", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины email
                            else if (email.length < 12) {
                                Toast.makeText(this@MainActivity, "Email должен быть не менее 12 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку знака @
                            else if (!email.contains("@")) {
                                Toast.makeText(this@MainActivity, "Email должен содержать символ @", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку адреса
                            else if (address.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Адрес", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины адреса
                            else if (address.length < 20) {
                                Toast.makeText(this@MainActivity, "Адрес должен быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку даты рождения
                            else if (birthDate.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Дата рождения", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку формата даты и возраста
                            else if (!isValidBirthDate(birthDate)) {
                                Toast.makeText(this@MainActivity, "Дата должна быть в формате dd.MM.yyyy возраст от 14 до 99 лет", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил сохранение и возврат к просмотру профиля
                            else {
                                Toast.makeText(this@MainActivity, "Данные сохранены", Toast.LENGTH_SHORT).show()
                                isEditing = false
                            }
                        },
                        modifier = Modifier
                            .fillMaxWidth()
                            .height(52.dp),
                        shape = RoundedCornerShape(14.dp),
                        colors = ButtonDefaults.buttonColors(
                            containerColor = Color(0xFF4DB6E8)
                        )
                    ) {
                        Text(
                            text = "Сохранить",
                            fontSize = 16.sp,
                            color = Color.White
                        )
                    }
                }
            }
        }
    }

    @Composable
    fun ProfileInfoRow(
        label: String,
        value: String,
        isEditing: Boolean,

        // Добавил обработку изменения текста
        onValueChange: (String) -> Unit,

        // Добавил проверку правильности поля
        isValid: Boolean,

        // Добавил тип клавиатуры
        keyboardType: KeyboardType = KeyboardType.Text
    ) {
        Column(
            modifier = Modifier.fillMaxWidth()
        ) {
            Text(
                text = label,
                fontSize = 16.sp,
                color = Color(0xFF2B2B2B),
                modifier = Modifier.padding(bottom = 4.dp)
            )

            OutlinedTextField(
                value = value,

                // Изменил доступность поля
                enabled = isEditing,

                // Изменил обработку ввода
                onValueChange = onValueChange,

                modifier = Modifier.fillMaxWidth(),
                placeholder = { Text(value) },
                shape = RoundedCornerShape(14.dp),

                // Добавил тип клавиатуры
                keyboardOptions = KeyboardOptions(
                    keyboardType = keyboardType
                ),

                // Добавил галочку или крестик справа
                trailingIcon = {
                    if (isEditing) {
                        Icon(
                            imageVector =
                                if (isValid) Icons.Default.Check
                                else Icons.Default.Clear,
                            contentDescription = null,
                            tint =
                                if (isValid) Color(0xFF4DB6E8)
                                else Color.Red
                        )
                    }
                },

                colors = OutlinedTextFieldDefaults.colors(
                    focusedBorderColor = Color(0xFFF7F7F9),
                    unfocusedBorderColor = Color(0xFFF7F7F9),
                    disabledBorderColor = Color(0xFFF7F7F9),
                    unfocusedContainerColor = Color(0xFFF7F7F9),
                    focusedContainerColor = Color(0xFFF7F7F9),
                    disabledContainerColor = Color(0xFFF7F7F9),
                    disabledTextColor = Color(0xFF6A6A6A)
                ),
                textStyle = LocalTextStyle.current.copy(
                    fontSize = 14.sp,
                    color =
                        if (isEditing) Color.Black
                        else Color(0xFF6A6A6A)
                )
            )
        }
    }

    // Добавил проверку даты рождения
    fun isValidBirthDate(date: String): Boolean {
        return try {
            val dateFormat = SimpleDateFormat("dd.MM.yyyy", Locale.getDefault())
            dateFormat.isLenient = false

            val parsedDate = dateFormat.parse(date) ?: return false

            val birthCalendar = Calendar.getInstance()
            birthCalendar.time = parsedDate

            val today = Calendar.getInstance()

            var age = today.get(Calendar.YEAR) - birthCalendar.get(Calendar.YEAR)

            if (today.get(Calendar.DAY_OF_YEAR) < birthCalendar.get(Calendar.DAY_OF_YEAR)) {
                age--
            }

            age in 14..99
        } catch (e: Exception) {
            false
        }
    }
}
```
Важное архитектурное замечание: Выбор конкретного инструмента всегда зависит от контекста. Для простых DTO (Data Transfer Objects) на входе в контроллер отлично подходят аннотации или DSL-валидаторы, в то время как глубоко внутри доменной модели лучше полагаться на строгие правила init-блоков, гарантирующие иммутабельность и корректность бизнес-сущностей на протяжении всего их жизненного цикла.


Об обработке ошибок: Исключения против функционального подхода
Архитектурный компромисс (Exceptions vs Functional): Выбрасывание исключений (например, IllegalArgumentException через require) — это отличный fail-fast механизм для внутренней логики приложения, где некорректные данные означают ошибку программиста. Однако на внешних слоях (API, пользовательский ввод) генерация Exception на каждое неверно заполненное поле — это антипаттерн, бьющий по производительности. В этих сценариях гораздо эффективнее использовать монадические структуры (например, Either из библиотеки Arrow или кастомные sealed-классы), которые превращают ошибки валидации в контролируемые данные, а не в аварийную остановку потока.


ПРИМЕР ВАРИАНТА 2

```Kotlin
package com.example.profileeditprofilev2

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Check
import androidx.compose.material.icons.filled.Clear
import androidx.compose.material.icons.filled.DateRange
import androidx.compose.material.icons.filled.Edit
import androidx.compose.material.icons.filled.Email
import androidx.compose.material.icons.filled.Person
import androidx.compose.material.icons.filled.Place
import androidx.compose.material3.Button
import androidx.compose.material3.ButtonDefaults
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.LocalTextStyle
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.OutlinedTextField
import androidx.compose.material3.OutlinedTextFieldDefaults
import androidx.compose.material3.Text
import androidx.compose.material3.TopAppBar
import androidx.compose.material3.TopAppBarDefaults
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.graphics.vector.ImageVector
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import java.text.SimpleDateFormat
import java.util.Calendar
import java.util.Locale

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            MaterialTheme { ProfileScreen() }
        }
    }

    @Preview(showSystemUi = true)
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun ProfileScreen() {
        var isEditing by remember { mutableStateOf(false) }

        // Добавил переменные данных профиля
        var firstName by remember { mutableStateOf("Emmanuel") }
        var lastName by remember { mutableStateOf("Oyiboke") }
        var email by remember { mutableStateOf("primer@gmail.com") }
        var address by remember { mutableStateOf("Nigeria") }
        var birthDate by remember { mutableStateOf("28.03.2003") }

        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(Color.White)
        ) {
            //Верхняя панель
            TopAppBar(
                title = {
                    Text(
                        text = "Профиль",
                        fontSize = 24.sp,
                        color = Color(0xFF2B2B2B),
                        fontWeight = FontWeight.Bold,
                        textAlign = TextAlign.Center,
                        modifier = Modifier.fillMaxWidth()
                    )
                },
                actions = {
                    IconButton(
                        onClick = {
                            // Изменил кнопку редактирования
                            isEditing = true
                        },
                        modifier = Modifier
                            .clip(RoundedCornerShape(19.dp))
                            .background(Color(0xFF8EDDFF))
                            .size(25.dp)
                    ) {
                        Icon(
                            Icons.Default.Edit,
                            contentDescription = "Редактировать",
                            modifier = Modifier.size(12.dp)
                        )
                    }
                },
                colors = TopAppBarDefaults.topAppBarColors(
                    containerColor = Color.White,
                    titleContentColor = Color.Black,
                    navigationIconContentColor = Color.Black,
                    actionIconContentColor = Color.Black
                ),
                modifier = Modifier
                    .fillMaxWidth()
                    .background(Color.White)
                    .padding(horizontal = 22.dp)
            )

            Spacer(modifier = Modifier.height(10.dp))

            Column(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(horizontal = 24.dp),
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                //Аватар пользователя
                Box(
                    modifier = Modifier
                        .size(96.dp)
                        .clip(CircleShape)
                ) {
                    Image(
                        painter = painterResource(id = R.drawable.emmanuel),
                        contentDescription = "Фото профиля",
                        modifier = Modifier.fillMaxSize()
                    )
                }

                Spacer(modifier = Modifier.height(8.dp))

                // Изменил подпись под фото
                Text(
                    text = "$firstName $lastName",
                    fontSize = 20.sp,
                    color = Color.Black
                )

                Spacer(modifier = Modifier.height(50.dp))

                // Имя
                ProfileInfoRow(
                    label = "Имя",
                    value = firstName,
                    isEditing = isEditing,
                    icon = Icons.Default.Person,
                    onValueChange = { firstName = it },
                    isValid = firstName.isNotBlank() && firstName.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Фамилия
                ProfileInfoRow(
                    label = "Фамилия",
                    value = lastName,
                    isEditing = isEditing,
                    icon = Icons.Default.Person,
                    onValueChange = { lastName = it },
                    isValid = lastName.isNotBlank() && lastName.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Email
                ProfileInfoRow(
                    label = "Email",
                    value = email,
                    isEditing = isEditing,
                    icon = Icons.Default.Email,
                    onValueChange = { email = it },
                    isValid = email.isNotBlank() && email.length >= 12 && email.contains("@"),
                    keyboardType = KeyboardType.Email
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Адрес
                ProfileInfoRow(
                    label = "Адрес",
                    value = address,
                    isEditing = isEditing,
                    icon = Icons.Default.Place,
                    onValueChange = { address = it },
                    isValid = address.isNotBlank() && address.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Дата рождения
                ProfileInfoRow(
                    label = "Дата рождения",
                    value = birthDate,
                    isEditing = isEditing,
                    icon = Icons.Default.DateRange,
                    onValueChange = { birthDate = it },
                    isValid = isValidBirthDate(birthDate),
                    keyboardType = KeyboardType.Number
                )

                // Добавил кнопку сохранения
                if (isEditing) {
                    Spacer(modifier = Modifier.height(24.dp))

                    Button(
                        onClick = {
                            // Добавил проверку имени
                            if (firstName.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Имя", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины имени
                            else if (firstName.length < 20) {
                                Toast.makeText(this@MainActivity, "Имя должно быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку фамилии
                            else if (lastName.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Фамилия", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины фамилии
                            else if (lastName.length < 20) {
                                Toast.makeText(this@MainActivity, "Фамилия должна быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку email
                            else if (email.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Email", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины email
                            else if (email.length < 12) {
                                Toast.makeText(this@MainActivity, "Email должен быть не менее 12 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку знака @
                            else if (!email.contains("@")) {
                                Toast.makeText(this@MainActivity, "Email должен содержать символ @", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку адреса
                            else if (address.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Адрес", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины адреса
                            else if (address.length < 20) {
                                Toast.makeText(this@MainActivity, "Адрес должен быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку даты рождения
                            else if (birthDate.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Дата рождения", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку формата даты и возраста
                            else if (!isValidBirthDate(birthDate)) {
                                Toast.makeText(this@MainActivity, "Дата должна быть в формате dd.MM.yyyy возраст от 14 до 99 лет", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил сохранение данных
                            else {
                                Toast.makeText(this@MainActivity, "Данные сохранены", Toast.LENGTH_SHORT).show()
                                isEditing = false
                            }
                        },
                        modifier = Modifier
                            .fillMaxWidth()
                            .height(52.dp),
                        shape = RoundedCornerShape(14.dp),
                        colors = ButtonDefaults.buttonColors(
                            containerColor = Color(0xFF8EDDFF)
                        )
                    ) {
                        Text(
                            text = "Сохранить",
                            fontSize = 16.sp,
                            fontWeight = FontWeight.Bold,
                            color = Color.White
                        )
                    }
                }
            }
        }
    }

    @Composable
    fun ProfileInfoRow(
        label: String,
        value: String,
        isEditing: Boolean,
        icon: ImageVector,

        // Добавил изменение текста
        onValueChange: (String) -> Unit,

        // Добавил проверку поля
        isValid: Boolean,

        // Добавил тип клавиатуры
        keyboardType: KeyboardType = KeyboardType.Text
    ) {
        Column(
            modifier = Modifier.fillMaxWidth()
        ) {
            Text(
                text = label,
                fontSize = 16.sp,
                color = Color(0xFF20AEEB),
                modifier = Modifier.padding(bottom = 4.dp)
            )

            OutlinedTextField(
                value = value,

                // Изменил доступность поля
                enabled = isEditing,

                // Изменил обработку изменения
                onValueChange = onValueChange,

                modifier = Modifier.fillMaxWidth(),
                leadingIcon = {
                    Icon(
                        imageVector = icon,
                        contentDescription = null,
                        tint = Color(0xFF515151)
                    )
                },

                // Добавил галочку или крестик справа
                trailingIcon = {
                    if (isEditing) {
                        Icon(
                            imageVector =
                                if (isValid) Icons.Default.Check
                                else Icons.Default.Clear,
                            contentDescription = null,
                            tint =
                                if (isValid) Color(0xFF20AEEB)
                                else Color.Red
                        )
                    }
                },
                placeholder = { Text(value) },
                shape = RoundedCornerShape(14.dp),

                // Добавил клавиатуру
                keyboardOptions = KeyboardOptions(
                    keyboardType = keyboardType
                ),

                colors = OutlinedTextFieldDefaults.colors(
                    focusedBorderColor = Color(0xFFF2F2F2),
                    unfocusedBorderColor = Color(0xFFF2F2F2),
                    disabledBorderColor = Color(0xFFF2F2F2),
                    unfocusedContainerColor = Color(0xFFF2F2F2),
                    focusedContainerColor = Color(0xFFF2F2F2),
                    disabledContainerColor = Color(0xFFF2F2F2),
                    disabledTextColor = Color(0xFF515151)
                ),
                textStyle = LocalTextStyle.current.copy(
                    fontSize = 14.sp,
                    color = Color(0xFF515151)
                )
            )
        }
    }

    // Добавил проверку даты рождения
    fun isValidBirthDate(date: String): Boolean {
        return try {
            val dateFormat = SimpleDateFormat("dd.MM.yyyy", Locale.getDefault())
            dateFormat.isLenient = false

            val parsedDate = dateFormat.parse(date) ?: return false

            val birthCalendar = Calendar.getInstance()
            birthCalendar.time = parsedDate

            val today = Calendar.getInstance()

            var age = today.get(Calendar.YEAR) - birthCalendar.get(Calendar.YEAR)

            if (today.get(Calendar.DAY_OF_YEAR) < birthCalendar.get(Calendar.DAY_OF_YEAR)) {
                age--
            }

            age in 14..99
        } catch (e: Exception) {
            false
        }
    }
}
```

О разделении ответственности (Separation of Concerns)
Замечание о чистоте домена: Существует соблазн навесить аннотации валидации (вроде @NotNull или @Size) прямо на доменные сущности базы данных. Однако это связывает бизнес-логику с конкретным фреймворком. Настоятельно рекомендуется разделять слои: внешние DTO принимают на себя удар «грязных» данных и проверяются синтаксически (формат email, длина строки), в то время как доменные модели оперируют уже семантической валидацией (проверка бизнес-правил, баланса, прав доступа), оставаясь полностью независимыми от внешних библиотек.

О комплексной валидации (Single-field vs Multi-field)
Нюанс контекстной валидации: Валидацию можно разделить на атомарную (проверка одного поля) и композитную (зависимость полей друг от друга). Если с проверкой формата телефона легко справляются регулярные выражения на уровне DTO, то валидация условий вида «поле Б обязательно, только если поле А имеет значение Х» требует выноса логики в отдельные сервисы-валидаторы или использования возможностей Kotlin DSL. Попытка уместить сложную кросс-полевую логику в стандартные аннотации часто приводит к созданию нечитаемого и хрупкого кода.

О подходе "Parse, don't validate" (Парси, а не валидируй)
Философский аспект (Type-Driven Design): Современный тренд в Kotlin-разработке смещается от классической валидации к концепции «Parse, don't validate». Вместо того чтобы хранить строку и постоянно проверять, является ли она валидным email-адресом, лучше один раз провалидировать её на входе и упаковать в специализированный тип (Value Class) — например, class Email(val value: String). Таким образом, сам факт наличия этого типа в аргументах функции на уровне компиляции гарантирует, что данные уже прошли проверку, избавляя от необходимости дублировать if-условия на каждом шагу.


ПРИМЕР ВАРИАНТА 3

``` Kotlin
package com.example.profileeditprofilev3

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Check
import androidx.compose.material.icons.filled.Clear
import androidx.compose.material.icons.filled.DateRange
import androidx.compose.material.icons.filled.Edit
import androidx.compose.material.icons.filled.Email
import androidx.compose.material.icons.filled.Person
import androidx.compose.material.icons.filled.Place
import androidx.compose.material3.Button
import androidx.compose.material3.ButtonDefaults
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.LocalTextStyle
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.OutlinedTextField
import androidx.compose.material3.OutlinedTextFieldDefaults
import androidx.compose.material3.Text
import androidx.compose.material3.TopAppBar
import androidx.compose.material3.TopAppBarDefaults
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.graphics.vector.ImageVector
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import java.text.SimpleDateFormat
import java.util.Calendar
import java.util.Locale

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            MaterialTheme { ProfileScreen() }
        }
    }

    @Preview(showSystemUi = true)
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun ProfileScreen() {
        var isEditing by remember { mutableStateOf(false) }

        // Добавил переменные для хранения данных профиля
        var firstName by remember { mutableStateOf("Emmanuel") }
        var lastName by remember { mutableStateOf("Oyiboke") }
        var email by remember { mutableStateOf("primer@gmail.com") }
        var address by remember { mutableStateOf("Nigeria") }
        var birthDate by remember { mutableStateOf("28.03.2003") }

        Column(
            modifier = Modifier
                .fillMaxSize()
                .background(Color.White)
        ) {
            // Верхняя панель
            TopAppBar(
                title = {
                    Text(
                        text = "Профиль",
                        fontSize = 24.sp,
                        color = Color(0xFF2B2B2B),
                        fontWeight = FontWeight.Bold,
                        textAlign = TextAlign.Center,
                        modifier = Modifier.fillMaxWidth()
                    )
                },
                actions = {
                    IconButton(
                        onClick = {
                            // Изменил кнопку карандаша чтобы включался режим редактирования
                            isEditing = true
                        },
                        modifier = Modifier
                            .clip(RoundedCornerShape(19.dp))
                            .background(Color(0xFF8EDDFF))
                            .size(25.dp)
                    ) {
                        Icon(
                            Icons.Default.Edit,
                            contentDescription = "Редактировать",
                            modifier = Modifier.size(12.dp)
                        )
                    }
                },
                colors = TopAppBarDefaults.topAppBarColors(
                    containerColor = Color.White,
                    titleContentColor = Color.Black,
                    navigationIconContentColor = Color.Black,
                    actionIconContentColor = Color.Black
                ),
                modifier = Modifier
                    .fillMaxWidth()
                    .background(Color.White)
                    .padding(horizontal = 22.dp)
            )

            Spacer(modifier = Modifier.height(10.dp))

            Column(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(horizontal = 24.dp),
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                // Аватар пользователя
                Box(
                    modifier = Modifier
                        .size(96.dp)
                        .clip(CircleShape)
                ) {
                    Image(
                        painter = painterResource(id = R.drawable.emmanuel),
                        contentDescription = "Фото профиля",
                        modifier = Modifier.fillMaxSize()
                    )
                }

                Spacer(modifier = Modifier.height(8.dp))

                // Изменил подпись чтобы она автоматически бралась из имени и фамилии
                Text(
                    text = "$firstName $lastName",
                    fontSize = 20.sp,
                    color = Color.Black
                )

                Spacer(modifier = Modifier.height(50.dp))

                // Имя
                ProfileInfoRow(
                    label = "Имя",
                    value = firstName,
                    isEditing = isEditing,
                    icon = Icons.Default.Person,
                    onValueChange = { firstName = it },
                    isValid = firstName.isNotBlank() && firstName.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Фамилия
                ProfileInfoRow(
                    label = "Фамилия",
                    value = lastName,
                    isEditing = isEditing,
                    icon = Icons.Default.Person,
                    onValueChange = { lastName = it },
                    isValid = lastName.isNotBlank() && lastName.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Email
                ProfileInfoRow(
                    label = "Email",
                    value = email,
                    isEditing = isEditing,
                    icon = Icons.Default.Email,
                    onValueChange = { email = it },
                    isValid = email.isNotBlank() && email.length >= 12 && email.contains("@"),
                    keyboardType = KeyboardType.Email
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Адрес
                ProfileInfoRow(
                    label = "Адрес",
                    value = address,
                    isEditing = isEditing,
                    icon = Icons.Default.Place,
                    onValueChange = { address = it },
                    isValid = address.isNotBlank() && address.length >= 20
                )

                Spacer(modifier = Modifier.height(12.dp))

                // Дата рождения
                ProfileInfoRow(
                    label = "Дата рождения",
                    value = birthDate,
                    isEditing = isEditing,
                    icon = Icons.Default.DateRange,
                    onValueChange = { birthDate = it },
                    isValid = isValidBirthDate(birthDate),
                    keyboardType = KeyboardType.Number
                )

                // Добавил кнопку сохранения только в режиме редактирования
                if (isEditing) {
                    Spacer(modifier = Modifier.height(24.dp))

                    Button(
                        onClick = {
                            // Добавил проверку имени
                            if (firstName.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Имя", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины имени
                            else if (firstName.length < 20) {
                                Toast.makeText(this@MainActivity, "Имя должно быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку фамилии
                            else if (lastName.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Фамилия", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины фамилии
                            else if (lastName.length < 20) {
                                Toast.makeText(this@MainActivity, "Фамилия должна быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку email
                            else if (email.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Email", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины email
                            else if (email.length < 12) {
                                Toast.makeText(this@MainActivity, "Email должен быть не менее 12 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку знака @
                            else if (!email.contains("@")) {
                                Toast.makeText(this@MainActivity, "Email должен содержать символ @", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку адреса
                            else if (address.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Адрес", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку длины адреса
                            else if (address.length < 20) {
                                Toast.makeText(this@MainActivity, "Адрес должен быть не менее 20 символов", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку даты рождения
                            else if (birthDate.isBlank()) {
                                Toast.makeText(this@MainActivity, "Заполните поле Дата рождения", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил проверку формата даты и возраста
                            else if (!isValidBirthDate(birthDate)) {
                                Toast.makeText(this@MainActivity, "Дата должна быть в формате dd.MM.yyyy возраст от 14 до 99 лет", Toast.LENGTH_SHORT).show()
                            }

                            // Добавил сохранение и возврат к просмотру профиля
                            else {
                                Toast.makeText(this@MainActivity, "Данные сохранены", Toast.LENGTH_SHORT).show()
                                isEditing = false
                            }
                        },
                        modifier = Modifier
                            .fillMaxWidth()
                            .height(52.dp),
                        shape = RoundedCornerShape(14.dp),
                        colors = ButtonDefaults.buttonColors(
                            containerColor = Color(0xFF8EDDFF)
                        )
                    ) {
                        Text(
                            text = "Сохранить",
                            fontSize = 16.sp,
                            fontWeight = FontWeight.Bold,
                            color = Color.White
                        )
                    }
                }
            }
        }
    }

    @Composable
    fun ProfileInfoRow(
        label: String,
        value: String,
        isEditing: Boolean,
        icon: ImageVector,

        // Добавил обработку изменения текста
        onValueChange: (String) -> Unit,

        // Добавил проверку правильности поля
        isValid: Boolean,

        // Добавил тип клавиатуры
        keyboardType: KeyboardType = KeyboardType.Text
    ) {
        Column(
            modifier = Modifier.fillMaxWidth()
        ) {
            Text(
                text = label,
                fontSize = 16.sp,
                color = Color(0xFF20AEEB),
                modifier = Modifier.padding(bottom = 4.dp)
            )

            OutlinedTextField(
                value = value,

                // Изменил доступность поля
                enabled = isEditing,

                // Изменил обработку ввода
                onValueChange = onValueChange,

                modifier = Modifier.fillMaxWidth(),

                leadingIcon = {
                    Icon(
                        imageVector = icon,
                        contentDescription = null,
                        tint = Color(0xFF515151)
                    )
                },

                // Добавил галочку или крестик справа
                trailingIcon = {
                    if (isEditing) {
                        Icon(
                            imageVector =
                                if (isValid) Icons.Default.Check
                                else Icons.Default.Clear,
                            contentDescription = null,
                            tint =
                                if (isValid) Color(0xFF20AEEB)
                                else Color.Red
                        )
                    }
                },

                placeholder = { Text(value) },
                shape = RoundedCornerShape(14.dp),

                // Добавил тип клавиатуры
                keyboardOptions = KeyboardOptions(
                    keyboardType = keyboardType
                ),

                colors = OutlinedTextFieldDefaults.colors(
                    focusedBorderColor = Color(0xFFF2F2F2),
                    unfocusedBorderColor = Color(0xFFF2F2F2),
                    disabledBorderColor = Color(0xFFF2F2F2),
                    unfocusedContainerColor = Color(0xFFF2F2F2),
                    focusedContainerColor = Color(0xFFF2F2F2),
                    disabledContainerColor = Color(0xFFF2F2F2),
                    disabledTextColor = Color(0xFF515151)
                ),
                textStyle = LocalTextStyle.current.copy(
                    fontSize = 14.sp,
                    color = Color(0xFF515151)
                )
            )
        }
    }

    // Добавил проверку даты рождения
    fun isValidBirthDate(date: String): Boolean {
        return try {
            val dateFormat = SimpleDateFormat("dd.MM.yyyy", Locale.getDefault())
            dateFormat.isLenient = false

            val parsedDate = dateFormat.parse(date) ?: return false

            val birthCalendar = Calendar.getInstance()
            birthCalendar.time = parsedDate

            val today = Calendar.getInstance()

            var age = today.get(Calendar.YEAR) - birthCalendar.get(Calendar.YEAR)

            if (today.get(Calendar.DAY_OF_YEAR) < birthCalendar.get(Calendar.DAY_OF_YEAR)) {
                age--
            }

            age in 14..99
        } catch (e: Exception) {
            false
        }
    }
}

```

В конечном счете, архитектурно правильный подход к валидации в Kotlin заключается в соблюдении баланса и разделении обязанностей. Как было продемонстрировано, не существует «серебряной пули»: синтаксическая проверка на уровне DTO защищает периметр приложения, строгие ограничения в init-блоках гарантируют целостность доменных моделей, а концепция «Parse, don't validate» переносит часть проверок на уровень компилятора, используя всю мощь статической типизации Kotlin.

Инвестирование времени в проектирование гибкого слоя валидации окупается снижением количества багов и легкостью масштабирования системы. Разработчик, эффективно использующий идиомы Kotlin, получает возможность создавать программные продукты, которые не просто «работают», но и сопротивляются энтропии в процессе долгосрочной поддержки.
