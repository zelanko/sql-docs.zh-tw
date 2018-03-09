---
title: "資料集屬性對話方塊、參數 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10150"
- sql13.rtp.rptdesigner.datasetproperties.parameters.f1
- "10023"
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
caps.latest.revision: "40"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 07882659f3ead59efe15d02ede109b6cae11ba29
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="dataset-properties-dialog-box-parameters"></a>資料集屬性對話方塊、參數
  選取 **[資料集屬性]** 對話方塊上的 **[參數]** 來加入、變更與刪除查詢參數，包括連結到報表參數的查詢參數。  
  
 每當在查詢索引標籤上變更查詢時，系統就會剖析查詢命令。 系統會針對已識別的每個查詢參數，建立含有相同之區分大小寫名稱的報表參數。 根據預設，系統會將查詢參數自動加入到查詢參數清單中，並連結到對應的報表參數。  
  
 如果有一個報表參數的預設值相依於另一個連結到查詢參數的報表參數，報表參數的順序 (出現在 [報表參數屬性] 對話方塊中的順序) 很重要。 稍後在清單中的報表參數可以參照先前在清單中的報表參數。 如需報表參數的詳細資訊，請參閱 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
## <a name="options"></a>選項。  
 **[加入]**  
 將新的參數加入到清單中。  
  
 **刪除**  
 從清單中移除選取的參數。  
  
 **參數名稱**  
 在 [資料集屬性] 對話方塊的 [查詢] 索引標籤上，輸入您要加入到資料集之查詢參數的名稱。  
  
 **參數值**  
 輸入查詢參數的值。 這可為靜態值或參考報表內之物件的運算式，但是它不可以參考任何報表項目或欄位。 根據預設， **[值]** 包含指向報表參數的運算式。  
  
 **向上箭頭**  
 將清單中所選取的參數向上移動。  
  
 **向下箭頭**  
 將清單中所選取的參數向下移動。  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
