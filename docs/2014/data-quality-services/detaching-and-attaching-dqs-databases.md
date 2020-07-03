---
title: 卸離和附加 DQS 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e83f8c2f75725c5de0dc7fa6e3e78666568fad8f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85886012"
---
# <a name="detaching-and-attaching-dqs-databases"></a>卸離和附加 DQS 資料庫
  本主題描述如何卸離和附加 DQS 資料庫。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Limitations"></a> 限制事項  
 如需限制事項的清單，請參閱 [資料庫卸離與附加 &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md)中卸離資料庫。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   請確定 DQS 中沒有任何執行中的活動或處理序。 這可以使用 **[活動監控]** 畫面加以確認。 如需有關在此畫面工作的詳細資訊，請參閱＜ [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md)＞。  
  
-   確定沒有任何使用者登入 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
-   您的 Windows 使用者帳戶必須是 SQL Server 執行個體之 db_owner 固定伺服器角色的成員，才能卸離 DQS 資料庫。  
  
-   您的 Windows 使用者帳戶必須擁有 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 權限，才能附加資料庫。  
  
-   您必須擁有 DQS_MAIN 資料庫的 dqs_administrator 角色，才能在 DQS 中終止任何執行中的活動或停止任何執行中的處理序。  
  
##  <a name="detach-dqs-databases"></a><a name="Detach"></a>卸離 DQS 資料庫  
 當您使用 SQL Server Management Studio 卸離 DQS 資料庫時，卸離的檔案仍會保留在您的電腦上，可供您將其重新附加至相同的 SQL Server 執行個體，或是移到另一部伺服器並附加至該處。 DQS 資料庫檔案通常位於 Data Quality Services 電腦上的下列位置： C:\Program Files\Microsoft SQL Server\MSSQL12。*<Instance_Name>* \mssql\data。  
  
1.  啟動 Microsoft SQL Server Management Studio，並連接到適當的 SQL Server 執行個體。  
  
2.  在 [物件總管] 中，展開 **[資料庫]** 節點。  
  
3.  以滑鼠右鍵按一下 **[DQS_MAIN]** 資料庫，並指向 **[工作]**，然後按一下 **[卸離]**。 **[卸離資料庫]** 對話方塊隨即出現。  
  
4.  選取 **[卸除]** 資料行底下的核取方塊，然後按一下 **[確定]** 以卸離 DQS_MAIN 資料庫。  
  
5.  針對 DQS_PROJECTS 及 DQS_STAGING_DATA 資料庫重複步驟 3 和 4 予以卸離。  
  
 您也可以使用 Transact-SQL 陳述式，透過 sp_detach_db 預存程序卸離 DQS 資料庫。 如需有關使用 Transact-SQL 陳述式卸離資料庫的詳細資訊，請參閱＜ [Using Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) ＞中的＜ [Detach a Database](../relational-databases/databases/detach-a-database.md)＞。  
  
##  <a name="attach-dqs-databases"></a><a name="Attach"></a>附加 DQS 資料庫  
 請使用下列指示，將 DQS 資料庫附加至相同的 SQL Server 執行個體 (原本卸離之處) 或是 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 安裝所在的另一個 SQL Server 執行個體。  
  
1.  啟動 Microsoft SQL Server Management Studio，並連接到適當的 SQL Server 執行個體。  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下 **[資料庫]**，然後按一下 **[附加]**。 **[附加資料庫]** 對話方塊隨即出現。  
  
3.  若要指定欲附加的資料庫，請按一下 **[加入]**。 **[尋找資料庫檔案]** 對話方塊隨即出現。  
  
4.  選取資料庫所在的磁碟機、展開目錄樹狀結構，尋找並選取資料庫的 .mdf 檔案。 以 DQS_MAIN 資料庫為例：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  **[資料庫詳細資料]** (下方) 窗格會顯示要附加之檔案的名稱。 若要確認或變更檔案的路徑名稱，請按一下 [瀏覽]  按鈕 ( ... )。  
  
6.  按一下 **[確定]** 以附加 DQS_MAIN 資料庫。  
  
7.  針對 DQS_PROJECTS 及 DQS_STAGING_DATA 資料庫重複步驟 2-6 予以附加。  
  
8.  在您還原 DQS_MAIN 資料庫之後，還必須執行下一個步驟中的 Transact-SQL 陳述式，否則當您嘗試使用 Data Quality Client 應用程式連接到資料品質伺服器時，將會因為無法連接而出現錯誤訊息。 但是，如果您只附加了 DQS_PROJECTS 或 DQS_STAGING_DATA 資料庫而非 DQS_MAIN，便不需要執行步驟 9 和 10。  
  
     若要執行 Transact-SQL 陳述式，請在 [物件總管] 中以滑鼠右鍵按一下伺服器，然後按一下 **[新增查詢]**。  
  
9. 在 [查詢編輯器] 視窗中，複製下列 SQL 陳述式：  
  
    ```sql  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##]  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##]  
    ```  
  
10. 按 F5 執行陳述式。 檢查 [結果] 窗格，確認陳述式是否皆已成功地執行。 您將會看到下列訊息： `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`  
  
11. 使用 Data Quality Client 連接到資料品質伺服器以確認能否順利連接。  
  
 您也可以使用 Transact-SQL 陳述式附加 DQS 資料庫。 如需有關使用 Transact-SQL 陳述式附加資料庫的詳細資訊，請參閱＜ [Using Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) ＞中的＜ [Attach a Database](../relational-databases/databases/attach-a-database.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [管理 DQS 資料庫](../../2014/data-quality-services/manage-dqs-databases.md)  
  
  
