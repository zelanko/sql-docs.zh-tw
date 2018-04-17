---
title: 直接執行 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7ff1baa498a99f9e9279d1c104df179fa34cbea3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="direct-execution"></a>直接執行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  直接執行是執行陳述式的一種最基本的方式。 應用程式會建立一個字元字串，其中包含[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式並將它提交執行使用**SQLExecDirect**函式。 當此陳述式到達伺服器時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將它編譯成執行計畫，然後立即執行此執行計畫。  
  
 直接執行通常是由執行階段建立及執行陳述式的應用程式所使用，而且對於將要單次執行的陳述式也是最有效率的方法。 但是它在許多資料庫中有一個缺點，就是每當執行此 SQL 陳述式時，都必須要剖析及編譯它，這樣會在該陳述式執行多次時增加負擔。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會大幅改善在多使用者環境中經常執行之陳述式的直接執行效能，而且針對經常執行的 SQL 陳述式搭配參數標記使用 SQLExecDirect 可以讓已備妥的執行提高效率。  
  
 當連接到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會使用[sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)傳輸 SQL 陳述式或批次上指定**SQLExecDirect**。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具有邏輯，可快速判斷 SQL 陳述式或批次執行**sp_executesql**符合陳述式或批次產生執行計畫已經存在記憶體中。 如果兩者相符，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 只會重複使用現有的計畫，而不是編譯新的計畫。 經常執行的 SQL 陳述式執行，但這表示**SQLExecDirect**在系統中與多位使用者將受益於許多計畫重複使用這些優點之前只可在舊版的預存程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 只有當幾位使用者正在執行相同的 SQL 陳述式或批次時，重複使用執行計畫的這項好處才有效。 請遵循編碼慣例來增加不同用戶端執行的 SQL 陳述式非常類似於能夠重複使用執行計畫的機率：  
  
-   請勿在 SQL 陳述式中包含資料常數，而是要改用繫結至程式變數的參數標記。 如需詳細資訊，請參閱[使用陳述式參數](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)。  
  
-   使用完整的物件名稱。 如果物件名稱不是完整的，就不會重複使用執行計畫。  
  
-   盡量讓應用程式連接使用一組常用的連接和陳述式選項。 使用一組選項 (如 ANSI_NULLS) 為連接產生的執行計畫將不會重複用於具有另一組選項的連接。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者都會針對這些選項使用相同的預設值。  
  
 如果使用的所有陳述式執行**SQLExecDirect**使用這些慣例，會自動程式化[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在有機會時可以重複使用執行計畫。  
  
## <a name="see-also"></a>另請參閱  
 [執行陳述式 & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
