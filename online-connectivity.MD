## Online connectivity con Quicksort
```C
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

## Online connectivity con Quickunion
```C
#include <stdio.h>
#define N 10000

int main() {
    int i, j, p, q, id[N];
    
    for (i=0; i<N; i++) {
        id[i] = i;
    }
        
    printf("Input pair p q:  ");  
    while (scanf("%d %d", &p, &q) ==2) {
        for (i = p; i!= id[i]; i = id[i]);
        for (j = q; j!= id[j]; j = id[j]);
        
        if (i == j)
            printf("pair %d %d already connected\n", p,q);
        else {
            id[i] = j;
            printf("pair %d %d not yet connected\n", p, q);
        }
        
        printf("Input pair p q:  ");
    }
	
	return 0;
}
```
