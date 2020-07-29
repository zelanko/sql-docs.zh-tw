---
title: 利用 SQL Server Management Studio 管理伺服器
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 96119c90c8a187830fd5a2264e833bb326593a29
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010918"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>利用 SQL Server Management Studio 管理伺服器
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是一個非常豐富的整合式管理用戶端，專為了符合 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Azure SQL Database 管理員的伺服器管理需求而設計。 在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中可以使用 [物件總管] 來完成管理工作，其中可以讓您連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 系列的任何伺服器，並以圖形方式瀏覽其內容。 伺服器可以是 [!INCLUDE[ssDE](../includes/ssde_md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 或 Azure SQL Database 的執行個體。  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的工具元件包括已註冊的伺服器、物件總管、方案總管、範本總管、物件總管詳細資料頁面，以及文件視窗。 若要顯示工具，請在 [檢視]  功能表上按一下工具名稱。 若要顯示查詢編輯器工具，請在工具列上按一下 [新增查詢]  按鈕。  
  
> [!IMPORTANT]  
> 依預設，不會加密 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之間的網路傳輸。 除非您已建立加密連接，否則，請勿在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中使用機密資料 (包括密碼)。 如需詳細資訊，請參閱 [如何：啟用 Database Engine 的加密連接 (SQL Server 組態管理員)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006)。  
  
請利用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 來執行下列動作：  
  
-   註冊伺服器。  
  
-   連線到 [!INCLUDE[ssDE](../includes/ssde_md.md)]、SSAS、[!INCLUDE[ssRS](../includes/ssrs.md)]、[!INCLUDE[ssIS](../includes/ssis_md.md)] 或 Azure SQL Database 的執行個體。  
  
-   設定伺服器屬性。  
  
-   管理資料庫和 SSAS 物件，如 Cube、維度和組件。  
  
-   建立物件，如資料庫、資料表、Cube、資料庫使用者和登入。  
  
-   管理檔案和檔案群組。  
  
-   附加或卸離資料庫。  
  
-   啟動指令碼工具。  
  
-   管理安全性。  
  
-   檢視系統記錄。  
  
-   監視目前的活動。  
  
-   設定複寫。  
  
-   管理全文檢索索引。  
  
若要啟動和停止 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent，請使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員。  
  
## <a name="see-also"></a>另請參閱  
[使用 SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[如何：檢視伺服器屬性 (SQL Server Management Studio)](https://msdn.microsoft.com/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  
