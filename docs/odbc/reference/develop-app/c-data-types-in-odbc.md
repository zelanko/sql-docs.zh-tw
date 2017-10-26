---
title: "在 ODBC C 資料類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65a5bd882462dbd72c39c751dcfed52c61ab194c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="c-data-types-in-odbc"></a>在 ODBC C 資料類型
ODBC 定義應用程式變數和其相對應的類型識別項所使用的 C 資料類型。 會使用這些繫結至結果集資料行和陳述式的參數緩衝區。 例如，假設應用程式想要擷取成字元格式的結果集資料行的資料。 它會宣告一個變數以 SQLCHAR * 資料類型，並將此變數繫結至類型識別碼為 SQL_C_CHAR 的結果集資料行。 C 資料類型和類型識別碼的完整清單，請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 也已經定義成 C 資料類型從每個 SQL 資料類型的預設對應。 例如，資料來源中的 2 位元組的整數會對應至應用程式中的 2 位元組的整數。 若要使用預設對應，應用程式會指定 SQL_C_DEFAULT 類型識別項。 不過，不建議使用這個識別碼，基於互通性考量。  
  
 ODBC 1 中定義的所有整數 C 資料類型*.x*所簽署。 不帶正負號的 C 資料類型和其相對應的類型識別項已加入 ODBC 2.0 中。 因此，應用程式和驅動程式必須要特別小心處理 1 時*.x*版本。  
  
## <a name="c-data-type-extensibility"></a>C 資料類型擴充性  
 在 ODBC 3.8，您可以指定特定驅動程式的 C 資料類型。 這可讓您以在 ODBC 應用程式的驅動程式專屬 C 類型繫結 SQL 類型，當您呼叫[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，或[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。 這可能是適用於支援新的伺服器類型，因為現有的 C 資料類型可能無法正確呈現新的伺服器資料類型。 使用特定驅動程式的 C 類型可以增加驅動程式可以執行轉換的數目。  
  
 例如，假設資料庫管理系統 (DBMS) 導入了新的 SQL 類型， **DATETIMEOFFSET**，表示日期和時間與時區資訊。 對應到 ODBC 中會有沒有特定的 C 類型**DATETIMEOFFSET**。 應用程式必須將繫結**DATETIMEOFFSET** SQL_C_BINARY 和轉型為其使用者定義的資料類型。 使用 C 資料類型擴充功能的 ODBC 3.8 從開始，驅動程式可以定義新的對應 C 類型。 例如的新 SQL 型別 DATETIMEOFFSET，驅動程式可以定義 SQL_C_DATETIMEOFFSET 例如新的對應 C 類型。 然後，應用程式可以做為特定驅動程式的 C 類型繫結新的 SQL 類型。  
  
 C 資料類型會定義驅動程式中，如下所示：  
  
-   應用程式、 ODBC 驅動程式和驅動程式管理員 ODBC 相容性層級是 3.8 （或更新版本）。  
  
-   驅動程式特有的 C 類型的資料範圍是 0x4000 和 0x7FFF 之間。  
  
-   驅動程式會定義對應到 C 類型的資料結構。  作法是驅動程式特有的 SDK 中。  
  
 驅動程式管理員將不會驗證 0x4000 和 0x7FFF; 的範圍中定義的 C 類型驅動程式將會執行驗證和任何資料類型轉換。 但是，如果傳遞至驅動程式管理員 C 類型的資料範圍是介於 0x0000 0x3FFF 或 0x8000 和 0xFFFF 之間，驅動程式管理員會進行驗證的 C 資料類型。  
  
> [!NOTE]  
>  驅動程式特有的 C 資料類型應該在驅動程式文件中說明。  
  
 若要指定 ODBC 相容性層級的 3.8，應用程式呼叫[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) SQL_ATTR_ODBC_VERSION 屬性設定為**SQL_OV_ODBC3_80**。 若要判斷驅動程式版本，應用程式呼叫**SQLGetInfo** SQL_DRIVER_ODBC_VER 與。  
  
 如需 ODBC 3.8 的詳細資訊，請參閱[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另請參閱  
 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)

