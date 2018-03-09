---
title: "資料錄集定位 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c5b7e11012d4efc94bf4924a6390b1cfbd68195
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="recordset-positioning"></a>定位資料錄集
使用**AbsolutePosition**屬性移至資料，根據其序數位置中**資料錄集**物件，或要判定目前記錄的序數位置。 提供者必須支援這個屬性才能使用適當的功能。  
  
 **AbsolutePosition**是以 1 為基礎，並且等於 1，目前的記錄時的第一個記錄**資料錄集**。 如先前所述，您可以取得中的記錄總數**資料錄集**物件從**RecordCount**屬性。  
  
 當您將**AbsolutePosition**屬性，即使它是目前的快取中的記錄 ADO 重新載入快取以一組新的記錄從您指定的記錄。 **CacheSize**屬性會決定此群組的大小。  
  
> [!NOTE]
>  您不應該使用**AbsolutePosition**屬性設為代理的記錄數目。 刪除先前的記錄時，就會變更特定記錄的位置。 也沒有任何指定的資料錄將會具有相同的保證**AbsolutePosition**如果**資料錄集**物件是重新查詢，或重新開啟。 書籤的建議方式是的保留，並傳回指定的位置和是唯一的方法，在所有類型的定位**資料錄集**物件。
