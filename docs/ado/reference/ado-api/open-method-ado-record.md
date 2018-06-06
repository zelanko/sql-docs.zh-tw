---
title: Open 方法 （ADO 資料錄） |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 432f2a821bd276efd46f61497f4ef7ae95502bf7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-record"></a>Open 方法 （ADO 資料錄）
開啟現有的[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，或建立新的項目所代表**記錄**，例如檔案或目錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A **Variant**可能代表實體的 URL，而這表示**記錄**物件**命令**，開啟[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或另一個**記錄**物件，包含 SQL SELECT 陳述式或資料表名稱的字串。  
  
 *ActiveConnection*  
 選擇性。 A **Variant**表示連接字串或開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
 *模式*  
 選擇性。 A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，指定產生的存取模式**記錄**物件。 預設值是**adModeUnknown**。  
  
 *CreateOptions*  
 選擇性。 A [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)值，指定是否應該開啟現有的檔案或目錄，或應建立新的檔案或目錄。 預設值是**adFailIfNotExists**。 如果設為預設值、 存取模式取自[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。 這個參數已忽略時*來源*參數不包含 URL。  
  
 *選項。*  
 選擇性。 A [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)值，指定開啟選項**記錄**。 預設值是**adOpenRecordUnspecified**。 這些值可以合併。  
  
 *UserName*  
 選擇性。 A**字串**值，其中包含的使用者識別碼，如有必要，授與存取權*來源*。  
  
 *密碼*  
 選擇性。 A**字串**包含，如有必要，驗證的密碼值*UserName*。  
  
## <a name="remarks"></a>備註  
 *來源*可能是：  
  
-   URL 中。 如果是 http URL 的通訊協定，網際網路提供者會叫用預設值。 如果 URL 指向的節點，其中包含可執行的指令碼 (例如。ASP 網頁），**記錄**其中包含來源，而不是執行預設會開啟內容。 使用*選項*引數以修改此行為。  
  
-   A**記錄**物件。 A**記錄**從另一個物件開啟**記錄**會複製原始**記錄**物件。  
  
-   A**命令**物件。 開啟**記錄**物件都代表藉由執行傳回單一資料列**命令**。 如果結果包含多個單一資料列，第一個資料列的內容會放在記錄和錯誤可能會加入至**錯誤**集合。  
  
-   SQL SELECT 陳述式。 開啟**記錄**物件都代表所執行的字串內容傳回單一資料列。 如果結果包含多個單一資料列，第一個資料列的內容會放在記錄和錯誤可能會加入至**錯誤**集合。  
  
-   資料表名稱。  
  
 如果**記錄**物件都代表無法使用 URL 存取的實體 (例如，一個資料列的**資料錄集**衍生自資料庫)，兩者的值[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性和欄位，以存取**adRecordURL**常數都是 null。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 （ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
