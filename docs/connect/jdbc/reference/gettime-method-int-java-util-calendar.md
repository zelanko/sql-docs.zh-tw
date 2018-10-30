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
manager: craigg
ms.openlocfilehash: b5c0172dd04e13775b977a93f05f2976791a2343
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611910"
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
  
 月曆物件。  
  
## <a name="return-value"></a>傳回值  
 時間物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這項 getTime 方法由 java.sql.CallableStatement 介面中的 getTime 方法指定。  
  
 圖表標題為 「 Getter 方法轉換 」 所示[了解資料類型轉換](../../../connect/jdbc/understanding-data-type-conversions.md)若要查看哪些[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可以使用此方法擷取的資料型別。  
  
## <a name="see-also"></a>另請參閱  
 [getTime 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
