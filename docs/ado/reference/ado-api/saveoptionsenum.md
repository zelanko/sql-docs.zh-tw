---
description: SaveOptionsEnum
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
ms.openlocfilehash: edac11f61b003307703ec13daed8022b8af31bae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777557"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定從 [資料流程](./stream-object-ado.md) 物件儲存時是否應該建立或覆寫檔案。 值可以是 **adSaveCreateNotExist** 或 **adSaveCreateOverWrite**。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|預設值。 如果 *FileName* 參數指定的檔案不存在，則會建立新的檔案。|  
|**adSaveCreateOverWrite**|2|如果*Filename*參數指定的檔案已經存在，則會使用目前開啟之**資料流程**物件中的資料來覆寫檔案。 如果 *Filename* 參數指定的檔案不存在，則會建立新的檔案。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [SaveToFile 方法](./savetofile-method.md)