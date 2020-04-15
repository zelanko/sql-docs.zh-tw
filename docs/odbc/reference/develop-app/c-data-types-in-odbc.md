---
title: ODBC 中的 C 資料型態 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306293"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 資料類型
ODBC 定義應用程式變數及其相應的類型識別碼使用的C資料類型。 這些由綁定到結果集列和語句參數的緩衝區使用。 例如,假設應用程式希望以字元格式從結果集列檢索數據。 它聲明具有 SQLCHAR + 資料類型的變數,並將此變數綁定到具有SQL_C_CHAR類型識別符的結果集列。 關於 C 資料型態和類型識別碼的完整清單,請參考附錄[D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 還定義從每個 SQL 資料類型到 C 資料類型的預設映射。 例如,資料源中的 2 位元組整數映射到應用程式中的 2 位元組整數。 要使用預設映射,應用程式指定SQL_C_DEFAULT類型標識符。 但是,出於互操作性的原因,不鼓勵使用此標識符。  
  
 在 ODBC *1.x*中定義的所有整數 C 數據類型都進行了簽名。 在 ODBC 2.0 中添加了未簽名的 C 數據類型及其相應的類型標識符。 因此,在處理*1.x*版本時,應用程式和驅動程式需要特別小心。  
  
## <a name="c-data-type-extensibility"></a>C 資料型態擴充性  
 在 ODBC 3.8 中,您可以指定特定於驅動程式的 C 資料類型。 這使您能夠在調用[SQLBindCol、SQLGetData](../../../odbc/reference/syntax/sqlbindcol-function.md)或[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md)[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)時,在 ODBC 應用程式中將 SQL 類型綁定為特定於驅動程式的 C 類型。 這對於支援新的伺服器類型非常有用,因為現有的C資料類型可能無法正確表示新的伺服器數據類型。 使用特定於驅動程式的 C 類型可以增加驅動程式可以執行的轉換次數。  
  
 例如,假設資料庫管理系統 (DBMS) 引入了新的 SQL 類型**DATETIMEOFFSET,** 以表示具有時區資訊的日期和時間。 ODBC 中沒有與**DATETIMEOFFSET**相對應的特定 C 類型。 應用程式必須將**DATETIMEOFFSET**綁定為SQL_C_BINARY並將其轉換為使用者定義的數據類型。 從具有 C 資料類型擴充性的 ODBC 3.8 開始,驅動程式可以定義新的對應 C 類型。 例如,對於新的 SQL 類型 DATETIMEOFFSET,驅動程式可以定義新的對應 C 類型,如SQL_C_DATETIMEOFFSET。 然後,應用程式可以將新的 SQL 類型綁定為特定於驅動程式的 C 類型。  
  
 在驅動程式中定義 C 資料類型,如下所示:  
  
-   應用程式、ODBC 驅動程式和驅動程式管理員的 ODBC 合規性級別為 3.8(或更高)。  
  
-   特定於驅動程式的 C 類型的數據範圍介於 0x4000 和 0x7FFF 之間。  
  
-   驅動程式定義與 C 類型對應的數據的結構。  這可以在特定於驅動程式的 SDK 中完成。  
  
 驅動程式管理員不會驗證在 0x4000 和 0x7FFF 範圍內定義的 C 類型;因此,驅動程式管理員將驗證在 0x4000 和 0x7FFF 範圍內定義的 C 類型。驅動程式將執行驗證和任何數據類型轉換。 但是,如果傳遞給驅動程式管理器的 C 類型的數據範圍介於 0x0000 和 0x3FFF 之間或介於 0x8000 和 0xFFFF 之間,則驅動程式管理器將驗證 C 數據類型。  
  
> [!NOTE]  
>  驅動程式文件中應描述特定於驅動程式的 C 資料類型。  
  
 要指定 ODBC 合規性等級 3.8,應用程式呼叫[SQLSetEnvAttr,SQL_ATTR_ODBC_VERSION](../../../odbc/reference/syntax/sqlsetenvattr-function.md)屬性設定為**SQL_OV_ODBC3_80**。 要確定驅動程式的版本,應用程式使用SQL_DRIVER_ODBC_VER調用**SQLGetInfo。**  
  
 有關 ODBC 3.8 的詳細資訊,請參閱[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另請參閱  
 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)
