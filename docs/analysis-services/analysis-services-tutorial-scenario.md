---
title: "Analysis Services 教學課程案例 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 933a07504d0237d67becb2d98e1f5271548cb14a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-tutorial-scenario"></a>Analysis Services 教學課程案例
這個教學課程是以一家虛構的公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]為基礎。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨國製造公司，專門生產及批發金屬和合成器材自行車給北美、歐洲和亞洲的商場。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的總公司在華盛頓 Bothell，該公司雇用 500 位員工。 另外， [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 它的市場還雇用了一些地區銷售團隊。  
  
在最近幾年， [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 購買了一間墨西哥的小型製造工廠 Importadores Neptuno。 Importadores Neptuno 為 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 產品線製造幾項重要的子零件。 這些子零件運送到 Bothell 地點進行最後產品組裝。 在 2005 年，Importadores Neptuno 成為自行車產品類的唯一製造商和批發商。  
  
在豐收的會計年度之後，現在 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 想要以這些方式來擴展它的市場佔有率：鎖定最佳客戶來打廣告、透過外部網站延伸產品可用性，並以減少實際成本來降低銷售成本。  
  
## <a name="current-analysis-environment"></a>目前分析環境  
為了支援銷售和行銷團隊以及資深管理的資料分析需求，該公司目前是從 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 資料庫取得交易資料，再從試算表取得非交易資訊，如銷售配額，然後將這項資訊合併到 **AdventureWorksDW2012** 關聯式資料倉儲。 不過，關聯式資料倉儲帶來下列挑戰：  
  
-   報表是靜態的。 使用者無法互動地瀏覽報表中的資料來取得更詳細的資訊，如同他們在處理 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 樞紐資料表一般。 雖然現有的預先定義報表集對許多使用者而言已經足夠，但更進階的使用者需要直接查詢來存取資料庫中的互動式查詢和特殊報表。 不過，由於 **AdventureWorksDW2012** 資料庫很複雜，進階使用者需要很多時間才能學會如何建立有效率的查詢。  
  
-   查詢效能變化很大。 例如，有些查詢在短短幾秒鐘內就可以傳回結果，有些查詢則需要花幾分鐘才能傳回。  
  
-   彙總資料表不好管理。 為了改進查詢回應時間， [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 的資料倉儲團隊在 **AdventureWorksDW2012** 資料庫中建立幾份彙總資料表。 例如，他們建置一個按月彙總銷售量的資料表。 不過，雖然這些彙總資料表可大幅改進查詢效能，但他們經過一段時間建置來維護資料表的基礎架構既脆弱，又容易出錯。  
  
-   複雜的計算邏輯埋藏在報表定義中，使報表之間很難分享。 因為每一個報表的這個商務邏輯是個別產生的，所以報表之間的摘要資訊有時候並不相同。 因此，管理階層對於資料倉儲的報表不太有信心。  
  
-   不同事業單位的使用者對不同資料檢視感興趣。 每一個團體對於不相關的資料元素感到困擾及困惑。  
  
-   計算邏輯對於需要特殊報表的使用者更是一大挑戰。 因為這類使用者必須個別為每一個報表定義計算邏輯，所以對於計算邏輯如何定義並沒有集中控制的方法。 例如，有些使用者知道他們應該使用基本統計技巧，例如移動平均值，但他們不知道如何去建構這樣的計算，而沒有使用這些技巧。  
  
-   要合併相關資訊集很難。 商務使用者很難去建構結合兩組相關資訊 (如銷售量和銷售配額) 的特殊查詢。 這類查詢會使資料庫癱瘓，因此公司需要使用者向資料倉儲團隊要求跨主題區的資料集。 所以，只定義少數預先定義的報表來結合多個主題區的資料。 此外，由於太過複雜，使用者也不願意嘗試修改這些報表。  
  
-   報表主要重點在於美國的商務資訊。 非美國分公司的使用者很不滿意這項重點，他們想要以不同貨幣和不同語言檢視報表。  
  
-   資訊很難稽核。 財務部門目前使用的 **AdventureWorksDW2012** 資料庫只做為大量查詢的資料來源。 他們會將資料下載到個別的試算表，然後花很多時間準備資料及處理試算表。 因此，公司財務報表很難在整個公司進行準備、稽核和管理的工作。  
  
## <a name="the-solution"></a>方案  
資料倉儲團隊最近對目前分析系統進行設計檢閱。 這項檢閱包括對目前問題和未來需求的差距分析。 資料倉儲團隊認為 **AdventureWorksDW2012** 資料庫是一個設計完善的維度資料庫，其中包含符合標準的維度和 Surrogate 索引鍵。 符合維度可讓維度使用於多個資料超市，例如 [時間] 維度或 [產品] 維度。 Surrogate 索引鍵是假造的索引鍵，連結維度和事實資料表，用來確保唯一性及改進效能。 此外，資料倉儲團隊也判定 **AdventureWorksDW2012** 資料庫中基底資料表的載入和管理方面目前沒有重大問題。 因此該團隊決定使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 來完成下列各項：  
  
-   透過共同中繼資料層，提供統一資料存取，以進行邏輯分析和報告。  
  
-   簡化使用者的資料檢視，加速開發互動式及預先定義的查詢和預先定義的報表。  
  
-   正確建構查詢來結合多個主題區域的資料。  
  
-   管理彙總。  
  
-   儲存和重複使用複雜計算。  
  
-   對美國以外地區的商務使用者提供當地語系化體驗。  
  
Analysis Services 教學課程中的課程提供建立符合這些所有目標之 Cube 資料庫的指導方針。 若要開始使用，請繼續進行第一課： [第 1 課：建立新的表格式模型專案](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="see-also"></a>另請參閱  
[多維度模型化 &#40;Adventure Works 教學課程&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
  
  

