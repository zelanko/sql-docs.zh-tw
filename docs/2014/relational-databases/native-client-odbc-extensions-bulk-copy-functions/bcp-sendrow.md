---
title: bcp_sendrow |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 97229063d5ce78ebae1293eb85b05ee8765fc4c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029808"
---
# <a name="bcpsendrow"></a>bcp_sendrow
  將程式變數中的資料列傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_sendrow**函式會建置程式變數中的資料列，並將它傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 然後再呼叫**bcp_sendrow**，您必須進行的呼叫[bcp_bind](bcp-bind.md)即可指定包含資料列資料的程式變數。  
  
 如果**bcp_bind**指定長型、 變動長度資料類型，例如，呼叫*eDataType* SQLTEXT 和非 Null 的參數*pData*參數、 **bcp_sendrow**傳送整個資料值，就如同任何其他資料型別。 如果，不過， **bcp_bind**有 NULL *pData*參數， **bcp_sendrow**以傳送至指定的資料的所有資料行之後，立即將控制權傳回給應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 應用程式可以接著呼叫[bcp_moretext](bcp-moretext.md)重複將長型、 變動長度資料傳送給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，一次一個區塊。 如需詳細資訊，請參閱[bcp_moretext](bcp-moretext.md)。  
  
 當**bcp_sendrow**用於大量複製資料列從程式變數到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，會認可資料列在使用者呼叫時，才[bcp_batch](bcp-batch.md)或[bcp_done](bcp-done.md). 使用者可以選擇呼叫**bcp_batch**之後每個*n*資料列或內送資料的期間有暫停情況發生時。 如果**bcp_batch**是永遠不會呼叫，會認可資料列時**bcp_done**呼叫。  
  
 衄壽重大變更中大量複製中開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，請參閱[執行大量複製作業&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  