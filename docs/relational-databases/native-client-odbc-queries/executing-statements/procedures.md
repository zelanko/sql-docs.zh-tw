---
title: 程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 751d434619c6699847490a7688491ec36ed9e875
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069998"
---
# <a name="procedures"></a>程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  預存程序是包含一個或多個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的先行編譯可執行物件。 預存程序可以有輸入和輸出參數，也可以輸出整數傳回碼。 應用程式可以使用目錄函數來列舉可用的預存程序。  
  
 目標為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC 應用程式僅能使用直接執行來呼叫預存程序。 當連接到舊版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，則[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會實作[SQLPrepare 函數](http://go.microsoft.com/fwlink/?LinkId=59360)建立暫存預存程序，然後呼叫它在**SQLExecute**. 它會新增到有額外負荷**SQLPrepare**建立暫存預存程序，僅呼叫目標預存程序與直接執行目標預存程序。 即使在連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時，跨網路準備呼叫都需要額外的往返，而且需要建立只呼叫預存程序執行計畫的執行計畫。  
  
 執行預存程序時，ODBC 應用程式應該會使用 ODBC CALL 語法。 使用 ODBC CALL 語法時，系統會最佳化驅動程式，使用遠端程序呼叫機制來呼叫程序。 這比將 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 陳述式傳送到伺服器所使用的機制更有效率。  
  
 如需詳細資訊，請參閱 <<c0> [ 執行預存程序](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)。  
  
## <a name="see-also"></a>另請參閱  
 [執行陳述式&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
