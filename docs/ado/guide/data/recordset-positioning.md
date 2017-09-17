---
title: "資料錄集定位 |Microsoft 文件"
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
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aee0d64d0fe1e310f42d79de36f5cf36c3813bf3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-positioning"></a>定位資料錄集
使用**AbsolutePosition**屬性移至資料，根據其序數位置中**資料錄集**物件，或要判定目前記錄的序數位置。 提供者必須支援這個屬性才能使用適當的功能。  
  
 **AbsolutePosition**是以 1 為基礎，並且等於 1，目前的記錄時的第一個記錄**資料錄集**。 如先前所述，您可以取得中的記錄總數**資料錄集**物件從**RecordCount**屬性。  
  
 當您將**AbsolutePosition**屬性，即使它是目前的快取中的記錄 ADO 重新載入快取以一組新的記錄從您指定的記錄。 **CacheSize**屬性會決定此群組的大小。  
  
> [!NOTE]
>  您不應該使用**AbsolutePosition**屬性設為代理的記錄數目。 刪除先前的記錄時，就會變更特定記錄的位置。 也沒有任何指定的資料錄將會具有相同的保證**AbsolutePosition**如果**資料錄集**物件是重新查詢，或重新開啟。 書籤的建議方式是的保留，並傳回指定的位置和是唯一的方法，在所有類型的定位**資料錄集**物件。
