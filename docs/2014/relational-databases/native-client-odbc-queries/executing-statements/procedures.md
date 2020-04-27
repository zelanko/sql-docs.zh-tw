---
title: 程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: d030d4fb12ce9217bbdb88f501a0b0674c5a5828
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68206756"
---
# <a name="procedures"></a>程序
  預存程序是包含一個或多個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式的先行編譯可執行物件。 預存程序可以有輸入和輸出參數，也可以輸出整數傳回碼。 應用程式可以使用目錄函數來列舉可用的預存程序。  
  
 目標為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC 應用程式僅能使用直接執行來呼叫預存程序。 當連接到舊版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會藉由建立暫存預存程序來執行[SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360)函式，然後在**SQLExecute**上呼叫它。 它會增加額外負荷，讓**SQLPrepare**建立只呼叫目標預存程式的暫存預存程序，而不是直接執行目標預存程式。 即使在連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時，跨網路準備呼叫都需要額外的往返，而且需要建立只呼叫預存程序執行計畫的執行計畫。  
  
 執行預存程序時，ODBC 應用程式應該會使用 ODBC CALL 語法。 使用 ODBC CALL 語法時，系統會最佳化驅動程式，使用遠端程序呼叫機制來呼叫程序。 這比將 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 陳述式傳送到伺服器所使用的機制更有效率。  
  
 如需詳細資訊，請參閱執行[預存程式](../../native-client-odbc-stored-procedures/running-stored-procedures.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行語句](executing-statements-odbc.md)  
  
  
