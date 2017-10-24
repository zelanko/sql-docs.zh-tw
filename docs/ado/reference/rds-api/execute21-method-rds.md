---
title: "Execute21 方法 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b3a985a6bb9d9e50a3a6d6741a8f379abafc26af
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="execute21-method-rds"></a>Execute21 方法 (RDS)
執行要求，並在 ADO 中 2.1 建立用於 ADO 資料錄集。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>參數  
 *連接字串*  
 字串，用來連接到 OLE DB 提供者要求執行的傳送位置。 如果處理常式會指定使用*HandlerString*，它可以編輯或取代連接字串。  
  
 *HandlerString*  
 此字串會識別要搭配此執行的處理常式。 此字串包含兩個部分。 第一個部分包含要使用的處理常式的名稱 (ProgID)。 字串的第二個部分包含要傳遞至處理常式的引數。 如何解譯引數字串是特定的處理常式。 （雖然引數字串可以包含額外的逗號分隔） 以第一個執行個體，在字串中的逗號分隔的兩個部分。 引數是選擇性的。  
  
 *查詢字串*  
 連接字串中識別 OLE DB 提供者所支援的命令語言中的命令。 對於以 SQL 為基礎的提供者，它可能包含[!INCLUDE[tsql](../../../includes/tsql_md.md)]命令陳述式，但對於非 SQL 提供者 (例如，MSDataShape) 這可能不是[!INCLUDE[tsql](../../../includes/tsql_md.md)]查詢陳述式。  
  
 此外，如果正在使用的處理常式 （且強烈建議使用的處理常式），此處理常式可以改變，或取代此處指定的值。 例如，處理常式通常會取代*QueryString*含查詢字串，從其.ini 檔。 根據預設，會使用 Msdfmap.ini 檔案。  
  
 *lMarshalOptions*  
 用來設定資料列集/資料錄集所傳回的封送處理選項。  
  
 *TableID*  
 Variant 類型 VT_EMPTY 或 VT_BSTR。 如果此值為 VT_EMPTY 型別的，則會忽略它。 如果是 VT_BSTR 類型的利用建立資料錄集**adCmdTableDirect**使用此處指定的值和*QueryString*參數已忽略。  
  
 *lExecuteOptions*  
 位元遮罩執行選項：  
  
 1 =*ReadOnly*資料錄集將會開啟使用**Recordset**。  
  
 2 =*NoBatch*資料錄集將會開啟使用**Adlockreadonly**。  
  
 4 =*AllParamInfoSupplied*呼叫端可以保證中已提供所有參數的參數資訊*pParameters*。  
  
 8 =*GetInfo*取自 OLE DB 提供者和中傳回查詢的參數資訊*pParameters*參數。 無法執行查詢，並傳回沒有資料錄集。  
  
 16 = 資料錄集將會開啟使用 GetHiddenColumns **Adlockpessimistic**和任何隱藏的資料行都會包含在資料錄集。  
  
 雖然*ReadOnly*， *NoBatch*和*GetHiddenColumns*是互斥的選項，它不是設定其中的多個錯誤。 如果設定多個選項， *GetHiddenColumns*優先順序高於所有其他選項，後面接著*ReadOnly*。 如果未不指定任何選項，根據預設，使用來開啟資料錄集**Adlockpessimistic**但不是包含隱藏的資料行中資料錄集。  
  
 *pParameters*  
 其中包含安全陣列的參數定義的變數。 如果*GetInfo*選項中指定了*lExecuteOptions*，這個參數用來傳回從 OLE DB 提供者取得的參數定義。 否則，這個參數可以是空的。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 項目，就會發生這種情況下，端視 RDS 伺服器的設定方式而定。 處理常式的字串"MSDFMAP.handler"表示應該使用 Microsoft 提供處理常式 (Msdfmap.dll)。 處理常式的字串"MASDFMAP.handler,sample.ini 」 指出應 Msdfmap.dll 處理常式和 「 sample.ini"的引數都應該傳遞至處理常式。 MSDFMAP.dll 會解譯為以用來檢查連接和查詢字串的 sample.ini 方向的引數。  
  
> [!NOTE]
>  **Execute21**方法是版本的[Execute 方法 (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)。 您要使用**Execute**方法進行通訊與 ADO 2.1， **Execute21**改為呼叫方法。 功能**Execute** ADO 2.5 和更新版本中的方法是在 ADO 2.1 中相同的方法所提供的功能的超集。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



