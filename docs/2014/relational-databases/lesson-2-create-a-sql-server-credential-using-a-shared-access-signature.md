---
title: 第3課：建立 SQL Server 認證 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 808438e544e3beb18b2e2afa9c399b5666277483
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025060"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>第 3 課：建立 SQL Server 認證
  在這一課，您將建立認證，以儲存用來存取 Azure 儲存體帳戶的安全性資訊。  
  
 SQL Server 認證是用來儲存連接到 SQL Server 外部資源所需之驗證資訊的物件。 認證會儲存儲存體容器的 URI 路徑以及共用存取簽章金鑰值。 對於資料或記錄檔所使用的每一個儲存體容器，您必須建立名稱符合容器路徑的 SQL Server 認證。  
  
 如需認證的一般資訊，請參閱[認證 &#40;資料庫引擎&#41;](security/authentication-access/credentials-database-engine.md)。  
  
> [!IMPORTANT]  
>  以下所述建立 SQL Server 認證的需求，僅適用于[Azure 功能中 SQL Server 的資料檔案](databases/sql-server-data-files-in-microsoft-azure.md)。 如需建立在 Azure 儲存體中執行備份程序所需之認證的資訊，請參閱＜ [Lesson 2: Create a SQL Server Credential](../tutorials/lesson-2-create-a-sql-server-credential.md)＞。  
  
 若要建立 SQL Server 認證，請依照下列步驟進行：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  在 [物件總管] 中連接到已安裝的 Database Engine 執行個體。  
  
3.  在 [標準] 工具列上，按一下 [新增查詢]。  
  
4.  將下列範例複製並貼入查詢視窗中，並視需要修改。 下列語句會建立 SQL Server 認證，以儲存儲存體容器的共用存取憑證。  
  
    ```sql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     如需詳細資訊，請參閱 SQL Server 線上叢書中的[&#40;transact-sql&#41;建立認證](/sql/t-sql/statements/create-credential-transact-sql)。  
  
5.  若要查看所有可用的認證，可以在查詢視窗中執行下列陳述式：  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     如需有關 sys.databases 的詳細資訊，請參閱 SQL Server 線上叢書中[&#40;transact-sql&#41;的 sys. 認證](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql)。  
  
 **下一課：**  
  
 [第 4 課：在 Azure 儲存體中建立資料庫](lesson-3-database-backup-to-url.md)  
  
  
