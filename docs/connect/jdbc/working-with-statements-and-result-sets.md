---
title: 使用陳述式及結果集 |Microsoft 文件
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
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8da0153ec1058be2a548fbdb01ade0bd09715127
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-statements-and-result-sets"></a>使用陳述式及結果集
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]和陳述式，而且結果集物件，它提供，您可以使用來改善效能和可靠性的應用程式的幾項技術。  
  
## <a name="use-the-appropriate-statement-object"></a>使用適當的陳述式物件  
 當您使用其中一個 JDBC 驅動程式陳述式物件，例如[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，或[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件，請確定您對工作使用適當的物件。  
  
-   如果您沒有 OUT 參數，您不需要使用 SQLServerCallableStatement 物件。 相反地，使用 SQLServerStatement 或 SQLServerPreparedStatement 物件。  
  
-   如果您不想執行陳述式一次以上，或者沒有 IN 或 OUT 參數，您不需要使用 SQLServerCallableStatement 或 SQLServerPreparedStatement 物件。 相反地，使用 SQLServerStatement 物件。  
  
## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>對 ResultSet 物件使用適當的並行  
 除非您真的想要更新結果，否則當建立會產生結果集的陳述式時，請不要要求可更新的並行。 預設的順向、唯讀資料指標模型是讀取小型結果集的最快模型。  
  
## <a name="limit-the-size-of-your-result-sets"></a>限制結果集的大小  
 請考慮使用[setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)方法 （或 SET ROWCOUNT 或 SELECT TOP N SQL 語法） 的資料列數目限制可能的大型結果集傳回的。 如果您必須處理大型結果集，請考慮設定連接字串屬性 responseBuffering=adaptive (預設模式)，藉此使用適應性回應緩衝。 這種方法會允許應用程式處理大型結果集，而不需要伺服器端資料指標，而且會將應用程式的記憶體使用量降到最低。 如需詳細資訊，請參閱[使用適應性緩衝](../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="use-the-appropriate-fetch-size"></a>使用適當的提取大小  
 若是唯讀的伺服器資料指標，就要在往返於伺服器與驅動程式中使用的記憶體數量之間作取捨。 若是可更新的伺服器資料指標，提取大小也會影響結果集對變更的敏感性以及伺服器上的並行。 目前的提取緩衝區內的資料列更新才會顯示明確[refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)發出方法或直到資料指標離開提取緩衝區。 大型提取緩衝區將具有更好的效能 (更少的伺服器往返)，但是對變更的敏感性較低，並會減少伺服器上的並行 (如果使用 CONCUR_SS_SCROLL_LOCKS (1009))。 如需最大的變更敏感性，請使用提取大小 1。 然而，請注意這將會導致每一個提取的資料列都要往返於伺服器。  
  
## <a name="use-streams-for-large-in-parameters"></a>對大型 IN 參數使用資料流  
 使用資料流或以遞增方式具體化的 BLOB 和 CLOB，處理更新大型資料行值或傳送大型 IN 參數。 JDBC 驅動程式會多次往返將這些項目「大量」送至伺服器，容許您設定及更新的值大於記憶體可包含的值。  
  
## <a name="see-also"></a>另請參閱  
 [善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
