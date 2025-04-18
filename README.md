# 📊 Анализ A/B-тестов и линеаризация метрик

## 🗂 Описание

Этот репозиторий содержит анализ результатов двух экспериментов по улучшению рекомендательного алгоритма. В первом случае мприменяется классический метод анализа A/B-теста, во втором — более продвинутый подход с использованием **линеаризации метрик**, позволяющий повысить чувствительность статистических тестов.

---

## 🧪 Задание 1 — Классический анализ A/B-теста (Группы 1 и 2)

### 📅 Период эксперимента:
2025-01-31 — 2025-02-06

### 🧾 Описание:
- **Группа 1** — контрольная (старый алгоритм)
- **Группа 2** — тестовая (новый алгоритм рекомендаций)
- Цель: проверить, приводит ли новый алгоритм к увеличению CTR (лайки/просмотры)

---

### 🔬 Применённые методы анализа:

- T-тест по пользовательскому CTR
- Манна-Уитни тест
- Пуассоновский бутстрап
- Сглаженный CTR (α=5)
- Бакетизация + T-тест и Манна-Уитни

---

### 📊 Результаты:

- **T-тест по "сырым" пользовательским CTR** показал **высокое p-value**, т.е. **различий не выявлено** — вероятно, из-за высокой дисперсии и выбросов.
- **Манна-Уитни и t-тест после бакетизации** показали **низкие p-value** → **статистически значимая разница**.
- **Бутстрап** визуально показал различие в распределениях CTR — в тестовой группе вовлечённость ниже.

---

### 📉 Вывод:

📌 **CTR в экспериментальной группе (группа 2) оказался значительно ниже, чем в контрольной (группа 1).**  
📌 Тесты сработали так, потому что в выборке наблюдаются:
- высокая дисперсия,
- ненормальность распределения,
- возможные выбросы.

---

### 💡 Потенциальные причины:

1. Ошибки в реализации нового алгоритма
2. Новый функционал не понравился пользователям
3. Сильная неоднородность реакций аудитории (много выбросов)

---

### 🚫 Заключение:

**Не стоит** внедрять новый алгоритм на всю аудиторию.

---

### ✅ Рекомендации:

1. Проверить реализацию на наличие технических багов
2. Собрать качественную обратную связь от пользователей
3. Улучшить алгоритм с учётом предпочтений и повторно протестировать

---

## 📊 Задание 2 — Линеаризация метрик (CTR → Linearized Likes)

### 🎯 Цель:

Применить **метод линеаризации**, чтобы повысить чувствительность теста и точнее выявить изменения в метрике CTR (likes/views).

---

### 🔬 Метод:

1. Посчитать общий CTR в контрольной группе.
2. Построить линеаризованную метрику по формуле.
3. Сравнить группы с помощью t-теста по новой метрике.

---

### 📈 Сравнение по группам:

#### Группы 0 и 3:
- p-value по обычному CTR ≈ **0.68** — **различий не выявлено**
- p-value по линеаризованным лайкам ≈ **2.98e-09** — **различия статистически значимы**

#### Группы 1 и 2:
- Аналогичная картина — линеаризация помогла выявить различия, которые не были заметны при анализе обычного CTR.

---

### 💡 Вывод:

- Линеаризация **значительно снижает p-value**
- Повышается **чувствительность теста**
- Различия между группами становятся **более заметными**
- Метод особенно полезен при **большой дисперсии и шуме** в пользовательских метриках

---

## 🛠 Используемые библиотеки:

- Python 3.11+
- pandas, numpy
- scipy.stats
- matplotlib, seaborn
- tqdm (для прогресса симуляций)
