---
title: 連線及擷取資料
description: 了解如何使用 Microsoft JDBC Driver for SQL Server 和這些程式碼範例，連線到 SQL 資料庫並擷取資料。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7268688afe70d7152448ec2e3c0f18c9842582de
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632508"
---
# <a name="connecting-and-retrieving-data"></a>連線及擷取資料

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

當使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，有兩種主要方法，可用於建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的連線。 第一種方法就是在連線 URL 中設定連線屬性，然後呼叫 DriverManager 類別的 getConnection 方法，以傳回 [SQLServerConnection](reference/sqlserverconnection-class.md) 物件。  
  
> [!NOTE]  
> 如需 JDBC 驅動程式支援的連線屬性清單，請參閱[設定連線屬性](setting-the-connection-properties.md)。  
  
第二種方法牽涉到設定連線屬性，方法是使用[SQLServerDataSource](reference/sqlserverdatasource-class.md) 類別的 setter 方法，然後呼叫 [getConnection](reference/getconnection-method-sqlserverdatasource.md) 方法，以傳回 SQLServerConnection 物件。  
  
本節的主題說明您可以連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的不同方法，而且它們也示範了擷取資料的不同技術。  
  
## <a name="in-this-section"></a>本節內容  
  
| 主題                                                                | 描述                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [連接 URL 範例](connection-url-sample.md) | 說明如何使用連線 URL 來連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然後使用 SQL 陳述式來擷取資料。 |
| [資料來源範例](data-source-sample.md)       | 說明如何使用資料來源來連接到 SQL Server，然後使用預存程序來擷取資料。                                                 |
  
## <a name="see-also"></a>另請參閱

[範例 JDBC 驅動程式應用程式](sample-jdbc-driver-applications.md)  
  
