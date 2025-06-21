## CppBankManager

| **FR** | **Description**                                                                                        | **Status** |
| :----: | :----------------------------------------------------------------------------------------------------- | :--------: |
|    1   | Create a `Client` class with encapsulated attributes: name, ID, and list of accounts.                  |     🔲     |
|    2   | Create a `Account` class with methods for deposit, withdrawal, and transfer.                           |     🔲     |
|    3   | Implement inheritance with `CheckingAccount` and `SavingsAccount` derived from `Account`.              |     🔲     |
|    4   | Create a `Transaction` class with date, amount, transaction type, and linked account.                  |     🔲     |
|    5   | Associate transactions to accounts using `std::vector`.                                                |     🔲     |
|    6   | Store all clients in a `std::map<int, Client>` indexed by client ID.                                   |     🔲     |
|    7   | Implement custom exceptions (e.g., `InsufficientFundsException`, `InvalidAccountException`).           |     🔲     |
|    8   | Use `enum class TransactionType {Deposit, Withdrawal, Transfer}` to categorize transactions.           |     🔲     |
|    9   | Create `template` functions to search for clients or accounts by ID.                                   |     🔲     |
|   10   | Use `std::sort` with lambda functions to sort transactions by date or amount.                          |     🔲     |
|   11   | Save and load data from files (`clients.txt`, `accounts.txt`, `transactions.txt`).                     |     🔲     |
|   12   | Use `std::shared_ptr<Account>` within `Client` to allow shared accounts.                               |     🔲     |
|   13   | Separate code into `.h` and `.cpp` files, organized into `include/` and `src/` directories.            |     🔲     |
|   14   | Wrap all classes and functions in a `BankSystem` namespace.                                            |     🔲     |
|   15   | Document code using Doxygen-style comments to generate technical documentation.                        |     🔲     |
|   16   | Create a `Makefile` to compile the entire project easily.                                              |     🔲     |
|   17   | Implement reporting features: total balance per client, top accounts ranking, and transaction history. |     🔲     |
|   18   | Create a Command-Line Interface (CLI) to perform operations (login, bank actions, queries, etc.).      |     🔲     |
|   19   | Validate user input and ensure data integrity.                                                         |     🔲     |
|   20   | Allow exporting reports to `.csv` using `fstream`.                                                     |     🔲     |
