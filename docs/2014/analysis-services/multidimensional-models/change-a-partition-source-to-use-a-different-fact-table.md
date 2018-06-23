---
title: 變更要使用不同的事實資料表的分割區來源 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7355f5f7430a5e74cd06ffa73c1b6ed68e11a7c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146193"
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>變更分割區來源以使用不同的事實資料表
  當您建立 Cube 的分割區時，您可以選擇要使用不同的事實資料表。 不同資料表可能來自單一資料來源檢視、來自不同資料來源檢視或來自不同資料來源。 資料來源檢視也可能包含來自一個以上之資料來源的不同資料表。  
  
 Cube 分割區的所有事實資料表與維度，必須和 Cube 的事實資料表與維度具有相同結構。 例如，不同的事實資料表可以有相同結構但包含不同年份或不同產品線的資料。  
  
 您可以在分割區精靈的 [指定來源資訊] 頁面上，指定事實資料表。 在這個頁面上，於 [查詢] 旁邊的分割區來源群組中，指定要查看的資料來源或資料來源檢視。 接下來，按一下 [尋找資料表]，然後在 [可用的資料表] 之下，選取您要使用的資料表。  
  
 當您使用不同的事實資料表時，請確定分割區之間沒有重複資料。 例如，若有一個事實資料表只包含 2012 的交易，而另一個事實資料表只包含 2013 的交易，則這些資料表包含獨立資料。 同樣地，不同產品線或不同地理區域的事實資料表也是獨立的。  
  
 您可以 (但不建議) 使用包含重複資料的不同事實資料表。 在此情況下，您必須在資料分割中使用篩選來確保某資料分割使用的資料不會被另一個資料分割使用。 如需詳細資訊，請參閱[建立及管理本機資料分割 &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理本機資料分割&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  