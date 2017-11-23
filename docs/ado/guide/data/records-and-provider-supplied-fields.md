---
title: "記錄和提供者提供的欄位 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 16596d3ffa943f382e6c3a9ec2aa9c2e2e14432f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="records-and-provider-supplied-fields"></a>記錄和提供者提供的欄位
當[記錄](../../../ado/reference/ado-api/record-object-ado.md)開啟物件，其來源可以是目前已開啟的資料列[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，絕對 URL 或相對 URL 開啟搭配[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件.  
  
 如果**記錄**開啟從**資料錄集**、**記錄**物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合會包含從的所有欄位**資料錄集**，再加上由基礎提供者加入任何欄位。  
  
 提供者可能會插入額外的欄位做為補充特性**記錄**。 如此一來，**記錄**可能會有唯一的欄位中則不**資料錄集**以整個或任何**記錄**衍生自另一個資料列的**資料錄集**.  
  
 例如，所有資料列的**資料錄集**衍生自資料來源可能會有資料行這類做為從，和主旨的電子郵件。 A**記錄**衍生自該**資料錄集**會有相同的欄位。 不過，**記錄**可能還有其他特定的訊息，由唯一的欄位**記錄**，例如附件] 和 [副本 （副本）。  
  
 雖然**記錄**物件和目前資料列**資料錄集**有相同的欄位，它們是不同因為**記錄**和**資料錄集**物件具有不同的方法和屬性。  
  
 所持有的共通的欄位**記錄**和**資料錄集**可以修改其中一個物件上。 不過，欄位就無法刪除**記錄**物件，雖然基礎提供者可能支援將欄位設定為 null。  
  
 之後**記錄**已開啟，您可以透過程式設計方式加入欄位。 您也可以刪除您加入的欄位，但您無法刪除欄位，從原始**資料錄集**。  
  
 您也可以開啟**記錄**直接從 URL 的物件。 在此情況下，將欄位加入至**記錄**取決於基礎提供者。 目前，大部分的提供者會將一組欄位，描述所代表的實體**記錄**。 如果資料流的位元組為單位，例如簡單的檔案，包含實體[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件通常可以從開啟**記錄**。  
  
## <a name="special-fields-for-document-source-providers"></a>文件的特殊欄位來源提供者  
 是特殊類別的提供者，呼叫*來源提供者的文件*、 管理資料夾和文件。 當**記錄**物件代表文件或**資料錄集**物件表示文件的資料夾、 文件的來源提供者會填入這些物件與一組唯一的描述欄位文件的特性改為實際文件本身。 一般而言，一個欄位包含參考**資料流**表示文件。  
  
 這些欄位會構成資源**記錄**或**資料錄集**針對特定的提供者支援在這些[附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)。  
  
 兩個常數索引**欄位**的資源集合**記錄**或**資料錄集**擷取一組常用的欄位。 **欄位**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性會傳回所需的內容。  
  
-   使用存取欄位**adDefaultStream**常數包含相關聯的預設資料流**記錄**或**資料錄集**物件。 提供者會指派給物件的預設資料流。  
  
-   使用存取欄位**adRecordURL**常數包含識別文件的絕對 URL。  
  
 文件的來源提供者不支援[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合**記錄**和**欄位**物件。 內容**屬性**集合為 null 的此類物件。  
  
 文件的來源提供者可能會將提供者特定屬性例如**資料來源類型**識別是否文件的來源提供者。 如需如何判斷您的提供者類型的詳細資訊，請參閱您的提供者文件。  
  
## <a name="resource-recordset-columns"></a>資源資料錄集資料行  
 A*資源資料錄集*下列資料行所組成。  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|唯讀。 表示資源的 URL。|  
|RESOURCE_PARENTNAME|AdVarWChar|唯讀。 表示父記錄的絕對 URL。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|唯讀。 指出資源，也就是 PARENTNAME 和 PARSENAME 串連的絕對 URL。|  
|RESOURCE_ISHIDDEN|AdBoolean|如果隱藏的資源，則為 true。 除非明確建立資料列集的命令會選取 RESOURCE_ISHIDDEN 為 True 的資料列，將會不傳回任何資料列。|  
|RESOURCE_ISREADONLY|AdBoolean|如果資源是唯讀，則為 true。 嘗試開啟此資源用於 DBBINDFLAG_WRITE，且可因 DB_E_READONLY 失敗。 可以編輯這個屬性，即使只供讀取開啟資源。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|表示文件可能使用 — 例如，lawyer 的簡短。 這可能會對應至 Office 範本用來建立文件。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|指出 MIME 類型的文件，表示的格式，例如"`text/html`"。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|表示用來儲存內容的語言。|  
|RESOURCE_CREATIONTIME|AdFileTime|唯讀。 指出 FILETIME 結構，其中包含已建立資源的時間。 被報告的時間，格式為 Coordinated Universal Time (UTC)。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|唯讀。 指出 FILETIME 結構，其中包含資源的上次存取時間。 時間是以 UTC 格式。 FILETIME 成員都是零，如果提供者不支援這個時間成員。|  
|RESOURCE_LASTWRITETIME|AdFileTime|唯讀。 指出 FILETIME 結構，其中包含資源的上次寫入時間。 時間是以 UTC 格式。 FILETIME 成員都是零，如果提供者不支援這個時間成員。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|唯讀。 表示資源的預設資料流，以位元組為單位的大小。|  
|RESOURCE_ISCOLLECTION|AdBoolean|唯讀。 如果資源是集合，例如目錄，則為 true。 如果資源是簡單的檔案，則為 false。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|如果資源是結構化文件，則為 true。 如果資源不是結構化文件，則為 false。 它可能是集合或簡單的檔案。|  
|DEFAULT_DOCUMENT|AdVarWChar|唯讀。 指出這項資源都包含資料夾的預設簡單文件或結構化文件的 URL。 預設資料流要求資源時使用。 這個屬性是空白的簡單的檔案。|  
|CHAPTERED_CHILDREN|AdChapter|唯讀。 選擇性。 表示包含資源的子系的資料列集的章節。 ( *OLE DB Provider for Internet Publishing*不會使用此資料行。)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|唯讀。 表示資源的顯示名稱。|  
|RESOURCE_ISROOT|AdBoolean|唯讀。 如果資源是集合或結構化文件的根，則為 true。|  
  
## <a name="see-also"></a>請參閱＜  
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
