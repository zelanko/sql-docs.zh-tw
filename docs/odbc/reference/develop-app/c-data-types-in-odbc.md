---
title: ODBC 中的 C 資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3817b33aa294d6081b9fa2ee240e67ac38dd2a25
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793985"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 資料類型
ODBC 定義的 C 資料類型所使用的應用程式變數和其對應的型別識別項。 這些使用繫結至結果集資料行和陳述式參數的緩衝區。 例如，假設應用程式想要擷取成字元格式的結果集資料行中的資料。 它會宣告變數與 SQLCHAR * 資料類型，並將此變數繫結 SQL_C_CHAR 的型別識別項的結果集資料行。 如需 C 資料類型和類型識別碼的完整清單，請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 也定義成 C 資料類型從每個 SQL 資料類型的預設對應。 例如，資料來源中的 2 位元組的整數會對應至應用程式中的 2 位元組的整數。 若要使用預設對應，應用程式會指定 SQL_C_DEFAULT 型別識別項。 不過，不建議使用這個識別項的互通性的原因。  
  
 在 ODBC 中定義的所有整數 C 資料類型*1.x*所簽署。 不帶正負號的 C 資料類型和其對應的型別識別項，已新增 ODBC 2.0 中。 因此，應用程式和驅動程式需要特別小心處理*1.x*版本。  
  
## <a name="c-data-type-extensibility"></a>C 資料類型擴充性  
 在 ODBC 3.8，您可以指定驅動程式特有的 C 資料類型。 這可讓您將 ODBC 應用程式中的特定驅動程式的 C 類型作為繫結 SQL 型別，當您呼叫[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，或[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。 這可能是適用於支援新的伺服器類型，因為現有的 C 資料類型可能無法正確呈現新的伺服器資料類型。 使用驅動程式特有的 C 類型可以增加驅動程式可以執行的轉換數目。  
  
 例如，假設資料庫管理系統 (DBMS) 導入新的 SQL 型別**DATETIMEOFFSET**，以代表的日期和時間與時區資訊。 沒有特定的 C 類型會出在該值與 ODBC **DATETIMEOFFSET**。 應用程式必須繫結**DATETIMEOFFSET** SQL_C_BINARY 以及轉換到使用者定義的資料類型。 從 C 資料類型擴充性與符合 ODBC 3.8，驅動程式可以定義新的對應的 C 類型。 例如，針對新 SQL 型別 DATETIMEOFFSET，驅動程式可以定義新對應的 C 類型例如 SQL_C_DATETIMEOFFSET。 然後，應用程式可以做為驅動程式特有的 C 類型繫結的新的 SQL 型別。  
  
 C 資料類型會定義驅動程式中，如下所示：  
  
-   應用程式中，ODBC 驅動程式和驅動程式管理員 ODBC 相容性層級為 3.8 （或更新版本）。  
  
-   驅動程式特有的 C 類型的資料範圍是 0x4000 和 0x7FFF 之間。  
  
-   驅動程式定義對應至 C 類型的資料結構。  做法是在驅動程式特有的 SDK。  
  
 驅動程式管理員將不會驗證 0x4000 和 0x7FFF; 的範圍中定義的 C 類型驅動程式將會執行驗證和任何資料類型轉換。 但是，如果傳遞給驅動程式管理員 C 類型的資料範圍之間 0x8000 和 0xFFFF 或 0x0000 和 0x3FFF 之間，驅動程式管理員會驗證的 C 資料類型。  
  
> [!NOTE]  
>  驅動程式特有的 C 資料類型都應該驅動程式文件中所述。  
  
 若要指定 ODBC 相容性層級的 3.8，應用程式會呼叫[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) SQL_ATTR_ODBC_VERSION 屬性設為**SQL_OV_ODBC3_80**。 若要判斷驅動程式版本，應用程式會呼叫**SQLGetInfo** SQL_DRIVER_ODBC_VER 使用。  
  
 如需有關 ODBC 3.8 的詳細資訊，請參閱[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另請參閱  
 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)
