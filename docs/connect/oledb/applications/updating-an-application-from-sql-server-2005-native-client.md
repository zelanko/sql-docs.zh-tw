---
title: 從 SQL Server 2005 Native Client 更新應用程式 | Microsoft Docs
description: 從 SQL Server 2005 Native Client 更新應用程式
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7915b9fb74f05057e05eef022d7f9b0e4ccdd21f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989254"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>從 SQL Server 2005 Native Client 更新應用程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本主題討論自 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 起，OLE DB Driver for SQL Server 中的重大變更。  

 當您從 Microsoft Data Access Components (MDAC) 升級為 OLE DB Driver for SQL Server 時，可能也會看見一些行為差異。 如需詳細資訊，請參閱[將應用程式從 MDAC 更新為 OLE DB Driver for SQL Server](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 隨附於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 隨附於 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 隨附於 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 隨附於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。  

|與 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 相比，OLE DB Driver for SQL Server 中已變更的行為|描述|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 只會填補至定義的小數位數。|如果轉換作業會將轉換的資料傳送給伺服器，OLE DB Driver for SQL Server 最多只會在資料中用尾端零填滿至 **datetime** 值的最大長度。 SQL Server Native Client 9.0 則會填滿至 9 位數。|  
|驗證 ICommandWithParameter::SetParameterInfo 的 DBTYPE_DBTIMESTAMP。|OLE DB Driver for SQL Server 會在 ICommandWithParameter::SetParameterInfo 中實作 *bScale* 的 OLE DB 需求，以設定為 DBTYPE_DBTIMESTAMP 的小數秒精確度。|  
|**sp_columns** 預存程序現在會針對 IS_NULLABLE 資料行傳回 **"NO"** ，而非 **"NO "** 。|在 OLE DB Driver for SQL Server 中，**sp_columns** 預存程序現在會針對 IS_NULLABLE 資料行傳回 **"NO"** ，而非 **"NO "** 。|  
|當日期超出範圍時傳回不同錯誤。|若是 **datetime** 類型，OLE DB Driver for SQL Server 將會針對超出範圍的日期傳回與舊版不同的錯誤號碼。<br /><br /> 具體而言，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 會針對轉換為 **datetime** 之字串內所有超出範圍的年份值傳回 22007，而 OLE DB Driver for SQL Server 則會在日期位於 **datetime2** 支援的範圍內但是超出 **datetime** 或 **smalldatetime** 支援的範圍時，傳回 22008。|  
|**datetime** 值會截斷小數秒且不會四捨五入 (如果四捨五入會改變日期的話)。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，傳送給伺服器之 **datetime** 值的用戶端行為是要四捨五入到最接近的 1/300 秒。 在 OLE DB Driver for SQL Server 中，如果四捨五入會改變日期，這個情況會造成小數秒遭到截斷。|  
|可能會截斷 **datetime** 值的秒數。|如果您繫結至類型識別碼為 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC) 且小數位數為 0 的 datetime 資料行，則使用 OLE DB Driver for SQL Server 建置並且連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 伺服器的應用程式，將會截斷傳送至伺服器的資料中時間部分的秒和小數秒。<br /><br /> 例如：<br /><br /> 輸入資料：1994-08-21 21:21:36.000<br /><br /> 插入的資料：1994-08-21 21:21:00.000|  
|從 DBTYPE_DBTIME 轉換成 DBTYPE_DATE 的 OLE DB 資料轉換作業不會再造成日期變更。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的時間部分在午夜的半秒鐘之內，OLE DB 轉換程式碼會造成日期變更。 在 OLE DB Driver for SQL Server 中，日期將不會變更 (小數秒會遭到截斷，而且不會四捨五入)。|  
|IBCPSession::BCColFmt 轉換變更。|在 OLE DB Driver for SQL Server 中，當您使用 IBCPSession::BCOColFmt 將 SQLDATETIME 或 SQLDATETIME 轉換成字串類型時，會匯出小數值。 例如，將 SQLDATETIME 類型轉換成 SQLNVARCHARMAX 類型時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前的版本會傳回<br /> 1989-02-01 00:00:00。<br />OLE DB Driver for SQL Server 會傳回 <br />1989-02-01 00:00:00.0000000。|  
|使用 BCP API 的自訂應用程式現在可以看到警告。|如果資料長度大於所有類型之欄位所指定的長度，BCP API 將會產生一則警告訊息。 之前這個警告只針對字元類型來提供，但是將不會針對所有類型發出。|  
|將空字串插入繫結為日期/時間類型的 **sql_variant** 中會產生錯誤。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，將空字串插入繫結為日期/時間類型的 **sql_variant** 中並不會產生錯誤。 OLE DB Driver for SQL Server 在這種情況下會正確地產生錯誤。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能會在觸發程序執行時傳回不同的結果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中導入的變更可能會使得應用程式從陳述式中傳回不同的結果，該陳述式會在 **NOCOUNT OFF** 有效時造成觸發程序的執行。 在此狀況下，您的應用程式可能會產生錯誤。 若要解決這個錯誤，請在觸發程序中設定 **NOCOUNT ON**。|  

## <a name="see-also"></a>另請參閱   
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)
