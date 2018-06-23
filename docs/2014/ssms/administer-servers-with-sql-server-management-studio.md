---
title: 利用 SQL Server Management Studio 管理伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9b14e5ecd7cc10a5a3cb5b50b847e3945f9633ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133610"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>利用 SQL Server Management Studio 管理伺服器
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是一個豐富、 整合式管理用戶端是設計成符合[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]系統管理員的伺服器管理需求。 在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中可以使用 [物件總管] 來完成管理工作，其中可以讓您連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 系列的任何伺服器，並以圖形方式瀏覽其內容。 伺服器可以是 [!INCLUDE[ssDE](../includes/ssde-md.md)]、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的執行個體。  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的工具元件包括已註冊的伺服器、物件總管、方案總管、範本總管、物件總管詳細資料頁面，以及文件視窗。 若要顯示工具，請在 [檢視] 功能表上按一下工具名稱。 若要顯示查詢編輯器工具，請在工具列上按一下 [新增查詢] 按鈕。  
  
> [!IMPORTANT]  
>  依預設，不會加密 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之間的網路傳輸。 除非您已建立加密連接，否則，請勿在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中使用機密資料 (包括密碼)。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 請利用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 來執行下列動作：  
  
-   註冊伺服器。  
  
-   連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]、[!INCLUDE[ssAS](../includes/ssas-md.md)]、[!INCLUDE[ssRS](../includes/ssrs-md.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 的執行個體。  
  
-   設定伺服器屬性。  
  
-   管理資料庫和 [!INCLUDE[ssAS](../includes/ssas-md.md)] 物件，如 Cube、維度和組件。  
  
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
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [檢視或變更伺服器屬性 &#40;SQL Server&#41;](../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
  