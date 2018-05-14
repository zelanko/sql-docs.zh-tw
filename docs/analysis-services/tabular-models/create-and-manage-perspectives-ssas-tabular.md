---
title: 建立及管理檢視方塊 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 56c8f35aa15debbc064cacd73205234377224a28
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="create-and-manage-perspectives"></a>建立及管理檢視方塊 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  檢視方塊會定義可檢視之模型子集，對模型提供具體的商務特有或應用程式特有視點。 本主題中的工作會描述如何使用模型設計師中的 **[檢視方塊]** 對話方塊，建立及管理檢視方塊。  
  
## <a name="tasks"></a>工作  
 若要建立檢視方塊，請使用 **[檢視方塊]** 對話方塊，即可在其中加入、編輯、刪除、複製及查看檢視方塊。 若要在 **中檢視** [檢視方塊] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]對話方塊，請按一下 **[模型]** 功能表，然後按一下 **[檢視方塊]**。  
  
###  <a name="bkmk_add"></a> 加入檢視方塊  
  
-   若要加入新檢視方塊，請按一下 **[新增檢視方塊]**。 即可核取或取消核取要包含的欄位物件，並提供新檢視方塊的名稱。  
  
     如果您建立空白檢視方塊 (已取消核取所有欄位物件)，則使用此檢視方塊的使用者會看到空白的欄位清單。 檢視方塊應該至少包含一個資料表和一個資料行。  
  
###  <a name="bkmk_edit"></a> 若要編輯檢視方塊  
  
-   若要修改檢視方塊，請在檢視方塊的資料行中核取及取消核取欄位，如此即可在檢視方塊中加入和移除欄位物件。  
  
###  <a name="bkmk_rename"></a> 重新命名檢視方塊  
  
-   當您將滑鼠停留在檢視方塊的資料行標頭 (檢視方塊的名稱) 上方時，[重新命名] 按鈕隨即顯示。 若要重新命名檢視方塊，請按一下 **[重新命名]**，然後輸入新名稱或編輯現有名稱。  
  
###  <a name="bkmk_delete"></a> 刪除檢視方塊  
  
-   當您將滑鼠停留在檢視方塊的資料行標頭 (檢視方塊的名稱) 上方時，[刪除] 按鈕隨即顯示。 若要刪除檢視方塊，請按一下 **[刪除]** 按鈕，然後在確認視窗中按一下 **[是]** 。  
  
###  <a name="bkmk_copy"></a> 複製檢視方塊  
  
-   當您將滑鼠停留在檢視方塊的資料行標頭上方時， **[複製]** 按鈕隨即顯示。 若要複製檢視方塊，請按一下 **[複製]** 按鈕。 在現有檢視方塊的右邊就會加入選定檢視方塊的副本，做為新檢視方塊。 新檢視方塊會繼承原本檢視方塊的名稱，並且於名稱結尾處加上 *- 複本* 註記。 例如，建立 *Sales* 檢視方塊的副本時，新的檢視方塊名稱會是 *Sales – 複製*。  
  
## <a name="see-also"></a>另請參閱  
 [檢視方塊](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [階層架構](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
