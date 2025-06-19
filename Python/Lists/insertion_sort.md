Implemente o insertion sort dentro do Python:
?
```python
from utils.init_rand_array import init_rand_array

def insertion_sort(array):
    for i in range(1, len(array)):
        key = array[i]
        j = i - 1
        while j >= 0 and key < array[j]:
            array[j+1] = array[j]
            j -= 1
        array[j+1] = key

def check_correct(gen_array, exp_array):
    if not (len(gen_array) == len(exp_array)):
        return False
    print('Checagem de tamanho correta...')
    for i in range(len(gen_array)):
        if gen_array[i] != exp_array[i]:
            return False

    print('Vetores são iguais...')
    return True

if __name__ == '__main__':
	# 20 é o tamanho do vetor
	# 40 é o intervalo. Isto é, [0..40]
    arr = init_rand_array(20, 40) 
    arr_cp = arr[:]
    print('Initial array:', arr)
    insertion_sort(arr)
    print('Sorted array:', arr)
    print('Status: ', check_correct(arr, sorted(arr_cp)))
```