---
title: Synchronize21 方法（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: 454b012b8027b86256215721bdfca17122713c75
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750564"
---
# <a name="synchronize21-method-rds"></a>Synchronize21 方法 (RDS)
將指定的記錄集與連接字串所指定的資料庫同步處理，以便與 ADO 2.1 搭配使用。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 用來連接到要求將傳送至其中之 OLE DB 提供者的字串。 如果使用處理程式，處理常式就可以編輯或取代連接字串。  
  
 *HandlerString*  
 字串會識別要與此執行搭配使用的處理常式。 此字串包含兩個部分。 第一個部分包含要使用之處理常式的名稱（ProgID）。 字串的第二個部分包含要傳遞至處理常式的引數。 引數字串的解讀方式是處理常式特有的。 這兩個部分是由字串中的第一個逗號實例所分隔。 引數字串可以包含額外的逗號。 引數是選擇性的。  
  
 *lSynchronizeOptions*  
 同步處理選項的位元遮罩。  
  
 1 = 資料庫的*UpdateTransact*更新會包裝在交易中。 若有任何更新失敗，則會中止交易。  
  
 2 = 當未設定*Refresh*或*RefreshConflicts*時，*RefreshWithUpdate*會導致傳回資料列狀態。  
  
 4 =*重新*整理記錄集時，會使用資料庫中的目前資料進行重新整理。 暫止的更新不會推送到資料庫。 如果未設定此位，就不會重新整理記錄集，而且任何暫止的更新都會推送至資料庫。  
  
 8 =*RefreshConflicts*任何具有暫止變更的資料列都無法更新。 無法更新的資料列會以資料庫中的目前資料進行重新整理。  
  
 *ppRecordset*  
 要同步處理之記錄集指標的指標。  
  
 *pStatusArray*  
 Variant，用來針對受同步處理影響的資料列，傳回資料列狀態的安全陣列。 如果未設定下列同步處理選項，則未設定： *RefreshWithUpdate*、 *Refresh*和*RefreshConflicts*。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 在此情況下，會發生的情況取決於 RDS 伺服器的設定方式。 "MSDFMAP" 的處理常式字串表示應該使用 Microsoft 提供的處理常式（Msdfmap）。 "MASDFMAP" 處理常式字串 "Msdfmap" 表示應該使用處理程式，而且應該將引數 "sample" 傳遞給處理常式。 然後，Msdfmap 會將引數解讀為使用範例 .ini 來檢查連接和查詢字串的方向。  
  
> [!NOTE]
>  **Synchronize21**方法只是[SYNCHRONIZE 方法（RDS）](../../../ado/reference/rds-api/synchronize-method-rds.md)的版本。 當您需要使用**Synchronize**方法與 ADO 2.1 通訊時，可以改為呼叫**Synchronize21**方法。 ADO 2.5 和更新版本中的**Synchronize**方法功能，是在 ado 2.1 中針對相同方法提供的功能超集合。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


