---
title: 報表和快照集的大小限制 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- large reports
- maximum report size
- size [SQL Server], reports
- report size [Reporting Services]
- reports [Reporting Services], size
- denial of service attacks [Reporting Services]
ms.assetid: 1e3be259-d453-4802-b2f5-6b81ef607edf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 05ed8b22882264aa16efc8c5b7736bcc517e44f9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "65581446"
---
# <a name="report-and-snapshot-size-limits"></a>報表和快照集的大小限制
  管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署的管理員可以透過此主題中的資訊來了解，當報表發行至報表伺服器、在執行階段進行轉譯以及儲存至檔案系統時，報表大小的限制。 此主題也提供有關如何測量報表伺服器資料庫大小的實作指南，並且描述快照集大小對伺服器效能的影響。  
  
## <a name="maximum-size-for-published-reports"></a>已發行報表的大小上限  
 報表伺服器上報表和模型的大小，是根據您發行至報表伺服器上報表定義 (.rdl) 與報表模型 (.smdl) 檔案的大小來決定， 報表伺服器本身並不會限制您發行之報表的大小。 但是，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 會限制張貼到伺服器的項目大小上限。 依預設，此限制為 4 MB。 如果您將超出此限制的檔案上傳或發行至報表伺服器，您將收到一個 HTTP 例外狀況。 在此情況下，藉由增加 Machine.config 檔案中 **maxRequestLength** 元素的值，就可以修改預設值。  
  
 儘管報表模型的大小可能非常巨大，但是報表定義很少會超過 4 MB， 而且報表大小通常只在 KB 的範圍之內。 但是，如果您包含內嵌影像，則這些影像的編碼可能會產生超過 4 MB 預設值的大型報表定義。  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 會限制公佈之檔案的大小上限，以便減少針對伺服器的阻絕服務攻擊威脅。 增加上限值會逐漸破壞此限制所提供的一些保護。 只有當您確定增加上限值後的優點，大於任何額外的安全性風險時，才需要這麼做。  
  
 請記住，您為 **maxRequestLength** 元素所設定的值必須大於想要強制執行的實際大小限制。 將所有參數封裝在 SOAP Envelope 中，並將 Base64 編碼套用至特定參數之後，HTTP 要求大小必然會增加，因此您需要設定更大的值以容納增加的大小。 Base64 編碼會使原始資料大小增加約 33%。 因此，您為 **maxRequestLength** 元素所指定的值需要大於實際可用的項目大小約 33%。 例如，如果您為 **maxRequestLength**所指定的值為 64 MB，公佈到報表伺服器的報表檔案大小上限實際上應該約會是 48 MB。  
  
## <a name="report-size-in-memory"></a>記憶體中的報表大小  
 當您執行報表時，報表大小等於傳回的報表資料量再加上輸出資料流的大小。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會限制已轉譯之報表的大小上限。 系統記憶體會決定大小上限 (根據預設，轉譯報表時，報表伺服器會使用所有設定的可用記憶體)，但是您可以指定組態設定，以便設定記憶體臨界值和記憶體管理原則。 如需詳細資訊，請參閱 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。  
  
 對於任何報表而言，根據所傳回資料的數量以及該報表所使用的轉譯格式，其大小可以有許多不同的變化。 參數化報表可能會因為參數值影響查詢結果的情況，而會變得較大或較小。 所選取的報表輸出格式會對報表大小產生下列幾種影響：  
  
-   HTML 一次只會處理一頁報表， 由於報表以較小的單位進行處理，因此處理特定區塊時僅需要較少的記憶體。  
  
-   PDF、Excel、TIFF、XML 及 CSV 向使用者顯示報表前，會先在記憶體中處理整個報表。  
  
 若要測量已轉譯報表的大小，您可以檢視報表執行記錄。 如需詳細資訊，請參閱 [報表伺服器 ExecutionLog 和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
 若要計算磁碟中已轉譯報表的大小，您可以匯出報表，然後將報表儲存到檔案系統 (儲存的檔案包含資料以及報表格式資訊)。  
  
 報表大小唯一的硬限制只會發生在轉譯成 Excel 格式時， 因為工作表不能超過 65536 個資料列或 256 個資料行。 其他轉譯格式沒有這些限制，因此檔案大小僅受限於伺服器的資源數量。  
  
> [!NOTE]  
>  報表處理及轉譯是在記憶體中處理， 因此，如果您有大型的報表或大量的使用者，請務必先做好容量計劃，以確保您的報表伺服器部署執行方式可以滿足使用者。 如需有關工具和指導方針的詳細資訊，請參閱下列 MSDN 發行集：＜ [規劃 Reporting Services 的延展性和效能](/previous-versions/sql/sql-server-2005/administrator/cc966418(v=technet.10)) ＞(英文) 和＜ [在 SQL Server 2005 Reporting Services 報表伺服器上使用 Visual Studio 2005 執行負載測試](https://go.microsoft.com/fwlink/?LinkID=77519)＞(英文)。  
  
## <a name="measuring-snapshot-storage"></a>測量快照集儲存區  
 任何給定之快照集的大小，會與報表中的資料數量呈現直接正比， 因此會遠大於儲存在報表伺服器上的其他項目。 快照集大小一般會介於數 MB 到數十 MB 之間， 如果您的報表非常大，則可以預期會看到更大的快照集。 根據您使用快照集的頻率以及設定報表記錄的方式，可能在短時間內，報表伺服器資料庫所需的磁碟空間數量就會快速增加。  
  
 **reportserver** 與 **reportservertempdb** 兩種資料庫預設都設定為自動成長。 儘管資料庫大小會自動增加，但卻不會自動減少。 如果因為刪除快照集造成 **reportserver** 資料庫超出其容量，您就必須手動縮減資料庫的大小來復原磁碟空間。 相同的，如果擴充 **reportservertempdb** 以容納不尋常、極大量的互動式報告功能，磁碟空間配置將會維持這個設定直到您縮小資料庫大小為止。  
  
 若要測量報表伺服器資料庫的大小，您可以執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。 定期計算資料庫大小的總和可以幫助您建立在一段期間內合理預估報表伺服器資料庫的方式。 下列陳述式會測量目前使用的空間數量 (這些陳述式假定您使用的是預設的資料庫名稱)：  
  
```  
USE ReportServer  
EXEC sp_spaceused  
```  
  
## <a name="snapshot-size-and-report-server-performance"></a>快照集大小與報表伺服器效能  
 處理及轉譯報表時，快照集大小會影響伺服器的效能。 轉譯作業對伺服器效能的影響最大，因此如果有大型的快照集，當使用者對報表提出要求時應該會有一些延遲發生。 根據使用者的數量，當快照集大小超過 100 MB 時可能會發生延遲。  
  
 若要將大型快照集所造成的效能延遲降到最低，您可以執行下列動作：  
  
-   在個別的電腦上部署報表伺服器與 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。  
  
-   增加更多系統記憶體。  
  
-   檢閱 MSDN 網站上的＜規劃 Reporting Services 的延展性和效能＞文件，以了解設定企業報表伺服器的最佳做法。  
  
 儲存在報表伺服器資料庫中的快照集數量，是個別儲存的，與效能因素無關， 因此您可以儲存大量的快照集而不會影響伺服器的效能。 您可以永遠保留快照集， 但是，請注意報表記錄是可設定的， 如果報表伺服器管理員降低報表記錄的限制，您可能會遺失原本打算保留的記錄報表。 如果刪除該報表，所有的報告記錄也會隨之刪除。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)   
 [報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [處理大型報表](../../reporting-services/report-server/process-large-reports.md)  
  
  
