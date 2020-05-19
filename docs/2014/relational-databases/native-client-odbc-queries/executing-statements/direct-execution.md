---
title: 直接執行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: de740430601e3b596a1d4d9717a8e23ef1e528cf
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82710388"
---
# <a name="direct-execution"></a>直接執行
  直接執行是執行陳述式的一種最基本的方式。 應用程式會建立包含語句的字元字串 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ，並使用**SQLExecDirect**函數提交它以供執行。 當此陳述式到達伺服器時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將它編譯成執行計畫，然後立即執行此執行計畫。  
  
 直接執行通常是由執行階段建立及執行陳述式的應用程式所使用，而且對於將要單次執行的陳述式也是最有效率的方法。 但是它在許多資料庫中有一個缺點，就是每當執行此 SQL 陳述式時，都必須要剖析及編譯它，這樣會在該陳述式執行多次時增加負擔。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會大幅改善在多使用者環境中經常執行之陳述式的直接執行效能，而且針對經常執行的 SQL 陳述式搭配參數標記使用 SQLExecDirect 可以讓已備妥的執行提高效率。  
  
 當連接到的實例時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會使用[sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql)來傳輸在**SQLExecDirect**上指定的 SQL 語句或批次。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]具有邏輯，可以快速判斷以**sp_executesql**執行的 SQL 語句或批次是否符合產生已存在於記憶體中之執行計畫的語句或批次。 如果兩者相符，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 只會重複使用現有的計畫，而不是編譯新的計畫。 這表示，在具有許多使用者的系統中，使用**SQLExecDirect**執行的常用 SQL 語句，將受益于舊版中的預存程式所提供的許多方案重複使用優勢 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 只有當幾位使用者正在執行相同的 SQL 陳述式或批次時，重複使用執行計畫的這項好處才有效。 請遵循編碼慣例來增加不同用戶端執行的 SQL 陳述式非常類似於能夠重複使用執行計畫的機率：  
  
-   請勿在 SQL 陳述式中包含資料常數，而是要改用繫結至程式變數的參數標記。 如需詳細資訊，請參閱[Using 語句參數](../using-statement-parameters.md)。  
  
-   使用完整的物件名稱。 如果物件名稱不是完整的，就不會重複使用執行計畫。  
  
-   盡量讓應用程式連接使用一組常用的連接和陳述式選項。 使用一組選項 (如 ANSI_NULLS) 為連接產生的執行計畫將不會重複用於具有另一組選項的連接。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者都會針對這些選項使用相同的預設值。  
  
 如果所有使用**SQLExecDirect**執行的語句都是使用這些慣例來編碼， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就可以在發生商機時重複使用執行計畫。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行語句](executing-statements-odbc.md)  
  
  
