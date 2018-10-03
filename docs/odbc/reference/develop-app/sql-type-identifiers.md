---
title: SQL 型別識別項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1763ee0cd8c5bc2017160de44b9c047781649eba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740146"
---
# <a name="sql-type-identifiers"></a>SQL 類型識別碼
每個資料來源定義自己的 SQL 資料類型。 ODBC 定義型別識別項，並說明 SQL 資料類型，可能會對應至每個類型識別項的一般特性。 它是驅動程式專用的基礎資料來源中的每個資料類型對應至 ODBC SQL 類型識別碼的方式。  
  
 比方說，SQL_CHAR 是固定的長度，介於 1 到 254 個字元的字元資料行型別識別項。 這些特性會對應至許多 SQL 資料來源中找到的 CHAR 資料類型。 因此，當應用程式探索的資料行的型別識別項是 SQL_CHAR，它可以假設它可能處理 CHAR 資料行。 不過，它還是應該檢查假設它之前的資料行的位元組長度是介於 1 到 254 個字元;針對非 SQL 資料來源，例如，驅動程式可能對應 500 個字元的固定長度的字元資料行至 SQL_CHAR 或 SQL_LONGVARCHAR，因為兩者都完全相符。  
  
 ODBC 定義各種不同的 SQL 型別識別項。 不過，此驅動程式不需要使用所有這些識別項。 相反地，它使用基礎資料來源只有在需要公開 （expose） 支援的 SQL 資料類型的識別碼。 如果基礎資料來源支援的 SQL 資料類型的任何型別識別項對應，此驅動程式可以定義其他的型別識別項。 如需詳細資訊，請參閱 <<c0> [ 驅動程式專屬資料型別、 描述項類型、 資訊類型、 診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 SQL 型別識別項的完整說明，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d： 資料型別中。
