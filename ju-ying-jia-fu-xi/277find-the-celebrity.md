总结下

two pass,  O\(n\) & O\(1\)

Fiirst pass to find the candidate

for this candidate 0, 

if he don't know anybody, he may be the Celebrity.

if he know somebody, that buddy may be the Celebrity. 



Second pass:

Check if this candidate is the Celebrity.

if anyone doesn't know him \|\| he know some one,

we can say he's not

else 

he is.



```
public class Solution extends Relation {
    public int findCelebrity(int n) {
        int candidate = 0;
        // find the candidate
        for (int i = 0; i < n; i++) {
            if (knows(candidate, i)) {
                candidate = i;
            }
        }
        
        for (int i = 0; i < n; i++) {
            if (i != candidate && (knows(candidate, i) || !knows(i, candidate))) {
                return -1;
            }
        }
        
        return candidate;
    }
}
```



