---
description: 記錄和提供者提供的欄位
title: 記錄和提供者提供的欄位 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: rothja
ms.author: jroth
ms.openlocfilehash: 7cc7b8c4fb0116f96a2470a7161f9fbd30c7efb9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979949"
---
# <a name="records-and-provider-supplied-fields"></a>記錄和提供者提供的欄位
當 [記錄](../../../ado/reference/ado-api/record-object-ado.md) 物件開啟時，其來源可以是開啟之 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的目前資料列、絕對 URL，或與開啟的 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件結合的相對 URL。  
  
 如果從記錄**集**開啟**記錄**，**記錄**物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合會包含**記錄集**內的所有欄位，以及基礎提供者所加入的任何欄位。  
  
 提供者可能會插入其他欄位，做為 **記錄**的補充特性。 如此一來，**記錄**可能會有不在**記錄集中**的唯一欄位，或是從**記錄集**的另一個資料列衍生的任何**記錄**。  
  
 例如，衍生自電子郵件資料來源之 **記錄集** 的所有資料列，可能會有資料行，例如 From、To 和 Subject。 從該**記錄集**衍生的**記錄**將會有相同的欄位。 但是， **記錄** 可能也會有該 **記錄**所代表之特定訊息的其他欄位，例如附件和副本 (碳複製) 。  
  
 雖然記錄**物件和記錄****集**的目前資料列具有相同的欄位，但它們是不同的，因為**記錄**和**記錄集**物件具有不同的方法和屬性。  
  
 **記錄**和**記錄集**所擁有的欄位，可以在任一物件上修改。 但是，雖然基礎提供者可能支援將欄位設定為 null，但無法刪除 **記錄** 物件上的欄位。  
  
 開啟 **記錄** 之後，您可以用程式設計的方式新增欄位。 您也可以刪除已加入的欄位，但無法從原始 **記錄集**刪除欄位。  
  
 您也可以直接從 URL 開啟 **記錄** 物件。 在此情況下，加入至 **記錄** 的欄位會視基礎提供者而定。 目前，大部分的提供者會新增一組描述 **記錄**所代表之實體的欄位。 如果實體是由位元組資料流程（例如簡單的檔案）所組成，則通常可以從**記錄**開啟[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="special-fields-for-document-source-providers"></a>檔來源提供者的特殊欄位  
 提供者的特殊類別，稱為「 *檔來源提供者*」，會管理資料夾和檔。 當**記錄****物件代表**檔的資料夾時，檔來源提供者會以一組唯一的欄位來填入這些物件，而不會描述檔的特性，而不是實際檔本身。 通常，一個欄位包含表示檔之 **資料流程** 的參考。  
  
 這些欄位會構成資源 **記錄** 或 **記錄集** ，並且會針對在 [附錄 a：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)中支援它們的特定提供者列出。  
  
 兩個常數會編制資源**記錄**或**記錄集**之**欄位**集合的索引，以抓取一組常用的欄位。 **Field**物件[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性會傳回所需的內容。  
  
-   使用 **adDefaultStream** 常數存取的欄位包含與 **記錄** 或 **記錄集** 物件相關聯的預設資料流程。 提供者會將預設資料流程指派給物件。  
  
-   使用 **adRecordURL** 常數存取的欄位包含識別檔的絕對 URL。  
  
 檔來源提供者不支援**記錄**和**欄位**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 這類物件的 **Properties** 集合內容是 null。  
  
 檔來源提供者可以加入提供者特定的屬性，例如 **Datasource 型** 別，以識別它是否為檔來源提供者。 如需如何判斷您的提供者類型的詳細資訊，請參閱您的提供者檔。  
  
## <a name="resource-recordset-columns"></a>資源記錄集資料行  
 *資源記錄集*包含下列資料行。  
  
|欄名|類型|描述|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|唯讀。 指出資源的 URL。|  
|RESOURCE_PARENTNAME|AdVarWChar|唯讀。 表示父記錄的絕對 URL。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|唯讀。 指出資源的絕對 URL，這是 PARENTNAME 和 PARSENAME 的串連。|  
|RESOURCE_ISHIDDEN|AdBoolean|如果資源已隱藏，則為 True。 除非建立資料列集的命令明確地選取 RESOURCE_ISHIDDEN 為 True 的資料列，否則不會傳回任何資料列。|  
|RESOURCE_ISREADONLY|AdBoolean|如果資源是唯讀的，則為 True。 嘗試使用 DBBINDFLAG_WRITE 開啟此資源，將會失敗並出現 DB_E_READONLY。 即使已開啟資源以供讀取，也可以編輯此屬性。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|指出可能使用檔的原因，例如，律師的簡短。 這可能會對應到用來建立檔的 Office 範本。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|表示檔的 MIME 類型，表示格式，例如 " `text/html` "。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|指出儲存內容的語言。|  
|RESOURCE_CREATIONTIME|adFileTime|唯讀。 表示 FILETIME 結構，其中包含建立資源的時間。 時間是以國際標準時間 (UTC) 格式來回報。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|唯讀。 表示 FILETIME 結構，其中包含上次存取資源的時間。 時間是採用 UTC 格式。 如果提供者不支援這個時間成員，則 FILETIME 成員為零。|  
|RESOURCE_LASTWRITETIME|AdFileTime|唯讀。 表示 FILETIME 結構，其中包含上次寫入資源的時間。 時間是採用 UTC 格式。 如果提供者不支援這個時間成員，則 FILETIME 成員為零。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|唯讀。 表示資源的預設資料流程大小（以位元組為單位）。|  
|RESOURCE_ISCOLLECTION|AdBoolean|唯讀。 如果資源是集合，例如目錄，則為 True。 如果資源是簡單的檔案，則為 False。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|如果資源是結構化檔，則為 True。 如果資源不是結構化檔，則為 False。 它可以是集合或簡單的檔案。|  
|DEFAULT_DOCUMENT|AdVarWChar|唯讀。 指出此資源包含資料夾或結構化檔之預設簡單檔的 URL。 當從資源要求預設資料流程時使用。 簡單檔案的這個屬性是空白的。|  
|CHAPTERED_CHILDREN|AdChapter|唯讀。 選擇性。 指出包含資源子系的資料列集章節。  (*網際網路發佈的 OLE DB 提供者* 不會使用此資料行。 ) |  
|RESOURCE_DISPLAYNAME|AdVarWChar|唯讀。 指出資源的顯示名稱。|  
|RESOURCE_ISROOT|AdBoolean|唯讀。 如果資源是集合或結構化檔的根目錄，則為 True。|  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的記錄物件 ](../../../ado/reference/ado-api/record-object-ado.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
