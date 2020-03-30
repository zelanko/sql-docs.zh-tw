---
title: getTime 方法 (int, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 87b7fbaf-7149-494f-b3b2-16b468a8ebf1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33f5e25d45f1e08c30f3094a9200291de9510150
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979104"
---
# <a name="gettime-method-int-javautilcalendar"></a>getTime 方法 (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合使用指定的參數索引，透過使用指定 Calendar 物件，擷取指定參數的值來當作 java.sql.Time 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Time getTime(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
 *cal*  
  
 Calendar 物件。  
  
## <a name="return-value"></a>傳回值  
 Time 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這項 getTime 方法由 java.sql.CallableStatement 介面中的 getTime 方法指定。  
  
 請參閱[了解資料類型轉換](../../../connect/jdbc/understanding-data-type-conversions.md)中標題為「Getter 方法轉換」的圖表，以查看可以使用此方法擷取哪些 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [getTime 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
