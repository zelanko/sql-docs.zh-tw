---
title: Open 方法（ADO Record） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97c7f1c143c83dd35ca5ff17e9776d79fb734ff9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917919"
---
# <a name="open-method-ado-record"></a>Open 方法 (ADO Record)
開啟現有的[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，或建立**記錄**所代表的新專案，例如檔案或目錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 **Variant** ，可能代表此**記錄**物件所代表之實體的 URL、**命令**、開啟的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或其他**記錄**物件、包含 SQL SELECT 語句或資料表名稱的字串。  
  
 *ActiveConnection*  
 選擇性。 表示連接字串或開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的**Variant** 。  
  
 *模式*  
 選擇性。 [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，指定結果**記錄**物件的存取模式。 預設值為**adModeUnknown**。  
  
 *CreateOptions*  
 選擇性。 [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)值，指定是否應該開啟現有的檔案或目錄，或建立新的檔案或目錄。 預設值為**adFailIfNotExists**。 如果設定為預設值，則會從 [[模式]](../../../ado/reference/ado-api/mode-property-ado.md)屬性取得存取模式。 當*來源*參數不包含 URL 時，會忽略這個參數。  
  
 *選項*  
 選擇性。 [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)值，指定用來開啟**記錄**的選項。 預設值為**adOpenRecordUnspecified**。 這些值可以合併。  
  
 *UserName*  
 選擇性。 包含使用者識別碼的**字串**值，如有必要，會授權存取*來源*。  
  
 *密碼*  
 選擇性。 包含密碼的**字串**值（如有需要）會驗證使用者*名稱*。  
  
## <a name="remarks"></a>備註  
 *來源*可能是：  
  
-   一個 URL。 如果 URL 的通訊協定是 HTTP，則預設會叫用網際網路提供者。 如果 URL 指向包含可執行腳本的節點（例如）。ASP 網頁），預設會開啟包含來源而不是執行內容的**記錄**。 使用*Options*引數來修改此行為。  
  
-   **記錄**物件。 從另一筆**記錄**開啟的**記錄**物件將會複製原始**記錄**物件。  
  
-   **命令**物件。 已開啟的**記錄**物件代表藉由執行**命令**所傳回的單一資料列。 如果結果包含多個單一資料列，則會將第一個資料列的內容放在記錄中，而且可能會將錯誤加入至**錯誤**集合。  
  
-   SQL SELECT 語句。 已開啟的**記錄**物件代表執行字串內容所傳回的單一資料列。 如果結果包含多個單一資料列，則會將第一個資料列的內容放在記錄中，而且可能會將錯誤加入至**錯誤**集合。  
  
-   資料表名稱。  
  
 如果**記錄**物件代表無法以 URL 存取的實體（例如，從資料庫衍生的**記錄集**資料列），則[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性和使用**adRecordURL**常數存取之欄位的值都是 null。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法（ADO Connection）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法（ADO Stream）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
