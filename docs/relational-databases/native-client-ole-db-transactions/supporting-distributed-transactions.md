---
title: 支援分散式交易 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
ms.assetid: d250b43b-9260-4ea4-90cc-57d9a2f67ea7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fa228f7189e6940669f1cfbce2bb4a3e5763b22
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279985"
---
# <a name="supporting-distributed-transactions"></a>支援分散式交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供者使用者可以使用**ITransactionJoin::Join交易**方法參與由 Microsoft 分散式事務協調器 (MS DTC) 協調的分散式事務。  
  
 MS DTC 會公開 COM 物件，讓用戶端跨各種資料存放區的多個連接，起始並參與協調的交易。 要啟動事務,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式消費者使用 MS DTC **I交易分配器**介面。 **ITransactionDispenser** 的 **BeginTransaction** 成員會傳回分散式交易物件的參考。 此引用將傳遞給使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Join 事務**的原生用戶端 OLE 資料庫提供程式。  
  
 MS DTC 在分散式交易上支援非同步認可和中止。 為取得非同步交易狀態的通知，取用者會實作 **ITransactionOutcomeEvents** 介面，並將介面連接到 MS DTC 交易物件。  
  
 對於分散式事務,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式實現**I事務聯接::聯接事務**參數,如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*punkTransactionCoord*|MS DTC 交易物件的指標。|  
|*IsoLevel*|本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式忽略。 取用者從 MS DTC 取得交易物件時，會判斷 MS DTC 協調交易的隔離等級。|  
|*IsoFlags*|必須是 0。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消費者指定了任何其他值,本機用戶端 OLE 資料庫提供程式將返回XACT_E_NOISORETAIN。|  
|*POtherOptions*|如果不是 NULL,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式將從介面請求選項物件。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]選項物件的*ulTimeout*成員不是零,則本機用戶端 OLE DB 提供程式將返回XACT_E_NOTIMEOUT。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式忽略*sz 描述*成員的值。|  
  
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
 [交易](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
