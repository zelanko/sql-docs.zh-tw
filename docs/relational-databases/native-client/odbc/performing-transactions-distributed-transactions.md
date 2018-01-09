---
title: "執行分散式的交易 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95d087ba5c51409bd46c7a9f74fdc94e69f19567
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="performing-transactions---distributed-transactions"></a>執行交易為分散式交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Microsoft 分散式交易協調器 (MS DTC) 可讓應用程式在兩個或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之間擴充交易。 也可讓應用程式參與交易管理員所管理且符合 Open Group DTP XA 標準的交易。  
  
 一般來說，所有交易管理命令都是透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式傳送到伺服器。 應用程式啟動交易，藉由呼叫[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)自動認可模式關閉。 接著，應用程式執行交易，並呼叫所組成的更新[SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) SQL_COMMIT 或 SQL_ROLLBACK 選項。  
  
 當使用 MS DTC，不過，MS DTC 會變成交易管理員和應用程式不會再使用**SQLEndTran**。  
  
 當編列在分散式交易內，然後編列在第二個分散式交易內時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會從原始分散式交易脫離，並編列在新的交易中。 如需詳細資訊，請參閱[DTC 程式設計人員參考](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)。  
  
## <a name="see-also"></a>請參閱  
 [執行的交易 &#40; ODBC &#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
