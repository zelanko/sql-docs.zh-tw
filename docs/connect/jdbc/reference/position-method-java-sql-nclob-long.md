---
title: position 方法 (java.sql.NClob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed9313f31d30308b448381276608e119f279ea2a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914147"
---
# <a name="position-method-javasqlnclob-long"></a>position 方法 (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定 **NClob** 物件 *searchstr* 出現在此 **NClob** 物件中的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>參數  
 *searchstr*  
  
 要搜尋的 NClob 物件。  
  
 *start*  
  
 開始搜尋的位置，第一個位置是 1。  
  
## <a name="return-value"></a>傳回值  
 子字串的出現位置，如果未出現，則為 -1。 第一個位置是 1。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 position 方法是由 java.sql.NClob 介面中的 position 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [position 方法 &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
