---
title: 資料集屬性對話方塊、 欄位 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10021"
ms.assetid: 75c7e54a-3d20-4c9a-88da-ab36dce2ce42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 375d8eda6f0863dbe3852f1a88ea2e58ecc85b80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109426"
---
# <a name="dataset-properties-dialog-box-fields-report-builder"></a>資料集屬性對話方塊、欄位 (報表產生器)
  選取 **[資料集屬性]** 對話方塊上的 **[欄位]** ，即可變更報表資料集的欄位集合。 欄位清單會自動擴展，但您可以使用 **[欄位]** 來加入、編輯和刪除查詢與導出欄位。  
  
 只有在內嵌資料集上才支援導出欄位。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項。  
 **[加入]**  
 將新的查詢或導出欄位加入到資料集中。  
  
 **刪除**  
 從資料集中刪除選取的欄位。  
  
 **欄位名稱**  
 輸入欄位的名稱。 此欄位在資料集內必須是唯一的。 對於資料集中每個現有的欄位，系統都會預先填入名稱。  
  
 **欄位來源**  
 輸入欄位的值。  
  
 對導出欄位而言，欄位來源必須是資料集查詢所擷取之現有欄位的名稱，或是您建立的運算式。 例如，若要建立欄位來代表查詢欄位 Sales 之值的 10 倍，請使用運算式 `=10 * Fields!Sales.Value`。  
  
 對查詢欄位而言，欄位來源必須是由資料集查詢所擷取之現有欄位的名稱。  
  
 **運算式 (fx)**  
 為新的導出欄位加入或變更運算式。 只有在您按一下 **[加入]** ，並選取 **[導出欄位]** 時，此按鈕才會出現。  
  
## <a name="see-also"></a>另請參閱  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [資料集屬性對話方塊、 選項&#40;報表產生器&#41;](report-data/dataset-properties-dialog-box-options-report-builder.md)   
 [資料集屬性對話方塊、 篩選&#40;報表產生器&#41;](../../2014/reporting-services/dataset-properties-dialog-box-filters-report-builder.md)   
 [資料集屬性對話方塊、 參數&#40;報表產生器&#41;](../../2014/reporting-services/dataset-properties-dialog-box-parameters-report-builder.md)   
 [資料集屬性對話方塊、 查詢&#40;報表產生器&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
