---
title: "toString 方法 (DateTimeOffset) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c6dd16bfddfa331fd2647bd8fd191ac91941e71
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回的字串表示**DateTimeOffset**物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>傳回值  
 字串表示法**DateTimeOffset**物件。  
  
## <a name="remarks"></a>備註  
 字串具有格式*YYYY*-*公釐*-*DD**hh*:*公釐*:*ss*[。*fffffff*] [+ |-]*hh*:*公釐*。  
  
 產生之字串的小數秒會以零填補到宣告的有效位數。 例如， **datetimeoffset(6)**值為"2010年-03-10 12:34:56.78-08:00"將會格式化為 DateTimeOffset.toString"2010年-03-10 12:34:56.780000-08:00"。  
  
## <a name="see-also"></a>請參閱＜  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
