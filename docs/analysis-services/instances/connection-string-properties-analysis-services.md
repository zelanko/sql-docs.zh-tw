---
title: 連接字串屬性 (Analysis Services) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 198f2f184a703f270c4fb52a775c47330c68888b
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563844"
---
# <a name="connection-string-properties-analysis-services"></a>連接字串屬性 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  本主題說明您可能會設定其中一種設計工具 或 系統管理工具，或在建立連接到的用戶端應用程式和查詢 Analysis Services 資料的連接字串中看到的連接字串屬性。 因此，本文內容只涵蓋可用屬性的子集。 完整的清單包含許多伺服器和資料庫屬性，可讓您針對特定應用程式自訂連接，而不必在乎伺服器上設定執行個體或資料庫的方式。  
  
 開發人員若要透過撰寫應用程式的程式碼以建立自訂連接字串，應該檢閱適用於 ADOMD.NET 用戶端的 API 文件以檢視更詳細的清單： <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 本主題描述的是 Analysis Services 用戶端程式庫 (即 ADOMD.NET、AMO 及 OLE DB Provider for Analysis Services) 所使用的屬性。 大部分的連接字串屬性均可搭配所有三套用戶端程式庫使用。 例外狀況將於描述中提出。
  
> [!NOTE]  
>  設定屬性時，如果您不慎設定了兩次相同的屬性，則會使用連接字串中的最後一項。  
  
 如需有關如何在現有的 Microsoft 應用程式中指定 Analysis Services 連接的詳細資訊，請參閱[從用戶端應用程式連接 &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)。  
  
##  <a name="bkmk_common"></a> 常用的連接參數  
 下表描述建立連接字串時最常用的屬性。  
  
|屬性|描述|範例|  
|--------------|-----------------|-------------|  
|**Data Source** 或 **DataSource**|指定伺服器執行個體。 此屬性是所有連接的必要項。 有效值包括伺服器的網路名稱或 IP 位址、本機連接的 local 或 localhost 值、設定為 HTTP 或 HTTPS 存取之伺服器的 URL，或是本機 Cube (.cub) 檔案的名稱。 <br /><br /> 有效的值，Azure Analysis services， `<protocol>://<region>/<servername>` region 通訊協定是字串 asazure，是在伺服器建立所在的 Uri (例如 westus.asazure.windows.net)，servername 是您在區域內的唯一伺服器的名稱。 |`Data source=asazure://westus.asazure.windows.net/myasserver`<br /><br />`Data source=AW-SRV01` 代表預設執行個體及通訊埠 (TCP 2383)。<br /><br /> `Data source=AW-SRV01$Finance:8081` 代表具名執行個體 ($Finance) 及固定連接埠。<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` 代表完整網域名稱，假設是預設執行個體及通訊埠。<br /><br /> `Data source=172.16.254.1` 代表伺服器的 IP 位址，略過 DNS 伺服器查閱，對於疑難排解連接問題相當實用。|  
|**Initial Catalog** 或 **Catalog**|指定要連接的 Analysis Services 資料庫的名稱。 資料庫必須部署在 Analysis Services 上，而且您必須具有連接到該資料庫的權限。 此屬性對於 AMO 連接而言為選擇項，但卻是 ADOMD.NET 的必要項。|`Initial catalog=AdventureWorks2016`|  
|**提供者**|有效值包括 MSOLAP。\<版本 >，其中\<版本 > 是 4、 5、 6 或 7。<br /><br /> -   MSOLAP.4 是隨 SQL Server 2008 發行，並在 SQL Server 2008 R2 再度發行 (SQL Server 2008 和 2008 R2 中的檔案名稱為 msolap100.dll)<br />-   MSOLAP.5 是隨 SQL Server 2012 發行 (檔案名稱為 msolap110.dll)<br />-   MSOLAP.6 是隨 SQL Server 2014 發行 (檔案名稱為 msolap1200.dll)<br />-   MSOLAP.7 是隨 SQL Server 2016 發行 (檔案名稱為 msolap130.dll)<br /><br /> 此屬性是選擇項。 依預設，用戶端程式庫會從登錄讀取目前版本的 OLE DB 提供者。 只有在需要特定版本的資料提供者 (例如要連接到 SQL Server 2012 執行個體) 時，才需要設定此屬性。<br /><br /> MSOLAP.4 是隨 SQL Server 2008 及 SQL Server 2008 R2 發行。 2008 R2 版支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，有時候必須在 SharePoint 伺服器上手動安裝此版本。 若要區別這些版本，您必須檢查提供者檔案內容中的組建編號：移至 Program files\Microsoft Analysis Services\AS OLEDB\10。 以滑鼠右鍵按一下 msolap110.dll，然後選取 **[內容]**。 按一下 **[詳細資料]**。 檢視檔案版本資訊。 此版本應該包含 10.50.<buildnumber>。\<組建編號 > 適用於 SQL Server 2008 R2。 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859) 和 [用於 Analysis Services 連接的資料提供者](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)。|`Provider=MSOLAP.7` 的適用對象為需要 SQL Server 2016 版 OLE DB Provider for Analysis Services 的連接。|  
|**Cube**|Cube 名稱或檢視方塊名稱。 資料庫可能包含多個 Cube 和檢視方塊。 如果可能會有多重目標，請在連接字串中加入 Cube 或檢視方塊的名稱。|`Cube=SalesPerspective` 表示您可以使用 Cube 連接字串屬性指定 Cube 的名稱或檢視方塊的名稱。|  
  
##  <a name="bkmk_auth"></a> 驗證和安全性  
 本節包含與驗證及加密相關的連接字串屬性。 Analysis Services 僅使用 Windows 驗證，但是您可以在連接字串中設定屬性，傳入特定的使用者名稱與密碼。  
  
 屬性是依照字母順序列出。  
  
|屬性|描述|  
|--------------|-----------------|  
|**EffectiveUserName**|當伺服器上必須模擬使用者識別時使用。 以「網域\使用者」的格式指定帳戶。 若要使用此屬性，呼叫端必須具有 Analysis Services 的系統管理權限。 如需有關從 SharePoint 的 Excel 活頁簿中使用此屬性的資訊，請參閱＜ [在 SharePoint Server 2013 中使用 Analysis Services EffectiveUserName](http://go.microsoft.com/fwlink/?LinkId=311905)＞。 如需有關如何搭配 Reporting Services 使用此屬性的說明，請參閱 [使用 EffectiveUserName 在 SSAS 中模擬](http://go.microsoft.com/fwlink/?LinkId=301385)。<br /><br /> **EffectiveUserName** 是在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝中用於擷取使用方式資訊。 使用者識別會提供給伺服器，從而可將包含使用者識別的事件或錯誤記錄於記錄檔。 就 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]而言，它並非用於授權用途。|  
|**加密密碼**|指定是否使用本機密碼加密本機 Cube。 有效值為 True 或 False。 預設值是 False。|  
|**加密密碼**|用於將已加密的本機 Cube 解密的密碼。 預設值為空白。 使用者必須明確設定此值。|  
|**模擬等級**|指出伺服器模擬用戶端時，允許伺服器使用的模擬層級。 有效值包括：<br /><br /> -   Anonymous (匿名)。 用戶端對伺服器而言是匿名。 伺服器處理序無法取得有關用戶端的資訊，也無法模擬用戶端。<br />-   Identify (識別)。 伺服器處理序可以取得用戶端識別。 伺服器能夠基於授權目的模擬用戶端識別，但無法以用戶端的身分存取系統物件。<br />-   Impersonate (模擬)。 這是預設值。 只有在建立連接時才可以模擬用戶端識別，而非每一次呼叫都能模擬。<br />-   Delegate (委派)。 伺服器處理序可在代表用戶端時模擬用戶端安全性內容。 伺服器處理序也可以在代表用戶端期間對其他伺服器發出連出呼叫。|  
|**整合式安全性**|使用呼叫端的 Windows 識別連接到 Analysis Services。 有效值為空白、SSPI 和 BASIC。<br /><br /> **Integrated Security**=**SSPI** 是 TCP 連接的預設值，允許 NTLM、Kerberos 或匿名驗證。 空白是 HTTP 連接的預設值。<br /><br /> 使用 **SSPI**時， **ProtectionLevel** 必須設定為下列其中一項： **Connect**、 **PktIntegrity**、 **PktPrivacy**。|  
|**保存加密**|當用戶端應用程式需要由資料來源物件以加密形式保存機密的驗證資訊如密碼時，請設定此屬性。 預設情況下並不會保存驗證資訊。|  
|**保存安全性資訊**|有效值為 True 和 False。 設定為 True 時，一旦建立連接之後，即可從連接取得先前在連接字串中指定的使用者識別或密碼等安全性資訊。 預設值是 False。|  
|**保護層級**|決定連接所使用的安全性層級。 有效值為：<br /><br /> -   **無**。 未驗證或匿名連接。 對傳送到伺服器的資料不執行驗證。<br />-   **連接**。 驗證的連接。 只有在用戶端與伺服器建立關聯性時才會驗證。<br />-   **Pkt Integrity**。 加密的連接。 確認所有資料都是接收自用戶端，而且資料在傳輸過程中未遭到變更。<br />-   **Pkt Privacy**。 經簽署的加密，僅限 XMLA 支援此選項。 確認所有資料都是接收自用戶端，而且資料在傳輸過程中未遭到變更，並透過資料加密保護資料的隱私。<br /><br /> 如需詳細資訊，請參閱＜ [Establishing Secure Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md)＞|  
|**角色**|指定預先定義的角色以逗號分隔的清單，以便使用該角色所傳達的權限連接到伺服器或資料庫。 如果省略此屬性，則會使用所有角色，而且有效權限將是所有角色權限的組合。 將此屬性設定為空值 (例如 Roles=' ') 時，用戶端連接即不具備任何角色成員資格。<br /><br /> 系統管理員使用此屬性連接時將使用其角色所傳達的權限。 如果角色未提供足夠的權限，某些命令可能會失敗。|  
|**SSPI**|當 **Integrated Security** 設定為 **SSPI**時，明確指定哪一種安全性封裝用於用戶端驗證。 SSPI 支援多種封裝，但是您可以使用這個屬性來指定特定封裝。 有效的值為：交涉、Kerberos、NTLM 和匿名使用者。 如果未設定此屬性，所有封裝都將可供連接使用。|  
|**使用加密資料**|將資料傳輸加密。 有效值為 True 和 False。|  
|**User ID**=…; **Password**=|**User ID** 是與 **Password** 搭配使用。 Analysis Services 會模擬透過這些認證所指定的使用者識別。 只有當伺服器設定為 HTTP 存取，而且您針對 IIS 虛擬目錄指定了基本驗證而非整合式安全性時，才會使用透過命令列為 Analysis Services 連接提供認證的方式。 當直接連接到伺服器時，會忽略 **UserID** 和 **Password** 連接字串參數，並且會使用已登入之使用者的內容建立連接。 <br /><br />使用者名稱與密碼必須是 Windows 識別 (本機或網域使用者帳戶) 的認證。 請注意 **User ID** 有內嵌的空格。 此屬性的其他別名包括 **UserName** (不含空格) 和 **UID**。 **Password** 的別名則是 **PWD**。|  
  
##  <a name="bkmk_special"></a> 特殊用途的參數  
 本節描述其餘的連接字串參數。 這些參數是用於確保應用程式所需的特定連接行為。  
  
 屬性是依照字母順序列出。  
  
|屬性|描述|  
|--------------|-----------------|  
|**應用程式名稱**|設定與連接相關聯的應用程式名稱。 此值有助於監視追蹤事件，尤其是多個應用程式存取相同資料庫的情況。 例如，在連接字串中加入 Application Name='test' 會使 SQL Server Profiler 追蹤內出現 'test'，如以下螢幕擷取畫面所示：<br /><br /> ![SSAS_AppNameExcample](../../analysis-services/instances/media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> 此屬性的別名包括 **sspropinitAppName**和 **AppName**。 如需詳細資訊，請參閱 [連接到 SQL Server 時使用 Application Name 參數](http://go.microsoft.com/fwlink/?LinkId=301699)。|  
|**AutoSyncPeriod**|設定用戶端與伺服器快取同步處理的頻率 (以毫秒為單位)。 ADOMD.NET 會為記憶體負擔最低的常用物件提供用戶端快取功能。 這有助於減少與伺服器之間的往返次數。 預設值為 10000 毫秒 (或 10 秒)。 如果設定為 null 或 0，則會關閉自動同步處理。|  
|**字元編碼**|定義隨要求送出的字元編碼方式。 有效值為 Default 或 UTF-8 (此兩者同義) 和 UTF-16。| 
|**CommitTimeout**|XMLA 屬性。 決定在復原之前，目前執行中命令的認可階段等候時間長度 (以毫秒為單位)。 大於 0 時，會覆寫伺服器組態中對應 CommitTimeout 屬性的值。 |   
|**CompareCaseSensitiveStringFlags**|針對指定的地區設定，調整區分大小寫的字串比較。 如需有關設定此屬性的詳細資訊，請參閱 [CompareCaseSensitiveStringFlags 屬性](http://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx)。|  
|**壓縮等級**|如果 **TransportCompression** 是 XPRESS，您就可以設定壓縮層級控制所使用的壓縮程度。 有效值為 0 到 9，其中 0 的壓縮程度最低，而 9 的壓縮程度最高。 壓縮程度提高會降低效能。 預設值是 0。|  
|**連接逾時**|決定用戶端嘗試連接直到逾時的最大時間量 (以秒為單位)。若未在此期限內連接成功，用戶端便會停止嘗試連接並且產生錯誤。|  
|**DbpropMsmdRequestMemoryLimit**|此屬性會覆寫[Memory\QueryMemoryLimit](../server-properties/memory-properties.md)連接的伺服器屬性值。 指定此選項，以 kb 為單位。 |
|**MDX 相容性**|此屬性的目的是確保發出 MDX 查詢的應用程式有整套一致的 MDX 行為。 Excel 即是使用 MDX 查詢以填入和計算連接至 Analysis Services 的樞紐分析表，藉由將此屬性設定為 1 可確保在樞紐分析表內看得到不完全階層中的預留位置成員。 有效值包括 0、1 和 2。<br /><br /> 0 和 1 會公開預留位置成員，而 2 則否。 如果留空，則假設為 0。|  
|**MDX Missing Member Mode=Error**|指出是否要在 MDX 陳述式中忽略遺漏的成員。 有效值為 Default、Error 和 Ignore。 Default 會使用伺服器定義的值。 Error 將於成員不存在時產生錯誤。 Ignore 指定應該忽略遺漏的值。|  
|**最佳化回應**|指出已啟用下列哪幾項查詢回應最佳化的位元遮罩。<br /><br /> -   0x01 使用 NormalTupleSet (這是預設值)<br />-   0x02 當交叉分析篩選器空白時使用|  
|**封包大小**|網路封包大小 (以位元組為單位)，介於 512 和 32,767 之間。 預設的網路封包大小為 4096。|  
|**通訊協定格式**|設定傳送到伺服器的 XML 格式。 有效值為 Default、XML 或 Binary。 通訊協定是 XMLA。 您可指定以壓縮形式 (這是預設值)、原始 XML 形式或二進位格式傳送 XML。 二進位格式會將 XML 元素及屬性編碼成較小的形式。 壓縮是一種專屬格式，會進一步縮減要求和回應的大小。 使用壓縮和二進位格式可以加速資料傳輸要求與回應。<br /><br /> 如果使用二進位或壓縮格式，就必須使用連接的用戶端程式庫。 OLE DB 提供者可將要求和回應格式化為二進位或壓縮格式。 AMO 和 ADOMD.NET 會將要求格式化為文字，但所接受的回應為二進位或壓縮格式。<br /><br /> 此連接字串屬性相當於 **EnableBinaryXML** 和 **EnableCompression** 伺服器組態設定。|  
|**即時 OLAP**|設定此屬性以略過快取，使所有分割區主動接聽查詢通知。 此屬性依預設為未設定。|  
|**安全選項**|設定使用者定義函數和動作的安全性層級。 有效值為 0、1、2。 在 Excel 連接中，此屬性是 Safety Options=2。 這個選項的詳細資訊可在 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。|  
|**SQLQueryMode**|指定 SQL 查詢是否包含計算。 有效值為 Data、Calculated 和 IncludeEmpty。 Data 表示不允許計算。 Calculated 則允許計算。 IncludeEmpty 允許查詢結果傳回計算和空的資料列。|  
|**逾時**|指定用戶端程式庫在產生錯誤之前等候命令完成的時間 (以秒為單位)。|  
|**傳輸壓縮**|當透過 **Protocol Format** 屬性指定壓縮時，定義用戶端與伺服器通訊的壓縮方式。 有效值為 Default、None、Compressed 和 **gzip**。 Default 表示對 TCP 不壓縮，或對 HTTP 進行 **gzip** 壓縮。 None 表示不使用壓縮。 Compressed 會使用 XPRESS 壓縮 (SQL Server 2008 及更新版本)。 **gzip** 僅適用於 HTTP 連接，其中 HTTP 要求包含 Accept-Encoding=gzip。|  
|**UseExistingFile**|連接到本機 Cube 時使用。 此屬性指定是否要覆寫本機 Cube。 有效值為 True 或 False。 如果設定為 True，則 Cube 檔案必須已存在。 現有的檔案將是連接的目標。 如果設定為 False，便會覆寫 Cube 檔案。|  
|**VisualMode**|設定此屬性可控制在套用維度安全性的情況下彙總成員的方式。<br /><br /> 如果是允許每個人查看的 Cube 資料，彙總所有成員就有意義，因為分攤總計的所有值全都可見。 不過，若您根據使用者識別對維度進行篩選或限制，則顯示以所有成員為準的總計 (將限制和允許的值併入單一總計) 可能會造成混淆或顯示本不應揭露的資訊。<br /><br /> 若要指定在套用維度安全性的情況下彙總成員的方式，您可以將此屬性設定為 True 讓彙總只使用允許的值，或設定為 False 讓總計排除限制的值。<br /><br /> 透過連接字串設定時，此值將套用至 Cube 或檢視方塊層級。 而在模型內，您可以控制更細微層級的視覺化總計。<br /><br /> 有效值為 0、1 和 2。<br /><br /> -   0 是預設值。 目前，預設的行為相當於 2，也就是彙總包含了對使用者隱藏的值。<br />-   1 會從總計排除隱藏的值。 此為 Excel 的預設值。<br />-   2 會將隱藏的值納入總計。 這是伺服器上的預設值。<br /><br /> 此屬性的別名包括 **Visual Total** 或是 **Default MDX Visual Mode**。|  
  
##  <a name="bkmk_reserved"></a> 保留供日後使用  
 下列屬性可用於連接字串中，但對目前的 Analysis Services 版本沒有任何作用。  
  
-   已驗證的使用者  
  
-   快取驗證  
  
-   快取模式 (以往的版本曾調查過這個屬性的適用性。 您可能會發現有些部落格文章建議使用，但除非已有 Microsoft 支援人員指示，請盡量避免設定此屬性)。  
  
-   快取原則  
  
-   快取比率  
  
-   快取比率 2  
  
-   動態偵錯限制  
  
-   偵錯模式  
  
-   [模式]  
  
-   SQLCompatibility  
  
-   使用公式快取  
  
##  <a name="bkmk_examples"></a> 範例連接字串  
 本節示範常用的應用程式在設定 Analysis Services 連接時使用機率最高的連接字串。  
  
 **泛用連接字串**  
  
 如果您要設定來自 Reporting Services 的連接，可能就會使用類似以下的連接字串。  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Excel 中的連接字串**  
  
 Excel 中預設的 ADOMD.NET 連接字串會指定資料提供者、伺服器、資料庫名稱及 Windows 整合式安全性。 MDX 相容性層級一定會設定為 1。 雖然您可以變更目前工作階段的值，但是當下一次開啟此檔案時，Excel 會將 MDX 相容性重設為 1。  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 如需詳細資訊，請參閱[資料連接、資料來源與連接字串 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 和 [SharePoint Server 2013 的 Excel Services 資料驗證](http://go.microsoft.com/fwlink/?LinkId=296350)。  
  
##  <a name="bkmk_supportedstrings"></a> Analysis Services 中使用的連接字串格式  
 本節列出 Analysis Services 支援的所有連接字串格式。 除了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫的連接之外，您可以在應用程式中指定連接至 Analysis Services 的這些連接字串。  
  
 **伺服器的原生 (或直接) 連接**  
  
 `Data Source=server[:port][\instance]` ，其中 “port” 和 “\instance” 是選擇性的。 例如，指定 “Data Source=server1” 會在名稱為 “server1” 的伺服器上開啟預設執行個體 (以及預設通訊埠 2383) 的連接。  
  
 “Data Source=server1:port1” 將開啟在 “server1” 的通訊埠 “port1” 上執行之 Analysis Services 執行個體的連接。  
  
 “Data Source=server1\instance1” 將會開啟 SQL Browser (在其預設通訊埠 2382 上) 的連接、解析具名執行個體 “instance1” 的通訊埠，然後開啟該 Analysis Services 通訊埠的連接。  
  
 “Data Source=server1:port1\instance1” 將會開啟 “port1” 上 SQL Browser 的連接、解析具名執行個體 “instance1” 的通訊埠，然後開啟該 Analysis Services 通訊埠的連接。  
  
 **本機 Cube 連接 (.cub 檔)**  
  
 `Data Source=<path>`，例如 “Data Source=c:\temp\a.cub”  
  
 **msmdpump.dll 的 Http(s) 連接**  
  
 `Data Source=<URL>`，其中 URL 是包含 msmdpump.dll 之虛擬 IIS 資料夾的 HTTP 或 HTTPS 位址。 如需詳細資訊，請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿 (.xlsx、.xlsb 或 .xlsm 檔案) 的 Http(s) 連接**  
  
 `Data Source=<URL>`，其中 URL 是已發行至 SharePoint 文件庫之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的 SharePoint 路徑。 例如， `Data Source=http://localhost/Shared Documents/Sales.xlsx` 。  
  
 **BI 語意模型連接檔案的 Http(s) 連接**  
  
 `Data Source=<URL>` ，其中 URL 是 .bism 檔案的 SharePoint 路徑。 例如， `Data Source=http://localhost/Shared Documents/Sales.bism` 。  
  
 **內嵌的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 連接**  
  
 `Data Source=$Embedded$` 其中 $embedded$ 是參考活頁簿內部內嵌之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料模型的 Moniker。 此連接字串是在內部建立並管理。 請勿修改該字串。 內嵌的連接字串是由用戶端工作站上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 增益集，或 SharePoint 伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 執行個體所解析。  
  
 **Analysis Services 預存程序中的本機伺服器內容**  
  
 `Data Source=*`，其中 * 會解析為本機執行個體。  
  
##  <a name="bkmk_encrypt"></a> 加密連接字串  
 Analysis Services 會使用本身的加密金鑰來加密連接字串。 它不會產生自我簽署憑證。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會加密和儲存用來連接到每一個資料來源的連接字串。 如果資料來源的連接需要使用者名稱和密碼，您可以選擇讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在連接字串中儲存名稱和密碼，或每次需要連接資料來源時提示您輸入名稱和密碼。 讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提示您輸入使用者資訊，表示此資訊不必儲存和加密。 不過，如果您在連接字串中儲存此資訊，則此資訊需要加密和保護。  
  
 若要加密並保護連接字串資訊安全， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用資料保護 API。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用個別的加密金鑰來加密每個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的連接字串資訊。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會建立此金鑰，並依據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 啟動帳戶來加密連接字串資訊。 當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 啟動時，會讀取、解密並儲存每個資料庫的加密金鑰。 之後，當[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 需要連接到資料來源時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用適當的解密金鑰來解密資料來源連接字串資訊。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [設定 Analysis Services 進行 Kerberos 限制委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [用於 Analysis Services 連接的資料提供者](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)   
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
