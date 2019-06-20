---
title: 混合資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef8d5142397b4169513cf262ba4126ccba1fc1c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785837"
---
# <a name="mixed-cursors"></a>混合資料指標

混合的資料指標為索引鍵集驅動資料指標和動態資料指標的組合。 結果集太大而無法合理地儲存整個結果集的索引鍵時，會使用其項目。 藉由建立小於整個結果集，但大於資料列集索引鍵集實作混合式資料指標。  
  
 只要應用程式將索引鍵集內捲動，則行為是索引鍵集導向。 當應用程式捲動外部索引鍵集時，行為是動態的：資料指標提取要求的資料列，並建立新的索引鍵集。 建立新的索引鍵集之後，行為會還原為索引鍵集導向的索引鍵集內。  
  
 例如，假設有 1,000 個資料列結果集，與使用 100 的索引鍵集大小和 10 個資料列集大小的混合式資料指標。 當擷取第一個資料列集時，資料指標會建立的前 100 個資料列的索引鍵所組成的索引鍵集。 然後傳回所要求的前 10 個資料列。  
  
 現在假設另一個應用程式刪除資料列 11 和 101。 如果資料指標會嘗試擷取資料列 11，它就會發生間距，因為它擁有這個資料列索引鍵，但沒有資料列存在，這是索引鍵集導向的行為。 如果資料指標會嘗試擷取資料列 101，資料指標將無法偵測的資料列已遺失，因為它並沒有資料列的索引鍵。 相反地，它會擷取功能先前資料列 102。 這是動態資料指標行為。  
  
 索引鍵集大小的結果集大小等於時，相當於索引鍵集驅動資料指標的混合式資料指標。 索引鍵集大小等於 1 時，混合式資料指標會就相當於動態資料指標。
