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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a91dacf8ea9c0ed0db2c3b64634ddd53b854a534
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307433"
---
# <a name="mixed-cursors"></a>混合資料指標

混合資料指標是索引鍵集驅動資料指標和動態資料指標的組合。 當結果集太大而無法合理地儲存整個結果集的索引鍵時，就會使用它。 混合資料指標的執行方式是建立一個小於整個結果集但大於資料列集的索引鍵集。  
  
 只要應用程式在索引鍵集內滾動，此行為就會是索引鍵集驅動。 當應用程式在索引鍵集外滾動時，其行為是動態的：資料指標會提取要求的資料列，並建立新的索引鍵集。 建立新的索引鍵集之後，此行為會還原為該索引鍵集內的索引鍵集驅動。  
  
 例如，假設結果集有1000個數據列，並使用索引鍵集大小為100且資料列集大小為10的混合資料指標。 提取第一個資料列集時，資料指標會建立一個索引鍵集，其中包含前100個數據列的索引鍵。 然後，它會依要求傳回前10個數據列。  
  
 現在假設另一個應用程式刪除資料列11和101。 如果資料指標嘗試抓取資料列11，就會遇到間距，因為它有此資料列的索引鍵，但沒有資料列存在;這是索引鍵集驅動的行為。 如果資料指標嘗試取得資料列101，資料指標將不會偵測到資料列遺失，因為它沒有資料列的索引鍵。 相反地，它會抓取先前的資料列102。 這是動態資料指標行為。  
  
 當索引鍵集大小等於結果集大小時，混合資料指標就相當於索引鍵集驅動資料指標。 當索引鍵集大小等於1時，混合資料指標就相當於動態資料指標。
