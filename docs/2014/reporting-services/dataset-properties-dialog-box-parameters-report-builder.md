---
title: 資料集屬性對話方塊、參數（報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 295a40bc7964e50e5fc0c4a9ea0294b593fdde18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109385"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>資料集屬性對話方塊、參數 (報表產生器)
  選取 [**資料集屬性**] 對話方塊上的 [**參數**] 來加入、變更和刪除查詢參數。  
  
 內嵌資料集的選項適用於報表定義中的資料集。  
  
 共用資料集的選項則適用於報表伺服器上的共用資料集定義。  
  
 如需詳細資訊，請參閱[內嵌和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項。  
 **加入**  
 將新的參數加入到清單中。  
  
 **刪除**  
 從清單中移除選取的參數。  
  
 **向上箭頭**  
 將清單中所選取的參數向上移動。  
  
 **向下箭頭**  
 將清單中所選取的參數向下移動。  
  
 **參數名稱**  
 在 [資料集屬性]  對話方塊的 [查詢]  索引標籤上，輸入您要加入到資料集之查詢參數的名稱。  
  
 **參數值**  
 僅適用於內嵌資料集。  
  
 輸入查詢參數的值。 這可為靜態值或參考報表內之物件的運算式，但是它不可以參考任何報表項目或欄位。 根據預設， **[值]** 包含指向報表參數的運算式。  
  
 **預設值**  
 僅適用於共用資料集。  
  
 選取此核取方塊以指定預設值。  
  
 輸入預設值。 這可以是靜態值或參考報表內之物件的運算式。 此運算式無法參照報表項目、報表參數或欄位。  
  
 若要指定空白，請將文字方塊留空。  
  
 若要指定一個 Null，選取 [可為 Null] 選項。  
  
 **唯讀**  
 僅適用於共用資料集。  
  
 選取此選項，將此參數在共用資料集定義中標示為唯讀。 將共用資料集加入至報表時，參數不會出現在屬性中。 在報表伺服器上快取共用資料集時，無法變更值。  
  
 **Nullable**  
 僅適用於共用資料集。  
  
 選取此選項以允許 Null 值。  
  
 **從查詢中忽略**  
 僅適用於共用資料集。  
  
 當報表參數的參考位於共用資料集篩選 (而非查詢) 中的運算式時，請選取此選項。 當您選取這個選項時，您不需要在執行查詢時，指定這個參數的預設值。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和嚮導的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [資料集屬性對話方塊、查詢 &#40;報表產生器&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [查詢設計工具 &#40;報表產生器&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [建立共用資料集或內嵌資料集 &#40;報表產生器和 SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
