---
title: bcp_sendrow |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: baf75dd4d0c9c040573a54dd102f38ef3ecd4f21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32945273"
---
# <a name="bcpsendrow"></a>bcp_sendrow
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
 **Bcp_sendrow**函式會建置程式變數中的資料列，並將它傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 然後再呼叫**bcp_sendrow**，您必須進行的呼叫[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)即可指定包含資料列資料的程式變數。  
  
 如果**bcp_bind**指定長型、 變動長度資料類型，例如，呼叫*eDataType* SQLTEXT 和非 NULL 的參數*pData*參數、 **bcp_sendrow**傳送整個資料值，就如同任何其他資料型別。 如果，不過， **bcp_bind**有 NULL *pData*參數， **bcp_sendrow**以傳送至指定的資料的所有資料行之後，立即將控制權傳回給應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 應用程式可以接著呼叫[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)重複將長型、 變動長度資料傳送給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，一次一個區塊。 如需詳細資訊，請參閱[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)。  
  
 當**bcp_sendrow**用於大量複製資料列從程式變數到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，會認可資料列在使用者呼叫時，才[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)或[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). 使用者可以選擇呼叫**bcp_batch**之後每個*n*資料列或內送資料的期間有暫停情況發生時。 如果**bcp_batch**是永遠不會呼叫，會認可資料列時**bcp_done**呼叫。  
  
 衄壽重大變更中大量複製中開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，請參閱[執行大量複製作業&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
