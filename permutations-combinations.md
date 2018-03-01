Permutations II & Combinations Sum II



Mistake was made on the condition of duplicates.

### What should be considered as duplicates?

1. if starts at the beginning?   No, that does not count as duplicate.   
2. pre.val == cur.val && in this time, we have not use the pre node. 



### Another mistake is put the add to list logic outside of the forloop.

### Apply the sort, things will became easier







wrong code:

```
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> resL = new ArrayList<>();
        List<Integer> tmpL = new ArrayList<>();
        HashSet<Integer> set = new HashSet<>();
        
        permuteUnique(nums, 0, tmpL, resL, set, Integer.MIN_VALUE);
        
        return resL;
    }
    
    private void permuteUnique(int[] num, int pos, List<Integer> tmpL, List<List<Integer>> resL, HashSet<Integer> visitedCachSet, int preV) {
        //  base case
        if (pos == num.length) {
            resL.add(new ArrayList<Integer>(tmpL));
            return;
        }
        if (preV == num[pos]) {
            return;
        }
        
        //  process
        tmpL.add(num[pos]);
        visitedCachSet.add(pos);
        
        for (int i = 0; i < num.length; i++) {
            if (visitedCachSet.contains(i)) {
                continue;
            }
            
            permuteUnique(num, i, tmpL, resL, visitedCachSet, num[pos]);
        }
        
        tmpL.remove(tmpL.size() - 1);
        visitedCachSet.remove(pos);
        //  return
        return;
    }
}
```

Correct one:

```
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        boolean[] used = new boolean[nums.length];
        List<Integer> list = new ArrayList<Integer>();
        Arrays.sort(nums);
        dfs(nums, used, list, res);
        return res;
    }

    public void dfs(int[] nums, boolean[] used, List<Integer> list, List<List<Integer>> res){
        if(list.size()==nums.length){
            res.add(new ArrayList<Integer>(list));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if(used[i]) continue;
            if(i>0 &&nums[i-1]==nums[i] && !used[i-1]) continue;
            used[i]=true;
            list.add(nums[i]);
            dfs(nums,used,list,res);
            used[i]=false;
            list.remove(list.size()-1);
        }
    }
}

```



#### What is the swap version of permutations II?



## Combinations Sum II

The hard part is also on the duplicate part.

### always remember, in the for loop, every index should use the i not the fixed passing value: pos.

wrong version:

```
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> rList = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, 0, target, new ArrayList<Integer>(), rList);
        
        return rList;
    }
    
    private void backtrack(int[] nums, int pos, int remain, List<Integer> tList, List<List<Integer>> rList) {
        if (0 == remain) {
            // done   a(dd tmp into rList
            rList.add(new ArrayList<>(tList));
            return;
        }
        if (0 > remain) {
            return;
        }
        
        for (int i = pos; i < nums.length; i++) {
            tList.add(nums[pos]);
            
            backtrack(nums, pos, remain - nums[pos], tList, rList);
            
            tList.remove(tList.size() - 1);
        }
        
        return;
    }
}
```



```
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> rList = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, 0, target, new ArrayList<Integer>(), rList);
        
        return rList;
    }
    
    private void backtrack(int[] nums, int pos, int remain, List<Integer> tList, List<List<Integer>> rList) {
        if (0 == remain) {
            // done   a(dd tmp into rList
            rList.add(new ArrayList<>(tList));
            return;
        }
        if (0 > remain) {
            return;
        }
        
        for (int i = pos; i < nums.length; i++) {
            if (i > pos && nums[pos] == nums[pos - 1]) continue;
            
            tList.add(nums[pos]);
            
            backtrack(nums, pos + 1, remain - nums[pos], tList, rList);
            
            tList.remove(tList.size() - 1);
        }
        
        return;
    }
}
```

correct one:

```
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> rList = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, 0, target, new ArrayList<Integer>(), rList);
        
        return rList;
    }
    
    private void backtrack(int[] nums, int pos, int remain, List<Integer> tList, List<List<Integer>> rList) {
        if (0 == remain) {
            // done   a(dd tmp into rList
            rList.add(new ArrayList<>(tList));
            return;
        }
        if (0 > remain) {
            return;
        }
        
        for (int i = pos; i < nums.length; i++) {
            //if(i > start && nums[i] == nums[i-1]) continue; // skip duplicates
            if (i > pos && nums[i] == nums[i - 1]) continue;
            
            tList.add(nums[i]);
            
            backtrack(nums, i + 1, remain - nums[i], tList, rList);
            
            tList.remove(tList.size() - 1);
        }
        
        return;
    }
}
```



