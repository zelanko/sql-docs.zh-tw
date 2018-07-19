---
title: SeekEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f61e71b03a05a8e13c1b069e4880f362ff0985a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281587"
---
# <a name="seekenum"></a>SeekEnum
指定的型別[搜尋](../../../ado/reference/ado-api/seek-method.md)來執行。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|@shouldalert|搜尋第一個索引鍵等於*Parentkeyvalue*。|  
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
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
