---
description: Open 方法 (ADO Recordset)
title: " (ADO 記錄集的 Open 方法) |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 879456c30c3b34773d6f6b1395a88e04f5faaf9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990309"
---
# <a name="open-method-ado-recordset"></a>Open 方法 (ADO Recordset)
開啟 [記錄集](./recordset-object-ado.md) 物件上的資料指標。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 判斷值為有效的[命令](./command-object-ado.md)物件、SQL 語句、資料表名稱、預存程序呼叫、URL，或包含持續儲存之[記錄集](./recordset-object-ado.md)之檔案或[資料流程](./stream-object-ado.md)物件名稱的**Variant** 。  
  
 *ActiveConnection*  
 選擇性。 判斷值為有效[連接](./connection-object-ado.md)物件變數名稱的**Variant** ，或包含[ConnectionString](./connectionstring-property-ado.md)參數的**字串**。  
  
 *CursorType*  
 選擇性。 [CursorTypeEnum](./cursortypeenum.md)值，決定提供者在開啟**記錄集**時應使用的資料指標類型。 預設值為 **adOpenForwardOnly**。  
  
 *LockType*  
 選擇性。 [LockTypeEnum](./locktypeenum.md)值，可決定提供者在開啟**記錄集**時應使用的鎖定 (並行) 類型。 預設值為 **adLockReadOnly**。  
  
 *選項*  
 選擇性。 **Long**值，指出提供者應該如何評估*來源*引數（如果它代表**Command**物件以外的某個值），或是要從先前儲存的檔案還原**記錄集**。 可以是一個或多個 [CommandTypeEnum](./commandtypeenum.md) 或 [ExecuteOptionEnum](./executeoptionenum.md) 值，可以與位 or 運算子結合。  
  
> [!NOTE]
>  如果您從包含保存之**記錄集**的**資料流程**開啟**記錄集**，則使用**adAsyncFetchNonBlocking**的[ExecuteOptionEnum](./executeoptionenum.md)值將不會有任何作用;提取將會是同步和封鎖。  
  
> [!NOTE]
>  **AdExecuteNoRecords**或**adExecuteStream**的**ExecuteOpenEnum**值不應與**Open**一起使用。  
  
## <a name="remarks"></a>備註  
 ADO **記錄集** 的預設資料指標是位於伺服器上的順向唯讀資料指標。  
  
 在**記錄集**物件上使用**Open**方法會開啟資料指標，以表示基表中的記錄、查詢的結果，或先前儲存的**記錄集**。  
  
 使用選擇性的 *來源* 引數，利用下列其中一項來指定資料來源： **命令** 物件變數、SQL 語句、預存程式、資料表名稱、URL 或完整的檔案路徑名稱。 如果 *來源* 是檔案路徑名稱，它可以是完整路徑 ( "c:\dir\file.rst" ) ，相對路徑 ( "）。\file.rst ") 或 (`https://files/file.rst`) URL。  
  
 使用**Open**方法的*Source*引數來執行不會傳回記錄的動作查詢並不是個好主意，因為沒有簡單的方法可以判斷呼叫是否成功。 這類查詢所傳回的 **記錄集** 將會關閉。 若要執行不傳回記錄的查詢，例如 SQL INSERT 語句，請改為呼叫**命令**物件的[Execute](./execute-method-ado-command.md)方法或[連接](./connection-object-ado.md)物件的[execute](./execute-method-ado-connection.md)方法。  
  
 *ActiveConnection*引數會對應至[ActiveConnection](./activeconnection-property-ado.md)屬性，並指定要開啟**記錄集**物件的連接。 如果您傳遞此引數的連接定義，ADO 會使用指定的參數開啟新的連接。 當您將[CursorLocation](./cursorlocation-property-ado.md)屬性設定為**adUseClient**來開啟具有用戶端資料指標的**記錄集**之後，您可以變更這個屬性的值，將更新傳送給另一個提供者。 或者，您可以將此屬性設定為 Microsoft Visual Basic) 中的 **Nothing** (或 Null，以中斷 **記錄集** 與任何提供者的連線。 但是，變更伺服器端資料指標的 *ActiveConnection* 會產生錯誤。  
  
 對於直接與 **記錄集** 物件的屬性相對應的其他引數 (*Source*、 *CursorType*和 *LockType*) ，這些屬性的引數關聯性如下所示：  
  
-   在 **記錄集** 物件開啟之前，屬性是讀取/寫入。  
  
-   除非您在執行 **Open** 方法時傳遞對應的引數，否則會使用屬性設定。 如果您傳遞引數，它會覆寫對應的屬性設定，並以引數值更新屬性設定。  
  
-   開啟 **記錄集** 物件之後，這些屬性會變成隻讀。  
  
> [!NOTE]
>  如果**記錄集**物件的 [[來源](./source-property-ado-recordset.md)] 屬性設定為有效的**命令**物件，則**ActiveConnection**屬性為唯讀，即使尚未開啟**記錄集**物件也是如此。  
  
 如果您在*來源*引數中傳遞**命令**物件，並同時傳遞*ActiveConnection*引數，則會發生錯誤。 **命令**物件的**ActiveConnection**屬性必須已設定為有效的**連接**物件或連接字串。  
  
 如果您在*來源*引數中傳遞**命令**物件以外的內容，您可以使用*Options*引數優化*來源*引數的評估。 如果未定義 *Options* 引數，您可能會遇到效能降低的情況，因為 ADO 必須對提供者進行呼叫，以判斷引數是否為 SQL 語句、預存程式、URL 或資料表名稱。 如果您知道所使用的 *來源* 類型，設定 *Options* 引數會指示 ADO 直接跳到相關的程式碼。 如果 *選項* 引數與 *來源* 類型不符，就會發生錯誤。  
  
 如果您在*來源*引數中傳遞**資料流程**物件，則不應將資訊傳遞至其他引數。 這樣會產生錯誤。 從**資料流程**開啟**記錄集**時，不會保留**ActiveConnection**資訊。  
  
 如果沒有與**記錄集**相關聯的連接，則*選項*引數的預設值為**adCmdFile** 。 這通常會是持續儲存的 **記錄集** 物件的情況。  
  
 如果資料來源未傳回任何記錄，則提供者會將 [BOF](./bof-eof-properties-ado.md) 和 [EOF](./bof-eof-properties-ado.md) 屬性都設定為 **True**，而且目前的記錄位置是未定義的。 如果資料指標類型允許，您仍然可以將新的資料加入此空的 **記錄集** 物件。  
  
 當您已完成開啟的 **記錄集** 物件的作業時，請使用 [Close](./close-method-ado.md) 方法釋放任何相關聯的系統資源。 關閉物件並不會將它從記憶體中移除;您可以變更其屬性設定，並使用 **open** 方法，稍後再重新開啟。 若要完全消除記憶體中的物件，請將物件變數設定為 *Nothing*。  
  
 在設定**ActiveConnection**屬性之前，請呼叫**Open** with no 運算元來建立將欄位附加至**記錄集**[欄位](./fields-collection-ado.md)集合所建立之**記錄集**的實例。  
  
 如果您已將 [CursorLocation](./cursorlocation-property-ado.md) 屬性設定為 **adUseClient**，您可以透過下列兩種方式的其中一種來以非同步方式取得資料列。 建議的方法是將 *選項* 設為 **adAsyncFetch**。 或者，您可以使用 [屬性](./properties-collection-ado.md) 集合中的「非同步資料列集處理」動態屬性，但如果您未將 *Options* 參數設定為 **adAsyncFetch**，則相關的已抓取事件可能會遺失。  
  
> [!NOTE]
>  只有透過 **Open** 方法的 *Options* 參數，才支援 MS 遠端提供者中的背景提取。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
 [CommandTypeEnum](./commandtypeenum.md)和[ExecuteOptionEnum](./executeoptionenum.md)值的某些組合無效。 如需無法合併哪些選項的詳細資訊，請參閱 [ExecuteOptionEnum](./executeoptionenum.md)的主題和 [CommandTypeEnum](./commandtypeenum.md)。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 Open 和 Close 方法範例) ](./open-and-close-methods-example-vb.md)   
 [ (VBScript) 的開啟和關閉方法範例 ](./open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法範例 (VC + +) ](./open-and-close-methods-example-vc.md)   
 [ (VB) 的儲存和開啟方法範例 ](./save-and-open-methods-example-vb.md)   
 [ (ADO Connection) 的 Open 方法 ](./open-method-ado-connection.md)   
 [ (ADO 記錄) 的 Open 方法 ](./open-method-ado-record.md)   
 [ (ADO Stream 的 Open 方法) ](./open-method-ado-stream.md)   
 [OpenSchema 方法](./openschema-method.md)   
 [Save 方法](./save-method.md)