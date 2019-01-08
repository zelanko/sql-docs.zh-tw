---
title: 記錄和提供者提供的欄位 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c64555e0035de8a06d3bb9227262f4202f73f9a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538037"
---
# <a name="records-and-provider-supplied-fields"></a>記錄和提供者提供的欄位
當[記錄](../../../ado/reference/ado-api/record-object-ado.md)開啟物件、 其來源可以是已開啟的目前資料列[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，絕對 URL 或開啟搭配的相對 URL[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件.  
  
 如果**記錄**從開啟**資料錄集**，則**記錄**物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合將包含從的所有欄位**資料錄集**，再加上任何新增的基礎提供者的欄位。  
  
 提供者可能會插入額外的欄位做為補充特性**記錄**。 如此一來，**記錄**可能會有唯一的欄位中則不**資料錄集**做為整體或任何**記錄**衍生自另一個資料列的**資料錄集**.  
  
 例如的所有資料列**資料錄集**衍生自資料來源可能會有資料行這類 From、、 和主旨的電子郵件。 A**記錄**衍生自該**資料錄集**會有相同的欄位。 不過，**記錄**可能也有其他欄位所代表的特定訊息的唯一**記錄**，例如附件] 和 [副本 （副本）。  
  
 雖然**記錄**物件和目前資料列**資料錄集**具有相同的欄位，它們是不同因為**記錄**並**資料錄集**物件有不同的方法和屬性。  
  
 所持有的共通的欄位**記錄**並**資料錄集**可以修改其中一個物件上。 不過，無法刪除欄位，在**記錄**物件，雖然基礎提供者可能支援將欄位設定為 null。  
  
 在後**記錄**會開啟，您可以透過程式設計方式加入欄位。 您也可以刪除欄位，您已新增，但您無法刪除欄位，從原始**資料錄集**。  
  
 您也可以開啟**記錄**直接從 URL 的物件。 在此情況下，將欄位加入至**記錄**取決於基礎提供者。 目前，大部分的提供者加入一組描述所代表之實體的欄位**記錄**。 如果實體組成的資料流的位元組，簡單的檔案，例如[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件通常可以從開啟**記錄**。  
  
## <a name="special-fields-for-document-source-providers"></a>文件的特殊欄位來源提供者  
 是特殊類別的提供者，呼叫*文件來源提供者*、 管理資料夾和文件。 當**記錄**物件表示文件或**資料錄集**物件表示文件的資料夾、 文件的來源提供者會填入這些物件具有一組唯一的描述欄位文件的特性而是實際文件本身。 一般而言，一個欄位包含的參考**Stream**表示的文件。  
  
 這些欄位會構成資源**記錄**或是**資料錄集**並列出特定提供者支援在[附錄 a:提供者](../../../ado/guide/appendixes/appendix-a-providers.md)。  
  
 兩個常數索引**欄位**的資源集合**記錄**或是**資料錄集**擷取有兩個常用的欄位。 **欄位**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性會傳回所需的內容。  
  
-   使用存取的欄位**adDefaultStream**常數包含相關聯的預設資料流**記錄**或是**資料錄集**物件。 提供者會指派給物件的預設資料流。  
  
-   使用存取的欄位**adRecordURL**常數包含識別文件的絕對 URL。  
  
 文件的來源提供者不支援[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**記錄**並**欄位**物件。 內容**屬性**集合是這類物件則為 null。  
  
 文件的來源提供者可能會新增提供者特定屬性例如**資料來源類型**識別是否文件的來源提供者。 如需如何判斷您的提供者類型的詳細資訊，請參閱您的提供者文件。  
  
## <a name="resource-recordset-columns"></a>資源資料錄集資料行  
 A*資源的資料錄集*下列資料行所組成。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|唯讀。 表示資源的 URL。|  
|RESOURCE_PARENTNAME|AdVarWChar|唯讀。 表示父記錄的絕對 URL。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|唯讀。 表示資源，也就是串連 PARENTNAME 和 PARSENAME 絕對的 URL。|  
|RESOURCE_ISHIDDEN|adBoolean|如果資源已隱藏，則為 true。 除非明確地建立資料列集的命令會選取其中 RESOURCE_ISHIDDEN 為 True 的資料列，則會不傳回任何資料列。|  
|RESOURCE_ISREADONLY|adBoolean|如果資源是唯讀，則為 true。 嘗試開啟此資源 DBBINDFLAG_WRITE 與將會失敗並 DB_E_READONLY。 可以編輯這個屬性，即使資源只開啟進行讀取。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|表示文件的可能用法-例如諮詢法律顧問的簡短。 這可能會對應至 Office 範本用來建立文件。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|表示 MIME 類型的文件，表示的格式，例如"`text/html`」。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|表示用來儲存內容的語言。|  
|RESOURCE_CREATIONTIME|adFileTime|唯讀。 指示 FILETIME 結構，其中包含已建立資源的時間。 被報告的時間，格式為 Coordinated Universal Time (UTC)。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|唯讀。 指示 FILETIME 結構，其中包含上次存取資源的時間。 時間是 UTC 格式。 FILETIME 成員都是零，如果提供者不支援這個時間成員。|  
|RESOURCE_LASTWRITETIME|AdFileTime|唯讀。 指示 FILETIME 結構，其中包含資源的上次寫入時間。 時間是 UTC 格式。 FILETIME 成員都是零，如果提供者不支援這個時間成員。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|唯讀。 表示資源的預設資料流，以位元組為單位的大小。|  
|RESOURCE_ISCOLLECTION|adBoolean|唯讀。 如果資源是集合，例如目錄，則為 true。 如果資源是簡單的檔案，則為 false。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|如果資源是結構化文件，則為 true。 如果資源不是結構化文件，則為 false。 可能是簡單的檔案或集合。|  
|DEFAULT_DOCUMENT|AdVarWChar|唯讀。 表示此資源包含資料夾的預設簡單文件或結構化文件的 URL。 預設資料流所要求資源時使用。 這個屬性是空白的簡單的檔案。|  
|CHAPTERED_CHILDREN|adChapter|唯讀。 選擇性。 表示資料列集包含資源的子系的章節。 ( *OLE DB Provider for Internet Publishing*不會使用此資料行。)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|唯讀。 表示資源的顯示名稱。|  
|RESOURCE_ISROOT|adBoolean|唯讀。 如果資源是集合或結構化文件的根目錄，則為 true。|  
  
## <a name="see-also"></a>另請參閱  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
