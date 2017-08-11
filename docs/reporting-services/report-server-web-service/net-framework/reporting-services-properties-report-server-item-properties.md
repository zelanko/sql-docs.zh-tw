---
title: "報表伺服器項目屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- report servers [Reporting Services], properties
- item-specific properties [Reporting Services]
- report items [Reporting Services], properties
- items [Reporting Services], properties
ms.assetid: 21edec6d-9897-48fb-8c75-182305b1dbdb
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ae7f1a99b09e4c8fc5f2483e9aa360cce83da2df
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="reporting-services-properties---report-server-item-properties"></a>Reporting Services 內容-報表伺服器項目屬性
  項目屬性是報表伺服器資料庫中項目特有的屬性。 這類型的項目包括報表、連結報表、資料夾、資源、模型以及資料來源。  
  
 下列項目屬性名稱會保留。 您無法建立具有相同名稱的使用者定義屬性。 您可以使用報表伺服器 Web 服務方法來讀取或修改許多屬性。  
  
## <a name="item-properties"></a>項目屬性  
 下列屬性適用報表伺服器資料庫中的所有項目。  
  
|屬性|Description|  
|--------------|-----------------|  
|**CreatedBy**|原先將項目加入報表伺服器資料庫的使用者名稱。|  
|**CreationDate**|項目加入報表伺服器資料庫的日期與名稱。|  
|**描述**|項目的描述。|  
|**Hidden**|指出使用者是否可看到和使用項目的值。|  
|**識別碼**|報表伺服器資料庫中項目的識別碼。|  
|**[Modifiedby]**|報表伺服器資料庫中上次修改項目的使用者名稱。|  
|**ModifiedDate**|使用者上次修改項目的日期和時間。|  
|**名稱**|報表伺服器資料庫中項目的名稱。|  
|**路徑**|項目的完整路徑名稱。 報表伺服器資料庫中任何項目的路徑，其最大字元長度為 260。|  
|**大小**|報表伺服器資料庫中項目的大小 (以位元組為單位)。|  
|**類型**|報表伺服器資料庫中項目的類型。|  
|**VirtualPath**|報表伺服器資料庫中項目的虛擬路徑。 <xref:ReportService2010.CatalogItem.VirtualPath%2A> 屬性值是使用者預期可用來檢視項目的路徑。 例如，名為 report1 的報表是位於使用者個人的 [我的報表] 資料夾中，具有 My Reports 的虛擬路徑。 項目的實際路徑是 /Users/username/My Reports。|  
  
## <a name="folder-properties"></a>資料夾屬性  
 除了先前所列的項目屬性之外，下列屬性會套用至報表伺服器資料庫中的資料夾。  
  
|屬性|Description|  
|--------------|-----------------|  
|**保留**|針對報表伺服器所保留的資料夾，由 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法傳回的值。 保留的資料夾包含 [使用者]、[我的報表] 和 /。 無法修改或移除保留的資料夾。|  
  
## <a name="report-properties"></a>報表屬性  
 除了先前所列的項目屬性之外，下列屬性會套用至報表伺服器資料庫中的報表。  
  
|屬性|Description|  
|--------------|-----------------|  
|**語言**|報表中使用的語言。 這個值是網際網路工程任務推動小組 (IETF) RFC1766 規格中定義的語言代碼。 第一部分是由基本語言的兩個字元所指定。 第二個部分是由連字號分隔，並指定語言的變化或是方言。 如果在與報表定義中的 **Body** 元素相關聯的 **Style** 元素中未指定值，預設值是報表伺服器的語言。|  
|**ReportProcessingTimeout**|個別報表的逾時 (以秒為單位)。 如果已設定此值，當指定時間已經過時，報表伺服器會嘗試停止處理報表。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果值為**-1**，報表處理期間不會逾時。 如果值為**null**，系統屬性的值**ReportProcessingTimeout**用於報表處理逾時。 預設值是**null**。 如需詳細資訊，請參閱[報表伺服器系統屬性](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)。|  
|**ExecutionDate**|上次為報表建立報表快照集的日期和時間。|  
|**CanRunUnattended**|指出是否可依照排程自動執行報表的值。 如果這個屬性設定為**true**、 定義報表參數的預設值和資料來源認證會儲存在報表中，或認證擷取選項設定為**無**。 如果這個屬性設定為**false**，不符合自動執行報表的必要條件。 如需詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。|  
|**HasParameterDefaultValues**|這個值會指出報表是否具有為所有報表參數設定的有效預設值。 值也是**true**如果報表沒有報表參數。 如果此屬性設定為 **false**，則表示一個或多個報表參數沒有有效的預設值。|  
|**HasDataSourceCredentials**|這個值會指出針對所有與報表相關聯的資料來源，所設定的認證擷取選項是 **None** 或 **Store**。 如果這個屬性設定為 **false**，針對與報表相關聯的其中一個資料來源所設定的認證擷取選項會是 **Integrated** 或 **Prompt**。|  
|**IsSnapshotExecution**|這個值會指出報表是否為快照集。|  
|**HasScheduleReadyDataSources**|這個值會指出報表的資料來源是否設定為支援排程的執行。 如果這個屬性設定為**false**，使用者便無法訂閱報表。|  
  
## <a name="resource-properties"></a>資料屬性  
 除了先前所列的項目屬性之外，下列屬性會套用至報表伺服器資料庫中的資源。  
  
|屬性|Description|  
|--------------|-----------------|  
|**MimeType**|報表伺服器資料庫中資源的 MIME 類型。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和.NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技術參考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
