# Emotion Recognition from Facial Expressions

Проект по распознаванию эмоций на основе изображений лиц с использованием двух алгоритмов: сверточной нейронной сети (CNN) и градиентного бустинга (CatBoost).

## Структура проекта

emotions/
├── notebook/                       # Jupyter ноутбуки
│   ├── mini_eda.ipynb
│   ├── CNN_training.ipynb          # Обучение CNN
│   ├── CNN_testing.ipynb           # Тестирование CNN
│   └── CatBoost.ipynb              # Обучение и тест CatBoost
├── best_models/                    # Сохранённые модели
│   ├── model_checkpoint_60.62.pth
│   └── catboost_model.cbm
├── data/                           # Датасет 
│   ├── train/
│   │   ├── angry/
│   │   ├── disgust/
│   │   └── ...
│   └── test/
│       ├── angry/
│       ├── disgust/
│       └── ...
├── README.md                       # Этот файл
└── requirements.txt                # Зависимости

## Результаты

-- CNN (PyTorch) **60.62%** | 
-- CatBoost | 42.4% 

## Архитектура CNN

emotions/
├── notebook/    # Jupyter ноутбуки
│   ├── mini_eda.ipynb
│   ├── CNN_training.ipynb    # Обучение CNN
│   ├── CNN_testing.ipynb    # Тестирование CNN
│   └── CatBoost.ipynb # Обучение и тест CatBoost
├── best_models/    # Сохранённые модели
│   ├── model_checkpoint_60.62.pth
│   └── catboost_model.cbm
├── data/      # Датасет 
│   ├── train/
│   │   ├── angry/
│   │   ├── disgust/
│   │   └── ...
│   └── test/
│       ├── angry/
│       ├── disgust/
│       └── ...
├── README.md                 # Этот файл
└── requirements.txt          # Зависимости