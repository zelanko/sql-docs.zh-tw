---
title: 執行分散式交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ec23fd1883749e35e67f888e26bdf031ccf7fb8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055873"
---
# <a name="performing-distributed-transactions"></a>執行分散式交易
  Microsoft 分散式交易協調器 (MS DTC) 可讓應用程式在兩個或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之間擴充交易。 也可讓應用程式參與交易管理員所管理且符合 Open Group DTP XA 標準的交易。  
  
 一般來說，所有交易管理命令都是透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式傳送到伺服器。 應用程式會藉由在關閉自動認可模式的情況下呼叫[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)來啟動交易。 應用程式接著會執行組成交易的更新，並使用 SQL_COMMIT 或 SQL_ROLLBACK 選項來呼叫[SQLEndTran](../../native-client-odbc-api/sqlendtran.md) 。  
  
 不過，在使用 MS DTC 時，MS DTC 會變成交易管理員，而應用程式不會再使用**SQLEndTran**。  
  
 當編列在分散式交易內，然後編列在第二個分散式交易內時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會從原始分散式交易脫離，並編列在新的交易中。 如需詳細資訊，請參閱 DTC 程式設計[人員參考](https://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行交易](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
