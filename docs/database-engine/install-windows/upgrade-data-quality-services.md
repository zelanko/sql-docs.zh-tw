---
title: "升級 Data Quality Services | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d18fdc2c65408898ed5faacc255e74b7a6261d57
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="upgrade-data-quality-services"></a>升級 Data Quality Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供如何升級現有 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Services (DQS) 安裝的資訊。 升級 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Server 的過程中，您也必須升級 DQS 資料庫結構描述。  
  
> [!IMPORTANT]  
>  -   在升級 DQS 之前，您必須先備份 DQS 資料庫，以免在結構描述升級期間有任何意外的遺失資料狀況。 如需有關備份 DQS 資料庫的詳細資訊，請參閱 [備份及還原 DQS 資料庫](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)。  
> -   您可以使用最新或舊版的 Data Quality Client 連線至 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Server，或連線至 Integration Services 的 [DQS 清理轉換](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)，執行您的資料品質工作。  
> -   升級 Data Quality Services 和 Master Data Services 之後，所有適用於 Excel 的舊版 Master Data Services 增益集都無法再繼續運作。 您可以從[這裡](http://go.microsoft.com/fwlink/?LinkID=506665)下載 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 版適用於 Exel 的 Master Data Services 增益集。  
  
##  <a name="Prerequisites"></a> 必要條件  
  
-   您必須以 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 電腦上 Administrator 群組成員的身分登入。  
  
-   您的 Windows 使用者帳戶必須是安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 之 SQL Server 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
##  <a name="Upgrade"></a> 升級 DQS  
 升級 DQS：  
  
1.  在開始升級程序之前，請先備份 DQS 資料庫。 如需有關備份 DQS 資料庫的詳細資訊，請參閱 [備份及還原 DQS 資料庫](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)。  
  
2.  升級已安裝 DQS 的 SQL Server 執行個體。  
  
    1.  執行 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安裝精靈。  
  
    2.  按一下左窗格中的 [安裝]。  
  
    3.  在右窗格中，按一下 [升級來源] 從舊版 SQL Server 升級。  
  
    4.  完成安裝精靈。  
  
        > [!NOTE]  
        >  如果 Data Quality Client 先前已安裝在這部電腦上，此作業會將您的 SQL Server 執行個體升級至 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]，而且也會安裝最新的 Data Quality Client。 如果您已將 Data Quality Client 安裝在其他電腦上，則必須在那些電腦上執行步驟 2 的子步驟，才能安裝 Data Quality Client 的目前版本。 安裝精靈會將 Data Quality Client 的目前版本與 Data Quality Client 的現有版本並列安裝。 升級 DQS 資料庫結構描述之後，您可以使用最新或舊版 Data Quality Client 連接至 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 版的資料品質伺服器。  
  
3.  升級 DQS 資料庫結構描述。  
  
    1.  以系統管理員身分啟動命令提示字元。  
  
    2.  在命令提示字元中，將目錄變更為 DQSInstaller.exe 所在的位置。 若為 SQL Server 的預設執行個體，DQSInstaller.exe 檔案位於 C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn：  

      >[!NOTE]
      >將資料夾路徑中的 [nn] 替換成 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 版本號碼。
      >- SQL Server 2016 為 13
      >- SQL Server 2017 為 14

        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  在命令提示字元中輸入下列命令，然後按 ENTER：  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  安裝程式會提示您先備份 DQS 資料庫後再繼續。 如果您已經備份 DQS 資料庫，請輸入 **Y** 或 **Yes**，然後按 ENTER 繼續升級。  
  
    5.  在成功升級 DQS 資料庫結構描述之後，將會顯示完成訊息。  
  
##  <a name="Verify"></a> 確認 DQS 資料庫結構描述升級  
 若要確認 DQS 資料庫結構描述升級成功，您可以查詢中每個資料庫中的 A_DB_VERSION 資料表，以檢查 DQS_MAIN 和 DQS_PROJECTS 資料庫中的目前版本。 若要這樣做：  
  
1.  啟動 SQL Server Management Studio，並連接到包含已升級之 DQS 資料庫結構描述的 SQL Server 執行個體。  
  
2.  執行下列查詢：  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  輸出會顯示每個升級項目和升級日期。 最新日期的最大 VERSION_ID 和 ASSEMBLY_VERSION 為目前版本。 STATUS 資料行中的值為 2 代表成功。 如果發生錯誤，錯誤會列示在 ERROR 資料行中。 範例輸出：  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|error|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<網域\使用者名稱>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<網域\使用者名稱>|2||  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [移除 Data Quality Server 物件](../../sql-server/install/remove-data-quality-server-objects.md)   
 [升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
