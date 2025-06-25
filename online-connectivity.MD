### Online connectivity con Quick-Find
> Implementazione base dell'algoritmo di _Union-Find_ usando un array di ID. Ogni elemento ha un identificativo univoco, e due elementi sono nello stesso componente se condividono lo stesso ID.  
> Ogni unione richiede l'**aggiornamento di tutti gli ID** degli elementi del componente, rendendo l'approccio semplice ma inefficiente per insiemi grandi.

> [!TIP]  
> Ogni coppia richiede $2$ `find`, ciascuno in $\Theta(1)$: costo totale $\Theta(d)$.  
> Ogni `union` aggiorna fino a $N$ elementi: costo totale $\Theta(dN)$.  
> Complessità complessiva: $\Theta(d + dN) = \Theta(dN)$ per $N \to \infty$.

| $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{Representation}$ |
| ------------------ | ---------------- | ------------------------- |
| $\Theta(dN)$       | $O(dN)$          | Flat array                |

```C title:OnlineConnectivityQuicksort.c fold
#include <stdio.h>
#define N 10000

int main() {
    int i, t, p, q, id[N];
    
    for (i = 0; i < N; i++)
        id[i] = i;
		
    printf("Input pair p q: ");
    while (scanf("%d %d", &p, &q) == 2) {
        if (id[p] == id[q]) {
            printf("%d %d already connected\n", p, q);
        } else {
            for (t = id[p], i = 0; i < N; i++) {
                if (id[i] == t)
                    id[i] = id[q];
            }
            printf("pair %d %d not yet connected\n", p, q);
        }
        printf("Input pair p q: ");
    }
	
    return 0;
}
```

### Online connectivity con Quickunion
> Variante ottimizzata di _Union-Find_ che rappresenta ciascun insieme come un albero: ogni nodo punta al proprio genitore, e la radice è l'identificatore del componente.  
> Le unioni sono più efficienti rispetto a Quick-Find, ma senza ottimizzazioni possono generare alberi profondi, rallentando le operazioni di `find`.

> [!TIP]  
> Ogni `find` attraversa una catena di lunghezza fino a $O(N)$, quindi $2d \cdot O(N) = O(dN)$.  
> Ogni `union` ha costo $O(1)$ perché collega due radici.  
> Complessità complessiva: $O(dN)$ nel caso peggiore.

| $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{Representation}$ |
| ------------------ | ---------------- | ------------------------- |
| $\Theta(dN)$       | $O(dN)$          | Trees                     |

```C title:OnlineConnectivityQuickunion fold
#include <stdio.h>
#define N 10000

int main() {
    int i, j, p, q, id[N];
    
    for (i=0; i<N; i++) {
        id[i] = i;
    }
        
    printf("Input pair p q:  ");  
    while (scanf("%d %d", &p, &q) == 2) {
        for (i = p; i != id[i]; i = id[i]);
        for (j = q; j != id[j]; j = id[j]);
        
        if (i == j) {
            printf("pair %d %d already connected\n", p, q);
        }
        else {
            id[i] = j;
            printf("pair %d %d not yet connected\n", p, q);
        }
        
        printf("Input pair p q:  ");
    }
	
	return 0;
}
```
