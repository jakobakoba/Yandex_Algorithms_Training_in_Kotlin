Line 60: Char 22: error: type mismatch: inferred type is Array<(out) IntArray!>! but List<IntArray> was expected
param_1, param_2
- ошибся в input, там был array, а я написал List<IntArray>

WA n = 4  queries =[[0,3],[0,2]] 271/972
следующий query переписывал предыдущий даже если он был 
лучше
- добавил if замена только если arr[query[0]] < query[1]
то есть заменяем только если текущий меньше чем 
новоприбывающий

WA n = 6 queries = [[1,4],[0,2]] 452 / 972
тут мое неоптимальное решение полностью себя дискредитирует
, потому что уже надо выбирать между несколькими
путями. Мое решение - обрабатывай query и иди прямо - больше не работает.

```
нерабочее неоптимальное решение
first thing i notice without queries the road always will be n - 1
            могу наверное каждый раз идти с самого начала но на каждом шаге буду писать самый дальний шаг
            то есть надо создать IntArray
            потом надо каждый раз создать counter
            
            сначала создаю intarray каждый шаг для каждого шага
            то есть сначала for циклом иду по queries
            query меняет intarray
            и внутри сразу начинаю идти с самого начала используя самый дальний шаг
            
class Solution{
    fun shortestDistanceAfterQueries(n: Int, queries: Array<IntArray>): IntArray {
       
        
        val arr = IntArray(n)
        for (i in 0 until n){
            arr[i] = i + 1
        }
        var counter = 0
        val answer = mutableListOf<Int>()
        for (query in queries){
            if(arr[query[0]] < query[1]){
                arr[query[0]] = query[1]    
            }
            var cur = 0
            while(cur != n - 1){
                cur = arr[cur]
                counter += 1
            }
            answer.add(counter)
            counter = 0
        }
        return answer.toIntArray()
    }
}
```