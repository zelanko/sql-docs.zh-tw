---
title: 關閉物件不在使用時 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88292579bb8e77fac42a48a6961dedd6a67e4921
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="closing-objects-when-not-in-use"></a>不使用時關閉物件
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您使用的物件[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，尤其是[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)或其中一個陳述式的物件，例如[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)或[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)，您應該在不再需要時使用其關閉的方法，明確地關閉它們。 這樣可以盡快釋放驅動程式與伺服器資源，而不必等待 Java Virtual Machine 記憶體回收行程為您執行，藉以改善效能。  
  
 當您使用捲動鎖定時，關閉物件對於在伺服器上維持良好的並行特別重要。 在關閉結果集之前，會保留最後存取之提取緩衝區中的捲動鎖定。 同樣地，在關閉陳述式之前，會保留準備控制代碼的陳述式。 如果您要針對多個陳述式重複使用連接，在您讓這些陳述式離開範圍前關閉它們將會讓伺服器提早清除準備的控制代碼。  
  
## <a name="see-also"></a>另請參閱  
 [善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
