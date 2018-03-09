---
title: "大量複製 Text 與 Image 資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67b2cf5a000fc96468536bffcb07a9955be5592e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="bulk-copying-text-and-image-data"></a>大量複製 Text 與 Image 資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  大型**文字**， **ntext**，和**映像**值會使用大量複製使用[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)函式。 您撰寫程式碼[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)如**文字**， **ntext**，或**映像**具有資料行*pData*指標設定為NULL 表示資料會提供**bcp_moretext**。 請務必指定每個提供資料的確切長度**文字**， **ntext**，或**映像**中每個大量複製資料列的資料行。 如果資料行資料的長度不同於指定的資料行長度[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)，使用[bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)長度設定為適當的值。 A [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)傳送所有非**文字**、 非-**ntext**，和非-**映像**資料; 您可以接著呼叫**bcp_moretext**傳送**文字**， **ntext**，或**映像**個別單位中的資料。 目前，已傳送所有資料的大量複製函數決定**文字**， **ntext**，或**映像**透過傳送之資料的長度總和的資料行**bcp_moretext**等於指定的最新的長度**bcp_collen**或**bcp_bind**。  
  
 **bcp_moretext**沒有識別資料行的參數。 如果有多個**文字**， **ntext**，或**映像**列中的資料行**bcp_moretext**上運作**文字**， **ntext**，或**映像**開頭具有最低的序號，並繼續到具有最高的序數號碼資料行的資料行的資料行。 **bcp_moretext**傳送的資料長度總和等於指定的最新的長度時，從一個資料行移至下一個**bcp_collen**或**bcp_bind**目前的資料行。  
  
## <a name="see-also"></a>另請參閱  
 [執行大量複製作業 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
