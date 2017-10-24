---
title: "SeekEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 051f4e1c300796e2777e9b06a1514c9ce00b9b02
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="seekenum"></a>SeekEnum
指定的型別[搜尋](../../../ado/reference/ado-api/seek-method.md)來執行。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|搜尋第一個索引鍵等於*Parentkeyvalue*。|  
|**adSeekLastEQ**|2|搜尋的最後一個索引鍵等於*Parentkeyvalue*。|  
|**adSeekAfterEQ**|4|搜尋等於任一金鑰*Parentkeyvalue*或只在其中可能發生的相符項目之後。|  
|**adSeekAfter**|8|只在位置之後搜尋索引鍵相符*Parentkeyvalue*可能發生。|  
|**adSeekBeforeEQ**|16|搜尋等於任一金鑰*Parentkeyvalue*或之前其中可能發生的相符項目。|  
|**adSeekBefore**|32|之前搜尋的索引鍵，其中的相符*Parentkeyvalue*可能發生。|  
  
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
 [搜尋方法](../../../ado/reference/ado-api/seek-method.md)

