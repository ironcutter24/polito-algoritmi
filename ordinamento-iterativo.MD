# Quadratici\( - $O(n^2)$\)

---

### Insertion sort
> Great for nearly-sorted data

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ---------------------------------- | ------------------------------------- | -------------------- | ------------------- | ----------------- |
| $\Omega (n)$                             | $\Theta (n^2)$                              | $O(n^2)$             | ✅                  | ✅                |

```C title:InsertionSort.c fold
void InsertionSort(int A[], int N) {  
    int i, j, l=0, r=N-1, x;
    
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
> Easy but slow

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- |
| $\Omega (n)$                             | $\Theta (n^2)$                              | $O(n^2)$             | ✅                  | ✅                |                  

```C title:BubbleSort.c fold
void BubbleSort(int A[], int N){  
    int i, j, l=0, r=N-1;
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
    int i, j, l=0, r=N-1, flag=1;
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
> Simple but inefficient

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- |
| $\Omega (n^2)$                           | $\Theta (n^2)$                              | $O(n^2)$             | ✅                  | ❌                |      

```C title:SelectionSort.c fold
void SelectionSort(int A[], int N) {  
    int i, j, l=0, r=N-1, min;
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
> Depends on gap sequence

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- |
| $\Omega (n \log n)$*                     | $\Theta (n \log^2 n)$*                      | $O(n^2)$*            | ✅                  | ❌                |     

```C title:ShellSort.c fold
void ShellSort(int A[], int N) {  
    int i, j, x, l=0, r=N-1, h=1;
    
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

# Lineari<span> - $O(n + k)$ / $O(nk)$</span>

---

### Counting sort
> Only for small integer ranges

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- |
| $\Omega (n + k)$                         | $\Theta (n + k)$                            | $O(n + k)$           | ❌                  | ✅                | 

```C title:CountingSort.c fold
void CountingSort(int A[],int B[],int C[],int N,int k){  
    int i, l=0, r=N-1;
    
    for (i = 0; i < k; i++)
        C[i] = 0;  // inizializzazione di C
        
    for (i = l; i <= r; i++)
        C[A[i]]++;  // occorrenze semplici
        
    for (i = 1; i < k; i++)
        C[i] += C[i-1];  // occorrenze multiple
        
    for (i = r; i >= l; i--) {
        // posizionamento corretto elementi
        B[C[A[i]] - 1] = A[i];
        C[A[i]]--;
    }
    
    for (i = l; i <= r; i++)
        A[i] = B[i];  // ricopiatura risultato
}
```

### Radix sort
> For fixed-length keys

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- |
| $\Omega (nk)$                            | $\Theta (nk)$                               | $O(nk)$              | ❌                  | ✅                |          

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

# Linearitmici<span> - $O(n \log n)$</span>

---

### Bottom-up Merge sort
> Iterative variant of Merge Sort

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- |
| $\Omega (n \log n)$                      | $\Theta (n \log n)$                         | $O(n \log n)$        | ❌                  | ✅                |  

```C title:BottomUpMergeSort.c fold
void BottomUpMergeSort(int A[], int B[], int N) {  // B vettore ausiliario  
    int i, q, m;
    int l=0, r=N-1;  // estremi
    
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
