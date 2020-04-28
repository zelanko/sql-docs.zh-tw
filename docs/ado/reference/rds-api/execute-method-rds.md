---
title: Execute 方法（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1a5fa5c9002d4a27490dfc98fb79f482539f042
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964310"
---
# <a name="execute-method-rds"></a>Execute 方法 (RDS)
執行要求，並建立要在 ADO 2.5 和更新版本中使用的 ADO 記錄集。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 用來連接到 OLE DB 提供者的字串，其中將會傳送要求以進行執行。 如果使用*HandlerString*來指定處理常式，它就可以編輯或取代連接字串。  
  
 *HandlerString*  
 兩部分的字串，可識別要與此執行搭配使用的處理常式。 此字串包含兩個部分。 第一個部分包含要使用之處理常式的名稱（ProgID）。 第二個部分包含要傳遞至處理常式的引數。 如何解讀引數字串的詳細資料是每個處理常式特有的。 這兩個部分是由字串中的第一個逗號實例所分隔。 引數字串可以包含額外的逗號。 引數是選擇性的。  
  
 *QueryString*  
 在連接字串中識別的 OLE DB 提供者所支援之命令語言中的命令。 對於以 SQL 為基礎的提供者， *QueryString*可能包含 transact-sql 命令語句，但對於非 SQL 提供者（例如 MSDataShape），這可能不是[!INCLUDE[tsql](../../../includes/tsql-md.md)]查詢語句。  
  
 如果正在使用處理程式，則處理常式可以改變或取代此處所指定的值。 例如，處理常式通常會以其 .ini 檔案中的查詢字串來取代*QueryString* 。 預設會使用 Msdfmap .ini 檔案。  
  
 *lFetchOptions*  
 表示非同步提取的類型。  
  
 如需詳細資訊，請參閱[FetchOptions 屬性（RDS）](../../../ado/reference/rds-api/fetchoptions-property-rds.md)。  
  
 *TableID*  
 類型為 VT_EMPTY 或 VT_BSTR 的**Variant** 。 如果這個值是 VT_EMPTY 類型，則會予以忽略。 如果它的類型是 VT_BSTR，就會使用**adCmdTableDirect**來建立記錄集，而在此處指定的值和*QueryString*參數會被忽略。  
  
 *lExecuteOptions*  
 執行選項的位元遮罩：  
  
 1 =*唯讀*：記錄集將使用**adLockReadOnly**開啟。  
  
 2 =*NoBatch*將使用**adLockOptimistic**開啟記錄集。  
  
 4 =*AllParamInfoSupplied*呼叫端保證*pParameters*中提供所有參數的參數資訊。  
  
 8 = 查詢的*GetInfo*參數資訊會從 OLE DB 提供者取得，並在*pParameters*參數中傳回。 不會執行查詢，也不會傳回任何記錄集。  
  
 16 =*GetHiddenColumns*會使用**adLockBatchOptimistic**來開啟記錄集，而且任何隱藏的資料行都將包含在記錄集中。  
  
 *ReadOnly*、 *NoBatch*和*GetHiddenColumns*是互斥的選項;不過，它不會產生錯誤來設定其中一個以上的。 如果設定了多個選項， *GetHiddenColumns*會優先于所有其他專案，後面接著*ReadOnly*。 如果未指定任何選項，則預設會使用**adLockBatchOptimistic**來開啟記錄集，而且記錄集不會包含隱藏的資料行。  
  
 *pParameters*  
 包含參數定義之安全陣列的**Variant** 。 如果已在*lExecuteOptions*中指定*GetInfo*選項，則會使用這個參數來傳回從 OLE DB 提供者取得的參數定義。 否則，這個參數可以是空的。  
  
 *lcid*  
 用來建立*pInformation*中所傳回之任何錯誤的 LCID。  
  
 *pInformation*  
 Execute 所傳回之資訊錯誤的指標。 如果是 Null，則不會傳回任何錯誤資訊。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 在此情況下，會發生的情況取決於 RDS 伺服器的設定方式。 "MSDFMAP" 的處理常式字串表示應該使用 Microsoft 提供的處理常式（Msdfmap）。 "MASDFMAP" 處理常式字串 "Msdfmap" 表示應該使用處理程式，而且應該將引數 "sample" 傳遞給處理常式。 MSDFMAP 會將引數解讀為使用範例 .ini 來檢查連接和查詢字串的方向。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


