---
title: 日期和時間增強功能 |Microsoft 文件
description: 日期和時間增強功能 OLE DB 驅動程式 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d6b287b7cf96ec91ce776dd65bcec01e8c777a1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="date-and-time-improvements"></a>日期和時間增強功能
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題說明中所加入的日期和時間資料類型的 SQL Server 支援 OLE DB 驅動程式[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  
  
 如需有關日期/時間改善功能的詳細資訊，請參閱[日期和時間增強功能&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)。  
  
 如需示範這項功能的範例應用程式資訊，請參閱[SQL Server 資料程式設計範例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="usage"></a>使用方式  
 下列章節描述使用新日期和時間類型的各種方式。  
  
### <a name="use-date-as-a-distinct-data-type"></a>將 Date 當做不同的資料類型使用  
 開頭為[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]，增強型的日期/時間類型支援可讓使用 DBTYPE_DBDATE OLE DB 類型更有效率。  
  
### <a name="use-time-as-a-distinct-data-type"></a>將 Time 當做不同的資料類型使用  
 OLE DB 已經有只包含時間的資料類型 DBTYPE_DBTIME，其精確度為 1 秒。
  
 新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時間資料類型的小數秒精確度為 100 奈秒。 這需要 SQL Server 的 OLE DB 驅動程式中的新類型： DBTYPE_DBTIME2。 為使用不含小數秒的時間而撰寫的現有應用程式可以使用 time(0) 資料行。 現有的 OLE DB DBTYPE_TIME 類型和其相對應的結構應該正常運作，除非應用程式依賴中繼資料中傳回的型別。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>使用包含擴充小數秒精確度的 Time 做為不同的資料類型  
 有些應用程式 (例如，處理序控制項和製造應用程式) 必須能夠處理精確度高達 100 奈秒的時間資料。 針對此目的，OLE DB 中的新類型為 DBTYPE_DBTIME2。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>使用包含擴充小數秒精確度的 Datetime  
 OLE DB 已經定義一個精確度高達 1 奈秒的類型。 不過，此類型已由現有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式所使用，而且此類應用程式的精確度應該只有一秒的 1/300。 新**datetime2(3)** 類型不直接相容於現有 datetime 類型。 如果這有影響應用程式行為的風險，應用程式必須使用新的 DBCOLUMN 旗標來判斷實際的伺服器類型。    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>使用包含擴充小數秒精確度和時區的 Datetime  
 某些應用程式需要包含時區資訊的日期時間值。 這會受到新 DBTYPE_DBTIMESTAMPOFFSET 型別。
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>搭配與現有轉換一致的用戶端轉換使用 Date/Time/Datetime/Datetimeoffset 資料  
 轉換會擴充以一致的方式，以包含所有中導入的日期和時間類型之間的轉換[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
