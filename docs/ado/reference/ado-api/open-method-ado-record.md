---
description: Open 方法 (ADO Record)
title: " (ADO 記錄) 的開啟方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 980e7c840cfb19077c6f4f1d1041d1f1eb8acf64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773797"
---
# <a name="open-method-ado-record"></a>Open 方法 (ADO Record)
開啟現有的 [記錄](./record-object-ado.md) 物件，或建立 **記錄**所代表的新專案，例如檔案或目錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 **Variant** ，可能代表此**記錄**物件所代表之實體的 URL、**命令**、開啟的[記錄集](./recordset-object-ado.md)或其他**記錄**物件、包含 SQL SELECT 語句的字串或資料表名稱。  
  
 *ActiveConnection*  
 選擇性。 表示連接字串或開啟[連接](./connection-object-ado.md)物件的**Variant** 。  
  
 *模式*  
 選擇性。 [ConnectModeEnum](./connectmodeenum.md)值，指定結果**記錄**物件的存取模式。 預設值為 **adModeUnknown**。  
  
 *CreateOptions*  
 選擇性。 [RecordCreateOptionsEnum](./recordcreateoptionsenum.md)值，指定是否應該開啟現有的檔案或目錄，或建立新的檔案或目錄。 預設值為 **adFailIfNotExists**。 如果設定為預設值，則會從 [mode](./mode-property-ado.md) 屬性取得存取模式。 當 *來源* 參數未包含 URL 時，會忽略此參數。  
  
 *選項*  
 選擇性。 [RecordOpenOptionsEnum](./recordopenoptionsenum.md)值，指定用來開啟**記錄**的選項。 預設值為 **adOpenRecordUnspecified**。 這些值可以合併。  
  
 *UserName*  
 選擇性。 包含使用者識別碼的 **字串** 值（如有需要）會授權存取 *來源*。  
  
 *密碼*  
 選擇性。 包含密碼的 **字串** 值，如果需要的話，請驗證使用者 *名稱*。  
  
## <a name="remarks"></a>備註  
 *來源* 可能是：  
  
-   URL。 如果 URL 的通訊協定為 HTTP，則預設會叫用網際網路提供者。 如果 URL 指向包含可執行腳本的節點， (例如。ASP 頁面) ，預設會開啟包含來源的 **記錄** ，而不是執行的內容。 使用 *Options* 引數來修改此行為。  
  
-   **記錄**物件。 從另一筆**記錄**開啟的**記錄**物件將會複製原始的**記錄**物件。  
  
-   **命令**物件。 開啟的 **記錄** 物件代表藉由執行 **命令**所傳回的單一資料列。 如果結果包含一個以上的單一資料列，則第一個資料列的內容會放在記錄中，而錯誤可能會新增至 **錯誤** 集合。  
  
-   SQL SELECT 語句。 開啟的 **記錄** 物件代表藉由執行字串內容所傳回的單一資料列。 如果結果包含一個以上的單一資料列，則第一個資料列的內容會放在記錄中，而錯誤可能會新增至 **錯誤** 集合。  
  
-   資料表名稱。  
  
 如果 **記錄** 物件代表無法使用 URL 存取的實體 (例如，從資料庫) 衍生的 **記錄集** 資料列，則 [ParentURL](./parenturl-property-ado.md) 屬性和使用 **adRecordURL** 常數所存取的欄位值都是 null。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO Connection) 的 Open 方法 ](./open-method-ado-connection.md)   
 [ (ADO 記錄集的 Open 方法) ](./open-method-ado-recordset.md)   
 [ (ADO Stream 的 Open 方法) ](./open-method-ado-stream.md)   
 [OpenSchema 方法](./openschema-method.md)