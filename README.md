# ValidParenthesis
public class ValidParentheses {
    public static boolean isValidParentheses(String s) {
        int minOpen = 0; // Minimum open parentheses required
        int maxOpen = 0; // Maximum open parentheses possible
        
        for (char c : s.toCharArray()) {
            if (c == '(') {
                // Increment both min and max for an opening parenthesis
                minOpen++;
                maxOpen++;
            } else if (c == ')') {
                // Decrement both min and max for a closing parenthesis
                minOpen = Math.max(minOpen - 1, 0); // Min cannot go below 0
                maxOpen--;
            } else {
                // For '*', treat it as '(', ')' or an empty string
                minOpen = Math.max(minOpen - 1, 0); // Treat as ')'
                maxOpen++; // Treat as '('
            }

            // If maxOpen becomes negative, parentheses are invalid
            if (maxOpen < 0) {
                return false;
            }
        }

        // String is valid if minOpen is 0 (all open parentheses are closed)
        return minOpen == 0;
    }

    public static void main(String[] args) {
        // Test cases
        System.out.println(isValidParentheses("(*)"));       // true
        System.out.println(isValidParentheses("((*)"));      // true
        System.out.println(isValidParentheses("(*))"));      // true
        System.out.println(isValidParentheses("(((**)"));    // false
        System.out.println(isValidParentheses(")"));         // false
    }
}
