---
title: 建立 SQL 語句（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eab0db859bbecea43d19b012a56b2e491b4ecfcf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81291424"
---
# <a name="constructing-an-sql-statement-odbc"></a>建構 SQL 陳述式 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 應用程式會透過執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，執行幾乎所有資料庫存取作業。 這些陳述式的形式完全取決於應用程式的需求。 您可以利用下列方式來建構 SQL 陳述式：  
  
-   寫入程式碼  
  
     應用程式當做固定工作執行的靜態陳述式。  
  
-   在執行階段建構  
  
     在執行階段建構的 SQL 陳述式，可讓使用者使用 SELECT、WHERE 和 ORDER BY 等一般子句來調整陳述式。 這包括使用者輸入的隨選查詢。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式只會針對不直接支援的 ODBC 和 ISO 語法[!INCLUDE[ssDE](../../includes/ssde-md.md)]，剖析 SQL 語句，驅動程式會將它轉換成[!INCLUDE[tsql](../../includes/tsql-md.md)]。 所有其他 SQL 語法會原封不動地傳遞至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將判斷它是否為有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這個方法會產生兩個優點：  
  
-   減少負擔  
  
     驅動程式的處理負擔會降到最低，因為它只需要掃描少數 ODBC 和 ISO 子句。  
  
-   彈性  
  
     程式設計人員可以調整其應用程式的可攜性。 若要針對多個資料庫強化可攜性，請主要使用 ODBC 和 ISO 語法。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有的增強功能，請使用適當的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式支援完整[!INCLUDE[tsql](../../includes/tsql-md.md)]的語法，因此，以 ODBC 為基礎的應用程式可以利用中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有功能。  
  
 SELECT 陳述式中的資料行清單應該僅包含執行目前工作所需的資料行。 這樣做不僅可減少透過網路傳送的資料量，還能減少資料庫變更對應用程式造成的影響。 如果某個應用程式沒有參考資料表中的資料行，此應用程式就不會受到對該資料行所做之任何變更的影響。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行查詢](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
