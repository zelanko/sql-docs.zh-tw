---
title: truncate 方法 (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b7e8210d-a724-4bae-832a-ae4c63031c9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fa3559769e06545b8e1cf69c29d389223d1d090
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80908325"
---
# <a name="truncate-method-sqlservernclob"></a>truncate 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  截斷 **NCLOB** 成為指定的長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>參數  
 *len*  
  
 以字元為單位的長度，即應該將 **NCLOB** 值截斷成的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 truncate 方法是由 java.sql.NClob 介面中的 truncate 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
