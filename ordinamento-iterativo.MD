# Quadratici
> $O(n^2)$

---

### Insertion sort
> A simple and intuitive algorithm that builds the sorted list one element at a time, inserting each new element into its correct position among the already sorted ones. It performs well on **small** or **nearly sorted** arrays.  
> It's in-place and stable, making it a good choice for online sorting and as a base case for more complex algorithms like **Merge Sort** or **Quick Sort** in hybrid implementations.

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
> A basic algorithm that repeatedly steps through the list, **compares adjacent elements**, and **swaps them** if they're in the wrong order. Though easy to implement and understand, it's highly inefficient for large datasets.  
> The optimized variant introduces a flag to detect early termination if no swaps are performed in a pass. Despite this, it remains unsuitable for performance-critical tasks.

| $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| --------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (n)$    | $\Theta (n^2)$     | $O(n^2)$         | ✅                  | ✅                |

```C title:BubbleSort.c fold
void BubbleSort(int A[], int N){
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
> A simple comparison-based algorithm that repeatedly **selects the minimum element** from the unsorted part and **places it at the beginning**. It performs the minimum number of swaps $O(n)$, but its quadratic number of comparisons makes it inefficient on large arrays.  
> It's in-place but not stable, which limits its use in practice.

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
> An efficient generalization of Insertion sort that allows **comparison and exchange of elements far apart**. Although not stable, it's in-place and **works well for medium-sized datasets**.

| $\textbf{Best}$      | $\textbf{Average}$     | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| -------------------- | ---------------------- | ---------------- | ------------------- | ----------------- |
| $\Omega (n \log n)$* | $\Theta (n \log^2 n)$* | $O(n^2)$*        | ✅                  | ❌                |

_*Depends on gap sequence_

> Knuth's Gap Sequence
> The gap sequence proposed by Donald Knuth is defined as:  
> 
> $$h_k = \frac{3^k - 1}{2}$$  
>
> Which gives a sequence like:  
> 
> $$1,\ 4,\ 13,\ 40,\ 121,\ 364,\ \ldots$$  
> 
> $O(n^{3/2})$ in the worst case.

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
> A non-comparison sorting algorithm that works by **counting the occurrences of each unique value**. Ideal for small integer ranges where the maximum value $k$ isn’t drastically larger than the number of elements $n$.  
> It runs in linear time but isn't in-place and consumes $O(k)$ extra space. It’s stable and often used as a subroutine in Radix sort.

| $\textbf{Best}$  | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ |
| ---------------- | ------------------ | ---------------- | ------------------- | ----------------- |
| $\Omega (n + k)$ | $\Theta (n + k)$   | $O(n + k)$       | ❌                  | ✅                |

```C title:CountingSort.c fold
void CountingSort(int A[],int B[],int C[],int N,int k){  
    const int l=0, r=N-1;
    int i;
    
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
> A digit-wise non-comparison sorting algorithm, typically used for sorting integers or strings of fixed length. It **processes elements from the least significant digit** to the most, often using Counting sort as a stable intermediate step.  
> It has linear complexity when the number of digits $k$ is constant or small relative to $n$, but requires extra space and isn’t in-place. Performs **best when input sizes are large** and the keys are bounded.

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

# Linearitmici
> $O(n \log n)$

---

### Bottom-up Merge sort
> An iterative version of Merge Sort that eliminates recursion by progressively **merging adjacent subarrays** of increasing size (1, 2, 4, 8, ...).  
> Like its recursive counterpart, it guarantees $O(n \log n)$ time in all cases, and is stable. However, it requires $O(n)$ extra space and is not in-place. Well-suited for **linked lists** and **external sorting** (e.g. on disk).

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
