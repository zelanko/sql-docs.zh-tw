---
description: ISO 選項的作用
title: ISO 選項的效果 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 53012e9698cdd7132b6ea35a8296d84287a2767f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438371"
---
# <a name="effects-of-iso-options"></a>ISO 選項的作用
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC 標準與 ISO 標準相當接近，而且 ODBC 應用程式應該是來自 ODBC 驅動程式的標準行為。 為了使其行為與 ODBC 標準中所定義的行為更緊密地相符， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式一律會使用所連接之 SQL Server 版本中可用的任何 ISO 選項。  
  
 當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT odbc 驅動程式連接到的實例時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，伺服器會偵測到用戶端正在使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native client odbc 驅動程式，並在上設定數個選項。  
  
 驅動程式本身會發出這些陳述式；ODBC 應用程式不用做任何事情就可以要求它們。 設定這些選項可以使用驅動程式，讓 ODBC 應用程式更容易攜帶，因為伺服器行為會符合 ISO 標準。  
  
 以 DB-Library 為基礎的應用程式一般不會開啟這些選項。 在執行相同的 SQL 語句時觀察 ODBC 或 DB-Library 用戶端間不同行為的網站，不應該假設這會指向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式的問題。 他們應該先在 DB-Library 環境中，使用與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式所使用的相同 SET 選項來重新執行語句。  
  
 由於使用者和應用程式可以隨時開啟和關閉 SET 選項，因此，預存程序和觸發程序的開發人員也應該在開啟和關閉以上列出的 SET 選項時，小心測試其程序和觸發程序。 無論特定連接叫用程序或觸發程序時已經設定哪些選項，這都可以確保程序和觸發程序能正常運作。 對於需要為這些選項的其中之一進行特定設定的觸發程序或預存程序，應該在觸發程序或預存程序開始時發出 SET 陳述式。 此 SET 陳述式只有在執行觸發程序或預存程序時才有效，當程序或觸發程序結束時，就會還原原始的設定。  
  
 連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體時，也會將第四個 SET 選項，也就是 CONCAT_NULL_YIELDS_NULL，設定為開啟。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]如果資料來源或[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)中指定了 AnsiNPW = NO，Native Client ODBC 驅動程式就不會將這些選項設定為 on。  
  
 如同稍早所述的 ISO 選項， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式不會在資料來源或 **SQLDriverConnect** 或 **SQLBrowseConnect** 中指定 QuotedID = NO 時，開啟 QUOTED_IDENTIFIER 選項。  
  
 為了讓驅動程式知道 SET 選項的目前狀態，ODBC 應用程式應該不會使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET 陳述式來設定這些選項。 它們應該只會使用資料來源或連接選項設定這些選項。 如果應用程式發出 SET 陳述式，此驅動程式可能會產生不正確的 SQL 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行語句 ](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
