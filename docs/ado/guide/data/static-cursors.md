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
ms.openlocfilehash: 520c484bdaaa6eb59488900208993a607c5b0f7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924111"
---
# <a name="static-cursors"></a>靜態資料指標
靜態資料指標一律會顯示第一次開啟資料指標時的結果集。 視執行而定，靜態資料指標為唯讀或讀取/寫入，並提供向前和向後滾動。 靜態資料指標通常不會在開啟資料指標之後，偵測對結果集的成員資格、順序或值所做的變更。 雖然不需要執行這項操作，但靜態資料指標可能會偵測自己的更新、刪除和插入。  
  
 靜態資料指標永遠不會偵測到其他更新、刪除和插入。 例如，假設靜態資料指標擷取一個資料列，而其他應用程式接著更新該資料列。 如果應用程式從靜態資料指標重新擷取該資料列，它所看到的值會保持不變，即使其他應用程式已進行變更亦然。 支援所有類型的滾動，但提供者可能會也不支援書簽。  
  
 如果您的應用程式不需要偵測資料變更，而且需要滾動，靜態資料指標就是最佳選擇。 使用**AdOpenStatic CursorTypeEnum** ，表示您想要在 ADO 中使用靜態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
