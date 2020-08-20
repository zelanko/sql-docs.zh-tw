---
description: ODBC 中的 C 資料類型
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
ms.openlocfilehash: 395f60860dd3179326687a6c2fb10bbaf027ca3a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494758"
---
# <a name="c-data-types-in-odbc"></a>ODBC 中的 C 資料類型
ODBC 會定義應用程式變數所使用的 C 資料類型，以及其對應的類型識別碼。 這些緩衝區是由系結至結果集資料行和語句參數的緩衝區所使用。 例如，假設應用程式想要以字元格式從結果集資料行中取出資料。 它會宣告具有 SQLCHAR * 資料類型的變數，並將此變數系結至類型識別碼為 SQL_C_CHAR 的結果集資料行。 如需 C 資料類型和類型識別碼的完整清單，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 ODBC 也會定義從每個 SQL 資料類型到 C 資料類型的預設對應。 例如，資料來源中的2個位元組整數會對應到應用程式中的2個位元組整數。 若要使用預設對應，應用程式會指定 SQL_C_DEFAULT 類型識別碼。 不過，基於互通性的理由，不建議使用此識別碼。  
  
 *ODBC 1.x*中定義的所有整數 C 資料類型都已簽署。 ODBC 2.0 中新增了未簽署的 C 資料類型及其對應的類型識別碼。 因此，當處理 *1.x 版時* ，應用程式和驅動程式必須特別小心。  
  
## <a name="c-data-type-extensibility"></a>C 資料類型擴充性  
 在 ODBC 3.8 中，您可以指定驅動程式特定的 C 資料類型。 這可讓您在呼叫 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)或 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)時，將 SQL 型別系結為 ODBC 應用程式中的驅動程式特定 C 類型。 這有助於支援新的伺服器類型，因為現有的 C 資料類型可能無法正確表示新的伺服器資料類型。 使用驅動程式特定的 C 類型可以增加驅動程式可執行檔轉換數目。  
  
 例如，假設資料庫管理系統 (DBMS) 引進了新的 SQL 類型（ **DATETIMEOFFSET**）來表示具有時區資訊的日期和時間。 ODBC 中不會有對應至 **DATETIMEOFFSET**的特定 C 類型。 應用程式必須將 **DATETIMEOFFSET** 系結為 SQL_C_BINARY，並將其轉換成使用者定義的資料類型。 從具有 C 資料類型擴充性的 ODBC 3.8 開始，驅動程式可以定義新的對應 C 型別。 例如，針對新的 SQL 型別 DATETIMEOFFSET，驅動程式可以定義新的對應 C 類型（例如 SQL_C_DATETIMEOFFSET）。 然後，應用程式可以將新的 SQL 類型系結為驅動程式特定的 C 類型。  
  
 C 資料類型定義于驅動程式中，如下所示：  
  
-   應用程式、ODBC 驅動程式和驅動程式管理員的 ODBC 相容性層級為 3.8 (或更高的) 。  
  
-   驅動程式專用 C 類型的資料範圍介於0x4000 和0x7FFF 之間。  
  
-   驅動程式會定義對應至 C 類型之資料的結構。  這可以在驅動程式專用的 SDK 中完成。  
  
 驅動程式管理員不會驗證0x4000 和0x7FFF 範圍中定義的 C 類型;驅動程式將會執行驗證和任何資料類型轉換。 但是，如果傳遞至驅動程式管理員的 C 類型資料範圍介於0x0000 和0x3FFF 之間，或在0x8000 到0xFFFF 之間，驅動程式管理員將會驗證 C 資料類型。  
  
> [!NOTE]  
>  驅動程式特有的 C 資料類型應該在驅動程式檔中說明。  
  
 為了指定 ODBC 相容性層級3.8，應用程式會呼叫 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) ，並將 SQL_ATTR_ODBC_VERSION 屬性設定為 **SQL_OV_ODBC3_80**。 為了判斷驅動程式的版本，應用程式會使用 SQL_DRIVER_ODBC_VER 來呼叫 **SQLGetInfo** 。  
  
 如需 ODBC 3.8 的詳細資訊，請參閱 [odbc 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
## <a name="see-also"></a>另請參閱  
 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)
