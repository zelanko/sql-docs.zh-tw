---
title: 混合游標 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307433"
---
# <a name="mixed-cursors"></a>混合資料指標

混合游標是鍵集驅動的游標和動態游標的組合。 當結果集太大而無法合理地保存整個結果集的鍵時,將使用它。 通過創建小於整個結果集但大於行集的鍵集實現混合游標。  
  
 只要應用程式在密鑰集中滾動,該行為就是按鍵集驅動的。 當應用程式在密鑰集外部滾動時,行為是動態的:游標獲取請求的行並創建新的鍵集。 創建新鍵集后,該行為將恢復為該鍵集中內的鍵集驅動。  
  
 例如,假設結果集具有 1,000 行,並使用鍵集大小為 100 和行集大小為 10 的混合游標。 提取第一個行集時,游標將創建一個鍵集,其中包含前 100 行的鍵。 然後,它根據需要返回前 10 行。  
  
 現在假設另一個應用程式刪除行 11 和 101。 如果游標嘗試檢索行 11,它將遇到間隙,因為它具有此行的鍵,但不存在任何行;這是鍵集驅動的行為。 如果游標嘗試檢索行 101,游標將不會檢測到該行丟失,因為它沒有該行的鍵。 相反,它將檢索以前第 102 行的內容。 這是動態遊標行為。  
  
 當鍵集大小等於結果集大小時,混合游標等效於鍵集驅動的游標。 當鍵集大小等於 1 時,混合游標等效於動態游標。
