---
title: "功能屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQMSupportEnabled property
- ComUdfEnabled property
- LinkToOtherInstanceEnabled property
- ManagedCodeEnabled property
- ConnStringEncryptionEnabled property
- LinkFromOtherInstanceEnabled property
- LinkInsideInstanceEnabled property
- UseCachedPageAllocators property
ms.assetid: a34d046a-6562-4d98-b827-37cebc6d77b4
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b96a0fe3f5b3a1bd036543e58b8ec34be3f602b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="feature-properties"></a>功能屬性
  與產品功能有關的功能屬性，大部分是進階屬性，包含控制伺服器執行個體間之連結的屬性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於** ：僅限於多維度伺服器模式  
  
## <a name="properties"></a>屬性  
  
|屬性|預設值|說明|  
|--------------|-------------|-----------------|  
|**ManagedCodeEnabled**|1|此為布林值屬性，指出是否啟用 CLR 儲存程序。|  
|**LinkInsideInstanceEnabled**|1|此為布林值屬性，指出是否可以在相同的伺服器執行個體內建立連結物件。|  
|**LinkToOtherInstanceEnabled**|0|此為布林值屬性，指出是否可以連結到遠端伺服器上的物件。|  
|**LinkFromOtherInstanceEnabled**|0|此為布林值屬性，指出是否可從其他伺服器執行個體連結到物件。|  
|**ConnStringEncryptionEnabled**|1|此為布林值屬性，指出在伺服器組態檔中的連接字串是否有加密。|  
|**UseCachedPageAllocators**|0|此為布林值屬性，指出是否啟用快取的頁面配置器。|  
|**ComUdfEnabled**|0|此為布林值屬性，指出是否啟用定義為 COM 物件的使用者定義函數。|  
|**SQMSupportEnabled**|1|此為布林值屬性，指出錯誤和功能使用方式報表是否自動傳送至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。|  
|**ResourceMonitoringEnabled**|1|此為布林屬性，指出是否啟用內部資源監視計數器。 此屬性預設為啟用。 啟用時，此屬性可讓計數器收集有關 CPU、記憶體和 I/O 活動的使用量資料。<br /><br /> 報告有關資源使用量的動態管理檢視 (DMV) 會使用內部資源監視計數器。 如果您停用此屬性，DMV 查詢仍會執行，但結果集將會無效。 相依於此屬性的 DMV 如下：<br /><br /> **DISCOVER_OBJECT_ACTIVITY**<br /><br /> **DISCOVER_COMMAND_OBJECTS**<br /><br /> **DISCOVER_SESSIONS** (用於 SESSION_READS、SESSION_WRITES、SESSION_CPU_TIME_MS)<br /><br /> <br /><br /> 注意：在使用 NUMA 架構的多核心系統上，停用此屬性可以改善查詢效能，尤其是多使用者的高工作負載。 您將需要執行比較測試，判斷變更此屬性是否使查詢效能獲得改善。 如需執行比較測試的最佳作法，包括清除快取和避免常見的錯誤，請參閱 [SQL Server 2008 R2 Analysis Services 作業指南](http://go.microsoft.com/fwlink/?LinkID=225539)。|  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
