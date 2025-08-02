---
metaTitle: Настройка и использование input и textinput в React Native
metaDescription: Подробная инструкция по настройке и использованию input и textinput в React Native - синтаксис, управление состоянием, обработка событий и стилизация
author: Олег Марков
title: Настройка и использование input и textinput в React Native
preview: Освойте работу с input и textinput в React Native - настройка, примеры использования, обработка событий и лучшие практики для вашего мобильного приложения
---

## Введение

React Native стал де-факто стандартом для кроссплатформенной мобильной разработки с использованием JavaScript и React. Одна из ключевых задач любого мобильного приложения — взаимодействие пользователя с интерфейсом, особенно через ввод данных. Для этой цели в React Native используется компонент `TextInput`, который выступает аналогом HTML-элемента `<input>`, но со своими особенностями. 

В этой статье я подробно расскажу о том, как правильно настраивать и использовать `TextInput` в React Native, разберем управление состоянием, обработку событий, стилизацию, работу с клавиатурой, маскировку ввода пароля и другие нюансы. Приведем практические примеры и обсудим расширенные возможности, которые помогут вам гибко интегрировать поля ввода в ваше мобильное приложение.

## Компонент TextInput в React Native: базовые сведения

В React Native для работы с текстовыми полями предусмотрен специализированный компонент `TextInput`. С его помощью пользователь может ввести текст, числа, пароли и другую информацию.

### Основной синтаксис

Вот самый простой пример использования:

```jsx
import React from 'react'
import { TextInput, View } from 'react-native'

export default function App() {
  return (
    <View>
      <TextInput
        placeholder="Введите текст"
      />
    </View>
  )
}
```
  
Здесь `placeholder` отображает подсказку, если поле пустое.

### Uncontrolled vs Controlled TextInput

В React и React Native существует два подхода к работе с полями ввода: неконтролируемые (uncontrolled) и контролируемые (controlled).

- **Контролируемый TextInput**: Значение зависит от состояния React, обычно с помощью хука useState.
- **Неконтролируемый TextInput**: Значение живет внутри компонента; React не управляет им напрямую.

Чаще всего в React Native используется контролируемый способ — так вам проще валидировать и обрабатывать данные.

Input и TextInput являются основными компонентами для ввода текста в React Native приложениях, и их правильная настройка и использование критичны для обеспечения удобного пользовательского опыта. Важно уметь обрабатывать ввод, валидировать данные, настраивать внешний вид и обеспечивать доступность для пользователей с ограниченными возможностями. Если вы хотите детальнее погрузиться в настройку и использование input и textinput, а также другие аспекты создания UI в React Native, — приходите на наш большой курс [React Native и Expo Router](https://purpleschool.ru/course/react-native?utm_source=knowledgebase&utm_medium=article&utm_campaign=Nastroyka-i-ispolzovanie-input-i-textinput-v-React-Native). На курсе 184 уроков и 11 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

#### Контролируемый пример:

```jsx
import React, { useState } from 'react'
import { View, TextInput, Text } from 'react-native'

export default function ControlledInput() {
  const [text, setText] = useState('')

  return (
    <View>
      <TextInput
        placeholder="Введите имя"
        value={text}
        onChangeText={setText} // onChangeText передает новый ввод
      />
      <Text>Вы ввели: {text}</Text>
    </View>
  )
}
```
  
В этом примере вы всегда храните актуальное значение поля в состоянии компонента (`text`), что позволяет гибко реагировать на изменения.

## Основные свойства и методы TextInput

`TextInput` обладает множеством полезных свойств. Давайте рассмотрим их подробнее.

### Свойство value и обратный вызов onChangeText

- **value** — текущее значение текстового поля.
- **onChangeText** — функция, которая вызывается при каждом изменении текста. Обычно задается как обработчик, который обновляет состояние компонента.

```jsx
<TextInput
  value={text}
  onChangeText={setText}
/>
```

### placeholder и placeholderTextColor

- **placeholder** — отображает подсказку, когда поле пустое.
- **placeholderTextColor** — задает цвет текста подсказки.

```jsx
<TextInput
  placeholder="Введите email"
  placeholderTextColor="#999"
/>
```

### keyboardType 

Это свойство определяет тип экранной клавиатуры, которая будет показана пользователю. Вот основные значения:

- `default` (по умолчанию, универсальная клавиатура)
- `numeric` (цифровая клавиатура)
- `email-address` (специализированная клавиатура для email)
- `phone-pad` (клавиатура для телефона)
- ...и другие специфические типы

Пример, если вы ожидаете телефон:

```jsx
<TextInput
  keyboardType="phone-pad"
  placeholder="Введите номер телефона"
/>
```

### secureTextEntry: работа с паролями

Если вам требуется скрытый ввод (например, для поля пароля), используйте свойство `secureTextEntry`.

```jsx
<TextInput
  secureTextEntry={true}
  placeholder="Введите пароль"
/>
```

Теперь символы, которые вводит пользователь, будут скрыты. 

### multiline и numberOfLines

Если вашему приложению нужен ввод нескольких строк или абзацев, включите свойство `multiline`.

```jsx
<TextInput
  multiline={true}
  numberOfLines={4} // Количество строк, видимых пользователю
  placeholder="Напишите сообщение..."
/>
```
Обратите внимание: в iOS и Android компонент ведет себя немного по-разному, но для большинства задач этого достаточно.

### autoCapitalize, autoCorrect, maxLength и другие параметры

Эти параметры существенно влияют на удобство набора текста.

- **autoCapitalize**: контролирует автоматическое изменение регистра (например, `sentences`, `words`, `characters`, `none`).
- **autoCorrect**: включает автокоррекцию (true/false).
- **maxLength**: ограничивает максимальное число символов.
- **editable**: делает поле доступным или недоступным для ввода.

Пример — поле ФИО:

```jsx
<TextInput
  placeholder="ФИО"
  autoCapitalize="words"
  autoCorrect={false}
  maxLength={50}
  editable={true}
/>
```

### style и стилизация TextInput

Cтилизация происходит через свойство `style`, аналогично большинству элементов в React Native. 

```jsx
<TextInput
  style={{
    height: 48,
    borderColor: '#007AFF',
    borderWidth: 1,
    paddingHorizontal: 12,
    borderRadius: 8
  }}
  placeholder="Введите текст"
/>
```

Здесь вы видите базовую рамку, скругления и внутренние отступы. Можно создавать стили через StyleSheet для переиспользования.

## Работа с клавиатурой в TextInput

Мобильная клавиатура влияет на поведение приложения, её появление может перекрывать другие элементы на экране. React Native предлагает инструменты, которые помогают управлять этими аспектами.

### Управление появлением/скрытием клавиатуры

Чтобы скрыть клавиатуру при необходимости, используйте метод `Keyboard.dismiss()` из пакета `react-native`.

```jsx
import { Keyboard, TouchableWithoutFeedback } from 'react-native'

<TouchableWithoutFeedback onPress={Keyboard.dismiss}>
  <View>{/* Ваши компоненты */}</View>
</TouchableWithoutFeedback>
```

Теперь при нажатии вне текстовых полей клавиатура будет исчезать.

### Фокусировка и рефы

Иногда требуется программно установить фокус на поле ввода или убрать его. Для этого удобно использовать `ref`:

```jsx
import React, { useRef } from 'react'
import { TextInput, Button, View } from 'react-native'

export default function FocusInput() {
  const inputRef = useRef(null)

  const focusInput = () => {
    inputRef.current && inputRef.current.focus()
  }

  return (
    <View>
      <TextInput
        ref={inputRef}
        placeholder="Имя"
      />
      <Button title="Фокус на поле" onPress={focusInput} />
    </View>
  )
}
```

### Перемещение между полями (focusNext)

В длинных формах пользователь часто хочет быстро переходить между полями. Можно реализовать это с помощью нескольких рефов:

```jsx
import React, { useRef } from 'react'
import { TextInput, View } from 'react-native'

export default function MultiInputForm() {
  const input2 = useRef(null)

  return (
    <View>
      <TextInput
        placeholder="Поле 1"
        returnKeyType="next"
        onSubmitEditing={() => input2.current && input2.current.focus()}
      />
      <TextInput
        ref={input2}
        placeholder="Поле 2"
      />
    </View>
  )
}
```
  
Здесь при нажатии Enter на первом поле, курсор автоматически переходит во второе.

### Smart Keyboard Avoiding

Когда клавиатура появляется, она может перекрыть поле ввода, что ухудшает UX. Чтобы этого избежать, используйте компоненты `KeyboardAvoidingView` (поведение платформ отличается):

```jsx
import { KeyboardAvoidingView, Platform } from 'react-native'

<KeyboardAvoidingView
  behavior={Platform.OS === "ios" ? "padding" : "height"}
  style={{ flex: 1 }}
>
  {/* Ваши поля ввода */}
</KeyboardAvoidingView>
```

## Обработка текстовых событий

TextInput поддерживает множество событий, которые помогают реализовать сложные сценарии работы с данными пользователя.

### onFocus, onBlur

- **onFocus** вызывается при получении фокуса.
- **onBlur** — при потере фокуса.

Часто используются для изменения стилей поля или запуска проверки данных.

```jsx
<TextInput
  onFocus={() => console.log('Фокус в поле')}
  onBlur={() => console.log('Фокус потерян')}
/>
```

### onEndEditing и onSubmitEditing

- **onEndEditing**: вызывается после окончания редактирования (выход из поля).
- **onSubmitEditing**: срабатывает при нажатии на "Готово"/Enter на клавиатуре.

Пример, если хотите валидировать email после ввода:

```jsx
<TextInput
  onEndEditing={e => validateEmail(e.nativeEvent.text)}
/>
```

## Расширенные возможности и кастомизация

Разберем несколько интересных трюков и расширенных возможностей компонента `TextInput` в React Native.

### Изменение вида подчеркивания в Android

В Android по умолчанию у текстовых полей есть подчеркивание. Вы можете убрать его, задав свойство:

```jsx
<TextInput
  underlineColorAndroid="transparent"
/>
```

### Маска для ввода значений (например, телефон)

Для маски введённого значения используйте сторонние библиотеки, такие как [react-native-masked-text](https://github.com/benhurott/react-native-masked-text):

```jsx
import { TextInputMask } from 'react-native-masked-text'

<TextInputMask
  type={'custom'}
  options={{
      mask: '+7 (999) 999-99-99'
  }}
  value={phone}
  onChangeText={setPhone}
/>
```

Этот подход позволит отображать уже отформатированный номер во время ввода.

### Ограничение ввода только цифрами

Для таких задач удобно использовать свойство `keyboardType="numeric"` и проводить дополнительную валидацию прямо внутри onChangeText:

```jsx
const onChangeNumber = value => {
  // Разрешаем ввод только цифр
  const parsed = value.replace(/[^0-9]/g, '')
  setNumber(parsed)
}

<TextInput
  keyboardType="numeric"
  value={number}
  onChangeText={onChangeNumber}
/>
```

## Типовые компоненты на базе TextInput

Обычно компоненты ввода строятся по единому шаблону, позволяя использовать переиспользуемый код в вашем проекте.

### Базовый компонент ввода

Создадим простой обертку:

```jsx
import React from 'react'
import { TextInput, StyleSheet, View, Text } from 'react-native'

export default function Input({ label, error, ...props }) {
  return (
    <View style={styles.container}>
      <Text style={styles.label}>{label}</Text>
      <TextInput style={styles.input} {...props} />
      {error && <Text style={styles.error}>{error}</Text>}
    </View>
  )
}

const styles = StyleSheet.create({
  container: { marginVertical: 8 },
  label: { marginBottom: 4, fontWeight: 'bold' },
  input: { borderWidth: 1, borderColor: '#ccc', borderRadius: 6, padding: 12 },
  error: { color: 'red', marginTop: 4 }
})
```

В результате у вас появляется переиспользуемый Input с поддержкой ошибок и кастомизации.

## Подводные камни и советы по работе с TextInput

- Никогда не забывайте явно указывать свойство value для контролируемых компонентов, иначе возможны неожиданные баги.
- Если используете много TextInput на экране, подумайте о производительности и оптимизации перерисовок.
- Проверяйте особое поведение на iOS и Android: стили, появление клавиатуры, отступы могут отличаться.
- Тестируйте автозаполнение и autoCorrect с реальными клавиатурами разных устройств.
- Для форм с многими полями удобно использовать библиотеки — например, Formik и react-hook-form + yup для валидации.

В этой статье мы разобрали все основные и многие дополнительные аспекты работы с `TextInput` в React Native. Теперь вы знаете, как создавать простые и сложные поля ввода, управлять ими, оптимизировать UX с учетом платформы, а также кастомизировать внешний вид и поведение поля.

Настройка Input и TextInput — это лишь один из элементов создания удобного пользовательского интерфейса. Для разработки полноценного приложения необходимо также уметь создавать переиспользуемые компоненты, управлять состоянием, обеспечивать навигацию и работать с нативными модулями. На нашем курсе [React Native и Expo Router](https://purpleschool.ru/course/react-native?utm_source=knowledgebase&utm_medium=article&utm_campaign=Nastroyka-i-ispolzovanie-input-i-textinput-v-React-Native) вы найдете все необходимые знания для создания профессиональных React Native приложений. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир React Native прямо сегодня.

## Частозадаваемые технические вопросы и ответы

### Как отключить автозаполнение или автозамену в TextInput?

Для отключения автокоррекции используйте свойство autoCorrect:

```jsx
<TextInput autoCorrect={false} />
```
Для авто-заполнения на Android/iOS используются разные подходы, но еще можно добавить текстовый тип:

```jsx
<TextInput textContentType="none" />
```

### Как очистить поле ввода программно?

Вы можете сбросить значение, используя состояние:

```jsx
const [value, setValue] = useState("")
setValue("") // Очистить поле
```
Или вызвать метод clear() через ref:

```jsx
inputRef.current.clear()
```

### Как сделать только чтение в TextInput?

Задайте свойство editable:

```jsx
<TextInput editable={false} />
```

### Как сделать кастомную кнопку “показать/скрыть пароль”?

Используйте состояние для переключения:

```jsx
const [secure, setSecure] = useState(true)

<TextInput secureTextEntry={secure} />
<Button title="👁" onPress={() => setSecure(!secure)} />
```

### Как динамически менять стиль TextInput при ошибке или фокусе?

Используйте условную вставку стилей:

```jsx
<TextInput
  style={[
    styles.input,
    error && styles.inputError,
    focused && styles.inputFocused
  ]}
  onFocus={() => setFocused(true)}
  onBlur={() => setFocused(false)}
/>
```
Где `styles.inputError` и `styles.inputFocused` — дополнительные стили.
