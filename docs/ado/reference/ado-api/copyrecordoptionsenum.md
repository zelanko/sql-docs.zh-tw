---
description: CopyRecordOptionsEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8cb5b72579313f538ca763079787f2aba640d692
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444370"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
指定 [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) 方法的行為。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|指出如果由於*目的地*位於不同的伺服器上，或由不同于*來源*的提供者提供服務，則*來源*提供者會嘗試使用下載和上傳作業來模擬複製。 請注意，不同的提供者功能可能會妨礙效能或遺失資料。|  
|**adCopyNonRecursive**|2|將目前目錄（但不是它的任何子目錄）複製到目的地。 複製作業不是遞迴的。|  
|**adCopyOverWrite**|1|如果 *目的地* 指向現有的檔案或目錄，則覆寫檔案或目錄。|  
|**adCopyUnspecified**|-1|預設值。 執行預設複製作業：如果目的地檔案或目錄已經存在，作業就會失敗，而且作業會以遞迴方式複製。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [CopyRecord 方法 (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
