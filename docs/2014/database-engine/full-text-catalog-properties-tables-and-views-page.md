---
title: 全文檢索目錄屬性 （資料表和檢視頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e0e73607bf54d066c0328ae45785151ceaa2cca1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298910"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>全文檢索目錄屬性 (資料表和檢視頁面)
  使用此對話方塊以檢視或修改指派給全文檢索目錄的資料表和檢視。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **此資料庫中的所有適合的資料表/檢視物件**  
 列出已定義唯一索引的資料表和檢視，但還不屬於全文目錄的一部份。 若要選取資料表或檢視並將其指派給目錄，請在清單方塊中選取項目，並按下「->」按鈕。  
  
 **指派給目錄的資料表/檢視物件**  
 列出目前已指派給全文檢索目錄的資料表和檢視  
  
## <a name="selected-object-properties"></a>選取的物件屬性  
 **選取的物件屬性**  
 在已指派給目錄的物件清單方塊中，顯示選取之物件的屬性。  
  
 **唯一索引**  
 列出資料表或檢視可用的唯一索引。  
  
 **資料表的全文檢索已啟用**  
 選取此核取方塊，以啟用資料表的全文檢索索引。 清除核取方塊以停用全文檢索索引。  
  
## <a name="eligible-columns-grid"></a>適合的資料行方格  
  
|||  
|-|-|  
|**可用的資料行**|顯示已全文檢索索引的所有資料行。 選取核取方塊以將資料行加入全文檢索索引。|  
|**斷詞工具的語言**|顯示斷詞工具的語言。|  
|**資料類型資料行**|列出資料行文件類型中所列的資料行的資料表中的資料行的名稱**可用的資料行**資料行是否`varbinary(max)`或`image`資料行。|  
|**統計語意**|選取是否要針對選取的資料行啟用語意索引。 如需詳細資訊，請參閱[語意搜尋 &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md)。<br /><br /> 如果您在選取 **[統計語意]** 之前選取 **[語言]**，而且選取的語言沒有相關聯的語意語言模型，則會停用 **[統計語意]** 核取方塊。 如果您在選取 [語言] 之前選取 [統計語意]，則下拉式方塊中提供的語言將受限為有語意語言模型支援的語言。|  
  
## <a name="track-changes"></a>追蹤變更  
  
|||  
|-|-|  
|**自動**|當修改、加入或刪除基礎資料表中的資料時，全文檢索索引會自動更新。|  
|**手動**|當修改、 新增或刪除索引的資料，在資料[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會追蹤變更。 **[手動]** 變更追蹤生效時，索引不會自動更新這些變更。 相反地，系統管理員可以手動套用變更使用[ALTER FULLTEXT INDEX...START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql)陳述式。|  
|**不要追蹤變更**|此選項生效時，不會記錄目錄中索引資料的變更。 管理員必須使用 ALTER FULLTEXT INDEX 搭配 FULL POPULATION 或 INCREMENTAL POPULATION 來建立索引。|  
  
## <a name="see-also"></a>另請參閱  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [擴展全文檢索索引](../relational-databases/indexes/indexes.md)  
  
  
