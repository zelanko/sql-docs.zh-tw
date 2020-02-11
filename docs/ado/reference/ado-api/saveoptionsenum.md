---
title: SaveOptionsEnum |Microsoft Docs
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
ms.openlocfilehash: 807a8d7e5757a2caf76f100a1ae51c4a8a3f4e98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931142"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定在從[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件儲存時，是否要建立或覆寫檔案。 值可以是**adSaveCreateNotExist**或**adSaveCreateOverWrite**。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|預設。 如果*FileName*參數所指定的檔案不存在，就會建立新的檔案。|  
|**adSaveCreateOverWrite**|2|如果*Filename*參數所指定的檔案已經存在，則會使用目前開啟的**資料流程**物件中的資料來覆寫檔案。 如果*Filename*參數所指定的檔案不存在，就會建立新的檔案。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
