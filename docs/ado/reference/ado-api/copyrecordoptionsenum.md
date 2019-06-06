---
title: CopyRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a944d3f82940d9364312fb8033ec8b8937b0c49c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695770"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
指定的行為[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|指出*來源*提供者會嘗試模擬使用下載的複本，並上傳作業，如果此方法失敗，因為*目的地*位在不同的伺服器上，或都由不同服務以外的提供者*來源*。 請注意不同的提供者功能可能會拖累效能，或遺失的資料。|  
|**adCopyNonRecursive**|2|將目前的目錄，但不包括其子目錄，複製到目的地。 複製作業不是遞迴的。|  
|**adCopyOverWrite**|1|如果覆寫的檔案或目錄*目的地*指向現有的檔案或目錄。|  
|**adCopyUnspecified**|-1|預設值。 會執行預設的複製作業：如果目的地檔案或目錄已經存在，則作業會失敗並操作複本以遞迴方式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [CopyRecord 方法 (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
