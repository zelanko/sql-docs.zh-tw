---
title: 建構 SQL 陳述式 (ODBC) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3e4b2665920541ac2b59a706e0088adc83c35ad2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937311"
---
# <a name="constructing-an-sql-statement-odbc"></a>建構 SQL 陳述式 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 應用程式會透過執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，執行幾乎所有資料庫存取作業。 這些陳述式的形式完全取決於應用程式的需求。 您可以利用下列方式來建構 SQL 陳述式：  
  
-   寫入程式碼  
  
     應用程式當做固定工作執行的靜態陳述式。  
  
-   在執行階段建構  
  
     在執行階段建構的 SQL 陳述式，可讓使用者使用 SELECT、WHERE 和 ORDER BY 等一般子句來調整陳述式。 這包括使用者輸入的隨選查詢。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client ODBC 驅動程式會剖析 SQL 陳述式，只針對不直接支援的 ODBC 和 ISO 語法[!INCLUDE[ssDE](../../includes/ssde-md.md)]，其驅動程式會將轉換成[!INCLUDE[tsql](../../includes/tsql-md.md)]。 所有其他 SQL 語法會原封不動地傳遞至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將判斷它是否為有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這個方法會產生兩個優點：  
  
-   減少負擔  
  
     驅動程式的處理負擔會降到最低，因為它只需要掃描少數 ODBC 和 ISO 子句。  
  
-   彈性  
  
     程式設計人員可以調整其應用程式的可攜性。 若要針對多個資料庫強化可攜性，請主要使用 ODBC 和 ISO 語法。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特有的增強功能，請使用適當的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援完整[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，因此以 ODBC 為基礎的應用程式可以充分利用中的所有功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 SELECT 陳述式中的資料行清單應該僅包含執行目前工作所需的資料行。 這樣做不僅可減少透過網路傳送的資料量，還能減少資料庫變更對應用程式造成的影響。 如果某個應用程式沒有參考資料表中的資料行，此應用程式就不會受到對該資料行所做之任何變更的影響。  
  
## <a name="see-also"></a>另請參閱  
 [執行查詢&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
