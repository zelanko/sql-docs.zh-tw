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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 886825b4d32354572a5162487add419b00ec35d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931061"
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
