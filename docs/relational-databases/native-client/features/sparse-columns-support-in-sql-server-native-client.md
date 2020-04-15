---
title: SQL 本機客戶端的稀疏列支援
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 958424a4710b76e7e09ae15e10b612630f09eee3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303776"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>SQL Server Native Client 中的疏鬆資料行支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支援疏鬆資料行。 如需有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中疏鬆資料行的詳細資訊，請參閱[使用疏鬆資料行](../../../relational-databases/tables/use-sparse-columns.md)和[使用資料行集](../../../relational-databases/tables/use-column-sets.md)。  
  
 有關本機客戶端[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的 稀疏列支援的詳細資訊,請參閱[稀疏列支援&#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)和[稀疏列支援&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)。  
  
 如需示範這項功能之範例應用程式的詳細資訊，請參閱 [SQL Server 資料程式設計範例](https://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>疏鬆資料行與 SQL Server Native Client 的使用者案例  
 下表針對包含疏鬆資料行的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用者摘要一般使用者案例：  
  
|狀況|行為|  
|--------------|--------------|  
|**從資料表**或 IOpenRowset::OpenRowset 選取 \*。|傳回不屬於疏鬆 **column_set** 成員的所有資料行，加上包含屬於疏鬆 **column_set** 成員之所有非 Null 資料行值的 XML 資料行。|  
|依名稱參考資料行。|不管其疏鬆資料行狀態或 **column_set** 成員資格，都可以參考資料行。|  
|透過計算 XML 資料行，存取 **column_set** 成員資料行。|屬於疏鬆 **column_set** 成員的資料行可以透過依名稱選取 **column_set** 來存取，而且可以透過更新 **column_set** 資料行中的 XML 來插入和更新值。<br /><br /> 這個值必須符合 **column_set** 資料行的結構描述。|  
|透過 SQLColumn 檢索表中所有列的中繼資料,列搜尋模式為 NULL 或"%" (ODBC);或通過沒有列限制(OLE DB)的DBSCHEMA_COLUMNS架構行集。|傳回不屬於疏鬆 **column_set** 成員之所有資料行的資料列。 如果資料表包含疏鬆 **column_set**，將會針對該資料表傳回一個資料列。<br /><br /> 請注意，這不會針對屬於 **column_set** 成員的資料行傳回中繼資料。|  
|不管 **column_set** 中的疏鬆度或成員資格，擷取所有資料行的中繼資料。 這可能會傳回非常大量的資料列。|將描述符位SQL_SOPT_SS_NAME_SCOPE設定為SQL_SS_NAME_SCOPE_EXTENDED並調用[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC)。<br /><br /> 呼叫 IDB 架構羅資料集::取得DBSCHEMA_COLUMNS_EXTENDED架構列集 (OLE DB) 的 Rowset。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以直接查詢系統檢視。|  
|僅針對屬於 **column_set** 成員的資料行擷取中繼資料。 這可能會傳回非常大量的資料列。|將描述符位SQL_SOPT_SS_NAME_SCOPE設定為SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET並調用 SQLColumns (ODBC)。<br /><br /> 調用 IDB 架構羅資料集::獲取DBSCHEMA_SPARSE_COLUMN_SET架構列集(OLE DB)的獲取羅資料集。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以查詢系統檢視。|  
|決定資料行是否為疏鬆。|請參閱 SQLColumn 結果集 (ODBC) 的SS_IS_SPARSE列。<br /><br /> 查閱 DBSCHEMA_COLUMNS 結構描述資料列集 (OLE DB) 的 SS_IS_SPARSE 資料行。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以查詢系統檢視。|  
|判斷資料行是否為 **column_set**。|請參閱 SQLColumn 結果集的SS_IS_COLUMN_SET列。 或者，查閱 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專屬的資料行屬性 SQL_CA_SS_IS_COLUMN_SET (ODBC)。<br /><br /> 查閱 DBSCHEMA_COLUMNS 結構描述資料列集的 SS_IS_COLUMN_SET 資料行。 或者，查閱 IColumnsRowset::GetColumnsRowset 所傳回的資料列集中 IColumnsinfo::GetColumnInfo 或 DBCOLUMNFLAGS 傳回的 *dwFlags*。 對於**column_set**列,將設置DBCOLUMNFLAGS_SS_ISCOLUMNSET(OLE DB)。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以查詢系統檢視。|  
|針對沒有 **column_set** 的資料表，依 BCP 匯入和匯出疏鬆資料行。|從舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 開始，沒有行為上的變更。|  
|針對包含 **column_set** 的資料表，依 BCP 匯入和匯出疏鬆資料行。|**column_set** 的匯入和匯出方式與 XML 相同；也就是說，如果當作二進位類型繫結，如同 **varbinary(max)**，或者，如果當作 **char** 或 **wchar** 類型繫結，則如同 **nvarchar(max)**。<br /><br /> 屬於疏鬆 **column_set** 成員的資料行不會匯出為不同的資料行；它們只會在 **column_set** 的值中匯出。|  
|BCP 的 **queryout** 行為。|從舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 開始，在明確具名的資料行處理上沒有變更。<br /><br /> 與包含不同結構描述之資料表間匯入和匯出相關的案例可能需要特殊處理。<br /><br /> 如需有關 BCP 的詳細資訊，請參閱本主題稍後的「疏鬆資料行的大量複製 (BCP) 支援」。|  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 下層用戶端僅會針對不屬於 SQLColumns 和 DBSCHMA_COLUMNS 之疏鬆 **column_set** 成員的資料行傳回中繼資料。 本機用戶端中[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]引入的其他 OLE DB 架構列集將不可用,也無法通過SQL_SOPT_SS_NAME_SCOPE對 ODBC 中的 SQLColumns 進行修改。  
  
 下層用戶端可以依名稱存取屬於疏鬆 **column_set** 成員的資料行，而且 **column_set** 資料行將可以存取 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 用戶端的 XML 資料行。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>疏鬆資料行的大量複製 (BCP) 支援  
 對於稀疏列或**column_set**功能,在 ODBC 或 OLE DB 中對 BCP API 沒有更改。  
  
 如果某個資料表包含 **column_set**，則不會將疏鬆資料行當作不同的資料行處理。 所有疏鬆資料行的值都包含在 **column_set** 的值中，其匯出方式與 XML 資料行相同，也就是說，如果當作二進位類型繫結，如同 **varbinary(max)**，或者，如果當作 **char** 或 **wchar** 類型繫結，則如同 **nvarchar(max)**。 匯入時，**column_set** 值必須符合 **column_set** 的結構描述。  
  
 針對 **queryout** 作業，不會變更處理明確參考之資料行的方式。 **column_set** 資料行的行為與 XML 資料行相同，而且疏鬆度對於具名疏鬆資料行的處理沒有作用。  
  
 不過，如果 **queryout** 用於匯出，而且您參考的疏鬆資料行屬於依名稱設定之疏鬆資料行集的成員，則您無法直接匯入結構類似的資料表。 這是因為 BCP 使用與**導入的選定&#42;** 操作一致的元數據,並且無法**將column_set**成員列與此元數據匹配。 若要個別匯入 **column_set** 成員資料行，您必須在資料表上定義參考所需 **column_set** 資料行的檢視表，而且您必須使用檢視表執行匯入作業。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
