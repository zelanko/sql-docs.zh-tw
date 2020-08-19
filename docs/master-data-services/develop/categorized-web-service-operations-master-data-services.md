---
description: 分類的 Web 服務作業 (Master Data Services)
title: 分類的 Web 服務作業
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: reference
ms.assetid: e3f346b5-7e26-481d-9821-1846e2e91289
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bd6c3db52323385712bb946c63254e11c45cd5f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495020"
---
# <a name="categorized-web-service-operations-master-data-services"></a>分類的 Web 服務作業 (Master Data Services)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

   Web 服務包含一組完整的作業，這組作業可讓您撰寫程式碼以控制  透過其使用者介面所執行的所有功能。 這些 Web 服務作業是透過 <xref:Microsoft.MasterDataServices.IService> 介面定義，並當做 <xref:Microsoft.MasterDataServices.ServiceClient> 類別中的方法實作。 本主題將 Web 服務作業分為概念性類別目錄，以協助您了解如何使用 Web 服務 API。  
  
## <a name="model-operations"></a>模型作業  
 這些作業用於建立、更新與刪除模型，以及針對模型的所有內容操作，例如實體、階層和版本。 如需詳細資訊，請參閱[模型 &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.MetadataClone%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.MetadataCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.MetadataDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.MetadataGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>
  
## <a name="entity-operations"></a>實體作業  
 這些作業用於建立、更新與刪除單一實體的成員。 如需詳細資訊，請參閱[實體 &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md) 和[成員 &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberKeyLookup%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCopy%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersMerge%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersUpdate%2A>
  
## <a name="member-operations"></a>成員作業  
 這些作業用於取得、更新與刪除成員。 這組成員的操作對象可以包含來自多個實體的成員。 如需詳細資訊，請參閱[成員 &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkMerge%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkUpdate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersGet%2A>
  
## <a name="attribute-and-hierarchy-operations"></a>屬性和階層作業  
 這些作業用於取得屬性和階層資訊。 您也可以使用模型作業 (例如 <xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>) 來修改屬性和階層。 如需詳細資訊，請參閱[屬性 &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md) 和[階層 &#40;Master Data Services&#41;](../../master-data-services/hierarchies-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAttributesGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.HierarchyMembersGet%2A>
  
## <a name="business-rule-operations"></a>商務規則作業  
 這些作業用於建立、更新、刪除與發佈商務規則。 如需詳細資訊，請參閱[商務規則 &#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesClone%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPaletteGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPublish%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesUpdate%2A>
  
## <a name="annotation-operations"></a>註解作業  
 這些作業用於建立、更新與刪除註解。 如需詳細資訊，請參閱[註解 &#40;Master Data Services&#41;](../../master-data-services/annotations-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsUpdate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsGet%2A>
  
## <a name="transaction-operations"></a>交易作業  
 這些作業用於取得與反轉交易。 如需詳細資訊，請參閱[交易 &#40;Master Data Services&#41;](../../master-data-services/transactions-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.TransactionsGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.TransactionsReverse%2A>
  
## <a name="version-and-validation-operations"></a>版本和驗證作業  
 這些作業用於複製和驗證版本。 如需詳細資訊，請參閱[版本 &#40;Master Data Services&#41;](../../master-data-services/versions-master-data-services.md) 和[驗證 &#40;Master Data Services&#41;](../../master-data-services/validation-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.VersionCopy%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ValidationGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ValidationProcess%2A>
  
## <a name="data-quality-operations"></a>資料品質作業  
 這些作業用於執行資料品質工作及檢查其結果。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityCleansingOperationCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityMatchingOperationCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityInstalledState%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityKnowledgeBasesGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStart%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationResultsGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStatus%2A>
  
## <a name="data-import-operations"></a>資料匯入作業  
 這些作業用於將資料匯入至 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫。 如需詳細資訊，請參閱 [總覽：從資料表匯入資料 &#40;Master Data Services&#41;](../../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingClear%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingLoad%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingProcess%2A>
  
 下列作業用於透過 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中包含的暫存處理序匯入資料。 這些作業僅用於支援現有的資料庫。 對於新的開發，請使用先前列出的作業。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.StagingClear%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.StagingGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.StagingNameCheck%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.StagingProcess%2A>
  
## <a name="data-export-operations"></a>資料匯出作業  
 這些作業用於透過訂閱檢視匯出資料。 如需詳細資訊，請參閱 [概觀：匯出資料 &#40;Master Data Services&#41;](../../master-data-services/overview-exporting-data-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.ExportViewCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ExportViewDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ExportViewListGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ExportViewUpdate%2A>
  
## <a name="security-operations"></a>安全性作業  
 這些作業用於修改控制對 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫之存取的安全性設定。 如需詳細資訊，請參閱[安全性 &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsClone%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsUpdate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesClone%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesCreate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesUpdate%2A>
  
## <a name="system-operations"></a>系統作業  
 這些作業用於取得與更新系統設定和使用者喜好設定。  
  
- <xref:Microsoft.MasterDataServices.ServiceClient.ServiceCheck%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.ServiceVersionGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SystemDomainListGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SystemPropertiesGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsUpdate%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesDelete%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesGet%2A>
- <xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesUpdate%2A>
  
  
