---
title: SeekEnum | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a6e044c4a2cda01fcc9cbba2667beaae75a12caf
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63459340"
---
# <a name="seekenum"></a>SeekEnum
指定的型別[搜尋](../../../ado/reference/ado-api/seek-method.md)來執行。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|搜尋的第一個索引鍵相等*Parentkeyvalue*。|  
|**adSeekLastEQ**|2|搜尋等於最後一個索引鍵*Parentkeyvalue*。|  
|**adSeekAfterEQ**|4|搜尋可能索引鍵相等*Parentkeyvalue*或後方會有發生該相符項目。|  
|**adSeekAfter**|8|後方的位置搜尋索引鍵相符*Parentkeyvalue*時可能發生。|  
|**adSeekBeforeEQ**|16|搜尋可能索引鍵相等*Parentkeyvalue*或之前其中時可能發生的相符項目。|  
|**adSeekBefore**|32|之前搜尋的索引鍵，其中相符*Parentkeyvalue*時可能發生。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>適用於  
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
