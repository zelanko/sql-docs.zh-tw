---
title: 支援本機交易 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b75104940cca183005f8a465ea19d0a517247c25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213820"
---
# <a name="supporting-local-transactions"></a>支援本機交易
  工作階段會分隔交易範圍[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者本機交易。 當取用者，方向[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者提交要連接的執行個體的要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此要求會構成的工作單位[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 本機交易永遠在單一上包裝一或多個工作單位[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者工作階段。  
  
 使用預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者自動認可模式，單一工作單位視為本機交易的範圍。 只有一個單位會參與本機交易。 建立工作階段時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會開始工作階段的交易。 成功完成工作單位之後，就會認可該工作。 失敗時，系統會回復開始的任何工作，而且會將錯誤回報給取用者。 在任一情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會開始新的本機交易的工作階段，讓所有工作都在交易內都進行。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者可以直接使用的更精確地控制本機交易範圍**ITransactionLocal**介面。 當取用者工作階段起始交易時，交易起始點和最終的 **Commit** 或 **Abort** 方法呼叫之間的所有工作階段工作單位都會視為一個不可部分完成的單位。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會隱含地開始取用者引導時的交易。 如果取用者不要求保留，工作階段會還原到父交易層級的行為，也就是最常見的自動認可模式。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會支援**itransactionlocal:: Starttransaction**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*isoLevel*[in]|與此交易搭配使用的隔離等級。 在本機交易， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援下列：<br /><br /> -ISOLATIONLEVEL_UNSPECIFIED<br />-ISOLATIONLEVEL_CHAOS<br />-   ISOLATIONLEVEL_READUNCOMMITTED<br />-   ISOLATIONLEVEL_READCOMMITTED<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-ISOLATIONLEVEL_CURSORSTABILITY<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_SERIALIZABLE<br />-ISOLATIONLEVEL_ISOLATED<br />-ISOLATIONLEVEL_SNAPSHOT**附註：** 開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，ISOLATIONLEVEL_SNAPSHOT 無效*isoLevel*是否啟用資料庫的版本控制的引數。 不過，如果使用者嘗試執行執行陳述式，而未啟用版本控制且/或資料庫不是唯讀的，則會發生錯誤。 此外，如果在連接到早於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本時，將 ISOLATIONLEVEL_SNAPSHOT 指定為 *isoLevel*，則會發生 XACT_E_ISOLATIONLEVEL 錯誤。|  
|*isoFlags*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回任何值不是零的錯誤。|  
|*pOtherOptions*[in]|如果不是 NULL， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會從介面要求選項物件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回 XACT_E_NOTIMEOUT 選項物件的*ulTimeout*成員不是零。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會忽略的值*szDescription*成員。|  
|*pulTransactionLevel*[out]|如果不是 NULL， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回交易的巢狀層級。|  
  
 若是本機交易， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會實作**itransaction:: Abort**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*pboidReason*[in]|如果設定，則略過。 可以安全地成為 NULL。|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會還原到自動認可模式工作階段。|  
|*fAsync*[in]|不支援非同步中止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回 XACT_E_NOTSUPPORTED 值不是 FALSE。|  
  
 若是本機交易， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會實作**itransaction:: Commit**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會還原到自動認可模式工作階段。|  
|*grfTC*[in]|不支援非同步和第一階段傳回是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者 XACT_E_NOTSUPPORTED xacttc_sync 的任何值傳回 XACT_E_NOTSUPPORTED。|  
|*grfRM*[in]|必須是 0。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的資料列的工作階段上，保留在本機認可或中止作業根據 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 資料列集屬性的值。 根據預設，這些屬性都是 VARIANT_FALSE，而且所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者的工作階段上的資料列集將都會遺失在中止或認可作業之後。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不會實作**Itransactionobject&lt**介面。 取用者在介面上擷取參考的嘗試會傳回 E_NOINTERFACE。  
  
 此範例會使用 **ITransactionLocal**。  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>另請參閱  
 [交易](transactions.md)   
 [使用快照隔離](../native-client/features/working-with-snapshot-isolation.md)  
  
  
