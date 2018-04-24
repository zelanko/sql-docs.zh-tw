---
title: 概觀：從 Excel 匯入資料 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
caps.latest.revision: 13
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8dc133095f5913fd8528c89fa611b395f4d74370
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="overview-importing-data-from-excel-mds-add-in-for-excel"></a>概觀：從 Excel 匯入資料 (適用於 Excel 的 MDS 增益集)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，如果您想要與其他使用者共用資料，請將資料發行至 MDS 存放庫。 一旦發行資料之後，這項資料就可供此增益集的其他使用者下載。  
  
 發行資料時，您已加入或更新的任何資料都會發行至 MDS 儲存機制。 不過，您已刪除的資料則不會發行。您必須個別刪除資料。 如需詳細資訊，請參閱 [刪除資料列 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  發行無法用來建立新的實體。 如需建立實體的詳細資訊，請參閱[建立實體 &#40;MDS 適用於 Excel 的增益集&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)。  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>多位使用者同時發行時  
 多位使用者可以發行相同資料的更新。 當每位使用者發行時，更新會儲存至資料庫。 這表示，沒有使用最近更新之資料的使用者仍然可以在發行時變更值。  
  
 只有您所進行的更新會發行至資料庫。 系統不會發行工作表中的任何過期資料。  
  
## <a name="transactions-and-annotations"></a>交易和註解  
 每個發行的變更都會儲存成交易。 如果您選擇，可以將註解加入至交易，以便說明進行變更的原因。  
  
-   雖然刪除項目會儲存成可由管理員反轉的交易，不過您無法註解刪除項目。  
  
-   如果您變更了某個成員的 **Code** 值，此成員的所有先前交易將無法使用。 藉由將 **Code** 值傳回給原始值，您可以存取先前的交易。  
  
-   您可以檢視其他使用者對成員所做的交易。 您也可以檢視自己對成員所做的所有交易，即使您不再擁有特定屬性的權限也一樣。 您無法檢視涉及您的權限設定為拒絕之屬性的交易。  
  
 您可以檢視對成員所做的所有交易。 如需詳細資訊，請參閱 [檢視成員的所有註解或交易 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)。  
  
> [!IMPORTANT]  
>  如果您輸入了超過 500 個字元的註解，系統將自動截斷註解。  
  
## <a name="business-rule-and-other-validation"></a>商務規則和其他驗證  
 發行資料時，系統會在資料加入至 MDS 儲存機制之前執行驗證，確保資料正確無誤。 如果資料不符合指定的準則，就不會發行至儲存機制。 如需詳細資訊，請參閱[驗證資料 &#40;MDS 適用於 Excel 的增益集&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|將資料從使用中工作表發行回 MDS 儲存機制。|[將資料從 Excel 匯入 Master Data Services &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|同時從 MDS 儲存機制和工作表中刪除資料列。|[刪除資料列 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)|  
|當您想要在一段時間之後檢視資料的更新時，請檢視資料列 (成員) 的註解和交易。|[檢視成員的所有註解或交易 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|當您要在發行前比較資料時，可以結合兩個工作表的資料。|[結合資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>相關內容  
  
-   [重新整理資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [適用於 Microsoft Excel 的 Master Data Services 增益集](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
