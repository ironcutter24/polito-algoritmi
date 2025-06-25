| $\textbf{Algorithm}$      | $\textbf{Best}$      | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ | $\textbf{Notes}$                |
| ------------------------- | -------------------- | ------------------ | ---------------- | ------------------- | ----------------- | ------------------------------- |
| **Quadratic**             |                      |                    |                  |                     |                   |                                 |
| Insertion sort       | $\Omega(n)$          | $Θ(n^2)$           | $O(n^2)$         | ✅                  | ✅                | Great for nearly-sorted data    |
| Exchange / Bubble sort          | $\Omega(n)$          | $Θ(n^2)$           | $O(n^2)$         | ✅                  | ✅                | Easy but slow                   |
| Selection sort       | $\Omega(n^2)$        | $Θ(n^2)$           | $O(n^2)$         | ✅                  | ❌                | Simple but inefficient          |
| Shell sort          | $\Omega(n \log n)^*$ | $Θ(n \log^2 n)^*$  | $O(n^2)^*$       | ✅                  | ❌                | Depends on gap sequence         |
| **Linear**                |                      |                    |                  |                     |                   |                                 |
| Counting sort        | $\Omega(n + k)$      | $Θ(n + k)$         | $O(n + k)$       | ❌                  | ✅                | Only for small integer ranges   |
| Radix sort          | $\Omega(nk)$         | $Θ(nk)$            | $O(nk)$          | ❌                  | ✅                | For fixed-length keys           |
| **Linearithmic**          |                      |                    |                  |                     |                   |                                 |
| Bottom-up Merge sort | $\Omega(n \log n)$   | $Θ(n \log n)$      | $O(n \log n)$    | ❌                  | ✅                | Iterative variant of Merge Sort |

**🔄 In-place**  
Vettore di n dati + locazioni di memoria ausiliarie in numero fisso

**🧱 Stabile**  
Immutato l’ordinamento relativo di dati con ugual valore della chiave  
(L’ordine in uscita di dati con la stessa chiave è lo stesso dell’ordine in ingresso)

> [!TIP]
> - [Sorting algorithms visualization — chrislaux.com](https://www.chrislaux.com/miscsort)

# Quadratici
> $O(n^2)$

---

### Insertion sort
> Un algoritmo semplice e intuitivo che costruisce la lista ordinata un elemento alla volta, inserendo ciascun nuovo elemento nella posizione corretta tra quelli già ordinati. Funziona bene su array **piccoli** o **quasi ordinati**.  
> È in-place e stabile, quindi adatto all’ordinamento online e come caso base in algoritmi più complessi come **Merge Sort** o **Quick Sort** in implementazioni ibride.

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| --------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (n)$    | $\Theta (n^2)$     | $O(n^2)$         | ✅                  | ✅                |

```C title:InsertionSort.c fold
void InsertionSort(int A[], int N) {
	const int l=0, r=N-1;
    int i, j, x;
    
    for (i = l+1; i <= r; i++) {
        x = A[i];
        j = i - 1;
        
        while (j >= l && x < A[j]) {
            A[j+1] = A[j];
            j--;
        }
        
        A[j+1] = x;
    }
}
```

### Exchange / Bubble sort
> Un algoritmo di base che passa ripetutamente attraverso la lista, **confronta gli elementi adiacenti** e **li scambia** se sono nell’ordine sbagliato. Sebbene sia facile da implementare e comprendere, è molto inefficiente su grandi dataset.  
> La variante ottimizzata introduce una flag per interrompere in anticipo se non vengono effettuati scambi in un passaggio. Tuttavia, rimane inadatto per compiti critici in termini di prestazioni.

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| --------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (n)$    | $\Theta (n^2)$     | $O(n^2)$         | ✅                  | ✅                |

```C title:BubbleSort.c fold
void BubbleSort(int A[], int N) {
	const int l=0, r=N-1;
    int i, j;
    int temp;
    
    for (i = l; i < r; i++) {
        for (j = l; j < r - i + l; j++) {
            if (A[j] > A[j+1]) {
                temp = A[j];
                A[j] = A[j+1];
                A[j+1] = temp;
            }
        }
    }
    return;
}
```

```C title:OptBubbleSort.c fold
void OptBubbleSort(int A[], int N) {
	const int l=0, r=N-1;
    int i, j, flag=1;
    int temp;
    
    for (i = l; i < r && flag==1; i++) {
        flag = 0;
        for (j = l; j < r - i + l; j++) {
            if (A[j] > A[j+1]) {
                flag = 1;
                temp = A[j];
                A[j] = A[j+1];
                A[j+1] = temp;
            }
        }
    }
    return;
}
```

### Selection sort
> Un algoritmo semplice basato su confronti che seleziona ripetutamente **l’elemento minimo** dalla parte non ordinata e lo **porta all’inizio**. Esegue il numero minimo di scambi $O(n)$, ma il numero quadratico di confronti lo rende inefficiente su array grandi.  
> È in-place ma non stabile, il che ne limita l’uso pratico.

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| --------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (n^2)$  | $\Theta (n^2)$     | $O(n^2)$         | ✅                  | ❌                |

```C title:SelectionSort.c fold
void SelectionSort(int A[], int N) {  
    const int l=0, r=N-1;
    int i, j, min;
    int temp;
    
    for (i = l; i < r; i++) {
        min = i;
        
        for (j = i+1; j <= r; j++) {
            if (A[j] < A[min])
                min = j;
        }
        
        if (min != i) {
            temp = A[i];
            A[i] = A[min];
            A[min] = temp;
        }
    }
    return;
}
```

### Shell sort
> Una generalizzazione efficiente dell’**Insertion Sort** che permette di **confrontare e scambiare elementi lontani tra loro**. Anche se non è stabile, è in-place e **funziona bene su dataset di medie dimensioni**.

| $\textbf{Best}$      | $\textbf{Average}$     | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| -------------------- | ---------------------- | ---------------- | ------------------- | ----------------- |
| $\Omega (n \log n)$* | $\Theta (n \log^2 n)$* | $O(n^2)$*        | ✅                  | ❌                |

> [!NOTE]
> La sua complessità dipende dalla sequenza di intervalli (gap) usata.  
> La sequenza proposta da Knuth è:  
> $$h_k = \frac{3^k - 1}{2} \quad \quad (1,\ 4,\ 13,\ 40,\ 121,\ 364,\ \ldots)$$  
> Nel caso peggiore, può arrivare a $O(n^{3/2})$.

> [!NOTE]
> $$
\begin{array}{111}
\textbf{Shell} && 1, \ 2, \ 4, \ 8, \ 16 \dots && O(n^2) \\
\textbf{Hibbard} && 1, \ 3, \ 7, \ 15, \ 31 \dots && O(n^{3/2}) \\
\textbf{Pratt} && 1, \ 2, \ 3, \ 4, \ 6, \ 8, \ 9, \ 12 \dots && O(n \log^2{n}) \\
\textbf{Knuth} && 1, \ 4, \ 13, \ 40, \ 121 \dots && O(n^{3/2}) \\
\textbf{Sedgewick} && 1, \ 5, \ 19, \ 41, \ 109, \ 209 \dots && O(n^{4/3})
\end{array}$$

```C title:ShellSort.c fold
void ShellSort(int A[], int N) {
	const int l=0, r=N-1;
    int i, j, x, h=1;
    
    while (h <= N/3)
        h = 3*h+1;  // sequenza di Knuth
    
    while (h >= 1) {
        for (i = l + h; i <= r; i++) {
            j = i;
            x = A[i];
            
            while (j >= l + h  && x < A[j-h]) {
                A[j] = A[j-h];
                j -=h;
            }
            
            A[j] = x;
        }
        h = h/3;
    }
}
```

# Lineari
> $O(n + k)$ / $O(nk)$

---

### Counting sort
> Un algoritmo di ordinamento che **non si basa su confronti**, ma conta il numero di occorrenze di ogni valore unico. È ideale per insiemi di interi **con intervalli piccoli**, dove il valore massimo $k$ non è molto più grande del numero di elementi $n$.  
> Ha complessità lineare, ma **non è in-place** e usa spazio extra $O(k)$. È stabile e spesso usato nel [[#Radix sort]].

| $\textbf{Best}$  | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ---------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (n + k)$ | $\Theta (n + k)$   | $O(n + k)$       | ❌                  | ✅                |

```C title:CountingSort.c fold
void CountingSort(int A[], int B[], int C[], int N, int k) {  
    const int l=0, r=N-1;
    int i;
    
    for (i = 0; i < k; i++)
        C[i] = 0;  // inizializzazione di C
        
    for (i = l; i <= r; i++)
        C[A[i]]++;  // occorrenze semplici
        
    for (i = 1; i < k; i++)
        C[i] += C[i-1];  // occorrenze multiple
        
    for (i = r; i >= l; i--) {  // ordinamento
        B[C[A[i]] - 1] = A[i];
        C[A[i]]--;
    }
    
    for (i = l; i <= r; i++)
        A[i] = B[i];  // ricopiatura risultato
}
```

### Radix sort
> Un algoritmo di ordinamento non basato su confronti che lavora **cifra per cifra**, spesso su interi o stringhe di lunghezza fissa. **Processa le cifre dalla meno significativa alla più significativa**, spesso usando il [[#Counting Sort]] come passo intermedio stabile.  
> Ha complessità lineare quando il numero di cifre $k$ è costante o piccolo rispetto a $n$, ma richiede spazio extra e **non è in-place**. Funziona **molto bene su insiemi grandi** con chiavi limitate.

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| --------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (nk)$   | $\Theta (nk)$      | $O(nk)$          | ❌                  | ✅                |

```C title:RadixSort.c fold
void radixSort(int A[], int B[], int C[], int D[], int n) {  
    int d=1, i;
    int largest = getMax(A, n);  // identificazione del massimo di A
    
    while (largest/10 > 0) {
        d++;  // calcolo del numero di cifre d
        largest /= 10;
    }
    
    for (i = 0; i < d; i++)
        CountingSort(A, B, C, D, n , i);  // d iterazioni di Counting sort
}
```

```C title:CountingSortForRadix.c fold
void CountingSort(int A[], int B[], int C[], int D[], int N, int step) {
    const int l=0, r=N-1;
    int i, weight=1;
	
    for (i = 0; i < step; i++)
	    weight *= 10;  // calcolo di 10^step
		
    for (i = 0; i < 10; i++)
	    C[i] = 0;
		
    for (i = l; i <= r; i++)
	    D[i] = (A[i] / weight) % 10;  // identificazione colonna
		
    for (i = l; i <= r; i++)
	    C[D[i]]++;  // occorrenze semplici
		
    for (i = 1; i < 10; i++)
	    C[i] += C[i - 1];  // occorrenze multiple
		
    for (i = r; i >= l; i--) {  // ordinamento
        B[C[D[i]] - 1] = A[i];
        C[D[i]]--;
    }
	
    for (i = l; i <= r; i++)
	    A[i] = B[i];  // ricopiatura
}
```

# Linearitmici
> $O(n \log n)$

---

### Bottom-up Merge sort
> Una versione **iterativa** del Merge Sort che elimina la ricorsione unendo progressivamente **sotto-array adiacenti** di dimensione crescente (1, 2, 4, 8, ...).  
> Come la sua controparte ricorsiva, garantisce un tempo di esecuzione di $O(n \log n)$ in tutti i casi ed è **stabile**. Tuttavia, richiede **$O(n)$ di spazio extra** e non è in-place. È particolarmente adatto per **linked lists** e **external sorting**.

| $\textbf{Best}$     | $\textbf{Average}$  | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------- | ------------------- | ---------------- | ------------------- | ----------------- |
| $\Omega (n \log n)$ | $\Theta (n \log n)$ | $O(n \log n)$    | ❌                  | ✅                |

```C title:BottomUpMergeSort.c fold
void BottomUpMergeSort(int A[], int B[], int N) {  // B vettore ausiliario  
    const int l=0, r=N-1;
    int i, q, m;
    
    for (m = 1; m <= r - l; m = m + m) {
        for (i = l; i <= r - m; i += m + m) {
	        // identificazione dell’indice iniziale della prossima coppia
	        // di sottovettori contigui e ordinati di dimensione m
            q = i+m-1;
            
            // fusione di coppie di sottovettori ordinati
            Merge(A, B, i, q, r, m);
        }
    }
}
```

```C title:Merge.c fold
void Merge(int A[], int B[], int l, int q, int r, int m) {  
    int i, j, k;
    i = l;
    j = q+1;
    
    for (k = l; k <= r; k++) {
        if (i > q)  // esaurito sottovettore sinistro  
            B[k] = A[j++];
        else if (j > q+m)  // esaurito sottovettore destro  
            B[k] = A[i++];
        else if ((A[i] < A[j]) || (A[i] == A[j]))
            B[k] = A[i++];
        else
	    B[k] = A[j++];
    }
	        
    for ( k = l; k <= r; k++ )
        A[k] = B[k];
        
    return;  
}
```
