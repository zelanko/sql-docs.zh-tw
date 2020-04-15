---
title: SQLGetTypeInfo |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81ba57c6e66f156f13055ff5ec941fa8f0c86381
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298433"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 ODBC 驅動程式報告**SQLGetTypeInfo**的結果集中的其他列 USERTYPE。 USERTYPE 會報告 DB-Library 資料類型定義，而且對於將現有 DB-Library 應用程式移植至 ODBC 的開發人員很有用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將識別視為屬性，而 ODBC 則會將它視為資料類型。 為了解決這種不符合 **,SQLGetTypeInfo**傳回資料類型:**身份識別**,**小身份**識別、**小身份**識別、**小數位識別**與**數位識別**。 **SQLGetTypeInfo**結果集列AUTO_UNIQUE_VALUE報告這些資料類型的值 TRUE。  
  
 對於**瓦爾查爾**,**恩瓦爾查爾**和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**瓦二進位**, 本機用戶端 ODBC 驅動程式繼續報告 8000,4000 和 8000 分別COLUMN_SIZE值,即使它實際上是無限的。 這為了確保回溯相容性。  
  
 對於**xml**資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型, 本機用戶端 ODBC 驅動程式SQL_SS_LENGTH_UNLIMITED報告,以便COLUMN_SIZE表示無限大小。  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 和資料表值參數  
 表值參數的表類型實際上是一種元類型,即用於定義其他類型的類型。 因此,它不必通過 SQLGetTypeInfo 公開。 應用程式必須使用 SQLTables 而不是 SQLGetTypeInfo 來檢索與表值參數一起使用的表類型的中數據。  
  
 有關詳細資訊,請參閱有關檢索表值參數的 metdata,請參閱[影響表值參數的語句屬性](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)。  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLGetTypeInfo 支援  
 關於日期/時間類型傳回的值,請參考[目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 有關更一般的資訊,請參閱[ODBC&#41;&#40;日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLGetTypeInfo 支援  
 **SQLGetTypeInfo**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetTypeInfo 函數](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
