---
title: SQLGetTypeInfo |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60c4c4d364f9c07e9ca241dd357535f7f7acb42d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046683"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會在的結果集中報告額外的資料行`SQLGetTypeInfo`USERTYPE。 USERTYPE 會報告 DB-Library 資料類型定義，而且對於將現有 DB-Library 應用程式移植至 ODBC 的開發人員很有用。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將識別視為屬性，而 ODBC 則會將它視為資料類型。 若要解決這種`SQLGetTypeInfo`不相符的情形，會傳回資料類型： **intidentity**、 **Smallintidentity**、 **Tinyintidentity**、 **decimalidentity**和**numericidentity**。 [ `SQLGetTypeInfo`結果集] 資料行 AUTO_UNIQUE_VALUE 報告這些資料類型的 TRUE 值。  
  
 若為**Varchar**、 **Nvarchar**和**Varbinary**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會繼續針對 COLUMN_SIZE 值分別報告8000、4000和8000，即使它實際上不受限制。 這為了確保回溯相容性。  
  
 針對**xml**資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會報告 COLUMN_SIZE 的 SQL_SS_LENGTH_UNLIMITED，以表示無限制的大小。  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 和資料表值參數  
 資料表值參數的資料表類型實際上是中繼類型，也就是用來定義其他類型的類型。 因此，它不需要透過 SQLGetTypeInfo 公開。 應用程式必須使用 SQLTables （而非 SQLGetTypeInfo）來抓取與資料表值參數搭配使用之資料表類型的中繼資料。  
  
 如需有關為數據表值參數抓取 metdata 的詳細資訊，請參閱[影響資料表值參數的語句屬性](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetTypeInfo 支援  
 如需日期/時間類型傳回的值，請參閱[目錄中繼資料](../native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需更多一般資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetTypeInfo 支援  
 
  `SQLGetTypeInfo` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetTypeInfo 函式](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
