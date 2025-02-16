# Leetcode---1718
Construct the Lexicographically Largest Valid Sequence
//code in java
class Solution {
    private int[] result;
    private boolean[] used;
    
    public int[] constructDistancedSequence(int n) {
        result = new int[2 * n - 1];
        used = new boolean[n + 1];
        
        if (backtrack(0, n)) {
            return result;
        }
        
        return new int[0];
    }
    
    private boolean backtrack(int index, int n) {
        if (index == result.length) {
            return true;
        }
        
        if (result[index] != 0) {
            return backtrack(index + 1, n);
        }
        
        for (int num = n; num >= 1; num--) {
            if (used[num]) {
                continue;
            }
            
            result[index] = num;
            used[num] = true;
            
            if (num == 1) {
                if (backtrack(index + 1, n)) {
                    return true;
                }
            } else if (index + num < result.length && result[index + num] == 0) {
                result[index + num] = num;
                
                if (backtrack(index + 1, n)) {
                    return true;
                }
                
                result[index + num] = 0;
            }
            
            result[index] = 0;
            used[num] = false;
        }
        
        return false;
    }
    
    public static void main(String[] args) {
        Solution solution = new Solution();
        int n = 3;
        int[] result = solution.constructDistancedSequence(n);
        System.out.println("The constructed sequence is: ");
        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
