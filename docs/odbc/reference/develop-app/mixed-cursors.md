---
title: 混合資料指標 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16fd4840718c286adfe711b6b7322154f7f5f9cb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mixed-cursors"></a>混合的資料指標
混合的資料指標為索引鍵集驅動資料指標和動態資料指標的組合。 它用於結果集是太大，無法適當地儲存整個結果集的金鑰。 混合的資料指標是藉由建立小於整個結果集，但大於資料列集索引鍵集實作。  
  
 只要應用程式將索引鍵集內捲動，則行為是索引鍵集驅動。 當應用程式將捲動外部索引鍵集時，則行為是動態： 資料指標提取要求的資料列，並建立新的索引鍵集。 建立新的索引鍵集之後，行為會還原為索引鍵集驅動的索引鍵集內。  
  
 例如，假設有 1,000 個資料列結果集，並使用混合的資料指標索引鍵集大小為 100 且資料列集大小為 10。 當擷取第一個資料列集時，資料指標會建立索引鍵集的前 100 個資料列的索引鍵所組成。 它接著會傳回前 10 個資料列中，要求。  
  
 現在，假設另一個應用程式刪除資料列 11 和 101。 如果資料指標會嘗試擷取資料列 11，它就會發生漏洞，因為它有這個資料列的索引鍵，但沒有資料列存在，這是索引鍵集導向的行為。 如果資料指標會嘗試擷取資料列 101，資料指標不會偵測到的資料列已遺失，因為它並沒有資料列的索引鍵。 相反地，它會擷取功能先前資料列 102。 這是動態資料指標行為。  
  
 混合的資料指標相當於索引鍵集驅動資料指標時的結果集大小的索引鍵集大小相當。 索引鍵集大小等於 1 時，混合的資料指標就相當於動態資料指標。
