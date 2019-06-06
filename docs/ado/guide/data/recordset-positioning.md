---
title: 資料錄集定位 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c01d24a5f92b4bca1e5b41a0cbece980237fd961
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701676"
---
# <a name="recordset-positioning"></a>資料錄集定位
使用**AbsolutePosition**屬性，以移至記錄，根據其序數位置中**資料錄集**物件，或若要判斷目前的資料錄的序數位置。 提供者必須支援這個屬性才能使用適當的功能。  
  
 **AbsolutePosition**是以 1 為基礎，並等於 1，當目前的記錄中的第一個記錄**資料錄集**。 如先前所述，您可以取得中的記錄總數**Recordset**物件**RecordCount**屬性。  
  
 當您設定**AbsolutePosition**屬性，即使它是目前的快取中的記錄 ADO 重新載入快取以一組新的記錄從您指定的記錄。 **CacheSize**屬性會決定此群組的大小。  
  
> [!NOTE]
>  您不應該使用**AbsolutePosition**屬性做 surrogate 的記錄數目。 當您刪除先前的記錄，就會變更指定記錄的位置。 也可以指定的記錄會有相同的不保證**AbsolutePosition**如果**資料錄集**物件查詢，或重新開啟。 書籤的建議方式是的保留，並傳回指定的位置和是唯一的方法在所有類型的定位**資料錄集**物件。
