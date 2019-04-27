---
title: 處理插入、更新與刪除 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],processing data
ms.assetid: 13a84d21-2623-4efe-b442-4125a7a2d690
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 24ab4d509638b3195c7105602c663c04fb47a411
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771124"
---
# <a name="process-inserts-updates-and-deletes"></a>處理插入、更新與刪除
  在執行累加式變更資料載入之 Integration Services 封裝的資料流程中，第二個工作是分隔插入、更新與刪除。 然後，您可以使用適當的命令，將其套用到目的地。  
  
> [!NOTE]  
>  設計執行累加式變更資料載入之封裝資料流程的第一個工作是，設定執行擷取變更資料之查詢的來源元件。 如需此元件的詳細資訊，請參閱[擷取與了解變更資料](retrieve-and-understand-the-change-data.md)。 如需建立可執行累加式變更資料載入之封裝的完整程序描述，請參閱[異動資料擷取 &#40;SSIS&#41;](change-data-capture-ssis.md)。  
  
## <a name="associating-friendly-values-to-separate-inserts-updates-and-deletes"></a>將易記值與個別的插入、更新與刪除產生關聯  
 在擷取變更資料的範例查詢中，**cdc.fn_cdc_get_net_changes_<擷取執行個體>** 函數僅會傳回名稱為 **__$operation** 之中繼資料的資料行。 此中繼資料行包含表示哪個作業造成變更的序數值。  
  
> [!NOTE]  
>  如需使用呼叫 **cdc.fn_cdc_get_net_changes_<擷取執行個體>** 函數之查詢的詳細資訊，請參閱[建立函數以擷取變更資料](create-the-function-to-retrieve-the-change-data.md)。  
  
 比對序數值及其對應作業的方式不像使用作業的助憶鍵那麼容易。 例如，'D' 可以輕易地表示刪除作業，而 'I' 則表示插入作業。 在＜ [建立函數以擷取變更資料](create-the-function-to-retrieve-the-change-data.md)＞主題中建立的範例查詢可以進行從序數值轉換為在新資料行中傳回之易記字串值的這個轉換。 下列程式碼區段會示範這項轉換：  
  
```  
select   
    ...  
    case __$operation  
        when 1 then 'D'  
        when 2 then 'I'  
        when 4 then 'U'  
        else null  
     end as CDC_OPERATION  
```  
  
## <a name="configuring-a-conditional-split-transformation-to-direct-inserts-updates-and-deletes"></a>將條件式分割轉換設定為直接插入、更新與刪除  
 若要將變更資料的資料列直接轉換為三種輸出之一，「條件式分割」轉換最為理想。 此轉換只會檢查每個資料列中 **CDC_OPERATION** 資料行的值，然後判斷該變更為插入、更新還是刪除。  
  
> [!NOTE]  
>  CDC_OPERATION 資料行包含從 **__$operation** 資料行中之數值衍生的易記字串值。  
  
#### <a name="to-split-inserts-updates-and-deletes-for-processing-by-using-a-conditional-split-transformation"></a>使用條件式分割轉換分割要處理的插入、更新與刪除  
  
1.  在 **[資料流程]** 索引標籤上，加入「條件式分割」轉換。  
  
2.  將 OLE DB 來源的輸出連接到「條件式分割」轉換。  
  
3.  在 **[條件式分割轉換編輯器]** 的下方窗格中，輸入下列三行以指定三種輸出  
  
    1.  針對直接插入的資料列，將條件為 `CDC_OPERATION == "I"` 的行輸入到插入的輸出。  
  
    2.  針對直接更新的資料列，將條件為 `CDC_OPERATION == "U"` 的行輸入到更新的輸出。  
  
    3.  針對直接刪除的資料列，將條件為 `CDC_OPERATION == "D"` 的行輸入到刪除的輸出。  
  
## <a name="next-step"></a>下一個步驟  
 分割要處理的資料列後，下一個步驟是將變更套用到目的地。  
  
 **下一個主題：**[將變更套用到目的地](apply-the-changes-to-the-destination.md)  
  
## <a name="see-also"></a>另請參閱  
 [條件式分割轉換](../data-flow/transformations/conditional-split-transformation.md)   
 [使用條件式分割轉換來分割資料集](../data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
