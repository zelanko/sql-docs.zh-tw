---
title: Execute21 方法（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8434345dcc4436865e4981a19ef1164d35a852f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964206"
---
# <a name="execute21-method-rds"></a>Execute21 方法 (RDS)
執行要求，並建立 ADO 記錄以用於 ADO 2.1。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 用來連接到 OLE DB 提供者的字串，其中將會傳送要求以進行執行。 如果使用*HandlerString*來指定處理常式，它就可以編輯或取代連接字串。  
  
 *HandlerString*  
 字串會識別要與此執行搭配使用的處理常式。 此字串包含兩個部分。 第一個部分包含要使用之處理常式的名稱（ProgID）。 字串的第二個部分包含要傳遞至處理常式的引數。 引數字串的解讀方式是處理常式特有的。 這兩個部分會以字串中的第一個逗號實例分隔（雖然引數字串可以包含其他逗號）。 引數是選擇性的。  
  
 *QueryString*  
 在連接字串中識別的 OLE DB 提供者所支援之命令語言中的命令。 對於以 SQL 為基礎的提供者，它[!INCLUDE[tsql](../../../includes/tsql-md.md)]可能包含 command 語句，但對於非 SQL 提供者（例如 MSDataShape），這可能不是[!INCLUDE[tsql](../../../includes/tsql-md.md)]查詢語句。  
  
 此外，如果正在使用處理程式（而且強烈建議使用處理程式），則處理常式可以改變或取代此處所指定的值。 例如，處理常式通常會以其 .ini 檔案中的查詢字串來取代*QueryString* 。 預設會使用 Msdfmap .ini 檔案。  
  
 *lMarshalOptions*  
 用來設定所傳回之資料列集/記錄集的封送處理選項。  
  
 *TableID*  
 類型為 VT_EMPTY 或 VT_BSTR 的 variant。 如果這個值是 VT_EMPTY 類型，則會予以忽略。 如果它的類型是 VT_BSTR，就會使用**adCmdTableDirect**來建立記錄集，並使用這裡指定的值，並忽略*QueryString*參數。  
  
 *lExecuteOptions*  
 執行選項的位元遮罩：  
  
 1 =*唯讀*：記錄集將使用**adLockReadOnly**開啟。  
  
 2 =*NoBatch*將使用**adLockOptimistic**開啟記錄集。  
  
 4 =*AllParamInfoSupplied*呼叫端保證*pParameters*中提供所有參數的參數資訊。  
  
 8 = 查詢的*GetInfo*參數資訊會從 OLE DB 提供者取得，並在*pParameters*參數中傳回。 不會執行查詢，也不會傳回任何記錄集。  
  
 16 = GetHiddenColumns 會使用**adLockBatchOptimistic**來開啟記錄集，而且任何隱藏的資料行都將包含在記錄集中。  
  
 雖然*ReadOnly*、 *NoBatch*和*GetHiddenColumns*是互斥的選項，但設定其中一個以上並不會產生錯誤。 如果設定了多個選項， *GetHiddenColumns*會優先于所有其他選項，後面接著*ReadOnly*。 如果未指定任何選項，則預設會使用**adLockBatchOptimistic**來開啟記錄集，但是記錄集內不會包含隱藏的資料行。  
  
 *pParameters*  
 包含參數定義之安全陣列的 variant。 如果已在*lExecuteOptions*中指定*GetInfo*選項，則會使用這個參數來傳回從 OLE DB 提供者取得的參數定義。 否則，這個參數可能是空的。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 在此情況下，會根據 RDS 伺服器的設定方式而定。 "MSDFMAP" 的處理常式字串表示應該使用 Microsoft 提供的處理常式（Msdfmap）。 "MASDFMAP" 處理常式字串 "Msdfmap" 表示應該使用處理程式，而且應該將引數 "sample" 傳遞給處理常式。 MSDFMAP 會將引數解讀為使用範例 .ini 來檢查連接和查詢字串的方向。  
  
> [!NOTE]
>  **Execute21**方法是[EXECUTE 方法（RDS）](../../../ado/reference/rds-api/execute-method-rds.md)的版本。 當您需要使用**Execute**方法與 ADO 2.1 通訊時，可以改為呼叫**Execute21**方法。 在 ADO 2.5 和更新版本中， **Execute**方法的功能是在 ado 2.1 中針對相同方法提供的功能超集合。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


