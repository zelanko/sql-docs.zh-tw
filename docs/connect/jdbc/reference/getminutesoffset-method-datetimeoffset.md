---
description: getMinutesOffset 方法 (DateTimeOffset)
title: getMinutesOffset 方法 (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a3184c0dc0389a696904386361496ea31582b0af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435410"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回此 DateTimeOffset 物件與 GMT 之間位移 (以分鐘為單位)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>傳回值  
 以分鐘為單位的位移。  
  
## <a name="remarks"></a>備註  
 若 DateTimeOffset 物件代表 8 March 2010, 11:35:48 -0800，則 getMinutesOffset 會傳回值 480。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
