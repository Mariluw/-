# Пушкина Мария
//Задание 1
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
            System.out.println("\n🎉 Ура! Слово: " + word);
        } else {
            System.out.println("\n💀 Проиграл! Слово было: " + word);
        }
        
        sc.close();
    }
    
    public static void main(String[] args) {
        HangmanGame game = new HangmanGame();
        game.start();
    }
}
