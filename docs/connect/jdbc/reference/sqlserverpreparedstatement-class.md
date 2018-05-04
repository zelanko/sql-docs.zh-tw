---
title: SQLServerPreparedStatement 類別 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c7b37e26faedf7cb064880d68e17f4688bfbe73
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 備妥之陳述式功能的基本實作。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** SQLServerStatement  
  
 **實作：** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>備註  
 SQLServerPreparedStatement 提供可讓您提供參數，例如任何原生 Java 類型及許多 Java 物件類型的方法。 SQLServerPreparedStatement 陳述式的準備使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **sp_prepare**預存程序，然後再重複使用傳回的陳述式為每個後續執行的陳述式中，通常會使用不同的處理使用者所提供的參數。  
  
 SQLServerPreparedStatement 支援批次處理，其中一組備妥的陳述式會執行單一資料庫中來回行程，以改善執行階段效能。  
  
 這個類別支援解除包裝成為 SQLServerPreparedStatement 類別、 ISQLServerPreparedStatement 介面、 java.sql.PreparedStatement 介面和類別及所 SQLServerStatement 支援解除包裝的介面。 如需詳細資訊，請參閱[包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
