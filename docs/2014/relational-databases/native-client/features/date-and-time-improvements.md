---
title: 日期和時間增強功能 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a30f330bf4d7e5976d3873bec5e6042f498c9c95
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031846"
---
# <a name="date-and-time-improvements"></a>日期和時間增強功能
  本主題描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中所加入日期和時間資料類型的支援。  
  
 如需有關日期/時間改善功能的詳細資訊，請參閱[日期和時間增強功能&#40;OLE DB&#41; ](../../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)和[日期和時間增強功能&#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
 如需示範這項功能的範例應用程式資訊，請參閱[SQL Server 資料程式設計範例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="usage"></a>使用方式  
 下列章節描述使用新日期和時間類型的各種方式。  
  
### <a name="use-date-as-a-distinct-data-type"></a>將 Date 當做不同的資料類型使用  
 從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，對於日期/時間類型的增強支援讓使用 SQL_TYPE_DATE ODBC 類型 (適用於 ODBC 2.0 應用程式的 SQL_DATE) 和 DBTYPE_DBDATE OLE DB 類型更有效率。  
  
### <a name="use-time-as-a-distinct-data-type"></a>將 Time 當做不同的資料類型使用  
 OLE DB 已經有只包含時間的資料類型 DBTYPE_DBTIME，其精確度為 1 秒。 在 ODBC 中，對等的類型為 SQL_TYPE_TIME (適用於 ODBC 2.0 應用程式的 SQL_TIME)。  
  
 新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時間資料類型的小數秒精確度為 100 奈秒。 這需要在新的型別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端： DBTYPE_DBTIME2 (OLE DB) 和 SQL_SS_TIME2 (ODBC)。 為使用不含小數秒的時間而撰寫的現有應用程式可以使用 time(0) 資料行。 除非應用程式依賴中繼資料中所傳回的類型，否則現有的 OLE DB DBTYPE_TIME 和 ODBC SQL_TYPE_TIME 類型及其對應的結構應該正常運作。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>使用包含擴充小數秒精確度的 Time 做為不同的資料類型  
 有些應用程式 (例如，處理序控制項和製造應用程式) 必須能夠處理精確度高達 100 奈秒的時間資料。 基於此目的的新類型為 DBTYPE_DBTIME2 (OLE DB) 和 SQL_SS_TIME2 (ODBC)。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>使用包含擴充小數秒精確度的 Datetime  
 OLE DB 已經定義一個精確度高達 1 奈秒的類型。 不過，此類型已由現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式所使用，而且此類應用程式的精確度應該只有一秒的 1/300。 新的 `datetime2(3)` 類型與現有的日期時間類型不直接相容。 如果這有影響應用程式行為的風險，應用程式必須使用新的 DBCOLUMN 旗標來判斷實際的伺服器類型。  
  
 ODBC 也已經定義一個精確度高達 1 奈秒的類型。 不過，此類型已由現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式所使用，而且此類應用程式的精確度應該只有 3 毫秒。 新的 `datetime2(3)` 類型與現有的 `datetime` 類型不直接相容。 `datetime2(3)` 的精確度為 1 毫秒，而 `datetime` 的精確度為一秒的 1/300。 在 ODBC 中，應用程式可以判斷正搭配描述項欄位 SQL_DESC_TYPE_NAME 使用的伺服器類型。 因此，現有的類型 SQL_TYPE_TIMESTAMP (適用於 ODBC 2.0 應用程式的 SQL_TIMESTAMP) 可同時用於兩種類型。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>使用包含擴充小數秒精確度和時區的 Datetime  
 某些應用程式需要包含時區資訊的日期時間值。 這受到新 DBTYPE_DBTIMESTAMPOFFSET (OLE DB) 和 SQL_SS_TIMESTAMPOFFSET (ODBC) 類型的支援。  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>搭配與現有轉換一致的用戶端轉換使用 Date/Time/Datetime/Datetimeoffset 資料  
 ODBC 標準描述現有日期、時間和時間戳記類型之間的轉換如何運作。 這些類型會以一致的方式擴充，以包含 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中所推出之所有日期和時間類型之間的轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  