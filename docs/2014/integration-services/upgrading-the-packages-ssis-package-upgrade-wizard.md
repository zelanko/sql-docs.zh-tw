---
title: 升級封裝 （SSIS 封裝升級精靈） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.is.upgradewizard.upgradingpackage.f1
ms.assetid: cdb842e3-2e59-4ede-b127-be4fde46875c
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6485982823d1ee2deafa0c981d1fc16950699799
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023367"
---
# <a name="upgrading-the-packages-ssis-package-upgrade-wizard"></a>升級封裝 (SSIS 封裝升級精靈)
  使用 **[正在升級封裝]** 頁面，即可檢視封裝升級的進度，並在必要時中斷升級程序。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈會逐一升級選取的封裝。  
  
 **若要檢視的升級封裝儲存到 SQL Server 資料庫或封裝存放區**  
  
-   在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]的 [物件總管] 中，連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的本機執行個體，然後展開 **[存放的封裝]** 節點，查看已升級的封裝。  
  
 **若要檢視已從 SQL Server 資料工具升級的升級的封裝**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的 [方案總管] 中，開啟 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，然後展開 **[SSIS 封裝]** 節點，查看升級的封裝。  
  
## <a name="options"></a>選項。  
 **訊息窗格**  
 在升級進行期間顯示進度訊息和摘要資訊。  
  
 **動作**  
 檢視升級中的動作。  
  
 **狀態**  
 檢視每個動作的結果。  
  
 **Message**  
 檢視每個動作所產生的錯誤訊息。  
  
 **停止**  
 停止封裝升級。  
  
 **報表**  
 選取您想要針對包含封裝升級結果的報表採取什麼動作：  
  
-   線上檢視報表。  
  
-   將報表儲存為檔案。  
  
-   將報表複製到剪貼簿。  
  
-   以電子郵件訊息傳送報表。  
  
## <a name="see-also"></a>另請參閱  
 [升級 Integration Services 套件](install-windows/upgrade-integration-services-packages.md)  
  
  