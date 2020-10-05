---
description: Execute 方法 (RDS)
title: Execute 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
author: rothja
ms.author: jroth
ms.openlocfilehash: dcb81dbe0fc719b2bb31c08a0799e4bc5084519a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720783"
---
# <a name="execute-method-rds"></a>Execute 方法 (RDS)
執行要求並建立 ADO 記錄集，以便在 ADO 2.5 和更新版本中使用。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 用來連接 OLE DB 提供者的字串，此要求將會傳送要求以供執行。 如果使用 *HandlerString* 來指定處理常式，它可以編輯或取代連接字串。  
  
 *HandlerString*  
 兩部分的字串，識別要與此執行一起使用的處理常式。 此字串包含兩個部分。 第一個部分包含要使用之處理常式 (ProgID) 的名稱。 第二個部分包含要傳遞給處理常式的引數。 如何解讀引數字串的詳細資料是每個處理常式的特定詳細資料。 這兩個部分會以字串中逗號的第一個實例隔開。 引數字串可包含額外的逗號。 引數是選擇性的。  
  
 *QueryString*  
 在連接字串中識別之 OLE DB 提供者所支援的命令語言命令。 針對以 SQL 為基礎的提供者， *QueryString* 可能包含 transact-sql 命令語句，但對於非 SQL 提供者 (例如，MSDataShape) 這可能不是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查詢語句。  
  
 如果正在使用處理程式，則處理常式可以改變或取代此處指定的值。 例如，處理常式通常會以其 .ini 檔案中的查詢字串來取代 *QueryString* 。 預設會使用 Msdfmap.ini 檔案。  
  
 *lFetchOptions*  
 表示非同步提取的型別。  
  
 如需詳細資訊，請參閱 [FetchOptions 屬性 (RDS) ](./fetchoptions-property-rds.md)。  
  
 *TableID*  
 VT_EMPTY 或 VT_BSTR 類型的 **變數** 。 如果這個值的類型為 VT_EMPTY，則會予以忽略。 如果它的類型是 VT_BSTR，則會使用 **adCmdTableDirect** 和此處指定的值來建立記錄集，並忽略 *QueryString* 參數。  
  
 *lExecuteOptions*  
 執行選項的位元遮罩：  
  
 1 =*ReadOnly* 將會使用 **adLockReadOnly**來開啟記錄集。  
  
 2 =*NoBatch* 將會使用 **adLockOptimistic**來開啟記錄集。  
  
 4 =*AllParamInfoSupplied* 呼叫端保證 *pParameters*中提供所有參數的參數資訊。  
  
 8 = 查詢的*GetInfo* 參數資訊將從 OLE DB 提供者取得，並在 *pParameters* 參數中傳回。 查詢不會執行，也不會傳回任何記錄集。  
  
 16 =*GetHiddenColumns* 將會使用 **adLockBatchOptimistic** 來開啟記錄集，而且任何隱藏的資料行都會包含在記錄集中。  
  
 *ReadOnly*、 *NoBatch* 和 *GetHiddenColumns* 都是互斥的選項;但是，它不會產生錯誤來設定一個以上的專案。 如果設定了多個選項， *GetHiddenColumns* 會優先于所有其他選項，後面接著 *ReadOnly*。 如果未指定任何選項，則預設會使用 **adLockBatchOptimistic** 來開啟記錄集，且記錄集不會包含隱藏的資料行。  
  
 *pParameters*  
 包含參數定義之安全陣列的 **Variant** 。 如果在*lExecuteOptions*中指定了*GetInfo*選項，這個參數會用來傳回從 OLE DB 提供者取得的參數定義。 否則，此參數可以是空的。  
  
 *lcid*  
 用來建立 *pInformation*中所傳回之任何錯誤的 LCID。  
  
 *pInformation*  
 Execute 所傳回的資訊錯誤指標。 如果是 Null，則不會傳回任何錯誤資訊。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 在此情況下，會發生什麼情況取決於 RDS 伺服器的設定方式。 "MSDFMAP" 處理常式字串表示應使用 Microsoft 提供的處理常式 ( # A0) 。 "MASDFMAP" 處理常式字串 "sample.ini" 表示應使用 Msdfmap.dll 處理常式，並將引數 "sample.ini" 傳遞給處理常式。 MSDFMAP.dll 會將引數解讀為使用 sample.ini 來檢查連接和查詢字串的方向。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](./datafactory-object-rdsserver.md)