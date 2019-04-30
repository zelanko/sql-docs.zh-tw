---
title: 動態資料指標 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0d7a19476a00fb88e0b2195c761993f91b7a5d4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161788"
---
# <a name="dynamic-cursors"></a>動態資料指標
動態資料指標偵測到所有資料列的結果集，不論是否發生的變更從資料指標內或資料指標之外的其他使用者所做的變更。 所有的 insert、 update 和 delete 陳述式所做的所有使用者可透過資料指標。 動態資料指標可以偵測資料列、 順序和結果集資料指標開啟後的值所做的變更。 資料指標之外所做的更新不會顯示，直到 （除非資料指標交易隔離等級設為 「 認可 」） 經過認可為止。  
  
 例如，假設動態資料指標會擷取兩個資料列和另一個應用程式，然後更新其中一個資料列，並刪除其他。 如果動態資料指標之後擷取這些資料列，它會找不到已刪除的資料列，但會顯示已更新資料列的新值。  
  
 如果您的應用程式必須偵測到所有其他使用者所進行的並行更新，動態資料指標會是不錯的選擇。 使用  **adOpenDynamic CursorTypeEnum**來指出您想要使用動態資料指標在 ADO 中。  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [靜態資料指標](../../../ado/guide/data/static-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)
