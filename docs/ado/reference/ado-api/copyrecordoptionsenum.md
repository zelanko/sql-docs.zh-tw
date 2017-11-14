---
title: "CopyRecordOptionsEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e747e5bb2bcff9a8e414d809c127df09c251afa4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
指定的行為[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|表示*來源*提供者會嘗試模擬使用下載的複本，並上傳作業，如果此方法失敗，因為*目的地*位於不同的伺服器上，或由不同的服務以外的提供者*來源*。 請注意不同提供者功能可能會影響效能或資料遺失。|  
|**adCopyNonRecursive**|2|將目前的目錄，但不會為其子目錄複製到目的地。 複製作業不是遞迴的。|  
|**adCopyOverWrite**|1|如果覆寫的檔案或目錄*目的地*指向現有的檔案或目錄。|  
|**adCopyUnspecified**|-1|預設值。 執行複製作業預設值： 如果目的地檔案或目錄已存在，此作業會失敗並操作複本以遞迴方式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [CopyRecord 方法 (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)

