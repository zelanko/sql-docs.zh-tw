---
title: 大量複製文字和影像資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: rothja
ms.author: jroth
ms.openlocfilehash: 9240fd0eb8c32ed39613824ea5a07764e277160c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021260"
---
# <a name="bulk-copying-text-and-image-data"></a>大量複製 Text 與 Image 資料
  大型**text**、 **Ntext**和**image**值會使用[bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)函數進行大量複製。 您會將**text**、 **Ntext**或**image**資料行的程式碼[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) ，並將*pData*指標設定為 Null，表示將會提供**bcp_moretext**的資料。 請務必指定為每個大量複製資料列中的每個**text**、 **Ntext**或**image**資料行所提供的確切資料長度。 如果資料行的資料長度與[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)中指定的資料行長度不同，請使用[bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)將長度設定為適當的值。 [Bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)傳送所有非**文字**、非**Ntext**和非**影像**的資料;接著，您可以呼叫**bcp_moretext** ，以不同的單位傳送**text**、 **Ntext**或**image**資料。 大量複製函數會在透過**bcp_moretext**傳送的資料長度總和等於最新**bcp_collen**或**bcp_bind**中指定的長度時，判斷所有資料都已傳送給目前的**text**、 **Ntext**或**image**資料行。  
  
 **bcp_moretext**沒有用來識別資料行的參數。 當資料列中有多個**text**、 **Ntext**或**image**資料行時， **bcp_moretext**會在**text**、 **Ntext**或**image**資料行上操作，並以具有最低序數的資料行為開頭，並繼續進行序號最高的資料行。 當所傳送資料的長度總和等於最新**bcp_collen**或目前資料行**bcp_bind**中指定的長度時， **bcp_moretext**會從一個資料行移到下一個。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行大量複製作業](performing-bulk-copy-operations-odbc.md)  
  
  
