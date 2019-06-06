---
title: Execute21 方法 (RDS) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 1c65fe01fef6ba2cab2f41ca056bb96a8ef50f39
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707855"
---
# <a name="execute21-method-rds"></a>Execute21 方法 (RDS)
執行要求，並在 ADO 2.1 中建立用於 ADO 資料錄集。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 字串，用來連接到 OLE DB 提供者將要求傳送供執行。 如果使用指定的處理常式*HandlerString*，它可以編輯或取代連接字串。  
  
 *HandlerString*  
 此字串會識別要用於此執行的處理常式。 此字串包含兩個部分。 第一個部分包含要使用的處理常式的名稱 (ProgID)。 字串的第二個部分包含要傳遞至處理常式的引數。 引數字串的解譯方式，是特定的處理常式。 （雖然引數字串可以包含額外的逗號） 以第一個執行個體，在字串中的逗號分隔的兩個部分。 引數是選擇性的。  
  
 *QueryString*  
 中所識別的連接字串中的 OLE DB 提供者支援的命令語言的命令。 對於以 SQL 為基礎的提供者，它可能包含[!INCLUDE[tsql](../../../includes/tsql-md.md)]命令陳述式，但對於非 SQL 提供者 (例如 MSDataShape) 這可能不是[!INCLUDE[tsql](../../../includes/tsql-md.md)]查詢陳述式。  
  
 此外，如果正在使用的處理常式 （且強烈建議使用的處理常式），則處理常式可以改變，或取代這裡指定的值。 例如，處理常式通常會取代*QueryString*包含查詢字串從其.ini 檔。 根據預設，會使用 Msdfmap.ini 檔案。  
  
 *lMarshalOptions*  
 用來設定資料列集/資料錄集所傳回的封送處理選項。  
  
 *TableID*  
 Variant 類型為 VT_EMPTY 或 VT_BSTR。 如果此值為 VT_EMPTY 型別的，則會忽略它。 如果是 VT_BSTR 類型的資料錄集由使用**adCmdTableDirect**這裡使用指定的值和*QueryString*參數會被忽略。  
  
 *lExecuteOptions*  
 位元遮罩執行選項：  
  
 1 =*ReadOnly*使用也會開啟資料錄集**Recordset**。  
  
 2 =*NoBatch*使用也會開啟資料錄集**adLockOptimistic**。  
  
 4 =*AllParamInfoSupplied*呼叫端可以保證中會提供所有參數的參數資訊*pParameters*。  
  
 8 =*GetInfo*將從 OLE DB 提供者取得並傳回查詢的參數資訊*pParameters*參數。 不會執行查詢，並傳回任何資料錄集。  
  
 16 = 使用也會開啟資料錄集的 GetHiddenColumns **Adlockpessimistic**任何隱藏的資料行將包含在資料錄集。  
  
 雖然*ReadOnly*， *NoBatch*並*GetHiddenColumns*是互斥的選項，它不是設定以上其中一個錯誤。 如果設定了多個選項， *GetHiddenColumns*優先順序高於所有其他選項，後面接著*ReadOnly*。 如果未不指定任何選項，根據預設，資料錄集使用開啟**Adlockpessimistic**但隱藏的資料行不包含資料錄集。  
  
 *pParameters*  
 變數包含安全陣列的參數定義。 如果*GetInfo*選項中指定了*lExecuteOptions*，這個參數用來傳回取自 OLE DB 提供者的參數定義。 否則，這個參數可以是空的。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可能是 null。 項目，就會發生這種情況下，端視 RDS 伺服器的設定方式而定。 處理常式的字串"MSDFMAP.handler"表示應該使用 Microsoft 提供處理常式 (Msdfmap.dll)。 處理常式的字串"MASDFMAP.handler,sample.ini 」 表示，應使用 Msdfmap.dll 處理常式，然後"sample.ini"的引數應該會傳遞至處理常式。 MSDFMAP.dll 將解譯的方向，用以 sample.ini 檢查連接和查詢字串引數。  
  
> [!NOTE]
>  **Execute21**方法是版本[Execute 方法 (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)。 您要使用**Execute**方法進行通訊與 ADO 2.1 **Execute21**改為呼叫方法。 功能**Execute** ADO 2.5 及更新版本中的方法是提供給相同的方法，在 ADO 2.1 的功能超集。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


