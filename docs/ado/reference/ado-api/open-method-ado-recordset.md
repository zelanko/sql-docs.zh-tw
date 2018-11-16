---
title: Open 方法 (ADO Recordset) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c1a53f8c310f43503b7dde8c85beb862a66e953
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606670"
---
# <a name="open-method-ado-recordset"></a>Open 方法 (ADO Recordset)
在開啟資料指標[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A **Variant**評估為有效[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，SQL 陳述式、 資料表名稱、 預存程序呼叫、 URL 或檔案的名稱或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件，包含持續儲存[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 *ActiveConnection*  
 選擇性。 任一**Variant**評估為有效[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件的變數名稱，或**字串**包含[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)參數。  
  
 *CursorType*  
 選擇性。 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值，決定資料指標開啟時，應該使用提供者的型別**資料錄集**。 預設值是**adOpenForwardOnly**。  
  
 *LockType*  
 選擇性。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，決定使用哪種類型的鎖定 （並行） 提供者應該開啟時**資料錄集**。 預設值是**Recordset**。  
  
 *選項。*  
 選擇性。 A**長**值，指出提供者應該如何評估*來源*引數，如果它代表的項目以外的其他**命令**物件，或是**資料錄集**應該從先前儲存的位置的檔案還原。 可以是一或多個[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或是[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)可與位元的 OR 運算子結合的值。  
  
> [!NOTE]
>  如果您開啟**Recordset**從**Stream**包含保存**資料錄集**，並使用[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值**adAsyncFetchNonBlocking**會有任何作用，但會同步和封鎖提取。  
  
> [!NOTE]
>  **ExecuteOpenEnum**的值**adExecuteNoRecords**或是**adExecuteStream**不應使用**開啟**。  
  
## <a name="remarks"></a>備註  
 ADO 的預設游標**資料錄集**是位於伺服器上的順向、 唯讀資料指標。  
  
 使用**開放**方法**Recordset**物件開啟資料指標，表示記錄基底資料表、 查詢，或先前儲存的結果**資料錄集**。  
  
 使用選擇性*來源*引數來指定資料來源，使用下列其中之一：**命令**物件變數，SQL 陳述式、 預存程序、 資料表名稱、 URL 或完整檔案路徑名稱。 如果*來源*是檔案的路徑名稱，它可以是完整路徑 ("c:\dir\file.rst 」) 的相對路徑 ("...\file.rst")，或 URL ("https://files/file.rst」)。  
  
 它不是個不錯的主意，使用*來源*引數**開啟**方法，以執行動作查詢不會傳回記錄，因為沒有任何簡單的方法，以判斷呼叫是否成功。 **資料錄集**傳回這類查詢將會關閉。 若要執行的查詢，不會傳回記錄，例如 SQL INSERT 陳述式，呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**物件或[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
 *ActiveConnection*引數對應至[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性，並指定要開啟的連線中**資料錄集**物件。 如果您傳遞連接定義為這個引數時，ADO 會開啟新的連線，使用指定的參數。 開啟之後**資料錄集**使用所設定的用戶端資料指標[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設**adUseClient**，您可以變更這個屬性，以傳送的值另一個提供者的更新。 或您可以將此屬性設定為**Nothing** (Microsoft Visual Basic 中) 或 NULL 中斷**資料錄集**從任何提供者。 變更*ActiveConnection*伺服器端資料指標會產生錯誤，不過。  
  
 直接對應到屬性的其他引數**Recordset**物件 (*來源*， *CursorType*，以及*LockType*)，屬性的引數的關聯性如下所示：  
  
-   屬性是讀取/寫入之前**資料錄集**開啟物件。  
  
-   除非您傳遞的相對應的引數，執行時，會使用的屬性設定**開啟**方法。 如果您傳遞的引數，它會覆寫對應的屬性設定，而且屬性設定會更新引數值。  
  
-   在您開啟之後**資料錄集**物件，這些屬性會變成唯讀。  
  
> [!NOTE]
>  **ActiveConnection**屬性是唯讀**Recordset**物件，而其[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性設定為有效**命令**物件，即使**資料錄集**物件未開啟。  
  
 如果您傳遞**命令**物件中*來源*引數以及傳遞*ActiveConnection*引數，則會發生錯誤。 **ActiveConnection**屬性**命令**物件必須已設定為有效**連接**物件或連接字串。  
  
 如果傳遞的項目以外**命令**物件中*來源*引數，您可以使用*選項*引數，以最佳化的評估*來源*引數。 如果*選項*引數未定義時，您可能會感覺到的效能，因為 ADO 必須進行呼叫以判斷引數是否 SQL 陳述式、 預存程序、 URL 或資料表名稱的提供者。 如果您知道*來源*您所使用，設定型別的*選項*引數會指示 ADO，直接跳到相關的程式碼。 如果*選項*引數不符合*來源*輸入時，發生錯誤。  
  
 如果您傳遞**Stream**物件中*來源*引數，您應該不將資訊傳入其他引數。 這樣會產生錯誤。 **ActiveConnection**資訊不是保留時**Recordset**從開啟**Stream**。  
  
 預設值*選項*引數是**adCmdFile**如果沒有連接相關聯**資料錄集**。 這通常會是大小寫，持續儲存**資料錄集**物件。  
  
 如果資料來源會不傳回任何記錄，提供者會設定兩者[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)並[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性，以**True**，和目前的記錄位置會是未定義。 您仍然可以將新資料加入此空白**資料錄集**物件如果資料指標類型可讓它。  
  
 當您透過開啟完成您的作業**Recordset**物件，請使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法來釋放任何相關聯的系統資源。 關閉物件不會將它從記憶體中; 中移除您可以變更其屬性設定，並使用**開啟**稍後再重新開啟它的方法。 若要完全排除記憶體中的物件，設定為物件變數*Nothing*。  
  
 再**ActiveConnection**屬性設定，請呼叫**開啟**若要建立的執行個體的任何運算元使用**資料錄集**附加欄位，以建立**資料錄集**[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
 如果您已將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設**adUseClient**，您可以擷取資料列，以非同步方式在兩種方式之一。 建議的方法是將*選項*要**adAsyncFetch**。 或者，您可以使用中，「 非同步資料列集處理 」 的動態屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，但相關的擷取的事件不會遺失您未設定*選項*參數**adAsyncFetch**。  
  
> [!NOTE]
>  背景擷取 MS 遠端提供者中支援只能透過**開放**方法的*選項*參數。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 某些的組合[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)並[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值不是有效。 了解哪種選項都無法結合的資訊，請參閱主題[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)，並[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 和 Close 方法範例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法範例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Save 和 Open 方法範例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 記錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
