---
title: bcp_done |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ca26e8e8f3bdb17afe9908b99bfe5cf09ff3b563
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701977"
---
# <a name="bcp_done"></a>bcp_done
  結束從程式變數進行大量複製，以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [bcp_sendrow](bcp-sendrow.md)執行。  
  
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
  
## <a name="returns"></a>傳回  
 在最後一次呼叫[bcp_batch](bcp-batch.md)之後永久儲存的資料列數，如果發生錯誤，則為-1。  
  
## <a name="remarks"></a>備註  
 呼叫[bcp_sendrow](bcp-sendrow.md)或[bcp_moretext](bcp-moretext.md)的最後一次呼叫之後**bcp_done** 。 複製所有資料之後，無法呼叫**bcp_done**會導致錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
