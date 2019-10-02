---
title: bcp_sendrow | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5bc7b03405d6e43a6b19cc2903875685177942e1
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707530"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  將程式變數中的資料列傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_sendrow**函式會從程式變數建立資料列，並將它傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 呼叫**bcp_sendrow**之前，您必須呼叫[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) ，以指定包含資料列資料的程式變數。  
  
 如果呼叫**bcp_bind**時指定長的可變長度資料類型（例如，SQLTEXT 的*eDataType*參數和非 Null *pData*參數）， **bcp_sendrow**就會傳送整個資料值，就像對任何其他資料所做的一樣。型. 不過，如果**bcp_bind**有 Null *pData*參數， **bcp_sendrow**會在所有具有指定資料的資料行傳送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，立即將控制權傳回給應用程式。 然後，應用程式可以重複呼叫[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) ，將長的可變長度資料傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，一次一個區塊。 如需詳細資訊，請參閱[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)。  
  
 當**bcp_sendrow**用來將程式變數中的資料列大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 個數據表時，只有在使用者呼叫[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)或[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)時，才會認可資料列。 使用者可以選擇每*n*個數據列一次呼叫**bcp_batch** ，或在傳入的資料期間內有牢靠。 如果永遠不會呼叫**bcp_batch** ，則會在呼叫**bcp_done**時認可資料列。  
  
 如需從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始大量複製的重大變更相關資訊，請參閱[執行大量複製作業&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
