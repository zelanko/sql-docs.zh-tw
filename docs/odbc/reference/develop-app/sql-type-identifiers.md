---
title: "SQL 類型識別項 |Microsoft 文件"
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
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ec2f197029fab2467c7dced5f1cb720cf88f598
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sql-type-identifiers"></a>SQL 類型識別碼
每個資料來源定義自己的 SQL 資料類型。 ODBC 定義類型的識別項，並描述可能會對應至每個類型識別項的 SQL 資料類型的一般特性。 它是驅動程式專用的基礎資料來源中的每個資料類型如何對應至 ODBC SQL 類型識別碼。  
  
 例如，SQL_CHAR 是介於 1 到 254 個字元的固定長度的字元資料行的類型識別項。 這些特性會對應至多個 SQL 資料來源中找到的 CHAR 資料類型。 因此，當應用程式探索的資料行的類型識別項是 SQL_CHAR，它可以假設可能因 CHAR 資料行。 不過，它應該仍檢查假設它之前的資料行的位元組長度是介於 1 到 254 個字元。針對非 SQL 資料來源，比方說，驅動程式可能會對應 500 個字元的固定長度的字元資料行 SQL_CHAR 或 SQL_LONGVARCHAR，因為兩者都完全相符。  
  
 ODBC 定義各種不同的 SQL 類型識別項。 不過，驅動程式不需要使用所有這些識別項。 相反地，它使用基礎資料來源必須支援的 SQL 資料類型會公開這些識別項。 如果基礎資料來源支援的 SQL 資料類型轉換成對應的任何型別識別碼，驅動程式可以定義其他的型別識別項。 如需詳細資訊，請參閱[驅動程式特定資料類型，描述元類型、 資訊類型、 診斷的型別，以及屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 SQL 類型識別碼的完整說明，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d： 資料型別中。
