---
title: Execute 方法 (RDS) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 488b4056ca768cfae943558aefc9922bd1a16368
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288187"
---
# <a name="execute-method-rds"></a>Execute 方法 (RDS)
執行要求，並在 ADO 中建立用於 ADO 資料錄集，2.5 和更新版本。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 字串，用來連接到 OLE DB 提供者要求執行的傳送位置。 如果處理常式會指定使用*HandlerString*可以編輯或取代連接字串。  
  
 *HandlerString*  
 識別要搭配此執行的處理常式的兩個部分字串。 此字串包含兩個部分。 第一個部分包含要使用的處理常式的名稱 (ProgID)。 第二個部分包含要傳遞至處理常式的引數。 引數字串的解譯方式的詳細資料僅適用於每個處理常式。 以第一個執行個體，在字串中的逗號分隔的兩個部分。 引數字串可以包含額外的逗號。 引數是選擇性的。  
  
 *QueryString*  
 連接字串中識別 OLE DB 提供者所支援的命令語言中的命令。 對於以 SQL 為基礎的提供者， *QueryString*可能包含 TRANSACT-SQL 命令的陳述式，但是對於非 SQL 提供者 (例如，MSDataShape) 這可能不是[!INCLUDE[tsql](../../../includes/tsql_md.md)]查詢陳述式。  
  
 如果正在使用的處理常式，此處理常式可以改變，或取代此處指定的值。 例如，處理常式通常會取代*QueryString*含查詢字串，從其.ini 檔。 根據預設，會使用 Msdfmap.ini 檔案。  
  
 *lFetchOptions*  
 表示非同步擷取的類型。  
  
 如需詳細資訊，請參閱[FetchOptions 屬性 (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)。  
  
 *TableID*  
 A **Variant**型別的 VT_EMPTY 或 VT_BSTR。 如果此值為 VT_EMPTY 型別的，則會忽略它。 如果是 VT_BSTR 類型的利用建立資料錄集**adCmdTableDirect**此處指定的值和*QueryString*參數已忽略。  
  
 *lExecuteOptions*  
 位元遮罩執行選項：  
  
 1 =*ReadOnly*資料錄集將會開啟使用**Recordset**。  
  
 2 =*NoBatch*資料錄集將會開啟使用**Adlockreadonly**。  
  
 4 =*AllParamInfoSupplied*呼叫端可以保證中已提供所有參數的參數資訊*pParameters*。  
  
 8 =*GetInfo*取自 OLE DB 提供者和中傳回查詢的參數資訊*pParameters*參數。 無法執行查詢，並傳回沒有資料錄集。  
  
 16 =*GetHiddenColumns*資料錄集將會開啟使用**Adlockpessimistic**和任何隱藏的資料行都會包含在資料錄集。  
  
 *ReadOnly*， *NoBatch*和*GetHiddenColumns*是互斥的選項; 不過，不會產生設定其中的多個錯誤。 如果設定多個選項， *GetHiddenColumns*優先順序高於所有其他項目，後面接著*ReadOnly*。 如果未不指定任何選項，根據預設，使用來開啟資料錄集**Adlockpessimistic**和隱藏資料行未被納入資料錄集。  
  
 *pParameters*  
 A **Variant** ，其中包含安全陣列的參數定義。 如果*GetInfo*選項中指定了*lExecuteOptions*，這個參數用來傳回從 OLE DB 提供者取得的參數定義。 否則，這個參數可以是空的。  
  
 *lcid*  
 用來建立會傳回任何錯誤的 LCID *pInformation*。  
  
 *pInformation*  
 執行所傳回的資訊錯誤指標。 如果是 NULL，則會不傳回任何資訊時發生錯誤。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 會發生什麼情況在此情況下，端視 RDS 伺服器的設定方式而定。 處理常式的字串"MSDFMAP.handler"表示應該使用 Microsoft 提供處理常式 (Msdfmap.dll)。 處理常式的字串"MASDFMAP.handler,sample.ini 」 指出應 Msdfmap.dll 處理常式和 「 sample.ini"的引數都應該傳遞至處理常式。 MSDFMAP.dll 會解譯為以用來檢查連接和查詢字串的 sample.ini 方向的引數。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


