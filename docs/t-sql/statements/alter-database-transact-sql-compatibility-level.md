---
title: "ALTER DATABASE 相容性層級 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs: TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
caps.latest.revision: "89"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 62a9e4eec99073e63d53c2d610a7527fbe5f9c91
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTER DATABASE (TRANSACT-SQL) 相容性層級
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  
設定要相容於指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的資料庫行為。 如需其他 ALTER DATABASE 選項，請參閱[ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是要修改之資料庫的名稱。  
  
 COMPATIBILITY_LEVEL {140 | 130 | 120 | 110 | 100 | 90 | 80}  
 資料庫所要相容的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 您可以設定下列的相容性層級的值：  
  
|產品|資料庫引擎版本|相容性層級指定|支援的相容性層級值|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|SQL Server 2005|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
>  **Azure SQL Database** V12 已於 2014 年 12 月發行。 該版本的其中一個層面是新建立的資料庫有相容性層級設定為 120。 2015 的 SQL 資料庫開始支援層級 130，雖然預設變得讚賞 120。  
> 
> 從開始**2016 年 6 月 mid**，在 Azure SQL Database 中，預設相容性層級是 130 而不是 120 個**新建**資料庫。 2016 年 6 月 mid 之前建立的現有資料庫不受影響，並維持其目前的相容性層級 （100、 110 或 120）。 
> 
> 如果您想層級 130 為您的資料庫一般，但您有理由来偏好層級 110**基數估計**演算法，請參閱[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)，以及特別是其關鍵字 LEGACY_CARDINALITY_ESTIMATION = ON。  
>  
>  如需有關如何評估 Azure SQL Database 上的兩個相容性層級，將最重要的查詢效能差異的詳細資料請參閱[改善查詢效能與 Azure SQL Database 中的相容性層級 130](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。


 執行下列查詢，以判斷版本[!INCLUDE[ssDE](../../includes/ssde-md.md)]連線到。  
  
```tsql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
>  並非所有功能會因相容性層級上都支援[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  

 若要判斷目前的相容性層級，請查詢**compatibility_level**資料行[sys.databases &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```tsql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>備註  
 為所有安裝的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，預設相容性層級設定的版本為[!INCLUDE[ssDE](../../includes/ssde-md.md)]。 資料庫都設定為這個層級，除非**模型**資料庫有較低的相容性層級。 當資料庫升級任何舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果它是至少要有最小允許該執行個體，資料庫會保留其現有的相容性層級[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 升級具有的相容性層級低於允許的層級的資料庫，會將資料庫設定為層級允許的最低相容性。 這同樣適用於系統和使用者資料庫。 使用**ALTER DATABASE**若要變更資料庫的相容性層級。 若要檢視資料庫的目前相容性層級，請查詢**compatibility_level**中的資料行**sys.databases**目錄檢視。  

  
## <a name="using-compatibility-level-for-backward-compatibility"></a>使用相容性層級來提供回溯相容性  
 相容性層級只會影響指定之資料庫的行為，而不會影響整個伺服器的行為。 相容性層級只會提供與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的部分回溯相容性。 從 130 的相容性模式開始，任何新查詢計劃影響已加入功能只為新的相容性模式。 這種做法為了效能降低，因為查詢計劃變更時引發的升級期間將風險降到最低。 從應用程式的觀點而言，目標仍然是為了繼承部分新功能，以及在查詢最佳化工具空間中完成的效能改進，但若要這樣做的受控制的方式，是最新的相容性層級。 請使用相容性層級做為暫時移轉協助，協助您解決相關相容性層級設定所控制之行為的版本差異。 如需詳細資訊，請參閱本文稍後升級的最佳作法。  
  
 如果現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應用程式會受到您的版本中的行為差異[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，轉換至緊密地與新的相容性模式下使用應用程式。 然後使用**ALTER DATABASE**變更為 130 的相容性層級。 新資料庫的相容性設定生效時**USE Database**發行或處理新的登入的預設資料庫為該資料庫。  
  
## <a name="best-practices"></a>最佳作法  
 在使用者連接到資料庫時變更相容性層級，可能會讓使用中的查詢產生不正確的結果集。 例如，如果在編譯查詢計劃時變更相容性層級，編譯的計畫可能會同時以新的和舊的相容性層級為根據，而導致不正確的計畫以及可能不精確的結果。 此外，如果此計畫放入計畫快取且重複用於後續的查詢，問題可能更嚴重。 若要避免發生不精確的查詢結果，建議您使用下列程序變更資料庫的相容性層級：  
  
1.  使用 ALTER DATABASE SET SINGLE_USER 將資料庫設定為單一使用者存取模式。  
  
2.  變更資料庫的相容性層級。  
  
3.  使用 ALTER DATABASE SET MULTI_USER 將資料庫設定成多使用者存取模式。  
  
4.  如需有關設定資料庫的存取模式的詳細資訊，請參閱[ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="compatibility-levels-and-stored-procedures"></a>相容性層級和預存程序  
 當執行預存程序時，它會使用定義所在之資料庫的目前相容性層級。 當資料庫的相容性設定改變時，也會同時自動重新編譯它的所有預存程序。  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>相容性層級 130 和層級 140 之間的差異  
本章節描述相容性層級 140 導入了新的行為。

|或更低的 130 的相容性層級設定|相容性層級設定為 140|  
|--------------------------------------------------|-----------------------------------------|  
|基數估計值的陳述式參考多重陳述式資料表值函式會使用固定的資料列猜測。|基數估計值適合的陳述式參考多重陳述式資料表值函式會使用實際的函式輸出基數。  這透過啟用**交錯執行**多重陳述式資料表值函式。|
|批次模式的查詢要求記憶體不足，無法授與溢出到磁碟中的結果可能會繼續發生問題上連續執行的大小。|批次模式要求記憶體不足，無法授與大小溢出到磁碟中的結果可能會改善效能上連續執行的查詢。  這透過啟用**批次模式記憶體授與意見反應**如果溢出所發生的批次模式運算子，這會更新快取計畫的記憶體授與大小。 |
|批次模式的查詢要求過多的記憶體授與對連續執行的問題可能會繼續並行問題導致的大小。|批次模式的查詢要求過多的記憶體授與並行問題所導致的大小可能會改善上連續執行的並行。  這透過啟用**批次模式記憶體授與意見反應**如果原始要求很長，這會更新快取計畫的記憶體授與大小。|
|批次模式的查詢包含聯結運算子都適合進行三種實體聯結演算法，包括巢狀的迴圈、 雜湊聯結和合併聯結。  如果聯結的輸入不正確的基數估計值，可選取不適當的聯結演算法。  如果發生這種情況，會降低效能，而且不適當的聯結演算法會保持使用中，直到快取的計畫重新編譯。|沒有其他聯結運算子稱為**適應性聯結**。 如果外部建置聯結輸入不正確的基數估計值，可選取不適當的聯結演算法。  如果發生這種情況，而且在陳述式可供自動調整的聯結，將使用較小的聯結輸入巢狀的迴圈和雜湊聯結將會用於較大的聯結輸入動態而不需要重新編譯。 |
|一般參考資料行存放區索引的計劃不適合批次模式執行。 |參考資料行存放區索引的簡單式計劃將捨棄由適用於批次模式執行的計劃。|
|Sp_execute_external_script UDX 運算子只可以在資料列模式執行。|Sp_execute_external_script UDX 運算子都適合進行批次模式執行。|  
|沒有交錯的執行多重陳述式 TVF。 |若要改善的計畫品質的多重陳述式 tvf 的交錯的執行。 |

預設現在啟用了在舊版的 SQL Server 2017 之前的 SQL Server 追蹤旗標 4199 下的修正程式。 與相容性模式 140。 追蹤旗標 4199 仍會適用於新的查詢最佳化工具修正 SQL Server 2017 之後所發行。 如需有關追蹤旗標 4199 資訊，請參閱[追蹤旗標 4199](https://support.microsoft.com/en-us/kb/974006)。  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>層級 130 的相容性層級 120 之間的差異  
本章節描述相容性層級 130 導入了新的行為。   

  
|相容性層級設定為 120 或更低|相容性層級設定為 130|  
|--------------------------------------------------|-----------------------------------------|  
|Insert select 陳述式中的插入是單一執行緒。|Insert select 陳述式中的插入多執行緒，或可以有平行計畫。|  
|記憶體最佳化資料表上的查詢執行單一執行緒。|記憶體最佳化資料表上的查詢現在可以有平行計畫。|  
|導入的 SQL 2014 基數估計工具**CardinalityEstimationModelVersion ="120"**|進一步的基數估計 (CE) 改善基數估計模型 130 才會顯示從查詢與計劃。 **CardinalityEstimationModelVersion"130"**|  
|與資料行存放區索引的資料列模式變更批次模式<br /><br /> 具有資料行存放區索引的資料表上的排序是在資料列模式<br /><br /> 在資料列模式，例如延隔時間或負責人運作，視窗化函式彙總<br /><br /> 在具有多個資料列模式操作的 distinct 子句的資料行存放區資料表上的查詢<br /><br /> 在 MAXDOP 1 下或在資料列模式執行序列計畫執行的查詢 | 與資料行存放區索引的資料列模式變更批次模式<br /><br /> 排序資料行存放區索引的資料表上現在是以批次模式<br /><br /> 視窗彙總值現在在例如延隔時間或前置的批次模式下運作<br /><br /> 在批次模式運作，在具有多個 distinct 子句的資料行存放區資料表上的查詢<br /><br /> 批次模式執行 Maxdop1 或序列計畫執行的查詢|  
| 可以自動更新統計資料。 | 它會自動更新統計資料的邏輯是更積極的在大型資料表上。  在實務上，這應該降低客戶其中經常但其中統計資料尚未更新為包含值，其中查詢新插入的資料列的查詢看到效能問題的情況。 |  
| 追蹤 2371年中預設是 OFF [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 | [追蹤 2371年](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/)中預設為 ON [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 追蹤旗標 2371年指示要取樣的較小尚未直接資料列的子集，具有很棒的多個資料列的資料表中的自動統計資料更新程式。 <br/> <br/> 一個改善就是要包含在此範例中的最近插入多個資料列。 <br/> <br/> 另一個改善就是讓查詢執行時，更新統計資料程序會執行，而不是封鎖的查詢。 |  
| 統計資料取樣的層級 120 的*單一*-執行緒程序。 | 統計資料取樣的層級 130*多重*-執行緒程序。 |  
| 內送 253 的外部索引鍵是的限制。 | 最多 10,000 個連入的外部索引鍵或類似的參考可以參考給定的資料表。 相關限制，請參閱 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)。 |  
|允許使用已被取代的 MD2、 MD4、 MD5、 SHA 和 SHA1 雜湊演算法。|允許使用唯一的 SHA2_256 和 SHA2_512 雜湊演算法。|  
  
  
修正程式已在追蹤旗標 4199 較舊版本中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]現在預設會啟用。 與 130 的相容性模式。 追蹤旗標 4199 仍會適用於發行後發行的新查詢最佳化工具修正[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 若要使用較舊的查詢最佳化工具在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]您必須選取相容性層級為 110。 如需有關追蹤旗標 4199 資訊，請參閱[追蹤旗標 4199](https://support.microsoft.com/en-us/kb/974006)。  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>更低相容性層級和層級 120 之間的差異  
 本章節描述相容性層級 120 所導入的新行為。  
  
|相容性層級設定為 110 或更低|相容性層級設定為 120|  
|--------------------------------------------------|-----------------------------------------|  
|使用舊版的查詢最佳化工具。|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 包括了可建立及最佳化查詢計劃之元件的大幅改良。 這個新的查詢最佳化工具功能取決於資料庫相容性層級 120 的使用。 新的資料庫應用程式應該使用資料庫相容性層級 120 加以開發，以便充分利用這些改良功能。 從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉的應用程式應該謹慎測試，以確認良好的效能得以持續或改善。 如果效能降低，您可以將資料庫相容性層級設定為 110 或更低的數字，以便使用舊的查詢最佳化工具方法。<br /><br /> 資料庫相容性層級 120 會使用新的基數估計工具，其經過調整適合於新型資料倉儲和 OLTP 工作負載。 在之前設定資料庫相容性層級為 110，基於效能考量，請參閱中的查詢計劃區段的建議[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [What's New in Database Engine](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)主題。|  
|在低於 120 的相容性層級，轉換時，會忽略語言設定**日期**值字串值。 請注意，此行為是只**日期**型別。 請參閱下面的範例 > 一節中的範例 B。|轉換時，不會忽略語言設定**日期**值字串值。|  
|EXCEPT 子句右邊的遞迴參考會建立無限迴圈。 下列範例 > 一節中的範例 C 示範此行為。|EXCEPT 子句中的遞迴參考會產生符合 ANSI SQL 標準的錯誤。|  
|遞迴 CTE 允許重複的資料行名稱。|遞迴 CTE 不允許重複的資料行名稱。|  
|如果觸發程序經過更改，則停用的觸發程序會再次啟用。|更改觸發程序不會變更觸發程序的狀態 (啟用或停用)。|  
|OUTPUT INTO 資料表子句會忽略 IDENTITY_INSERT SETTING = OFF 並允許插入外顯值。|當 IDENTITY_INSERT 設為 OFF 時，您無法在資料表中插入識別欄位的外顯值。|  
|當資料庫內含項目設定為部分時，驗證 MERGE 陳述式的 OUTPUT 子句中的 $action 欄位可能會傳回定序錯誤。|MERGE 陳述式的 $action 子句所傳回值的定序是資料庫定序，而不是伺服器定序，且不會傳回定序衝突錯誤。|  
|A **SELECT INTO**陳述式一律會建立單一執行緒的插入作業。|A **SELECT INTO**陳述式可以建立平行插入作業。 當插入大量資料列時，平行作業可以提升效能。|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>更低相容性層級與層級 110 和 120 之間的差異  
 本章節描述相容性層級 110 所導入的新行為。   這一節也適用於層級 120。  
  
|相容性層級設定為 100 或更低|至少為 110 的相容性層級設定|  
|--------------------------------------------------|--------------------------------------------------|  
|Common Language Runtime (CLR) 資料庫物件是使用 CLR 4 版執行。 不過，CLR 4 版中導入的部分行為變更會加以忽略。 如需詳細資訊，請參閱[What's New in CLR 整合](../../relational-databases/clr-integration/clr-integration-what-s-new.md)。|CLR 資料庫物件是使用 CLR 4 版執行。|  
|XQuery 函數**字串長度**和**substring**每個 surrogate 計算為兩個字元。|XQuery 函數**字串長度**和**substring**每一個 surrogate 視為一個字元。|  
|可以在遞迴通用資料表運算式 (CTE) 查詢中使用 PIVOT。 但每個分組如有多個資料列，查詢會傳回的結果將會不正確。|不可在遞迴通用資料表運算式 (CTE) 查詢中使用 PIVOT。 傳回錯誤。|  
|只有 RC4 演算法支援回溯相容性。 只有在資料庫相容性層級為 90 或 100 時，才能使用 RC4 或 RC4_128 加密新資料  (不建議使用)。在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中使用 RC4 或 RC4_128 加密的資料，可以在任何相容性層級進行解密。|不可使用 RC4 或 RC4_128 加密新資料。 請改用較新的演算法，例如其中一個 AES 演算法。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中使用 RC4 或 RC4_128 加密的資料，可以在任何相容性層級進行解密。|  
|CAST 和 CONVERT 作業的預設樣式**時間**和**datetime2**資料型別為 121 計算資料行運算式中使用其中一種類型時。 若為計算資料行，預設樣式為 0。 當您建立計算資料行、將它們用於包含自動參數化的查詢或用於條件約束定義時，這種行為就會影響計算資料行。<br /><br /> 下列範例 > 一節中範例樣式 0 與 121 之間的差異。 此範例不會示範上述的行為。 如需日期和時間樣式的詳細資訊，請參閱[CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).|在相容性層級 110，CAST 和 CONVERT 作業的預設樣式上**時間**和**datetime2**資料型別一律為 121。 如果您的查詢仰賴舊的行為，請使用低於 110 的相容性層級，或在受影響的查詢中明確指定 0 樣式。<br /><br /> 將資料庫升級為相容性層級 110 不會變更已經儲存至磁碟的使用者資料。 您必須依適當情況手動更正這項資料。 例如，如果您使用了 SELECT INTO，根據包含上述計算資料行運算式的來源建立資料表，系統就會儲存資料 (使用樣式 0) 而非計算資料行定義本身。 您必須手動將這項資料更新為符合樣式 121。|  
|遠端資料表中的類型的任何資料行**smalldatetime**資料分割檢視所參考之對應為**datetime**。 （在選取清單中的相同序數位置） 的本機資料表中對應資料行必須是型別**datetime**。|遠端資料表中的類型的任何資料行**smalldatetime**資料分割檢視所參考之對應為**smalldatetime**。 （在選取清單中的相同序數位置） 的本機資料表中對應資料行必須是型別**smalldatetime**。<br /><br /> 在升級到 110 後，分散式分割區檢視會因為資料類型不符合而失敗。 您可以變更遠端資料表的資料類型來解決這**datetime**或設定相容性層級的本機資料庫設為 100 或更低。|  
|SOUNDEX 函數會實作以下規則：<br /><br /> 1）-大寫 H 或大寫 W 會忽略分隔兩個子音，有相同數目的 SOUNDEX 代碼。<br /><br /> 2） 如果的前 2 個字元*character_expression*有相同數目的 SOUNDEX 代碼，這兩個字元會包含在內。 否則，如果一組並存子音有相同的 SOUNDEX 代碼數字，除了第一個子音，所有子音都會被排除在外。|SOUNDEX 函數會實作以下規則：<br /><br /> 1） 如果大寫 H 或大寫 W 分隔兩個子音有相同數目的 SOUNDEX 代碼，而右邊的子音，則會忽略<br /><br /> 2） 如果一組由並存子音有相同數目的 SOUNDEX 代碼，全部都排除第一個除外。<br /><br /> <br /><br /> 其他規則可能會使 SOUNDEX 函數計算的值不同於在舊版相容性層級下計算的值。 升級到相容性層級 110 之後，您可能需要重建使用 SOUNDEX 函數的索引、堆積或 CHECK 條件約束。 如需詳細資訊，請參閱[SOUNDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>相容性層級 90 和 100 之間的差異  
 本章節描述相容性層級 100 所導入的新行為。  
  
|相容性層級設定為 90|相容性層級設定為 100|影響的可能性|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|如果不論工作階段層級設定為何都會建立多重陳述式資料表值函式，則 QUOTED_IDENTIFER 設定一定會針對這種函數設定為 ON。|當建立多重陳述式資料表值函式時，可接受 QUOTED IDENTIFIER 工作階段設定。|中|  
|當您建立或改變分割區函數， **datetime**和**smalldatetime**函式中的常值會評估時會假設 US_English 為語言設定。|目前語言設定用來評估**datetime**和**smalldatetime**常值的資料分割函數。|中|  
|INSERT 和 SELECT INTO 陳述式內允許 FOR BROWSE 子句 (而且會予以忽略)。|INSERT 和 SELECT INTO 陳述式內不允許 FOR BROWSE 子句。|中|  
|OUTPUT 子句中允許全文檢索述詞。|OUTPUT 子句中不允許全文檢索述詞。|低|  
|CREATE FULLTEXT STOPLIST、ALTER FULLTEXT STOPLIST 和 DROP FULLTEXT STOPLIST 都不受支援。 系統停用字詞表會自動與新的全文檢索索引產生關聯。|CREATE FULLTEXT STOPLIST、ALTER FULLTEXT STOPLIST 和 DROP FULLTEXT STOPLIST 都有支援。|低|  
|MERGE 不會強制為保留關鍵字。|MERGE 是完整的保留關鍵字。 100 和 90 相容性層級之下都有支援 MERGE 陳述式。|低|  
|使用\<dml_table_source > 的 INSERT 陳述式的引數就會引發語法錯誤。|您可以在巢狀 INSERT、UPDATE、DELETE 或 MERGE 陳述式中擷取 OUTPUT 子句的結果，並將這些結果插入目標資料表或檢視表中。 這是使用\<dml_table_source > 的 INSERT 陳述式的引數。|低|
|除非指定了 NOINDEX，否則 DBCC CHECKDB 或 DBCC CHECKTABLE 會針對單一資料表或索引檢視表及它的所有非叢集索引和 XML 索引進行實體和邏輯一致性檢查。 不支援空間索引。|除非指定了 NOINDEX，否則 DBCC CHECKDB 或 DBCC CHECKTABLE 會針對單一資料表及它的所有非叢集索引進行實體和邏輯一致性檢查。 但是根據預設，XML 索引、空間索引和索引檢視表只會進行實體一致性檢查。<br /><br /> 如果指定了 WITH EXTENDED_LOGICAL_CHECKS，將會針對索引檢視表、XML 索引和空間索引 (如果有的話) 執行邏輯檢查。 根據預設，實體一致性檢查會在邏輯一致性檢查之前執行。 如果也指定了 NOINDEX，則只會執行邏輯檢查。|低|  
|搭配資料操作語言 (DML) 陳述式使用 OUTPUT 子句而且在陳述式執行期間發生執行階段錯誤時，就會終止和回復整個交易。|搭配資料操作語言 (DML) 陳述式使用 OUTPUT 子句而且在陳述式執行期間發生執行階段錯誤時，其行為取決於 SET XACT_ABORT 設定。 如果 SET XACT_ABORT 為 OFF，使用 OUTPUT 子句之 DML 陳述式所產生的陳述式中止錯誤將會結束此陳述式，但是批次會繼續執行，而且不會回復交易。 如果 SET XACT_ABORT 為 ON，使用 OUTPUT 子句之 DML 陳述式所產生的所有執行階段錯誤將會結束批次，而且會回復交易。|低|  
|不會強制 CUBE 和 ROLLUP 必須為保留關鍵字。|CUBE 和 ROLLUP 在 GROUP BY 子句中為保留關鍵字。|低|  
|嚴格驗證會套用至的 XML 項目**anyType**型別。|Lax 驗證會套用至的項目**anyType**型別。 如需詳細資訊，請參閱[萬用字元元件和內容驗證](../../relational-databases/xml/wildcard-components-and-content-validation.md)。|低|  
|特殊屬性**xsi: nil**和**xsi: type**無法進行查詢或修改的資料操作語言陳述式。<br /><br /> 這表示`/e/@xsi:nil`失敗時`/e/@*`忽略**xsi: nil**和**xsi: type**屬性。 不過，`/e`傳回**xsi: nil**和**xsi: type**屬性的一致性`SELECT xmlCol`，即使`xsi:nil = "false"`。|特殊屬性**xsi: nil**和**xsi: type**儲存為一般屬性和可查詢，並修改。<br /><br /> 例如，執行查詢`SELECT x.query('a/b/@*')`傳回所有屬性，包括**xsi: nil**和**xsi: type**。 若要排除在查詢中的這些型別，取代`@*`與`@*[namespace-uri(.) != "` *insert xsi 命名空間 uri* `"`而非`(local-name(.) = "type"`或`local-name(.) ="nil".`|低|  
|將 XML 常數字串值轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期時間類型的使用者定義函數，會標示為決定性。|將 XML 常數字串值轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期時間類型的使用者定義函數會標示為不具決定性。|低|  
|XML 聯集和清單類型並未受到完整支援。|聯集和清單類型受到完整支援，包括以下功能：<br /><br /> 清單的聯集<br /><br /> 聯集的聯集<br /><br /> 不可部分完成之類型的清單<br /><br /> 聯集的清單|低|  
|當此方法包含在檢視表或是內嵌資料表值函式內時，不會驗證 xQuery 方法所需的 SET 選項。|當此方法包含在檢視表或是內嵌資料表值函式內時，將會驗證 xQuery 方法所需的 SET 選項。 如果未能正確設定此方法的 SET 選項，將會引發錯誤。|低|  
|包含行尾字元 (歸位字元和換行字元) 的 XML 屬性值不會根據 XML 標準來正規化。 也就是說，會傳回這兩個字元，而不是單一換行字元。|包含行尾字元 (歸位字元和換行字元) 的 XML 屬性值會根據 XML 標準來正規化。 也就是說，外部剖析之實體 (包括文件實體) 內的所有分行符號都會在輸入上正規化，其方式是將雙字元序列 #xD #xA 及任何緊接著 #xA 的 #xD 轉換成單一 #xA 字元。<br /><br /> 使用屬性來傳輸包含行尾字元之字串值的應用程式將不會在提交這些字元時收回這些字元。 為了避免正規化的程序，請使用 XML 數值字元實體來編碼所有行尾字元。|低|  
|資料行屬性 ROWGUIDCOL 和 IDENTITY 可以錯誤地命名為條件約束。 例如，陳述式 `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` 會執行，但是條件約束名稱不會保留，也無法供使用者存取。|資料行屬性 ROWGUIDCOL 和 IDENTITY 無法命名為條件約束。 傳回錯誤 156。|低|  
|使用雙向指派來更新資料行 (例如 `UPDATE T1 SET @v = column_name = <expression>`) 會產生非預期的結果，因為陳述式執行期間可以在其他子句 (如 WHERE 和 ON 子句) 中使用變數的即時值，而不是陳述式起始值。 這會導致述詞的意義會根據每個資料列而以非預期的方式變更。<br /><br /> 只有當相容性層級設定為 90 時，才適用這個行為。|使用雙向指派來更新資料行會產生預期的結果，因為陳述式執行期間只會存取資料行的陳述式起始值。|低|  
|請參閱下面的範例 > 一節中的範例 E。|請參閱下面的範例 > 一節中的範例 F。|低|  
|ODBC 函數 {fn CONVERT()} 會使用語言的預設日期格式。 對於某些語言來說，預設格式為 YDM，這可能會在 CONVERT() 結合其他必須是 YMD 格式的函數 (例如 {fn CURDATE()}) 使用時產生轉換錯誤。|當 ODBC 函數 {fn CONVERT()} 轉換成 ODBC 資料類型 SQL_TIMESTAMP、SQL_DATE、SQL_TIME、SQLDATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP 時，會使用樣式 121 (與語言無關的 YMD 格式)。|低|  
|日期時間內建 (如 DATEPART) 不會要求字串輸入值必須是有效的日期時間常值。 例如，SELECT DATEPART (year, '2007/05-30') 會編譯成功。|日期時間內建 (如 DATEPART) 會要求字串輸入值必須是有效的日期時間常值。 當使用無效的日期時間常值時會傳回錯誤 241。|低|  
  
## <a name="reserved-keywords"></a>保留關鍵字  
 相容性設定也決定了 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所保留的關鍵字。 下表顯示每個相容性層級所使用的保留關鍵字。  
  
|相容性層級設定|保留關鍵字|  
|----------------------------------|-----------------------|  
|130|有待決定。|  
|120|無。|  
|110|WITHIN GROUP、TRY_CONVERT、SEMANTICKEYPHRASETABLE、SEMANTICSIMILARITYDETAILSTABLE、SEMANTICSIMILARITYTABLE|  
|100|CUBE、MERGE、ROLLUP|  
|90|EXTERNAL、PIVOT、UNPIVOT、REVERT、TABLESAMPLE|  
  
 在給定的相容性層級中，保留關鍵字包含這個層級或這個層級以下所導入的所有關鍵字。 例如，對於層級 110 的應用程式而言，上表所列出的所有關鍵字都會保留下來。 在較低的相容性層級中，層級 100 的關鍵字仍是有效的物件名稱，但對應於這些關鍵字的層級 110 語言功能則無法使用。  
  
 導入之後，關鍵字會維持保留狀態。 例如，相容性層級 90 所導入的保留關鍵字 PIVOT，也會保留在層級 100 和 110 和 120 中。  
  
 如果應用程式使用的識別碼是其相容性層級的保留關鍵字，應用程式便會失敗。 若要解決這個問題，請將任一個括號之間的識別項 (**[]**) 或引號 (**""**); 例如，若要升級應用程式使用識別碼**外部**相容性層級 90，您可以變更為識別碼**[外部]**或**「 外部 」**。  
  
 如需詳細資訊，請參閱[保留關鍵字 &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-compatibility-level"></a>A. 變更相容性層級  
 下列範例會變更的相容性層級[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫`110,` [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 下列範例會傳回目前資料庫的相容性層級。  
  
```tsql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>B. 正在略過相容性層級 120 以外的 SET LANGUAGE 陳述式  
 下列查詢會忽略除了相容性層級 120 的 SET LANGUAGE 陳述式。  
  
```tsql  
SET DATEFORMAT dmy;   
DECLARE @t2 date = '12/5/2011' ;  
SET LANGUAGE dutch;   
SELECT CONVERT(varchar(11), @t2, 106);   
  
-- Results when the compatibility level is less than 120.   
12 May 2011   
  
-- Results when the compatibility level is set to 120).  
12 mei 2011  
```  
  
### <a name="c"></a>C.  
 對於相容性層級設定為 110 或更低，EXCEPT 子句右邊的遞迴參考會建立無限迴圈。  
  
```tsql  
WITH   
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),  
r   
AS (SELECT a FROM Table1  
UNION ALL  
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )   
SELECT a   
FROM r;  
  
```  
  
### <a name="d"></a>D.  
 此範例顯示樣式 0 與 121 之間的差異。 如需日期和時間樣式的詳細資訊，請參閱[CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
```tsql  
CREATE TABLE t1 (c1 time(7), c2 datetime2);   
  
INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());  
  
SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0  
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121  
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0  
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121  
FROM t1;  
  
-- Returns values such as the following.  
TimeStyle0       TimeStyle121       
Datetime2Style0      Datetime2Style121  
---------------- ----------------   
-------------------- --------------------------  
3:15PM           15:15:35.8100000   
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000  
```  
  
### <a name="e"></a>E.  
 在包含最上層 UNION 運算子的陳述式中允許使用變數指派，但是會傳回非預期的結果。 例如在下列陳述式中，會將兩個資料表之聯集中的 `@v` 資料行值指派給 `BusinessEntityID` 區域變數。 就定義來說，如果 SELECT 陳述式傳回多個值，就會將最後傳回的值指派給變數。 在此情況下，便會將最後一個值正確地指派給變數，但是也會傳回 SELECT UNION 陳述式的結果集。  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 90;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>F.  
 在包含最上層 UNION 運算子的陳述式中，不允許使用變數指派。 傳回錯誤 10734。 若要解決此錯誤，請重寫查詢，如下列範例所示。  
  
```tsql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [保留關鍵字 &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
