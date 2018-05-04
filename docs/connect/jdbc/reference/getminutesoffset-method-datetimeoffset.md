---
title: getMinutesOffset 方法 (DateTimeOffset) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6c768d1be182091db5306100c0b6ec239c4adc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  會傳回位移，以分鐘為單位從 GMT 這個 DateTimeOffset 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>傳回值  
 以分鐘為單位的位移。  
  
## <a name="remarks"></a>備註  
 DateTimeOffset 物件，表示 8 2010 年 3 月 11:35:48-0800，getMinutesOffset 傳回 480 這個值。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
