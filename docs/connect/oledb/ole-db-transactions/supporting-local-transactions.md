---
title: 支援本機交易 (OLE DB 驅動程式)
description: 了解 OLE DB Driver for SQL Server 如何支援本機交易，以及如何使用 ITransactionLocal 更精確地控制本機交易範圍。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5923c9f475a20fe31963b907f9e7cc76ef68bb04
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861897"
---
# <a name="supporting-local-transactions"></a>支援本機交易
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  工作階段會分隔 OLE DB Driver for SQL Server 本機交易的交易範圍。 當 OLE DB Driver for SQL Server 在取用者的指示下將要求提交給以連線的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時，此要求會構成 OLE DB Driver for SQL Server 的工作單位。 本機交易一律會將一或多個工作單位包裝為單一 OLE DB Driver for SQL Server 工作階段。  
  
 使用預設的 OLE DB Driver for SQL Server 自動認可模式時，會將單一工作單位視為本機交易的範圍。 只有一個單位會參與本機交易。 已建立工作階段時，OLE DB Driver for SQL Server 會開始該工作階段的交易。 成功完成工作單位之後，就會認可該工作。 失敗時，系統會回復開始的任何工作，而且會將錯誤回報給取用者。 在任一種情況下，OLE DB Driver for SQL Server 會針對工作階段開始一個新的本機交易，讓所有工作都在交易內進行。  
  
 OLE DB Driver for SQL Server 取用者可以使用 **ITransactionLocal** 介面，更精確地控制本機交易範圍。 當取用者工作階段起始交易時，交易起始點和最終的 **Commit** 或 **Abort** 方法呼叫之間的所有工作階段工作單位都會視為一個不可部分完成的單位。 OLE DB Driver for SQL Server 會在取用者的指示下，隱含地開始交易。 如果取用者不要求保留，工作階段會還原到父交易層級的行為，也就是最常見的自動認可模式。  
  
 OLE DB Driver for SQL Server 支援 **ITransactionLocal::StartTransaction** 參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*isoLevel*[in]|與此交易搭配使用的隔離等級。 在本機交易中，OLE DB Driver for SQL Server 支援下列項目：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，不論是否啟用資料庫的版本控制，ISOLATIONLEVEL_SNAPSHOT 都適用於 *isoLevel* 引數。 不過，如果使用者嘗試執行執行陳述式，而未啟用版本控制且/或資料庫不是唯讀的，則會發生錯誤。 此外，如果在連接到早於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本時，將 ISOLATIONLEVEL_SNAPSHOT 指定為 *isoLevel*，則會發生 XACT_E_ISOLATIONLEVEL 錯誤。|  
|*isoFlags*[in]|OLE DB Driver for SQL Server 會針對非零的任何值傳回錯誤。|  
|*pOtherOptions*[in]|如果不是 NULL，OLE DB Driver for SQL Server 會從介面要求選項物件。 如果選項物件的 *ulTimeout* 成員不是零，OLE DB Driver for SQL Server 會傳回 XACT_E_NOTIMEOUT。 OLE DB Driver for SQL Server 會忽略 *szDescription* 成員的值。|  
|*pulTransactionLevel*[out]|如果不是 NULL，OLE DB Driver for SQL Server 會傳回交易的巢狀層級。|  
  
 針對本機交易，OLE DB Driver for SQL Server 會實作 **ITransaction::Abort** 參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*pboidReason*[in]|如果設定，則略過。 可以安全地成為 NULL。|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 當為 FALSE 時，OLE DB Driver for SQL Server 會還原到工作階段的自動認可模式。|  
|*fAsync*[in]|OLE DB Driver for SQL Server 不支援非同步中止。 如果值不是 FALSE，OLE DB Driver for SQL Server 會傳回 XACT_E_NOTSUPPORTED。|  
  
 針對本機交易，OLE DB Driver for SQL Server 會實作 **ITransaction::Commit** 參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 當為 FALSE 時，OLE DB Driver for SQL Server 會還原到工作階段的自動認可模式。|  
|*grfTC*[in]|OLE DB Driver for SQL Server 不支援非同步和第一階段傳回。 OLE DB Driver for SQL Server 會針對非 XACTTC_SYNC 的任何值傳回 XACT_E_NOTSUPPORTED。|  
|*grfRM*[in]|必須是 0。|  
  
 工作階段上的 OLE DB Driver for SQL Server 資料列集會根據 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 資料列集屬性的值，保留在本機認可或中止作業。 根據預設，這些屬性都是 VARIANT_FALSE，而且在中止或認可作業之後，工作階段上的所有 OLE DB Driver for SQL Server 資料列集都會遺失。  
  
 OLE DB Driver for SQL Server 不會實作 **ITransactionObject** 介面。 取用者在介面上擷取參考的嘗試會傳回 E_NOINTERFACE。  
  
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
  
  
