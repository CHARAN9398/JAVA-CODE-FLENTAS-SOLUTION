import java.util.*;

public class PermutationInString {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int t = scanner.nextInt(); // number of test cases
        
        while (t-- > 0) {
            String pattern = scanner.next();
            String text = scanner.next();
            
            // create frequency maps for pattern and current window in text
            Map<Character, Integer> patternFreq = getFrequencyMap(pattern);
            Map<Character, Integer> windowFreq = getFrequencyMap(text.substring(0, pattern.length()));
            
            boolean found = false;
            for (int i = pattern.length(); i <= text.length(); i++) {
                if (patternFreq.equals(windowFreq)) {
                    found = true;
                    break;
                }
                
                // remove first character from window and add next character
                char prevChar = text.charAt(i - pattern.length());
                int prevCount = windowFreq.get(prevChar);
                if (prevCount == 1) {
                    windowFreq.remove(prevChar);
                } else {
                    windowFreq.put(prevChar, prevCount - 1);
                }
                
                char nextChar = i < text.length() ? text.charAt(i) : '\0';
                windowFreq.put(nextChar, windowFreq.getOrDefault(nextChar, 0) + 1);
            }
            
            System.out.println(found ? "YES" : "NO");
        }
    }
    
    
    private static Map<Character, Integer> getFrequencyMap(String str) {
        Map<Character, Integer> freq = new HashMap<>();
        for (char c : str.toCharArray()) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }
        return freq;
    }
}
K CHARAN
kasamsettycharan@gmail.com
9398074963
