---
description: 跳至記錄
title: 跳至 a 記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: rothja
ms.author: jroth
ms.openlocfilehash: 96987a5c51d7a888672609aa28f3fd223ccfffa1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980399"
---
# <a name="jumping-to-a-record"></a>跳至記錄
[Move](../../reference/ado-api/move-method-ado.md)方法可讓您使用下列語法，在**記錄集中**向前或向後移動指定的記錄數目：  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>備註  
 所有**記錄集**物件都支援**Move**方法。  
  
 如果 *NumRecords* 引數大於零，則目前的記錄位置會向 (向前移動到 **記錄集**) 的結尾。 如果 *NumRecords* 小於零，則目前的記錄位置會向後 (朝 **記錄集** 的開頭) 。  
  
 如果 **移動** 呼叫會將目前的記錄位置移至第一筆記錄之前的某個點，則 ADO 會將目前的記錄設定為 **記錄集** 內的第一筆記錄之前的位置， (**BOF** 為 **True**) 。 當 **BOF** 屬性已 **為 True** 時，嘗試向後移動會產生錯誤。  
  
 如果 **移動** 呼叫會將目前的記錄位置移至最後一筆記錄之後的某個點，則 ADO 會將目前的記錄設定為 **記錄集** 內最後一筆記錄之後的位置， (**EOF** 是 **True**) 。 當 **EOF** 屬性已 **成立** 時，嘗試向前移動會產生錯誤。  
  
 從空的**記錄集**物件呼叫**Move**方法會產生錯誤。  
  
 如果您在 *Start* 引數中傳遞書簽，則如果 **記錄集** 物件支援書簽，移動就會相對於含有此書簽的記錄。 書簽是使用 [bookmark](../../reference/ado-api/bookmark-property-ado.md) 屬性取得的。 如果未指定，則移動會相對於目前的記錄。  
  
 如果您使用 **CacheSize** 屬性從提供者本機快取記錄，則傳遞可將目前記錄位置移至目前快取記錄群組之外的 *NumRecords* 引數，會強制 ADO 從目的地記錄開始取得新的記錄群組。 **CacheSize**屬性會決定新抓取群組的大小，而目的地記錄是第一個抓取的記錄。