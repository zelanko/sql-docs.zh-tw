---
title: 在升級過程中，確認所有資料和記錄檔的自動成長皆已開啟 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0217d959759a59e49ce76e4a841c5d52e958e9ce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091221"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>在升級過程中，確認已為所有資料和記錄檔開啟自動成長
  Upgrade Advisor 偵測到未設定為自動成長的資料或記錄檔。 新的和增強功能需要額外的磁碟空間供使用者資料庫和**tempdb**系統資料庫之用。 為了確保在升級和後續的生產作業期間，資源可以配合大小的增加，建議您在升級之前，將所有使用者資料和記錄檔以及**tempdb**資料和記錄檔的自動成長設定為 [開啟]。  
  
 升級並測試工作負載之後，您可能會想要關閉自動成長，或根據使用者資料和記錄檔調整 FILEGROWTH 增量。 我們建議**tempdb**系統資料庫的自動成長保持開啟。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜tempdb 的容量計劃＞。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 **資料檔案**  
  
 下表將列出針對使用者定義資料檔案產生額外磁碟空間需求的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能變更。  
  
|功能|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的變更|  
|-------------|-----------------------------------------------------|  
|全文檢索|文件識別碼 (DOCID) 對應會儲存在資料檔案中，而非全文檢索目錄中。|  
|`text`、`ntext` 和 `image` 資料行|定義為 `text`、`ntext` 或 `image` 資料類型的大型物件 (LOB) 資料行需要每一個資料行有額外 40 個位元組的磁碟空間。 這個單次空間的增加是在每一個 LOB 資料行第一次更新期間發生的。|  
|中繼資料|其他系統中繼資料是針對資料庫物件和使用者權限，在每一個使用者資料庫的 PRIMARY 檔案群組中建立及維護。 例如，在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，與同意授權者或被授與者相關聯的權限是以點陣圖儲存在單一資料列中。 點陣圖已擴充為多個資料列。<br /><br /> 在升級程序期間，系統必須有足夠的磁碟空間，才能同時儲存舊和新的中繼資料。 否則，在升級完成之後，系統會刪除舊的中繼資料。|  
  
 **交易記錄檔**  
  
 下表將列出針對使用者定義交易記錄檔產生額外磁碟空間需求的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能變更。  
  
|功能|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的變更|  
|-------------|-----------------------------------------------------|  
|還原和復原|在損毀復原的恢復階段，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許使用者存取資料庫。 因為發生損毀時未認可的交易會重新取得損毀之前已保留的任何鎖定，所以這是可能發生的。 回復這些交易時，它們的鎖定會保護它們，不受到使用者的干擾。 這個額外鎖定資訊必須在交易記錄中維護。|  
  
 **tempdb 資料和記錄檔**  
  
 在舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中， **tempdb**資料庫是用來儲存下列物件：  
  
-   明確建立的暫存物件，例如資料表、預存程序、資料表變數或資料指標。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所建立的內部工作資料表。  
  
-   當您建立或重建索引時暫時排序的結果 (如果指定了 SORT_IN_TEMPDB 的話)。  
  
 其他物件也會使用**tempdb**資料庫。 下表列出會導致**tempdb**資料和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔產生額外磁碟空間需求的功能變更或新增專案。  
  
|功能|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的變更|  
|-------------|-----------------------------------------------------|  
|資料列版本設定|資料列版本設定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的一般架構，可用來執行下列作業：<br /><br /> 支援觸發程式：在觸發程式中建立已插入和已刪除的資料表。 經由觸發程序修改過的任何資料列都會被建立版本。 這包括啟動觸發程序之陳述式所修改的資料列，以及觸發程序所做的任何資料修改。 AFTER 觸發程式會使用**tempdb**的版本存放區來存放觸發程式所變更之資料列的 before 影像。 當您在啟用觸發程序的情況下大量載入資料時，系統會將每個資料列的副本加入至版本存放區。<br /><br /> 支援 Multiple Active Result Sets (MARS)。 如果 MARS 工作階段在有現用結果集的情況下，發出資料修改陳述式 (例如 INSERT、UPDATE 或 DELETE)，就會為修改陳述式所影響的資料列建立版本。<br /><br /> 支援指定 ONLINE 選項的索引作業。 線上索引作業會使用資料列版本設定來隔離索引作業與其他交易所進行的修改影響。 這樣可避免在已讀取的資料列上要求共用鎖定。 此外，線上索引作業期間的並行使用者更新和刪除作業需要**tempdb**中版本記錄的空間。<br /><br /> 支援以資料列版本設定為基礎的交易隔離等級：讀取認可隔離等級的新執行，其使用資料列版本設定來提供語句層級的讀取一致性。 新的隔離等級 (快照集)，可以提供交易等級的讀取一致性。<br /><br /> <br /><br /> 資料列版本會保留在**tempdb**版本存放區中，足以滿足在以資料列版本設定為基礎的隔離等級下執行之交易的需求。<br /><br /> 如需有關資料列版本設定和版本存放區的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜了解以資料列版本設定為基礎的隔離等級＞主題。|  
|暫存資料表和暫存變數中繼資料的快取|針對在中繼資料快取中快取的臨時表和暫存變數[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每個中繼資料，會為**tempdb**配置兩個額外的頁面。<br /><br /> 如果預存程序或觸發程序建立暫存資料表或暫存變數，則在該程序或觸發程序完成執行時，將不會刪除暫存物件。 而是將暫存物件截斷為單一頁面，並在下次執行該程序或觸發程序時重複使用。|  
|分割區資料表的索引|當[!INCLUDE[ssDE](../../includes/ssde-md.md)]執行排序來建立分割區索引時，如果指定了 SORT_IN_TEMPDB 索引選項， **tempdb**中就需要有足夠的空間來容納每個資料分割的中繼排序執行。|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)]保留不能留在記憶體中的現有對話內容（每個對話約 1 KB）時，會明確使用**tempdb** 。<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)]會透過在查詢執行內容中的物件快取，隱含使用**tempdb** 。 例如，用於計時器事件和背景傳遞交談的工作資料表。<br /><br /> DBMail、事件通知和查詢通知等功能會隱含使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。|  
|大型物件 (LOB) 資料類型<br /><br /> LOB 變數與參數|`varchar(max)`資料類型`nvarchar(max)`、、 **Varbinary （max）文字**、 `ntext` `image,`和`xml`是大型物件類型。<br /><br /> 在資料庫上啟用以資料列版本設定為基礎的交易隔離等級，並對大型物件進行修改時，會將已變更的 LOB 片段複製到**tempdb**中的版本存放區。<br /><br /> 定義為大型物件資料類型的參數會儲存在**tempdb**中。|  
|一般資料表運算式 (CTE)|執行一般資料表運算式查詢時，會在**tempdb**中建立多工緩衝處理作業的暫存工作資料表。|  
  
## <a name="corrective-action"></a>更正動作  
 若要將資料或記錄檔設為自動成長，請修改下列陳述式以指定資料庫的資料和記錄檔。 您應該將 FILEGROWTH 增量調整為適合您環境的值。  
  
```  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = tempdev,  
    FILEGROWTH = 20MB);  
GO  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = templog,  
    FILEGROWTH = 10MB);  
```  
  
 資料檔案的預設成長增量為 1 MB。 記錄檔的預設值為 10%。 設定 FILEGROWTH 增量時，我們建議您使用下列指導方針：  
  
|檔案大小|FILEGROWTH 增量|  
|---------------|--------------------------|  
|0-50MB|10MB|  
|100-200 MB|20MB|  
|500 MB 以上|10%|  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
