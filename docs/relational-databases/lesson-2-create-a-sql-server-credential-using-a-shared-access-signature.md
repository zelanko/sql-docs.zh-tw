---
title: "第 2 課︰使用共用存取簽章建立 SQL Server 認證 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 17
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 17
---
# 第 2 課︰使用共用存取簽章建立 SQL Server 認證
在本課程中，您將建立用來儲存安全性資訊的認證，這些資訊可供 SQL Server 用來寫入及讀取您在[第 1 課︰在 Azure 容器上建立預存存取原則和共用存取簽章](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)所建立之 Azure 容器中的內容。  
  
SQL Server 認證是用來儲存連接到 SQL Server 外部資源所需之驗證資訊的物件。 認證會儲存儲存體容器的 URI 路徑，以及該容器的共用存取簽章金鑰值。  
  
> [!NOTE]  
> 如果您想要將 SQL Server 2012 SP1 CU2 或更新版本的資料庫或 SQL Server 2014 資料庫備份至此 Azure 容器，您可以使用這裡所記載之[已被取代的語法](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx)，依據儲存體帳戶金鑰建立 SQL Server 認證。  
  
## 建立 SQL Server 認證  
若要建立 SQL Server 認證，請依照下列步驟進行：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到內部部署環境中資料引擎的 SQL Server 2016 執行個體。  
  
3.  在新的查詢視窗中，貼上第 1 課的共用存取簽章及 CREATE CREDENTIAL 陳述式，然後執行該指令碼。  
  
    指令碼看起來類似下列程式碼。  
  
    ```Transact-SQL  
  
    USE master  
    CREATE CREDENTIAL 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>' – this name must match the container path, start with https and must not contain a forward slash.  
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 1.   
    GO  
  
    ```  
  
4.  若要查看所有可用的認證，您可以在已連接到執行個體的查詢視窗中執行下列陳述式：  
  
    ```Transact-SQL  
    SELECT * from sys.credentials  
    ```  
  
5.  開啟新的查詢視窗，並連接到 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體。  
  
6.  在新的查詢視窗中，貼上第 1 課的共用存取簽章及 CREATE CREDENTIAL 陳述式，然後執行該指令碼。  
  
7.  如果您想要讓任何其他 SQL Server 2016 執行個體擁有 Azure 容器的存取權，請重複步驟 5 和 6。  
  
**下一課：**  
  
[第 3 課：資料庫備份至 URL](../relational-databases/lesson-3-database-backup-to-url.md)  
  
## 另請參閱  
[認證 &#40;Database Engine&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
