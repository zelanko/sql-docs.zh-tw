---
title: 記錄集定位 |Microsoft Docs
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
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924436"
---
# <a name="recordset-positioning"></a>資料錄集定位
您可以使用**AbsolutePosition**屬性，根據記錄**集**物件中的序數位置，或判斷目前記錄的序數位置，來移至記錄。 提供者必須支援適當的功能，才能使用此屬性。  
  
 **AbsolutePosition**是以1為基礎，而當目前記錄是記錄**集**內的第一筆記錄時，等於1。 如先前所述，您可以從**RecordCount**屬性取得記錄**集**物件中的記錄總數。  
  
 當您設定**AbsolutePosition**屬性時，即使它是目前快取中的記錄，ADO 還是會以您指定的記錄開頭的一組新記錄來重載快取。 **CacheSize**屬性會決定此群組的大小。  
  
> [!NOTE]
>  您不應該使用**AbsolutePosition**屬性做為代理記錄號碼。 當您刪除先前的記錄時，指定記錄的位置會變更。 如果重新查詢或重新開啟**記錄集**物件，也不保證給定的記錄會有相同的**AbsolutePosition** 。 書簽是保留並返回指定位置的建議方式，而且是在所有類型的**記錄集**物件上定位的唯一方法。
