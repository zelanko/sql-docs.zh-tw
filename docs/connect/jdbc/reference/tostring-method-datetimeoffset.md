---
title: toString 方法 (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef3cd31068c324475e8edfe8bf8f7c16acc4a2de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968519"
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回**DateTimeOffset**物件的字串表示。  
  
## <a name="syntax"></a>語法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>傳回值  
 **DateTimeOffset**物件的字串表示。  
  
## <a name="remarks"></a>Remarks  
 字串的格式為*YYYY* - *MM* - *DD * * hh*:*MM*:*ss*[。*fffffff*] [+ |-]*hh*:*mm*。  
  
 產生之字串的小數秒會以零填補到宣告的有效位數。 例如, 值為 "2010-03-10 12:34: 56.78-08:00" 的**datetimeoffset (6)** 將由 datetimeoffset 格式設定為 "2010-03-10 12:34: 56.780000-08:00"。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
