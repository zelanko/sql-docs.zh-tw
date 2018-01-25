---
title: "SQL Server Native Client 中的疏鬆資料行支援 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 541c38e37a581c929da8ca3185b39fbaef065b92
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>SQL Server Native Client 中的疏鬆資料行支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 支援疏鬆資料行。 如需有關疏鬆資料行中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請參閱[使用疏鬆資料行](../../../relational-databases/tables/use-sparse-columns.md)和[使用資料行集](../../../relational-databases/tables/use-column-sets.md)。  
  
 如需有關疏鬆資料行支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，請參閱[疏鬆資料行支援 &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)和[疏鬆資料行支援 &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)。  
  
 如需示範這項功能的範例應用程式資訊，請參閱[SQL Server 資料程式設計範例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>疏鬆資料行與 SQL Server Native Client 的使用者案例  
 下表針對包含疏鬆資料行的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用者摘要一般使用者案例：  
  
|狀況|行為|  
|--------------|--------------|  
|**選取\*從資料表**或 iopenrowset:: Openrowset。|傳回所有資料行不屬於疏鬆**column_set**，再加上包含屬於疏鬆的所有非 null 資料行的值的 XML 資料行**column_set**。|  
|依名稱參考資料行。|可以參考資料行，而不論其疏鬆資料行狀態或**column_set**成員資格。|  
|存取**column_set**成員透過計算 XML 資料行的資料行。|成員的疏鬆資料行**column_set**可以透過選取**column_set**依名稱還可以具有值插入和更新的更新中的 XML **column_set**資料行。<br /><br /> 值必須符合的結構描述**column_set**資料行。|  
|擷取資料行搜尋模式 NULL 或 '%' (ODBC); 透過 SQLColumns 的資料表中的所有資料行的中繼的資料或透過沒有資料行限制 (OLE DB) 的 DBSCHEMA_COLUMNS 結構描述資料列集。|傳回一個資料列的所有資料行不屬於**column_set**。 如果資料表包含疏鬆**column_set**，它會傳回一個資料列。<br /><br /> 請注意這不會傳回成員的資料行的中繼資料**column_set**。|  
|擷取中繼資料的所有資料行，不論疏鬆度或成員資格**column_set**。 這可能會傳回非常大量的資料列。|描述項欄位 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_EXTENDED，然後呼叫[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC)。<br /><br /> Idbschemarowset:: Getrowset 呼叫 DBSCHEMA_COLUMNS_EXTENDED 結構描述資料列集 (OLE DB)。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以直接查詢系統檢視表。|  
|擷取中繼資料，只對成員的資料行**column_set**。 這可能會傳回非常大量的資料列。|設定描述項欄位 sql_sopt_ss_name_scope 設定為 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 而且呼叫 SQLColumns (ODBC)。<br /><br /> Idbschemarowset:: Getrowset 呼叫 DBSCHEMA_SPARSE_COLUMN_SET 結構描述資料列集 (OLE DB)。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以查詢系統檢視。|  
|決定資料行是否為疏鬆。|請參閱 SQLColumns 結果集 (ODBC) 的 SS_IS_SPARSE 資料行。<br /><br /> 查閱 DBSCHEMA_COLUMNS 結構描述資料列集 (OLE DB) 的 SS_IS_SPARSE 資料行。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以查詢系統檢視。|  
|判斷資料行是否為**column_set**。|請參閱 SQLColumns 結果集的 SS_IS_COLUMN_SET 資料行。 或者，查閱 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專屬的資料行屬性 SQL_CA_SS_IS_COLUMN_SET (ODBC)。<br /><br /> 查閱 DBSCHEMA_COLUMNS 結構描述資料列集的 SS_IS_COLUMN_SET 資料行。 或者，查閱*dwFlags* icolumnsinfo:: Getcolumninfo 或 DBCOLUMNFLAGS 中 icolumnsrowset:: Getcolumnsrowset 所傳回的資料列集傳回。 如**column_set**資料行，將會設定 DBCOLUMNFLAGS_SS_ISCOLUMNSET (OLE DB)。<br /><br /> 此案例不可能來自使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前版本之 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 的應用程式。 不過，這類應用程式可以查詢系統檢視。|  
|匯入和匯出不含資料表在 bcp 的疏鬆資料行**column_set**。|從舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 開始，沒有行為上的變更。|  
|匯入和匯出的資料表在 bcp 的疏鬆資料行**column_set**。|**Column_set**是匯入和匯出成 XML; 相同的方式也就是為**varbinary （max)**如果繫結為二進位的型別，或**nvarchar （max)**如果繫結為**char**或**wchar**型別。<br /><br /> 成員的疏鬆資料行**column_set**不會匯出為不同的資料行; 它們只匯出的值中**column_set**。|  
|**queryout** BCP 的行為。|從舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 開始，在明確具名的資料行處理上沒有變更。<br /><br /> 與包含不同結構描述之資料表間匯入和匯出相關的案例可能需要特殊處理。<br /><br /> 如需有關 BCP 的詳細資訊，請參閱本主題稍後的「疏鬆資料行的大量複製 (BCP) 支援」。|  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 下層用戶端將會傳回只對不屬於疏鬆的資料行的中繼資料**column_set** SQLColumns 和 DBSCHMA_COLUMNS。 中導入其他 OLE DB 結構描述資料列[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]原生用戶端將無法使用，也不會在透過 SQL_SOPT_SS_NAME_SCOPE ODBC SQLColumns 的修改。  
  
 下層用戶端可以存取屬於疏鬆資料行**column_set**名稱，而**column_set**當做 XML 資料行仍可從資料行[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]用戶端。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>疏鬆資料行的大量複製 (BCP) 支援  
 沒有 ODBC 或 OLE DB 中的 BCP api 變更的疏鬆資料行或**column_set**功能。  
  
 如果資料表有**column_set**，疏鬆資料行不當做不同的資料行處理。 值中包含的所有疏鬆資料行值**column_set**，其匯出方式與相同的 XML 資料行; 也就是做為**varbinary （max)**如果繫結為二進位的型別，或**nvarchar （max)**如果繫結為**char**或**wchar**類型)。 在匯入時， **column_set**值必須符合的結構描述**column_set**。  
  
 如**queryout**作業，以處理明確參考之資料行的方式沒有變更。 **column_set**資料行有相同的行為與 XML 資料行而且疏鬆度對於不會影響處理的具名疏鬆資料行。  
  
 不過，如果**queryout**使用的匯出，而且您參考疏鬆資料行成員的疏鬆資料行依名稱設定，您不能執行直接匯入結構類似的資料表。 這是因為 BCP 會使用與一致的中繼資料**選取\***匯入作業，且無法符合**column_set**成員資料行與此中繼資料。 若要匯入**column_set**成員資料行必須定義的檢視參考所需的資料表上的個別**column_set**資料行，而且您必須執行匯入作業使用的檢視。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
