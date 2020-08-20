---
description: SQL 最小文法
title: SQL 最小文法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07adcbb100fa28a941be4fdac6efabb445ffb9ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456561"
---
# <a name="sql-minimum-grammar"></a>SQL 最小文法
本節說明 ODBC 驅動程式必須支援的最小 SQL 語法。 本章節所述的語法是 SQL-92 之專案層級語法的子集。  
  
 應用程式可以使用本節中的任何語法，並確保任何符合 ODBC 規範的驅動程式都支援該語法。 若要判斷是否支援不在此區段中的其他 SQL-92 功能，應用程式應該使用 SQL_SQL_CONFORMANCE 資訊類型來呼叫 **SQLGetInfo** 。 即使驅動程式不符合任何 SQL-92 一致性層級，應用程式仍然可以使用本節中所述的語法。 另一方面，如果驅動程式符合 SQL-92 層級，就會支援該層級所包含的所有語法。 這包括本節中的語法，因為此處所述的最小文法是最低的 SQL-92 一致性層級的純子集。 一旦應用程式知道支援的 SQL-92 層級，就可以藉由呼叫 **SQLGetInfo** 與對應于該功能的個別資訊類型，判斷是否支援較高層級的功能 (如果有任何) 。  
  
 僅適用于唯讀資料來源的驅動程式，可能不支援本節中包含在處理變更資料的部分文法。 應用程式可以使用 SQL_DATA_SOURCE_READ_ONLY 資訊類型來呼叫 **SQLGetInfo** ，以判斷資料來源是否為唯讀。  
  
## <a name="statement"></a>引數  
 *create-table 語句* ：： =  
  
 CREATE TABLE *基礎資料表名稱*  
  
  (*資料行識別碼資料類型* [*，資料行識別碼資料類型*] ... )   
  
> [!IMPORTANT]  
>  在*create-table 語句*中，應用程式必須使用**SQLGetTypeInfo**所傳回之結果集的 TYPE_NAME 資料*行中的*資料類型。  
  
 *delete 語句-搜尋* ：： =  
  
 從 *資料表名稱* 刪除 [WHERE *搜尋條件*]  
  
 *drop table 語句* ：： =  
  
 DROP TABLE *-資料表名稱*  
  
 *insert 語句* ：： =  
  
 插入 *資料表名稱* [ ( 資料 *行識別碼* [，資料 *行識別碼*] ... ) ] 值 (*插入值*[， *插入值*] ... )   
  
 *select-statement* ::=  
  
 選取 [所有 &#124; 相異] *選取清單*  
  
 從 *資料表參考清單*  
  
 [WHERE *搜尋條件*]  
  
 [*order by 子句*]  
  
 *語句* ：： = *create-table 語句*  
  
 &#124; *delete 語句-搜尋*  
  
 &#124; *drop table 語句*  
  
 &#124; *insert 語句*  
  
 &#124; *select 語句*  
  
 &#124; *更新語句-搜尋*  
  
 *update 語句-搜尋*  
  
 更新 *資料表名稱*  
  
 設定資料 *行識別碼* = {*expression* &#124; Null}  
  
 [，資料 *行識別碼* = {*運算式* &#124; Null}] .。。  
  
 [WHERE *搜尋條件*]  
  
 此章節包含下列主題。  
  
-   [SQL 陳述式中使用的項目](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [資料類型支援](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [參數資料類型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [參數標記](../../../odbc/reference/appendixes/parameter-markers.md)
