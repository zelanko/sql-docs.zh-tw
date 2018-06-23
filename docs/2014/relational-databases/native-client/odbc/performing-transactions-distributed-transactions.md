---
title: 執行分散式的交易 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d6c03f674722e817fc8c16dd712572c3236e73d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033911"
---
# <a name="performing-distributed-transactions"></a>執行分散式交易
  Microsoft 分散式交易協調器 (MS DTC) 可讓應用程式在兩個或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之間擴充交易。 也可讓應用程式參與交易管理員所管理且符合 Open Group DTP XA 標準的交易。  
  
 一般來說，所有交易管理命令都是透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式傳送到伺服器。 應用程式啟動交易，藉由呼叫[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)自動認可模式關閉。 接著，應用程式執行交易，並呼叫所組成的更新[SQLEndTran](../../native-client-odbc-api/sqlendtran.md) SQL_COMMIT 或 SQL_ROLLBACK 選項。  
  
 當使用 MS DTC，不過，MS DTC 會變成交易管理員和應用程式不會再使用**SQLEndTran**。  
  
 當編列在分散式交易內，然後編列在第二個分散式交易內時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會從原始分散式交易脫離，並編列在新的交易中。 如需詳細資訊，請參閱[DTC 程式設計人員參考](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)。  
  
## <a name="see-also"></a>另請參閱  
 [執行交易&#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  