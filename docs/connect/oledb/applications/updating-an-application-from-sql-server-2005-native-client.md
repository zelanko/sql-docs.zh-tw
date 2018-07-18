---
title: 從 SQL Server 2005 Native Client 將應用程式更新 |Microsoft 文件
description: 從 SQL Server 2005 Native Client 將應用程式更新
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 60a03e3ec34c29821a6b29d3174b11c5376511e6
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612063"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>從 SQL Server 2005 Native Client 更新應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主題討論自 SQL Server 的 OLE DB 驅動程式的重大變更[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的原生用戶端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  

 當您升級至 OLE DB 驅動程式的從 Microsoft Data Access Components (MDAC) for SQL Server 時，您也可能會看到一些行為差異。 如需詳細資訊，請參閱[應用程式更新至 OLE DB 驅動程式的 SQL Server 從 MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 隨附[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 隨附[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 隨附於 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 隨附於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。  

|OLE DB 驅動程式中的行為變更的 SQL Server 相較於[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]原生用戶端|描述|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 只會填補至定義的小數位數。|OLE DB 驅動程式的 SQL Server 會只為止的最大長度的資料中的尾端零填補進行轉換的轉換的資料傳送給伺服器， **datetime**值。 SQL Server Native Client 9.0 則會填滿至 9 位數。|  
|如 ICommandWithParameter::SetParameterInfo 驗證 DBTYPE_DBTIMESTAMP。|OLE DB 驅動程式的 SQL Server 實作的 OLE DB 需求*bScale*中 ICommandWithParameter::SetParameterInfo 針對 DBTYPE_DBTIMESTAMP 設定為小數的秒數有效位數。|  
|**Sp_columns**預存程序現在會傳回 **"NO"** 而不是 **"NO"** IS_NULLABLE 資料行。|OLE DB 驅動程式中的 SQL Server **sp_columns**預存程序現在會傳回 **"NO"** 而不是 **"NO"** IS_NULLABLE 資料行。|  
|當日期超出範圍時傳回不同錯誤。|如**datetime** ，不同的錯誤數目將會傳回類型的 OLE DB 驅動程式適用於 SQL Server 超出範圍的日期比在舊版中傳回。<br /><br /> 具體來說， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 會針對所有超出範圍的年份值在字串轉換為傳回 22007 **datetime**，和 OLE DB 驅動程式的 SQL Server 時的日期是所支援的範圍內，傳回22008**datetime2**所支援的範圍外**datetime**或**smalldatetime**。|  
|**datetime**值會截斷小數秒數和 round 如果不在四捨五入會改變日期。|之前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 的用戶端行為**datetime**傳送到伺服器的值是要四捨五入到最接近的 1/300 秒。 OLE DB 驅動程式的 SQL Server，在這個情況會造成小數秒被截斷，如果四捨五入會改變日期。|  
|可能會截斷秒為單位的**datetime**值。|連接到 SQL Server 的 OLE DB 驅動程式建置的應用程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]2005年伺服器將會截斷秒和小數秒的時間部分的資料傳送到伺服器，如果您繫結至類型識別碼為 DBTYPE_DBTIMESTAMP （datetime 資料行OLE DB) 或 SQL_TIMESTAMP (ODBC) 和小數位數為 0。<br /><br /> 例如：<br /><br /> 輸入資料：1994-08-21 21:21:36.000<br /><br /> 插入的資料：1994-08-21 21:21:00.000|  
|從 DBTYPE_DBTIME 轉換成 DBTYPE_DATE 的 OLE DB 資料轉換作業不會再造成日期變更。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的時間部分在午夜的半秒鐘之內，OLE DB 轉換程式碼會造成日期變更。 OLE DB 驅動程式中的 SQL Server，日期將不會變更 （小數秒會截斷，並不會四捨五入）。|  
|IBCPSession::BCColFmt 轉換變更。|OLE DB 驅動程式中的 SQL Server，當您使用 IBCPSession::BCOColFmt 將 SQLDATETIME 或 SQLDATETIME 轉換成字串類型，就會匯出小數值。 例如，當轉換輸入 SQLDATETIME 類型 SQLNVARCHARMAX，之前的版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 傳回<br /> 1989-02-01 00:00:00.<br />OLE DB 驅動程式的 SQL Server 傳回 <br />1989-02-01 00:00:00.0000000。|  
|使用 BCP API 的自訂應用程式現在可以看到警告。|如果資料長度大於所有類型之欄位所指定的長度，BCP API 將會產生一則警告訊息。 之前這個警告只針對字元類型來提供，但是將不會針對所有類型發出。|  
|將空字串插入**sql_variant**繫結為日期/時間類型會產生錯誤。|在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 9.0 中，將空字串插入**sql_variant**繫結為日期/時間類型不會產生錯誤。 OLE DB 驅動程式的 SQL Server 會在此情況下，正確地產生錯誤。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能會在觸發程序執行時傳回不同的結果。|中導入變更[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]可能會導致應用程式有不同的結果造成觸發程序時要執行的陳述式所傳回**NOCOUNT OFF**作用中。 在此狀況下，您的應用程式可能會產生錯誤。 若要解決這個錯誤，將**NOCOUNT ON**觸發程序。|  

## <a name="see-also"></a>另請參閱   
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)
