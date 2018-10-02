---
title: 資料庫專案設定 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DebugProperties
- sql.data.tools.dacsettings.dialog
- sql.data.tools.dbsqlclrlanguagevb
- SQL.DATA.TOOLS.DBADVANCEDBUILDSETTINGSCS
- sql.data.tools.dbadvancedbuildsettingscs
- ql.data.tools.criticalerror.dialog
- sql.data.tools.dbassemblysigningchangekeypassword
- sql.data.tools.advanceddeploymentsystemdefined.dialog
- sql.data.tools.advanceddatabasesettings.dialog
- sql.data.tools.extendedpropertiesvalueeditor.dialog
- sql.data.tools.dbsqlclrlanguagecs
- ql.data.tools.dbassemblysigningpasswordneeded
- sql.data.tools.vbadvancedsettings.dialog
- sql.data.tools.dbsqlclr
- sql.data.tools.SqlCmdVariablesProperties
- sql.data.tools.dbassemblysigning
- sql.data.tools.advanceddeploymentsettings.dialog
- sql.data.tools.advancedpublishsettings.dialog
- sql.data.tools.BuildActionProperties
- sql.data.tools.serverselectionpolicy.dialog
- sql.data.tools.dbadvancedbuildsettingsvb
- sql.data.tools.dbprojectwizard.buildeventcommandline
- sql.data.tools.dbreferencepaths
- sql.data.tools.GeneralProperties
- sql.data.tools.BuildProperties
- sql.data.tools.DeployProperties
- sql.data.tools.csadvancedsettings.dialog
- sql.data.tools.dbassemblyinfo
- sql.data.tools.extendedpropertieseditor.dialog
ms.assetid: 34418730-1aaa-4948-aee2-8f1e62cda85c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f05341938208dc0459afda8de77bb85b5f5efd6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636967"
---
# <a name="database-project-settings"></a>資料庫專案設定
您可以使用資料庫專案設定，控制資料庫、偵錯與組建組態的各個部分。 這些設定可分類如下：  
  
-   [專案設定](#bkmk_proj_settings)  
  
-   [擴充的 Transact-SQL 驗證](#bkmk_evf)  
  
-   [SQLCLR](#bkmk_sqlclr)  
  
-   [SQLCLR 與 SQLCLR 建置](#bkmk_sqlclr_sqlclrbuild)  
  
-   [建置](#bkmk_build)  
  
-   [SQLCMD 變數](#bkmk_sqlcmd_variables)  
  
-   [建置事件](#bkmk_build_events)  
  
-   [偵錯](#bkmk_debug)  
  
-   [參考路徑](#bkmk_ref_paths)  
  
-   [程式碼分析](#bkmk_code_analysis)  
  
### <a name="to-configure-properties-for-your-database-project"></a>若要設定資料庫專案的屬性  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下要為其設定屬性的資料庫專案，然後選取 [屬性]。  
  
    或者，按兩下 [ **方案總管** ] 中專案的 [ **屬性**] 節點。  
  
2.  資料庫專案的屬性工作表隨即出現。  
  
3.  按一下 [ **專案設定** ] 索引標籤。現在您就可以設定資料庫專案屬性的一般屬性。 注意左窗格中各種索引標籤 (代表不同分類) 的可用性。  
  
## <a name="bkmk_proj_settings"></a>專案設定  
下列表格中的設定會套用至這個資料庫專案的所有組態。  
  
|欄位|預設值|Description|  
|---------|-----------------|---------------|  
|目標平台|Microsoft SQL Server 2012|指定這個資料庫專案所設定的目標 SQL Server 版本。|  
|為一般物件啟用擴充的 Transact\-SQL 驗證。|當您建立新專案時，不會啟用。<br /><br />當您從 [SQL Server 物件總管] 連接至 SQL Azure 以建立專案、將 SQL Azure 資料庫匯入專案或將專案的目標平台變更為 SQL Azure 時，則會啟用。|一旦啟用此選項，將報告在專案中所發現造成 SQL Server 編譯器驗證失敗的錯誤。 如果您將目標平台變更為 SQL Azure，擴充驗證就會變成啟用狀態。 儘管您變更目標平台，也不會取消勾選此選項。<br /><br />您可以對其他版本的 SQL Server 啟用此選項，但是驗證只限於 Microsoft SQL Server 2012 部分自主資料庫和 SQL Azure。 並非所有 SQL Server 版本都支援全部的 Transact\-SQL 語法。<br /><br />如需詳細資訊，請參閱本主題稍後的[擴充的 Transact-SQL 驗證](#bkmk_evf)|  
|輸出類型|||  
|資料層應用程式 (.dacpac 檔案)|已啟用並鎖定。 建置資料庫專案時，專案的建置輸出一定會產生 .dacpac 封裝。|如果您正在使用具有 [建立其他下層 .dacpac 檔案 (v2.0)] 選項的 SQL Server Data Tools (SSDT) 版本，而且希望套件能與 SQL Server Management Studio 或 SQL Azure 管理入口網站相容，請選取該選項。 您可以直接從 (SSDT) 部署 .dacpac 套件，但在 SQL Server Data Tools 正式發行後，透過 SQL Server Management Studio 只能部署 2.0 版 .dacpac 檔案。|  
|建立指令碼 (.sql 檔案)||指定是否要為專案中的所有物件產生整段 .sql CREATE 指令碼，並在建置專案時將指令碼放入 bin\debug 資料夾。 您可以使用 **[專案發行]** 命令或 SQL 比較公用程式來建立累加更新指令碼。|  
|泛型|||  
|預設的結構描述|dbo|指定用以同時建立 SQLCLR 和 Transact\-SQL 物件的預設結構描述。 您可藉由直接為物件指定結構描述以覆寫此設定。|  
|在檔案名稱中包含結構描述名稱|否|指定檔案名稱中是否需包含結構描述做為前置詞 (例如 dbo.Products.table.sql)。 如果取消選取此核取方塊，則物件的檔案名稱格式為 ObjectName.ObjectType.sql (例如 Products.table.sql)。|  
|驗證識別項的大小寫。|是|指定是否要在建置專案時驗證專案中各個 SQL 物件識別項的大小寫。 此選項適用於指定資料庫定序區分大小寫的資料庫專案。|  
|資料庫設定|由資料庫的標準組態設定所決定的預設值。|可供指定的幾項設定，例子包括 SQL Server 資料庫的定序方法和資料庫層級設定等。|  
  
## <a name="bkmk_evf"></a>擴充的 Transact-SQL 驗證  
  
> [!IMPORTANT]  
> 擴充的 Transact-SQL 驗證功能將從 SQL Server Data Tools 的下一個功能版本以及 Visual Studio 的下一個主要版本中移除。  
  
擴充的 Transact-SQL 驗證是資料庫專案系統中的一項功能，可讓開發人員在建置階段將其資料庫專案提交至 Transact-SQL Compiler Service，以便根據 SQL Server 引擎的剖析器和解譯器驗證程式碼。  
  
### <a name="transact-sql-compiler-service"></a>Transact-SQL Compiler Service  
Transact-SQL 編譯器服務是以 Microsoft SQL Server 2012 資料庫引擎為基礎的元件。 這項服務可以驗證 DDL 陳述式的語法和語意，而且其精確度與 Microsoft SQL Server 2012 資料庫引擎相同。 這也就表示編譯器服務不支援 Microsoft SQL Server 2012 中已淘汰的語法或功能。 如需已取代功能的詳細資訊，請參閱 [SQL Server 2012 中已中止的資料庫引擎功能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)。  
  
為了驗證資料庫專案，Compiler Service 會建立部分自主資料庫並且根據該資料庫模擬 DDL 陳述式的執行。 如需詳細資訊，請參閱 [部分自主資料庫](http://msdn.microsoft.com/en-us/library/ff929071%28v=SQL.110%29.aspx)。  
  
Compiler Service 具有兩種限制分類。  
  
仰賴資料庫或執行個體組態的功能，包括：  
  
-   3 或 4 部分物件參考  
  
-   FileTable  
  
-   變更追蹤  
  
-   資料列集函式 - OPENROWSET、OPENQUERY、OPENDATASOURCE  
  
-   全文檢索語意搜尋  
  
目前不支援驗證的功能，包括：  
  
-   Service Broker  
  
-   具有使用者定義檔案群組的資料分割結構描述  
  
-   SQL Azure 中繼資料定序 (Compiler Service 會使用 SQL Server 2012 部分自主資料庫中繼資料定序 - Latin1_General_100_CI_AS_KS_WS_SC)  
  
### <a name="enablingdisabling-extended-verification"></a>啟用/停用擴充驗證  
直接從 SQL Azure 資料庫建立的資料庫專案或其目標平台設定為 SQL Azure 的專案預設會啟用擴充的 Transact-SQL 驗證。 針對 SQL Azure 或是以 SQL Server 2012 為目標的應用程式範圍資料庫進行開發時，建議您使用擴充驗證。 如需應用程式範圍資料庫的詳細資訊，請參閱 [部分自主資料庫](http://msdn.microsoft.com/en-us/library/ff929071%28v=SQL.110%29.aspx)。  
  
此外，當您開發 SQL Server 2008/R2 的應用程式範圍資料庫時，也可以使用擴充驗證功能，以達到與 Microsoft SQL Server 2012 和 SQL Azure 相容的目的。  
  
##### <a name="to-enable-or-disable-extended-verification-at-the-project-level"></a>若要在專案層級啟用或停用擴充驗證  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。  
  
2.  在 [專案設定] 的 [目標平台] 底下，選取或取消選取 [啟用一般物件的擴充 Transact-SQL 驗證]。  
  
##### <a name="to-disable-extended-verification-at-the-file-level"></a>若要在檔案層級停用擴充驗證  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下 .sql 檔案。  
  
    > [!NOTE]  
    > 若要在檔案層級停用擴充的 Transact\-SQL 驗證功能，檔案的 [建置動作] 屬性必須設定為 [建置]。  
  
2.  在 [屬性] 中，將 [擴充的 T-SQL 驗證] 屬性變更為 [False]。  
  
![檔案屬性](../ssdt/media/ssdt-evf.gif "檔案屬性")  
  
### <a name="special-considerations-for-collations"></a>定序的特殊考量  
如需部分自主資料庫中之定序的詳細資訊，請參閱 [自主資料庫定序](http://msdn.microsoft.com/en-us/library/ff929080%28v=sql.110%29.aspx)。  
  
## <a name="bkmk_sqlclr"></a>SQLCLR  
如需組件選項的詳細資訊，請參閱 [組件資訊對話方塊](http://msdn.microsoft.com/en-us/library/1h52t681.aspx?queryresult=true)。  
  
如需簽署的詳細資訊，請參閱 **專案設計工具、簽署頁** 主題的＜ [組件簽署](http://msdn.microsoft.com/en-us/library/0k50fs3b.aspx?queryresult=true) ＞一節。  
  
## <a name="bkmk_sqlclr_sqlclrbuild"></a>SQLCLR 與 SQLCLR 建置  
**[SQLCLR]** 和 **[SQLCLR 建置]** 屬性頁包含許多在專案中使用 SQL CLR 物件的設定。 具體來說， **[SQLCLR]** 屬性頁含有權限等級設定，可設定對 SQLCLR 組件的權限。 此頁亦提供「產生 DDL」設定，可控制是否要為已加入至專案的 SQLCLR 物件產生動態資料語言 (DDL)。 **[SQLCLR 建置]** 屬性頁包含所有的編譯器選項，可用來設定專案中 SQLCLR 程式碼的編譯組態。  
  
**[SQLCLR 建置]** 屬性頁包含了建置 SQL CLR 物件時所用的進階建置設定。 根據 (VB or C#) 用於撰寫 SQL CLR 物件程式碼的語言而定，提供的選項有所不同。  
  
1.  如果物件是以 C# 撰寫，您可以按一下 [SQLCLR 建置] 屬性頁中的 [進階] 按鈕來存取選項。 C# 選項的描述可以在[進階建置設定對話方塊 (C#)](http://msdn.microsoft.com/en-us/library/s4wcexbc.aspx) 找到。  
  
2.  如果以 VB 撰寫物件，您可以先在 **[語言]** 中選擇 VB，然後按一下 **[進階]** 。 VB 選項的描述可以在[進階編譯器設定對話方塊 (Visual Basic)](http://msdn.microsoft.com/en-us/library/07bysfz2.aspx) 找到  
  
如需詳細資訊，請參閱[組建組態屬性](http://msdn.microsoft.com/query/dev10.query?appId=Dev10IDEF1&l=EN-US&k=k(CS.PROJECTPROPERTIESBUILD)) \(機器翻譯\)  
  
## <a name="bkmk_build"></a>建置  
您可以為方案中的每一個資料庫專案選擇建置組態。 組態預設只有一個，但是您可以新增自訂組態。 例如，如果您想要使用永遠會刪除並重新建立資料庫的自訂組態，就可以選擇這樣做。 在包含不同專案類型的方案中，可以建立含有個別專案特定建置組態的自訂方案組態。  
  
#### <a name="to-specify-a-build-configuration-for-a-solution"></a>若要指定方案的建置組態  
  
1.  在 [ **方案總管**] 中，按一下要為其指定建置組態的方案節點。  
  
2.  按一下 [ **建置** ] 功能表上的 [ **組態管理員**]。 [ **組態管理員** ] 對話方塊隨即出現。  
  
    指定您要用於方案中每個專案的組態設定。  
  
#### <a name="to-specify-a-build-configuration-for-a-database-project"></a>若要指定資料庫專案的建置組態  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下您要為其指定組建組態的資料庫專案，然後選取 [屬性]。  
  
2.  使用 [ **建置** ] 索引標籤中的 [ **組態** ] 下拉式清單，指定您要用於這個專案的組態設定。  
  
下列表格中的設定會套用至這個資料庫專案的建置組態。  
  
|欄位|預設值|Description|  
|---------|-----------------|---------------|  
|建置輸出路徑|bin\Debug\|指定當您建置或部署資料庫專案時，產生建置輸出的位置。 如果指定相對路徑，您必須指定該路徑會相對於資料庫專案路徑。 如果路徑不存在，則會建立路徑。|  
|建置輸出檔名稱|*DatabaseProjectName*|指定當您建置資料庫專案時，要賦予所產生之輸出的名稱。|  
|將 Transact\-SQL 警告視為錯誤|否|指定出現 Transact\-SQL 警告時是否應取消建置和部署處理程序。 如果已清除此核取方塊，則會出現警告，但是建置和部署程序會繼續進行。 此設定為專案而不是使用者特有的，並儲存在 .sqlproj 檔案中。|  
|隱藏 Transact\-SQL 警告|空白|指定以逗號或分號分隔的警告編號清單，以識別隱藏的警告。<br /><br />即使選取了 [將 Transact\-SQL 警告當成錯誤] 核取方塊，已隱藏的警告也不會出現在 [錯誤清單] 視窗中，而且不會影響建置順利完成。|  
  
## <a name="bkmk_sqlcmd_variables"></a>SQLCMD 變數  
在 SQL Server 資料庫專案中，您可以利用 SQLCMD 變數，提供用於偵錯或發行的動態置換功能。 透過輸入變數名稱和值，這些值將在建置期間遭置換。 若是沒有區域數值，則會使用預設值。 在專案屬性中輸入各個變數後，發行時便會自動提供這些變數，且變數將儲存於發行設定檔。 您可以透過 [載入值] 按鈕，提取專案的變數值將其納入發行。  
  
請確定您在專案屬性中輸入的變數無誤，因為這些變數不會根據專案中的指令碼進行驗證，而指令碼所使用的變數也不會自動填入。  
  
此外，命令列發行方式還可讓您透過命令列或使用設定檔覆寫這些值。  
  
## <a name="bkmk_build_events"></a>建置事件  
您可以使用這些設定指定命令列在建置作業開始前執行，同時指定另一個命令列在建置作業完成後執行。  
  
|欄位|預設值|Description|  
|---------|-----------------|---------------|  
|建置前事件命令列|None|指定建置專案前執行的命令列。 按一下 [建置前進行編輯] 可修改命令列。|  
|建置後事件命令列|None|指定建置專案後執行的命令列。 按一下 [建置後進行編輯] 可修改命令列。|  
|執行建置後事件|建置成功時|指定建置後命令列應永遠執行、只有在建置成功時執行，或只有在建置更新專案輸出 (建置指令碼) 時執行。|  
  
## <a name="bkmk_debug"></a>偵錯  
您可以使用下列設定來控制資料庫專案的偵錯。  
  
|欄位|預設值|Description|  
|---------|-----------------|---------------|  
|啟動執行|None|指定對專案進行偵錯時要執行的指令碼或外部程式。|  
|目標連接字串|Data Source=(localdb)\\*SolutionName*;Initial Catalog=*DatabaseProjectName*;Integrated Security=True;Pooling=False;Connect Timeout=30|指定連接資訊，以連接所指定建置組態的目標資料庫伺服器。 預設連接字串的對象為動態建立的 SQL Server LocalDB 執行個體和資料庫。|  
|部署資料庫屬性|是|指定當您部署資料庫專案時，是否要部署或更新 DatabaseProerties.DatabaseProperties 設定。|  
|永遠重新建立資料庫|否|指定是否要卸除並重新建立資料庫，而不執行累加式升級。 例如，如果要對全新部署的資料庫執行資料庫單元測試，您可能想要選取這個核取方塊。 如果清除這個核取方塊，則會更新現有的資料庫，而不會捨棄並重新建立資料庫。|  
|如果可能發生資料遺失，則封鎖累加部署|是|指定一旦更新導致資料遺失，是否將停止部署。 如果選取這個核取方塊，那麼可能會使資料遺失的變更會導致部署停止並顯示錯誤，以免發生遺失資料的情況。 例如，若 `varchar(50)` 資料行變更為 `varchar(30)`，則會停止部署。<br /><br />**注意：** 只有當可能發生資料遺失的資料表包含資料時，才會封鎖部署。 如果不會遺失任何資料，則會繼續進行部署。|  
|在目標中但不在專案中的 DROP 物件|否|指定如果物件位於目標資料庫但不在資料庫專案內，是否應在部署指令碼執行時捨棄。 您可以排除專案中的某些檔案，以便從組建指令碼中暫時移除這些檔案。 但是，您可以將這些物件的現有版本留在目標資料庫中。 如果選取 [永遠重新建立資料庫] 核取方塊，這個核取方塊不會有任何作用，因為這時會卸除整個資料庫。|  
|請勿使用 ALTER ASSEMBLY 陳述式來更新 CLR 型別|否|指定當您部署變更時，是否要使用 ALTER ASSEMBLY 陳述式來更新 Common Language Runtime (CLR) 型別，或者是否會卸除執行個體化 CLR 型別的物件，然後再重新建立此物件。|  
|進階...|否|此命令按鈕可讓您指定選項以控制事件和部署的行為。|  
  
## <a name="bkmk_ref_paths"></a>參考路徑  
您可以使用這個頁面定義與跨資料庫參考相關的伺服器和資料庫變數。 此外，您也可以指定那些變數的值。 如需詳細資訊，請參閱 [在資料庫專案中使用參考](http://msdn.microsoft.com/en-us/library/bb386242.aspx)。  
  
## <a name="bkmk_code_analysis"></a>程式碼分析  
您可以使用程式碼分析，找出指令碼中的潛在問題，例如設計、命名和效能問題。 資料庫專案的規則會組織成預先定義的規則集，並且以特定方面為目標，您可以在 **[專案屬性]** 屬性頁的 **[程式碼分析]** 索引標籤中啟用或停用任何規則。 在相同索引標籤中，您可以指定要在每次建置專案時自動執行程式碼分析，或指定是否將警告視為錯誤。  
  
若要手動使用程式碼分析，請以滑鼠右鍵按一下 [方案總管] 中的專案，再選取 [執行程式碼分析]。 程式碼分析警告列在 **[錯誤清單]** 視窗中。 按兩下警告即可巡覽至有問題的原始程式碼，而且使用 [顯示錯誤說明] 快顯功能表也可以檢視警告的其他資訊與可能的修正方法。 如需有關程式碼分析的詳細資訊，請參閱 [分析資料庫程式碼以提升程式碼品質](http://msdn.microsoft.com/en-us/library/dd172133.aspx)。  
  
