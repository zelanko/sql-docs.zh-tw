---
description: 資料錄集定位
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9d5cdea25dbf14ef5f26d02612f357768acdad61
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452960"
---
# <a name="recordset-positioning"></a>資料錄集定位
您可以使用 **AbsolutePosition** 屬性，根據記錄 **集** 物件中的序數位置，移至記錄，或決定目前記錄的序數位置。 提供者必須支援適當的功能，才能使用此屬性。  
  
 當目前記錄是**記錄集**內的第一筆記錄時， **AbsolutePosition**是以1為基礎，而等於1。 如先前所述，您可以從**RecordCount**屬性取得**記錄集**物件中的總記錄數。  
  
 當您設定 **AbsolutePosition** 屬性時，即使它是目前快取中的記錄，ADO 仍會以您指定的記錄開頭的新記錄組重載快取。 **CacheSize**屬性會決定這個群組的大小。  
  
> [!NOTE]
>  您不應該使用 **AbsolutePosition** 屬性做為代理記錄號碼。 當您刪除先前的記錄時，指定記錄的位置會變更。 如果重新查詢或重新開啟**記錄集**物件，也不保證指定的記錄會有相同的**AbsolutePosition** 。 書簽是保留並返回指定位置的建議方式，而且是在所有 **記錄集** 物件類型之間唯一定位的方法。
