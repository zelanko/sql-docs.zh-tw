---
title: getAsciiStream 方法 (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ff1d47e4-572a-4169-a631-ac261f7642b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22177442dcec9fb873d4a824b73845ce6fc9bfdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954123"
---
# <a name="getasciistream-method-sqlservernclob"></a>getAsciiStream 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將這個 **NClob** 物件所指定的 **NCLOB** 值擷取為 ASCII 資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>傳回值  
 包含 NCLOB 資料的 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getAsciiStream 方法是由 java.sql.SQLServerNClob 介面中的 getAsciiStream 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
