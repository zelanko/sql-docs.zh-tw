---
description: toString 方法 (DateTimeOffset)
title: toString 方法 (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 66931c3ada32b112de920aab3ac62fdb50fd40cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431430"
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **DateTimeOffset** 物件的字串表示。  
  
## <a name="syntax"></a>語法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>傳回值  
 **DateTimeOffset** 物件的字串表示。  
  
## <a name="remarks"></a>備註  
 字串格式為 `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm`。  
  
 產生之字串的小數秒會以零填補到宣告的有效位數。 例如，值為 "2010-03-10 12:34:56.78 -08:00" 的 **datetimeoffset(6)**，將由 DateTimeOffset.toString 設定格式為 "2010-03-10 12:34:56.780000 -08:00"。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
