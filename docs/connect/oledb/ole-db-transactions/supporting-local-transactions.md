---
title: 支援本機交易 |Microsoft Docs
description: 在 OLE DB Driver for SQL Server 的本機交易
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: bf5ac300b37f42c3d995e81d69bb0befc60ed372
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43020817"
---
# <a name="supporting-local-transactions"></a>支援本機交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  工作階段會分隔 OLE DB driver for SQL Server 的本機交易的交易範圍。 時，取用者的方向，OLE DB Driver for SQL Server 提交要求至連接的執行個體的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，此要求會構成的 OLE DB driver for SQL Server 的工作單位。 本機交易一律會將單一 OLE DB 驅動程式在一或多個工作單位的 SQL Server 工作階段。  
  
 使用預設的 OLE DB Driver for SQL Server 自動認可模式時，會將單一工作單位視為本機交易的範圍。 只有一個單位會參與本機交易。 建立工作階段時，OLE DB Driver for SQL Server 就會開始工作階段的交易。 成功完成工作單位之後，就會認可該工作。 失敗時，系統會回復開始的任何工作，而且會將錯誤回報給取用者。 在任一種情況下，OLE DB Driver for SQL Server 會針對工作階段開始一個新的本機交易，讓所有工作都在交易內進行。  
  
 OLE DB Driver for SQL Server 取用者可以使用 **ITransactionLocal** 介面，更精確地控制本機交易範圍。 當取用者工作階段起始交易時，交易起始點和最終的 **Commit** 或 **Abort** 方法呼叫之間的所有工作階段工作單位都會視為一個不可部分完成的單位。 OLE DB Driver for SQL Server 會隱含地開始的交易，取用者引導時。 如果取用者不要求保留，工作階段會還原到父交易層級的行為，也就是最常見的自動認可模式。  
  
 OLE DB Driver for SQL Server 支援**itransactionlocal:: Starttransaction**參數，如下所示。  
  
|參數|Description|  
|---------------|-----------------|  
|*isoLevel*[in]|與此交易搭配使用的隔離等級。 在本機交易，OLE DB Driver for SQL Server 支援以下功能：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，不論是否啟用資料庫的版本控制，ISOLATIONLEVEL_SNAPSHOT 都適用於 *isoLevel* 引數。 不過，如果使用者嘗試執行執行陳述式，而未啟用版本控制且/或資料庫不是唯讀的，則會發生錯誤。 此外，如果在連接到早於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本時，將 ISOLATIONLEVEL_SNAPSHOT 指定為 *isoLevel*，則會發生 XACT_E_ISOLATIONLEVEL 錯誤。|  
|*isoFlags*[in]|OLE DB Driver for SQL Server 會傳回非零的任何值的錯誤。|  
|*pOtherOptions*[in]|如果不是 NULL，OLE DB Driver for SQL Server 會從介面要求選項物件。 OLE DB Driver for SQL Server 會傳回 XACT_E_NOTIMEOUT，如果選項物件的*ulTimeout*成員不是零。 OLE DB Driver for SQL Server 會忽略值*szDescription*成員。|  
|*pulTransactionLevel*[out]|如果不是 NULL，OLE DB Driver for SQL Server 就會傳回交易的巢狀層級。|  
  
 若是本機交易，OLE DB Driver for SQL Server 會實作**itransaction:: Abort**參數，如下所示。  
  
|參數|Description|  
|---------------|-----------------|  
|*pboidReason*[in]|如果設定，則略過。 可以安全地成為 NULL。|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE，OLE DB Driver for SQL Server 會還原為自動認可模式工作階段。|  
|*fAsync*[in]|OLE DB 驅動程式適用於 SQL Server 不支援非同步中止。 如果值不是 FALSE，OLE DB Driver for SQL Server 就會傳回 XACT_E_NOTSUPPORTED。|  
  
 若是本機交易，OLE DB Driver for SQL Server 會實作**itransaction:: Commit**參數，如下所示。  
  
|參數|Description|  
|---------------|-----------------|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE，OLE DB Driver for SQL Server 會還原為自動認可模式工作階段。|  
|*grfTC*[in]|非同步和第一階段傳回不支援的 OLE DB Driver for SQL Server。 OLE DB Driver for SQL Server XACT_E_NOTSUPPORTED 以外的任何值傳回 XACT_E_NOTSUPPORTED。|  
|*grfRM*[in]|必須是 0。|  
  
 工作階段上的 OLE DB Driver for SQL Server 資料列集會根據 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 資料列集屬性的值，保留在本機認可或中止作業。 根據預設，這些屬性都是 VARIANT_FALSE，而且在中止或認可作業之後，工作階段上的所有 OLE DB Driver for SQL Server 資料列集都會遺失。  
  
 OLE DB Driver for SQL Server 不會實作**Itransactionobject&lt**介面。 取用者在介面上擷取參考的嘗試會傳回 E_NOINTERFACE。  
  
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
 [交易](../../oledb/ole-db-transactions/transactions.md)   
 [使用快照隔離](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
