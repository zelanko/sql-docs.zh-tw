---
title: 同步處理方法 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d780c6140c1c1d09a21f7d643d7c274986b0268d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697270"
---
# <a name="synchronize-method-rds"></a>Synchronize 方法 (RDS)
使用 ADO 2.5 及更新版本中使用的連接字串所指定的資料庫，同步處理指定的資料錄集。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 字串，用來連接到 OLE DB 提供者會傳送要求。 如果處理常式，處理常式可能會編輯或取代連接字串。  
  
 *HandlerString*  
 此字串會識別要用於此執行的處理常式。 此字串包含兩個部分。 第一個部分包含要使用的處理常式的名稱 (ProgID)。 字串的第二個部分包含要傳遞至處理常式的引數。 引數字串的解譯方式，是特定的處理常式。 （雖然引數字串可能包含額外的逗號） 以第一個執行個體，在字串中的逗號分隔的兩個部分。 引數是選擇性的。  
  
 *lSynchronizeOptions*  
 同步處理選項的位元遮罩。  
  
 1 =*UpdateTransact*對資料庫的更新會包裝在交易中。 如果有任何更新失敗，則會中止交易。  
  
 2 =*RefreshWithUpdate*會導致資料列時都不會傳回狀態*重新整理*也*RefreshConflicts*設定。  
  
 4 =*重新整理*目前資料庫的資料重新整理資料錄集。 暫止的更新並未推送至資料庫。 如果未設定此位元，不會重新整理資料錄集，以及任何暫止的更新都會推送至資料庫。  
  
 8 =*RefreshConflicts*暫止的變更任何資料列無法更新。 無法更新資料列會以目前資料庫中的資料重新整理。  
  
 *ppRecordset*  
 同步處理資料錄集指標。  
  
 *pStatusArray*  
 同步處理的 variant，用來傳回受影響的資料列的資料列狀態的安全陣列。 如果未下的同步處理選項的設定，未設定：*RefreshWithUpdate*，*重新整理*並*RefreshConflicts*。  
  
 *lcid*  
 用來建立會傳回任何錯誤的 LCID *pInformation*。  
  
 *pInformation*  
 指標所傳回的資訊時發生錯誤**Execute**。 如果是 NULL，則會不傳回任何資訊時發生錯誤。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可能是 null。 在此情況下的情況取決於 RDS 伺服器的設定方式。 處理常式的字串"MSDFMAP.handler"表示應該使用 Microsoft 提供處理常式 (Msdfmap.dll)。 處理常式的字串"MASDFMAP.handler,sample.ini 」 表示，應使用 Msdfmap.dll 處理常式，然後"sample.ini"的引數應該會傳遞至處理常式。 Msdfmap.dll 然後會解譯引數，用以 sample.ini 檢查連接和查詢字串的方向。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


