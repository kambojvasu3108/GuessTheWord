# GuessTheWord
#word
package game;

import java.util.Random;

public class Words {
	
	private String[] randomWords = {"animals", "happiness", "indefinite", "steady", "birthday", "extreme", "rights", "properties", "ceremony", "independence"
, "beneath", "information", "students", "employee"};
	
	public String selectedWord;
	private Random random = new Random();
	private char[] letters;
	
	public Words() {
		selectedWord = randomWords[random.nextInt(randomWords.length)];
		letters = new char[selectedWord.length()];
	}
	
	public String toString() {
		
		//String word = " ";
		StringBuilder text = new StringBuilder();
		//letters[1] = 'a';
		//letters[2] = 'a';
		
		for(char letter: letters) {
			
			text.append(letter == '\u0000' ? '-' : letter);
			
//			if(letter == '\u0000') {
//				//word += '-';
//				text.append('-');
//			}
//			else {
//				//word += letter;
//				text.append(letter);
//			}
			//word += ' ';
			text.append(' ');
		}
		
		//return word;
		return text.toString();		
		//return randomWords[1];
		//return selectedWord;
	}
	
	public boolean isGuessedRight() {
		for(char letter: letters) {
			if(letter == '\u0000') {
				return false;
			}
		}
		return true;
	}

	public boolean guess(char letter) {
		
		boolean guessedRight = false;
		
		for(int i = 0; i<selectedWord.length(); i++) {
			if(letter == selectedWord.charAt(i)) {
				letters[i] = letter;
				guessedRight = true;
			}
		}
		return guessedRight;
		
	}
}

#application
package game;

public class Application {

	public static void main(String[] args) {
		Guess_the_word game = new Guess_the_word();
		game.start();
		game.end();

	}

}


#Guess the word
package game;

import java.util.Scanner;

public class Guess_the_word {

	private boolean play = true;
	private Scanner scanner = new Scanner(System.in);
	private Words randomWord = new Words();
	private int rounds = 10;
	private char lastRound;

	public void start() {

		do {
			showWord();
			getInput();
			checkInput();
		} while (play);

	}

	void showWord() {
		System.out.println("You have " + rounds + " tries left.");
		System.out.println(randomWord);
	}

	void getInput() {
		System.out.print("Enter a letter to guess the word:");
		String userGuess = scanner.nextLine();
		lastRound = userGuess.charAt(0);
		// System.out.println("getInput");
		// char letter;

	}

	void checkInput() {
		// System.out.println("checkInput");

		boolean isGuessedRight = randomWord.guess(lastRound);

		if (isGuessedRight) {
			if (randomWord.isGuessedRight()) {
				System.out.println("Congrats, you won!");
				System.out.println("The word is: " + randomWord);
				play = false;
			}
		}
		else {
			rounds--;
			if(rounds == 0) {
				System.out.println("Game Over!");
				play = false;
			}
		}
	}

	public void end() {
		scanner.close();
	}

}
