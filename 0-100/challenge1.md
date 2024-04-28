# 1. Reconstruction de la file d'attente par Taille
## Description du problème

Supposez qu'un groupe de personnes soit disposé dans une file d'attente de manière désordonnée. L'array `people` représente certains attributs des personnes dans la file d'attente (pas nécessairement dans l'ordre). Chaque `people[i] = [h_i, k_i]` où `h_i` est la taille de la personne `i` et `k_i` est le nombre exact de personnes devant cette personne qui sont de taille égale ou plus grande que `h_i`.

Vous devez reconstruire et retourner la file d'attente représentée par l'array `people`. La file d'attente reconstruite doit être formatée en tant qu'array `queue`, où `queue[j] = [h_j, k_j]` représente les attributs de la personne `j` dans la file d'attente (avec `queue[0]` étant la personne en avant de la file).

## Solutions proposées

### Méthode en Python
```python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        people.sort(key=lambda x: (-x[0], x[1]))
        ans = []
        for p in people:
            ans.insert(p[1], p)
        return ans
```

### Méthode en Java
```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (a, b) -> a[0] == b[0] ? a[1] - b[1] : b[0] - a[0]);
        List<int[]> ans = new ArrayList<>(people.length);
        for (int[] p : people) {
            ans.add(p[1], p);
        }
        return ans.toArray(new int[ans.size()][]);
    }
}
```

### Méthode en C++
```cpp
class Solution {
public:
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(), people.end(), [](const vector<int>& a, const vector<int>& b) {
            return a[0] > b[0] || (a[0] == b[0] && a[1] < b[1]);
        });
        vector<vector<int>> ans;
        for (const vector<int>& p : people)
            ans.insert(ans.begin() + p[1], p);
        return ans;
    }
};
```

### Méthode en Go
```go
func reconstructQueue(people [][]int) [][]int {
    sort.Slice(people, func(i, j int) bool {
        a, b := people[i], people[j]
        return a[0] > b[0] || a[0] == b[0] && a[1] < b[1]
    })
    var ans [][]int
    for _, p := range people {
        i := p[1]
        ans = append(ans[:i], append([][]int{p}, ans[i:]...)...)
    }
    return ans
}
```
