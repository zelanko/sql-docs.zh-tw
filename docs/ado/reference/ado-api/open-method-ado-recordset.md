---
title: Open 方法（ADO Recordset） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a091a606cf3049c055794bc16cc51db78a40978
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762176"
---
# <a name="open-method-ado-recordset"></a>Open 方法 (ADO Recordset)
在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上開啟資料指標。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>參數  
 *來源*  
 選擇性。 評估為有效[命令](../../../ado/reference/ado-api/command-object-ado.md)物件、SQL 語句、資料表名稱、預存程序呼叫、URL，或包含持續儲存之[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之檔案或[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件名稱的**Variant** 。  
  
 *ActiveConnection*  
 選擇性。 判斷值為有效[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件變數名稱的**Variant** ，或包含[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)參數的**字串**。  
  
 *CursorType*  
 選擇性。 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值，決定在開啟**記錄集**時，提供者應該使用的資料指標類型。 預設值為**adOpenForwardOnly**。  
  
 *LockType*  
 選擇性。 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，決定在開啟**記錄集**時，提供者應該使用的鎖定類型（並行）。 預設值為**adLockReadOnly**。  
  
 *選項*  
 選擇性。 **Long**值，指出提供者應該如何評估*來源*引數（如果它代表**Command**物件以外的專案），或者應該從先前儲存的檔案還原**記錄集**。 可以是一個或多個[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值，可以與位 or 運算子結合。  
  
> [!NOTE]
>  如果您從包含持續性**記錄集**的**資料流程**開啟**記錄集**，使用**adAsyncFetchNonBlocking**的[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值將不會有任何作用;提取將會同步並封鎖。  
  
> [!NOTE]
>  **AdExecuteNoRecords**或**adExecuteStream**的**ExecuteOpenEnum**值不應與**Open**搭配使用。  
  
## <a name="remarks"></a>備註  
 ADO**記錄集**的預設資料指標是位於伺服器上的順向唯讀資料指標。  
  
 在**記錄集**物件上使用**Open**方法會開啟一個資料指標，代表基表的記錄、查詢的結果，或先前儲存的**記錄集**。  
  
 使用選擇性的*來源*引數，以使用下列其中一種方法來指定資料來源：**命令**物件變數、SQL 語句、預存程式、資料表名稱、URL 或完整的檔案路徑名稱。 如果*Source*是檔案路徑名稱，它可以是完整路徑（"c:\dir\file.rst"），也就是相對路徑（".。\file.rst "）或 URL （" <https://files/file.rst> "）。  
  
 使用**Open**方法的*Source*引數來執行不會傳回記錄的動作查詢並不是個好主意，因為沒有簡單的方法可以判斷呼叫是否成功。 這類查詢所傳回的**記錄集**將會關閉。 若要執行不會傳回記錄的查詢（例如 SQL INSERT 語句），請改為呼叫**命令**物件的[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法或[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法。  
  
 *ActiveConnection*引數會對應至[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性，並指定要在哪個連接中開啟**記錄集**物件。 如果您傳遞這個引數的連接定義，ADO 就會使用指定的參數來開啟新的連接。 當您藉由將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**，以用戶端資料指標開啟**記錄集**之後，您可以變更此屬性的值，以將更新傳送至另一個提供者。 或者，您可以將此屬性設定為 [**無**] （在 Microsoft Visual Basic 中）或 [Null]，將**記錄集**與任何提供者中斷連接。 不過，變更伺服器端資料指標的*ActiveConnection*會產生錯誤。  
  
 對於直接對應至**記錄集**物件屬性（*來源*、 *CursorType*和*LockType*）的其他引數，屬性的引數關聯性如下所示：  
  
-   在開啟**記錄集**物件之前，會先讀取/寫入屬性。  
  
-   除非您在執行**Open**方法時傳遞對應的引數，否則會使用屬性設定。 如果您傳遞引數，它會覆寫對應的屬性設定，而屬性設定會以引數值進行更新。  
  
-   在您開啟**記錄集**物件之後，這些屬性會變成隻讀。  
  
> [!NOTE]
>  如果**記錄**集物件的[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性設定為有效的**Command**物件，則**ActiveConnection**屬性會是唯讀的，即使**記錄集**物件並未開啟也是一樣。  
  
 如果您在*來源*引數中傳遞**命令**物件，並同時傳遞*ActiveConnection*引數，就會發生錯誤。 **命令**物件的**ActiveConnection**屬性必須已經設定為有效的**連接**物件或連接字串。  
  
 如果您在*source*引數中傳遞**命令**物件以外的專案，您可以使用*Options*引數來優化*source*引數的評估。 如果未定義*Options*引數，您可能會遇到效能降低的情況，因為 ADO 必須呼叫提供者，以判斷引數是 SQL 語句、預存程式、URL 或資料表名稱。 如果您知道您所使用的*來源*類型，設定*Options*引數會指示 ADO 直接跳到相關的程式碼。 如果*選項*引數不符合*來源*類型，則會發生錯誤。  
  
 如果您在*來源*引數中傳遞**資料流程**物件，則不應該將資訊傳遞到其他引數中。 這樣會產生錯誤。 從**資料流程**開啟**記錄集**時，不會保留**ActiveConnection**資訊。  
  
 如果沒有與**記錄集**相關聯的連接， *Options*引數的預設值會是**adCmdFile** 。 這通常會是持久儲存之**記錄集**物件的情況。  
  
 如果資料來源未傳回任何記錄，則提供者會將[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性設為**True**，而目前的記錄位置為 undefined。 如果游標類型允許，您仍然可以將新的資料加入此空的**記錄集**物件。  
  
 當您完成開啟的**記錄集**物件的作業時，請使用[Close](../../../ado/reference/ado-api/close-method-ado.md)方法來釋放任何相關聯的系統資源。 關閉物件並不會將它從記憶體中移除;您可以變更其屬性設定，並使用**open**方法，稍後再重新開啟它。 若要完全排除記憶體中的物件，請將物件變數設為 [*無*]。  
  
 設定**ActiveConnection**屬性之前，請呼叫**Open**而不使用運算元，以建立藉由將欄位附加至**記錄集**[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合而建立之**記錄集**的實例。  
  
 如果您已將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**，您可以使用下列兩種方式的其中一種非同步地抓取資料列。 建議的方法是將*選項*設定為**adAsyncFetch**。 或者，您可以使用[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合中的「非同步資料列集處理」動態屬性，但如果您未將*Options*參數設定為**adAsyncFetch**，則相關的抓取事件可能會遺失。  
  
> [!NOTE]
>  只有透過**Open**方法的*Options*參數，才支援 MS 遠端提供者中的背景提取。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)和[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值的某些組合無效。 如需無法結合哪些選項的相關資訊，請參閱[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)和[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)的主題。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 和 Close 方法範例（VB）](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法範例（VBScript）](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例（VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Save 和 Open 方法範例（VB）](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 方法（ADO Connection）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO Record）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法（ADO Stream）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
