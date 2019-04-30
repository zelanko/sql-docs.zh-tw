---
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aaf396e8969d490933e26652e18c0c070e030785
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63060963"
---
# <a name="resyncenum"></a>ResyncEnum
指定基礎值會覆寫呼叫[Resync](../../../ado/reference/ado-api/resync-method.md)。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|預設值。 會覆寫資料，並取消擱置中的更新。|  
|**adResyncUnderlyingValues**|1|不會不會覆寫資料，並不會取消暫止的更新。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>適用於  
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
