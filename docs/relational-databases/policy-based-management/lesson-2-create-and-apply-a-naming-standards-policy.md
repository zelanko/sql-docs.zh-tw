---
title: 第 2 課：建立與套用命名標準原則
description: 此教學課程說明如何在 SQL Server 中建立和套用原則式管理的命名標準原則。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 86014f1a4c7ee4f9c002df67d2f739124dc70e2a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785082"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>第 2 課：建立和套用命名標準原則
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
某些以原則為基礎的管理原則類型可以建立觸發程序，以便強制執行原則的未來合規性。 在這一課，您會建立針對資料表強制執行命名標準的原則。 然後，您會透過嘗試建立違反此原則的資料表，測試此原則。  


## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio 和執行 SQL Server 的伺服器存取權。

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
  
## <a name="create-the-finance-database"></a>建立 Finance 資料庫  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，開啟查詢視窗並執行下列陳述式：  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  在物件總管中，按一下 [資料庫]  ，然後按下 F5 重新整理資料庫的清單。  

## <a name="create-the-finance-tables-condition"></a>建立 Finance 資料表條件 

1.  在物件總管中，依序展開 [管理]  和 [原則管理]  ，以滑鼠右鍵按一下 [條件]  ，然後按一下 [新增條件]  。 

   ![新增條件](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  在 [建立新條件]  對話方塊的 [名稱]  方塊中，輸入 **Finance Tables**。  
    1. 在 [Facet]  清單中，選取 [多部分名稱]  。 
    1. 在 [運算式]  區域的 [欄位]  方塊中，選取 **\@名稱**；在 [運算子]  方塊中，選取 [Like]  ；然後在 [值]  方塊中，輸入 ```'fintbl%'```，強制所有資料表名稱都以字母 **fintbl** 為開頭。
    1. 在 [描述]  頁面上，輸入**財務資料表名稱的開頭必須是 fintbl**，然後按一下 [確定]  建立條件。  

    ![Finance 資料表條件](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>建立 Finance 名稱原則  
  
1.  在物件總管中，以滑鼠右鍵按一下 [原則]  ，然後按一下 [新增原則]  。  

   ![新增原則](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  在 [建立新原則]  對話方塊的 [名稱]  方塊中，輸入 **Finance Name**。
    1. 在 [檢查條件]  清單中，選取 [Finance Tables]  。 這會位於 [多部分名稱]  區域中。 
    1. 在 [針對]  區域中，您將會看見可套用此原則的資料庫物件清單。 選取 [每份資料表]  的核取方塊。
    1. 選取 [已啟用]  清單 ([已啟用]  方塊不會套用至 [視需要]  原則)。
    1. 在 [評估模式]  清單中，選取 [變更時: 避免]  。 這樣就會透過在 Finance 資料庫上建立資料庫觸發程序，強制執行此原則。 
    1. 在 [伺服器限制]  清單中，選取 [無]  。 
    1. 在 [描述]  頁面上，新增這項描述：'Table names in the Finance database must contain 'fintbl%'.' 
    1. 返回 [一般]  頁面，接著在 [每個資料庫]  區域中，展開 [全部]  ，然後按一下 [新增條件]  。

    ![建立新的 Finance 名稱原則](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  在 [建立新條件]  對話方塊的 [名稱]  方塊中，輸入 **Finance Database**。
    1. 在 [運算式]  方塊中，完成要包含 @Name = 'Finance' 的運算式，然後按一下 [確定]  關閉條件頁面。 
  
    ![建立新的 'finance database' 條件](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > 您可能必須按下 TAB 鍵跳離 [值]  方塊，才能啟用 [確定]  按鈕。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>建立 Finance 原則類別目錄  
  
1.  在物件總管中，展開 [管理]  ，以滑鼠右鍵按一下 [原則管理]  ，然後按一下 [管理類別目錄]  。  

   ![管理類別目錄](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  在 [管理原則類別目錄]  對話方塊之 [名稱]  下的空白方塊中，輸入 **Finance**，然後清除 [託管資料庫訂閱]  。 [託管資料庫訂閱]  將會強制執行個體中的每一個資料庫訂閱屬於這個原則類別目錄的原則。 基於這個理由，只有 Finance 資料庫應該訂閱 Finance Name 原則。  

    ![管理原則類別目錄](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>訂閱 Finance 原則類別目錄  
  
1.  在物件總管中，展開 [資料庫]  、以滑鼠右鍵按一下 **Finance**、指向 [原則]  ，然後按一下 [類別目錄]  。 

   ![Finance 原則類別目錄](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  針對 **Finance** 類別目錄，選取 [已訂閱]  核取方塊。  

   ![已訂閱 finance 原則](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>測試 Finance 名稱原則的強制執行  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，開啟查詢視窗。 執行下列陳述式，以便嘗試建立違反 **Finance Name** 原則的資料表。 此資料表違反了原則，因為資料表名稱並未以字母 **fintbl**為開頭。  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    請注意，這個原則會讓您無法建立資料表，並且傳回提供原則名稱的參考用訊息。 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  若要提供有效的名稱，請依照下列內容修改程式碼並再次執行陳述式。  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    這次就會建立資料表。  
  
## <a name="apply-the-policy-to-the-whole-server"></a>將原則套用至整個伺服器  
  
1.  目前，只有 Finance 資料庫訂閱 Finance 原則類別目錄。 在許多情況下，將原則類別目錄套用至整個伺服器是比較簡單的方式。 在物件總管中，展開 [管理]  ，以滑鼠右鍵按一下 [原則管理]  ，然後按一下 [管理類別目錄]  。  
  
2.  在 [管理原則類別目錄]  對話方塊中，找出 Finance 類別目錄，然後針對 Finance 類別目錄選取 [託管資料庫訂閱]  核取方塊。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 此時，Finance 類別目錄會套用至所有資料庫，但是您已建立的條件會將 Finance Name 原則限制為 Finance 資料庫。 這點就說明了如何以將在許多伺服器上正確套用的方式，使用複雜的條件組合來建立原則的目標。  
  
## <a name="summary"></a>摘要  
這個教學課程已經示範了如何建立以原則為基礎的管理條件、原則和原則群組，以及如何套用篩選和檢查以原則為基礎的管理目標是否符合。  
  
## <a name="next"></a>下一頁  
本教學課程已完成。 若要返回起始處，請瀏覽[教學課程：使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md)。  
  
如需教學課程清單，請參閱 [適用於 SQL Server 2016 的教學課程](../../sql-server/tutorials-for-sql-server-2016.md)。  
  
## <a name="see-also"></a>另請參閱  
[使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
