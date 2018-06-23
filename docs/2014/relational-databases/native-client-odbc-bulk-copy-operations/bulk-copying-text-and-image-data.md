---
title: 大量複製 Text 與 Image 資料 |Microsoft 文件
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
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c674c24b4000ada4651dfb44ed2d49e9fd5bde83
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029821"
---
# <a name="bulk-copying-text-and-image-data"></a>大量複製 Text 與 Image 資料
  大型**文字**， **ntext**，和**映像**值會使用大量複製使用[bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)函式。 您撰寫程式碼[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)如**文字**， **ntext**，或**映像**具有資料行*pData*指標設定為NULL 表示資料會提供**bcp_moretext**。 請務必指定每個提供資料的確切長度**文字**， **ntext**，或**映像**中每個大量複製資料列的資料行。 如果資料行資料的長度不同於指定的資料行長度[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)，使用[bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)長度設定為適當的值。 A [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)傳送所有非**文字**、 非-**ntext**，和非-**映像**資料; 您可以接著呼叫**bcp_moretext**傳送**文字**， **ntext**，或**映像**個別單位中的資料。 目前，已傳送所有資料的大量複製函數決定**文字**， **ntext**，或**映像**透過傳送之資料的長度總和的資料行**bcp_moretext**等於指定的最新的長度**bcp_collen**或**bcp_bind**。  
  
 **bcp_moretext**沒有識別資料行的參數。 如果有多個**文字**， **ntext**，或**映像**列中的資料行**bcp_moretext**上運作**文字**， **ntext**，或**映像**開頭具有最低的序號，並繼續到具有最高的序數號碼資料行的資料行的資料行。 **bcp_moretext**傳送的資料長度總和等於指定的最新的長度時，從一個資料行移至下一個**bcp_collen**或**bcp_bind**目前的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [執行大量複製作業&#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  