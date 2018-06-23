---
title: bcp_done |Microsoft 文件
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
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 56c1d20d56d95263e93e33a45f712447b749b1be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146738"
---
# <a name="bcpdone"></a>bcp_done
  結束從程式變數大量複製[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行[bcp_sendrow](bcp-sendrow.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 在上次呼叫之後永久儲存的資料列數目[bcp_batch](bcp-batch.md)則為-1，如果發生錯誤。  
  
## <a name="remarks"></a>備註  
 呼叫**bcp_done**之後在上次呼叫[bcp_sendrow](bcp-sendrow.md)或[bcp_moretext](bcp-moretext.md)。 無法呼叫**bcp_done**之後複製所有資料會導致錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  