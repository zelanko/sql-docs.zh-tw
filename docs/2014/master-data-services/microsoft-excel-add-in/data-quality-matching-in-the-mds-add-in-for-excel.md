---
title: 適用於 Excel 的 MDS 增益集中的資料品質比對 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: be78d051-0d56-46d3-bb89-327e218dadd6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 696a114c74ecb6d4b8f4cfe6b2d16b33869e1602
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478907"
---
# <a name="data-quality-matching-in-the-mds-add-in-for-excel"></a>適用於 Excel 的 MDS 增益集中的資料品質比對
  經過一段時間後，您需要將更多的資料加入至 MDS 儲存機制。 在新增資料之前，比較新資料與已在 MDS 中受控的資料，有助於確保不會新增重複或不精準的資料。  
  
 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Data Quality Services (DQS) 功能來比較相似的資料。 當您使用增益集的比對功能時，相似記錄會群組在一起，而且會顯示代表結果精確度的分數。 如需有關 DQS 所提供之比對功能的詳細資訊，請參閱＜ [Data Matching](../../data-quality-services/data-matching.md)＞。  
  
## <a name="workflow-for-data-quality-matching"></a>資料品質比對的工作流程  
 搭配使用 DQS 與 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]時，請使用下列工作流程：  
  
1.  擷取 MDS 管理之資料的清單，並將它與不在 MDS 中管理之資料的清單結合。 如需詳細資訊，請參閱 [結合資料 &#40;適用於 Excel 的 MDS 增益集&#41;](combine-data-mds-add-in-for-excel.md)＞。  
  
2.  使用 DQS 知識，比較合併清單中的資料。 如需詳細資訊，請參閱 [比對相似資料 &#40;適用於 Excel 的 MDS 增益集&#41;](match-similar-data-mds-add-in-for-excel.md)＞。  
  
3.  若要檢視 DQS 所找到之相似度的詳細資料，請顯示詳細資料資料行。  
  
4.  瀏覽結果，判斷哪些資料應該加入至 MDS 儲存機制，哪些資料是重複的。  
  
5.  將新的和/或已更新的資料發行到 MDS 儲存機制。  
  
## <a name="knowledge-bases"></a>知識庫  
 增益集所提供的比對結果是以 DQS 知識庫為基礎。  
  
-   安裝 DQS 時，會建立預設知識庫 (DQS 資料)。 若您選擇使用預設知識庫 (而沒有透過 Data Quality Client 將比對原則加入預設知識庫)，您必須將工作表中的資料行對應至知識庫的網域，然後再指派權數值給您所選擇的網域。  
  
-   您可以使用 Data Quality Client 建立含有比對原則的新知識庫，或是將比對原則加入預設知識庫。 在此情況下，加權值是由您已建立的比對原則所決定，您只需要將資料行對應至定義域。 如需相關資訊，請參閱 [建立訂閱](../../data-quality-services/create-a-matching-policy.md)。  
  
 如需有關知識庫的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|結合外部資料與 MDS 管理的資料，準備進行比較。|[結合 Data &#40;適用于 Excel 的 MDS 增益集&#41;](combine-data-mds-add-in-for-excel.md)|  
|使用 DQS 知識來尋找資料中的相似度。|[符合適用于 Excel&#41;的類似資料 &#40;MDS 增益集](match-similar-data-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [發行資料 &#40;適用于 Excel 的 MDS 增益集&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [資料比對](../../data-quality-services/data-matching.md)  
  
  
