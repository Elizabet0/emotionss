# Emotion Recognition from Facial Expressions

Проект по детекции лиц и последующему распознаванию эмоций на основе использования сверточной нейронной сети. Датасет fer2013, 35к изображений, 7 эмоций.

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
│   ├── Augms.ipynb                  # Обучение и тест с аугментацией
│   └──Detector.ipynb                # Детектор лиц 
├── best_models/                     # Сохранённые модели
│   ├── model_checkpoint_60.62.pth
│   └── ...
├── data/                            # Датасет 
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

## Аугментация

Я решила сделать аугментацию disgust и fear (('flip', 'rotate', 'brightness', 'contrast')) из-за дисбаланса классов и по результатам метрик по этим классам. Accuracy после этого упало с 60.87 до 57.78 :( 

## Детектор

Детектор не входил в изначальные планы по проекту, так как в датасете и так обрезаны лица. Поэтому он просто "приклеен": отдельно есть ноутбук, куда можно передать свою картинку, затем применяется детектор haarcascades _frontalface (каскад Хаара для фронтальной части лица) и затем обрезанная детектором часть изображения передаётся в обученню CNNку.

## Окончательный пример работы детектора + классификатора

![Снимок экрана 2026-01-22 020205](https://github.com/user-attachments/assets/50a3e054-402f-471a-94b6-a04ffaf00546)

## Результатыss

-- CNN  **60.876%**

(По всем метрикам кому интересно:)
```
                precision    recall  f1-score   support

        fear       0.49      0.31      0.38      1024
       happy       0.79      0.84      0.81      1774
         sad       0.48      0.49      0.48      1247
    surprise       0.72      0.77      0.74       831
     disgust       0.68      0.36      0.47       111
       angry       0.51      0.51      0.51       958
     neutral       0.54      0.64      0.58      1233

    accuracy                           0.61      7178
   macro avg       0.60      0.56      0.57      7178
weighted avg       0.60      0.61      0.60      7178
```