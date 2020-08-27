---
description: 靜態資料指標
title: 靜態資料指標 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: rothja
ms.author: jroth
ms.openlocfilehash: 65ca384d89c4afbeeb24120debfd2ead5c2716ed
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979549"
---
# <a name="static-cursors"></a>靜態資料指標
靜態資料指標一律會顯示第一次開啟資料指標時的結果集。 根據執行的不同，靜態資料指標是唯讀或讀取/寫入，可提供向前及向後滾動。 靜態資料指標通常不會偵測到資料指標開啟後對結果集的成員資格、順序或值所做的變更。 雖然不需要執行這項操作，但靜態資料指標可能會偵測自己的更新、刪除和插入。  
  
 靜態資料指標絕對不會偵測到其他更新、刪除和插入。 例如，假設靜態資料指標擷取一個資料列，而其他應用程式接著更新該資料列。 如果應用程式從靜態資料指標重新擷取該資料列，它所看到的值會保持不變，即使其他應用程式已進行變更亦然。 所有類型的滾動都受到支援，但提供者不一定支援書簽。  
  
 如果您的應用程式不需要偵測資料變更，而且需要滾動，則靜態資料指標是最佳選擇。 使用 **AdOpenStatic CursorTypeEnum** 來指出您想要在 ADO 中使用靜態資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
