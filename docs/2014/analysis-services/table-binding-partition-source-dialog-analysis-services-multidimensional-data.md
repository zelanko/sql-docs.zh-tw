---
title: 資料表系結詳細資料（資料分割來源對話方塊）（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitiontableselection.f1
ms.assetid: 67d05389-81ae-4a6b-947b-986d37ec72b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f8ea36c8c3d49d4903379ed4450548fc760937a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067873"
---
# <a name="table-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>資料表繫結詳細資料 (資料分割來源對話方塊) (Analysis Services - 多維度資料)
  使用 **[資料分割來源]** 對話方塊中的 **[資料表繫結]** 選項，即可指定提供資料給資料分割的事實資料表。 您可以從 **[資料分割來源]** 對話方塊的 **[繫結類型]** 選項中，選取 **[資料表繫結]** 來顯示此窗格。  
  
## <a name="options"></a>選項。  
 **量值群組**  
 顯示此資料分割的量值群組。  
  
 **Look in**  
 選取包含此資料分割之來源資料表的資料來源或資料來源檢視。 依預設，會選取所選量值群組使用的資料來源檢視。  
  
 **篩選資料表**  
 輸入用於 (依資料表名稱) 限制 [可用的資料表]**** 中顯示之資料表的字串。  
  
 **尋找資料表**  
 選取即可重新整理 [可用的資料表]**** 中的資料表清單，如果在 [篩選資料表]**** 中指定了字串，就可以進一步限制清單。  
  
 **可用的資料表**  
 按一下即可選取資料表，用來作為資料分割的來源資料表。  
  
 如果在 **[篩選資料表]** 中沒有指定篩選，就會列出在 **[查詢]** 中指定的資料來源或資料來源檢視內、結構與 **[量值群組]** 中所指定量值群組使用之事實資料表類似的所有資料表。  
  
 如果在 **[篩選資料表]** 中有指定篩選，將藉由比較篩選與符合上述準則的資料表名稱，來進一步限制清單。 顯示只有包含 **[篩選資料表]** 中指定之字串的資料表。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割來源對話方塊 &#40;Analysis Services-多維度資料&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
