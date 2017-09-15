---
title: "靜態資料指標 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd0ace9aabf10c2b7e5b34d28bd54dbde84cfd0a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="static-cursors"></a>靜態資料指標
靜態資料指標一律會將結果集時第一次開啟資料指標。 根據實作方式，靜態資料指標都是唯讀或讀取/寫入，並提供向前及向後捲動。 靜態資料指標通常無法偵測的成員資格、 順序或值之結果集資料指標開啟後所做的變更。 靜態資料指標可能偵測出自己的更新、 刪除和插入，雖然不需要這樣做。  
  
 靜態資料指標永遠不會偵測其他更新、 刪除和插入。 例如，假設在靜態資料指標提取資料列與另一個應用程式，然後再更新該資料列。 如果應用程式 refetches 靜態資料指標的資料列，它會看到的值是不變，即使其他應用程式所做的變更。 支援捲動的所有類型，但提供者可能會或可能不支援書籤。  
  
 如果您的應用程式不需要以偵測資料變更，且需要捲動，靜態資料指標會是最佳選擇。 使用**adOpenStatic CursorTypeEnum**來指出您想要使用在 ADO 中的靜態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
