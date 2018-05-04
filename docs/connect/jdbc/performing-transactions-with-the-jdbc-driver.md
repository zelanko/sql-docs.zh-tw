---
title: 使用 JDBC 驅動程式執行異動 |Microsoft 文件
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
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cecc83cced06fcc53fcddaa365e5c04fedbf469
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>以 JDBC 驅動程式執行交易
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  必須確保其永續性資料一致的所有應用程式，交易處理都會是一項強制需求。 與[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，交易處理可以在本機執行或分散式。 交易的執行為不可部分完成、一致、隔離和持久 (ACID) 的模組。  
  
 本節的主題說明 JDBC 驅動程式支援交易的方式，包括隔離等級、交易儲存點和結果集保留性。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[了解交易](../../connect/jdbc/understanding-transactions.md)|提供交易如何與 JDBC 驅動程式搭配使用的概觀。|  
|[了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)|提供 XA 交易如何與 JDBC 驅動程式搭配使用的概觀。|  
|[了解隔離等級](../../connect/jdbc/understanding-isolation-levels.md)|描述 JDBC 驅動程式支援的各種隔離等級。|  
|[使用儲存點](../../connect/jdbc/using-savepoints.md)|描述如何使用 JDBC 驅動程式搭配交易儲存點。|  
|[使用保留性](../../connect/jdbc/using-holdability.md)|描述如何使用 JDBC 驅動程式搭配結果集保留性。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
