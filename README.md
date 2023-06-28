# UNIBIT_Assessment_Solution

import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.*;

public class TwoSumCombination {
    public static int[][] findTwoSumCombination(int[] nums, int target) {
        Map<Integer, List<List<Integer>>> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    List<Integer> pair = Arrays.asList(nums[i], nums[j]);
                    if (!map.containsKey(target))
                        map.put(target, new ArrayList<>());
                    map.get(target).add(pair);
                }
            }
        }
        int[][] result = new int[map.get(target).size()][2];
        for (int i = 0; i < map.get(target).size(); i++) {
            result[i][0] = map.get(target).get(i).get(0);
            result[i][1] = map.get(target).get(i).get(1);
        }
        return result;
    }

    public static int[][] findDoubleTargetCombination(int[] nums, int target) {
        int doubleTarget = target * 2;
        Map<Integer, List<List<Integer>>> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                for (int k = j + 1; k < nums.length; k++) {
                    for (int l = k + 1; l < nums.length; l++) {
                        if (nums[i] + nums[j] + nums[k] + nums[l] == doubleTarget) {
                            List<Integer> combination = Arrays.asList(nums[i], nums[j], nums[k], nums[l]);
                            if (!map.containsKey(doubleTarget))
                                map.put(doubleTarget, new ArrayList<>());
                            map.get(doubleTarget).add(combination);
                        }
                    }
                }
            }
        }
        int[][] result = new int[map.get(doubleTarget).size()][4];
        for (int i = 0; i < map.get(doubleTarget).size(); i++) {
            List<Integer> combination = map.get(doubleTarget).get(i);
            for (int j = 0; j < combination.size(); j++) {
                result[i][j] = combination.get(j);
            }
        }
        return result;
    }

    public static void main(String[] args) {
      
        int[] nums = {1, 3, 2, 2, -4, -6, -2, 8};
        int target = 4;

        int[][] twoSumCombination = findTwoSumCombination(nums, target);
        System.out.println("First Combination For \"" + target + "\":");
        for (int[] pair : twoSumCombination) {
            System.out.println(Arrays.toString(pair));
        }

        int[] mergedArray = Arrays.stream(nums).sorted().toArray();
        System.out.println("Merge Into a Single Array:");
        System.out.println(Arrays.toString(mergedArray));

        int[][] doubleTargetCombination = findDoubleTargetCombination(mergedArray, target);
        int doubleTarget = target * 2;
        System.out.println("Second Combination For \"" + doubleTarget + "\":");
        for (int[] combination : doubleTargetCombination) {
            System.out.println(Arrays.toString(combination));
        }
    }
}
