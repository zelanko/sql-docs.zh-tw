---
title: bcp_sendrow |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2810dd25a14f35ed275a7d1117fc21d7946cc90e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423537"
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
 **Bcp_sendrow**函式建立一個資料列從程式變數，並將它傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 然後再呼叫**bcp_sendrow**，您必須對進行呼叫[bcp_bind](bcp-bind.md)即可指定包含資料列資料的程式變數。  
  
 如果**bcp_bind**指定為長型、 變動長度資料類型，例如，呼叫*eDataType* SQLTEXT 和非 Null 的參數*pData*參數，則**bcp_sendrow**會傳送整個資料值，就如同任何其他資料型別。 如果，不過， **bcp_bind**有 NULL *pData*參數**bcp_sendrow**以傳送至指定的資料的所有資料行之後，立即將控制權傳回給應用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 應用程式接著可以呼叫[bcp_moretext](bcp-moretext.md)重複將長型、 變動長度資料傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，一次一個區塊。 如需詳細資訊，請參閱 < [bcp_moretext](bcp-moretext.md)。  
  
 當**bcp_sendrow**用來複製資料列從程式變數大量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，會認可資料列只有在使用者呼叫時，才[bcp_batch](bcp-batch.md)或[bcp_done](bcp-done.md). 使用者可以選擇呼叫**bcp_batch**一旦每*n*資料列或內送資料的期間有暫停情況發生時。 如果**bcp_batch**是絕不會呼叫，會認可資料列時**bcp_done**呼叫。  
  
 如需中斷變更中大量複製中的開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，請參閱 <<c2> [ 執行大量複製作業&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)。</c2>  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
