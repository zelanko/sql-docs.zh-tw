---
title: 靜態資料指標 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8815522ee4f9a4221887696a23a201910d7cfad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062834"
---
# <a name="static-cursors"></a>靜態資料指標
靜態資料指標一律會顯示的結果集時的第一次開啟資料指標。 根據實作中，靜態資料指標都是唯讀或讀取/寫入，並提供向前及向後捲動。 靜態資料指標通常無法偵測成員資格、 順序或結果集資料指標開啟後的值所做的變更。 雖然不需要執行這項操作，但靜態資料指標可能會偵測自己的更新、刪除和插入。  
  
 靜態資料指標永遠不會偵測其他更新、 刪除和插入。 例如，假設靜態資料指標擷取一個資料列，而其他應用程式接著更新該資料列。 如果應用程式從靜態資料指標重新擷取該資料列，它所看到的值會保持不變，即使其他應用程式已進行變更亦然。 支援所有類型的捲動，但提供者可能會或可能不支援書籤。  
  
 如果您的應用程式不需要偵測資料變更，且需要捲動，靜態資料指標就會是最佳選擇。 使用  **adOpenStatic CursorTypeEnum**來指出您想要使用在 ADO 中的靜態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
