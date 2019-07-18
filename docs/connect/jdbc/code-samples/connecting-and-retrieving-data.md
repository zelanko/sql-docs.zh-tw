---
title: 連接及擷取資料 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c87089b59855ef2c68a9e3b1051ed39850d7b17e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770066"
---
# <a name="connecting-and-retrieving-data"></a>連接及擷取資料

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

當使用 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 時，有兩種主要方法，可用於建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的連線。 第一種方法就是在連線 URL 中設定連線屬性，然後呼叫 DriverManager 類別的 getConnection 方法，以傳回 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。  
  
> [!NOTE]  
> 如需 JDBC 驅動程式支援的連接屬性的清單，請參閱 <<c0> [ 設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
第二種方法牽涉到設定連線屬性，方法是使用[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別的 setter 方法，然後呼叫 [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 方法，以傳回 SQLServerConnection 物件。  
  
本節的主題說明您可以連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的不同方法，而且它們也示範了擷取資料的不同技術。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[連接 URL 範例](../../../connect/jdbc/code-samples/connection-url-sample.md)|說明如何使用連線 URL 來連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，然後使用 SQL 陳述式來擷取資料。|  
|[資料來源範例](../../../connect/jdbc/code-samples/data-source-sample.md)|說明如何使用資料來源來連接到 SQL Server，然後使用預存程序來擷取資料。|  
  
## <a name="see-also"></a>另請參閱

[範例 JDBC 驅動程式應用程式](../../jdbc/code-samples/sample-jdbc-driver-applications.md)
  
