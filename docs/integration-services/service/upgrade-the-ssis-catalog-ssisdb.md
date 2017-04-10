---
title: "升級 SSIS 目錄 (SSISDB) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.dbupgradewizard.f1"
ms.assetid: 170c3dc9-f5bf-4599-ae56-d24a620f23e8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 升級 SSIS 目錄 (SSISDB)
  當資料庫版本比目前的 SQL Server 執行個體版本還舊時，執行 SSISDB 升級精靈來升級 SSIS 目錄資料庫 (SSISDB)。 這會在下列其中一個條件成立時發生：  
  
-   您已從舊版 SQL Server 還原資料庫。  
  
-   您在升級 SQL Server 執行個體之前，並未從 AlwaysOn 可用性群組移除資料庫。 這可防止資料庫自動升級。 如需詳細資訊，請參閱＜ [Upgrading SSISDB in an availability group](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)＞。  
  
 此精靈只能升級本機伺服器執行個體上的資料庫。  
  
## 執行 SSISDB 升級精靈升級 SSIS 目錄 (SSISDB)  
  
1.  備份 SSIS 目錄資料庫 (SSISDB)。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展開本機伺服器，然後展開 [Integration Services 目錄] 。  
  
3.  以滑鼠右鍵按一下 [SSISDB]，然後選取 [資料庫升級] 啟動 [SSISDB 升級精靈]。  
  
     ![Launch the SSISDB upgrade wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png "Launch the SSISDB upgrade wizard")  
  
4.  在 [選取執行個體]  頁面上，選取本機伺服器上的 SQL Server 執行個體。  
  
    > [!IMPORTANT]  
    >  此精靈只能升級本機伺服器執行個體上的資料庫。  
  
     選取此核取方塊，表示您已經在執行這個精靈之前備份 SSISDB 資料庫。  
  
     ![Select the server in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "Select the server in the SSISDB Upgrade Wizard")  
  
5.  選取 [升級]  升級 SSIS 目錄資料庫。  
  
6.  在 [結果]  頁面上，檢閱結果。  
  
     ![Review the results in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "Review the results in the SSISDB Upgrade Wizard")  
  
  