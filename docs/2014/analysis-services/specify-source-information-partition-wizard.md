---
title: 指定來源資訊 （資料分割精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aca14c9462d847d91ae2b51dfdf179650ee06732
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068165"
---
# <a name="specify-source-information-partition-wizard"></a>指定來源資訊 (資料分割精靈)
  使用 [指定來源資訊]  頁面，即可選取要在其中建立資料分割 (以及該資料分割的資料來源檢視和篩選資料表) 的量值群組。  
  
> [!CAUTION]  
>  如果您在另一個資料分割所用的 [可用的資料表]  中指定資料表，就必須在 [限制資料列]  頁面中提供查詢，或承擔 Cube 中有重複資料的風險。  
  
## <a name="options"></a>選項。  
 **量值群組**  
 選取此分割區的量值群組。  
  
 **Look in**  
 選取包含此資料分割之來源資料表的資料來源或資料來源檢視。 依預設，會選取量值群組所用的資料來源檢視。  
  
 **篩選資料表**  
 輸入用於 (依資料表名稱) 限制 [可用的資料表]  中顯示之資料表的字串。  
  
 **尋找資料表**  
 選取即可重新整理 [可用的資料表]  中的資料表清單，如果在 [篩選資料表]  中指定了字串，就可以進一步限制清單。  
  
 **可用的資料表**  
 選取用來作為資料分割之來源資料表的資料表。 [資料分割精靈]  會為在 [可用的資料表]  中選取的每個資料表建立一個資料分割。  
  
 如果未在 [篩選資料表]  中指定篩選，此選項會列出在 [查詢]  中指定之資料來源或資料來源檢視中的所有資料表，其結構類似於在 [量值群組]  中指定之量值群組所用的事實資料表。  
  
 如果在 [篩選資料表]  中指定篩選，就會藉由比較篩選與符合先前準則的資料表名稱，來進一步限制此清單。 顯示只有包含 **[篩選資料表]** 中指定之字串的資料表。  
  
> [!NOTE]  
>  如果選取一個以上的資料表，就無法顯示 [限制資料列]  頁面，而且無法限制從所選資料表建立之資料分割的資料列。 若要限制每個資料分割的資料列，請為要建立資料分割的每個資料表執行一次資料分割精靈。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
