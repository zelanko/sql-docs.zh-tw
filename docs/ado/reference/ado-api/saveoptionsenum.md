---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5965b74d5d02137222f704cfcf27a0ffb95962b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定檔案是否要建立或覆寫時從儲存[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。 值可以是**adSaveCreateNotExist**或**adSaveCreateOverWrite**...  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|預設值。 如果指定的檔案建立新檔案*FileName*參數不存在。|  
|**adSaveCreateOverWrite**|2|目前開啟的資料覆寫檔案**資料流**物件，如果所指定的檔案*Filename*參數已經存在。 如果指定的檔案*Filename*參數不存在，會建立新的檔案。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
