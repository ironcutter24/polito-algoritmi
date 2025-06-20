| $\textbf{Algorithm}$     | $\textbf{Best}$ | $\textbf{Average}$ | $\textbf{Worst}$ | $\textbf{In-place}$ | $\textbf{Stable}$ | $\textbf{Notes}$                |
| ------------------------ | ---------------------------------- | ------------------------------------- | -------------------- | ------------------- | ----------------- | ------------------------------- |
| **Quadratic**        |                                    |                                       |                      |                     |                   |                                 |
| **Insertion Sort**       | $\Omega(n)$                             | $Θ(n^2)$                              | $O(n^2)$             | ✅                  | ✅                | Great for nearly-sorted data    |
| **Bubble Sort**          | $\Omega(n)$                             | $Θ(n^2)$                              | $O(n^2)$             | ✅                  | ✅                | Easy but slow                   |
| **Selection Sort**       | $\Omega(n^2)$                           | $Θ(n^2)$                              | $O(n^2)$             | ✅                  | ❌                | Simple but inefficient          |
| **Shell Sort**           | $\Omega(n \log n)$*                     | $Θ(n \log^2 n)$*                      | $O(n^2)$*            | ✅                  | ❌                | Depends on gap sequence         |
| **Linear**           |                                    |                                       |                      |                     |                   |                                 |
| **Counting Sort**        | $\Omega(n + k)$                         | $Θ(n + k)$                            | $O(n + k)$           | ❌                  | ✅                | Only for small integer ranges   |
| **Radix Sort**           | $\Omega(nk)$                            | $Θ(nk)$                               | $O(nk)$              | ❌                  | ✅                | For fixed-length keys           |
| **Linearithmic**     |                                    |                                       |                      |                     |                   |                                 |
| **Bottom-Up Merge Sort** | $\Omega(n \log n)$                      | $Θ(n \log n)$                         | $O(n \log n)$        | ❌                  | ✅                | Iterative variant of Merge Sort |
| ~~**Merge Sort**~~           | $\Omega(n \log n)$                      | $Θ(n \log n)$                         | $O(n \log n)$        | ❌                  | ✅                | Divide & conquer                |
| ~~**Quick Sort**~~           | $\Omega(n \log n)$                      | $Θ(n \log n)$                         | $O(n^2)$             | ✅                  | ❌                | Fast but unstable               |
| ~~**Heap Sort**~~            | $\Omega(n \log n)$                      | $Θ(n \log n)$                         | $O(n \log n)$        | ✅                  | ❌                | Always `O(n log n)`             |


**Ordinamento in loco:** vettore di n dati + locazioni di memoria ausiliarie in numero fisso
**Ordinamento stabile:** immutato l’ordinamento relativo di dati con ugual valore della chiave (l’ordine in uscita di dati con la stessa chiave è lo stesso dell’ordine in ingresso)

## Tipologie di problemi
- Decisione (ammettono una risposta sì/no)
- Verifica (data una soluzione, appurare che è davvero tale)
- Ottimizzazione (se esiste, quale è la soluzione migliore?)

## Classi di complessità
- $P \quad$(Polinoniale)
	- Operando su n dati, termina in un numero di passi limitato superiormente da $n^2$
- $NP \quad$(Non-deterministico Polinomiale)
	- Conosciamo algoritmi di soluzione esponenziali, ma non conosciamo algoritmi polinomiali, non possiamo però escludere che esistano
	- $P \subseteq NP$, ma non è noto se $P$ è un sottoinsieme proprio di $NP$ o se al limite coincide con esso
- $NP-C \quad$(NP-Completo)
	- E' $NP$ e ogni altro problema in NP è riducibile ad esso attraverso una trasformazione polinomiale
	- Se un problema $NP-C$ fosse risolvibile con un algoritmo polinomiale, si troverebbero algoritmi polinomiali per tutti i problemi $NP$
	- Rende probabile che $P \subset NP$ e non $P = NP$
- $NP-H \quad$(NP-Hard)
	- Ogni problema in $NP$ è riducibile ad esso in tempo polinomiale (anche se non appartiene ad $NP$)

## Classificazione degli algoritmi
- $1 \to$ costante
	- Numero di operazioni costante
- $log(n) \to$ logaritmico
	- Tipico di algoritmi che dimezzano il problema a ogni passo
		- e.g. Ricerce binaria
- $n \to$ lineare
	- Applicabili solo con ipotesi restrittive sui dati, basati sul calcolo
		- Counting sort, Radix sort, Bin/Bucket sort
- $n \cdot log(n) \to$ linearitmico
	- Tipico di divide-et-impera applicato su tutti gli elementi
		- e.g. Merge sort, Quick sort, Heap sort, Bottom-up Merge Sort (iterativo)
- $n^2 \to$ quadratico
	- Semplici, iterativi, basati sul confronto
		- e.g. Insertion sort, Selection sort, Exchange/Bubble sort
- $n^3 \to$ cubico
- $2^n \to$ esponenziale
