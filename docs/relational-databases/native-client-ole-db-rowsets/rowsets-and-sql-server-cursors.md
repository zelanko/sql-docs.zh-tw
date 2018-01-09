---
title: "資料列集和 SQL Server 資料指標 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- OLE DB rowsets, cursors
- SQL Server Native Client OLE DB provider, rowsets
- rowsets [OLE DB], cursors
- properties [OLE DB]
- cursors [OLE DB]
ms.assetid: 26a11e26-2a3a-451e-8f78-fba51e330ecb
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e0546fe394d34b9a06bed38b0277192ca8f9ff8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="rowsets-and-sql-server-cursors"></a>資料列集和 SQL Server 資料指標
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用兩個方法將結果集傳回給取用者：  
  
-   具有以下功能的預設結果集：  
  
    -   將負擔最小化。  
  
    -   在提取資料時提供最大效能。  
  
    -   只支援預設的順向、唯讀資料指標功能。  
  
    -   一次將一個資料列傳回給取用者。  
  
    -   一次只支援連接上有一個作用中陳述式。  
  
         在執行陳述式之後，要等到取用者已經擷取所有結果或是陳述式已被取消之後，才可以在連接上執行其他陳述式。  
  
    -   支援所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   具有以下功能的伺服器資料指標：  
  
    -   支援所有的資料指標功能。  
  
    -   可以將資料列區塊傳回給取用者。  
  
    -   支援單一連接上有多個作用中陳述式。  
  
    -   平衡資料指標功能與效能。  
  
         資料指標功能的支援會減少相對於預設結果集的效能。 如果取用者可以使用資料指標功能來擷取較小的資料列集，就可以抵銷這個作用。  
  
    -   請勿支援會傳回單一結果集以上的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
 取用者可藉由設定某些資料列集屬性，在資料列集中要求不同的資料指標行為。 如果取用者未設定任何一個資料列集屬性，或將它們設定為其預設值，所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會實作使用預設結果集的資料列集。 如果任何一個屬性設為預設值以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會實作使用伺服器資料指標的資料列集。  
  
 下列資料列集屬性會指引 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標。 某些屬性可以安全地與其他屬性合併在一起。 例如，顯示 DBPROP_IRowsetScroll 和 DBPROP_IRowsetChange 屬性的資料列集將會是一個顯示立即更新行為的書籤資料列集。 其他屬性互斥。 例如，顯示 DBPROP_OTHERINSERT 的資料列集不能包含書籤。  
  
|屬性識別碼|ReplTest1|資料列集行為|  
|-----------------|-----------|---------------------|  
|DBPROP_SERVERCURSOR|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 資料列集是循序的，只支援順向捲動和提取。 支援相對資料列定位。 命令文字可以包含 ORDER BY 子句。|  
|DBPROP_CANSCROLLBACKWARDS 或 DBPROP_CANFETCHBACKWARDS|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集支援一個方向的捲動和提取。 支援相對資料列定位。 命令文字可以包含 ORDER BY 子句。|  
|DBPROP_BOOKMARKS 或 DBPROP_LITERALBOOKMARKS|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 資料列集是循序的，只支援順向捲動和提取。 支援相對資料列定位。 命令文字可以包含 ORDER BY 子句。|  
|DBPROP_OWNUPDATEDELETE 或 DBPROP_OWNINSERT 或 DBPROP_OTHERUPDATEDELETE|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集支援一個方向的捲動和提取。 支援相對資料列定位。 命令文字可以包含 ORDER BY 子句。|  
|DBPROP_OTHERINSERT|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集支援一個方向的捲動和提取。 支援相對資料列定位。 如果參考的資料行上有索引存在，命令文字可以包含 ORDER BY 子句。<br /><br /> 如果資料列集包含書籤，DBPROP_OTHERINSERT 不能為 VARIANT_TRUE。 嘗試建立具有這個可見性屬性和書籤的資料列集會產生錯誤。|  
|DBPROP_IRowsetLocate 或 DBPROP_IRowsetScroll|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集支援一個方向的捲動和提取。 書籤和絕對定位透過**IRowsetLocate**介面中的資料列集支援。 命令文字可以包含 ORDER BY 子句。<br /><br /> DBPROP_IRowsetLocate 和 DBPROP_IRowsetScroll 需要資料列集中的書籤。 嘗試建立具有書籤且將 DBPROP_OTHERINSERT 設定為 VARIANT_TRUE 的資料列集會產生錯誤。|  
|DBPROP_IRowsetChange 或 DBPROP_IRowsetUpdate|VARIANT_TRUE|可以透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 資料列集是循序的，只支援順向捲動和提取。 支援相對資料列定位。 支援可更新之資料指標的所有命令都可支援這些介面。|  
|DBPROP_IRowsetLocate 或 DBPROP_IRowsetScroll 及 DBPROP_IRowsetChange 或 DBPROP_IRowsetUpdate|VARIANT_TRUE|可以透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集支援一個方向的捲動和提取。 書籤和絕對定位透過**IRowsetLocate**中資料列集支援。 命令文字可以包含 ORDER BY 子句。|  
|DBPROP_IMMOBILEROWS|VARIANT_FALSE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集只支援順向捲動。 支援相對資料列定位。 如果參考的資料行上有索引存在，命令文字可以包含 ORDER BY 子句。<br /><br /> 只有當資料列集可以顯示其他工作階段上的命令所插入或其他使用者所插入的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料列時，才能在資料列集中使用 DBPROP_IMMOBILEROWS。 嘗試在 DBPROP_OTHERINSERT 不能是 VARIANT_TRUE 的任何資料列集上開啟此屬性設定為 VARIANT_FALSE 的資料列集時，將會產生錯誤。|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|無法透過資料列集來更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料。 此資料列集只支援順向捲動。 支援相對資料列定位。 命令文字可以包含 ORDER BY 子句 (除非由另一個屬性所限制)。|  
  
 A[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上可以輕鬆地建立 Native Client OLE DB 提供者資料列集支援伺服器資料指標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]基底資料表或檢視使用**iopenrowset:: Openrowset**方法。 依名稱指定資料表或檢視表，傳遞所需的資料列集屬性會設定*rgPropertySets*參數。  
  
 當取用者要求伺服器資料指標支援資料列集時，建立此資料列集的命令文字會受到限制。 具體而言，命令文字會受限為傳回單一資料列集結果的單一 SELECT 陳述式，或是實作單一 SELECT 陳述式來傳回單一資料列集結果的預存程序。  
  
 這兩個表會顯示各種 OLE DB 屬性和資料指標模型的對應。 也會顯示應該設定哪些資料列集屬性來使用某種類型的資料指標模型。  
  
 表中的每一個資料格都包含特定資料指標模型的資料列集屬性值。 本主題稍早所列之所有資料列集屬性的資料類型為 VT_BOOL，而且預設值為 VARIANT_FALSE。 下表將使用下列符號。  
  
 F = 預設值 (VARIANT_FALSE)  
  
 T = VARIANT_TRUE  
  
 \-= VARIANT_TRUE 或 VARIANT_FALSE  
  
 若要使用某種類型的資料指標模型，請找出對應至此資料指標模型的資料行，並尋找此資料行中具有 'T' 值的所有資料列集屬性。 將這些資料列集屬性設定為 VARIANT_TRUE，以便使用特定的資料指標模型。 具有 '-' 值的資料列集屬性可以設定為 VARIANT_TRUE 或 VARIANT_FALSE。  
  
|資料列集屬性/資料指標模型|預設<br /><br /> result<br /><br /> 集合<br /><br /> (RO)|快速<br /><br /> 順<br /><br /> 向<br /><br /> (RO)|靜態<br /><br /> (RO)|索引鍵集<br /><br /> 驅動<br /><br /> (RO)|  
|--------------------------------------|-------------------------------------------|--------------------------------------------|-----------------------|----------------------------------|  
|DBPROP_SERVERCURSOR|F|T|T|T|  
|DBPROP_DEFERRED|F|F|-|-|  
|DBPROP_IrowsetChange|F|F|F|F|  
|DBPROP_IrowsetLocate|F|F|-|-|  
|DBPROP_IrowsetScroll|F|F|-|-|  
|DBPROP_IrowsetUpdate|F|F|F|F|  
|DBPROP_BOOKMARKS|F|F|-|-|  
|DBPROP_CANFETCHBACKWARDS|F|F|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|F|F|-|-|  
|DBPROP_CANHOLDROWS|F|F|-|-|  
|DBPROP_LITERALBOOKMARKS|F|F|-|-|  
|DBPROP_OTHERINSERT|F|T|F|F|  
|DBPROP_OTHERUPDATEDELETE|F|T|F|T|  
|DBPROP_OWNINSERT|F|T|F|T|  
|DBPROP_OWNUPDATEDELETE|F|T|F|T|  
|DBPROP_QUICKSTART|F|F|-|-|  
|DBPROP_REMOVEDELETED|F|F|F|-|  
|DBPROP_IrowsetResynch|F|F|F|-|  
|DBPROP_CHANGEINSERTEDROWS|F|F|F|F|  
|DBPROP_SERVERDATAONINSERT|F|F|F|-|  
|DBPROP_UNIQUEROWS|-|F|F|F|  
|DBPROP_IMMOBILEROWS|-|-|-|T|  
  
|資料列集屬性/資料指標模型|動態 (RO)|索引鍵集 (R/W)|動態 (R/W)|  
|--------------------------------------|--------------------|---------------------|----------------------|  
|DBPROP_SERVERCURSOR|T|T|T|  
|DBPROP_DEFERRED|-|-|-|  
|DBPROP_IrowsetChange|F|-|-|  
|DBPROP_IrowsetLocate|F|-|F|  
|DBPROP_IrowsetScroll|F|-|F|  
|DBPROP_IrowsetUpdate|F|-|-|  
|DBPROP_BOOKMARKS|F|-|F|  
|DBPROP_CANFETCHBACKWARDS|-|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|-|-|-|  
|DBPROP_CANHOLDROWS|F|-|F|  
|DBPROP_LITERALBOOKMARKS|F|-|F|  
|DBPROP_OTHERINSERT|T|F|T|  
|DBPROP_OTHERUPDATEDELETE|T|T|T|  
|DBPROP_OWNINSERT|T|T|T|  
|DBPROP_OWNUPDATEDELETE|T|T|T|  
|DBPROP_QUICKSTART|-|-|-|  
|DBPROP_REMOVEDELETED|T|-|T|  
|DBPROP_IrowsetResynch|-|-|-|  
|DBPROP_CHANGEINSERTEDROWS|F|-|F|  
|DBPROP_SERVERDATAONINSERT|F|-|F|  
|DBPROP_UNIQUEROWS|F|F|F|  
|DBPROP_IMMOBILEROWS|F|T|F|  
  
 如果是特定的一組資料列集屬性，將會依照以下方式決定所選取的資料指標模型。  
  
 請從指定的資料列集屬性集合中，取得上述表格中所列之屬性的子集。 根據每一個資料列集屬性的旗標值，將這些屬性分成兩個子群組：必要 (T、F) 或選擇性 (-)。 對於每一個資料指標模型而言，請從第一個表開始，然後從左到右移動，並將這兩個子群組中的屬性值與該資料行內的對應屬性值相比較。 如果資料指標模型沒有任何項目符合必要屬性，而且不符合選擇性屬性的數目最少，則會選取該資料指標模型。 如果有一個以上的資料指標模型，則會選擇最左邊。  
  
## <a name="sql-server-cursor-block-size"></a>SQL Server 資料指標區塊大小  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料指標支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料列集的資料列中的項目數的控制代碼陣列參數的**irowset:: Getnextrows**或**irowsetlocate:: Getrowsat**方法定義的資料指標區塊大小。 此陣列中控制代碼所指示的資料列為資料指標區塊的成員。  
  
 支援書籤的資料列集，資料列控制代碼擷取使用**irowsetlocate:: Getrowsbybookmark**方法定義的資料指標區塊的成員。  
  
 不論用來擴展資料列集及形成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標區塊的方法為何，在資料列集上執行下一個資料列提取方法之前，資料指標區塊都是使用中狀態。  
  
## <a name="see-also"></a>請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
