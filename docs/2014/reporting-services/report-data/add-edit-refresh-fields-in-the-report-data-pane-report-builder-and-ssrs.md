---
title: 新增、編輯、重新整理報表資料窗格中的欄位 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2e36f0fe-8100-4513-b169-14d611646f81
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 002caf336a45e9b1b8b01e2e1ba2308b05a38378
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62697724"
---
# <a name="add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs"></a>加入、編輯、重新整理報表資料窗格中的欄位 (報表產生器及 SSRS)
  資料集欄位是欄位名稱的內建集合，代表資料集查詢在外部資料來源上執行時所傳回的資料。  
  
 如果是內嵌資料集，資料集欄位就是當您建立查詢並關閉 [查詢設計工具] 窗格之後所建立的欄位，以及您所建立的導出欄位。  
  
 如果是共用資料集，資料集欄位就是當您將共用資料集定義加入至報表時，該定義中的欄位。 雖然當您執行報表時，一定會使用報表伺服器上共用資料集中的查詢，但是報表中的資料集欄位清單是靜態的。  
  
 使用 **[重新整理欄位]** 來更新報表中的欄位清單，以符合共用資料集查詢中的目前欄位清單。 重新整理此欄位清單並不會影響您在報表內定義的導出欄位。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-query-field"></a>若要加入查詢欄位  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料集，然後按一下 [新增查詢欄位]。  
  
    > [!NOTE]  
    >  如果您看不到 [報表資料] 窗格，請按一下 [檢視] 功能表上的 [報表資料]。  
  
2.  在 **[資料集屬性]** 對話方塊的 **[欄位]** 頁面上，按一下 **[加入]**，然後按一下 **[查詢欄位]**。 新的資料列就會加入方格的底部。  
  
3.  在 **[欄位名稱]** 文字方塊中，輸入欄位的名稱。  
  
    > [!NOTE]  
    >  名稱在資料集內必須是唯一的。  
  
4.  在 **[欄位來源]** 文字方塊中，輸入資料來源上現有欄位的名稱。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-calculated-field"></a>加入導出欄位  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料集，然後按一下 [新增導出欄位]。  
  
2.  在 **[資料集屬性]** 對話方塊的 **[欄位]** 頁面上，按一下 **[加入]**，然後按一下 **[導出欄位]**。 新的資料列就會加入方格的底部。  
  
3.  在 **[欄位名稱]** 文字方塊中，輸入欄位的名稱。  
  
    > [!NOTE]  
    >  名稱在資料集內必須是唯一的。  
  
4.  在 **[欄位來源]** 文字方塊中，輸入欄位的運算式。 按一下運算式 (**fx**) 按鈕，即可建立運算式。  
  
    > [!NOTE]  
    >  導出欄位的運算式不能包含報表項目的彙總或參考。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-a-query-field-or-a-dataset-field"></a>編輯查詢欄位或資料集欄位  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下欄位，然後按一下 [欄位屬性]。  
  
2.  在 **[資料集屬性]** 對話方塊的 **[欄位]** 頁面上，按一下現有的欄位來選取資料列。  
  
3.  變更欄位的名稱或欄位的值。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-query-field-or-a-calculated-field"></a>刪除查詢欄位或導出欄位  
  
1.  在 [報表資料] 窗格中，展開資料集來顯示欄位集合。  
  
2.  以滑鼠右鍵按一下您要移除的欄位，然後按一下 [刪除]。  
  
### <a name="to-refresh-the-field-collection-in-the-report-data-pane-for-a-shared-dataset"></a>若要在 [報表資料] 窗格中重新整理共用資料集的欄位集合  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料集，然後按一下 [查詢]。  
  
2.  按一下 **[重新整理欄位]**。  
  
     在報表伺服器上，共用資料集查詢會執行並傳回目前的欄位集合。  
  
## <a name="see-also"></a>另請參閱  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Reporting Services 查詢設計工具](../reporting-services-query-designers.md)   
 [查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)  
  
  
