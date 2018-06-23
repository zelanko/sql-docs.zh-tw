---
title: 第 3 課： 建立 SQL Server 認證 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 201863a1df64cdc85ef41a55170948dbf4eba419
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136630"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>第 3 課：建立 SQL Server 認證
  在這一課，您將會建立認證以儲存用來存取 Windows Azure 儲存體帳戶的安全性資訊。  
  
 SQL Server 認證是用來儲存連接到 SQL Server 外部資源所需之驗證資訊的物件。 認證會儲存儲存體容器的 URI 路徑以及共用存取簽章金鑰值。 對於資料或記錄檔所使用的每一個儲存體容器，您必須建立名稱符合容器路徑的 SQL Server 認證。  
  
 如需認證的一般資訊，請參閱[認證&#40;Database Engine&#41;](security/authentication-access/credentials-database-engine.md)。  
  
> [!IMPORTANT]  
>  建立 SQL Server 認證，如下所述的需求特有[Windows Azure 中的 SQL Server 資料檔案](databases/sql-server-data-files-in-microsoft-azure.md)功能。 如需在 Azure 儲存體中建立的備份程序的認證資訊，請參閱[第 2 課： 建立 SQL Server 認證](../tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
 若要建立 SQL Server 認證，請依照下列步驟進行：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  在 [物件總管] 中連接到已安裝的 Database Engine 執行個體。  
  
3.  在 [標準] 工具列上，按一下 [新增查詢]。  
  
4.  將下列範例複製並貼入查詢視窗中，並視需要修改。 下列陳述式將會建立 SQL Server 認證來儲存您的儲存體容器的共用存取憑證。  
  
    ```tsql  
  
    USE master  
    CREATE CREDENTIAL credentialname – this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     如需詳細資訊，請參閱[CREATE CREDENTIAL &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) SQL Server 線上叢書 》 中。  
  
5.  若要查看所有可用的認證，可以在查詢視窗中執行下列陳述式：  
  
    ```tsql  
    SELECT * from sys.credentials  
    ```  
  
     如需有關 sys.credentials 的詳細資訊，請參閱[sys.credentials &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) SQL Server 線上叢書 》 中。  
  
 **下一課：**  
  
 [第 4 課： 建立 Windows Azure 儲存體中的資料庫](lesson-3-database-backup-to-url.md)  
  
  
