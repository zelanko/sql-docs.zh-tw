---
title: bcp_batch | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_batch
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1aa705c42846b02ae67eb66eba38660e724bf2e
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="bcpbatch"></a>bcp_batch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  認可的所有資料列先前大量複製從程式變數，並傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBINT bcp_batch (HDBC  
        hdbc);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 在上次呼叫後儲存的資料列數目**bcp_batch**，則為-1，如果發生錯誤。  
  
## <a name="remarks"></a>備註  
 大量複製批次會定義交易。 當應用程式使用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和**bcp_sendrow**大量複製資料列從程式變數到 SQL Server 資料表，會認可資料列僅當程式呼叫**bcp_batch**或[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)。  
  
 您可以呼叫**bcp_batch**之後每個 *n* 資料列或是當發生暫停情況發生 （如同在應用程式） 的內送資料中。 如果應用程式不會呼叫**bcp_batch**會認可大量複製資料列時，才**bcp_done**呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
