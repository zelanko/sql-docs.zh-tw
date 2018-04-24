---
title: Open 方法 （ADO 資料錄集） |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: a86f84251dca3a76d0e7110c781fea26395fc9d9
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="open-method-ado-recordset"></a>Open 方法 （ADO 資料錄集）
開啟資料指標上[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A **Variant**會評估為有效[命令](../../../ado/reference/ado-api/command-object-ado.md)物件、 SQL 陳述式、 資料表名稱、 預存程序呼叫、 URL 或檔案的名稱或[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件，包含持續儲存[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 *ActiveConnection*  
 選擇性。 任一**Variant**會評估為有效[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件變數的名稱，或**字串**包含[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)參數。  
  
 *CursorType*  
 選擇性。 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)判斷開啟時，應該使用提供者的資料指標類型的值**資料錄集**。 預設值是**adOpenForwardOnly**。  
  
 *LockType*  
 選擇性。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，決定使用哪種類型的鎖定 (concurrency) 提供者應該開啟時**資料錄集**。 預設值是**Recordset**。  
  
 *選項。*  
 選擇性。 A**長**值，指出提供者應該如何評估*來源*引數，如果它不是代表項目**命令**物件，或**資料錄集**應該還原先前儲存的位置的檔案。 可以是一個或多個[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)可以與位元 OR 運算子結合的值。  
  
> [!NOTE]
>  如果您開啟**資料錄集**從**資料流**包含保存**資料錄集**，並使用[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值**adAsyncFetchNonBlocking**會有任何作用，則提取將會同步和封鎖。  
  
> [!NOTE]
>  **ExecuteOpenEnum**值**adExecuteNoRecords**或**adExecuteStream**不應與**開啟**。  
  
## <a name="remarks"></a>備註  
 ADO 的預設游標**資料錄集**是一個順向唯讀資料指標位於伺服器上。  
  
 使用**開啟**方法**資料錄集**物件開啟資料指標從基底資料表、 查詢或先前儲存的結果，代表記錄**資料錄集**。  
  
 使用選擇性*來源*引數來指定資料來源，使用下列其中之一：**命令**物件變數，SQL 陳述式、 預存程序、 資料表名稱、 URL 或完整檔案路徑名稱。 如果*來源*是檔案的路徑名稱，它可以是完整路徑 ("c:\dir\file.rst") 的相對路徑 ("..\file.rst")，或 URL ("http://files/file.rst")。  
  
 不建議使用*來源*引數的**開啟**方法，以執行動作的查詢不會傳回記錄，因為沒有簡單的方法可以判斷呼叫是否成功。 **資料錄集**傳回這類查詢將會關閉。 若要執行的查詢，不會傳回記錄，例如 SQL INSERT 陳述式，呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**物件或[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)改為物件。  
  
 *ActiveConnection*引數會對應至[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性，並指定要開啟的連接**資料錄集**物件。 如果您要傳入的連接定義，這個引數，ADO 會開啟新的連接使用指定的參數。 開啟之後**資料錄集**藉由設定的用戶端資料指標與[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**，您可以變更傳送至這個屬性的值另一個提供者的更新。 您可將此屬性設**Nothing** (在 Microsoft Visual Basic) 或 NULL 中斷連線**資料錄集**從任何提供者。 變更*ActiveConnection*伺服器端資料指標會產生錯誤，不過。  
  
 直接對應到屬性的其他引數**資料錄集**物件 (*來源*， *CursorType*，和*LockType*)，引數的屬性關聯性如下所示：  
  
-   屬性是讀取/寫入之前**資料錄集**開啟物件。  
  
-   除非您將對應的引數傳遞執行時，會使用屬性設定**開啟**方法。 如果您傳遞的引數，它會覆寫對應的屬性設定，而且會更新引數值屬性設定。  
  
-   開啟之後**資料錄集**物件，這些屬性會變成唯讀。  
  
> [!NOTE]
>  **ActiveConnection**屬性是唯讀，如**資料錄集**物件[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性設定為有效**命令**物件，即使**資料錄集**物件未開啟。  
  
 如果您要傳入**命令**物件存放至*來源*引數以及傳遞*ActiveConnection*引數，就會發生錯誤。 **ActiveConnection**屬性**命令**物件必須已設為有效**連接**物件或連接字串。  
  
 如果傳遞的項目以外**命令**物件存放至*來源*引數，您可以使用*選項*引數，若要最佳化的評估*來源*引數。 如果*選項*引數未定義時，您可能會感覺到的效能降低，因為 ADO 必須進行呼叫以判斷是否在 SQL 陳述式、 預存程序、 URL 或資料表名稱引數的提供者。 如果您知道*來源*所要使用的類型，設定*選項*引數會指示 ADO，直接跳到相關的程式碼。 如果*選項*引數不符合*來源*輸入時，發生錯誤。  
  
 如果您要傳入**資料流**物件存放至*來源*引數，您應該不傳遞資訊到其他引數。 這樣會產生錯誤。 **ActiveConnection**資訊不是保留時**資料錄集**開啟從**資料流**。  
  
 預設值為*選項*引數是**adCmdFile**如果沒有連接相關聯**資料錄集**。 這通常會是大小寫，持續儲存**資料錄集**物件。  
  
 如果資料來源會不傳回任何記錄，提供者會同時設定[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性**True**，且目前的記錄位置未定義。 您仍然可以將新資料加入此空**資料錄集**如果資料指標類型可讓它的物件。  
  
 當您透過開啟得到您的作業**資料錄集**物件，請使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法來釋放任何相關聯的系統資源。 關閉物件不會將它從記憶體中移除您可以變更其屬性設定，並使用**開啟**方法，以在稍後重新開啟它。 若要完全消除從記憶體物件，設定為物件變數*Nothing*。  
  
 之前**ActiveConnection**屬性設定，請呼叫**開啟**來建立執行個體的任何運算元使用**資料錄集**附加欄位以建立**資料錄集**[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
 如果您已將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**，您可以擷取資料列，以非同步方式在兩種方式之一。 建議的方法是將*選項*至**adAsyncFetch**。 或者，您可以使用中，「 非同步資料列集處理 」 的動態屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，但相關的擷取的事件可能會遺失如果您未設定*選項*參數**adAsyncFetch**。  
  
> [!NOTE]
>  背景擷取 MS 遠端提供者中只能透過支援**開啟**方法的*選項*參數。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 特定組合[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)和[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值不是有效。 無法結合選項相關的資訊，請參閱主題[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)，和[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [開啟與關閉方法範例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [開啟與關閉方法範例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [開啟與關閉方法範例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [儲存並開啟方法的範例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 方法 （ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 資料錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
