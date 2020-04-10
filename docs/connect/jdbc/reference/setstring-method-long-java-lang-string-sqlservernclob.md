---
title: setString 方法 (long, java.lang.String) - NClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 698073b2-3f0c-449c-ad68-48144698fe8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eae050bb80728a530accb73eb2cb22f5320e7ed9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926642"
---
# <a name="setstring-method-long-javalangstring-sqlservernclob"></a>setString 方法 (long, java.lang.String) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從指定位置開始將指定 **String** 寫入 **NCLOB**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int setString(long pos,  
              java.lang.String str)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 開始寫入至 **NCLOB** 的位置，第一個位置是 1。  
  
 *str*  
  
 要寫入至 **NCLOB** 的 String。  
  
## <a name="return-value"></a>傳回值  
 寫入的字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setString 方法是由 java.sql.NClob 介面中的 setString 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
