---
title: 檢視表 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], about views
ms.assetid: ada83c28-e8b7-45d9-b53c-b3d67c8820c8
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e4d6f376e98a032ad9f0680f92624562fdc35176
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566252"
---
# <a name="views"></a>檢視
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
  檢視表是一種虛擬資料表，是由查詢定義其內容。 與資料表類似，檢視表是由一組具名資料行和資料列所組成。 除了索引檢視以外，檢視在資料庫中並沒有儲存的資料值集。 資料的資料列與資料行是從定義檢視的查詢所參考的資料表而來，而且在參考檢視時不會動態產生。  
  
 檢視是做為檢視中所參考的基礎資料表上的篩選。 定義檢視的查詢可以從一或多個資料表而來，或從目前或其他資料庫中的其他檢視而來。 分散式查詢也可用以定義使用多個異質性來源之資料的檢視。 例如，如果您想結合不同伺服器的相似結構資料，每一個伺服器儲存著組織中不同區域的資料，這將非常有用。  
  
 檢視表的功能一般是用來對焦 (Focus)、簡化和自訂每位使用者查看資料庫的角度。 檢視也可以做為安全機制，讓使用者只可透過檢視來存取資料，而無法直接存取檢視的基底資料表。 檢視可以用來提供回溯相容介面，以模擬已存在但其結構描述已變更的資料表。 當您將資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 及從中複製資料時，也可以使用檢視表，來提高效能及分割資料。  
  
## <a name="types-of-views"></a>檢視表的類型  
 除了基本使用者定義檢視表的標準角色之外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還提供資料庫中具有特殊用途的下列檢視表類型。  
  
 索引檢視表  
 索引檢視表是已具體化的檢視。 這表示已計算檢視表定義，而且產生的資料會像資料表一樣儲存。 若要索引檢視表，就必須在該檢視表上建立唯一叢集索引。 索引檢視表可以大幅改善某些查詢類型的效能。 索引檢視最適用於彙總許多資料列的查詢。 它們不適用於經常更新的基礎資料集。  
  
 分割區檢視  
 資料分割檢視會水平聯結一個或多個伺服器上一組成員資料表的分割資料。 這可讓顯示的資料好像源自於一個資料表。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相同執行個體上聯結成員資料表的檢視是本機資料分割檢視。  
  
 系統檢視表  
 系統檢視表會公開目錄中繼資料。 您可以使用系統檢視表來傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或此執行個體中所定義物件的詳細資訊。 例如，您可以查詢 sys.databases 目錄檢視，以傳回執行個體中可用的使用者定義資料庫的詳細資訊。 如需詳細資訊，請參閱[系統檢視 &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)。  
  
## <a name="common-view-tasks"></a>一般檢視工作  
 下表提供與建立或修改檢視相關聯之一般工作的連結。  
  
|檢視工作|主題|  
|----------------|-----------|  
|描述如何建立檢視表。|[建立檢視表](../../relational-databases/views/create-views.md)|  
|描述如何建立索引檢視表。|[建立索引檢視表](../../relational-databases/views/create-indexed-views.md)|  
|描述如何修改檢視表定義。|[修改檢視表](../../relational-databases/views/modify-views.md)|  
|描述如何透過檢視表修改資料。|[透過檢視表修改資料](../../relational-databases/views/modify-data-through-a-view.md)|  
|描述如何刪除檢視表。|[刪除檢視表](../../relational-databases/views/delete-views.md)|  
|描述如何傳回檢視表 (例如檢視表定義) 的詳細資訊。|[取得檢視表的資訊](../../relational-databases/views/get-information-about-a-view.md)|  
|描述如何重新命名檢視表。|[重新命名檢視表](../../relational-databases/views/rename-views.md)|  
  
## <a name="see-also"></a>另請參閱  
 [建立 XML 資料行的檢視表](../../relational-databases/xml/create-views-over-xml-columns.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)  
  
  
