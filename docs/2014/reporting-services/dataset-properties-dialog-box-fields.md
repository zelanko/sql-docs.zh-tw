---
title: 資料集屬性對話方塊、 欄位 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b1c49beb22a3a91e3d42aa7ce4ed99b5e107b4d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956924"
---
# <a name="dataset-properties-dialog-box-fields"></a>資料集屬性對話方塊、欄位
  選取 **[資料集屬性]** 對話方塊上的 **[欄位]** ，即可變更報表資料集的欄位集合。 欄位清單會自動擴展，但您可以使用 **[欄位]** 來加入、編輯和刪除查詢與導出欄位。  
  
## <a name="options"></a>選項。  
 **[加入]**  
 將新的查詢欄位或導出欄位加入到資料集中。  
  
 **刪除**  
 從資料集中刪除選取的欄位。  
  
 **欄位名稱**  
 輸入欄位的名稱。 此欄位在資料集內必須是唯一的。 對於資料集查詢中每個現有的欄位，系統都會預先填入名稱。  
  
 **欄位來源**  
 輸入欄位的值。  
  
 對導出欄位而言，欄位來源必須是資料集查詢所擷取之現有欄位的名稱，或是您建立的運算式。 例如，若要建立欄位來代表查詢欄位 Sales 之值的 10 倍，請使用運算式 `=10 * Fields!Sales.Value`。  
  
 對查詢欄位而言，欄位來源必須是由資料集查詢所擷取之現有欄位的名稱。  
  
 **運算式 (fx)**  
 為導出欄位加入或變更運算式。 只有在您按一下 **[加入]** ，並選取 **[導出欄位]** 時，此按鈕才會出現。  
  
## <a name="see-also"></a>另請參閱  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
