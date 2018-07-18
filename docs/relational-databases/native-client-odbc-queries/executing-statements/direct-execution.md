---
title: 直接執行 |Microsoft Docs
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
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bf81d3e9994cb755615593861d30d428ffb4727f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427267"
---
# <a name="direct-execution"></a>直接執行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  直接執行是執行陳述式的一種最基本的方式。 應用程式會建立一個字元字串，其中包含[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式並將它提交為執行使用**SQLExecDirect**函式。 當此陳述式到達伺服器時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將它編譯成執行計畫，然後立即執行此執行計畫。  
  
 直接執行通常是由執行階段建立及執行陳述式的應用程式所使用，而且對於將要單次執行的陳述式也是最有效率的方法。 但是它在許多資料庫中有一個缺點，就是每當執行此 SQL 陳述式時，都必須要剖析及編譯它，這樣會在該陳述式執行多次時增加負擔。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會大幅改善在多使用者環境中經常執行之陳述式的直接執行效能，而且針對經常執行的 SQL 陳述式搭配參數標記使用 SQLExecDirect 可以讓已備妥的執行提高效率。  
  
 當連接到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，則[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會使用[sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)傳輸的 SQL 陳述式或批次中指定**SQLExecDirect**。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具有邏輯可快速判斷如果 SQL 陳述式或批次執行**sp_executesql**比對陳述式或批次產生執行計畫已存在於記憶體中。 如果兩者相符，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 只會重複使用現有的計畫，而不是編譯新的計畫。 這表示，經常執行的執行的 SQL 陳述式**SQLExecDirect**在系統中與多位使用者將受益於許多計劃重複使用率優點之前只提供給舊版中的預存程序，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 只有當幾位使用者正在執行相同的 SQL 陳述式或批次時，重複使用執行計畫的這項好處才有效。 請遵循編碼慣例來增加不同用戶端執行的 SQL 陳述式非常類似於能夠重複使用執行計畫的機率：  
  
-   請勿在 SQL 陳述式中包含資料常數，而是要改用繫結至程式變數的參數標記。 如需詳細資訊，請參閱 <<c0> [ 使用陳述式參數](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)。  
  
-   使用完整的物件名稱。 如果物件名稱不是完整的，就不會重複使用執行計畫。  
  
-   盡量讓應用程式連接使用一組常用的連接和陳述式選項。 使用一組選項 (如 ANSI_NULLS) 為連接產生的執行計畫將不會重複用於具有另一組選項的連接。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者都會針對這些選項使用相同的預設值。  
  
 如果所有的陳述式執行**SQLExecDirect**使用這些慣例，會自動程式化[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可以重複使用執行計畫，在有機會時。  
  
## <a name="see-also"></a>另請參閱  
 [執行陳述式&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
