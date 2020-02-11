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
ms.openlocfilehash: 54d55926d2bec89b0764b751bf165586e8d3c6c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924510"
---
# <a name="records-and-provider-supplied-fields"></a>記錄和提供者提供的欄位
當[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件開啟時，其來源可以是開啟之[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的目前資料列、絕對 URL，或與開啟的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件結合的相對 URL。  
  
 如果**記錄**是從**記錄集**開啟，**記錄**物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合會包含**記錄集**內的所有欄位，以及基礎提供者所加入的任何欄位。  
  
 提供者可以插入額外的欄位，做為**記錄**的補充特性。 如此一來，**記錄**可能會有唯一的欄位，而不是記錄**集**內的全部或任何衍生自**記錄集**之另一個資料列的**記錄**。  
  
 例如，從電子郵件資料來源衍生之**記錄集**的所有資料列，可能會有資料行，例如 From、To 和 Subject。 衍生自該**記錄集**的**記錄**將會具有相同的欄位。 不過，**記錄**可能也會有該**記錄**所代表之特定訊息特有的其他欄位，例如 [附件] 和 [副本] （碳複製）。  
  
 雖然記錄**物件和記錄****集**目前的資料列具有相同的欄位，但它們是不同的，因為**record**和**Recordset**物件有不同的方法和屬性。  
  
 **記錄**和**記錄集**共同保存的欄位可以在任一物件上進行修改。 不過，雖然基礎提供者可能支援將欄位設定為 null，但無法刪除**記錄**物件上的欄位。  
  
 **記錄**開啟之後，您可以透過程式設計方式加入欄位。 您也可以刪除已加入的欄位，但無法從原始**記錄集**刪除欄位。  
  
 您也可以直接從 URL 開啟**記錄**物件。 在此情況下，加入至**記錄**的欄位取決於基礎提供者。 目前，大部分的提供者都會新增一組欄位，以描述**記錄**所代表的實體。 如果實體是由位元組資料流程（例如簡單檔案）所組成，通常可以從**記錄**開啟[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="special-fields-for-document-source-providers"></a>檔來源提供者的特殊欄位  
 提供者的特殊類別，稱為*檔來源提供者*，負責管理資料夾和檔。 當**記錄**物件代表檔或**記錄集**物件代表檔的資料夾時，檔來源提供者會使用一組唯一的欄位來填入這些物件，以描述檔的特性，而不是實際的檔本身。 通常，一個欄位包含代表檔之**資料流程**的參考。  
  
 這些欄位會構成資源**記錄**或**記錄集**，並列出在[附錄 a：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)中支援它們的特定提供者。  
  
 兩個常數會為資源**記錄**或**記錄集**的**Fields**集合編制索引，以抓取一對常用的欄位。 **Field**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性會傳回所需的內容。  
  
-   使用**adDefaultStream**常數存取的欄位包含與**記錄**或**記錄集**物件相關聯的預設資料流程。 提供者會將預設資料流程指派給物件。  
  
-   以**adRecordURL**常數存取的欄位包含可識別檔的絕對 URL。  
  
 檔來源提供者不支援**記錄**和**欄位**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 對於這類物件， **Properties**集合的內容是 null。  
  
 檔來源提供者可以加入提供者特定的屬性（例如**Datasource 類型**），以識別它是否為檔來源提供者。 如需如何決定提供者類型的詳細資訊，請參閱您的提供者檔。  
  
## <a name="resource-recordset-columns"></a>資源記錄集資料行  
 *資源記錄集*包含下列資料行。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|唯讀。 指出資源的 URL。|  
|RESOURCE_PARENTNAME|AdVarWChar|唯讀。 指出父記錄的絕對 URL。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|唯讀。 表示資源的絕對 URL，也就是 PARENTNAME 和 PARSENAME 的串連。|  
|RESOURCE_ISHIDDEN|AdBoolean|如果資源已隱藏，則為 True。 除非建立資料列集的命令明確地選取 RESOURCE_ISHIDDEN 為 True 的資料列，否則不會傳回任何資料列。|  
|RESOURCE_ISREADONLY|AdBoolean|如果資源是唯讀的，則為 True。 嘗試使用 DBBINDFLAG_WRITE 開啟此資源，將會失敗並出現 DB_E_READONLY。 即使資源只有開啟以供讀取，此屬性也可以進行編輯。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|指出可能使用檔的情況，例如律師的簡短。 這可能會對應到用來建立檔的 Office 範本。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|表示檔的 MIME 類型，表示 "`text/html`" 之類的格式。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|表示用來儲存內容的語言。|  
|RESOURCE_CREATIONTIME|adFileTime|唯讀。 表示 FILETIME 結構，其中包含資源的建立時間。 時間是以國際標準時間（UTC）格式來報告。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|唯讀。 表示 FILETIME 結構，其中包含上次存取資源的時間。 時間是 UTC 格式。 如果提供者不支援這個時間成員，FILETIME 成員就會是零。|  
|RESOURCE_LASTWRITETIME|AdFileTime|唯讀。 表示 FILETIME 結構，其中包含資源的上次寫入時間。 時間是 UTC 格式。 如果提供者不支援這個時間成員，FILETIME 成員就會是零。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|唯讀。 表示資源的預設資料流程大小（以位元組為單位）。|  
|RESOURCE_ISCOLLECTION|AdBoolean|唯讀。 如果資源是集合（例如目錄），則為 True。 如果資源是簡單的檔案，則為 False。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|如果資源是結構化檔，則為 True。 如果資源不是結構化檔，則為 False。 它可以是集合或簡單的檔案。|  
|DEFAULT_DOCUMENT|AdVarWChar|唯讀。 表示此資源包含資料夾或結構化檔之預設簡單檔的 URL。 當從資源要求預設資料流程時使用。 簡單檔案的這個屬性是空白的。|  
|CHAPTERED_CHILDREN|AdChapter|唯讀。 選擇性。 表示資料列集的章節，其中包含資源的子系。 （*網際網路發佈的 OLE DB 提供者*不會使用這個資料行）。|  
|RESOURCE_DISPLAYNAME|AdVarWChar|唯讀。 表示資源的顯示名稱。|  
|RESOURCE_ISROOT|AdBoolean|唯讀。 如果資源是集合或結構化檔的根目錄，則為 True。|  
  
## <a name="see-also"></a>另請參閱  
 [Record 物件（ADO）](../../../ado/reference/ado-api/record-object-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
