---
title: bcp_batch |Microsoft 文件
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
- bcp_batch
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e01952fbe3fcba497544b9defd94044bdf06bf09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035712"
---
# <a name="bcpbatch"></a>bcp_batch
  認可的所有資料列先前大量複製從程式變數，並傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 在上次呼叫後儲存的資料列數目**bcp_batch**，則為-1，如果發生錯誤。  
  
## <a name="remarks"></a>備註  
 大量複製批次會定義交易。 當應用程式使用[bcp_bind](bcp-bind.md)和**bcp_sendrow**大量複製資料列從程式變數到 SQL Server 資料表，會認可資料列僅當程式呼叫**bcp_batch**或[bcp_done](bcp-done.md)。  
  
 您可以呼叫**bcp_batch**之後每個*n*資料列或是當發生暫停情況發生 （如同在應用程式） 的內送資料中。 如果應用程式不會呼叫**bcp_batch**會認可大量複製資料列時，才**bcp_done**呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  