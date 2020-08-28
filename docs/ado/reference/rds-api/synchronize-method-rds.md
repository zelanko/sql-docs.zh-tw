---
description: Synchronize 方法 (RDS)
title: " (RDS) 同步處理方法 |Microsoft Docs"
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 36cf462cf7f004055acedb215146d6c909175e79
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980969"
---
# <a name="synchronize-method-rds"></a>Synchronize 方法 (RDS)
將指定的記錄集與連接字串所指定的資料庫同步處理，以便在 ADO 2.5 和更新版本中使用。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 用來連接到要求將傳送至其中之 OLE DB 提供者的字串。 如果使用處理程式，處理常式可能會編輯或取代連接字串。  
  
 *HandlerString*  
 字串會識別要與此執行搭配使用的處理常式。 此字串包含兩個部分。 第一個部分包含要使用之處理常式 (ProgID) 的名稱。 字串的第二個部分包含要傳遞給處理常式的引數。 引數字串的解讀方式是處理常式特定的。 這兩個部分會以字串中逗號的第一個實例分隔 (但引數字串可能包含額外的逗號) 。 引數是選擇性的。  
  
 *lSynchronizeOptions*  
 同步處理選項的位元遮罩。  
  
 1 = 資料庫的*UpdateTransact* 更新會包裝在交易中。 如果任何更新失敗，就會中止交易。  
  
 2 = 如果沒有設定*Refresh*或*RefreshConflicts* ，*RefreshWithUpdate*會導致傳回資料列狀態。  
  
 4 = 重新整理記錄*集，並* 以資料庫中目前的資料重新整理。 暫止的更新不會推送至資料庫。 如果未設定此位，則不會重新整理記錄集，且會將任何暫止的更新推送至資料庫。  
  
 8 =*RefreshConflicts* 具有暫止變更的任何資料列無法更新。 無法更新的資料列會以資料庫中目前的資料重新整理。  
  
 *ppRecordset*  
 要同步處理之記錄集的指標。  
  
 *pStatusArray*  
 變數，用來針對受同步處理影響的資料列，傳回資料列狀態的安全陣列。 如果未設定下列任何同步處理選項，則未設定： *RefreshWithUpdate*、 *Refresh* 和 *RefreshConflicts*。  
  
 *lcid*  
 用來建立 *pInformation*中所傳回之任何錯誤的 LCID。  
  
 *pInformation*  
 **Execute**所傳回的資訊錯誤指標。 如果是 Null，則不會傳回任何錯誤資訊。  
  
## <a name="remarks"></a>備註  
 *HandlerString*參數可以是 null。 在此情況下，會發生什麼情況取決於 RDS 伺服器的設定方式。 "MSDFMAP" 處理常式字串表示應使用 Microsoft 提供的處理常式 ( # A0) 。 "MASDFMAP" 處理常式字串 "sample.ini" 表示應使用 Msdfmap.dll 處理常式，並將引數 "sample.ini" 傳遞給處理常式。 Msdfmap.dll 接著會將引數解讀為使用 sample.ini 來檢查連接和查詢字串的方向。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](./datafactory-object-rdsserver.md)