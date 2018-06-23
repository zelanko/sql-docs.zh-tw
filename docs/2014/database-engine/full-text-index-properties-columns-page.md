---
title: 全文檢索索引屬性 （資料行頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.columns.f1
ms.assetid: 75e52edb-0d07-4393-9345-8b5af4561e35
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 223a3e0db58b73f2b841cebd23d41bc36ba4a85b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031085"
---
# <a name="full-text-index-properties-columns-page"></a>全文檢索索引屬性 (資料行頁面)
  **若要檢視或變更全文檢索索引的屬性**  
  
-   [管理全文檢索索引](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>UIElement 清單  
 **唯一索引**  
 從下拉式清單中選取索引。 索引必須是單一索引鍵資料行、唯一的且不可以是 Null 的索引。  
  
 **選取適合將全文檢索索引的資料行**  
 此方格會顯示可用於這個全文檢索索引的資料表資料行。 目前已建立全文檢索索引的資料行都會處於已核取狀態。 另外，您可以核取想要建立全文檢索索引的其他資料行。  
  
> [!IMPORTANT]  
>  請確定至少核取了一個資料行，然後再按一下 [確定]。  
  
|||  
|-|-|  
|**可用的資料行**|資料行名稱。|  
|**斷詞工具的語言**|斷詞工具及字幹分析器會在所有全文檢索索引資料上執行語言分析的語言。<br /><br /> 如需詳細資訊，請參閱[設定和管理的斷詞工具與字幹分析器搜尋](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)和[選擇語言時建立的全文檢索索引](../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。|  
|**型別**|資料表資料行的名稱，此資料行會保存已選取之資料行的文件類型。 這是一個唯讀屬性。|  
|**統計語意**|選取是否要針對選取的資料行啟用語意索引。 如需詳細資訊，請參閱[語意搜尋 &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md)。<br /><br /> 如果您在選取 **[統計語意]** 之前選取 **[語言]**，而且選取的語言沒有相關聯的語意語言模型，則會停用 **[統計語意]** 核取方塊。 如果您在選取 [語言] 之前選取 [統計語意]，則下拉式方塊中提供的語言將受限為有語意語言模型支援的語言。|  
  
## <a name="see-also"></a>另請參閱  
 [擴展全文檢索索引](../relational-databases/search/populate-full-text-indexes.md)  
  
  