---
title: SQLSpecialColumns |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 83800ef5c07d73413c236a890e2aea59d00d9437
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701089"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  當要求資料列識別碼 (*IdentifierType* SQL_BEST_ROWID)， **SQLSpecialColumns**傳回空的結果集 （無資料列） 的任何要求針對 SQL_SCOPE_CURROW 以外的範圍。 產生的結果集表示資料行只有在這個範圍中才是有效的。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援識別碼的虛擬資料行。 **SQLSpecialColumns**結果集將會將所有資料行識別為 SQL_PC_NOT_PSEUDO。  
  
 **SQLSpecialColumns**可以在靜態資料指標上執行。 嘗試執行**SQLSpecialColumns**上可更新 （索引鍵集驅動或動態） 傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已經變更。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSpecialColumns 支援  
 如需值的資訊傳回的資料行 DATA_TYPE、 TYPE_NAME、 COLUMN_SIZE、 BUFFER_LENGTH 和 DECIMAL_DIGTS 日期/時間類型，請參閱 <<c0> [ 目錄中繼資料](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSpecialColumns 支援  
 **SQLSpecialColumns**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSpecialColumns 函數](http://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
