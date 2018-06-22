---
title: 支援本機交易 |Microsoft 文件
description: OLE DB 驅動程式中的 SQL Server 的本機交易
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 25d6c98c17c139a1658d0711bcff0c1c8f3f1d18
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689361"
---
# <a name="supporting-local-transactions"></a>支援本機交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  工作階段會分隔 OLE DB driver for SQL Server 的本機交易的交易範圍。 時，取用者的方向，在 SQL Server OLE DB 驅動程式提交要求至連接的執行個體的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，此要求會構成的 SQL Server 的 OLE DB 驅動程式的工作單位。 本機交易一律會將單一 OLE DB 驅動程式在一或多個工作單位的 SQL Server 工作階段。  
  
 使用 OLE DB 驅動程式的預設 SQL Server 自動認可模式下，單一工作單位視為本機交易的範圍。 只有一個單位會參與本機交易。 建立工作階段時，SQL Server OLE DB 驅動程式會開始該工作階段的交易。 成功完成工作單位之後，就會認可該工作。 失敗時，系統會回復開始的任何工作，而且會將錯誤回報給取用者。 在任一情況下，SQL Server OLE DB 驅動程式會開始新的本機交易的工作階段，讓所有工作都在交易內都進行。  
  
 SQL Server 取用者，OLE DB 驅動程式可以藉由直接更精確地控制本機交易範圍**ITransactionLocal**介面。 當取用者工作階段起始交易時，所有工作階段工作單位交易之間開始點和最終**認可**或**中止**方法呼叫會被視為不可部分完成的單位。 SQL Server OLE DB 驅動程式會以隱含方式開始交易在取用者引導時。 如果取用者不要求保留，工作階段會還原到父交易層級的行為，也就是最常見的自動認可模式。  
  
 SQL Server 的 OLE DB 驅動程式支援**itransactionlocal:: Starttransaction**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*isoLevel*[in]|與此交易搭配使用的隔離等級。 在本機交易中，SQL Server OLE DB 驅動程式支援以下功能：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE 的情況下**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意︰ 開頭[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，ISOLATIONLEVEL_SNAPSHOT 都是有效的*isoLevel*是否啟用資料庫的版本控制的引數。 不過，如果使用者嘗試執行執行陳述式，而未啟用版本控制且/或資料庫不是唯讀的，則會發生錯誤。 此外，如果 ISOLATIONLEVEL_SNAPSHOT 指定為將會發生 XACT_E_ISOLATIONLEVEL 錯誤*isoLevel*連線到的版本時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早於[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。|  
|*isoFlags*[in]|SQL Server OLE DB 驅動程式會傳回錯誤的任何非零的值。|  
|*pOtherOptions*[in]|如果不是 NULL，SQL Server OLE DB 驅動程式會從介面要求選項物件。 SQL Server OLE DB 驅動程式會傳回 XACT_E_NOTIMEOUT 如果選項物件*ulTimeout*成員不是零。 SQL Server OLE DB 驅動程式會略過的值*szDescription*成員。|  
|*pulTransactionLevel*[out]|如果不是 NULL，SQL Server OLE DB 驅動程式傳回交易的巢狀層級。|  
  
 若是本機交易，SQL Server OLE DB 驅動程式會實作**itransaction:: Abort**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*pboidReason*[in]|如果設定，則略過。 可以安全地成為 NULL。|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE，SQL Server OLE DB 驅動程式會還原到自動認可模式工作階段。|  
|*fAsync*[in]|OLE DB 驅動程式適用於 SQL Server 不支援非同步中止。 如果值不是 FALSE，SQL Server OLE DB 驅動程式會傳回 XACT_E_NOTSUPPORTED。|  
  
 若是本機交易，SQL Server OLE DB 驅動程式會實作**itransaction:: Commit**參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 若為 FALSE，SQL Server OLE DB 驅動程式會還原到自動認可模式工作階段。|  
|*grfTC*[in]|非同步和第一階段傳回不支援的 OLE DB 驅動程式的 SQL Server。 SQL Server OLE DB 驅動程式 XACT_E_NOTSUPPORTED 以外的任何值傳回 XACT_E_NOTSUPPORTED。|  
|*grfRM*[in]|必須是 0。|  
  
 SQL Server 會保留在本機認可或中止作業中的工作階段上的資料列集，OLE DB 驅動程式根據 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 資料列集屬性的值。 根據預設，這些屬性會是 VARIANT_FALSE，而且所有 OLE DB 驅動程式的 SQL Server 的工作階段上的資料列集都會遺失中止或認可作業。  
  
 SQL Server OLE DB 驅動程式不會實作**j**介面。 取用者在介面上擷取參考的嘗試會傳回 E_NOINTERFACE。  
  
 這個範例會使用**ITransactionLocal**。  
  
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
  
  
