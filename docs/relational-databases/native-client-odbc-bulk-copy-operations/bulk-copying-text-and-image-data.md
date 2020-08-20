---
description: 大量複製 Text 與 Image 資料
title: 大量複製文字和影像資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55635292fab4a720e706cb62797bce4d1a1ce378
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455939"
---
# <a name="bulk-copying-text-and-image-data"></a>大量複製 Text 與 Image 資料
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  大型的 **text**、 **Ntext**和 **image** 值是使用 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) 函數進行大量複製。 您會將**text**、 **Ntext**或**image**資料行的[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)程式碼，並將 *.pdata*指標設為 Null，表示將會提供**bcp_moretext**的資料。 請務必在每個大量複製的資料列中，指定針對每個 **text**、 **Ntext**或 **image** 資料行提供的確切資料長度。 如果資料行的資料長度與 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)中指定的資料行長度不同，請使用 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) 將長度設定為適當的值。 [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)傳送所有非**文字**、非**Ntext**和非**影像**的資料;然後，您可以呼叫**bcp_moretext** ，以不同的單位來傳送**text**、 **Ntext**或**image**資料。 大量複製函數會在透過**bcp_moretext**傳送的資料長度總和等於最新**bcp_collen**或**bcp_bind**中指定的長度時，判斷已傳送目前**text**、 **Ntext**或**image**資料行的所有資料。  
  
 **bcp_moretext** 沒有用來識別資料行的參數。 當資料列中有多個 **text**、 **Ntext**或 **image** 資料行時， **bcp_moretext** 會在 **text**、 **Ntext**或 **image** 資料行上作業，從具有最小序號的資料行開始，然後繼續至序號最高的資料行。 當所傳送資料的長度總和等於目前資料行的最新**bcp_collen**或**bcp_bind**中指定的長度時， **bcp_moretext**會從一個資料行移到下一個資料行。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行大量複製作業 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
