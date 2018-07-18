---
title: 全文檢索索引屬性 （排程頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.schedule.f1
ms.assetid: a828e284-097e-4854-8c49-931934eb73bf
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 83eeb3ca9ea1f2e22f3d2dadf8089b8ba510c951
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306228"
---
# <a name="full-text-index-properties-schedules-page"></a>全文檢索索引屬性 (排程頁面)
  您可以使用這個頁面來檢視和建立執行 SQL Server Agent 作業的排程，以便針對全文檢索索引的基底資料表啟動更新的累加母體擴展。 如果基底資料表或檢視表不包含的資料行`timestamp`資料類型，會執行完整母體擴展。  
  
 **若要檢視或變更全文檢索索引的屬性**  
  
-   [管理全文檢索索引](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>UIElement 清單  
 **排程**  
 針對全文檢索索引的基底資料表列出每個排程的累加母體擴展 (如果有的話)。  
  
 **名稱**  
 顯示每個排程母體擴展的名稱。  
  
 **母體類型**  
 顯示每個排程母體擴展的類型。  
  
 **已啟用**  
 指出排程的母體擴展目前為啟用或停用。  
  
 **說明**  
 顯示建立排程時所指定的描述。  
  
 **新增**  
 按一下即可建立擴展全文檢索索引的新排程。  
  
## <a name="see-also"></a>另請參閱  
 [使用全文檢索索引精靈](../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [擴展全文檢索索引](../relational-databases/search/populate-full-text-indexes.md)  
  
  
