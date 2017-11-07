---
title: "全球化秘訣和最佳作法 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- translations [Analysis Services], client applications
- date comparisons
- day-of-week comparisons [Analysis Services]
- time [Analysis Services]
- month comparisons [Analysis Services]
ms.assetid: 71a8c438-1370-4c69-961e-d067ee4e47c2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79c80dd57b6a6ea1257c00dfb95bf1e9a08a5b99
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>全球化秘訣和最佳作法 (Analysis Services)
  [!INCLUDE[applies](../includes/applies-md.md)] 僅限多維度  
  
 下列秘訣和指導方針有助於提高商業智慧方案的可攜性，並避免發生與語言和定序設定直接相關的錯誤。  
  
##  <a name="bkmk_sameColl"></a> 在整個堆疊中使用類似的定序  
 請盡可能嘗試在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用針對資料庫引擎所使用的相同定序設定，力求在區分全半形、大小寫和腔調字方面保持一致。  
  
 每項服務都有自己的定序設定，其中資料庫引擎預設為 SQL_Latin1_General_CP1_CI_AS，而 Analysis Services 設為 Latin1_General_AS。 這些預設值在區分大小寫、全半形和腔調字方面保持一致。 請注意，如果您改變任何一個定序的設定，當定序屬性基本上有所分歧時，可能會發生問題。  
  
 即使定序設定的功能相同，您還是可能會遇到每項服務以不同方式解譯字串中任何位置之空格的特殊大小寫情況。  
  
 由於空格字元可以半形 (SBCS) 或全形 (DBCS) Unicode 字元集來表示，因此是「特殊大小寫」。 在關聯式引擎中，兩個以空格分隔的複合字串 (一個使用 SBCS，另一個使用 DBCS) 會視為相同。 在 Analysis Services 中，兩個相同的複合字串在處理期間並不相同，並且第二個執行個體會標示為重複項目。  
  
 如需詳細資訊和建議的解決方法，請參閱 [Unicode 字串中的空格根據定序而有不同的處理結果](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)。  
  
##  <a name="bkmk_recos"></a> 常見的定序建議  
 Analysis Services 一律會顯示所有可用語言和定序的完整清單，而不會依據您所選取的語言篩選定序。 請務必選擇可用的組合。  
  
 某些較常用的定序包含下列清單中的定序。  
  
 您應該將這份清單視為進一步調查的起點，而不是排除其他選項的最終建議。 您可能會發現未特別建議的定序是最適合您資料的定序。 若要驗證資料值是否經過適當地排序和比較，唯一方式是進行徹底測試。 一如往常，請務必在測試定序時，同時執行處理和查詢工作負載。  
  
-   Latin1_General_100_AS 通常會用於使用 [ISO 基本拉丁字母](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet)之 26 個字元的應用程式。  
  
-   包含斯堪地那維亞字母 (例如 ø) 的北歐語言可以使用 Finnish_Swedish_100。  
  
-   東歐語言 (例如俄文) 通常會使用 Cyrillic_General_100。  
  
-   中文語言和定序因地區而異，但通常會是簡體中文或繁體中文。  
  
     在中國和新加坡，Microsoft 支援通常會以簡體中文顯示，並以拼音做為慣用的排序次序。 建議的定序為 Chinese_PRC (適用於 SQL Server 2000)、Chinese_PRC_90 (適用於 SQL Server 2005) 或 Chinese_Simplified_Pinyin_100 (適用於 SQL Server 2008 及更新版本)。  
  
     在台灣，則較常看到繁體中文，且建議的排序次序是依據筆劃數：Chinese_Taiwan_Stroke (適用於 SQL Server 2000)、Chinese_Taiwan_Stroke_90 (適用於 SQL Server 2005) 或 Chinese_Traditional_Stroke_Count_100 (適用於 SQL Server 2008 及更新版本)。  
  
     其他地區 (例如香港特別行政區和澳門特別行政區) 也會使用繁體中文。 在香港特別行政區，還很常會看到 Chinese_Hong_Kong_Stroke_90 (在 SQL Server 2005 上) 的定序。 在澳門特別行政區，也經常會使用 Chinese_Traditional_Stroke_Count_100 (在 SQL Server 2008 及更新版本上)。  
  
-   日文的最常用定序是 Japanese_CI_AS。 Japanese_XJIS_100 可用於支援 [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213)的安裝。 在資料移轉專案中通常會看到 Japanese_BIN2，其資料源自於非 Windows 平台，或源自於 SQL Server 關聯式資料庫引擎以外的資料來源。  
  
     在執行 Analysis Services 工作負載的伺服器上很少會看到 Japanese_Bushu_Kakusu_100。  
  
-   建議針對韓文使用 Korean_100。 雖然 Korean_Wansung_Unicode 在清單中仍然可用，但是它已被取代。  
  
##  <a name="bkmk_objid"></a> 物件識別碼的區分大小寫  
 自 SQL Server 2012 SP2 開始，會強制與定序分開執行物件識別碼的區分大小寫，但行為會視語言而異：  
  
|字集|區分大小寫|  
|---------------------|----------------------|  
|**基本拉丁字母**|以拉丁文字 (26 個英文大小寫字母的任何幾個字母) 表示的物件識別碼會視為區分大小寫，而不論定序為何。 例如，下列物件識別碼會視為相同：54321**abcdef**、54321**ABCDEF**、54321**AbCdEf**。 Analysis Services 會在內部將字串中的字元視為全部大寫，然後執行與語言無關的簡單全半形比較。<br /><br /> 請注意，只有 26 個字元會受到影響。 如果是西歐語言，但使用斯堪地那維亞字元，其他字元不會使用大寫。|  
|**斯拉夫文、希臘文、科普特文、亞美尼亞文**|非拉丁文複合字集的物件識別碼 (例如斯拉夫文) 則一律會區分大小寫。 例如，Измерение 和 измерение 的唯一差異是第一個字母的大小寫，即便如此，這兩個字仍會視為兩個相異值。|  
  
 **物件識別碼的區分大小寫含意**  
  
 只有物件識別碼會受到表格中所述之大小寫行為的影響，物件名稱則不會受到影響。 如果您發現方案效果有所改變 (比較前和比較後 - 安裝SQL Server 2012 SP2 或更新版本之後)，很有可能是處理問題。 查詢不會受到物件識別碼的影響。 針對這兩種查詢語言 (DAX 和 MDX)，公式引擎會使用物件名稱 (而不是識別碼)。  
  
> [!NOTE]  
>  與區分大小寫相關的程式碼變更對於某些應用程式而言向來是個中斷變更。 如需詳細資訊，請參閱 [SQL Server 2016 中 Analysis Services 功能的重大變更](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md) 。  
  
##  <a name="bkmk_test"></a> 使用 Excel、SQL Server Profiler 和 SQL Server Management Studio 測試地區設定  
 測試翻譯時，連接必須指定翻譯的 LCID。 如 [從 SSAS 取得不同的語言並加入 Excel](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx)中所述，您可以使用 Excel 來測試翻譯。  
  
 您可以手動編輯 .odc 檔案加入地區設定識別碼連接字串屬性，來執行這項操作。 請使用 Adventure Works 範例多維度資料庫來試試看。  
  
-   搜尋現有的 .odc 檔案。 當您找到 Adventure works 多維度的檔案時，請以滑鼠右鍵按一下檔案，在 [記事本] 中開啟檔案。  
  
-   將 `Locale Identifier=1036` 新增至連接字串。 儲存並關閉檔案。  
  
-   開啟 Excel | [資料] | [現有連接]。 將清單篩選到只剩下這部電腦上的連接檔案。 尋找 Adventure Works 的連接 (請仔細查看名稱；您可能會有一個以上的連接)。 開啟連接。  
  
     您應該會看到 Adventure Works 範例資料庫中的法文翻譯。  
  
     ![Excel 樞紐分析表使用法文翻譯](../analysis-services/media/ssas-localetest-excel.png "使用法文翻譯的 Excel 樞紐分析表")  
  
 接著，您可以使用 SQL Server Profiler 來確認地區設定。 按一下 `Session Initialize` 事件，然後查看下方文字區域中的屬性清單，尋找 `<localeidentifier>1036</localeidentifier>`。  
  
 在 Management Studio 中，您可以指定伺服器連接的地區設定識別碼。  
  
-   在物件總管 中，選取 [連接]  |  | ，然後按一下 [其他連接參數] **Additional ion Parameters** 索引標籤。  
  
-   輸入 `Local Identifier=1036` ，然後按一下 [連接] 。  
  
-   對 Adventure Works 資料庫執行 MDX 查詢。 查詢結果應該是法文翻譯。  
  
     ![使用 SSMS 中的法文翻譯的 MDX 查詢](../analysis-services/media/ssas-localetest-ssms.png "SSMS 中使用法文翻譯的 MDX 查詢")  
  
##  <a name="bkmk_mdx"></a> 在包含翻譯的方案中撰寫 MDX 查詢  
 翻譯會提供 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件名稱的顯示資訊，但不會翻譯相同物件的識別碼。 可能的話，請使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件的識別碼和索引鍵，而不要使用翻譯的標題和名稱。 例如，針對多維度運算式 (MDX) 陳述式和指令碼，請使用成員索引鍵而不要使用成員名稱，以確保多種語言的可攜性。  
  
> [!NOTE]  
>  您應該記得，不論定序為何，表格式物件名稱一律不會區分大小寫。 相反地，多維度物件名稱會遵循定序的區分大小寫。 由於只有多維度物件名稱會區分大小寫，因此請確定參考多維度物件之所有 MDX 查詢的大小寫都正確。  
  
##  <a name="bkmk_datetime"></a> 撰寫包含日期和時間值的 MDX 查詢  
 下列建議可讓以日期和時間為基礎的 MDX 查詢在不同語言之間的可攜性更高：  
  
1.  **使用數值部分進行比較和運算**  
  
     當您執行月和週中的日比較和運算時，請使用日期和時間的數值部分，而不是對等字串 (例如使用 MonthNumberofYear 而不是 MonthName)。 數值最不會受到語言翻譯差異的影響。  
  
2.  **在結果集中使用對等字串**  
  
     當建立向使用者顯示的結果集時，請考慮使用字串 (例如 MonthName)，如此一來您的多語系觀眾便可受益於您所提供的翻譯。  
  
3.  **針對通用的日期和時間資訊使用 ISO 日期格式**  
  
     某位 [Analysis Services 專家](http://geekswithblogs.net/darrengosbell/Default.aspx) 有這項建議：「針對要傳入 SQL 或 MDX 查詢的任何日期字串，我一律會使用 ISO 日期格式 yyyy-mm-dd，這樣做不僅可避免模擬兩可，且不論用戶端或伺服器的地區設定為何都有效。 我同意當剖析模稜兩可的日期格式時，伺服器應該遵循其地區設定，但我也認為如果您已有一個不開放轉譯的選項時，何不選擇這個選項。」  
  
4.  **使用 Format 函數在任何地區語言設定下強制套用特定格式**  
  
     下列取自論壇文章的 MDX 查詢說明如何使用 [格式]，來傳回特定格式的日期，而不論基礎地區設定為何。  
  

    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 的全球化案例](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [撰寫國際通用的 Transact-SQL 陳述式](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  

