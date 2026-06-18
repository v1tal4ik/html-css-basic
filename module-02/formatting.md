# Автоформатування при збереженні у VS Code

## Крок 1: Встановити Prettier

1. Відкрити панель розширень: `Cmd + Shift + X`
2. Знайти "Prettier - Code formatter"
3. Натиснути Install

## Крок 2: (Опціонально) Створити конфіг Prettier у проєкті

Файл `.prettierrc` в корені проєкту:

{
"printWidth": 80,
"semi": true,
"singleQuote": true,
"tabWidth": 2,
"trailingComma": "es5"
}

## Крок 3: Відкрити налаштування

`Cmd + Shift + P` → ввести "Preferences: Open Settings (JSON)" → Enter

## Крок 4: Додати налаштування

У файл `settings.json` додати:

{
"editor.formatOnSave": true,
"editor.defaultFormatter": "esbenp.prettier-vscode"
}

## Важливо

- Після цього при кожному `Cmd + S` код автоматично форматується.
- Prettier підтримує HTML, CSS, JS, JSON, Markdown та інші.
- Якщо форматування не працює — перевірити що Prettier обраний як Default Formatter.
- Для конкретної мови можна задати окремий форматер у settings.json.
