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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3423d215fa4a52286509769bb2ac0b75d2283a02
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755832"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定在從[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件儲存時，是否要建立或覆寫檔案。 值可以是**adSaveCreateNotExist**或**adSaveCreateOverWrite**。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|預設值。 如果*FileName*參數所指定的檔案不存在，就會建立新的檔案。|  
|**adSaveCreateOverWrite**|2|如果*Filename*參數所指定的檔案已經存在，則會使用目前開啟的**資料流程**物件中的資料來覆寫檔案。 如果*Filename*參數所指定的檔案不存在，就會建立新的檔案。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
