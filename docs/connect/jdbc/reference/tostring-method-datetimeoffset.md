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
manager: jroth
ms.openlocfilehash: 64186b6add766a21e0881fb6b3f59d49048334e8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778588"
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回的字串表示法**DateTimeOffset**物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>傳回值  
 字串表示法**DateTimeOffset**物件。  
  
## <a name="remarks"></a>Remarks  
 字串具有格式*YYYY*-*MM*-*DD * * hh*:*mm*:*的*[.*fffffff*] [+ |-]*hh*:*mm*。  
  
 產生之字串的小數秒會以零填補到宣告的有效位數。 比方說， **datetimeoffset(6)** 值是 「 2010年-03-10 12:34:56.78-08:00"將會格式化為 DateTimeOffset.toString"2010年-03-10 12:34:56.780000-08:00"。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
