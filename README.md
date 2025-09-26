# Пушкина Мария 
# Задание 1


package hangman;

import java.util.Arrays;
import java.util.Random;
import java.util.Scanner;

public class HangmanGame {
    // Список слов для отгадывания
    private static final String[] WORDS = {
        "программирование", "компьютер", "алгоритм", 
        "интерфейс", "база", "фреймворк"
    };
    
    private static final int MAX_TRIES = 6;
    private String word;
    private char[] guess;
    private int tries;
    private StringBuilder used;
    
    public HangmanGame() {
        Random rand = new Random();
        this.word = WORDS[rand.nextInt(WORDS.length)];
        this.guess = new char[word.length()];
        Arrays.fill(guess, '_');
        this.tries = MAX_TRIES;
        this.used = new StringBuilder();
    }
    
    private void showGame() {
        System.out.println("\nСлово: " + String.valueOf(guess));
        System.out.println("Жизни: " + tries);
        System.out.println("Были: " + used.toString());
        drawMan();
    }
    
    private void drawMan() {
        switch (tries) {
            case 6:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |");
                System.out.println(" |");
                System.out.println(" |");
                System.out.println("_|_");
                break;
            case 5:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |    O");
                System.out.println(" |");
                System.out.println(" |");
                System.out.println("_|_");
                break;
            case 4:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |    O");
                System.out.println(" |    |");
                System.out.println(" |");
                System.out.println("_|_");
                break;
            case 3:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |    O");
                System.out.println(" |   /|");
                System.out.println(" |");
                System.out.println("_|_");
                break;
            case 2:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |    O");
                System.out.println(" |   /|\\");
                System.out.println(" |");
                System.out.println("_|_");
                break;
            case 1:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |    O");
                System.out.println(" |   /|\\");
                System.out.println(" |   /");
                System.out.println("_|_");
                break;
            case 0:
                System.out.println("  ____");
                System.out.println(" |    |");
                System.out.println(" |    O");
                System.out.println(" |   /|\\");
                System.out.println(" |   / \\");
                System.out.println("_|_");
                break;
        }
    }
    
    private boolean checkLetter(char letter) {
        letter = Character.toLowerCase(letter);
        
        // Проверяем, была ли буква
        if (used.indexOf(String.valueOf(letter)) != -1) {
            System.out.println("Уже была эта буква!");
            return false;
        }
        
        used.append(letter).append(" ");
        
        boolean found = false;
        for (int i = 0; i < word.length(); i++) {
            if (word.charAt(i) == letter) {
                guess[i] = letter;
                found = true;
            }
        }
        
        if (!found) {
            tries--;
            System.out.println("Нет буквы '" + letter + "'!");
        } else {
            System.out.println("Есть буква '" + letter + "'!");
        }
        
        return found;
    }
    
    private boolean isWin() {
        return String.valueOf(guess).equals(word);
    }
    
    private boolean isEnd() {
        return tries <= 0 || isWin();
    }
    
    public void start() {
        Scanner sc = new Scanner(System.in);
        
        System.out.println("Игра 'Виселица'!");
        System.out.println("Угадай слово. Осталось " + MAX_TRIES + " жизней.");
        
        while (!isEnd()) {
            showGame();
            
            System.out.print("\nВведи букву: ");
            String input = sc.nextLine().trim();
            
            if (input.length() != 1 || !Character.isLetter(input.charAt(0))) {
                System.out.println("Нужно одну букву!");
                continue;
            }
            
            checkLetter(input.charAt(0));
        }
        
        showGame();
        
        if (isWin()) {
            System.out.println("\n Ура! Слово: " + word);
        } else {
            System.out.println("\n Проиграл! Слово было: " + word);
        }
        
        sc.close();
    }
    
    public static void main(String[] args) {
        HangmanGame game = new HangmanGame();
        game.start();
    }
}

# Задание 2

package currencyconverter;

import java.util.Scanner;

public class CurrencyConverter {
    // Курсы валют относительно базовой валюты (USD)
    private static final double EUR_RATE = 0.85;
    private static final double GBP_RATE = 0.73;
    private static final double JPY_RATE = 110.25;
    private static final double CAD_RATE = 1.25;
    private static final double RUB_RATE = 73.50;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Запрос суммы у пользователя
        System.out.print("Введите сумму в USD: ");
        double amount = scanner.nextDouble();
        
        // Конвертация в другие валюты
        double eurAmount = amount * EUR_RATE;
        double gbpAmount = amount * GBP_RATE;
        double jpyAmount = amount * JPY_RATE;
        double cadAmount = amount * CAD_RATE;
        double rubAmount = amount * RUB_RATE;
        
        // Вывод результатов
        System.out.println("\nРезультаты конвертации:");
        System.out.println(amount + " USD = " + eurAmount + " EUR");
        System.out.println(amount + " USD = " + gbpAmount + " GBP");
        System.out.println(amount + " USD = " + jpyAmount + " JPY");
        System.out.println(amount + " USD = " + cadAmount + " CAD");
        System.out.println(amount + " USD = " + rubAmount + " RUB");
        
        scanner.close();
    }
}

# Задание 3
package passwordgenerator;

import java.util.Scanner;
import java.util.Random;

public class PasswordGenerator {
    // Наборы символов для пароля
    private static final String BIG_LETTERS = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    private static final String SMALL_LETTERS = "abcdefghijklmnopqrstuvwxyz";
    private static final String NUMBERS = "0123456789";
    private static final String SPECIAL_SYMBOLS = "!@#$%^&*()-_=+[]{}|;:,.<>?";
    
    // Объединенный набор всех символов
    private static final String ALL_SYMBOLS = BIG_LETTERS + SMALL_LETTERS + NUMBERS + SPECIAL_SYMBOLS;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        // Запрос длины пароля у пользователя
        System.out.print("Введите длину пароля (от 8 до 12 символов): ");
        int length = scanner.nextInt();
        
        // Проверка корректности длины
        if (length < 8 || length > 12) {
            System.out.println("Ошибка! Длина пароля должна быть от 8 до 12 символов.");
            scanner.close();
            return;
        }
        
        // Массив для хранения пароля
        char[] password = new char[length];
        
        // Гарантированно добавляем по одному символу из каждой категории
        password[0] = BIG_LETTERS.charAt(random.nextInt(BIG_LETTERS.length()));
        password[1] = SMALL_LETTERS.charAt(random.nextInt(SMALL_LETTERS.length()));
        password[2] = NUMBERS.charAt(random.nextInt(NUMBERS.length()));
        password[3] = SPECIAL_SYMBOLS.charAt(random.nextInt(SPECIAL_SYMBOLS.length()));
        
        // Заполняем оставшиеся позиции случайными символами из всех категорий
        for (int i = 4; i < length; i++) {
            password[i] = ALL_SYMBOLS.charAt(random.nextInt(ALL_SYMBOLS.length()));
        }
        
        // Перемешиваем символы в пароле для большей случайности
        for (int i = 0; i < length; i++) {
            int randomIndex = random.nextInt(length);
            char temp = password[i];
            password[i] = password[randomIndex];
            password[randomIndex] = temp;
        }
        
        // Вывод сгенерированного пароля
        System.out.println("Сгенерированный пароль: " + new String(password));
        
        scanner.close();
    }
}
