# Emotion Recognition from Facial Expressions

Проект по детекции лиц и последующему распознаванию эмоций на основе использования и сравнения двух алгоритмов: сверточной нейронной сети и градиентного бустинга (CatBoost). Датасет fer2013, 35к изображений, 7 эмоций.

## Описание проекта

Бывало ли у Вас такое, что при общении с человеком не можете понять, что он сейчас испытывает? (Ну, poor empathy skills, все такое..) А ещё и фокусировать свой взгляд надо на нем, чтобы казаться заинтересованным.. в общем, тяжело.
Моя моделька решает Ваши проблемы!

## Быстрый старт
1. git clone https://github.com/Elizabet0/emotionss.git
2. pip install -r requirements.txt
3. Откройте notebook/Detector.ipynb и вставьте Ваше изображение для тестирования! :)

## Структура проекта
```
emotions/
├── notebook/                        # Jupyter ноутбуки
│   ├── mini_eda.ipynb               # EDA анализ
│   ├── CNN_training.ipynb           # Обучение CNN
│   ├── CNN_testing.ipynb            # Тестирование CNN
│   ├── CatBoost.ipynb               # Обучение и тест CatBoost
│   ├── Detector.ipynb               # Детектор лиц
│   └── exeperimenting.ipynb         # Эксперименты с локальными фото
├── best_models/                     # Сохранённые модели
│   ├── model_checkpoint_60.62.pth
│   └── catboost_model.cbm
├── data/                            # Датасет (не в репозитории)
│   ├── train/
│   │   ├── angry/
│   │   ├── disgust/
│   │   └── ...
│   └── test/
│       ├── angry/
│       ├── disgust/
│       └── ...
├── README.md                        # Этот файл
└── requirements.txt                 # Зависимости
``` 

## Архитектура CNN
```
Input (1, 48, 48) → 
Conv2d(1→16) → BN → ReLU → 
Conv2d(16→16) → BN → ReLU → MaxPool2d(2)

Conv2d(16→32) → BN → ReLU → 
Conv2d(32→32) → BN → ReLU → MaxPool2d(2)

Conv2d(32→64) → BN → ReLU → MaxPool2d(2)

Flatten() → Dropout → Linear → BN → ReLU → Dropout → Linear
```
PS. BN - BatchNorm2d

## Catboost - 42.4%

iterations=300, learning_rate=0.1, depth=5, random_seed=42, eval_metric='Accuracy', early_stopping_rounds=50, use_best_model=True

Оценка проводилась на валидационной выборке (train/val = 85/15)

## Детектор

Детектор не входил в изначальные планы по проекту, так как в датасете и так обрезаны лица. Поэтому он просто "приклеен": отдельно есть ноутбук, куда можно передать картинку, и сначала делается конвертация в grayscale, затем применяется детектор haarcascades _frontalface (каскад Хаара для фронтальной части лица) и в конце концов обрезанная детектором часть изображения, изменённая до 48*48, передаётся в обученню CNNку.

## Окончательный пример работы детектора + классификатора

![Снимок экрана 2026-01-22 020205](https://github.com/user-attachments/assets/50a3e054-402f-471a-94b6-a04ffaf00546)

## Результатыss

-- CNN  **60.62%**

-- CatBoost 42.4% 

## TBD

Аугментация, вебка
