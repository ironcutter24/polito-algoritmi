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


## 🧠 Strategie risolutive

- **Basato sul confronto**  
  L’algoritmo ordina gli elementi effettuando confronti binari tra di essi (es. `a < b`).  
  **Esempi**: Quick Sort, Merge Sort, Heap Sort, Bubble Sort  
  > ❗ **Limite inferiore teorico**: $\Omega (n \log{n})$

- **Non basato sul confronto**  
  L’algoritmo sfrutta proprietà specifiche degli input, come il fatto che siano interi in un intervallo noto.  
  **Esempi**: Counting Sort, Radix Sort, Bucket Sort  
  >  ✅ **Può essere più veloce di** $O(n \log{n})$ **in casi particolari**
