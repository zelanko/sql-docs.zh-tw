---
title: 字元資料的自動翻譯 |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a8672f748af8d643fa39038be030efa5d434dc8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297878"
---
# <a name="autotranslation-of-character-data"></a>字元資料的自動轉譯
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  字元資料(如用SQL_C_CHAR或儲存在使用**字元****、varchar**或**文字**資料類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中儲存的資料聲明的 ANSI 字元變數)只能表示有限數量的字元。 每個字元使用一個位元組儲存的字元資料僅能代表 256 個字元。 儲存在 SQL_C_CHAR 變數中的值會使用用戶端電腦的 ANSI 字碼頁 (ACP) 解譯。 使用**字元****、varchar**或**文本**資料類型存儲在伺服器上的值使用伺服器的 ACP 進行評估。  
  
 如果伺服器和用戶端具有相同的 ACP,則它們在解釋存儲在SQL_C_CHAR、**字元****、varchar**或**文本**物件中的值時沒有問題。 如果伺服器和用戶端具有不同的 ASP,則來自用戶端SQL_C_CHAR數據可能會被解釋為伺服器上的不同字元,如果它用於**字元****、varchar**或**文本**列、變數或參數。 例如,包含值 0xA5 的字元位元組在電腦上使用代碼頁 437 將解釋為字元 +,並在運行代碼頁 1252 的電腦上解釋為日元符號 (*)。  
  
 Unicode 資料的每個字元會使用兩個位元組儲存。 Unicode 規格包含所有擴充字元，因此所有電腦都會以相同方式解譯所有 Unicode 字元。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式的 AutoTranslate 功能嘗試將在用戶端和具有不同代碼頁的伺服器之間行動字元資料時的問題降至最低。 自動轉換可以在[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)的連接字串中設定 ,在[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)的設定字串中,或者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 ODBC 管理員為本機用戶端 ODBC 驅動程式設定數據源時。  
  
 當 AutoTranslate 設定為「否」時,對客戶端和**資料庫中的字元****、varchar**或**文本**列、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]變數或參數 之間移動 SQL_C_CHAR的數據不執行轉換。 如果資料包含擴充字元，而且用戶端電腦和伺服器電腦的字碼頁不同，則位元模式在兩部電腦上的解譯方式可能會不同。 如果兩部電腦的字碼頁相同，資料將會以相同的方式解譯。  
  
 當 AutoTranslate 設定為「時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 ODBC 驅動程式使用 Unicode 轉換在客戶端和**資料庫中的字元****、varchar**或**文字**列、變數或參數[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之間移動 SQL_C_CHAR的資料:  
  
-   當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據從用戶端上的SQL_C_CHAR變數傳送到資料庫中的**字元****、varchar**或**文字**列、變數或參數時,ODBC 驅動程式首先使用用戶端的 ACP 從SQL_C_CHAR轉換為 Unicode,然後使用伺服器的 ACP 將 Unicode 轉換回字元。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當資料從資料庫中的**字元****、varchar**或**文字**列、變數或參數傳送到用戶端上的SQL_C_CHAR變數時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 本機客戶端 ODBC 驅動程式首先使用伺服器的 ACP 從字元轉換為 Unicode,然後使用用戶端的 ACP 從 Unicode 轉換回SQL_C_CHAR。  
  
 由於所有這些轉換都由在用戶端上執行的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式完成,因此伺服器ACP必須是用戶端電腦上安裝的代碼頁之一。  
  
 透過 Unicode 進行字元轉換可確保正確轉換同時存在兩個字碼頁上的所有字元。 但是，如果字元存在於其中一個字碼頁，但不存在於另一個字碼頁，則無法在目標字碼頁中表示字元。 例如，字碼頁 1252 擁有註冊商標符號 (®)，而字碼頁 437 則沒有。  
  
 AutoTranslate 設定在進行下列轉換時沒有作用：  
  
-   在字元SQL_C_CHAR用戶端變數和 Unicode **nchar、nvarchar**或**資料庫中的 ntext**列、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]變數或參數**nvarchar**之間 移動數據。  
  
-   在 Unicode SQL_C_WCHAR用戶端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]變數 和字元**字元****、varchar**或**資料庫中的文本**列、變數或參數之間行動資料。  
  
 從字元移到 Unicode 時，永遠必須轉換資料。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
