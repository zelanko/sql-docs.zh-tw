---
title: "SeekEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: SeekEnum
helpviewer_keywords: SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6f60ed06b2f23bceec62822f43b77f5c10c3ce1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
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
