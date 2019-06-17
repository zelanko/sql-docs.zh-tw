---
title: 存取用於 DQS 作業的資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 88dfb9ea-6321-4eaf-b9e4-45d36ef048f6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b3c722c5774a333773f4bcffc41c408d19ae28be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480524"
---
# <a name="access-data-for-the-dqs-operations"></a>存取用於 DQS 作業的資料
  若要使用您的來源資料進行 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 作業，並匯出已處理的資料，您可以執行下列任一項操作：  
  
-   將來源資料複製到 DQS_STAGING_DATA 資料庫中的資料表/檢視，然後使用該資料進行 DQS 作業。 您也可以將已處理的資料匯出到 DQS_STAGING_DATA 資料庫的新資料表中。 若要這樣做，您的 Windows 使用者帳戶必須擁有對於 DQS_STAGING_DATA 資料庫的讀取/寫入權限。  
  
-   使用您自己的資料庫做為 DQS 作業的來源資料以及匯出已處理資料的目的地。 若要執行此作業，請確定您的資料庫位於和 Data Quality Server 資料庫相同的 SQL Server 執行個體中。 否則，在 Data Quality Client 中，該資料庫將無法用於進行 DQS 作業。 此外，必須授與您的 Windows 使用者帳戶 DQS_STAGING_DATA 資料庫的權限，才可匯出比對結果，因為比對結果會以兩階段匯出：首先會將比對結果先匯出到 DQS_STAGING_DATA 資料庫中的暫存資料表，然後再將其移到目的地資料庫中的資料表。  
  
## <a name="prerequisites"></a>先決條件  
  
-   您必須執行 DQSInstaller.exe 檔案，才可以完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的安裝。 如需詳細資訊，請參閱 [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
-   您的 Windows 使用者帳戶在資料庫引擎執行個體中，必須是適當固定伺服器角色 (例如 securityadmin、serveradmin 或 sysadmin) 的成員，才能授與/修改對資料庫上 SQL 登入的存取權。  
  
### <a name="to-grant-readwrite-access-to-a-user-on-the-dqsstagingdata-database"></a>授與使用者 DQS_STAGING_DATA 資料庫的讀/寫存取權  
  
1.  啟動 Microsoft SQL Server Management Studio。  
  
2.  在 Microsoft SQL Server Management Studio 中，展開您的 SQL Server 執行個體及 **[安全性]** ，然後展開 **[登入]** 。  
  
3.  以滑鼠右鍵按一下 SQL 登入，然後按一下 **[屬性]** 。  
  
4.  在 **[登入屬性]** 對話方塊的左窗格中，按一下 **[使用者對應]** 頁面。  
  
5.  在右窗格中，選取 底下的核取方塊**地圖**資料行**DQS_STAGING_DATA**資料庫，然後再選取 在下列角色**資料庫角色成員資格對象：DQS_STAGING_DATA**窗格：  
  
    -   **db_datareader**：從資料表/檢視讀取資料。  
  
    -   **db_datawriter**：新增、刪除或變更資料表中的資料。  
  
    -   **db_ddladmin**：建立、修改或刪除資料表/檢視。  
  
6.  在 **[登入屬性]** 對話方塊中，按一下 **[確定]** 套用變更。  
  
## <a name="next-steps"></a>後續步驟  
 嘗試執行存取資料庫做為 DQS 作業之資料來源的 DQS 作業，然後將處理過的資料匯出到資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Data Quality Services](install-data-quality-services.md)  
  
  
