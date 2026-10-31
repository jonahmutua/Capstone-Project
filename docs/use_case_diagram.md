# Use case diagram



```mermaid
flowchart LR
  cashier["Cashier"]
  clerk["Stock Clerk"]
  manager["Manager"]
  admin["Admin"]
  scheduler["Scheduler<br/>(system actor)"]

  subgraph system["Inventory system"]
    direction TB
    recordSale(["Record sale"])
    manageCatalog(["Manage catalog"])
    manageSuppliers(["Manage suppliers"])
    createPurchase(["Create purchase"])
    receivePurchase(["Receive purchase"])
    viewRecs(["View recommendations"])
    acceptRecs(["Accept or dismiss"])
    runEngine(["Run restock engine"])
    viewReports(["View reports"])
    manageUsers(["Manage users"])
  end

  cashier --- recordSale

  clerk --- manageCatalog
  clerk --- createPurchase
  clerk --- receivePurchase
  clerk --- viewRecs

  manager --- recordSale & manageCatalog & manageSuppliers & createPurchase & receivePurchase
  manager --- viewRecs & acceptRecs & runEngine & viewReports

  admin --- manageUsers
  admin -.->|"inherits all Manager use cases"| manager

  scheduler --- runEngine

  classDef actor fill:#F1EFE8,stroke:#5F5E5A,color:#2C2C2A
  classDef usecase fill:#EEEDFE,stroke:#534AB7,color:#26215C
  classDef restock fill:#E1F5EE,stroke:#0F6E56,color:#085041
  class cashier,clerk,manager,admin,scheduler actor
  class recordSale,manageCatalog,manageSuppliers,createPurchase,receivePurchase,viewReports,manageUsers usecase
  class viewRecs,acceptRecs,runEngine restock
```

## Who can do what

| Use case | Actors |
|---|---|
| Record sale | Cashier, Manager, Admin |
| Manage catalog | Stock Clerk, Manager, Admin |
| Manage suppliers | Manager, Admin |
| Create purchase | Stock Clerk, Manager, Admin |
| Receive purchase | Stock Clerk, Manager, Admin |
| View recommendations | Stock Clerk (view only), Manager, Admin |
| Accept or dismiss | Manager, Admin |
| Run restock engine | Scheduler, Manager, Admin |
| View reports | Manager, Admin |
| Manage users | Admin |
