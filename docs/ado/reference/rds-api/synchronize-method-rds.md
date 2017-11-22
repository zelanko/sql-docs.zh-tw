---
title: "同步處理方法 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c69217abc435fb4b3438975db560b9ce5836ee8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="synchronize-method-rds"></a>同步處理方法 (RDS)
使用 ADO 2.5 和更新版本中使用的連接字串所指定的資料庫，同步處理指定的資料錄集。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>參數  
 *連接字串*  
 字串，用來連接到 OLE DB 提供者會傳送要求的位置。 如果使用處理常式，此處理常式可能編輯或取代連接字串。  
  
 *HandlerString*  
 此字串會識別要搭配此執行的處理常式。 此字串包含兩個部分。 第一個部分包含要使用的處理常式的名稱 (ProgID)。 字串的第二個部分包含要傳遞至處理常式的引數。 如何解譯引數字串是特定的處理常式。 （雖然引數字串可能包含額外的逗號分隔） 以第一個執行個體，在字串中的逗號分隔的兩個部分。 引數是選擇性的。  
  
 *lSynchronizeOptions*  
 同步處理選項的位元遮罩。  
  
 1 =*UpdateTransact*對資料庫的更新會包裝在交易中。 如果有任何更新失敗，交易便會中止。  
  
 2 =*RefreshWithUpdate*原因資料列時都不會傳回狀態*重新整理*也*RefreshConflicts*設定。  
  
 4 =*重新整理*目前資料庫中的資料重新整理資料錄集。 擱置的更新無法推送至資料庫。 如果未設定此位元，不會重新整理資料錄集，和任何擱置的更新會推入至資料庫。  
  
 8 =*RefreshConflicts*暫止的變更與任何資料列無法更新。 無法更新的資料列會重新整理目前資料庫中的資料。  
  
 *ppRecordset*  
 同步處理資料錄集指標。  
  
 *pStatusArray*  
 Variant，用來傳回安全陣列之影響的資料列的資料列狀態的同步處理。 如果沒有任何下列的同步處理選項的設定不會設定： *RefreshWithUpdate*，*重新整理*和*RefreshConflicts*。  
  
 *lcid*  
 用來建立會傳回任何錯誤的 LCID *pInformation*。  
  
 *pInformation*  
 指標所傳回的資訊錯誤**Execute**。 如果是 NULL，則會不傳回任何資訊時發生錯誤。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 會發生什麼情況在此情況下，端視 RDS 伺服器的設定方式而定。 處理常式的字串"MSDFMAP.handler"表示應該使用 Microsoft 提供處理常式 (Msdfmap.dll)。 處理常式的字串"MASDFMAP.handler,sample.ini 」 指出應 Msdfmap.dll 處理常式和 「 sample.ini"的引數都應該傳遞至處理常式。 Msdfmap.dll 然後將用來檢查連接和查詢字串的 sample.ini 方向為解譯引數。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


