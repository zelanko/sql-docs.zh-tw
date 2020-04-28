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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306293"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 資料類型
ODBC 會定義應用程式變數及其對應類型識別碼所使用的 C 資料類型。 這些是由系結至結果集資料行和語句參數的緩衝區所使用。 例如，假設應用程式想要從結果集資料行中取出字元格式的資料。 它會宣告具有 SQLCHAR * 資料類型的變數，並將此變數系結至具有 SQL_C_CHAR 之類型識別碼的結果集資料行。 如需 C 資料類型和類型識別碼的完整清單，請參閱[附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 也會定義從每個 SQL 資料類型到 C 資料類型的預設對應。 例如，資料來源中的2位元組整數會對應到應用程式中的2位元組整數。 若要使用預設對應，應用程式會指定 SQL_C_DEFAULT 類型識別碼。 不過，基於互通性的理由，不建議使用此識別碼。  
  
 *已簽署 ODBC 1.x*中定義的所有整數 C 資料類型。 ODBC 2.0 中已加入不帶正負號的 C 資料類型及其對應的類型識別碼。 因此，處理*1.x 版時*，應用程式和驅動程式必須特別小心。  
  
## <a name="c-data-type-extensibility"></a>C 資料類型擴充性  
 在 ODBC 3.8 中，您可以指定驅動程式特定的 C 資料類型。 當您呼叫[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)或[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)時，這可讓您將 SQL 類型系結為 ODBC 應用程式中的驅動程式特有 C 類型。 這對支援新的伺服器類型很有用，因為現有的 C 資料類型可能無法正確呈現新的伺服器資料類型。 使用驅動程式特定的 C 類型可能會增加驅動程式可執行檔轉換數目。  
  
 例如，假設資料庫管理系統（DBMS）引進了新的 SQL 型別**DATETIMEOFFSET**，以代表時區資訊的日期和時間。 在 ODBC 中，不會有任何特定 C 類型雖然該值至**DATETIMEOFFSET**。 應用程式必須將**DATETIMEOFFSET**系結為 SQL_C_BINARY，並將它轉換成使用者定義的資料類型。 從具有 C 資料類型擴充性的 ODBC 3.8 開始，驅動程式可以定義新的對應 C 類型。 例如，針對新的 SQL 類型 DATETIMEOFFSET，驅動程式可以定義新的對應 C 類型，例如 SQL_C_DATETIMEOFFSET。 然後，應用程式可以將新的 SQL 類型系結為驅動程式特有的 C 類型。  
  
 C 資料類型定義于驅動程式中，如下所示：  
  
-   應用程式的 ODBC 相容性層級（ODBC 驅動程式和驅動程式管理員）為3.8 （或更高版本）。  
  
-   驅動程式特定 C 類型的資料範圍是介於0x4000 和0x7FFF 之間。  
  
-   驅動程式會定義對應至 C 類型之資料的結構。  這可以在驅動程式特定的 SDK 中完成。  
  
 驅動程式管理員不會驗證0x4000 和0x7FFF 範圍內定義的 C 類型;驅動程式將會執行驗證和任何資料類型轉換。 但是，如果傳遞給驅動程式管理員的 C 類型的資料範圍是介於0x0000 和0x3FFF 之間，或是在0x8000 與0xFFFF 之間，驅動程式管理員將會驗證 C 資料類型。  
  
> [!NOTE]  
>  驅動程式特有的 C 資料類型應在驅動程式檔中說明。  
  
 若要指定 ODBC 相容性層級3.8，應用程式會呼叫[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) ，並將 SQL_ATTR_ODBC_VERSION 屬性設為**SQL_OV_ODBC3_80**。 為了判斷驅動程式的版本，應用程式會使用 SQL_DRIVER_ODBC_VER 來呼叫**SQLGetInfo** 。  
  
 如需 ODBC 3.8 的詳細資訊，請參閱[odbc 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另請參閱  
 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)
