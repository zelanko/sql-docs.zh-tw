---
title: "OLE DB 結構描述資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [OLE DB]
- schema rowsets [Analysis Services], OLE DB
- OLE DB schema rowsets
- rowsets [Analysis Services], OLE DB
ms.assetid: ca2ee87a-ba04-4501-9125-33934c58ab31
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6467a1e54dba2ad8a4e88f1d892dfa2f3cd64381
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="ole-db-schema-rowsets"></a>OLE DB 結構描述資料列集
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者支援下列 OLE DB 結構描述資料列集。 使用**DISCOVER_ENUMERATORS**含有資料列集[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法來檢查特定資料來源提供者是否支援資料列集。  
  
 您也可以在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 網站上於 MSDN® Library 的「OLE DB 程式設計人員參考」部分中，藉由搜尋「結構描述資料列集」主題，來尋找有關這些資料列集的詳細資訊。  
  
 下表描述此結構描述資料列集。  
  
|資料列集|Description|  
|------------|-----------------|  
|**DBSCHEMA_ASSERTIONS**|識別在目錄中所定義且由指定使用者所擁有的判斷提示。|  
|[DBSCHEMA_CATALOGS 資料列集](../../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md) <sup>1</sup>|識別與可從資料庫管理系統 (DBMS) 存取之目錄相關聯的實體屬性。 某些系統 (例如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access) 可能只有一個目錄。 對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，這個資料列集會列舉定義在系統資料庫中的所有目錄 (資料庫)。|  
|**DBSCHEMA_CHARACTER_SETS**|識別在目錄中所定義且可由指定使用者存取的字元集。|  
|**DBSCHEMA_CHECK_CONSTRAINTS**|識別在目錄中所定義且由指定使用者所擁有的檢查條件約束。|  
|**DBSCHEMA_CHECK_CONSTRAINTS_BY_TABLE**|識別在目錄中所定義且由指定使用者所擁有之指定資料表的檢查條件約束。|  
|**DBSCHEMA_COLLATIONS**|識別在目錄中所定義且可由指定使用者存取的字元定序。|  
|**DBSCHEMA_COLUMN_DOMAIN_USAGE**|識別在目錄中所定義的資料行，這些資料行會相依於目錄中定義的網域，並且由指定使用者擁有。|  
|**DBSCHEMA_COLUMN_PRIVILEGES**|識別在目錄中所定義資料表之資料行上的權限；指定之使用者可以取得或授與這些權限。|  
|[DBSCHEMA_COLUMNS 資料列集](../../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md) <sup>1</sup>|為所有符合提供之限制準則的資料行提供資料行資訊。|  
|**DBSCHEMA_CONSTRAINT_COLUMN_USAGE**|識別參考條件約束、唯一條件約束、檢查條件約束和判斷提示所使用的資料行 (定義在目錄中，並且由指定使用者所擁有)。|  
|**DBSCHEMA_CONSTRAINT_TABLE_USAGE**|識別參考條件約束、唯一條件約束、檢查條件約束和判斷提示所使用的資料表 (定義在目錄中，並且由指定使用者所擁有)。|  
|**DBSCHEMA_FOREIGN_KEYS**|識別由指定使用者在目錄中定義的外部索引鍵資料行。 此結構描述資料列集是建立在數個 ISO 結構描述檢視上，以便於非 SQL 程式設計人員使用。 如果支援，此結構描述資料列集必須同步處理具有相關的 ISO 檢視 (**REFERENTIAL_CONSTRAINTS**和**CONSTRAINT_COLUMN_USAGE**)。|  
|**DBSCHEMA_INDEXES**|識別在目錄中所定義且由指定使用者所擁有的索引。|  
|**DBSCHEMA_KEY_COLUMN_USAGE**|識別在目錄中所定義且由指定使用者以條件約束為索引鍵的資料行。|  
|**DBSCHEMA_PRIMARY_KEYS 完全相同**|識別由指定使用者在目錄中定義的主索引鍵資料行。 此結構描述資料列集是建立在 ISO 結構描述檢視上，以便於非 SQL 程式設計人員使用。 如果支援，此結構描述資料列集必須同步處理具有相關的 ISO 檢視 (**CONSTRAINT_COLUMN_USAGE**)。|  
|**DBSCHEMA_PROCEDURE_COLUMNS**|會傳回由程序所傳回資料列集之資料行的相關資訊。|  
|**DBSCHEMA_PROCEDURE_PARAMETERS**|會傳回程序的參數和傳回碼的相關資訊。|  
|**DBSCHEMA_PROCEDURES**|識別在目錄中所定義且由指定使用者所擁有的程序。 這是一種 OLE DB 延伸模組。|  
|[DBSCHEMA_PROVIDER_TYPES 資料列集](../../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md) <sup>1</sup>|識別資料提供者所支援的 (基底) 資料類型。|  
|**DBSCHEMA_REFERENTIAL_CONSTRAINTS**|識別在目錄中所定義且由指定使用者所擁有的參考條件約束。|  
|**DBSCHEMA_SCHEMATA**|識別由指定使用者所擁有的結構描述。|  
|**DBSCHEMA_SQL_LANGUAGES**|識別由目錄中定義的 SQL 實作處理資料所支援的一致性層級、選項和用語。|  
|**DBSCHEMA_STATISTICS**|識別在目錄中所定義且由指定使用者所擁有的統計資料。<br /><br /> 此資料表不相關**TABLE_STATISTICS**資料列集。|  
|**DBSCHEMA_TABLE_CONSTRAINTS**|識別在目錄中所定義且由指定使用者所擁有的資料表條件約束。|  
|**DBSCHEMA_TABLE_PRIVILEGES**|識別在目錄中所定義資料表之資料行上的權限，並由指定使用者取得或授與這些權限。|  
|**DBSCHEMA_TABLE_STATISTICS**|描述在提供者中可用之資料表上的統計資料集。<br /><br /> 此資料列集不相關**統計資料**資料列集。|  
|[DBSCHEMA_TABLES 資料列集](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) <sup>1</sup>|識別的量值群組和維度內公開為資料表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|**DBSCHEMA_TABLES_INFO** <sup>1</sup>|識別在目錄中所定義且可由指定使用者存取的資料表 (包括檢視表)。|  
|**DBSCHEMA_TRANSLATIONS**|識別在目錄中所定義且可由指定使用者存取的字元翻譯。|  
|**DBSCHEMA_TRUSTEE**|列舉資料來源的信任項。|  
|**DBSCHEMA_USAGE_PRIVILEGES**|識別**使用量**目錄中所定義且可用或已授與指定之使用者的物件上的權限。|  
|**DBSCHEMA_VIEW_COLUMN_USAGE**|識別定義在目錄中且可由指定使用者存取的檢視表。|  
|**DBSCHEMA_VIEW_TABLE_USAGE**|識別檢視之資料表 (定義在資料庫目錄中，並且由指定使用者所擁有) 相依的資料表。|  
|**DBSCHEMA_VIEWS**|識別定義在目錄中且可由指定使用者存取的檢視表。|  
  
 <sup>1</sup>指出支援的 MSOLAP 資料來源提供者的結構描述資料列集[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XMLA 提供者。  
  
## <a name="see-also"></a>另請參閱  
 [DISCOVER_ENUMERATORS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Analysis Services 結構描述資料列集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

