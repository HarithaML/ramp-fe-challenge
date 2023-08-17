
Please refer to this documentation for the edits i have done to the code

1. Bug-1 Changes
    In index.css 

    ```CSS
    .RampInputSelect--dropdown-container {
    
        /* position: fixed; */
       
       
        }
    ```
2. Bug-2 Changes

in component input checkbox (index.tsx)

   refer to the inputid 

   ```
   <label
    htmlFor={inputId}
   />
   <input
   name={inputId}
   />
   ```

   or

   put input tag inside label tag

3. Bug-3 changes

in  app.tsx 

in inputSelect component add 

```

 newValue.id ? await loadTransactionsByEmployee(newValue.id) : await loadAllTransactions()
```

if there is a selection load all the transactions by the employee or else load all the transactions

4. Bug-4 changes

IN hooks and usePaginatedTransactions

Initial transactions plus new transactions are returned 

```
return { data: [...previousResponse.data, ...response.data], nextPage: response.nextPage }
```

5. Bug-5 changes

In app.tsx

```

const loadAllTransactions = useCallback(async () => {
    // setIsLoading(true) Bug 5 
    transactionsByEmployeeUtils.invalidateData()

    await employeeUtils.fetchAll()
    await paginatedTransactionsUtils.fetchAll()

    // setIsLoading(false) Bug 5 
  }, [employeeUtils, paginatedTransactionsUtils, transactionsByEmployeeUtils])
```

6. Bug-6  changes

In app.tsx
View more button disappears if we reach end of data or if its filtered by employee
```
 {transactions !== null && paginatedTransactions?.nextPage && (
            <button
              className="RampButton"
              disabled={paginatedTransactionsUtils.loading}
              onClick={async () => {
                await loadAllTransactions()
              }}
            >
              View More
            </button>
          )}
```
7. Bug-7 changes
   transaction approval persists until cache is cleared from endpoint
   in transactions index.tsx use
    ```
   clearCacheByEndpoint()
  ```