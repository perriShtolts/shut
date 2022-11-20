# shut
import java.util.InputMismatchException;
import java.util.Scanner;

public class calculator {

    public static Scanner scanner = new Scanner(System.in);
    static int num1, num2, result;
    static char action;

    public static void main(String[] args) {

        System.out.println("Этот калькулятор может складывать, разделять, умножать иделиь числа от 1 и до 10 включительно просто введите необходимое вам выражение. Ввод может осуществляться как арабскими так и римскими цифрами. Внимание, если вы введёте числа из разных систем счислений то выполнить операцию не удастся!");
        String read = scanner.nextLine();
        char[] massiv10 = new char [10];

        for (int a = 0; a < read.length(); a++) {
            massiv10[a] = read.charAt(a);
            if (massiv10[a] == '+') {
                action = '+';
            }
            if (massiv10[a] == '-') {
                action = '-';
            }
            if (massiv10[a] == '*') {
                action = '*';
            }
            if (massiv10[a] == '/') {
                action = '/';
            }
        }
        String under_charString = String.valueOf(massiv10);
        String[] blacks = under_charString.split("[+-/*]");
        String stable00 = blacks[0];
        String stable01 = blacks[1];
        String string03 = stable01.trim();
        num1 = romanToNumber(stable00);
        num2 = romanToNumber(string03);
        if (num1 < 0 && num2 < 0) {
            result = 0;
        } else {
            result = calculated(num1, num2, action);
            System.out.println("---Результат для римских цифр----");
            String resultRoman = convertNumToRoman(result);
            System.out.println(stable00 + " " + action + " " + string03 + " = " + resultRoman);
        }
        num1 = Integer.parseInt(stable00);
        num2 = Integer.parseInt(string03);
        result = calculated(num1, num2, action);
        System.out.println("--Результат для арабских цифр----");
        System.out.println(num1 + " " + action + " " + num2 + " = " + result);
    }

    private static String convertNumToRoman (int numArabian) {
        String[] roman = {"O", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X", "XI", "XII", "XIII", "XIV", "XV", "XVI", "XVII", "XVIII", "XIX", "XX",
                "XXI", "XXII", "XXIII", "XXIV", "XXV", "XXVI", "XXVII", "XXVIII", "XXIX", "XXX", "XXXI", "XXXII", "XXXIII", "XXXIV", "XXXV", "XXXVI", "XXXVII", "XXXVIII", "XXXIX", "XL",
                "XLI", "XLII", "XLIII", "XLIV", "XLV", "XLVI", "XLVII", "XLVIII", "XLIX", "L", "LI", "LII", "LIII", "LIV", "LV", "LVI", "LVII", "LVIII", "LIX", "LX",
                "LXI", "LXII", "LXIII", "LXIV", "LXV", "LXVI", "LXVII", "LXVIII", "LXIX", "LXX",
                "LXXI", "LXXII", "LXXIII", "LXXIV", "LXXV", "LXXVI", "LXXVII", "LXXVIII", "LXXIX", "LXXX",
                "LXXXI", "LXXXII", "LXXXIII", "LXXXIV", "LXXXV", "LXXXVI", "LXXXVII", "LXXXVIII", "LXXXIX", "XC",
                "XCI", "XCII", "XCIII", "XCIV", "XCV", "XCVI", "XCVII", "XCVIII", "XCIX", "C"
        };
        final String s = roman[numArabian];
        return s;
    }


    private static int romanToNumber (String roman) {
        try {
            if (roman.equals("I")) {
                return 1;
            } else if (roman.equals("II")) {
                return 2;
            } else if (roman.equals("III")) {
                return 3;
            } else if (roman.equals("IV")) {
                return 4;
            } else if (roman.equals("V")) {
                return 5;
            } else if (roman.equals("VI")) {
                return 6;
            } else if (roman.equals("VII")) {
                return 7;
            } else if (roman.equals("VIII")) {
                return 8;
            } else if (roman.equals("IX")) {
                return 9;
            } else if (roman.equals("X")) {
                return 10;
            }
        } catch (InputMismatchException e) {
            throw new InputMismatchException("Неверный формат данных");
        }
        return -1;
    }

    public static int calculated (int num1, int num2, char op) {
        int result = 0;
        switch (op) {
            case '+':
                result = num1 + num2;
                break;
            case '-':
                result = num1 - num2;
                break;
            case '*':
                result = num1 * num2;
                break;
            case '/':
                try {
                    result = num1 / num2;
                } catch (ArithmeticException | InputMismatchException e) {
                    System.out.println("Exception : " + e);
                    System.out.println("Only integer non-zero parameters allowed");

                    break;
                }
                break;
            default:
                throw new IllegalArgumentException("Не верный знак операции");
        }
        return result;
    }
}


