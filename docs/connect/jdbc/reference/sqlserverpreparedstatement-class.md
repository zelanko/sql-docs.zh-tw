---
title: SQLServerPreparedStatement 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7112a20f7811a0796396045c50b1b243ed0c3802
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796949"
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 備妥之陳述式功能的基本實作。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** SQLServerStatement  
  
 **實作：** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerPreparedStatement 提供的方法可讓您提供參數，作為任何原生 Java 類型及許多 Java 物件類型。 SQLServerPreparedStatement 會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sp_prepare** 預存程序來準備陳述式，然後在後續每一次執行該陳述式時重複使用傳回的陳述式控制代碼，通常會使用該使用者提供的不同參數。  
  
 SQLServerPreparedStatement 支援批次處理，也就是一組備妥的陳述式會在單一資料庫來回行程中執行，以改善執行階段效能。  
  
 此類別支援解除包裝成為 SQLServerPreparedStatement 類別、 ISQLServerPreparedStatement 介面、 java.sql.PreparedStatement 介面和類別及解除包裝成為 SQLServerStatement 所支援的介面。 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
