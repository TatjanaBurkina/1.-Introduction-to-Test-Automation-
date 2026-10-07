# 🚪 Monty Hall Paradox Simulation (Симулятор парадокса Монти Холла)

Учебный Java-проект, моделирующий классический математический парадокс Монти Холла с использованием принципов объектно-ориентированного программирования (ООП) и паттерна проектирования **«Стратегия» (Strategy Pattern)**. Проект покрыт юнит-тестами для проверки вероятностей и собран с помощью Maven.

---

## 🛠 Технологии и стек
* **Java 11+**
* **Maven** (управление зависимостями и сборка)
* **JUnit 4** (модульное тестирование)
* **Design Patterns:** Strategy Pattern

---

## 📂 Архитектура и примеры стратегий (`GameStrategy`)
В проекте реализована гибкая архитектура с использованием интерфейса `GameStrategy`, что позволяет легко добавлять новые правила поведения игрока:
* **`AlwaysSwitchStrategy.java`** — стратегия постоянного переключения двери. Статистически приводит примерно к 2/3 (66%) побед.
* **`NeverSwitchStrategy.java`** — стратегия сохранения первоначального выбора. Статистически дает около 1/3 (33%) побед.
* **`RandomSwitchStrategy.java`** — стратегия случайного выбора с вероятностью смены двери 50/50.

---

## 💻 Пример кода симуляции (`MontyHallSimulation.java`)

```java
package com.example;
import java.util.Random;

public class MontyHallSimulation {
    private static final int NUM_ROUNDS = 1000;

    public int runSimulation(GameStrategy strategy) {
        int wins = 0;
        Random random = new Random();
        for (int i = 0; i < NUM_ROUNDS; i++) {
            int prizeDoor = random.nextInt(3);
            int playerChoice = random.nextInt(3);
            int revealedDoor;
            do {
                revealedDoor = random.nextInt(3);
            } while (revealedDoor == prizeDoor || revealedDoor == playerChoice);

            if (strategy.shouldSwitch()) {
                playerChoice = 3 - playerChoice - revealedDoor;
            }
            if (playerChoice == prizeDoor) {
                wins++;
            }
        }
        return wins;
    }
}
