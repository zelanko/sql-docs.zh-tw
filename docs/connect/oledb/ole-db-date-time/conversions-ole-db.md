---
title: 繫結和轉換 (OLE DB) |Microsoft 文件
description: 繫結和轉換 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 90c5a3086523b2cadce84678f2056cf265294648
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35304449"
---
# <a name="conversions-ole-db"></a>轉換 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本章節將討論如何將轉換之間**datetime**和**datetimeoffset**值。 本節中所描述的轉換已由 OLE DB 提供，或是一致的 OLE DB 延伸模組。  
  
 在 OLE DB 中，日期和時間之常值和字串的格式通常會遵循 ISO，而且不會相依於用戶端地區設定。 有一個例外是 DBTYPE_DATE，其中的標準為 OLE Automation。 不過，OLE DB 驅動程式的 SQL Server 僅在用戶端來回傳輸資料時的類型之間轉換，因為沒有任何要強制 OLE DB 驅動程式為 DBTYPE_DATE 和字串格式之間進行轉換的 SQL Server 的應用程式的方式。 否則，字串會使用下列格式 (以方括弧括住的文字表示選擇性的元素)：  
  
-   格式**datetime**和**datetimeoffset**字串是：  
  
     *yyyy*-*公釐*-*dd*[ *hh*:*公釐*:*ss*[。*9999999*] [± *hh*:*公釐*]]  
  
-   格式**時間**字串是：  
  
     *hh*:*公釐*:*ss*[。*9999999*]  
  
-   格式**日期**字串是：  
  
     *yyyy*-*mm*-*dd*  
  
> [!NOTE]  
>  如果標準轉換失敗，舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 和 SQLOLEDB 會實作 OLE 轉換。 SQL Server OLE DB 驅動程式會遵循相同的行為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端。 如此一來，針對 SQL Server OLE DB 驅動程式所執行的某些轉換與 OLE DB 規格不同。  
  
 字串的轉換在空白和欄位寬度上允許彈性。 如需詳細資訊，請參閱中的 「 資料格式： 字串和常值 」 一節[OLE DB 日期和時間增強功能的資料類型支援](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。  
  
 下面是一般轉換規則：  
  
-   當字串轉換為日期/時間類型時，會先將字串剖析為 ISO 常值。 如果失敗，則會將字串剖析為擁有日期元件的 OLE 日期常值。  
  
-   如果沒有任何時間存在，但是接收者可以儲存時間，則時間會設定為零。 如果沒有任何日期存在，但是接收者可以儲存日期，使用 ISO 轉換時，日期會設定為目前的日期，而使用 OLE 轉換時，則會設定為 1899-12-30。  
  
-   如果在資料類型中沒有用戶端所使用的時區存在，但是伺服器可以儲存時區，則會假設用戶端上的資料位於用戶端的時區中。  
  
-   如果在伺服器上沒有任何時區存在，但是用戶端擁有時區資訊，則會假設 UTC 時區。 這與伺服器行為不同。  
  
-   如果有時間存在，但是接收者無法儲存時間，則會忽略時間元件。  
  
-   如果有日期存在，但是接收者無法儲存日期，則會忽略日期元件。  
  
-   如果在從用戶端轉換為伺服器時發生秒或毫秒的截斷，就會傳回 DB_E_ERRORSOCCURRED，並設定 DBSTATUS_E_DATAOVERFLOW 狀態。  
  
-   如果在從伺服器轉換為用戶端時發生秒或毫秒的截斷，就會設定 DBSTATUS_S_TRUNCATED。  
  
## <a name="in-this-section"></a>本節內容  
 [從用戶端到伺服器執行的轉換](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)  
 描述之間執行的日期/時間轉換為 SQL Server 撰寫與 OLE DB 驅動程式的用戶端應用程式和[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更新版本）。  
  
 [從伺服器到用戶端執行的轉換](../../oledb/ole-db-date-time/conversions-performed-from-server-to-client.md)  
 描述之間執行的日期/時間轉換[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更新版本） 和 SQL Server 的撰寫與 OLE DB 驅動程式的用戶端應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間增強功能&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
