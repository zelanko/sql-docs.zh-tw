---
title: 字元資料的自動轉譯 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c08a0987e11f25c3f5b535d8d26526db5bb14a38
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779176"
---
# <a name="autotranslation-of-character-data"></a>字元資料的自動轉譯
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  字元資料（例如使用 SQL_C_CHAR 所宣告的 ANSI 字元變數，或使用**CHAR**、 **Varchar**或**text**資料類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存的資料）只能代表有限的字元數。 每個字元使用一個位元組儲存的字元資料僅能代表 256 個字元。 儲存在 SQL_C_CHAR 變數中的值會使用用戶端電腦的 ANSI 字碼頁 (ACP) 解譯。 在伺服器上使用**char**、 **Varchar**或**text**資料類型所儲存的值，會使用伺服器的 ACP 進行評估。  
  
 如果伺服器和用戶端都有相同的 ACP，就不會有任何問題解讀儲存在 SQL_C_CHAR、 **CHAR**、 **Varchar**或**text**物件中的值。 如果伺服器和用戶端有不同的 Acp，SQL_C_CHAR 則如果在**CHAR**、 **Varchar**或**text**資料行、變數或參數中使用用戶端的資料，則可能會在伺服器上將其轉譯為不同的字元。 例如，在使用字碼頁437的電腦上，包含值0xA5 的字元位元組會被解讀為字元-，並在執行字碼頁1252的電腦上解讀為日元符號（¥）。  
  
 Unicode 資料的每個字元會使用兩個位元組儲存。 Unicode 規格包含所有擴充字元，因此所有電腦都會以相同方式解譯所有 Unicode 字元。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的 AutoTranslate 功能會嘗試將在具有不同字碼頁的用戶端與伺服器之間移動字元資料的問題降到最低。 AutoTranslate 可以在[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)的連接字串、 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)的設定字串，或使用 ODBC 系統管理員為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式設定資料來源時，進行設定。  
  
 當 AutoTranslate 設定為 "no" 時，不會針對用戶端上的 SQL_C_CHAR 變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的**CHAR**、 **Varchar**或**text**資料行、變數或參數之間移動的資料進行轉換。 如果資料包含擴充字元，而且用戶端電腦和伺服器電腦的字碼頁不同，則位元模式在兩部電腦上的解譯方式可能會不同。 如果兩部電腦的字碼頁相同，資料將會以相同的方式解譯。  
  
 當 AutoTranslate 設定為 "yes" 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會使用 Unicode 來轉換在用戶端上 SQL_C_CHAR 變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的**CHAR**、 **Varchar**或**text**資料行、變數或參數之間移動的資料。資料  
  
-   當資料從用戶端上的 SQL_C_CHAR 變數傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的**CHAR**、 **Varchar**或**text**資料行、變數或參數時，ODBC 驅動程式會先使用用戶端的 ACP，從 SQL_C_CHAR 轉換為 Unicode，然後使用伺服器的 ACP，從 Unicode 回到字元。  
  
-   當資料從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的**char**、 **Varchar**或**text**資料行、變數或參數傳送到用戶端上的 SQL_C_CHAR 變數時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client ODBC 驅動程式會先使用 ACP，從字元轉換成 Unicode在伺服器上，然後使用用戶端的 ACP，從 Unicode 回到 SQL_C_CHAR。  
  
 因為這些轉換是由用戶端上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式所完成，所以伺服器 ACP 必須是安裝在用戶端電腦上的其中一個字碼頁。  
  
 透過 Unicode 進行字元轉換可確保正確轉換同時存在兩個字碼頁上的所有字元。 但是，如果字元存在於其中一個字碼頁，但不存在於另一個字碼頁，則無法在目標字碼頁中表示字元。 例如，字碼頁 1252 擁有註冊商標符號 (®)，而字碼頁 437 則沒有。  
  
 AutoTranslate 設定在進行下列轉換時沒有作用：  
  
-   在字元 SQL_C_CHAR 用戶端變數與 Unicode **Nchar**、 **Nvarchar**或**Ntext**資料行、變數或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的參數之間移動資料。  
  
-   在 Unicode SQL_C_WCHAR 用戶端變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的字元**char**、 **Varchar**或**text**資料行、變數或參數之間移動資料。  
  
 從字元移到 Unicode 時，永遠必須轉換資料。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41; ](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
