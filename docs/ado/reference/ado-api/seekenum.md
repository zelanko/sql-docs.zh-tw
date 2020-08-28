---
description: SeekEnum
title: SeekEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: rothja
ms.author: jroth
ms.openlocfilehash: 345e6dff5c2bc372f06eb386a4546a61b9e5a1bb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989149"
---
# <a name="seekenum"></a>SeekEnum
指定要執行的 [搜尋](./seek-method.md) 類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|搜尋第一個等於 *KeyValues*的索引鍵。|  
|**adSeekLastEQ**|2|搜尋等於 *KeyValues*的最後一個索引鍵。|  
|**adSeekAfterEQ**|4|搜尋等於 *KeyValues* 的索引鍵，或在相符的位置發生之後。|  
|**adSeekAfter**|8|在出現與 *KeyValues* 相符的位置之後搜尋索引鍵。|  
|**adSeekBeforeEQ**|16|搜尋等於 *KeyValues*的索引鍵，或只在發生相符的位置之前。|  
|**adSeekBefore**|32|在出現與 *KeyValues* 相符的位置之前搜尋索引鍵。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>套用至  
 [Seek 方法](./seek-method.md)