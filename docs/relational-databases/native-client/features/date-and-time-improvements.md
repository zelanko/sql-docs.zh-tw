---
title: 日期和時間改善 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f1bfa218a32d6cc4697fb0f7eef1748e117c0d7
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788252"
---
# <a name="date-and-time-improvements"></a>日期和時間改善
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中所加入日期和時間資料類型的支援。  
  
 如需日期/時間改善的詳細資訊，請參閱[日期和&#40;時間&#41;改進 OLE DB](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)和[ODBC&#41;的&#40;日期和時間改善](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
 如需示範這項功能之範例應用程式的詳細資訊，請參閱 [SQL Server 資料程式設計範例](https://msftdpprodsamples.codeplex.com/)。  
  
## <a name="usage"></a>使用方式  
 下列章節描述使用新日期和時間類型的各種方式。  
  
### <a name="use-date-as-a-distinct-data-type"></a>將 Date 當做不同的資料類型使用  
 從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，對於日期/時間類型的增強支援讓使用 SQL_TYPE_DATE ODBC 類型 (適用於 ODBC 2.0 應用程式的 SQL_DATE) 和 DBTYPE_DBDATE OLE DB 類型更有效率。  
  
### <a name="use-time-as-a-distinct-data-type"></a>將 Time 當做不同的資料類型使用  
 OLE DB 已經有只包含時間的資料類型 DBTYPE_DBTIME，其精確度為 1 秒。 在 ODBC 中，對等的類型為 SQL_TYPE_TIME (適用於 ODBC 2.0 應用程式的 SQL_TIME)。  
  
 新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時間資料類型的小數秒精確度為 100 奈秒。 這需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client： DBTYPE_DBTIME2 （OLE DB）和 SQL_SS_TIME2 （ODBC）中的新類型。 為使用不含小數秒的時間而撰寫的現有應用程式可以使用 time(0) 資料行。 除非應用程式依賴中繼資料中所傳回的類型，否則現有的 OLE DB DBTYPE_TIME 和 ODBC SQL_TYPE_TIME 類型及其對應的結構應該正常運作。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>使用包含擴充小數秒精確度的 Time 做為不同的資料類型  
 有些應用程式 (例如，處理序控制項和製造應用程式) 必須能夠處理精確度高達 100 奈秒的時間資料。 基於此目的的新類型為 DBTYPE_DBTIME2 (OLE DB) 和 SQL_SS_TIME2 (ODBC)。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>使用包含擴充小數秒精確度的 Datetime  
 OLE DB 已經定義一個精確度高達 1 奈秒的類型。 不過，此類型已由現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式所使用，而且此類應用程式的精確度應該只有一秒的 1/300。 新的 **datetime2(3)** 類型與現有的日期時間類型不直接相容。 如果這有影響應用程式行為的風險，應用程式必須使用新的 DBCOLUMN 旗標來判斷實際的伺服器類型。  
  
 ODBC 也已經定義一個精確度高達 1 奈秒的類型。 不過，此類型已由現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式所使用，而且此類應用程式的精確度應該只有 3 毫秒。 新的**datetime2 （3）** 類型與現有的**日期時間**類型不直接相容。 **datetime2 （3）** 的精確度為1毫秒，而**datetime**的精確度為1/300 秒。 在 ODBC 中，應用程式可以判斷正搭配描述項欄位 SQL_DESC_TYPE_NAME 使用的伺服器類型。 因此，現有的類型 SQL_TYPE_TIMESTAMP (適用於 ODBC 2.0 應用程式的 SQL_TIMESTAMP) 可同時用於兩種類型。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>使用包含擴充小數秒精確度和時區的 Datetime  
 某些應用程式需要包含時區資訊的日期時間值。 這受到新 DBTYPE_DBTIMESTAMPOFFSET (OLE DB) 和 SQL_SS_TIMESTAMPOFFSET (ODBC) 類型的支援。  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>搭配與現有轉換一致的用戶端轉換使用 Date/Time/Datetime/Datetimeoffset 資料  
 ODBC 標準描述現有日期、時間和時間戳記類型之間的轉換如何運作。 這些類型會以一致的方式擴充，以包含 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中所推出之所有日期和時間類型之間的轉換。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
