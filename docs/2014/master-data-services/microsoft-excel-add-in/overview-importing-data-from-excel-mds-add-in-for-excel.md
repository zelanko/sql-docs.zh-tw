---
title: 發行資料（適用于 Excel 的 MDS 增益集） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd5046c9a307f498ffb585c99cba8044c7b18b3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479036"
---
# <a name="publishing-data-mds-add-in-for-excel"></a>發行資料 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，如果您想要與其他使用者共用資料，請將資料發行至 MDS 存放庫。 一旦發行資料之後，這項資料就可供此增益集的其他使用者下載。  
  
 發行資料時，您已新增或更新的任何資料都會發行至 MDS 存放庫。 不過，您已刪除的資料則不會發行；您必須個別刪除資料。 如需詳細資訊，請參閱 [刪除資料列 &#40;適用於 Excel 的 MDS 增益集&#41;](delete-a-row-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  發行無法用來建立新的實體。 如需建立實體的詳細資訊，請參閱[建立實體 &#40;MDS 適用於 Excel 的增益集&#41;](create-an-entity-mds-add-in-for-excel.md)。  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>多位使用者同時發行時  
 多位使用者可以發行相同資料的更新。 當每位使用者發行時，更新會儲存至資料庫。 這表示，沒有使用最近更新之資料的使用者仍然可以在發行時變更值。  
  
 只有您所進行的更新會發行至資料庫。 系統不會發行工作表中的任何過期資料。  
  
## <a name="transactions-and-annotations"></a>交易和註解  
 每個發行的變更都會儲存成交易。 如果您選擇，可以將註解加入至交易，以便說明進行變更的原因。  
  
-   雖然刪除項目會儲存成可由管理員反轉的交易，不過您無法註解刪除項目。  
  
-   如果您變更了某個成員的**Code**值，它就不會記錄為交易，而且該成員的所有先前交易都無法使用。  
  
-   您可以檢視其他使用者對成員所做的交易。 您也可以檢視自己對成員所做的所有交易，即使您不再擁有特定屬性的權限也一樣。  
  
 您可以檢視對成員所做的所有交易。 如需詳細資訊，請參閱 [檢視成員的所有註解或交易 &#40;適用於 Excel 的 MDS 增益集&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)。  
  
> [!IMPORTANT]  
>  如果您輸入了超過 500 個字元的註解，系統將自動截斷註解。  
  
## <a name="business-rule-and-other-validation"></a>商務規則和其他驗證  
 發行資料時，系統會在資料新增至 MDS 存放庫之前執行驗證，確保資料正確無誤。 如果資料不符合指定的準則，就不會發行至儲存機制。 如需詳細資訊，請參閱[驗證資料 &#40;MDS 適用於 Excel 的增益集&#41;](validating-data-mds-add-in-for-excel.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|將資料從使用中工作表發行回 MDS 儲存機制。|[將 Excel 的資料發行至適用于 Excel 的 mds 增益集 &#40;&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|同時從 MDS 儲存機制和工作表中刪除資料列。|[&#40;適用于 Excel 的 MDS 增益集&#41;刪除資料列](delete-a-row-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [重新整理適用于 Excel 的 MDS 增益集&#41;的資料 &#40;](refreshing-data-mds-add-in-for-excel.md)  
  
-   [適用於 Microsoft Excel 的 Master Data Services 增益集](master-data-services-add-in-for-microsoft-excel.md)  
  
  
