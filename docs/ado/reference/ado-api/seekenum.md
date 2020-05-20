---
title: SeekEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: dca33c975b3d25347b0cb9bb804b852ec5f93d7d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765389"
---
# <a name="seekenum"></a>SeekEnum
指定要執行的[搜尋](../../../ado/reference/ado-api/seek-method.md)類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|搜尋等於*配置*的第一個索引鍵。|  
|**adSeekLastEQ**|2|搜尋等於*配置*的最後一個索引鍵。|  
|**adSeekAfterEQ**|4|搜尋等於*配置*的索引鍵，或在發生相符的位置之後。|  
|**adSeekAfter**|8|在出現與*配置*相符的位置之後搜尋索引鍵。|  
|**adSeekBeforeEQ**|16|搜尋等於*配置*的索引鍵，或只在發生相符的位置之前。|  
|**adSeekBefore**|32|在出現與*配置*相符的位置之前，搜尋索引鍵。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>套用至  
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
