---
title: 變更 DirectQuery 資料分割（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9df1e66-dd23-41b4-95eb-af110d10eda4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eb0b6349eac28bbd2abc22b9483ef74edf1bf33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088185"
---
# <a name="change-the-directquery-partition-ssas-tabular"></a>變更 DirectQuery 資料分割 (SSAS 表格式)
  因為資料表中只有一個資料分割可以指定為 DirectQuery 資料分割，所以根據預設，Analysis Services 會使用資料表中建立的第一個資料分割。 在模型專案撰寫期間，您可以藉由使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的 [資料分割管理員] 對話方塊來變更 DirectQuery 資料分割。 如果是部署的模型，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]來變更 DirectQuery 資料分割。  
  
### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>變更表格式模型專案的 DirectQuery 資料分割  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，於模型設計師中按一下包含分割資料表的資料表 (標籤)。  
  
2.  按一下 **[資料表]** 功能表，然後按一下 **[資料分割]**。  
  
3.  在 [資料分割管理員]**** 中，作為目前直接查詢資料分割的資料分割是由資料分割名稱上的前置詞 **(DirectQuery)** 所表示。  
  
     從 [資料分割]**** 清單中選取其他資料分割，然後按一下 [設為 DirectQuery]****。 選取目前的 DirectQuery 資料分割時，[設為 DirectQuery]**** 按鈕不會啟用，而且在模型尚未啟用直接查詢模式時，看不到此按鈕。  
  
4.  如果需要，請變更處理選項，然後按一下 [確定]****。  
  
### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>變更已部署的表格式模型的 DirectQuery 資料分割  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的物件總管中，開啟模型資料庫。  
  
2.  展開 [資料表]**** 節點，然後以滑鼠右鍵按一下資料分割資料表，再選取 [資料分割]****。  
  
     指定用於 DirectQuery 模式的資料分割在資料分割名稱上具有前置詞 (DirectQuery)。  
  
3.  若要變更為其他資料分割，請按一下 [直接查詢]**** 工具列圖示以開啟 [設定 DirectQuery 資料分割]**** 對話方塊。 在尚未啟用直接查詢的模型上，無法使用 DirectQuery 工具列圖示。  
  
4.  從 [資料分割名稱]**** 下拉式清單中選擇其他資料分割，然後視需要變更該資料分割的處理選項。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;SSAS 表格式&#41;](tabular-models/partitions-ssas-tabular.md)  
  
  
