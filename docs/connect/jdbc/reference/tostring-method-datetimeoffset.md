---
title: "toString 方法 (DateTimeOffset) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b0c31538c7260b81a88822099f56a05b70a0a96
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

