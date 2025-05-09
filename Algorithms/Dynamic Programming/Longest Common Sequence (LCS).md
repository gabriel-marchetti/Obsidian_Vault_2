Problema:
	Uma subsequência é originada de uma string str. A subsequência é gerada retirando 0 ou mais caracteres da string mantendo a ordem relativa entre os termos.
	O problema aqui é encontrar a LCS entre duas strings s1 e s2.

Note que "ABC" possui 8 subsequências.
	"", "A", "B", "C", "AB", "AC", "BC", "ABC" -- Note que podemos gerar $2^n$ subsequências de uma string.

**EXEMPLOS:**
--- start-multi-column: 
```column-settings  
number of columns: 3  
```

```
Input 1 = "ABC"
Input 2 = "ACD"

LCS : "AC"
```

--- end-column ---

```
Input 1 = "AGGTAB"
Input 2 = "GXTXAYB"

LCS : "GTAB"
```
--- end-column ---

```
Input 1 = "ABC"
Input 2 = "CBA"

LCS : "A" OU "B" OU "C"
```

--- end-multi-column
**NAIVA-APPROACH:**
```C++
#include <bits/stdc++.h>
using namespace std;

int __lcs__(string &s1, string &s2, int n, int m)
{
    if(n == 0 || m == 0)
    {
        return 0;
    }

    if( s1[n-1] == s2[m-1] )
    {
        return 1 + __lcs__(s1, s2, n-1, m-1);
    }
    
    return max( __lcs__(s1, s2, n, m-1), __lcs__(s1, s2, n-1, m) );
}

int lcs(string &s1, string &s2)
{
    return __lcs__(s1, s2, s1.size(), s2.size());
}

int main()
{
    string s1 = "AGGTAB";
    string s2 = "GXTXAYB";

    cout << lcs(s1, s2) << endl;
    return 0;
}
```
Note que o seguinte problema sempre fará a chamada de incluir ou não o próximo elemento, portanto, podemos majorar por $O(2^n)$ e complexidade espacial de $O(n)$.

