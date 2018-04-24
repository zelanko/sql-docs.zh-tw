---
title: 使用卸離與附加移動資料庫 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database attaching [SQL Server]
- moving databases [SQL Server]
- database detaching [SQL Server]
- relocating databases [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 6732a431-cdef-4f1e-9262-4ac3b77c275e
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4518130fe722bedbd19d4c5ef653fbc5c1f091e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="move-a-database-using-detach-and-attach-transact-sql"></a>使用卸離與附加移動資料庫 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何將卸離的資料庫移動到另一個位置，再重新附加到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中相同或不同的伺服器執行個體。 不過，建議您使用 ALTER DATABASE 計畫的重新放置程序來移動資料庫，而不要使用卸離和附加。 如需詳細資訊，請參閱 [移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)。  
  
> [!IMPORTANT]  
>  建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-move-a-database-by-using-detach-and-attach"></a>透過使用卸離和附加來移動資料庫  
  
1.  卸離資料庫。 如需詳細資訊，請參閱 [卸離資料庫](../../relational-databases/databases/detach-a-database.md)。  
  
2.  在 Windows 檔案總管或 Windows 的 [命令提示字元] 視窗中，將卸離的資料庫檔案和記錄檔移動到新位置。  
  
    > [!NOTE]  
    >  若要移動單一檔案的資料庫，且檔案小到可以容納在電子郵件中，您可以利用電子郵件來移動。  
  
     即使您想要建立新的記錄檔，也應該一併移動記錄檔。 在某些情況下，重新附加資料庫需要其現有的記錄檔。 因此，一律保留所有卸離的記錄檔，直到資料庫在沒有這些檔案的情形下成功附加為止。  
  
    > [!NOTE]  
    >  如果您嘗試在不指定記錄檔的情形下附加資料庫，附加作業會在其原始位置中尋找記錄檔。 如果原始位置中仍有記錄的副本存在，則會附加該副本。 若要避免使用原始記錄檔，請指定新記錄檔的路徑，或者移除記錄檔的原始副本 (在將記錄檔複製到新位置後)。  
  
3.  附加複製的檔案。 如需相關資訊，請參閱 [Attach a Database](../../relational-databases/databases/attach-a-database.md)。  
  
## <a name="example"></a>範例  
 下列範例可為 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫建立名為 `MyAdventureWorks`的副本。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會在 [查詢編輯器] 視窗中執行，此視窗連接到附加的伺服器執行個體。  
  
1.  執行下列 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 陳述式卸離 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料庫：  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'AdventureWorks2012';  
    GO  
    ```  
  
2.  使用您選擇的方法，將資料庫檔案 (AdventureWorks208R2_Data.mdf 和 AdventureWorks208R2_log) 分別複製到：C:\MySQLServer\AdventureWorks208R2_Data.mdf 和 C:\MySQLServer\AdventureWorks208R2_Log.ldf。  
  
    > [!IMPORTANT]  
    >  針對實際執行的資料庫，將資料庫與交易記錄放在不同的磁碟上。  
  
     若要經由網路將檔案複製到遠端電腦的磁碟，請使用遠端位置的通用命名慣例 (UNC) 名稱。 UNC 名稱的格式為 **\\\\***Servername***\\***Sharename***\\***Path***\\***Filename*。 如同將檔案寫入本機硬碟一樣，您必須將在遠端磁碟讀取或寫入檔案所需的適當權限，授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體所用的使用者帳戶。  
  
3.  若要附加已移動的資料庫和記錄檔 (選擇性)，請執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Data.mdf'),  
        (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Log.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，新附加的資料庫無法立即在 [物件總管] 中可見。 若要檢視資料庫，請在 [物件總管] 中按一下 **[檢視]** ，然後按一下 **[重新整理]**。 在 [物件總管] 中展開 **[資料庫]** 節點時，剛才附加的資料庫就會出現在資料庫清單中。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
