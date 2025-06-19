Nesse exercício você possui uma lista com nomes duplicados e deve fornecer uma lista com os nomes sem que haja a ocorrência de duplicatas, além disso o vetor gerado deve ser estável, portanto, deve manter a ordem de ocorrência da primeira aparição do nome.
?
```python
import random 

names_list = ['Ana', 
              'Bruno',
              'Claudia',
              'Daniel',
              'Eduardo',
              'Gabriel',
              'Fábio']

'''
    Generate a list with duplicates
'''
def dup_gen(name_list):
    res = []
    size = 2 * len(name_list) + 1 
    for _ in range(size):
        # Does a hard copy of name in names_lists
        res.append(name_list[random.randint(0, len(name_list) - 1)][:])

    return res

def remove_duplicates(name_list):
    no_dup_name_list = []
    for name in name_list:
        if name not in no_dup_name_list:
            no_dup_name_list.append(name)

    return no_dup_name_list


if __name__ == '__main__':
    name_list = dup_gen(names_list)
    print('..'.join(name_list))
    print('..'.join(remove_duplicates(name_list)))

```