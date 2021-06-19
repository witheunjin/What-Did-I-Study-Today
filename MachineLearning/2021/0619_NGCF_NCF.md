# NGCF & NCF
> Written by witheunjin(EunJin Lee)
> 
> Created on June, 19, 2021

## NGCF-PT_ejlee

### data: ratings.csv
+ Format of `ratings.csv`
```
userId,movieId,rating,timestamp
```

+ Format of `ratings.txt`
```
userId movieId1 movieId2 movieId3 ...
```
-----

### Generate an Adjacency Matrix from Data
* **`./run_ngcf.py`**
```python3
46 data_generator = Data(path=data_dir + dataset, batch_size=batch_size) #ratings.csv
47 adj_mtx = data_generator.get_adj_mat()
```
* **`get_adj_mat()`** : Function Location(Path) = `./utils/load_data.py`
```python3
def get_adj_mat(self):
        try:
            t1 = time()
            adj_mat = sp.load_npz(self.path + '/s_adj_mat.npz')
            print('Loaded adjacency-matrix (shape:', adj_mat.shape,') in', time() - t1, 'sec.')

        except Exception:
            print('Creating adjacency-matrix...')
            adj_mat = self.create_adj_mat()
            sp.save_npz(self.path + '/s_adj_mat.npz', adj_mat)
        return adj_mat
```
* **`create_adj_mat`** : Function Location(Path) = `./utils/load_data.py`
```python3
def create_adj_mat(self):
        t1 = time()
        
        adj_mat = sp.dok_matrix((self.n_users + self.n_items, self.n_users + self.n_items), dtype=np.float32)
        adj_mat = adj_mat.tolil()
        R = self.R_train.tolil() # to list of lists

        adj_mat[:self.n_users, self.n_users:] = R
        adj_mat[self.n_users:, :self.n_users] = R.T
        adj_mat = adj_mat.todok()
        print('Complete. Adjacency-matrix created in', adj_mat.shape, time() - t1, 'sec.')

        t2 = time()
```
> ### dok_matrix
> ```python3
> adj_mat = sp.dok_matrix((self.n_users + self.n_items, self.n_users, self.n_items), dtype=np.float32)
> ```
> This means 'Create (self.n_users + self.n_items) x (self.n_users, self.n_items) Matrix with data type float32'.
> 
> For example, `scipy.sparse.dok_matrix((m,n), dytype=numpy.float32)` means 'create m x n matrix with data type float32'.
> 
> So, after the code is runned, there is a matrix with (self.n_users + self.n_items) columns and (self.n_users + self.n_items) rows. 
> 
> **TEST(EXAMPLE) CODE**
> ```python3
> >>> import numpy as np
> >>> from scipy.sparse import dok_matrix
> >>> S = dok_matrix((5,5), dtype=np.float32)
> >>> for i in range(5):
> ...    for j in range(5):
> ...       S[i,j] = 10 * i + j
> ```
> **RESULT**
> ```
> >>> print(S)
>  (0, 1)	1.0
>  (0, 2)	2.0
>  (0, 3)	3.0
>  (0, 4)	4.0
>  (1, 0)	10.0
>  (1, 1)	11.0
>  (1, 2)	12.0
>  (1, 3)	13.0
>  (1, 4)	14.0
>  (2, 0)	20.0
>  (2, 1)	21.0
>  (2, 2)	22.0
>  (2, 3)	23.0
>  (2, 4)	24.0
>  (3, 0)	30.0
>  (3, 1)	31.0
>  (3, 2)	32.0
>  (3, 3)	33.0
>  (3, 4)	34.0
>  (4, 0)	40.0
>  (4, 1)	41.0
>  (4, 2)	42.0
>  (4, 3)	43.0
>  (4, 4)	44.0
> ```
> ### tolil
> ```python3
> adj_mat = adj_mat.tolil()
> ```
> This means 'Make the adjency matrix to list'.
