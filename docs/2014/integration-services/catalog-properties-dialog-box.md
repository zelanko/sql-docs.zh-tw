---
title: 目錄屬性對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.iscatalogprop.general.f1
- sql12.ssis.ssms.iscreatecatalog.f1
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d3492cce19906322ef9b420718aae0ae9e0e62d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061106"
---
# <a name="catalog-properties-dialog-box"></a>目錄屬性對話方塊
  使用 [目錄屬性] 對話方塊來設定 SSISDB 目錄。 目錄屬性會定義機密資料的加密方式、保留作業和專案版本設定資料的方式，以及驗證作業何時超時。SSISDB 目錄是[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]專案、封裝、參數與環境的中央儲存和管理點。  
  
 您也可以在 catalog.catalog_property 檢視表中檢視目錄屬性，以及使用 catalog.configure_catalog 預存程序來設定屬性。 如需詳細資訊，請參閱 [catalog.catalog_properties &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) 和 [catalog.configure_catalog &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)。  
  
 如需如何建立 SSISDB 目錄的資訊，請參閱 [建立 SSIS 目錄](catalog/ssis-catalog.md)。  
  
 **您想要做什麼事？**  
  
-   [開啟 [目錄屬性] 對話方塊](#open_dialog)  
  
-   [設定選項](#options)  
  
##  <a name="open_dialog"></a>開啟 [目錄屬性] 對話方塊  
  
1.  開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]  
  
2.  連接 Microsoft SQL Server Database Engine。  
  
3.  在物件總管中，展開 [Integration Services]**** 節點，並以滑鼠右鍵按一下 [SSISDB]****，然後按一下 [屬性]****。  
  
##  <a name="options"></a> 設定選項  
  
### <a name="options"></a>選項。  
 下表描述對話方塊中的特定屬性，以及 catalog.catalog_property 檢視表中的對應屬性。  
  
|屬性名稱 (目錄屬性對話方塊)|屬性名稱 (catalog.catalog_property 檢視表)|描述|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|加密演算法名稱|ENCRYPTION_CLEANUP_ENABLED|指定用來加密目錄中敏感性參數值的加密類型。 以下是可能的值：<br /><br /> **DES**<br /><br /> **TRIPLE_DES**<br /><br /> **TRIPLE_DES_3KEY**<br /><br /> **DESPX**<br /><br /> **AES_128**<br /><br /> **AES_192**<br /><br /> **AES_256** （預設值）|  
|驗證逾時 (秒)|VALIDATION_TIMEOUT|指定專案驗證或封裝驗證在停止之前，可以執行的秒數上限。 預設值為 300 秒。<br /><br /> 執行驗證是非同步作業。 專案或封裝愈大，驗證所需時間愈長。<br /><br /> 如需有關驗證專案和封裝的詳細資訊，請參閱＜ [Integration Services Data Types in Expressions](expressions/integration-services-data-types-in-expressions.md)＞。|  
|定期清除記錄檔|OPERATION_CLEANUP_ENABLED|將屬性設為 True，指出 SQL Server Agent 作業 (作業清除) 會執行。 否則請將屬性設為 False。|  
|保留週期 (天)|RETENTION_WINDOW|指定可允許的作業資料存在時間上限 (以天為單位)。 SQL Agent 作業 (作業清除) 會移除比指定天數還舊的資料。|  
|每一專案的版本數目上限|MAX_PROJECT_VERSIONS|指定多少個專案版本會儲存在目錄中。 當專案版本清除作業執行時，將會移除超過最大值的舊專案版本。|  
  
  
