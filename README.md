import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.InputMismatchException;
import java.util.Scanner;

class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}

public class ExceptionHandlingExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Checked Exception Example
        try {
            BufferedReader reader = new BufferedReader(new FileReader("example.txt"));
            String line = reader.readLine();
            System.out.println("First line in file: " + line);
            reader.close();
        } catch (IOException e) {
            System.out.println("An IOException occurred: " + e.getMessage());
        }

        // Unchecked Exception Example
        try {
            int[] numbers = {1, 2, 3};
            System.out.println("Accessing invalid index: " + numbers[3]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("An ArrayIndexOutOfBoundsException occurred: " + e.getMessage());
        }

        // Custom Exception Example
        try {
            System.out.print("Enter a number: ");
            int userInput = scanner.nextInt();
            validateNumber(userInput);
        } catch (MyCustomException e) {
            System.out.println("Caught MyCustomException: " + e.getMessage());
        } catch (InputMismatchException e) {
            System.out.println("Please enter a valid number.");
            scanner.next(); // clear the invalid input
        }

        // Finally Block Example
        try {
            int result = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("An ArithmeticException occurred: " + e.getMessage());
        } finally {
            System.out.println("This is the finally block. It always executes.");
        }

        // Try with Multiple Catches Example
        try {
            String text = null;
            System.out.println(text.length());
            int result = 10 / 0;
        } catch (NullPointerException e) {
            System.out.println("A NullPointerException occurred: " + e.getMessage());
        } catch (ArithmeticException e) {
            System.out.println("An ArithmeticException occurred: " + e.getMessage());
        } finally {
            System.out.println("This is the finally block. It always executes.");
        }

        scanner.close();
    }

    public static void validateNumber(int number) throws MyCustomException {
        if (number < 0) {
            throw new MyCustomException("Number is negative!");
        } else {
            System.out.println("Number is valid.");
        }
    }
}
