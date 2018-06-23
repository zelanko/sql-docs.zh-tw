---
title: 參數化資料列篩選 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], dynamic filters
- merge replication [SQL Server replication], dynamic filters
- parameterized filters [SQL Server replication]
- filters [SQL Server replication], dynamic
- merge replication parameterized filters [SQL Server replication]
- publications [SQL Server replication], parameterized filters
- parameterized filters [SQL Server replication], about parameterized filters
- filters [SQL Server replication], parameterized
- dynamic filters [SQL Server replication]
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
caps.latest.revision: 68
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 74cb3cd9631e0b709b7eb5cf0cb0856bc3b830af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034123"
---
# <a name="parameterized-row-filters"></a>Parameterized Row Filters
  參數化資料列篩選允許將不同的資料分割傳送到不同的訂閱者，而不需要建立多個發行集 (參數化篩選在舊版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中稱為動態篩選)。 資料分割是資料表中資料列的子集；根據建立參數化資料列篩選時選取的設定，已發行資料表中的每個資料列可僅屬於一個資料分割 (產生不重疊資料分割)，也可屬於兩個或兩個以上的資料分割 (產生重疊資料分割)。  
  
 不重疊資料分割可以在訂閱之間共用，或限制其僅讓一個訂閱能收到給定資料分割。 本主題之後的「使用適當的篩選選項」一節中會描述控制資料分割行為的設定。 透過使用這些設定，您可以依據應用程式及效能需求量身訂作參數化篩選。 一般來說，重疊資料分割允許較大的彈性，而複寫到單一訂閱的不重疊資料分割則會提供較佳的效能。  
  
 參數化篩選用於單一資料表，通常與聯結篩選組合以將篩選擴充到相關資料表。 如需相關資訊，請參閱 [Join Filters](join-filters.md)。  
  
 若要定義或修改參數化資料列篩選，請參閱＜ [針對合併發行項定義及修改參數化資料列篩選](../publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)＞。  
  
## <a name="how-parameterized-filters-work"></a>參數化篩選如何運作  
 參數化資料列篩選器使用 WHERE 子句選取要發行的適當資料。 您可以指定 SUSER_SNAME() 與 HOST_NAME() 系統函數中的其中之一或兩者，而不要在子句中指定常值 (如同對靜態資料列篩選那樣)。 也可以使用使用者定義函數，但它們必須在函數主體中包含 SUSER_SNAME() 或 HOST_NAME()，或者評估這些系統函數的其中之一 (例如 `MyUDF(SUSER_SNAME()`)。 如果使用者定義函數在函數主體中包含 SUSER_SNAME() 或 HOST_NAME()，則您將無法將參數傳遞到該函數。  
  
 系統函數 SUSER_SNAME() 和 HOST_NAME() 並不是合併式複寫的特定函數，但是可以由合併式複寫用來進行參數化篩選：  
  
-   SUSER_SNAME() 會傳回對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體建立連接的登入資訊。 當用於參數化篩選時，它會傳回「合併代理程式」使用其連接到「發行者」的登入 (建立訂閱時，您會指定一個登入)。  
  
-   HOST_NAME() 傳回連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體的電腦名稱。 當用於參數化篩選時，依預設，該函數會傳回「合併代理程式」執行於其上之電腦的名稱。 對於提取訂閱，它是「訂閱者」的名稱；對於發送訂閱，它是「散發者」的名稱。  
  
     也可以使用「訂閱者」或「散發者」名稱之外的其他值覆寫此函數。 通常，應用程式會使用更有意義的值覆寫此函數，例如業務員的姓名或識別碼。 如需詳細資訊，請參閱本主題中的＜覆寫 HOST_NAME() 值＞一節。  
  
 系統函數傳回的值會與要篩選之資料表中所指定的資料行加以比較，並且適當的資料也會下載到「訂閱者」。 此比較在初始化訂閱 (如此便只有適當的資料才會包含在初始快照集中) 以及每次同步處理訂閱時執行。 依預設，如果發行者端的變更導致資料列從資料分割中移出，則該資料列會在訂閱者端刪除 (此行為可透過使用 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 的 **@allow_partition_realignment** 參數來控制)。  
  
> [!NOTE]  
>  當為參數化篩選執行比較時，會始終使用資料庫定序。 例如，如果資料庫定序不區分大小寫，但資料表或資料行定序區分大小寫，則比較將不區分大小寫。  
  
### <a name="filtering-with-susersname"></a>使用 SUSER_SNAME() 篩選  
 請考慮 **範例資料庫中的** Employee 資料表 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 。 此資料表包括 **LoginID**資料行，其中含有每一位員工的登入，格式為 '*domain\login*'。 若要篩選這個資料表，好讓每一位員工只收到與其相關的資料，請指定以下的篩選子句：  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 例如，其中一位員工的值為 'adventure-works\john5'。 則當「合併代理程式」連接到「發行者」時，它會使用您在建立訂閱時指定的登入 (此狀況中為 'adventure-works\john5')。 「合併代理程式」會將 SUSER_SNAME() 傳回的值與資料表中的值相比較，並僅下載 **LoginID** 資料行中包含值 'adventure-works\john5' 的資料列。  
  
### <a name="filtering-with-hostname"></a>使用 HOST_NAME() 篩選  
 考慮 **HumanResources.Employee** 資料表。 假設此資料表包含一個資料行，如 **ComputerName** ，其中每一位員工的電腦名稱格式為 '*name_computertype*'。 若要篩選這個資料表，好讓每一位員工只收到與其相關的資料，請指定以下的篩選子句：  
  
```  
ComputerName = HOST_NAME()  
```  
  
 例如，其中一位員工的值為 'john5_laptop'。 當「合併代理程式」連接到「發行者」時，它會將 HOST_NAME() 傳回的值與資料表中的值相比較，並僅下載在 **ComputerName** 資料行中包含值 'john5_laptop' 的資料列。  
  
 也可以在一個篩選中合併多個函數。 例如，如果您想確保只有每位員工在各自電腦上使用他們的登入時才會接收資料，則篩選子句會是：  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 除非您正在覆寫 HOST_NAME() 值，否則使用 HOST_NAME() 進行篩選通常僅用於提取訂閱。 該函數傳回的值是「合併代理程式」執行於其上之電腦名稱。 針對提取訂閱，該值對每個訂閱均為不同，但是針對發送訂閱，該值是相同的 (所有「合併代理程式」都在發送訂閱的散發者端執行)。  
  
> [!IMPORTANT]  
>  HOST_NAME() 函數的值可以覆寫；因此不可使用包含 HOST_NAME() 的篩選控制資料分割的存取。 若要控制資料分割的存取，請將 SUSER_SNAME()、SUSER_SNAME() 與 HOST_NAME() 合併使用，或者使用靜態資料列篩選。  
  
#### <a name="overriding-the-hostname-value"></a>覆寫 HOST_NAME() 值  
 如前所述，依預設，HOST_NAME() 會傳回連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體的電腦名稱。 使用參數化篩選時，通常透過建立訂閱時提供一個值來覆寫此值。 HOST_NAME() 函數就會傳回您指定的值，而非電腦的名稱。  
  
> [!NOTE]  
>  如果您覆寫 HOST_NAME()，則所有對 HOST_NAME() 函數的呼叫均會傳回您指定的值。 請確定其他應用程式不會相依於由 HOST_NAME() 傳回電腦名稱。  
  
 考慮 **HumanResources.Employee** 資料表。 此資料表包含資料行 **EmployeeID**。 若要篩選這個資料表，使每個員工只收到與其相關的資料，請指定以下的篩選子句：  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 例如，Pamela Ansman-Wolfe 的員工識別碼已被指派為 280。 當您為此員工建立訂閱時，請將 HOST_NAME() 值指定成員工識別碼的值 (此範例中為 280)。 「合併代理程式」連接到發行者端時，它會將 HOST_NAME() 傳回的值與資料表中的值相比較，並僅下載在 **EmployeeID** 資料行中包含值 280 的資料列。  
  
> [!IMPORTANT]  
>  Host_name （） 函式會傳回`nchar`值，因此您必須使用 CONVERT 如果篩選子句中的資料行的數值資料類型，因為它是在上述範例中。 基於效能的考量，建議您不要在參數化資料列篩選器子句中的資料行名稱套用函數，例如 `CONVERT(nchar,EmployeeID) = HOST_NAME()`。 反之，建議您使用範例中顯示的方法： `EmployeeID = CONVERT(int,HOST_NAME())`。 這個子句可用於**@subset_filterclause**參數[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)，但它通常不能在 「 新增發行集精靈 」 （此精靈會執行篩選子句來進行驗證，這會失敗，因為電腦名稱不能轉換成`int`)。 如果您使用「新增發行集精靈」，建議在此精靈中指定 `CONVERT(nchar,EmployeeID) = HOST_NAME()` ，然後在建立發行集的快照集之前，使用 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) ，將該子句變更為 `EmployeeID = CONVERT(int,HOST_NAME())` 。  
  
 **覆寫 HOST_NAME() 值**  
  
 使用下列方法其中一之來覆寫 HOST_NAME() 值：  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：在 [新增訂閱精靈] 的 [HOST\_NAME\(\) 值] 頁面上指定一個值。 如需建立訂閱的詳細資訊，請參閱[訂閱發行集](../subscribe-to-publications.md)。  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計︰指定 [sp_addmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) (適用於發送訂閱) 或 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) (適用於提取訂閱) 的 **@hostname** 參數值。  
  
-   合併代理程式：在命令列中或透過代理程式設定檔為 **-Hostname** 參數指定一個值。 如需「合併代理程式」的詳細資訊，請參閱＜ [Replication Merge Agent](../agents/replication-merge-agent.md)＞。 如需代理程式設定檔的詳細資訊，請參閱＜ [Replication Agent Profiles](../agents/replication-agent-profiles.md)＞。  
  
## <a name="initializing-a-subscription-to-a-publication-with-parameterized-filters"></a>使用參數化篩選初始化發行集的訂閱  
 在合併發行集內使用參數化資料列篩選器時，覆寫會以兩段式的快照集來初始化每一個訂閱。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
## <a name="using-the-appropriate-filtering-options"></a>使用適當的篩選選項  
 使用參數化篩選時，您要控制的兩個主要方面為：  
  
-   可以透過兩個發行集設定的其中之一，來控制合併式複寫處理篩選的方式： **使用資料分割群組** 和 **保留資料分割變更**。  
  
-   必須透過發行項設定 **資料分割選項**，來反映資料在「訂閱者」之間的共用方式。  
  
 若要設定篩選選項，請參閱＜ [Optimize Parameterized Row Filters](../publish/optimize-parameterized-row-filters.md)＞。  
  
### <a name="setting-use-partition-groups-and-keep-partition-changes"></a>設定使用資料分割群組和保留資料分割變更  
 **使用資料分割群組** 和 **保留資料分割變更** 兩者均可以透過在發行集資料庫中儲存其他中繼資料，提升具有篩選發行項之發行集的同步處理效能。 [使用資料分割群組]  選項可以透過使用預先計算的資料分割功能，讓效能大為提升。 此選項設定為`true`依預設，如果您的發行集中發行項符合一組需求。 如需這些需求的詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](parameterized-filters-optimize-for-precomputed-partitions.md)。 如果您的發行項不符合使用預先計算的資料分割的需求**保留資料分割變更**選項設定為`true`。  
  
### <a name="setting-partition-options"></a>設定資料分割選項  
 依據「訂閱者」共用已篩選資料表中資料之方式，您可以建立發行項時為 **資料分割選項** 屬性指定一個值。 您可以使用 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)、 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)和 **[發行項屬性]** 對話方塊，將這個屬性設為四個值的其中一個。 使用 **[加入篩選]** 或 **[編輯篩選]** 對話方塊 (在「新增發行集精靈」和 **[發行集屬性]** 對話方塊中可用) 可以將屬性設定為兩個值中的其中之一。 下表簡單說明了可用值：  
  
|描述|「加入篩x」和「編輯篩選」中的值|「發行項屬性」中的值|預存程序中的值|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|資料分割中的資料為重疊，「訂閱者」可以更新參數化篩選中參考的資料行。|**這個資料表中的一個資料列會提供給多個訂閱**|**重疊**|**0**|  
|資料分割中的資料為重疊，「訂閱者」不能更新參數化篩選中參考的資料行。|N/A<sup>1</sup>|**重疊，不允許變更資料分割外的資料**|**1**|  
|資料分割中的資料為不重疊，資料在訂閱之間共用。 訂閱者無法更新參數化篩選中參考的資料行。|N/A<sup>1</sup>|**不重疊，共用於訂閱之間**|**2**|  
|資料分割中的資料不重疊，每一資料分割有單一訂閱。 「 訂閱者 」 無法更新參數化篩選中參考的資料行。<sup>2</sup>|**這個資料表中的一個資料列只會提供給一個訂閱**|**不重疊，單一訂閱**|**3**|  
  
 <sup>1</sup>如果基礎篩選選項設定為**0**，或**1**，或**2**、**加入篩選條件**和**編輯篩選**對話方塊會顯示**這個資料表中的資料列會提供給多個訂閱**。  
  
 <sup>2</sup>如果您指定這個選項時，只能有單一訂閱該發行項中的資料每個資料分割。 如果建立第二項訂閱，將新訂閱的篩選準則解析成現有訂閱的相同資料分割，就會卸除現有的訂閱。  
  
> [!IMPORTANT]  
>  **資料分割選項** 值必須依據訂閱者端共享資料的方式設定。 如果您指定資料分割為不重疊且每個資料分割有單一訂閱，但資料此時卻在另一個訂閱者端更新，在此情況下，「合併代理程式」在同步處理過程中可能失敗，並可能發生非聚合。  
  
#### <a name="selecting-the-appropriate-partition-option"></a>選取適當的資料分割選項  
 不重疊資料分割與預先計算資料分割一起使用，以便在某些功能限制可接受狀況下改善效能。 預先計算的資料分割會加速下載至「訂閱者」的動作，但是上傳動作會變慢。 非重疊的資料分割會讓與預先計算之資料分割有關的上傳成本減至最少。 當使用的參數化篩選和聯結篩選越複雜時，非重疊資料分割在效能上的益處更為醒目。  
  
 決定在發行集中使用哪些資料分割選項時，請考慮下列狀況。  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 擁有一支行動銷售團隊，每位業務員負責給定郵遞區號的客戶。 如果客戶從一個銷售領域移到另一個銷售領域時，應用程式會要求更新郵遞區號，以便將該客戶指派給另一位銷售員。 參數化篩選是以客戶的郵遞區號為根據，而更新動作會從一位銷售員的資料分割中移除此郵遞區號，然後將它插入到另一位銷售員的資料分割中。 這要求重疊資料分割具有更新參數化篩選中參考之資料行的能力。 此選項提供最大的彈性，但是其執行效果可能不如非重疊資料分割。  
  
-   職業介紹機構擁有可提供給各縣市之下區域辦事處的資料。 資料不會重疊；該機關總部資料表中的每一資料列都僅包含於一個資料分割中，但是該資料分割可以傳送到同一縣內的多個辦事處。 使用非重疊資料分割選項 (在訂閱之間共用資料分割) 是適當的動作，不但能夠改善重疊資料分割的效能，也會滿足應用程式的需求。  
  
-   如果您擁有不重疊資料分割，且僅有一個訂閱會收到並更新資料分割中的資料，則可以實現進一步的效能優勢。 這種狀況對銷售點系統，以及主要在訂閱者端收集資料，並將其上傳到發行者的現場服務應用程式來說很常見。 請考慮運送應用程式的 **Package** 資料表：每份套裝程式裝入卡車中時，會變更 **Package** 資料表中的套裝程式狀態，並且此變更會複寫回總部。 駕駛員不會在兩輛不同的卡車上更新同一套裝軟體的狀態，因此 **Package** 資料表非常適合做為每個資料分割有單一訂閱的不重疊資料分割。  
  
#### <a name="considerations-for-nonoverlapping-partitions"></a>不重疊資料分割之考量  
 使用不重疊資料分割時，請記住下列考量。  
  
##### <a name="general-considerations"></a>一般考量  
  
-   發行集必須使用預先計算的資料分割。  
  
-   一個資料列必須僅屬於一個資料分割。  
  
-   發行項不能是邏輯記錄的一部分。  
  
-   不支援替代同步夥伴 (此功能已經棄用)。  
  
-   訂閱者無法更新參數化篩選中參考的資料行。  
  
-   如果訂閱者端的插入不屬於資料分割，則它不會被刪除。 但是，它將不會被複寫到其他「訂閱者」。  
  
-   在某些具有重疊資料分割的情況下，會在「合併代理程式」插入資料時調整識別範圍。 在非重疊資料分割中，只能由有權在訂閱資料庫中調整識別範圍的使用者，在插入資料時調整識別範圍。 使用者必須擁有該資料表，或者是 **sysadmin** 固定伺服器角色、 **db_owner** 固定資料庫角色或 **db_ddladmin** 固定資料庫角色的成員。  
  
##### <a name="additional-considerations-for-nonoverlapping-partitions-with-a-single-subscription-per-partition"></a>每個資料分割有單一訂閱的不重疊資料分割之其他考量  
  
-   發行項可以僅存在於一個發行集中；不能重新發行發行項。  
  
-   發行集必須允許「訂閱者」初始化快照集處理。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
##### <a name="additional-considerations-for-join-filters"></a>聯結篩選之其他考量  
  
-   在聯結篩選階層中，有重疊資料分割的發行項無法在有不重疊資料分割之發行項的上方顯示。 換句話說，如果子發行項使用不重疊資料分割，則父發行項也必須如此。 如需聯結篩選的詳細資訊，請參閱＜ [Join Filters](join-filters.md)＞。  
  
-   如果不重疊資料分割在聯結篩選中是子系，則必須將 **聯結唯一索引鍵** 屬性設定為 1。 如需相關資訊，請參閱 [Join Filters](join-filters.md)。  
  
-   發行項應僅含有一個參數化篩選或聯結篩選。 允許含有參數化篩選且在聯結篩選中為父系。 不允許含有參數化篩選且在聯結篩選中為子系。 同樣也不允許有一個以上的聯結篩選。  
  
-   如果發行者端的兩個資料表含有聯結篩選關聯性，且子資料表的某些資料列在父資料表中沒有對應的資料列，則插入遺漏的父資料列不會導致相關資料列被下載到訂閱者 (資料列使用不重疊資料分割下載)。 例如，如果 **SalesOrderDetail** 資料表中的某些資料列在 **SalesOrderHeader** 資料表中沒有對應的資料列，而且您在 **SalesOrderHeader**中插入了該遺漏的資料列，則該資料列會下載到「訂閱者」，但不會下載 **SalesOrderDetail** 中的對應資料列。  
  
## <a name="see-also"></a>另請參閱  
 [以時間為基礎之資料列篩選的最佳做法](best-practices-for-time-based-row-filters.md)   
 [篩選發行的資料](../publish/filter-published-data.md)   
 [針對合併式複寫篩選發行的資料](filter-published-data-for-merge-replication.md)  
  
  
