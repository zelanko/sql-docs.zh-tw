---
description: bcp_sendrow
title: bcp_sendrow |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c470244b1a739b989b5bcff36e8d0804b464bb4a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483289"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  將程式變數中的資料列傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_sendrow** 函式會從程式變數建立一個資料列，並將其傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 在呼叫 **bcp_sendrow** 之前，您必須對 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 進行呼叫，以指定包含資料列資料的程式變數。  
  
 如果呼叫 **bcp_bind** 指定 long、variable 長度的資料類型（例如 SQLTEXT 的 *eDataType* 參數和非 Null 的 *.pdata* 參數），則 **bcp_sendrow** 傳送整個資料值，就如同任何其他資料類型一樣。 但是，如果 **bcp_bind** 具有 Null *.pdata* 參數， **bcp_sendrow** 會將控制權傳回給應用程式，並在指定資料的所有資料行都傳送至之後立即將控制權傳回給應用程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 然後，應用程式可以重複呼叫 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) ，以將長的可變長度資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一次傳送給一個區塊。 如需詳細資訊，請參閱 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)。  
  
 當 **bcp_sendrow** 用來將程式變數中的資料列大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表時，只有當使用者呼叫 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) 或 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)時，才會認可資料列。 使用者可以選擇每 *n* 個數據列呼叫 **bcp_batch** 一次，或者在傳入資料的期間內有牢靠。 如果從未呼叫 **bcp_batch** ，則會在呼叫 **bcp_done** 時認可資料列。  
  
 如需從開始大量複製之重大變更的相關資訊 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，請參閱 [&#40;ODBC&#41;執行大量複製作業 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
