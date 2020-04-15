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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280148"
---
# <a name="supporting-local-transactions"></a>支援本機交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  工作階段分隔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式本地事務的事務範圍。 當在消費者的指示下,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]向 連接的實例提交請求時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],請求構成了 本機用戶端 OLE 資料庫提供程式的工作單元。 本地事務始終在單個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式作業階段上包裝一個或多個工作單元。  
  
 使用預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式自動提交模式,單個工作單元將被視為本地事務的範圍。 只有一個單位會參與本機交易。 建立工作階段時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式將開始工作階段的事務。 成功完成工作單位之後，就會認可該工作。 失敗時，系統會回復開始的任何工作，而且會將錯誤回報給取用者。 在這兩種情況下,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式都啟動會話的新本地事務,以便所有工作在事務中執行。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者使用者可以使用**ITransactionLocal**介面更精確地控制本地事務範圍。 當取用者工作階段起始交易時，交易起始點和最終的 **Commit** 或 **Abort** 方法呼叫之間的所有工作階段工作單位都會視為一個不可部分完成的單位。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式在消費者指示時隱式啟動事務。 如果取用者不要求保留，工作階段會還原到父交易層級的行為，也就是最常見的自動認可模式。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者支援**I事務本地::啟動事務**參數,如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*isoLevel*[in]|與此交易搭配使用的隔離等級。 在本地事務中,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE 資料庫提供者支援以下內容:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，不論是否啟用資料庫的版本控制，ISOLATIONLEVEL_SNAPSHOT 都適用於 *isoLevel* 引數。 不過，如果使用者嘗試執行執行陳述式，而未啟用版本控制且/或資料庫不是唯讀的，則會發生錯誤。 此外，如果在連接到早於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本時，將 ISOLATIONLEVEL_SNAPSHOT 指定為 *isoLevel*，則會發生 XACT_E_ISOLATIONLEVEL 錯誤。|  
|*isoFlags*[in]|本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式返回除零以外的任何值的錯誤。|  
|*pOtherOptions*[in]|如果不是 NULL,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式將從介面請求選項物件。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]選項物件的*ulTimeout*成員不是零,則本機用戶端 OLE DB 提供程式將返回XACT_E_NOTIMEOUT。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式忽略*sz 描述*成員的值。|  
|*pulTransactionLevel*[out]|如果不是 NULL,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式將返回事務的嵌套級別。|  
  
 對於本地事務,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式實現**I事務:::中止**參數,如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*pboidReason*[in]|如果設定，則略過。 可以安全地成為 NULL。|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 FALSE 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 本機用戶端 OLE 資料庫提供程式將恢復為工作階段的自動提交模式。|  
|*fAsync*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供者不支援非同步中止。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值不是 FALSE,本機用戶端 OLE 資料庫提供程式將返回XACT_E_NOTSUPPORTED。|  
  
 對於本地事務,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式實現**I事務::提交**參數,如下所示。  
  
|參數|描述|  
|---------------|-----------------|  
|*fRetaining*[in]|當為 TRUE 時，就會針對工作階段隱含地開始新的交易。 此交易必須由取用者認可或結束。 FALSE 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 本機用戶端 OLE 資料庫提供程式將恢復為工作階段的自動提交模式。|  
|*grfTC*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供者不支援非同步和階段一傳回。 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式返回XACT_E_NOTSUPPORTEDXACTTC_SYNC以外的任何值。|  
|*grfRM*[in]|必須是 0。|  
  
 作業階段[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的本機用戶端 OLE DB 提供程式列集將保留在本地提交或中止操作上,具體取決於排集屬性DBPROP_ABORTPRESERVE和DBPROP_COMMITPRESERVE的值。 默認情況下,這些屬性都是VARIANT_FALSE,並且會話上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有本機用戶端 OLE DB 提供程式行集在中止或提交操作後都會丟失。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者不實現**I 事務物件**介面。 取用者在介面上擷取參考的嘗試會傳回 E_NOINTERFACE。  
  
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
  
  
