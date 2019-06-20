---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 537c5bfa6e1da125b562d4cc26820a2fcb5618fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711373"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定檔案是否要建立或覆寫時從儲存[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。 值可以是**adSaveCreateNotExist**或是**adSaveCreateOverWrite**...  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|預設值。 如果指定的檔案建立新的檔案*FileName*參數不存在。|  
|**adSaveCreateOverWrite**|2|使用來自目前開啟的資料覆寫檔案**Stream**物件，如果指定的檔案*Filename*參數已經存在。 如果指定的檔案*Filename*參數不存在，來建立新的檔案。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
