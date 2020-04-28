---
title: 支援本機交易 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8533747bbe5ccb79a06b10a754c4af45ab241843
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280148"
---
# <a name="supporting-local-transactions"></a>支援本機交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  會話會分隔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者本機交易的交易範圍。 當取用者的方向， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB 提供者將要求提交至已連接的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例時，此要求會構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client OLE DB 提供者的工作單位。 本機交易永遠會在單一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會話上包裝一或多個工作單位。  
  
 使用預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 Native Client OLE DB 提供者自動認可模式時，會將單一工作單位視為本機交易的範圍。 只有一個單位會參與本機交易。 建立會話時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會開始會話的交易。 成功完成工作單位之後，就會認可該工作。 失敗時，系統會回復開始的任何工作，而且會將錯誤回報給取用者。 不論是哪一種[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]情況，Native Client OLE DB 提供者都會針對會話開始新的本機交易，讓所有工作都在交易內進行。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者可以使用**ITransactionLocal**介面，直接對本機交易範圍進行更精確的控制。 當取用者工作階段起始交易時，交易起始點和最終的 **Commit** 或 **Abort** 方法呼叫之間的所有工作階段工作單位都會視為一個不可部分完成的單位。 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 提供者會在用戶端導向執行此動作時，隱含地開始交易。 如果取用者不要求保留，工作階段會還原到父交易層級的行為，也就是最常見的自動認可模式。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援**ITransactionLocal：： StartTransaction**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*isoLevel*[in]|與此交易搭配使用的隔離等級。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機交易中，Native Client OLE DB 提供者支援下列各項：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，不論是否啟用資料庫的版本控制，ISOLATIONLEVEL_SNAPSHOT 都適用於 *isoLevel* 引數。 不過，如果使用者嘗試執行執行陳述式，而未啟用版本控制且/或資料庫不是唯讀的，則會發生錯誤。 此外，如果在連接到早於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本時，將 ISOLATIONLEVEL_SNAPSHOT 指定為 *isoLevel*，則會發生 XACT_E_ISOLATIONLEVEL 錯誤。|  
|*isoFlags*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會針對零以外的任何值傳回錯誤。|  
|*pOtherOptions*[in]|如果不是 Null， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會向介面要求 options 物件。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] options 物件的*ulTimeout*成員不是零，Native Client OLE DB 提供者會傳回 XACT_E_NOTIMEOUT。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會忽略*szDescription*成員的值。|  
|*pulTransactionLevel*[out]|如果不是 Null， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回交易的嵌套層級。|  
  
 若是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機交易，Native Client OLE DB 提供者會依照下列方式來執行**ITransaction：： Abort**參數。  
  
|參數|描述|  
|---------------|-----------------|  
|*pboidReason*[in]|如果設定，則略過。 可以安全地成為 NULL。|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會還原為會話的自動認可模式。|  
|*fAsync*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不支援非同步中止。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值不是 FALSE，Native Client OLE DB 提供者會傳回 XACT_E_NOTSUPPORTED。|  
  
 若是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機交易，Native Client OLE DB 提供者會依照下列方式來執行**ITransaction：： Commit**參數。  
  
|參數|描述|  
|---------------|-----------------|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會還原為會話的自動認可模式。|  
|*grfTC*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不支援非同步和第一階段傳回。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會針對 XACTTC_SYNC 以外的任何值傳回 XACT_E_NOTSUPPORTED。|  
|*grfRM*[in]|必須是 0。|  
  
 系統[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會根據資料列集屬性 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 的值，將會話上的 Native Client OLE DB 提供者資料列集保留在本機認可或中止作業上。 根據預設，這些屬性都 VARIANT_FALSE，而且會話[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的所有 Native Client OLE DB 提供者資料列集會在中止或認可作業之後遺失。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不會執行**ITransactionObject**介面。 取用者在介面上擷取參考的嘗試會傳回 E_NOINTERFACE。  
  
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
 [交易](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [使用快照隔離](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
