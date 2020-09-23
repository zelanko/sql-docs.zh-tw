---
title: 支援分散式交易 (OLE DB 驅動程式)
description: 了解 OLE DB Driver for SQL Server 取用者如何使用 ITransactionJoin::JoinTransaction 方法來參與分散式交易。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71f782b415c61d4a9a180664ee6d2bbf357ac4cc
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861848"
---
# <a name="supporting-distributed-transactions"></a>支援分散式交易
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 取用者可以使用 **ITransactionJoin::JoinTransaction** 方法來參與 Microsoft 分散式交易協調器 (MS DTC) 協調的分散式交易。  
  
 MS DTC 會公開 COM 物件，讓用戶端跨各種資料存放區的多個連接，起始並參與協調的交易。 為起始交易，OLE DB Driver for SQL Server 取用者會使用 MS DTC **ITransactionDispenser** 介面。 **ITransactionDispenser** 的 **BeginTransaction** 成員會傳回分散式交易物件的參考。 此參考會使用 **JoinTransaction**，傳遞到 OLE DB Driver for SQL Server。  
  
 MS DTC 在分散式交易上支援非同步認可和中止。 為取得非同步交易狀態的通知，取用者會實作 **ITransactionOutcomeEvents** 介面，並將介面連接到 MS DTC 交易物件。  
  
 若是分散式交易，OLE DB Driver for SQL Server 會實作 **ITransactionJoin::JoinTransaction** 參數，如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*punkTransactionCoord*|MS DTC 交易物件的指標。|  
|*IsoLevel*|會由 OLE DB Driver for SQL Server 所忽略。 取用者從 MS DTC 取得交易物件時，會判斷 MS DTC 協調交易的隔離等級。|  
|*IsoFlags*|必須是 0。 如果取用者指定其他任何值，OLE DB Driver for SQL Server 會傳回 XACT_E_NOISORETAIN。|  
|*POtherOptions*|如果不是 NULL，OLE DB Driver for SQL Server 會從介面要求選項物件。 如果選項物件的 *ulTimeout* 成員不是零，OLE DB Driver for SQL Server 會傳回 XACT_E_NOTIMEOUT。 OLE DB Driver for SQL Server 會忽略 *szDescription* 成員的值。|  
  
 這個範例會使用 MS DTC 協調交易。  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
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
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>另請參閱  
 [交易](../../oledb/ole-db-transactions/transactions.md)  
  
  
