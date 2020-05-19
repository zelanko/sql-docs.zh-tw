---
title: 執行查詢（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 597d138832ab5234d0059c25e91fd4d830be255c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82711084"
---
# <a name="executing-queries-odbc"></a>執行查詢 (ODBC)
  當 ODBC 應用程式將連接控制代碼初始化並連接資料來源後，會在連接控制代碼上配置一個或多個陳述式控制代碼。 然後，應用程式可以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在語句控制碼上執行語句。 執行 SQL 陳述式的一般事件序列是：  
  
1.  設定任何需要的陳述式屬性。  
  
2.  建構陳述式。  
  
3.  執行陳述式。  
  
4.  擷取任何結果集。  
  
 當應用程式擷取在 (由 SQL 陳述式傳回的) 所有結果集的資料列後，可以在相同陳述式控制代碼上執行另一個查詢。 如果應用程式判斷不需要取得特定結果集中的所有資料列，它可以藉由呼叫[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md)或[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)來取消其餘的結果集。  
  
 在 ODBC 應用程式中，如果您必須用不同資料多次執行相同的 SQL 陳述式，則在 SQL 陳述式的建構中使用由問號 (?) 所代表的參數標記：  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 然後，每個參數標記都可以藉由呼叫[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)來系結至程式變數。  
  
 在執行所有 SQL 陳述式，而且也處理其結果集之後，應用程式會釋放陳述式控制代碼。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援每個連接控制碼有多個語句控制碼。 由於交易是在連接層級管理，因此在所有陳述式控制代碼上所執行的所有工作，會在單一連接控制代碼上管理成為相同交易的一部分。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [配置陳述式控制代碼](allocating-a-statement-handle.md)  
  
-   [&#40;ODBC&#41;來建立 SQL 語句](constructing-an-sql-statement-odbc.md)  
  
-   [建構資料指標的 SQL 陳述式](constructing-sql-statements-for-cursors.md)  
  
-   [使用陳述式參數](using-statement-parameters.md)  
  
-   [&#40;ODBC&#41;執行語句](executing-statements/executing-statements-odbc.md)  
  
-   [釋放陳述式控制代碼](freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
