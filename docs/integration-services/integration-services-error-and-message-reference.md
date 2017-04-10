---
title: "Integration Services 錯誤和訊息參考 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "錯誤代碼 [Integration Services]"
  - "HRESULT [Integration Services]"
  - "錯誤 [Integration Services]，已列出"
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Integration Services 錯誤和訊息參考
  下表列出預先定義的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤、警告和參考用訊息 (依據每一個類別內的遞增號碼順序)，連同這些訊息的數字代碼和符號名稱。 每一個錯誤都會以欄位形式定義於 <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別內。  
  
 當您遇到錯誤碼而沒有描述時，這個清單可能會非常有用。 此清單這次沒有包含疑難排解資訊。  
  
> [!IMPORTANT]  
>  在使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 時所看到的許多錯誤訊息都是來自其他元件。 在本主題中，您會找到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 元件所引發的所有錯誤。 如果您在清單中看不到您的錯誤，表示該錯誤是由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]之外的元件所引發。 這可能包括 OLE DB 提供者、其他的資料庫元件 (例如 [!INCLUDE[ssDE](../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]) 或是其他的服務或元件，例如檔案系統、SMTP 伺服器或 Message Queuing (也稱為 MSMQ) 等等。 若要尋找有關這些外部錯誤訊息的資訊，請參閱該元件的特定文件集。  
  
 此清單包含下列的訊息群組：  
  
-   [錯誤訊息 (DTS_E_*)](#msgError)  
  
-   [警告訊息 (DTS_W_*)](#msgWarning)  
  
-   [參考用訊息 (DTS_I_*)](#msgInfo)  
  
-   [一般和事件訊息 (DTS_MSG_*)](#msgGeneral)  
  
-   [成功訊息 (DTS_S_*)](#msgSuccess)  
  
-   [資料流程元件錯誤訊息 (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> 錯誤訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的符號名稱以 **DTS_E_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|說明|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|正在目的地端覆寫預存程序 "%1"。|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|%3 不支援在資料行 "%2" 找到的 "%1" 資料類型。 此資料行將轉換成 DT_NTEXT。|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|在 XML 結構描述中，資料表 %2 的資料行 %1 在外部中繼資料行中沒有對應。|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|內部物件或變數尚未初始化。 這是內部產品錯誤。  當變數應該包含有效值卻沒有時，就會傳回這個錯誤。|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services 評估期間已過。|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|這個屬性不能指定負值。 當只能包含正值的屬性指定負值時，例如 COUNT 屬性，就會發生這個錯誤。|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|索引不可以是負數。 當使用負值做為集合的索引時，就會發生這個錯誤。|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|無效的伺服器名稱 "%1"。 SSIS 服務不支援多重執行個體，請只使用伺服器名稱，而非 "server name\instance"。|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|無法在 64 位元平台上完成 VSA 指令碼的移轉，因為沒有 Visual Tools for Applications 設計工具支援。 請在 64 位元平台上以 WOW64 執行移轉。|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|命令執行產生錯誤。|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|若要在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 之外執行 SSIS 封裝，您必須安裝 %1 (含) 以上版本的 Integration Services。|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|找不到變數。 在執行封裝期間，嘗試從容器的 Variables 集合擷取變數時，如果此變數不存在，就會發生這個問題。 變數名稱可能已變更或尚未建立變數。|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|嘗試寫入唯讀變數 "%1" 時發生錯誤。|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|找不到包含工作和資料流程工作元件的目錄。 請檢查安裝的完整性。|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|封裝名稱太長。 限制為 128 個字元。 請縮短封裝名稱。|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|封裝描述太長。 限制為 1024 個字元。 請縮短封裝描述。|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments 屬性太長。 限制為 1024 個字元。 請嘗試縮短 VersionComments。|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|在集合中找不到此元素。 在執行封裝期間，當您嘗試從容器的集合擷取元素時，如果這個元素不存在，就會發生這個錯誤。|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|無法從 SQL Server 資料庫載入指定的封裝。|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|變數值指派無效。 當用戶端或工作指派執行階段物件給變數值時，就會發生這個錯誤。|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|指派命名空間給變數時發生錯誤。 命名空間 "System" 保留供系統使用。 當元件或工作嘗試建立命名空間為 "System" 的變數時，就會發生這個錯誤。|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|找不到連接 "%1"。 當找不到特定的連接元素時，Connections 集合就會擲回這個錯誤。|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|變數 "%1" 是 64 位元整數變數，在這個作業系統上不支援。 變數已重新轉換成 32 位元整數。|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|嘗試變更變數 "%1" 的唯讀屬性。 嘗試在執行階段變更變數的唯讀屬性時，就會發生這個錯誤。 只能在設計階段變更唯讀屬性。|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|將變數設定為容器參考的嘗試無效。  不允許變數參考容器。|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|指派無效的值或物件給變數 "%1"。 當值不適用於變數時，就會發生這個錯誤。|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|發生一個或多個錯誤。 在這個解釋錯誤詳細資料的錯誤之前，應該還有其他特定錯誤。 這個訊息用來當做遇到錯誤之函數的傳回值。|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|取得或設定陣列值時發生錯誤。 不允許類型 "%1"。 將陣列載入變數時，就會發生這個問題。|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|陣列包含不支援的類型。 將未支援類型的陣列儲存至變數時，就會發生這個問題。|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|從節點 "%2" 載入值 "%1" 時發生錯誤。|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|節點 "%1" 不是有效節點。 儲存失敗時會發生這個問題。|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|無法載入類型 "%2" 的工作 "%1"。 此工作的連絡資訊是 "%3"。|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|元素 "%1" 不存在於集合 "%2" 中。|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|主控物件的 XML 區塊中遺漏 ObjectData 元素。 當 XML 剖析器嘗試尋找物件的資料元素而找不到時，就會發生這個問題。|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|找不到變數 "%1"。 在執行封裝期間，嘗試從容器的變數集合擷取變數時，如果不存在此變數，就會發生這個錯誤。  變數名稱可能已變更或尚未建立變數。|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|無法執行封裝，因為封裝包含無法載入的工作。|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|無法載入工作。 此工作的連絡資訊是 "%1"。|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|載入工作 "%1" 時發生錯誤。|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|載入工作時發生錯誤。 從 XML 載入工作失敗時，就會發生這個問題。|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|%1 無法寫入快取，因為 %2 已經寫入快取。|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|無法為新資料準備快取。|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|無法將快取標記為已填滿資料。|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|快取未初始化，因此 %1 無法讀取快取。|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|無法為提供的資料準備快取。|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|%1 正在寫入快取，因此 %2 無法讀取快取。|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|正在從 %1 讀取快取，因此 %2 無法寫入快取。|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|無法從指定的 XML 節點載入執行階段物件。  嘗試從類型不正確的 XML 節點 (例如非 SSIS XML 節點) 載入封裝或其他物件時，就會發生這個問題。|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|無法開啟封裝檔案 "%1"，因為錯誤 0x%2!8.8X! 失敗。  當載入封裝但無法在 XML 文件正確開啟或載入時，就會發生這個問題。 可能是因為呼叫 LoadPackage 時指定不正確的檔案名稱，或指定的 XML 檔案格式不正確。|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|無法載入 XML，因為錯誤 0x%1!8.8X! "%2"。 當載入封裝但無法在 XML 文件正確開啟或載入檔案時，就會發生這個問題。  可能是因為提供不正確的檔案名稱給 LoadPackage 方法，或指定的 XML 檔案格式不正確。|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|無法從封裝檔案 "%1" 載入 XML，因為錯誤 0x%2!8.8X! 失敗。  當載入封裝但無法在 XML 文件正確開啟或載入檔案時，就會發生這個問題。 可能是因為提供不正確的檔案名稱給 LoadPackage 方法，或指定的 XML 檔案格式不正確。|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|無法開啟封裝檔案。 當載入封裝但無法在 XML 文件正確開啟或載入檔案時，就會發生這個問題。 可能是因為提供不正確的檔案名稱給 LoadPackage 方法，或指定的 XML 檔案格式不正確。|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|無法解碼封裝中的二進位格式。|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|無法將封裝載入為 XML，因為封裝缺少有效的 XML 格式。 將公佈特定的 XML 剖析器錯誤。|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|從 XML 載入時發生錯誤。 這個問題無法指定進一步的詳細錯誤資訊，因為未傳遞可存放詳細錯誤資訊的 Events 物件。|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|無法建立 XML 文件物件模組 (Document Object Model) 的執行個體。 可能尚未註冊 MSXML。|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|無法載入封裝。 嘗試載入舊版的封裝時，或封裝檔案參考到無效的結構化物件時，就會發生這個問題。|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|無法儲存封裝檔案。|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|無法儲存封裝檔案 "%1"，錯誤為 0x%2!8.8X! 失敗。|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|物件必須繼承自 IDTSName100，但並不是。|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|組態項目 "%1" 的格式不正確，因為開頭不是封裝分隔符號。 沒有 "\package" 分隔符號。|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|組態項目 "%1" 的格式不正確。 可能是因為遺漏分隔符號或格式化錯誤，例如無效的陣列分隔符號。|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|無法匯出組態檔。|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|無法修改屬性集合。|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|無法儲存組態檔。 檔案可能是唯讀的。|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure 屬性不適用於封裝容器。|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|工作 "%1" 無法在已安裝的 Integration Services %2 版本上執行。 它需要 %3 (含) 以上版本。|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|無法將 xml 儲存至 "%1"。 檔案可能是唯讀的。|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|在封裝路徑 "%2" 的組態 "%1" 中無法轉換類型。  當組態值無法從字串轉換成適當的目的地類型時，就會發生這個問題。 請檢查組態值，確定可以轉換成目的地屬性或變數的類型。|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|組態失敗。 這是所有組態類型的一般警告。 在這個警告之前，應該還有其他警告會提供詳細資訊。|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|ExecutePackage 工作發生封裝驗證失敗。 無法執行封裝。|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|無法建立 Mutex "%1"，錯誤為 0x%2!8.8X!。|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" 已經存在，且為另一位使用者所擁有。|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|無法取得 Mutex "%1"，錯誤為 0x%2!8.8X!。|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|無法釋放 Mutex "%1"，錯誤為 0x%2!8.8X!。|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|包裝函數工作指標無效。 包裝函數指向工作的指標無效。|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|可執行檔已經加入另一個容器的 Executables 集合中。 當用戶端嘗試將可執行檔加入一個以上的 Executables 集合中時，就會發生這個問題。 您必須從目前的 Executables 集合移除可執行檔，再嘗試加入。|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|為連接管理員 "%2" 指定的連接類型 "%1" 無法辨識為有效的連接管理員類型。 嘗試為未知的連接類型建立連接管理員時，就會傳回這個錯誤。 請檢查連接類型名稱的拼字。|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|已建立物件，但加入集合中的嘗試失敗。 可能是因為記憶體不足而導致這個情況發生。|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|建立開放式資料庫連接 (Open Database Connectivity，ODBC) 環境時發生錯誤。|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|建立開放式資料庫連接 (Open Database Connectivity，ODBC) 資料庫連接時發生錯誤。|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|嘗試與資料庫伺服器建立開放式資料庫連接 (Open Database Connectivity，ODBC) 時發生錯誤。|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|這個連接管理員執行個體上已設定限定詞。 每個執行個體只能設定一次限定詞。|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|這個連接管理員執行個體上尚未設定限定詞。 需要設定限定詞，才能完成初始化。|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|這個連接管理員不支援限定詞的指定。|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|無法為了跨處理序執行而複製連接管理員 "0x%1"。|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|SQL Server Profiler 的記錄提供者無法載入 pfclnt.dll。 請檢查是否已安裝 SQL Server Profiler。|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|SSIS 記錄基礎結構失敗，錯誤碼為 0x%1!8.8X!。 這個錯誤表示此記錄錯誤不能歸因於特定的記錄提供者。|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|SSIS 記錄提供者 "%1" 失敗，錯誤碼為 0x%2!8.8X!  (%3)。  這表示可歸因於特定之記錄提供者的記錄錯誤。|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|SaveToSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X!  (%2)。  發出的 SQL 陳述式失敗。|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|LoadFromSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X!  (%2)。  發出的 SQL 陳述式失敗。|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|RemoveFromSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。發出的 SQL 陳述式失敗。|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|ExistsOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X!  (%2)。 發出的 SQL 陳述式失敗。|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|使用提供的連接字串時，OLE DB 無法建立資料庫連接。|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|加入優先順序條件約束時，指定的 From 可執行檔不是這個容器的子系。|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|加入優先順序條件約束時，指定的 To 可執行檔不是這個容器的子系。|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|嘗試將 ODBC 連接編列到交易時發生錯誤。 SQLSetConnectAttr 無法設定 SQL_ATTR_ENLIST_IN_DTC 屬性。|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|因為封裝 OfflineMode 屬性設定為 TRUE，連接管理員 "%1" 將不會取得連接。 當 OfflineMode 為 TRUE 時，無法取得連接。|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|SSIS 執行階段無法啟動分散式交易，因為發生錯誤 0x%1!8.8X! "%2"。 DTC 交易無法啟動。 這可能是因為 MSDTC 服務不在執行中。|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|在封裝執行期間，連接管理員上無法呼叫 SetQualifier 方法。 這個方法只在設計階段使用。|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|要在 SQL Server 中儲存或修改封裝，SSIS 執行階段與資料庫必須是相同的版本。 不支援在舊版本中儲存封裝。|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|連接 "%1" 驗證失敗。|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|在連接中指定的檔案名稱 "%1" 無效。|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|當保留 (Retain) 屬性設定為 TRUE 時，連接中無法指定多個檔案名稱。 在連接字串中發現分隔號，表示指定多個檔案名稱，此外，保留屬性是 TRUE。|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|發生 ODBC 錯誤 %1!d! 。|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|"%1" 與 "%2" 之間的優先順序條件約束發生錯誤。|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|無法以原生 ForEachEnumerators 擴展 ForEachEnumeratorInfos 集合，錯誤碼: %1。|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|ForEach 列舉值的 GetEnumerator 方法失敗，錯誤為 0x%1!8.8X! "%2"。 當 ForEach 列舉值無法列舉時，就會發生這個問題。|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|無法從提供的憑證物件取得原始憑證資料 (錯誤: %1)。 當 CPackage::put_CertificateObject 無法具現化 ManagedHelper 物件、ManagedHelper 物件失敗或 ManagedHelper 物件傳回不正確的陣列時，就會發生這個問題。|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|無法建立憑證內容 (錯誤: %1)。 當對應的 CryptoAPI 函數失敗時，CPackage::put_CertificateObject 或 CPackage::LoadFromXML 中就會發生這個問題。|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|開啟 MY 憑證存放區失敗，錯誤為 "%1"。這個問題發生在 CPackage::LoadUserCertificateByName 和 CPackage::LoadUserCertificateByHash 中。|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|在 MY 存放區找不到依據名稱指定的憑證 (錯誤: %1)。 這個問題發生在 CPackage::LoadUserCertificateByName 中。|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|在 "MY" 存放區找不到依據雜湊指定的憑證 (錯誤: %1)。 這個問題發生在 CPackage::LoadUserCertificateByHash 中。|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|雜湊值不是一維的位元組陣列 (錯誤: %1)。 這個問題發生在 CPackage::LoadUserCertificateByHash 中。|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|無法存取陣列中的資料 (錯誤: %1)。 每當呼叫 GetDataFromSafeArray 時，就會發生這個錯誤。|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|SSIS Managed 協助程式物件在建立時失敗，錯誤為 0x%1!8.8X! "%2"。 每當 CoCreateInstance CLSID_DTSManagedHelper 失敗時，就會發生這個問題。|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|SSIS 執行階段無法將 OLE DB 連接編列到分散式交易中，錯誤為 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|封裝簽章失敗，錯誤為 0x%1!8.8X! "%2"。 當 ManagedHelper.SignDocument 方法失敗時，就會發生這個問題。|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|無法在封裝 XML 中檢查 XML 簽章封套 (Envelope)，錯誤為 0x%1!8.8X! "%2"。 這個問題發生在 CPackage::LoadFromXML 中。|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|無法從 XML DOM 物件取得 XML 來源，錯誤為 0x%1!8.8X! "%2"。 當 IXMLDOMDocument::get_xml 失敗時，就會發生這個問題。|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|封裝的密碼編譯簽章驗證失敗，因為錯誤 0x%1!8.8X! "%2"。 當簽章驗證作業失敗時，就會發生這個問題。|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|無法取得與指定憑證相關聯的密碼編譯金鑰組，錯誤為 0x%1!8.8X! "%2"。 請確認您擁有發出憑證的金鑰組。 嘗試使用個人沒有私密金鑰的憑證簽署文件時，通常會發生這個錯誤。|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|數位簽章無效。 封裝的內容已經遭到修改。|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|數位簽章有效; 不過，簽署人不受信任，因此，無法保證真實性。|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|連接不支援編列到分散式交易。|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|無法套用封裝保護，錯誤為 0x%1!8.8X! "%2"。 要儲存到 Xml 時發生這個錯誤。|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|無法移除封裝保護，錯誤為 0x%1!8.8X! "%2"。 這個問題發生在 CPackage::LoadFromXML 方法中。|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|封裝已經由密碼加密。 未指定密碼，或密碼不正確。|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|指定的可執行檔之間已經存在優先順序條件約束。 不允許一個以上的優先順序條件約束。|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|無法載入封裝，因為錯誤 0x%1!8.8X! "%2"。 當 CPackage::LoadFromXML 失敗時，就會發生這個問題。|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|在簽署的 XML 封套 (Envelope) 中找不到封裝物件，錯誤為 0x%1!8.8X! "%2"。 當簽署的 XML 未包含 SSIS 封裝時，預期會發生這個問題。|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|參數名稱、類型和描述陣列的長度不相等。 長度必須相等。 當陣列長度不相符時，就會發生這個問題。 在每一個陣列中，每個參數應該要有一個項目。|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|列舉封裝時，發生 OLE DB 錯誤 0x%1!8.8X! (%2)。 發出的 SQL 陳述式失敗。|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|為記錄提供者 "%2" 指定的記錄提供者類型 "%1" 無法辨識為有效的記錄提供者類型。 嘗試為未知的記錄提供者類型建立記錄提供者時，就會發生這個錯誤。 請檢查記錄提供者類型名稱的拼字。|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|記錄提供者類型無法辨識為有效的記錄提供者類型。 嘗試為未知的記錄提供者類型建立記錄提供者時，就會發生這個錯誤。 請檢查記錄提供者類型名稱的拼字。|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|為連接管理員指定的連接類型不是有效的連接管理員類型。 嘗試為未知的連接類型建立連接管理員時，就會發生這個錯誤。 請檢查連接類型名稱的拼字。|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|嘗試從 SQL Server 移除封裝 "%1" 時遇到錯誤。|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|在名稱為 "%1" 的 SQL Server 上，嘗試在資料夾 "%2" 中建立資料夾時遇到錯誤。|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|CreateFolderOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。發出的 SQL 陳述式失敗。|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|在 SQL Server 上，將資料夾 " %1\\\\%2" 重新命名為 "%1\\\\%3" 時發生錯誤。|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|RenameFolderOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X!  (%2)。 發出的 SQL 陳述式失敗。|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|刪除 SQL Server 資料夾 "%1" 時發生錯誤。|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|RemoveFolderOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2). 發出的 SQL 陳述式失敗。|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|指定的封裝路徑未包含封裝名稱。 當路徑未至少包含一個反斜線或一個斜線時，就會發生這個問題。|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|找不到資料夾 "%1"。|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|嘗試在 SQL 上尋找資料夾時發現 OLE DB 錯誤，錯誤碼為 0x%1!8.8X!  (%2)。|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|SSIS 記錄提供者無法開啟記錄。 錯誤碼：0x%1!8.8X!。|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|無法取得 ConnectionInfos 集合，錯誤為 0x%1!8.8X! "%2"。 當呼叫 IDTSApplication100::get_ConnectionInfos 失敗時，就會發生這個錯誤。|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|嘗試鎖定變數時偵測到死結。 在經過 16 次嘗試之後，仍然無法取得鎖定。 鎖定逾時。|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|未從 VariableDispenser 傳回 Variables 集合。 只有在分配的集合上，才允許嘗試的作業。|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|這個 Variables 集合已經解除鎖定。 在分配的 Variables 集合上只呼叫一次 Unlock 方法。|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|一或多個變數無法解除鎖定。|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|Variables 集合是從 VariableDispenser 傳回，無法修改。 在分配的集合中，無法加入或移除項目。|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|變數 "%1" 已經在讀取清單上。 在讀取鎖定清單或寫入鎖定清單上，一個變數只能加入一次。|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|變數 "%1" 已經在寫入清單上。 在讀取鎖定清單或寫入鎖定清單上，一個變數只能加入一次。|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|無法鎖定變數 "%1" 進行讀取，錯誤為 0x%2!8.8X! 失敗。|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|無法鎖定變數 "%1" 進行讀取/寫入，錯誤為 0x%2!8.8X! 失敗。|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|已使用不同的參數清單宣告自訂事件 "%1"。 有一個工作嘗試宣告自訂事件，但已有另一項工作使用不同的參數清單宣告此事件。|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|提供自訂事件 "%1" 的工作不允許在封裝中處理這個事件。 自訂事件已宣告為 AllowEventHandlers = FALSE。|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser 收到不安全的 Variables 集合。 無法重複這項作業。|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|在 ForEachEnumerator 上呼叫 GetPackagePath，但未指定 ForEachLoop 封裝路徑。|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|嘗試鎖定變數 "%1" 進行讀取時，偵測到死結。 在經過 16 次嘗試之後，仍然無法取得鎖定，鎖定逾時。|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|嘗試鎖定變數 "%1" 進行讀取/寫入時，偵測到死結。 在經過 16 次嘗試之後，仍然無法取得鎖定。 鎖定逾時。|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|嘗試鎖定變數 "%1" 進行讀取和鎖定變數 "%2" 進行讀取/寫入時，偵測到死結。 在經過 16 次嘗試之後，仍然無法取得鎖定。 鎖定逾時。|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|封裝的保護等級需要密碼，但 PackagePassword 屬性是空的。|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|無法將已加密的 XML 節點解密，因為未指定密碼或密碼不正確。 將在沒有加密資料的情況下，嘗試繼續載入封裝。|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|無法將以使用者金鑰加密的封裝解密。 您可能不是加密這個封裝的使用者，或並非使用儲存封裝的同一台電腦。|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|儲存至這個目的地時，無法使用保護層級 ServerStorage。 系統無法驗證目的地是否支援安全儲存體功能。|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer 方法失敗。|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|無法載入封裝，因為數位簽章的狀態違反簽章原則。 錯誤 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|封裝尚未簽署。|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|SQL Server Profiler 的記錄提供者無法載入 pfclnt.dll，因為只有 32 位元的系統才有支援。|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|無法加入物件，因為集合中已經存在相同名稱的另一個物件。 請使用不同名稱來解決這個錯誤。|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|物件名稱不能從 "%1 變更為 "%2"，因為集合中有另一個物件已經使用這個名稱。 請使用不同名稱來解決這個錯誤。|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|列舉封裝相依性時發生錯誤。 如需詳細資訊，請檢查其他訊息。|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|不支援目前的封裝設定。  請變更 SaveCheckpoints 屬性或 TransactionOption 屬性。|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|連接管理員無法脫離交易。|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|指定的中斷點識別碼已經存在。 當工作使用相同識別碼多次呼叫 CreateBreakpoint 時，就會發生這個錯誤。 如果工作在建立第一個中斷點時呼叫 RemoveBreakpoint，則在建立第二個中斷點之前，可能會使用相同識別碼建立中斷點許多次。|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|指定的中斷點識別碼不存在。 當工作參考的中斷點不存在時，就會發生這個錯誤。|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|無法開啟檔案 "%1" 進行寫入。 檔案可能是唯讀，或您沒有正確的權限。|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|這個查詢的執行沒有相關聯的結果資料列集。 未正確指定結果。|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|未正確產生偵錯傾印檔案。 hresult 為 0x%1!8.8X!。|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|指定的 URL 無效。 當伺服器或 Proxy URL 為 Null 或格式不正確時，就會發生這個問題。 有效的 URL 格式為 http://ServerName:Port/ResourcePath 或 https://ServerName:Port/ResourcePath。|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|URL %1 無效。 當指定 http 或 https 以外的配置或 URL 的格式不正確時，就會發生這個問題。 有效的 URL 格式為 http://ServerName:Port/ResourcePath 或 https://ServerName:Port/ResourcePath。|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|無法建立與伺服器 %1 的連接。 當伺服器不存在或 Proxy 設定不正確時，就會發生這個錯誤。|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|已經重設或結束與伺服器的連接。 請稍後再試一次。|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|"%1" 的登入嘗試失敗。 當提供的登入憑證不正確時，就會發生這個錯誤。 請驗證登入認證。|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|無法解析 URL %1 中指定的伺服器名稱。|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Proxy 驗證失敗。 當未提供登入認證或認證不正確時，就會發生這個錯誤。|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|從伺服器取得的 SSL 憑證回應無效。 無法處理要求。|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|要求已逾時。 當指定的逾時值太短時，或無法建立與伺服器或 Proxy 的連接時，就會發生這個錯誤。 請確定伺服器和 Proxy URL 都正確。|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|遺漏用戶端憑證。 當伺服器需要 SSL 用戶端憑證，但使用者提供無效的憑證或未提供憑證時，就會發生這個錯誤。 必須為這個連接設定用戶端憑證。|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|指定的伺服器 URL %1 有重新導向，但重新導向要求失敗。|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|伺服器驗證失敗。 當未提供登入認證或認證不正確時，就會發生這個錯誤。|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|無法處理要求。 請稍後再試一次。|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|伺服器傳回狀態碼 - %1!u!  : %2。 當伺服器遇到問題時，就會發生這個錯誤。|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|WinHttp 服務不支援這個平台。|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|逾時值無效。 逾時值應該在 %1!d! 至 %2!d!  到 %2!d!   (秒)。|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|區塊大小無效。 ChunkSize 屬性應該在 %1!d! 至 %2!d!  到 %2!d!   (KB)。|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|處理用戶端憑證時發生錯誤。 在個人憑證存放區 (Personal Certificate Store) 找不到提供的用戶端憑證時，就會發生這個錯誤。 請確認用戶端憑證有效。|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|伺服器傳回錯誤碼「403 - 禁止」。 當指定的資源需要 "https" 存取時，但憑證有效期間已過期、憑證在要求的用途上無效、憑證已撤鎖或無法檢查撤銷時，就會發生這個錯誤。|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|使用 Proxy "%1" 初始化 HTTP 工作階段時發生錯誤。 當指定無效的 Proxy 時，就會發生這個錯誤。 HTTP 連接管理員僅支援 CERN 類型 Proxy。|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|開啟憑證存放區時發生錯誤。|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|無法將保護的 XML 節點 "%1" 解密，錯誤為 0x%2!8.8X! 失敗。 您可能沒有存取這項資訊的權限。 當發生密碼編譯錯誤時，就會發生這個錯誤。 請確認有正確的金鑰。|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|無法將伺服器 "%1" 的受保護連接字串解密，錯誤為 0x%2!8.8X! 失敗。 您可能沒有存取這項資訊的權限。 當發生密碼編譯錯誤時，就會發生這個錯誤。 請確認有正確的金鑰。|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|版本號碼不可以是負值。 當封裝的 VersionMajor、VersionMinor 或 VersionBuild 屬性設定為負值時，就會發生這個錯誤。|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|封裝在載入期間已移轉至較新版本。 必須重新載入，才能完成處理程序。 此為內部錯誤碼。|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|封裝從 %1!d! 版本移轉至  %2!d! 版本 失敗，錯誤為 0x%3!8.8X! "%4"。|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|無法載入封裝移轉模組。|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|封裝移轉模組失敗。|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|無法使用預設的持續性機制 (Persistence) 來保存物件。 當預設的持續性機制無法決定主控物件上有哪些物件時，就會發生這個錯誤。|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|在執行階段模式下，無法在封裝中加入或移除元素。 當封裝執行時，如果嘗試在集合中加入或移除物件，就會發生這個錯誤。|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|在自訂的預設持續性機制中找不到 "%1" 節點。 如果可延伸物件預設儲存的 XML 已變更，導致找不到儲存的物件，或可延伸的物件本身已變更，就會發生這個錯誤。|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|在封裝驗證或執行期間，無法修改這個集合。|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|在封裝驗證或執行過程中無法修改 "%1" 集合。 無法將 "%2" 加入集合。|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|無法建立與 FTP 伺服器的連接。|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|要求的 FTP 作業發生錯誤。 詳細的錯誤描述: %1。|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|重試次數無效。 重試次數應該介於 %1!d! 至 %2!d! 。|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|FTP 連接管理員需要下列 DLL 才能正常運作: %1。|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|在連接字串中指定的通訊埠無效。 ConnectionString 格式為 ServerName:Port。 通訊埠應該是介於 %1!d! 到 %2!d! 之間的整數值 。|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|正在建立資料夾 "%1" ... %2。|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|正在刪除資料夾 "%1" ... %2。|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|正在將目前的目錄切換到 "%1"。 %2。|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|沒有要傳送的檔案。 當執行傳送或接收作業時，如果未指定傳送的檔案，就會發生這個錯誤。|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|指定的本機路徑無效。 請指定有效的本機路徑。 當指定的本機路徑為 Null 時，就會發生這個問題。|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|未指定要刪除的檔案。|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|載入憑證時發生內部錯誤。 當憑證資料無效時，就會發生這個錯誤。|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|儲存憑證資料時發生內部錯誤。|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|檢查點檔案 "%1" 與這個封裝不符。 封裝的識別碼和檢查點檔案中的識別碼不符。|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|現有檢查點檔案的內容似乎不是針對這個封裝，所以無法覆寫檔案來開始儲存新的檢查點。 請移除現有的檢查點檔案，然後再試一次。 當檢查點檔案存在時，且封裝設定為不使用檢查點檔案，但又要儲存檢查點，就會發生這個錯誤。 將不會覆寫現有的檢查點檔案。|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|檢查點檔案 "%1" 已被其他處理序鎖定。 如果這個封裝的其他執行個體正在執行，就可能發生這個問題。|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|無法開啟檢查點檔案 "%1"，因為錯誤 0x%2!8.8X! 失敗。|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|檢查點檔案 "%1" 在建立時失敗，因為發生錯誤 0x%2!8.8X!  失敗。|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|FTP 通訊埠包含無效的值。 FTP 通訊埠值應該是介於 %1!d! 到 %2!d! 之間的整數 。|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|連接到電腦 "%1" 上的 SSIS 服務失敗:<br /><br /> %2。|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|Variable 物件不支援 Expression 屬性。 請改用 EvaluateAsExpression 屬性。|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|無法評估屬性 "%2" 上的運算式 "%1"。 請修改為有效的運算式。|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|運算式 "%1" 在屬性 "%2" 上的結果無法寫入屬性。 已評估運算式，但無法在屬性上設定。|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|迴圈的評估運算式無效。 必須修改運算式。 應該還有其他錯誤訊息。|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|運算式 "%1" 必須評估為 True 或 False。 請變更運算式來評估成布林值。|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|沒有運算式可供迴圈評估。 當 For 迴圈上的運算式是空的，就會發生這個錯誤。 請加入運算式。|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|迴圈的指派運算式無效，必須修改。 應該還有其他錯誤訊息。|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|迴圈的初始化運算式無效，必須修改。 應該還有其他錯誤訊息。|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|封裝中的版本號碼無效。 此版本號碼不能大於目前的版本號碼。|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|封裝中的版本號碼無效。 此版本號碼為負值。|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|封裝的格式版本是舊的，但是自動封裝格式升級已停用。|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|在運算式評估期間發生截斷。|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|包裝函式無法設定 ExecutionValueVariable 屬性中所指定變數的值。|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|變數 "%1" 的運算式評估失敗。 運算式發生錯誤。|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|這個資料庫版本不支援所嘗試的作業。|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|使用保留的連接時，無法指定交易。 當連接管理員上的保留 (Retain) 設定為 TRUE 時，如果使用非 Null 交易參數呼叫 AcquireConnection，就會發生這個錯誤。|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|保留的連接指定了不相容的交易內容。 已在不同交易內容下建立這個連接。 保留的連接只能在一個交易內容中使用。|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Resume 呼叫失敗，因為封裝未暫停。 當用戶端呼叫 Resume 時，如果封裝未暫停，就會發生這個問題。|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Execute 呼叫失敗，因為可執行檔已經執行。 當用戶端在容器上呼叫 Execute 時，如果此容器自前次 Execute 呼叫後仍在執行，就會發生這個錯誤。|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Suspend 或 Resume 呼叫失敗，因為可執行檔未執行，或不是最上層可執行檔。 當用戶端在可執行檔上呼叫 Suspend 或 Resume 時，如果可執行檔目前未處理 Execute 呼叫，就會發生這個問題。|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|For Each File 列舉值指定的檔案無效。 請確認 For Each File 列舉值指定的檔案存在。|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|值索引不是整數。 請將 For Each Variable 數字 %1!d! 對應 至變數 "%2"。|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|值索引是負值。 ForEach Variable 對應數字 %1!d!  至變數 "%2"。|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|無法套用 ForEach Variable 對應數字 %1!d!  至變數 "%2"。|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|將物件加入不是 ForEachLoop 容器直接子系的 ForEachPropertyMapping 時失敗。|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|無法移除系統變數。 當移除的變數是必要變數時，就會發生這個錯誤。  必要變數是執行階段為了在工作和執行階段之間通訊而建立的變數。|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|變更變數的屬性失敗，因為它是系統變數。 系統變數是唯讀的。|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|變更變數的名稱失敗，因為它是系統變數。 系統變數是唯讀的。|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|變更變數的命名空間失敗，因為它是系統變數。 系統變數是唯讀的。|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|變更事件處理常式名稱失敗。 事件處理常式名稱是唯讀的。|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|無法擷取物件的路徑。 此為系統錯誤。|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|指派給變數 "%1" 的值類型不同於目前變數類型。 變數在執行期間不能變更類型。 除了 Object 類型的變數以外，變數類型都是 strict。|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|字串 "%1" 包含無效字元。 當提供給屬性值的字串包含不可列印字元時，就會發生這個問題。|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS 物件名稱無效。 應該已引發其他特定的錯誤，解釋確切的命名問題。|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|屬性 "%1" 是唯讀的。 嘗試變更唯讀屬性時，就會發生這個問題。|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|物件不支援類型資訊。 當執行階段嘗試從物件取得類型資訊來擴展 Properties 集合時，就會發生這個問題。  物件必須支援類型資訊。|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|擷取屬性 "%1" 的值時發生錯誤。 錯誤碼為 0x%2!8.8X!。|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|擷取屬性 "%1" 的值時發生錯誤。 錯誤碼為 0x%2!8.8X! 失敗。|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|設定屬性 "%1" 的值時發生錯誤。 傳回的錯誤為 0x%2!8.8X!。|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|設定屬性 "%1" 的值時發生錯誤。 傳回的錯誤為 0x%2!8.8X! 失敗。|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|屬性 "%1" 是唯寫的。 嘗試透過屬性物件擷取屬性的值時，如果屬性是唯寫的，就會發生這個錯誤。|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|物件未實作 IDispatch。 當屬性物件或屬性集合嘗試存取物件的 IDispatch 介面時，就會發生這個錯誤。|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|無法擷取物件的類型程式庫。 當 Properties 集合嘗試透過 IDispatch 介面擷取物件的類型程式庫時，就會發生這個錯誤。|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|無法根據 XML 為工作 "%1!s!"、類型 "%2!s!" 建立工作， 因為錯誤 0x%3!8.8X! "%4!s!"。|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|無法建立 XML 文件 "%1"。|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|發生錯誤，因為在屬性對應中，從變數對應至不同類型的屬性。 屬性類型必須與變數類型相符。|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|嘗試以未支援的物件類型為目標來設定屬性對應。 將不支援的物件類型傳遞至屬性對應時，就會發生這個錯誤。|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|無法將封裝路徑解析為封裝 "%1" 中的物件。  請確認封裝路徑有效。|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|屬性對應的目的地屬性是空的。 請設定目的地屬性名稱。|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|封裝無法還原至少一個屬性對應。|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|變數名稱模稜兩可，因為在不同的命名空間中有多個變數具有這個名稱。 請指定符合命名空間的名稱，以避免模糊不清。|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|屬性對應中的目的地物件沒有父系。 目的地物件不是任何時序容器的子系。 可能已從封裝中移除它。|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|屬性對應無效。 已忽略對應。|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|向屬性對應提出要移除目標的警示時發生失敗。|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|在 For Each 迴圈上發現無效的屬性對應。 當 ForEach 屬性對應無法還原時，就會發生這個問題。|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|在屬性對應上指定的目的地屬性無效。 在目的地物件上指定屬性時，如果該物件上找不到此屬性，就會發生這個問題。|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|無法從 XML 建立工作。 當執行階段無法解析名稱來建立工作時，就會發生這個問題。 請確認名稱正確。|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|無法使用更新的檢查點檔案取代現有的檢查點檔案。 已經在暫存檔中成功建立檢查點，但以新檔案覆寫現有的檔案失敗。|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|封裝設定為永遠從檢查點重新啟動，但未指定檢查點檔案。|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|嘗試載入 XML 檢查點檔案 "%1" 失敗，錯誤為 0x%2!8.8X! "%3"。 請確認指定的檔案名稱正確，且檔案存在。|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|封裝執行期間失敗，因為無法載入檢查點檔案。 需要檢查點檔案，才可能進一步執行封裝。 當 CheckpointUsage 屬性設定為 ALWAYS 時指定封裝一定會重新啟動，通常就會發生這個錯誤。|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|For 迴圈 "%1" 上的評估條件運算式是空的。 For 迴圈中必須有布林值評估運算式。|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|指派運算式 "%1" 的結果無法轉換成與被指派之變數相容的類型。|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|在指派運算式中使用唯讀變數 "%1" 時發生錯誤。 運算式結果無法指派給變數，因為變數是唯讀的。 請選擇可以寫入的變數，或從這個變數移除運算式。|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|無法評估運算式 "%1"，因為變數 "%2" 不存在或無法存取進行寫入。 運算式結果無法指派給變數，因為找不到變數，或無法鎖定變數進行寫入。|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|運算式 "%1" 的結果類型為 "%2"，無法轉換成支援的類型。|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|將運算式 "%1" 的結果從類型 "%2" 轉換成支援的類型失敗，錯誤碼為 0x%3!8.8X!。 嘗試將運算式結果轉換成執行階段引擎支援的類型時，即使支援類型轉換，仍然發生意外的錯誤。|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|物件名稱無效。 名稱不能設定為 NULL。|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|物件名稱無效。 名稱不可以是空的。|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|物件名稱 "%1" 無效。 名稱不能包含下列任何字元: / \ : [ ]。 =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|物件名稱 "%1" 無效。 名稱不能包含會造成無法列印的控制字元。|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|物件名稱 "%1" 無效。 名稱開頭不可以是空白字元。|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|物件名稱 "%1" 無效。 名稱結尾不可以是空白字元。|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|物件名稱 "%1" 無效。 名稱開頭必須是字母字元。|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|物件名稱 "%1" 無效。 名稱開頭必須是字母字元或底線 "_"。|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|物件名稱 "%1" 無效。 名稱只能包含英數字元或底線 "_"。|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|物件名稱 "%1" 無效。 名稱不能包含下列任何字元: / \ : ? " \< > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|無法使用預設持續性機制載入值屬性 "%1"。|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|連接管理員 "%1" 不是 "%2" 類型|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" 是空的|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|nodelist 列舉值區段中的資料節點無效|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|無法建立列舉值|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|作業失敗，因為快取正在使用中。|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|無法修改屬性。|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|封裝升級失敗。|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|錯誤 0x%1!8.8X! 發生錯誤 0x%1!8.8X!。 %2。|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|未指定封裝。|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|未指定連接。|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|連接管理員 "%1" 具有未支援的類型 "%2"。 僅支援 "FILE" 和 "OLEDB" 連接管理員。|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|錯誤 0x%1!8.8X! 將封裝檔案 "%3" 載入 XML 文件時發生錯誤。 %2。|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|錯誤 0x%1!8.8X! 準備載入封裝時發生錯誤。 %2。|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|在工作上的 Validate 方法失敗，並傳回錯誤碼 0x%1!8.8X! (%2)。 Validate 方法必須成功，並使用 "out" 參數表示結果。|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|在工作上的 Execute 方法傳回錯誤碼 0x%1!8.8X!  (%2)。 Execute 方法必須成功，並使用 "out" 參數表示結果。|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|擷取相依性時，工作 "%1"失敗：0x%2!8.8X! 。 發生錯誤時，執行階段正從工作的相依性集合擷取相依性。 工作可能未正確實作其中一個相依性介面。|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|工作驗證期間發生錯誤。|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|連接字串格式無效。 必須由一或多個 X=Y 格式的元件組成，並以分號隔開。 在資料庫連接管理員上設定不含元件的連接字串時，就會發生這個錯誤。|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|連接字串元件不能包含未加引號的分號。 如果值必須包含分號，請用引號括住整個值。 當連接字串中的值包含未加引號的分號時，例如 InitialCatalog 屬性，就會發生這個錯誤。|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|一個或多個記錄提供者的驗證失敗。 無法執行封裝。 當記錄提供者驗證失敗時，不會執行封裝。|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|陣列包含無效的值。|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|ForEach 列舉值傳回的列舉值元素未實作 IEnumerator，與 ForEach 列舉值的 CollectionEnumerator 屬性衝突。|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|列舉值無法擷取索引 "%1!d!" 處的元素。|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|找不到函數。|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|找不到函數。|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|使用錯誤的 XML 元素起始 ActiveX Script 工作。|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|找不到處理常式。|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|嘗試擷取系統上安裝的指令碼語言時發生錯誤。|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|建立 ActiveX Script Host 時發生錯誤。 請確認 Script Host 已正確安裝。|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|嘗試針對選擇的語言具現化 Script Host 時發生錯誤。 請確認您選擇的指令碼語言已安裝在系統上。|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|將 SSIS 變數加入 Script Host 命名空間時發生錯誤。 這可能導致工作無法在指令碼中使用 SSIS 變數。|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|嘗試剖析指令碼文字時發生嚴重錯誤。 請確認選定語言的指令碼引擎有正確安裝。|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|輸入的函數名稱無效。 請確認已經指定有效的函數名稱。|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|執行指令碼時發生錯誤。 請確認選定語言的指令碼引擎有正確安裝。|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|將 Managed 類型程式庫加入 Script Host 時發生錯誤。 請確認已經安裝 DTS 2000 執行階段。|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|使用錯誤的 XML 元素起始大量插入工作。|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|未指定資料檔案名稱。|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|找不到處理常式。|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|無法取得指定的連接: "%1"。|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|嘗試取得連接管理員失敗。|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|連接無效。|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|連接為 Null。|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|執行失敗。|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|從資料庫擷取資料表時發生錯誤。|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|從資料表擷取資料行時發生錯誤。|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|資料庫作業發生錯誤。|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|指定的連接 "%1" 無效，或指向無效物件。 若要繼續，請指定有效的連接。|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|指定的目的地連接無效。 請提供有效的連接，才能繼續。|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|您必須指定資料表名稱，才能繼續。|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 的標記 "%1" 發生錯誤。|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|SaveToXML 的標記 "%1" 發生錯誤。|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|連接無效。|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|執行失敗。|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|從資料庫擷取資料表時發生錯誤。|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|從資料表擷取資料行時發生錯誤。|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|嘗試開啟資料檔案時發生錯誤。|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|無法將輸入 OEM 檔案轉換成指定的格式。|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|資料庫作業發生錯誤。|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|未指定連接管理員。|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|連接 "%1" 不是 Analysis Services 連接。|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|找不到連接 "%1"。|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services 執行 DDL 工作收到無效的工作資料節點。|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services 處理工作收到無效的工作資料節點。|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|DDL 無效。|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|ProcessingCommands 中發現的 DDL 無效。|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|執行結果無法儲存在唯讀變數中。|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|未定義變數 "%1"。|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|未定義連接管理員 "%1"。|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|連接管理員 "%1" 不是 FILE 連接管理員。|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|在還原序列化期間，找不到 "%1"。|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|因為例外狀況，所以已經停止追蹤。|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|執行 DDL 失敗。|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|沒有與連接 "%1" 相關聯的檔案。|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|未定義變數 "%1"。|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|未定義檔案連接 "%1"。|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|使用錯誤的 XML 元素起始執行 DTS 2000 封裝工作。|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|找不到處理常式。|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|未指定封裝名稱。|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|未指定封裝識別碼。|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|未指定封裝版本 GUID。|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|未指定 SQL Server。|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|未指定 SQL Server 使用者名稱。|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|未指定儲存體檔案名稱。|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|DTS 2000 封裝屬性是空的。|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|執行 DTS 2000 封裝時發生錯誤。|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|無法從網路載入可用的 SQL Server。 請檢查網路連接。|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|資料類型不可以是 Null。 請指定用來驗證此值的正確資料類型。|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|無法對任何資料類型驗證 Null 值。|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|必要的引數是 Null。|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|如果要執行 DTS 2000 封裝工作，請啟動 SQL Server 安裝程式，然後在 [要安裝的元件] 頁面中，使用 [進階] 按鈕選取 [傳統元件]。|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" 不是數值類型。|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|無法將 "%1" 轉換成 "%2"。|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|無法對 "%2" 驗證 "%1"。|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 的標記 "%1" 發生錯誤。|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|SaveToXML 的標記 "%1" 發生錯誤。|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|提供的逾時值無效。 請指定工作允許處理序執行的秒數。 最小逾時值為 0，表示不使用逾時值，而處理序會執行到完成或直到發生錯誤為止。 最大逾時值為 2147483 (((2^31) - 1)/1000)。|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|如果處理序會繼續執行到超出工作的存留期間，則無法重新導向資料流。|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|處理序逾時。|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|未指定可執行檔。|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|標準輸出變數是唯讀的。|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|標準錯誤變數是唯讀的。|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|執行處理序工作收到無效的工作資料節點。|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|在 "%1" 端執行 "%2" "%3" 的處理序結束碼為 "%4"，但必須是 "%5"。|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|目錄 "%1" 不存在。|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|檔案/處理序 "%1" 不存在於目錄 "%2" 中。|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|檔案/處理序 "%1" 不在路徑中。|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|工作目錄 "%1" 不存在。|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|處理序結束，傳回碼為 "%1"， 但必須是 "%2"。|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|同步處理物件失敗。|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|檔案系統工作收到無效的工作資料節點。|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|目錄已經存在。|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" 在作業類型 "%2" 上無效。|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|未設定作業 "%1" 的目的地屬性。|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|未設定作業 "%1" 的來源屬性。|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|連接類型 "%1" 不是檔案。|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|變數 "%1" 不存在。|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|變數 "%1" 不是字串。|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|連接 "%2" 表示的檔案或目錄 "%1" 不存在。|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|目的地檔案連接管理員 "%1" 具有無效的使用類型: "%2"。|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|來源檔案連接管理員 "%1" 具有無效的使用類型 "%2"。|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|提供有關檔案系統作業的資訊。|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|檔案系統工作|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|執行檔案系統作業，例如複製和刪除檔案。|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|同步處理物件失敗。|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|無法取得檔案清單。|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|本機路徑是空的。|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|遠端路徑是空的。|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|本機變數是空的。|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|遠端變數是空的。|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|FTP 工作收到無效的工作資料節點。|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|連接是空的。 請確認已提供有效的 FTP 連接。|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|指定的連接不是 FTP 連接。 請確認已提供有效的 FTP 連接。|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|無法初始化含有 Null XML 元素的工作。|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|無法將工作儲存至 Null XML 文件。|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 的標記 "%1" 發生錯誤。|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|"%1" 端沒有任何檔案。|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|變數 "%1" 是空的。|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|變數 "%1" 是空的。|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|檔案 "%1" 未包含檔案路徑。|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|變數 "%1" 未包含檔案路徑。|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|變數 "%1" 不是字串。|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|變數 "%1" 不存在。|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|作業 "%1" 的路徑無效。|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" 已經存在。|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|連接類型 "%1" 不是檔案。|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|"%1" 表示的檔案不存在。|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|變數 "%1" 中未指定目錄。|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|在 "%1" 中找不到檔案。|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|檔案連接管理員 "%1" 中未指定目錄。|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|無法刪除本機檔案 "%1"。|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|無法移除本機目錄 "%1"。|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|無法建立本機目錄 "%1"。|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|無法使用 "%1" 接收檔案。|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|無法使用 "%1" 傳送檔案。|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|無法使用 "%1" 建立遠端目錄。|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|無法使用 "%1" 移除遠端目錄。|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|無法使用 "%1" 刪除遠端檔案。|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|無法使用 "%1" 連接 FTP 伺服器。|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|變數 "%1" 不是以 "/" 開頭。|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|遠端路徑 "%1" 不是以 "/" 開頭。|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|取得 FTP 連接時發生錯誤。 請檢查您是否已指定有效的連接類型 "%1"。|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|開啟憑證存放區失敗。|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|擷取憑證的顯示名稱時發生錯誤。|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|擷取憑證的簽發者名稱時發生錯誤。|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|擷取憑證的易記名稱時發生錯誤。|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|未設定 MSMQ 連接名稱。|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|使用錯誤的 XML 元素初始化工作。|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|資料檔案名稱是空的。|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|針對要儲存的資料檔案指定的名稱是空的。|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|檔案大小應該小於 4 MB。|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|儲存資料檔案失敗。|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|字串篩選值是空的。|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|佇列路徑無效。|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|此訊息佇列工作不支援編列到分散式交易。|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|訊息類型無效。|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|訊息佇列逾時。 未收到任何訊息。|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|指定的屬性無效。 請確認引數類型正確。|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|未驗證訊息。|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|嘗試以無效物件來設定加密演算法的值。|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|用來接收字串訊息的變數是空的。|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|用來接收變數訊息的變數是空的。|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|連接 "%1" 不是 MSMQ 類型。|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|指定的位置已有資料檔案 "%1"。 無法覆寫檔案，因為覆寫 (Overwrite) 選項設定為 false。|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|在封裝變數集合中，找不到指定用來接收字串訊息的變數 "%1"。|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|連接管理員 "%1" 是空的。|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|連接管理員 "%1" 不存在。|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|錯誤 "%1": "%2"\r\n行 "%3"   資料行 "%4" 至 "%5"。|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|編譯指令碼: "%1" 時發生錯誤。|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|錯誤 "%1": "%2"\r\n行 "%3" 資料行 "%4"-"%5"\r\n行文字: "%6"。|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|使用者指令碼傳回失敗結果。|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|無法載入使用者指令碼檔案。|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|使用者指令碼擲回例外狀況: "%1"。|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|無法建立進入點類別 "%1" 的執行個體。|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|從 XML 載入指令碼工作時發生例外狀況: "%1"。|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|在封裝中找不到來源項目 "%1"。|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|在封裝中找不到二進位項目 "%1"。|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" 無法辨識為有效的指令碼語言。|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|指令碼名稱無效。 不能包含空格、斜線、特殊字元或以數字開頭。|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|指定的指令碼語言無效。|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|無法初始化 Null 工作。|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|指令碼工作使用者介面必須初始化為指令碼工作。|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|指令碼工作使用者介面未初始化。|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|名稱不可以是空的。|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|專案名稱無效。 不能包含空格、斜線、特殊字元或以數字開頭。|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|指定的指令碼語言無效。|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|找不到進入點。|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|未指定指令碼語言。 請確認已指定有效的指令碼語言。|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|使用者介面初始化: 此工作是 Null。|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|使用不正確的工作初始化指令碼工作使用者介面。|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|未指定收件者。|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|未指定 Simple Mail Transfer Protocol (SMTP) 伺服器。 請提供 SMTP 伺服器的有效名稱或 IP 位址。|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|使用不正確的 XML 元素起始傳送郵件工作。|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|檔案 "%1" 不存在，或您沒有存取檔案的權限。|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|請確認指定的 Simple Mail Transfer Protocol (SMTP) 伺服器有效。|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|連接 "%1" 不是 File 類型。|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|在作業 "%1" 上，檔案 "%2" 不存在。|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|變數 "%1" 不是字串類型。|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|連接 "%1" 不是 SMTP 類型。|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|連接 "%1" 是空的。|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|指定的連接 "%1" 不存在。|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|未指定 Transact-SQL 陳述式。|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|連接不支援 XML 結果集。|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|找不到指定之連接類型的處理常式。|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|未指定連接管理員。|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|無法從連接管理員取得連接。|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|不能有 Null 參數名稱。|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|參數名稱無效。|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|有效參數名稱為 Int 或 String 類型。|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|變數 "%1" 無法用於結果繫結，因為它是唯讀的。|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|這個集合內未指派索引。|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|變數 "%1" 不能用來做為參數繫結中的 "out" 參數或傳回值，因為它是唯讀的。|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|物件不存在於這個集合中。|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|無法取得 Managed 連接。|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|無法擴展單一資料列結果類型的結果資料行。 查詢傳回空的結果集。|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|ResultSetType 傳回的結果繫結數目無效: "%1"。|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|完整結果集和 XML 結果的結果繫結名稱必須設定為零。|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|參數方向旗標無效。|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|XML 片段未包含 SQL 工作資料。|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|具有傳回值類型的參數不是第一個參數，或一個以上的參數具有傳回值類型。|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|連接 "%1" 不是檔案連接管理員。|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|"%1" 表示的檔案不存在。|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|變數 "%1" 的類型不是字串。|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|變數 "%1" 不存在或無法鎖定。|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|連接管理員 "%1" 不存在。|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|無法取得連接 "%1"。 連接可能未正確設定，或您沒有這個連接的正確權限。|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|這個連接類型不支援依據名稱 "%1" 的結果繫結。|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|指定單一資料列的結果集類型，但未傳回任何資料列。|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|Transact-SQL 陳述式沒有可用的中斷連接記錄集。|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|不支援的類型。|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|未知的類型。|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|參數繫結 \\"%s\\" 包含不支援的資料類型。|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|參數名稱不能混合序數和命名類型。|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|參數繫結 \\"%s\\" 上的參數方向無效。|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|不支援結果集繫結 \\"%s\\" 上的資料類型。|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|結果資料行索引 %d 無效。|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|在結果集找不到資料行 \\"%s\\"。|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|這個查詢的執行沒有相關聯的結果資料列集。|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|ODBC 連接沒有離線記錄集。|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|不支援結果集的資料行 %hd 的資料類型。|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|無法使用查詢結果載入 XML。|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|必須指定封裝的連接名稱或變數名稱。|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|無法建立封裝。|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|TableMetaDataNode 不是 XMLNode。|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|無法建立管線。|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|變數不是正確類型。|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|指定的連接管理員不是 FILE 連接管理員。|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|在連接管理員 "%1" 上指定無效的檔案名稱。|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|連接是空的。 請確認已指定有效的 HTTP 連接。|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|連接不存在。 請確認指定有效、現有的 HTTP 連接。|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|指定的連接不是 HTTP 連接。 請確認已指定有效的 HTTP 連接。|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|Web 服務名稱是空的。 請確認已指定有效的 Web 服務名稱。|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|Web 方法名稱是空的。 請確認已指定有效的 Web 方法。|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|Web 方法是空的或可能不存在。 請確認存在現有的 Web 方法可以指定。|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|輸出位置是空的。 請確認已指定現有的檔案連接或變數。|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|找不到變數。 請確認變數存在於封裝中。|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|無法儲存結果。 請確認變數不是唯讀的。|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 的標記 "%1" 發生錯誤。|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|SaveToXML 的標記 "%1" 發生錯誤。|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|無法將工作儲存至 Null XML 文件。|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|無法初始化含有 Null XML 元素的工作。|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|使用不正確的 XML 元素起始 Web 服務工作。|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|發現非預期的 XML 元素。|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|取得 HTTP 連接時發生錯誤。 請確認已指定有效的連接類型。|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|無法儲存結果。 請確認現有的檔案連接存在。|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|無法儲存結果。 請確認檔案存在。|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|無法儲存結果。 檔案名稱是空的或其他處理序正在使用檔案。|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|取得檔案連接時發生錯誤。 請確認已指定有效的檔案連接。|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|只支援具有基本值、基本陣列和列舉的複雜類型。|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|只支援 Primitive、Enum、Complex、PrimitiveArray 和 ComplexArray 類型。|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|不支援這個 WSDL 版本。|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|以不正確的 XML 元素初始化。|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|找不到強制屬性。|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|列舉 "%1" 沒有任何值。 WSDL 已損毀。|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|找不到連接。|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|使用這個名稱的連接已經存在。|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|連接不可以是 Null 或空的。|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|指定的連接不是 HTTP 連接。 請確認已指定有效的 HTTP 連接。|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|指定的統一資源識別碼 (URI) 未包含有效的 WSDL。|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|無法讀取 WSDL 檔案。 輸入的 WSDL 檔案無效。 讀取器擲回下列錯誤: "%1"。|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|服務描述不可以是 Null。|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|服務名稱不可以是 Null。|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL 不可以是 Null。|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|目前無法使用服務。|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|SOAP 通訊埠無法使用此服務。|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|無法剖析 Web 服務描述語言 (WSDL)。 找不到對應至 SOAP 通訊埠的繫結。|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|無法剖析 Web 服務描述語言 (WSDL)。 找不到對應至 SOAP 通訊埠的 PortType。|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|找不到對應至指定之方法的訊息。|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|無法為給定的 Web 服務產生 Proxy。 產生 Proxy "%1" 時遇到下列錯誤。|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|無法為給定的 Web 服務載入 Proxy。 確切的錯誤如下: "%1"。|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|找不到指定的服務。 確切的錯誤如下: "%1"。|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|在方法執行期間，Web 服務擲回下列錯誤: "%1"。|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|無法執行 Web 方法。 確切的錯誤如下: "%1"。|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo 不可以是 Null。|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|指定的 WebMethodInfo 不正確。 提供的 ParamValue 與 ParamType 不符。 DTSParamValue 不是 PrimitiveValue 類型。|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|指定的 WebMethodInfo 不正確。 提供的 ParamValue 與 ParamType 不符。 找到的 DTSParamValue 不是 EnumValue 類型。|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|指定的 WebMethodInfo 不正確。 提供的 ParamValue 與 ParamType 不符。 找到的 DTSParamValue 不是 ComplexValue 類型。|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|指定的 WebMethodInfo 不正確。 提供的 ParamValue 與 ParamType 不符。 找到的 DTSParamValue 不是 ArrayValue 類型。|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|您指定的 WebMethodInfo 不正確。 "%1" 不是 Primitive 類型。|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|ArrayValue 的格式無效。 陣列中應該至少有一個元素。|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|列舉的值不可以是 Null。 請選取列舉的預設值。|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|無法對任何資料類型驗證 Null。|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|列舉值不正確。|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|指定的類別未包含名稱為 "%1" 的公用屬性。|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|無法將 "%1" 轉換成 "%2"。|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|清除失敗。 可能尚未刪除為 Web 服務所建立的 Proxy。|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|無法建立類型 "%1" 的物件。 請檢查預設建構函式是否存在。|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" 不是數值類型。|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|無法驗證 "%1" (針對 "%1")。|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|資料類型不可以是 Null。 請指定要驗證的資料類型值。|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|無法在這個位置插入 ParamValue。 指定的索引可能小於零或大於長度。|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|輸入的 WSDL 檔案無效。|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|同步處理物件失敗。|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|遺漏 WQL 查詢。|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|必須設定目的地。|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|未設定 WMI 連接。|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI 資料讀取器工作收到無效的工作資料節點。|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|工作驗證失敗。|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|檔案 "%1" 不存在。|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|連接管理員 "%1" 不存在。|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|變數 "%1" 不是字串或物件類型。|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|連接 "%1" 不是 "FILE" 類型。|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|連接 "%1" 不是 "WMI" 類型。|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|檔案 "%1" 已經存在。|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|連接管理員 "%1" 是空的。|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|變數 "%1" 應該是物件類型，才能指派資料表給它。|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|工作失敗，因為無效的 WMI 查詢: "%1"。|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|無法寫入變數 "%1"，因為它設定為保留原始值。|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|同步處理物件失敗。|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|遺漏 WQL 查詢。|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|遺漏 WMI 連接。|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|工作無法執行 WMI 查詢。|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|WMI 事件監看員工作收到無效的工作資料節點。|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|連接管理員 "%1" 不存在。|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|檔案 "%1" 不存在。|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|變數 "%1" 不是字串類型。|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|連接 "%1" 不是 "FILE" 類型。|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|連接 "%1" 不是 "WMI" 類型。|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|檔案 "%1" 已經存在。|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|連接管理員 "%1" 是空的。|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|在 "%2" 所代表的事件之前，發生逾時 "%1" 秒。|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|監看 Wql 查詢時，造成下列系統例外狀況: "%1"。 請檢查查詢是否有錯誤，或檢查 WMI 連接的存取權限。|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|未定義指定的作業。|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|連接類型不是 File。|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|無法從來源 XML 文件取得 XmlReader。|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|無法從變更的 XML 文件取得 XmlReader。|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|無法從 XDL diffgram XML 取得 XDL diffgram 讀取器。|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|節點清單是空的。|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|找不到元素。|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|未定義指定的作業。|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|XPathNavigator 包含非預期的內容項目。|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|找不到要強制驗證的結構描述。|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|驗證執行個體文件時發生驗證錯誤。|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|同步處理物件失敗。|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|根節點不相符。|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|最終編輯指令碼中的編輯指令碼作業類型無效。|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|應該使用 DiffgramAddSubtrees 類別加入 CDATA 節點。|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|應該使用 DiffgramAddSubtrees 類別加入註解節點。|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|應該使用 DiffgramAddSubtrees 類別加入文字節點。|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|應該使用 DiffgramAddSubtrees 類別加入重要空格節點。|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|更正 OperationCost 陣列來反映 XmlDiffOperation 列舉。|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|工作中沒有作業。|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|文件已經包含資料，不可重複使用。|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|節點類型無效。|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|XML 工作收到無效的工作資料節點。|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|變數資料類型不是 String。|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|無法從 XML 取得編碼。|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|未指定來源。|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|未指定第二個運算元。|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|無效的 XDL diffgram。 "%1" 是無效的路徑描述項。|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|無效的 XDL diffgram。 沒有節點符合路徑描述項 "%1"。|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|無效的 XDL diffgram。 必須以 xd:xmldiff 做為命名空間 URI "%1" 的根元素。|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|XDL diffgram 無效。 xd:xmldiff 元素遺漏 srcDocHash 屬性。|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|XDL diffgram 無效。 xd:xmldiff 元素遺漏 options 屬性。|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|XDL diffgram 無效。 srcDocHash 屬性有無效的值。|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|XDL diffgram 無效。 options 屬性有無效的值。|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|XDL diffgram 不適用於此 XML 文件。 rcDocHash 值不相符。|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|無效的 XDL diffgram; 在 xd:node 或 xd:change 元素上，有一個以上的節點符合 "%1" 路徑描述項。|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|XDL diffgram 不適用於此 XML 文件。 無法加入新的 XML 宣告。|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|內部錯誤。 XmlDiffPathSingleNodeList 只能包含一個節點。|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|內部錯誤。 修補之後剩餘 "%1" 個節點，必須是 1。|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|XSLT 產生的檔案/文字不是有效的 XmlDocument，因此不能設定為作業的結果: "%1"。|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|沒有與連接 "%1" 相關聯的檔案。|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|屬性 "%1" 沒有來源 Xml 文字; Xml 文字無效、為 Null 或空的字串。|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|檔案 "%1" 已經存在。|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|必須指定來源連接。|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|必須指定目的地連接。|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|在封裝中找不到連接 "%1"。|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|連接 "%1" 指定的 SQL Server 執行個體的版本並無傳送支援。  支援的只有 7、2000 及 2005 等版本。|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|來源連接 "%1" 必須指定版本早於或等於目的地連接 "%2" 的 SQL Server 執行個體。|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|必須指定來源資料庫。|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|來源伺服器上必須存在來源資料庫 "%1"。|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|必須指定目的地資料庫。|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|來源資料庫與目的地資料庫不能相同。|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|傳送檔案資訊 %1 遺漏檔名。|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|傳送檔案資訊 %1 遺漏資料夾部分。|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|傳送檔案資訊 %1 遺漏網路共用部分。|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|來源傳送檔案的數目與目的地傳送檔案的數目必須相同。|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|不支援在交易中編列。|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|進行離線資料庫傳送時發生以下例外狀況: %1。|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|找不到網路共用 "%1"。|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|無法存取網路共用 "%1"。  錯誤為: %2。|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|使用者 "%1" 必須是 "%2" 的 DBO 或系統管理員 (sysadmin)，才能執行線上資料庫傳送。|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|使用者 "%1" 必須是 "%2" 上的系統管理員 (sysadmin)，才能執行離線資料庫傳送。|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|只有在 2 部 SQL Server 2005 伺服器之間執行離線資料庫傳送時，才能包含全文檢索目錄。|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|目的地伺服器 "%2" 上已經有資料庫 "%1" 存在。|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|至少必須指定一個來源檔案。|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|在來源資料庫 "%2" 中找不到檔案 "%1"。|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|符合 U.S. FIPS 140-2 的系統上不允許要求的作業。|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|執行查詢 "%1" 失敗，發生下列錯誤: "%2"。 可能的失敗原因: 查詢發生問題、未正確設定 "ResultSet" 屬性、未正確設定參數，或未正確建立連接。|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|從 XML 檔案讀取預存程序名稱時發生錯誤。|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|傳送預存程序工作的資料節點無效。|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|連接 "%1" 的類型不是 "SMOServer"。|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|執行失敗，出現下列錯誤 "%1"。|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|發生錯誤，並出現下列錯誤訊息: "%1"。|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|大量插入執行失敗。|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|目的地路徑無效。|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|無法建立目錄。 使用者選擇如果目錄存在，就讓工作失敗。|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|工作的交易選項是 [必要的]，而連接 "%1" 的類型是 "ODBC"。 ODBC 連接不支援交易。|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|指派變數 "%1" 的值時發生錯誤: "%2"。|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|來源是空的。|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|目的地是空的。|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|檔案或目錄 "%1" 不存在。|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|變數 "%1" 要用來做為來源或目的地，但卻是空的。|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|已刪除檔案或目錄 "%1"。|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|已刪除目錄 "%1"。|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|變數 "%1" 應該是物件類型，才能指派資料表給它。|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|變數 "%1" 沒有字串資料類型。|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|取得 FTP 連接時發生錯誤。 請確認已在 "%1" 指定有效的連接類型。|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|找不到 FTP 連接管理員 "%1"。|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|作業 "%3" 之連接 "%1" 的檔案使用類型應該為 "%2"。|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|來源伺服器不能與目的地伺服器一樣。|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|沒有要傳送的錯誤訊息。|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|錯誤訊息清單以及對應之語言清單的大小不同。|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|錯誤訊息識別碼 "%1" 超出使用者定義錯誤訊息的容許範圍。 使用者定義錯誤訊息識別碼介於 50000 和 2147483647 之間。|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|此工作不能參與交易。|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|無法傳送部分或全部錯誤訊息。|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|目的地伺服器上已有錯誤訊息 "%1"。|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|在來源伺服器端找不到錯誤訊息 "%1"。|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|執行失敗，出現下列錯誤: "%1"。|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|無法傳送作業。|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|沒有要傳送的作業。|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|目的地伺服器上已有作業 "%1"。|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|在來源伺服器上找不到作業 "%1"。|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|要傳送的登入清單是空的。|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|無法從來源伺服器取得登入清單。|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|目的地伺服器上已有登入 "%1" 存在。|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|來源端沒有登入 "%1" 存在。|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|無法傳送部分或全部登入。|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|無法傳送預存程序。 應該要引發詳細資訊的錯誤。|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|在來源端找不到預存程序 "%1"。|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|目的地伺服器端已有預存程序 "%1"。|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|沒有要傳送的預存程序。|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|無法傳送物件。|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|要傳送的「物件」清單是空的。|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|來源端沒有預存程序 "%1" 存在。|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|目的地端已有預存程序 "%1"。|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|嘗試設定要傳送的預存程序清單時發生錯誤: "%1"。|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|來源端沒有規則 "%1" 存在。|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|目的地端已有規則 "%1"。|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|嘗試設定要傳送的規則清單時發生錯誤: "%1"。|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|來源端沒有資料表 "%1" 存在。|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|目的地端已有資料表 "%1"。|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|嘗試設定要傳送的資料表清單時發生錯誤: "%1"。|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|來源端沒有檢視表 "%1" 存在。|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|目的地端已有檢視表 "%1"。|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|嘗試設定要傳送的檢視表清單時發生錯誤: "%1"。|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|來源端沒有使用者定義函數 "%1" 存在。|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|目的地端已有使用者定義函數 "%1"。|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|嘗試設定要傳送的使用者定義函數清單時發生錯誤: "%1"。|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|來源端沒有預設值 "%1" 存在。|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|目的地端已有預設值 "%1"。|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|嘗試設定要傳送的預設值清單時發生錯誤: "%1"。|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|來源端沒有使用者定義資料類型 "%1" 存在。|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|目的地端已有使用者定義資料類型 "%1"。|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|嘗試設定要傳送的使用者定義資料類型清單時發生錯誤: "%1"。|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|來源端沒有分割區函數 "%1" 存在。|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|目的地端已有分割區函數 "%1"。|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|嘗試設定要傳送的分割區函數清單時發生錯誤: "%1"。|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|來源端沒有分割區配置 "%1" 存在。|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|目的地端已有分割區配置 "%1"。|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|嘗試設定要傳送的分割區配置清單時發生錯誤: "%1"。|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|來源端沒有結構描述 "%1" 存在。|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|目的地端已有結構描述 "%1"。|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|嘗試設定要傳送的結構描述清單時發生錯誤: "%1"。|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|來源端沒有 SqlAssembly "%1" 存在。|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|目的地端已有 SqlAssembly "%1"。|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|嘗試傳送 SqlAssemblies 清單時發生錯誤: "%1"。|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|來源端沒有使用者定義彙總 "%1" 存在。|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|目的地端已有使用者定義彙總 "%1"。|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|嘗試設定要傳送的使用者定義彙總清單時發生錯誤: "%1"。|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|來源端沒有使用者定義型別 "%1" 存在。|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|目的地端已有使用者定義型別 "%1"。|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|嘗試設定要傳送的使用者定義型別清單時發生錯誤: "%1"。|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|來源端沒有 XmlSchemaCollection "%1" 存在。|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|目的地端已有 XmlSchemaCollection "%1"。|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|嘗試設定要傳送的 XmlSchemaCollections 清單時發生錯誤: "%1"。|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|只有在 SQL Server 2005 (含) 以後版本伺服器之間才支援 "%1" 類型的物件。|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|資料庫清單是空的。|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|來源端沒有登入 "%1" 存在。|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|目的地端已有登入 "%1"。|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|嘗試設定要傳送的登入清單時發生錯誤: "%1"。|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|來源端沒有使用者 "%1" 存在。|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|目的地端已有使用者 "%1"。|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|嘗試設定要傳送的使用者清單時發生錯誤: "%1"。|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|工作無法在交易中包含保留連接管理員。|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|無法以 Unicode 從 SQL Server 取得 XML 資料，因為提供者不支援 OUTPUTENCODING 屬性。|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|找不到 FTP 作業 "%1" 的檔案連接管理員 "%2"。|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"Logins" 是伺服器層級物件，不可先卸除，因為來源和目的地是同一部伺服器。 先卸除這些物件也會從來源移除登入。|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|"%1" 參數不可為負數。 (-1) 是使用於預設值。|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|無法載入 Data Flow 物件。 請檢查 Microsoft.SqlServer.PipelineXml.dll 是否已正確註冊。|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|無法儲存 Data Flow 物件。 請檢查 Microsoft.SqlServer.PipelineXml.dll 是否已正確註冊。|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|無法儲存 Data Flow 物件。|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|無法載入 Data Flow 物件。|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|無法儲存 Data Flow 物件。 不支援指定的格式。|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|無法載入 Data Flow 物件。 不支援指定的格式。|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|無法設定 Data Flow 物件的 XML 持續性事件屬性。|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|無法設定 Data Flow 物件的持續性 XML DOM 屬性。|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|無法設定 Data Flow 物件的持續性 XML ELEMENT 屬性。|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|無法設定 Data Flow 物件的 XML 持續性屬性。|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|無法取得 Data Flow 元件的自訂屬性集合。|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|執行樹狀目錄包含循環。|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|%1 物件 "%2" (%3!d!) 與配置已中斷連接。|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|配置物件的識別碼無效。|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|必要的輸入物件未連接路徑物件。|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 包含無效的同步輸入識別碼 %2!d!。|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 具有歷程識別碼 %2!d!，但應該要有 %3!d!。|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|封裝包含具有重複名稱 "%1" 和 "%2" 的兩個物件。|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|"%1" 和 "%2" 在相同的排除群組中，但沒有相同的同步輸入。|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|在相同集合中，兩個物件具有重複的歷程識別碼 %1!d!。 物件是 %2 和 %3。|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|配置驗證失敗。|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|一個或多個元件驗證失敗。|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|配置及一個或多個元件的驗證失敗。|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|資料流程工作引擎啟動時失敗，因為無法建立一個或多個必要的執行緒。|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|執行緒在初始化時無法建立 mutex。|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|執行緒在初始化時無法建立信號。|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|系統報告目前的記憶體負載為百分之 %1!d! 。 實體記憶體有 %2 個位元組，%3 個位元組可用。 虛擬記憶體有 %4 個位元組，%5 個位元組可用。 分頁檔有 %6 個位元組，%7 個位元組可用。|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|在配置 %1!d! 位元組時，緩衝區失敗 。|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|無法建立緩衝區管理員。|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|緩衝區類型 %1!d! 的大小為  %2!I64d! 位元組 。|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 標示為懸空，但已附加路徑。|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 驗證失敗，傳回錯誤碼 0x%2!8.8X!。|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 未通過執行後階段，傳回錯誤碼 0x%2!8.8X!。|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 未通過準備階段，傳回錯誤碼 0x%2!8.8X!。|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 未通過執行前階段，傳回錯誤碼 0x%2!8.8X!。|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 未通過清除階段，傳回錯誤碼 0x%2!8.8X!。|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 具有的歷程識別碼 %2!d!， 先前在資料流程工作中並未使用。|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|無法將 %1 連接到 %2，因為會造成循環。|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|無法比較資料類型 "%1"。 不支援比較此資料類型，所以它無法排序或做為索引鍵。|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|這個執行緒已經關閉，不接受緩衝區做為輸入。|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS 錯誤碼 DTS_E_THREADFAILED。  "%1" 執行緒已結束，錯誤碼為 0x%2!8.8X!。  在此之前可能已公佈過錯誤訊息，說明執行緒為何結束的詳細資訊。|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS 錯誤碼 DTS_E_PROCESSINPUTFAILED。  處理輸入 "%4" (%5!d!) 時，元件 "%1" (%2!d!) 上的 ProcessInput 方法失敗，錯誤碼為 0x%3!8.8X! 。 識別的元件從 ProcessInput 方法傳回錯誤。 此錯誤是元件特定的錯誤，但屬於嚴重錯誤，將導致資料流程工作停止執行。  在此之前可能已公佈過錯誤訊息，說明有關此失敗的詳細資訊。|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|無法實現一組虛擬緩衝區。|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|這個管線需要的執行緒數目是 %1!d! 個，已超出 %2!d! 個的系統限制。 為管線設定的執行緒需求數量太多。 可能是非同步輸出太多，或 EngineThreads 屬性設定太高。 請將管線拆解成多個封裝，或降低 EngineThreads 屬性的值。|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|資料流程引擎排程器無法取得配置中的來源計數。|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|資料流程引擎排程器無法取得配置中的目的地計數。|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|元件檢視無法使用。 請確定已經建立元件檢視。|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|元件檢視識別碼不正確。 元件檢視可能並未同步。 請嘗試釋放元件檢視再重新建立。|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|這個緩衝區未鎖定，無法操作。|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|資料流程工作無法配置記憶體來建立緩衝區定義。 緩衝區定義有 %1!d! 個資料行 。|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|資料流程工作無法註冊緩衝區類型。 類型具有 %1!d!  個資料行，且已用於 %2!d!. 執行樹狀目錄。|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|UsesDispositions 屬性無法變更初始值。 當編輯 XML 且修改 UsesDispositions 值時，就會發生這個問題。 這個值是在元件加入封裝時設定，不允許變更。|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|資料流程工作無法初始化必要的執行緒，無法開始執行。 執行緒先前已報告特定錯誤。|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|資料流程工作無法建立必要的執行緒，無法開始執行。 當發生記憶體不足的狀況時，通常會發生這個問題。|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|"%1" 的同步輸入無法設定為 "%2"，因為會造成循環。|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|名稱為 "%1" 的自訂屬性無效，因為已存在這個名稱的內建屬性。 在相同物件上，自訂屬性的名稱不能與內建屬性的名稱相同。|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|緩衝區已經解除鎖定。|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 初始化失敗，傳回錯誤碼 0x%2!8.8X!。|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 在關閉期間失敗，傳回錯誤碼 0x%2!8.8X!。 元件無法釋放其介面。|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS 錯誤碼 DTS_E_PRIMEOUTPUTFAILED。  在 %1 上的 PrimeOutput 方法傳回錯誤碼 0x%2!8.8X!。  當管線引擎呼叫 PrimeOutput() 時，元件傳回失敗碼。 失敗碼的意義由元件定義，但屬於嚴重錯誤，管線已停止執行。  在此之前可能已公佈過錯誤訊息，說明有關此失敗的詳細資訊。|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS 錯誤碼 DTS_E_THREADCANCELLED。  "%1" 執行緒收到關閉信號，正在結束。 使用者已要求關閉，或另一個執行緒的錯誤造成管線關閉。  在此之前可能已公佈過錯誤訊息，說明執行緒為何取消的詳細資訊。|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|因為錯誤 0x%8.8X，執行緒 "%1" 的散發者無法在元件 "%3" 上初始化屬性 "%2"。 散發者無法初始化元件的屬性，無法繼續執行。|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|資料流程工作無法註冊檢視緩衝區類型。 類型具有 %1!d!  個資料行，且已用於輸入識別碼 %2!d!。|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|記憶體不足，無法建立執行樹狀目錄。|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|記憶體不足，無法將物件插入雜湊表。|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|物件不在雜湊表中。|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|無法建立元件檢視，因為有另一個元件檢視已經存在。 一次只能存在一個元件檢視。|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|在輸入 "%1" (%2!d!) 上，虛擬輸入資料行集合未包含歷程識別碼為 %3!d! 的虛擬輸入資料行。|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|要求的物件具有不正確的物件類型。|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|緩衝區管理員無法在 BufferTempStoragePath 屬性中的任何路徑上建立暫存檔。 檔案名稱不正確或沒有權限，或路徑已滿。|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|緩衝區管理員無法在檔案 "%2" 中尋找至位移 %1!d! 。 檔案已損毀。|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|緩衝區管理員無法將檔案 "%1" 擴充為 %2!lu! 位元組長度 。  磁碟空間不足。|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|緩衝區管理員無法將 %1!d! 位元組寫入檔案 "%2" 。 磁碟空間或配額不足。|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|緩衝區管理員無法從檔案 "%2" 讀取 %1!d! 位元組 。 檔案已損毀。|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|緩衝區識別碼 %1!d!  支援其他虛擬緩衝區，但無法設定為循序模式。 在支援虛擬緩衝區的緩衝區上呼叫 IDTSBuffer100.SetSequentialMode。|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|無法執行這項作業，因為緩衝區是唯讀模式。 無法修改唯讀緩衝區。|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|識別碼 %1 無法設定為 %2!d!， 因為會造成循環。|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|嘗試延伸緩衝區類型的資料表時，緩衝區管理員用完記憶體。 這個問題是記憶體不足所引起。|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|緩衝區管理員無法建立新的緩衝區類型。|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|資料流程引擎排程器無法從配置擷取索引 %1!d! 的執行樹狀目錄 。 排程器收到的執行樹狀目錄計數，超過實際存在的數目。|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|資料流程工作無法建立緩衝區，對元件 "%1" (%2!d!) 上的輸出 "%3" (%4!d!) 呼叫 PrimeOutput。 這個錯誤通常是因為記憶體不足所引起。|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|資料流程引擎排程器無法建立執行緒物件，因為記憶體不足。 這個問題是記憶體不足所引起。|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|資料流程引擎排程器無法從配置擷取識別碼為 %1!d! 的物件 。 資料流程引擎排程器先前找到的物件，現在已無法使用。|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|資料流程工作無法針對從輸出 "%1" (%2!d!) 開始的執行樹狀節點準備緩衝區。|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|資料流程工作無法建立準備執行的虛擬緩衝區。|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|已到達最大識別碼。 已經沒有識別碼可以指派給物件。|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|%1 已經附加，無法再次附加。  請先卸離，然後再試一次。|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|無法使用輸出 "%2" 上的資料行名稱 "%1"，因為與同步輸入 "%3" 上相同名稱的資料行衝突。|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|資料流程工作無法建立緩衝區來標示資料列集結尾。|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|Managed 使用者元件擲回例外狀況 "%1"。|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|資料流程引擎排程器無法為執行結構配置足夠的記憶體。 在開始執行之前，系統的記憶體偏低。|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|記憶體不足，導致無法建立緩衝區物件。|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|記憶體不足的狀況，導致無法將緩衝區的歷程識別碼對應至 DTP_HCOL 索引。|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!"  無法快取 Variables 集合，傳回錯誤碼 0x%2!8.8X。|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1" 無法快取元件中繼資料物件，傳回錯誤碼 0x%2!8.8X!。|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" 具有非零的 SortKeyPosition，但值 (%2!ld!) 太大。 必須小於或等於資料行數目。|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|%1 的 IsSorted 屬性設定為 TRUE，但非零輸出資料行 SortKeyPositions 的絕對值，未形成從 1 開始的單純遞增序列。|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" 驗證失敗，傳回驗證狀態 "%2"。|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|元件 "%1!s!"  無法建立，傳回錯誤碼 0x%2!8.8X! "%3!s!"。 請確定元件已正確註冊。|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|未正確註冊或安裝包含 "%1" 的模組。|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|雖然包含 "%1" 的模組已註冊，但找不到。|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|指令碼元件設定為先行編譯指令碼，但是找不到二進位碼。 請按一下 [設計指令碼] 按鈕，移至指令碼元件編輯器中的 IDE，以產生二進位碼。|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|對於 BLOBTempStoragePath 屬性指定目錄中的 Long 物件，緩衝區管理員無法建立檔案來進行多工緩衝處理。  可能提供不正確的檔案名稱，或沒有權限，或路徑已滿。|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|"%1" 上的 SynchronousInputID 屬性是 %2!d!，必須為 %3!d! 。|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|不存在識別碼為 %1!d! 的物件。|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|因為錯誤碼 0x%2!8.8X!，找不到識別碼為 %1!d! 的物件 。|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|輸出資料行 "%2" (%3!d!) 指定的字碼頁 %1!d! 無效 。 請為輸出資料行 "%2" 選取不同的字碼頁。|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|"%1" 無法快取 EventInfos 集合，傳回錯誤碼 0x%2!8.8X!。|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|"%1" 的名稱重複。  所有名稱都必須是唯一的。|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|輸入資料行 "%1" (%2!d!) 沒有相關聯的輸出資料行。|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" 具有從根來源延伸的虛擬緩衝區。 非零的排除群組具有零的同步輸入。|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" 不可以是錯誤輸出，因為錯誤輸出不能放在同步、非獨佔的輸出上。|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|發生除以零的錯誤。 在運算式 "%1" 中，右邊運算元等於零。|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|常值 "%1" 太大，以致於無法納入類型 %2 中。 常值的大小造成此類型溢位。|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|在資料類型 %2 和 %3 執行二進位運算 "%1" 的結果，超出數值類型的大小上限。 運算元類型隱含轉換成數值 (DT_NUMERIC) 結果時，一定會遺失有效位數或小數位數。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|二進位運算 "%1" 的結果超出結果資料類型 "%2" 的大小上限。 運算結果的大小造成結果類型溢位。|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|函數呼叫 "%1" 的結果太大，以致於無法納入類型 "%2" 中。 函數呼叫的結果大小會造成運算元類型溢位。 可能需要明確轉換成較大的類型。|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|對二元運算子 "%3" 而言，資料類型 "%1" 和 "%2" 不相容。 運算元類型無法隱含轉換成運算相容的類型。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|資料類型 "%1" 不能用於二元運算子 "%2"。 運算不支援一或兩個運算元的類型。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|在運算 "%2" 中，位元二元運算子 "%1" 的符號不相符。 這個運算子的兩個運算元必須同為正數或負數。|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|二進位運算 "%1" 失敗，錯誤碼為 0x%2!8.8X!。 發生內部錯誤，或存在記憶體不足的狀況。|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|嘗試設定二進位運算 "%1" 的結果類型失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|比較 "%1" 和字串 "%2" 失敗。|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|資料類型 "%1" 不能用於一元運算子 "%2"。 運算不支援這個運算元類型。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|一元運算 "%1" 失敗，錯誤碼為 0x%2!8.8X!。 發生內部錯誤，或存在記憶體不足的狀況。|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|嘗試設定一元運算 "%1" 的結果類型失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|函數 "%1" 不支援參數編號 %3!d! 的資料類型 "%2"。 參數的類型無法隱含轉換成函數相容的類型。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|無法辨識函數 "%1"。 函數名稱不正確或不存在。|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|對函數 "%2" 而言，長度 %1!d!  無效。 長度參數不可以是負數。 請將長度參數變更為零或正值。|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|函數 "%2" 的起始索引 %1!d!  無效。 起始索引值必須是大於 0 的整數。 起始索引以一為基底，不是以零為基底。|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|函數 "%1" 無法在字串 "%2" 上執行字元對應。|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|對函數 "%2" 而言，"%1" 不是有效的日期部分。|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|在函數 NULL 中，資料類型為 "%2" 的參數編號 %1!d! 不是整數 。 NULL() 的參數必須是靜態，不能包含動態元素，例如輸入資料行。|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|在函數 NULL 中，資料類型為 "%2" 的參數編號 %1!d! 不是整數 。 NULL() 的參數必須是整數或可以轉換成整數的類型。|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|在函數 NULL 中，資料類型為 "%2" 的參數編號 %1!d! 不是整數 不是靜態。 這個參數必須是靜態，不能包含動態元素，例如輸入資料行。|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|在函數 NULL 中，資料類型為 "%2" 的參數編號 %1!d! 不是整數 。 轉換運算子的參數必須是靜態，且不能包含動態元素，例如輸入資料行。|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|在函數 NULL 中，資料類型為 "%2" 的參數編號 %1!d! 不是整數 。 轉換運算子的參數必須是整數或可以轉換成整數的類型。|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|運算式 "%1" 無法從資料類型 "%2" 轉換成資料類型 "%3"。 不支援要求的轉換。|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|嘗試剖析運算式 "%1" 失敗。  無法辨識行號 "%3"、字元編號 "%4" 的 Token "%2"。 無法剖析運算式，因為它在指定的位置上包含無效的元素。|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|剖析運算式 "%1" 時發生錯誤。 未知的原因導致運算式剖析失敗。|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|嘗試剖析運算式 "%1" 失敗，傳回錯誤碼 0x%2!8.8X!。 無法剖析運算式。 可能包含無效的元素或格式不正確。 也可能發生記憶體不足的錯誤。|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|運算式 "%1" 無效，無法剖析。 運算式可能包含無效元素或格式不正確。|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|沒有可以計算的運算式。 嘗試計算或取得空運算式的字串。|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|嘗試計算運算式 "%1" 失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|嘗試產生運算式的字串表示失敗，錯誤碼為 0x%1!8.8X!。 嘗試產生表示運算式的可顯示字串時失敗。|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|無法將運算式結果資料類型 "%1" 轉換成資料行資料類型 "%2"。 運算式的結果應該寫入輸入/輸出資料行，但運算式的資料類型無法轉換成資料行的資料類型。|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|條件運算子的條件運算式 "%1" 具有無效的資料類型 "%2"。 條件運算子的條件運算式必須傳回布林值，也就是類型 DT_BOOL。|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|對條件運算子而言，資料類型 "%1" 和 "%2" 不相容。 運算元類型無法隱含轉換成條件運算相容的類型。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|嘗試設定條件運算 "%1" 的結果類型失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|這個緩衝區已經被遺棄。 緩衝區管理員已關閉，留下尚未處理完畢的緩衝區，將不會清除緩衝區。 可能會發生記憶體遺漏或其他問題。|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|嘗試尋找名稱為 "%1" 的輸入資料行失敗，錯誤碼為 0x%2!8.8X!。 在輸入資料行集合中找不到指定的輸入資料行。|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|嘗試尋找歷程識別碼為 %1!d! 的輸入資料行失敗，錯誤碼為 0x%2!8.8X! 。 在輸入資料行集合中找不到此輸入資料行。|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|運算式包含無法辨識的 Token "%1"。 如果 "%1" 是變數，則必須以 "@%1" 表示。 指定的 Token 無效。 如果 Token 要做為變數名稱，則必須以 @ 符號為字首。|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|運算式包含無法辨識的 Token "#%1!d!"。|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|在 Variables 集合中找不到變數 "%1"。 變數可能不存在於正確的範圍中。|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|嘗試剖析運算式 "%1" 失敗。 運算式可能包含無效 Token、不完整的 Token 或無效元素， 可能是格式不正確，或遺漏部分必要元素，例如括號。|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|"%1" 的名稱是空白，但名稱不可以是空白。|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|"%1" 將 HasSideEffects 屬性設定為 TRUE，但 "%1" 為同步，不能有副作用。 請將 HasSideEffects 屬性設定為 FALSE。|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|在轉換成資料類型 "%2" 的運算中，為字碼頁參數指定的值 %1!d! 無效。 電腦上未安裝此字碼頁。|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|值 %1!d! 未辨識為有效的存取模式 。 有效位數必須在 %3!d! 到 %4!d! 的範圍內 ， 但有效位數值超出類型轉換的範圍。|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|值 %1!d! 未辨識為有效的存取模式 。 小數位數必須在 %3!d! 到 %4!d! 的範圍內 ， 但小數位數值超出類型轉換的範圍。 小數位數不得超出有效位數，且必須為正數。|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|"%1" 的 IsSorted 屬性為 false，但輸出資料行的 SortKeyPositions 的 %2!lu! 不是零 。|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|在類型 %2 的條件運算 "%1" 中，運算元的字碼頁必須相符。 左邊運算元的字碼頁不符合右邊運算元的字碼頁。 對指定類型的條件運算子而言，字碼頁必須相同。|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|輸入 "%1" (%2!d!) 參考輸入 "%3" (%4!d!)，但沒有相同的資料行數目。 輸入 %5!d! 有 %6!d! 個 資料行 ，輸入 %7!d! 有 %8!d! 個 資料行 。|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|不存在歷程識別碼為 %1!d! 的物件。|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|找不到檔案名稱的輸出資料行。|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|檔案名稱的輸出資料行不是以 Null 結束的 Unicode 字元字串，也就是資料類型 DT_WSTR。|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|因為錯誤 0x%2!8.8X!，散發者無法提供緩衝區給執行緒 "%1"。 目標執行緒可能已關閉。|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|這個系統未安裝 LocaleID %1!ld! 。|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|字串常值 "%1" 包含不合法的十六進位逸出序列 "\x%2"。 在運算式評估工具中，字串常值不支援逸出序列。 十六進位逸出序列必須是 \xhhhh 格式，其中 h 是有效的十六進位數。|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|字串常值 "%1" 包含不合法的逸出序列 "\\%2!c!"。 在運算式評估工具中，字串常值不支援逸出序列。 如果字串中需要反斜線，請使用雙反斜線 "\\\\"。|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" 未包含輸出資料行。 非同步輸出必須包含輸出資料行。|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|"%1" 具有 Long 物件資料類型 DT_TEXT、DT_NTEXT 或 DT_IMAGE，但不受支援。|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|輸出識別碼 %1!d!  有多個錯誤輸出組態。 第一個為 %2!d!  和 %3!d!，接著為 %4!d!  和 %5!d!。|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|在 "%1" 的資料類型轉換驗證期間，OLE DB 提供者失敗。|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|這個緩衝區表示資料列集結尾，無法變更資料列計數。  在具有資料列集結尾旗標的緩衝區上，嘗試呼叫 AddRow 或 RemoveRow。|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|運算式不支援資料類型 "%1"。 指定的類型不受支援或無效。|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|在 "%1" 上的 PrimeOutput 方法傳回成功，但未報告資料列集結尾。 此為元件中的錯誤。 應該報告資料列結尾。 管線將停止執行，避免無法預期的結果。|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|從資料類型 "%1" 轉換成資料類型 "%2" 時發生溢位。 來源類型對目的地類型而言太大。|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|不支援從資料類型 "%1" 轉換成資料類型 "%2"。 來源類型無法轉換成目的地類型。|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|嘗試從資料類型 %2 轉換成資料類型 %3 時發生錯誤，錯誤碼為 0x%1!8.8X! 。|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|條件運算 "%1" 失敗，錯誤碼為 0x%2!8.8X!。 發生內部錯誤或記憶體不足的錯誤。|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|將運算式 "%1" 從資料類型 "%2" 轉換成資料類型 "%3" 失敗，錯誤碼 0x%4!8.8X!。|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|評估函數 "%1" 失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|在函數 NULL 中，資料類型為 "%2" 的參數編號 %1!d! 不是整數 無法轉換成靜態值。|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|當快速載入選項已開啟且插入認可大小上限設定為零時，在 "%1" 上的錯誤資料列配置不能設定將資料列重新導向。|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|在類型 "%2" 的二元運算子 "%1" 中，運算元的字碼頁必須相符。 目前，左邊運算元的字碼頁不符合右邊運算元的字碼頁。 對指定類型的指定二元運算子而言，字碼頁必須相同。|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|擷取變數 "%1" 的值失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|運算式不支援變數 "%1" 的資料類型。|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|無法將運算式 "%1" 從資料類型 "%2" 轉換成資料類型 "%3"，因為要轉換之值的字碼頁 (%4!d!) 不符合要求的結果字碼頁 (%5!d!)。 來源的字碼頁必須符合目的地要求的字碼頁。|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|預設緩衝區大小必須介於 %1!d!  與 %2!d! 的資料行 。 嘗試將 DefaultBufferSize 屬性設定為太小或太大的值。|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|預設緩衝區最大資料列數必須大於 %1!d! 個資料列 資料列。 嘗試將 DefaultBufferMaxRows 屬性設定為太小的值。|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|%1 的字碼頁為 %2!d!， 但必須是 %3!d!。|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|無法將 %3!d! 指派給資料流程工作的 EngineThreads 屬性 。 值必須介於 %1!d! 至 %2!d! 之間 。|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|剖析運算式 "%1" 失敗。 行號 "%2"、字元編號 "%3" 的單引號為非預期的。|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|剖析運算式 "%1" 失敗。 不需要行號 "%2"、字元編號 "%3" 上的等號 (=)。 在指定的位置上可能需要雙等號 (==)。|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|元件 "%1" 無法快取執行階段物件參考追蹤程式集合，傳回錯誤碼 0x%2!8.8X!。|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|多個輸入資料行的名稱為 "%1"。 所要的輸入資料行必須唯一指定為 [Component Name].[%2]，或以歷程識別碼來參考。 目前，指定的輸入資料行存在於一個以上的元件中。|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|尋找名稱為 "[%1].[%2]" 的輸入資料行失敗，錯誤碼為 0x%3!8.8X!。 在輸入資料行集合中找不到此輸入資料行。|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|多個變數的名稱為 "%1"。 所要的變數必須唯一指定為 @[Namespace::%2]。 此變數存在於一個以上的命名空間中。|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|資料流程引擎排程器無法縮減管線的執行計畫。 請將 OptimizedMode 屬性設定為 false。|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|函數 SQRT 無法用於負值，而且負值已傳遞至 SQRT 函數。|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|函數 LN 無法用於零或負值，而且零或負值已傳遞至 LN 函數。|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|函數 LOG 無法用於零或負值，而且零或負值已傳遞至 LOG 函數。|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|無法評估傳遞至函數 POWER 的參數，而且產生未定的結果。|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|因為錯誤 0x%1!8.8X!，所以執行階段無法提供取消事件。|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|管線收到取消的要求，正在關閉中。|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|一元減號 (負) 運算的結果 "%1" 超出結果資料類型 "%2" 的大小上限。 運算結果的大小造成結果類型溢位。|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|運算式中發現預留位置 "%1"。 必須使用實際參數或運算元取代。|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|對函數 "%2" 而言，長度 %1!d!  。 長度參數必須為正數。|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|重複計數 %1!d! 是負的，對函數 "%2" 而言無效 。 重複計數參數不可以是負的。|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|讀取變數 "%1" 失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|對二進位運算的運算元而言，僅輸入資料行和轉換運算才支援資料類型 DT_STR。 運算式 "%1" 包含 DT_STR 運算元，但不是輸入資料行或轉換結果，無法用於二進位運算。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|對條件運算子的運算元而言，僅輸入資料行和轉換運算才支援資料類型 DT_STR。 運算式 "%1" 包含 DT_STR 運算元，但不是輸入資料行或轉換結果，無法用於條件運算。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|函數 "%2" 的發生計數 %1!d! 無效 無效。 這個參數必須大於零。|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" 無法快取 LogEntryInfos 集合，傳回錯誤碼 0x%2!8.8X!。|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|為函數 "%1" 指定的日期部分參數無效。 必須是靜態字串。  日期部分參數不能包含動態元素 (如輸入資料行)，且必須是 DT_WSTR 類型。|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|值 %1!d! 未辨識為有效的存取模式 。 長度必須是正數。|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|值 %1!d! 未辨識為有效的存取模式 。 電腦上未安裝此字碼頁。|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|值 %1!d! 未辨識為有效的存取模式 。 有效位數必須在 %3!d! 到 %4!d! 的範圍內 。|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|值 %1!d! 未辨識為有效的存取模式 。 小數位數必須在 %3!d! 到 %4!d! 的範圍內 。 小數位數不得超出有效位數，且不得為負數。|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|值 %1!d! 未辨識為有效的存取模式 。 長度必須是正數。|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|無法指派負值給 %1。|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|"%2" 的 "%1" 自訂屬性不能設定為 true。  資料行資料類型必須是下列其中一個: DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4、DT_UI8、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAMPOFFSET、DT_DATE、DT_DBDATE、DT_DBTIME、DT_DBTIME2 或 DT_FILETIME。|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|無法重新附加 "%1"。 請刪除路徑、加入新路徑，然後再附加。|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|函數 "%1" 需要 %2!d! 參數， 而非 %3!d!  參數。 已辨識函數名稱，但參數數目無效。|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|函數 "%1" 需要 %2!d! 參數， 而非 %3!d!  參數。 已辨識函數名稱，但參數數目無效。|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|函數 "%1" 需要 %2!d! 參數， 而非 %3!d!  參數。 已辨識函數名稱，但參數數目無效。|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|發生記憶體不足錯誤，因此嘗試剖析運算式 "%1" 失敗。|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 無法執行其必要產品層級檢查而傳回錯誤碼 0x%2!8.8X!。|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS 錯誤碼 DTS_E_PRODUCTLEVELTOLOW。  %1 無法在已安裝的 Integration Services %2 版本上執行。 它需要 %3 (含) 以上版本。|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|運算式中的字串常值超出最大容許長度 %1!d! 個字元 字元。|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|變數 %1 包含的字串超出最大容許長度 %2!d! 個字元 字元。|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|找到 %1，但是它不支援必要的 Integration Services 介面 (IDTSRuntimeComponent100)。  請向元件提供者取得這個元件的更新版本。|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|無法開啟登錄機碼 "%1"。|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|無法為 CLSID 為 "%1" 的元件取得檔案名稱。 請確認已正確註冊元件或提供的 CLSID 正確無誤。|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|其中一個元件的 CLSID 無效。 請確認管線中所有元件的 CLSID 有效。|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|其中一個識別碼為 %1!d! 的元件的 CLSID 無效 無效。|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|索引無效。|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|無法存取 Application 物件。 請確認已經正確安裝 SSIS。|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|擷取元件的檔案名稱失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|無法從識別碼為 %2!d! 的元件擷取屬性 "%1"。|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|嘗試在資料流程工作中多次使用識別碼 %1!d! 。|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|從未包含資料行的集合中，無法依據歷程識別碼擷取項目。|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|因為錯誤碼 0x%2!8.8X!，在連接管理員集合中找不到識別碼為 "%1" 的連接管理員。 在 "%4" 的連接管理員集合中，"%3" 需要此連接管理員。 請確認在連接管理員集合 Connections 中已經使用此識別碼建立連接管理員。|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|執行緒 "%1" 收到輸入 %2!d! 的緩衝區，但這個執行緒不負責該輸入。 發生錯誤，導致資料流程引擎排程器建立錯誤的執行計畫。|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|元件 "%1" (%2!d!) 無法提供 IDTSRuntimeComponent100 介面。|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|資料流程工作引擎嘗試複製緩衝區來指派另一個執行緒，但失敗。|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|資料流程工作引擎無法為緩衝區 %3!d 建立類型 %1!d! 的 檢視緩衝區來取代類型 %2!d! 。|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|緩衝區管理員無法在路徑 "%1" 上建立暫存檔。 不會再考慮使用此路徑做為暫存區。|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|緩衝區管理員嘗試將錯誤資料列發送到輸出，但此輸出未註冊為錯誤輸出。 在未將 IsErrorOut property 設定為 TRUE 的輸出上呼叫 DirectErrorRow。|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|在私用緩衝區上呼叫緩衝方法，但此私用緩衝區不支援這項作業。|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|私用模式緩衝區不支援這項作業。|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|在傳遞至 PrimeOutput 的緩衝區上，無法呼叫這項作業。 在 PrimeOutput 期間呼叫緩衝方法，但 PrimeOutput 期間不允許此呼叫。|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|在傳遞至 ProcessInput 的緩衝區上，無法呼叫這項作業。 在 ProcessInput 期間呼叫緩衝方法，但 ProcessInput 期間不允許此呼叫。|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|緩衝區管理員無法取得暫存檔名稱。|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|程式碼遇到太寬的資料行。|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|因為錯誤碼 0x%3!8.8X!，在 "%2" 的連接管理員集合 Connections 中，無法取得 "%1" 指定的執行階段連接管理員的識別碼。 請確認元件已經設定執行階段連接物件的 ConnectionManager.ID 屬性。|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|在 "%2" 連接管理員集合 Connections 中，"%1" 沒有 ID 屬性的值。 請確認元件已經設定執行階段連接物件的 ConnectionManagerID 屬性。|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|在執行期間無法變更中繼資料。|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|"%1" 的元件中繼資料無法升級到較新版的元件。 PerformUpgrade 方法失敗。|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|%1 的版本與這個 DataFlow 版本不相容。|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|元件遺漏、未註冊、無法升級或遺漏必要的介面。 這個元件的連絡資訊是 "%1"。|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|在錯誤的緩衝區上呼叫此方法。 未用於元件輸出的緩衝區不支援這項作業。|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|在運算式計算期間發生錯誤。|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|運算式發生除數為零的錯誤。|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|常值太大，以致於無法納入要求的類型中。|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|對數值類型的大小上限而言，二進位運算的結果太大。 運算元類型隱含轉換成數值 (DT_NUMERIC) 結果時，一定會遺失有效位數或小數位數。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|二進位運算的結果大小，造成結果資料類型的大小上限溢位。|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|函數呼叫的結果大太，以致於無法納入結果類型中，且造成運算元的類型溢位。 可能需要明確轉換成較大的類型。|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|搭配二元運算子使用了不相容的資料類型。 運算元類型無法隱含轉換成運算相容的類型。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|搭配二元運算子使用了不支援的資料類型。 運算不支援一個或兩個運算元的類型。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|位元二元運算子的符號不相符。 這個運算子的運算元必須同為正數或同為負數。|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|二進位運算失敗。 發生記憶體不足狀況或內部錯誤。|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|設定二進位運算的結果類型失敗。|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|無法比較兩個字串。|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|搭配一元運算子使用了不支援的資料類型。 運算不支援此運算元類型。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|一元運算失敗。 發生記憶體不足狀況或內部錯誤。|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|設定一元運算的結果類型失敗。|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|函數具有資料類型不受支援的參數。 此參數類型無法隱含轉換成函數相容的類型。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|運算式出現無效的函數名稱。 請確認函數名稱正確且存在。|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|對函數 SUBSTRING 而言，長度參數無效。 長度參數不可以是負數。|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|對函數 SUBSTRING 而言，起始索引無效。 起始索引值必須是大於零的整數。 起始索引以一為基底，不是以零為基底。|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|提供數目不正確的參數給函數。 已辨識此函數名稱，但參數數目不正確。|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|字元對應函數失敗。|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|對日期函數指定無法辨識的日期部分參數。|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|提供無效參數給函數 NULL。 NULL 的參數必須是靜態，不能包含動態元素，例如輸入資料行。|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|提供無效參數給函數 NULL。 NULL 的參數必須是整數，或可以轉換成整數的類型。|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|提供無效參數給函數。 這個參數必須是靜態，不能包含動態元素，例如輸入資料行。|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|提供無效參數給轉換運算。 轉換運算子的參數必須是靜態，不能包含動態元素，例如輸入資料行。|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|提供無效參數給轉換運算。 轉換運算子的參數必須是整數，或可以轉換成整數的類型。|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|運算式包含不支援的類型轉換。|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|運算式包含無法辨識的 Token。 無法剖析運算式，因為它包含無效元素。|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|運算式無效，無法剖析。 可能包含無效元素，或格式不正確。|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|一元減號 (負) 運算的結果，造成結果資料類型的大小上限溢位。 運算結果的大小造成結果類型溢位。|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|嘗試計算運算式失敗。|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|嘗試產生運算式的字串表示失敗。|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|無法將運算式結果資料類型轉換成資料行資料類型。 運算式的結果應該寫入輸入/輸出資料行，但運算式的資料類型無法轉換成資料行的資料類型。|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|條件運算子的條件運算式包含無效的資料類型。 條件運算式的類型必須是 DT_BOOL。|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|條件運算子的運算元資料類型不相容。 運算元類型無法隱含轉換成條件運算相容的類型。 若要執行此運算，必須使用轉換運算子，明確轉換一個或兩個運算元。|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|設定條件運算的結果類型失敗。|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|在輸入資料行集合中找不到指定的輸入資料行。|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|嘗試依據歷程識別碼尋找輸入資料行失敗。 在輸入資料行集合中找不到此輸入資料行。|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|運算式包含無法辨識的 Token (似乎是輸入資料行參考)，但輸入資料行集合無法用來處理輸入資料行。 尚未提供輸入資料行集合給運算式評估工具，但運算式包含輸入資料行。|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|在集合中找不到指定的變數。 可能不存在於正確的範圍中。 請確認變數存在且範圍正確。|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|嘗試剖析運算式失敗。 運算式包含無效或不完整的 Token。 它可能包含無效元素、遺漏部分必要的元素 (例如左括號) 或格式不正確。|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|在轉換成資料類型 DT_STR 或 DT_TEXT 的運算中，指定給字碼頁參數的值無效。 電腦上未安裝指定的字碼頁。|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|對轉換運算的有效位數參數所指定的值，超出類型轉換的範圍。|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|對轉換運算的小數位數參數所指定的值，超出類型轉換的範圍。 小數位數不得超出有效位數，且不得為負數。|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|條件運算中的字碼頁不相符。 左邊運算元的字碼頁不符合右邊運算元的字碼頁。 對此類型的條件運算子而言，字碼頁必須相同。|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|字串常值包含不合法的十六進位逸出序列。 在運算式評估工具中，字串常值不支援逸出序列。 十六進位逸出序列必須是 \xhhhh 格式，其中，h 是有效的十六進位數。|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|字串常值包含不合法的逸出序列。 在運算式評估工具中，字串常值不支援逸出序列。 如果字串中需要反斜線，請使用雙反斜線 "\\\\"。|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|運算式中使用了不支援或無法辨識的資料類型。|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|轉換資料類型時發生溢位。 來源類型太大，以致於無法納入目的地類型中。|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|運算式包含不支援的資料類型轉換。 來源類型無法轉換成目的地類型。|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|嘗試執行資料轉換時發生錯誤。 來源類型無法轉換成目的地類型。|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|條件運算失敗。|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|嘗試執行類型轉換時發生錯誤。|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|將 "%1" 從類型 DT_STR 轉換為類型 DT_WSTR 失敗，錯誤碼為 0x%2!8.8X!。 在輸入資料行上執行隱含轉換時發生錯誤。|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|將輸入資料行從類型 DT_STR 轉換成類型 DT_WSTR 失敗。 在輸入資料行上執行隱含轉換時發生錯誤。|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|評估函數時發生錯誤。|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|函數參數無法轉換成靜態值。 參數必須是靜態，不能包含動態元素，例如輸入資料行。|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|函數 RIGHT 的長度參數無效。 長度參數不可以是負數。|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|函數 REPLICATE 的重複計數參數無效。 這個參數不可以是負數。|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|二進位運算中的字碼頁不相符。 左邊運算元的字碼頁不符合右邊運算元的字碼頁。 對這個二進位運算而言，字碼頁必須相同。|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|擷取變數的值失敗。|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|運算式包含資料類型不受支援的變數。|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|無法轉換運算式，因為要轉換之值的字碼頁不符合要求的結果字碼頁。 來源的字碼頁必須符合目的地要求的字碼頁。|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|運算式包含非預期的單引號。 可能需要雙引號。|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|運算式包含非預期的等號 (=)。 當需要雙等號時 (==)，通常會發生這個錯誤。|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|指定了模糊不清的輸入資料行名稱。  資料行必須指定為 [Component Name].[Column Name] 或以歷程識別碼來參考。 當輸入資料行存在於一個以上的元件中時，就會發生這個錯誤，必須以其他元件名稱或歷程識別碼來區別。|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|在運算式中發現預留位置函數參數或運算元。 應該以實際參數或運算元取代。|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|指定了模稜兩可的變數名稱。 所要的變數必須指定為 @[Namespace::Variable]。 當變數存在於一個以上的命名空間中時，就會發生這個錯誤。|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|對二進位運算的運算元而言，僅輸入資料行和轉換運算才支援資料類型 DT_STR。 非輸入資料行或轉換結果的 DT_STR 運算元，不能用於二進位運算。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|對條件運算子的運算元而言，僅輸入資料行和轉換運算才支援資料類型 DT_STR。 非輸入資料行或轉換結果的 DT_STR 運算元，不能用於條件運算。 若要執行此運算，必須使用轉換運算子，明確轉換運算元。|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|函數 FINDSTRING 的發生計數參數無效。 這個參數必須大於零。|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|日期函數中指定的日期部分 (date part) 參數無效。 日期部分參數必須是靜態字串，不能包含動態元素，例如輸入資料行。 必須是 DT_WSTR 類型。|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|對轉換運算的長度參數所指定的值無效。 長度必須是正數。 指定給類型轉換的長度是負數。 請變更為正值。|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|對 NULL 函數的長度參數所指定的值無效。 長度必須是正數。 指定給 NULL 函數的長度是負數。 請變更為正值。|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|在資料類型為 DT_STR 或 DT_TEXT 的 NULL 函數中，為字碼頁參數指定的值無效。 電腦上未安裝指定的字碼頁。 請變更指定的字碼頁，或在電腦上安裝此字碼頁。|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|對 NULL 函數的有效位數參數所指定的值無效。 指定的有效位數超出 NULL 函數的範圍。|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|對 NULL 函數的小數位數參數所指定的值無效。 指定的小數位數超出 NULL 函數的範圍。 小數位數不得超出有效位數，且必須為正數。|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|%1 嘗試將資料寫入 %3 上的 %2 時失敗。 %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|查閱轉換收到使用者的取消要求。|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|字元或二進位大型物件 (LOB) 的處理已停止，因為達到了 4GB 的限制。|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|無法載入 Managed 管線元件 "%1"。  例外狀況為: %2。|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS 錯誤碼 DTS_E_OLEDB_EXCEL_NOT_SUPPORTED：64 位元版本的 SSIS 不支援 Excel 連接管理員，因為沒有 OLE DB 提供者可用。|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|快取檔案已損毀，或該檔案不是以快取連接管理員建立的。  請提供有效的快取檔案。|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|未正確設定 SQL 命令。 請檢查 SQLCommand 屬性。|  
|0xC0202002|-1071636478|DTS_E_COMERROR|有 COM 錯誤物件資訊可用。  來源: "%1"  錯誤碼: 0x%2!8.8X!  描述: "%3"。|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|無法存取已取得的連接。|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|資料行數目不正確。|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|在資料來源中找不到資料行 "%1"。|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|有 OLE DB 記錄可用。  來源: "%1" Hresult: 0x%2!8.8X!  描述: "%3"。|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS 錯誤碼 DTS_E_OLEDBERROR。  發生 OLE DB 錯誤。 錯誤碼：0x%1!8.8X!。|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|已經連接元件。 嘗試連接之前，元件必須中斷連接。|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|屬性 "%1" 的值不正確。|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|無法開啟資料檔 "%1"。|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|未提供目的地一般檔案名稱。 請確定一般檔案連接管理員已設定連接字串。 如果多個元件使用一般檔案連接管理員，請確定連接字串包含足夠的檔案名稱。|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|找不到資料行 "%1" 的文字限定詞。|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|不支援從 "%1" 到 "%2" 的轉換。|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|驗證從 %2 至 %3 的類型轉換時，傳回錯誤碼 0x%1!8.8X! 。|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|找不到歷程識別碼為 "%1!d!" 的輸入資料行， "%2" 需要該資料行。 請檢查輸出資料行的 SourceInputColumnLineageID 自訂屬性。|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|輸出數目不正確。 至少必須有 %1!d! 個輸出 。|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|輸出數目不正確。 必須正好是 %1!d! 個 輸出。|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|字串太長，無法轉換。|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|輸入數目不正確。 必須正好是 %1!d! 個 輸入。|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|%1 的輸入資料行數目不可以是零。|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|這個元件有 %1!d! 個 輸入。  這個元件不允許輸入。|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|使用無效的輸入識別碼 %1!d! 呼叫 ProcessInput。|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|自訂屬性 "%1" 必須是 %2 類型。|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|緩衝區類型無效。 請確定管線配置和所有元件都通過驗證。|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|自訂屬性 "%1" 的值不正確。|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|因為沒有連接而發生錯誤。 要求中繼資料時，需要連接。 如果您是離線工作，請在 SSIS 功能表上取消選取 [離線工作] 以啟用連接。|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|無法建立自訂屬性 "%1"。|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|無法擷取自訂屬性集合進行初始化。|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|無法建立 OLE DB 存取子。 請確認資料行中繼資料有效。|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|使用無效的輸出識別碼 %1!d! 呼叫 PrimeOutput。|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|在 "%2" 上，屬性 "%1" 的值無效。|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|需要連接才能讀取資料。|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|讀取標頭資料列時發生錯誤。|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|重複的資料行名稱 "%1"。|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|無法取得識別碼為 %1!d! 的資料行名稱。|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|將資料列導向到輸出 "%1" (%2!d!) 失敗。|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|因為錯誤 "%1"，無法建立大量插入執行緒。|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|SSIS 大量插入工作的執行緒初始化失敗。|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|SSIS 大量插入工作的執行緒已在執行中。|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|SSIS 大量插入工作的執行緒因錯誤或警告而結束。|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|無法開啟 "%1" 的快速載入 (FastLoad) 資料列集。 請檢查物件是否存在於資料庫中。|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|因為沒有連接而發生錯誤。 需要連接，才可以繼續中繼資料驗證。|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|尚未提供目的地資料表名稱。|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|OLE DB 配接器使用的 OLE DB 提供者不支援 IConvertType。 請將配接器的 ValidateColumnMetaData 屬性設定為 FALSE。|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|OLE DB 配接器使用的 OLE DB 提供者無法在 "%3" 的類型 "%1" 和 "%2" 之間轉換。|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|資料行中繼資料驗證失敗。|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" 是資料列識別碼資料行，不能包含在資料插入作業中。|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|嘗試插入到資料列版本資料行 "%1"。 無法插入到資料列版本資料行。|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|無法插入到唯讀資料行 "%1"。|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|無法從資料來源擷取資料行資訊。 請確定資料庫中的目標資料表可以使用。|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|無法鎖定緩衝區。 系統用完記憶體或緩衝區管理員已到達配額。|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|%1 的 ComparisonFlags 屬性包含值為 %2!d! 的額外旗標。|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|資料行中繼資料無法用於驗證。|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|無法寫入資料檔案。|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|找不到資料行 "%1" 的資料行分隔符號。|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|無法剖析資料檔案中的資料行 "%1"。|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|未正確指定檔案名稱。  請直接在 FileName 屬性中提供原始檔案的路徑與名稱，或在 FileNameVariable 屬性中指定變數以提供路徑與名稱。|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|無法開啟檔案 "%1" 進行寫入。 當沒有檔案權限或磁碟已滿時，就可能發生錯誤。|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|無法建立輸出檔的 I/O 緩衝區。 當沒有檔案權限或磁碟已滿時，就可能發生錯誤。|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|無法將 %1!d! 位元組寫入檔案 "%2" 。 如需詳細資料，請參閱先前的錯誤訊息。|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|在檔案標頭中發現不正確的中繼資料。 檔案已損毀或不是 SSIS 產生的原始資料檔案。|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|發生錯誤，因為輸出檔早已存在，而且 WriteOption 設定為 [建立一次]。 請將 WriteOption 屬性設定為 [永遠建立]，或者刪除檔案。|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|衝突的屬性設定造成錯誤。 AllowAppend 屬性和 ForceTruncate 屬性同時設定為 TRUE， 這兩個屬性不能同時設定為 TRUE。 請將兩個屬性的其中一個設定為 FALSE。|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|檔案具有不正確的版本和旗標資訊。 檔案已損毀或不是 SSIS 產生的原始資料檔案。|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|輸出檔是以不相容版本寫入，無法附加。 檔案可能是無法再使用的舊版檔案格式。|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|無法附加輸出檔，因為現有檔案中沒有資料行符合輸入的資料行 "%1"。 舊檔案的中繼資料不相符。|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|無法附加輸出檔，因為輸出檔的資料行數目不符合這個目的地的資料行數目。 舊檔案的中繼資料不相符。|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|擷取資料行字碼頁資訊時發生錯誤。|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|無法從檔案 "%2" 讀取 %1!d!  。 先前應該已經報告失敗的原因。|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|從檔案 "%2" 讀取 %1!d! 位元組時，發現非預期的檔案結尾 。 因為檔案的格式無效，所以檔案不當結束。|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|資料行 %1 無法使用。 原始配接器不支援 image、text 或 ntext 資料。|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|配接器發現無法辨識的資料類型 %1!d!。 這可能是損壞的輸入檔 (來源) 或無效的緩衝區類型 (目的地) 所引起。|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|字串太長。 配接器位移 %3!d! 上讀取長度為 %1!d! 位元組的字串， 但必須是長度不超過 %2!d! 位元組的字串 。 這可能表示損毀的輸入檔。 檔案指出字串長度太長，以致於無法納入緩衝區資料行中。|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|對於歷程識別碼為 %3!d! 的未參考資料行 "%2"， 原始配接器嘗試在輸入檔中略過 %1!d! 位元組，但發生錯誤。 先前應該已經報告作業系統傳回的錯誤。|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|對於歷程識別碼為 %3!d! 的資料行 "%2"， 原始配接器嘗試在輸入檔中讀取 %1!d! 位元組，但發生錯誤。 先前應該已經報告作業系統傳回的錯誤。|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|檔案名稱屬性無效。 檔案名稱是裝置或包含無效的字元。|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|無法準備 SSIS 大量插入來進行資料插入。|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|資料庫物件名稱 "%1" 無效。|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|排序子句無效。|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|無法開啟檔案 "%1" 進行讀取。 當沒有權限或找不到檔案時，就可能發生錯誤。 先前的錯誤訊息已報告確切的原因。|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|無法建立 Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator。|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|無法設定 Microsoft.AnalysisServices.TimeDimGenerator。|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|資料行 %1!d! 不支援的資料類型。|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|嘗試讀取 Microsoft.AnalysisServices.TimeDimGenerator 失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|嘗試讀取來自 Microsoft.AnalysisServices.TimeDimGenerator 的資料行 "%2!d!" 失敗， 錯誤碼為 0x%2!8.8X!。|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|VariableName 屬性未設定為有效變數的名稱。 需要可寫入的執行階段變數名稱。|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|無法建立或設定 ADODB.Recordset 物件。|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|寫入 ADODB.Recordset 物件時發生錯誤。|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|檔案名稱無效。 檔案名稱是裝置或包含無效的字元。|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|檔案名稱 "%1" 無效。 檔案名稱是裝置或包含無效的字元。|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|無法從 SQL 命令的參數擷取目的地資料行描述。|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|未繫結參數。 SQL 命令中的所有參數必須繫結到輸入資料行。|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|輸入資料行 "%1" (%2!d!) 的 PivotUsage 值無效。|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|發現太多樞紐索引鍵。 只有一個輸入資料行可以做為樞紐索引鍵。|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|找不到樞紐索引鍵。 必須使用一個輸入資料行做為樞紐索引鍵。|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|一個以上的輸出資料行 (例如 "%1" (%2!d!)) 對應到輸入資料行 "%3" (%4!d!)。|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|輸出資料行 "%1" (%2!d!) 無法對應到 PivotKey 輸入資料行。|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|輸出資料行 "%1" (%2!d!) 的 SourceColumn %3!d!  不是有效的輸入資料行歷程識別碼。|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|輸出資料行 "%1" (%2!d!) 對應到樞紐值輸入資料行，但遺漏其 PivotKeyValue 屬性值。|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|輸出資料行 "%1" (%2!d!) 對應到包含非唯一 PivotKeyValue 屬性值的樞紐值輸入資料行。|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|輸入資料行 "%1" (%2!d!) 未對應到任何輸出資料行。|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|比較集索引鍵的值時失敗。|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|輸入資料行 "%1" (%2!d!) 不能用於做為集索引鍵、樞紐索引鍵或樞紐值，因為包含 Long 資料。|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|不正確的輸出類型。 輸出資料行 "%1" (%2!d!) 的資料類型和中繼資料必須與對應的輸入資料行相同。|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|嘗試樞紐轉換來源記錄時失敗。|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|樞紐索引鍵值 "%1" 無效。|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|略過資料列時發生錯誤。|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|處理資料列 %2!I64d! 上的檔案 "%1" 時發生錯誤。|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|初始化一般檔案剖析器時發生錯誤。|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|無法從一般檔案連接管理員擷取資料行資訊。|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|無法輸出資料行 "%1" 的資料行名稱。|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|資料行 "%1" 的資料行類型不正確。 它的類型是 "%2"。 只能是 "%3" 或 "%4"。|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|嘗試將 %1!d! 個位元組的資料寫入磁碟 I/O 失敗 。 磁碟 I/O 緩衝區有 %2!d! 個可用的位元組 。|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|輸出檔案標頭時發生錯誤。|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|取得檔案 "%1" 的檔案大小時發生錯誤。|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|設定檔案 "%1" 的檔案指標時發生錯誤。|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|設定磁碟 I/O 緩衝區時發生錯誤。|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|資料行 "%1" 的資料行資料造成磁碟 I/O 緩衝區溢位。|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|讀取檔案時發生非預期的磁碟 I/O 錯誤。|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|讀取檔案時發生磁碟 I/O 逾時。|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|無法讀取/寫入對這個轉換的輸入資料行所指定的使用類型。 請將使用類型變更為唯讀。|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|無法為資料行 "%1" 複製或轉換一般檔案資料。|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|資料轉換失敗。 資料行 "%1" 的資料轉換傳回狀態值 %2!d! 和狀態文字 "%3" 。|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|無法使用 Variables 集合。|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|重複的 PivotKeyValue。 輸入資料行 "%1" (%2!d!) 對應到樞紐值輸出資料行，且具有非唯一的 PivotKeyValue。|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|找不到取消樞紐目的地。 至少一個輸入資料行必須以 PivotKeyValue 對應到輸出中的 DestinationColumn。|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue 無效。 在具有一個以上取消樞紐 DestinationColumn 的取消樞紐轉換中，每個目的地的 PivotKeyValues 集合必須完全相符。|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|不正確的 UnPivot 中繼資料。 在取消樞紐轉換中，所有已設定 PivotKeyValue 和指向相同 DestinationColumn 的輸入資料行，都必須有完全符合 DestinationColumn 的中繼資料。|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|無法將樞紐索引鍵值 "%1" 轉換成樞紐索引鍵資料行的資料類型。|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|指定太多樞紐索引鍵。 只有一個輸出資料行可以做為樞紐索引鍵。|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|沒有任何輸入資料行的 DestinationColumn 屬性對應輸出資料行 "%1" (%2!d!)。|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|沒有輸出資料行標示為 PivotKey。|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|輸入資料行 "%1" (%2!d!) 的 DestinationColumn 屬性值未參考有效的輸出資料行 LineageID。|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|重複目的地錯誤。 一個以上的非樞紐輸入資料行對應到相同目的地輸出資料行。|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|找不到輸入資料行。 至少一個輸入資料行必須對應到輸出資料行。|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|輸入和輸出資料行的數目不相等。 所有輸入上的輸入資料行總數必須等於輸出資料行總數。|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|輸入未排序。 必須排序 "%1"。|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|%1 的 JoinType 自訂屬性包含的值 %2!ld! 無效。 有效值是 0 (完整)、1 (左) 或 2 (內部)。|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|NumKeyColumns 值無效。 在 %1 中，NumKeyColumns 自訂屬性的值必須介於 1 到 %2!lu! 之間。|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|找不到索引鍵資料行。 %1 必須至少有一個資料行具有非零的 SortKeyPosition。|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|索引鍵資料行不足。 %1 必須至少有 %2!ld! 個 資料行具有非零的 SortKeyPosition 值。|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|發生資料類型不相符。 具有 SortKeyPosition 值 %1!ld! 的資料行的資料類型不符 。|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|具有 SortKeyPosition 值 %1!ld! 的資料行無效 無效。 應該是 %2!ld!。|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|排序方向不相符。 具有 SortKeyPosition 值 %1!ld! 的資料行的排序方向不符 。|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|遺漏資料行。 %1 必須有相關聯的輸入資料行。|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|輸入資料行必須有輸出資料行。 具有唯讀使用類型的輸入資料行，沒有相關聯的輸出資料行。|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|比較旗標不是零。 非字串資料行的比較旗標必須是零。|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|具有 SortKeyPosition 值 %1!ld! 的資料行的比較旗標不符 。|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|無法辨識的樞紐索引鍵值。|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|歷程項目值 %1!ld! 無效 無效。 有效範圍介於 %2!ld! 至 %3!ld! 之間 。|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|不允許輸入資料行。 輸入資料行的數目必須是零。|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|對指定的歷程項目而言，"%1" 的資料類型無效。|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|對指定的歷程項目而言，"%1" 的長度無效。|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|"%1" 的中繼資料不符合相關聯輸出資料行的中繼資料。|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|輸出資料行的 SortKeyPosition 值不符合相關聯輸入資料行的 SortKeyPosition。|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|嘗試將資料列加入資料流程工作緩衝區失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|將資料行 "%1" (%2!d!) 轉換成資料行 "%3" (%4!d!) 時，資料轉換失敗。  轉換傳回狀態值 %5!d! 和狀態文字 "%6" 。|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|嘗試配置資料列控制代碼緩衝區失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|嘗試將資料列傳送到 SQL Server 失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|嘗試準備緩衝區狀態失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|嘗試擷取緩衝區資料列的開頭失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|SSIS 大量插入的執行緒已停止執行。  無法再插入資料列。 請嘗試增加大量插入執行緒逾時值。|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|來源檔案無效。 來源檔案傳回超過 131,072 個資料行的計數。 當來源檔案不是從原始檔案目的地產生時，通常會發生這個問題。|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1 是未附加的多餘輸入，將會移除。|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|%1 未附加，但未標示為懸空。  將標示為懸空。|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|重複樞紐索引鍵值 "%1"。|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|重複樞紐索引鍵值。|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|無法擷取元件地區設定識別碼。 錯誤碼為 0x%1!8.8X!。|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|不相符的地區設定識別碼。 元件地區設定識別碼 (%1!d!) 不符合連接管理員地區設定識別碼 (%2!d!)。|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|未設定元件地區設定識別碼。 一般檔案配接器需要在一般檔案連接管理員上設定地區設定識別碼。|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|二進位欄位太大。 配接器嘗試讀取長度為 %1!d! 位元組的二進位欄位， 但在位移 %3!d! 上，欄位不能超過 %2!d! 位元組 。 當輸入檔無效時，通常會發生這個問題。 檔案包含太大的字串長度，以致於無法納入緩衝區資料行中。|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|對 "%1" 屬性而言，百分比值 %2!ld! 無效。 必須介於 0 和 100 之間。|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|對 "%1" 屬性而言，資料列數目 %2!ld! 無效。 必須大於 0。|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|要求配接器寫入的字串長度是 %1!I64d! 位元組， 但所有資料的長度必須小於 4294967295 位元組。|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|沒有輸入對應到輸出。 "%1" 至少必須有一個輸入資料行對應到輸出資料行。|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|不支援從字碼頁為 %2!d! 的 "%1" 轉換成字碼頁為  %4!d! 的 "%3" 。|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|%1 的外部中繼資料行對應無效。  外部中繼資料行識別碼不可以是零。|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|%1 對應到不存在的外部中繼資料行。|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|對於資料行 "%1"，將類型 DT_TEXT、DT_NTEXT 或 DT_IMAGE 的 Long 物件資料寫入資料流程工作緩衝區失敗。|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|開啟 "%1" 的資料列集失敗。 請檢查物件是否存在於資料庫中。|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|存取變數 "%1" 失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|找不到連接管理員 "%1"。 元件在 Connections 集合中找不到此連接管理員。|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|從版本 "%1" 升級到版本 %2!d! 失敗 。|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|輸入資料行的值太大，以致於無法儲存在 ADODB.Recordset 物件中。|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|資料行 "%1" 和 "%2" 無法在 Unicode 和非 Unicode 字串資料類型之間轉換。|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|VariableName 屬性指定的變數 "%1" 不是有效變數。 需要可寫入的有效變數名稱。|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|VariableName 屬性指定的變數 "%1" 不是整數。 請將變數變更為類型 VT_I4、VT_UI4、VT_I8 或 VT_UI8。|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|未指定讓元件在檔案中向前讀取的資料行。|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|"%1" 將 IsSorted 設定為 TRUE，但 SortKeyPosition 在所有輸出資料行上是零。 請將 IsSorted 變更為 FALSE，或至少選取一個輸出資料行來包含非零的 SortKeyPosition。|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|"%1" 中繼資料不符合輸入資料行的中繼資料。|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|找不到、無法鎖定或設定指定變數的值。|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|無法處理資料行 "%1"，因為指定一個以上的字碼頁 (%2!d! 和 %3!d!) 。|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|無法插入資料行 "%1"，因為不支援類型 %2 和 %3 之間的轉換。|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|資料行 "%1" 無法在 Unicode 和非 Unicode 字串資料類型之間轉換。|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1 在其輸入緩衝區中找不到 LineageID 為 %2!ld! 的資料行 。|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1 無法從其輸入緩衝區中取得資料行 "%2!lu!" 的資料行資訊 。|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|%1 無法從其複製緩衝區中取得資料行 "%2!lu!" 的 資料行資訊。|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1 無法註冊其複製緩衝區的緩衝區類型。|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1 無法建立要複製資料來排序的緩衝區。|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader 用戶端無法呼叫 Read 或已關閉 DataReader。|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|SQL 命令未傳回任何資料行資訊。|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1 無法擷取 SQL 命令的資料行資訊。 發生下列錯誤: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|尚未提供來源資料表名稱。|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|快取索引位置 %1!d! 無效。 對非索引資料行而言，索引位置應該是 0。 對索引資料行而言，索引位置則必須是連續的正數。|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|索引位置 %1!d! 重複。 對非索引資料行而言，索引位置應該是 0。 對索引資料行而言，索引位置則必須是連續的正數。|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|最後一個索引資料行必須指定給快取連接管理員。 若要指定索引資料行，必須設定快取資料行的索引位置屬性。|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|快取索引位置必須是連續的。 對非索引資料行而言，索引位置應該是 0。 對索引資料行而言，索引位置則必須是連續的正數。|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|"%2" 上不能設定屬性 "%1"。 指定的物件上不支援設定的屬性。 請檢查屬性名稱、大小寫和拼字。|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|無法變更元件所設定之類型的屬性類型。|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|輸出識別碼 %1!d!  失敗。 未建立新的輸出。|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|無法從輸出集合中刪除輸出識別碼 %1!d! 。  識別碼可能無效，或可能已做為預設或錯誤輸出。|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|無法在 "%2" 上設定屬性 "%1"。|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|無法將 %1 的類型設定為類型: "%2"、長度: %3!d!、有效位數: %4!d!、小數位數: %5!d!、字碼頁: %6!d!。|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|在元件上找到一個以上的錯誤輸出，但僅限於一個。|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|無法設定輸出資料行的屬性。|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|在錯誤 "%2" 中，無法修改 "%1" 的資料類型。|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|"%1" 無法將 IsSorted 屬性設定為 TRUE，因為它不是來源輸出。 來源輸出的 SynchronousInputID 值是零。|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|"%1" 無法將 SortKeyPosition 屬性設定為非零，因為 "%2" 不是來源輸出。 輸出資料行 "colname" (ID) 無法將 SortKeyPosition 屬性設定為非零，因為它的輸出 "outputname" (ID) 不是來源輸出。|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|"%1" 的 ComparisonFlags 屬性無法設定為非零的值，因為 "%2" 不是來源輸出。 輸出資料行 "colname" (ID) 無法將 ComparisonFlags 屬性設定為非零，因為輸出 "outputname" (ID) 不是來源輸出。|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|"%1" 的比較旗標必須是零，因為其類型不是字串類型。 對字串類型資料行而言，ComparisonFlags 只能是非零。|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|"%1" 無法將 ComparisonFlags 屬性設定為非零，因為 SortKeyPosition 已設定為零。 只有當 SortKeyPosition 也是非零時，輸出資料行的 ComparisonFlags 才會是非零。|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|屬性是唯讀的。|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|%1 設定無效的資料類型值 (%2!ld!)。|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|"%1" 需要設定字碼頁，但傳遞的值是零。|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|"%1" 具有無效的長度。 長度必須介於 %2!ld! 至 %3!ld! 之間 。|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|"%1" 具有無效的小數位數。 小數位數必須介於 %2!ld! 至 %3!ld! 之間 。|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|"%1" 具有無效的有效位數。 有效位數必須介於 %2!ld! 至 %3!ld! 之間 。|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|"%1" 設定的長度、有效位數、小數位數或字碼頁是非零的值，但資料類型需要值為零。|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1 不允許設定輸出資料行資料類型屬性。|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|"%1" 包含無效的資料類型。 "%1" 是特殊的錯誤資料行，唯一有效的資料類型是 DT_I4。|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|元件未提供錯誤碼描述。|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|指定的錯誤碼與這個元件沒有關聯。|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|依據截斷配置設定，截斷造成資料列重新導向。|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|"%1" 無法讓歷程識別碼為 %2!d! 的資料行讀取/寫入， 因為這個資料行不允許此使用類型。 嘗試將輸入資料行的使用類型變更為 UT_READWRITE 類型，但這個元件不支援此類型。|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|%1 已禁止使用歷程識別碼為 %2!d! 的輸入資料行。|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1" 無法針對歷程識別碼為 %2!d! 的輸入資料行執行要求的變更。 要求失敗，錯誤碼為 0x%3!8.8X!。 嘗試設定輸入資料行的使用類型時，發生指定的錯誤。|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|嘗試在 "%1" 設定資料類型屬性失敗，錯誤碼為 0x%2!8.8X!。 嘗試設定輸出資料行的一個或多個資料類型屬性時發生錯誤。|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|無法擷取 "%1" 的中繼資料。 請確定物件名稱正確且物件存在。|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|輸出資料行無法對應到外部中繼資料行。|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|變數 %1 必須是 "%2" 類型。|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1 不允許設定外部中繼資料行資料類型屬性。|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|識別碼 %1!lu! 不是輸入識別碼，也不是輸出識別碼。 指定的識別碼必須是外部中繼資料集合相關的輸入識別碼或輸出識別碼。|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|"%1" 上的外部中繼資料集合標示為未使用，所以無法執行任何作業。|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1 是同步輸出，且無法擷取同步輸出的緩衝區類型。|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|輸入資料行 "%1" 必須是唯讀的。 輸入資料行具有非唯讀的使用類型，這種情形是不允許的。|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|"%1" 遺漏必要的屬性 "%2"。 物件必須具有指定的自訂屬性。|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|輸出 %1 不能有屬性 "%2"，但目前已指派此屬性。|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1 必須在排除群組 %2!d! 中， 所有輸出都必須在指定的排除群組中。|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|屬性 "%1" 是空的。 此屬性不可以是空的。|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|無法配置運算式 "%1" 的記憶體。 當建立存放運算式的內部物件時，發生記憶體不足的錯誤。|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|無法剖析運算式 "%1"。 運算式無效，或發生記憶體不足的錯誤。|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|計算運算式 "%1" 失敗，錯誤碼為 0x%2!8.8X!。 運算式可能發生剖析時無法偵測到的錯誤，例如除以零，或發生記憶體不足的錯誤。|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|無法為 Expression 物件配置記憶體。 當建立 Expression 物件指標的陣列時，發生記憶體不足的錯誤。|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|當建立運算式管理員 (Expression Manager) 時，%1 失敗，錯誤碼為 0x%2!8.8X! 。|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|運算式 "%1" 不是布林值。 運算式的結果類型必須是布林值。|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|在 "%2" 上的運算式 "%1" 無效。|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|資料行 "%1" (%2!d!) 無法對應到任何輸入檔資料行。 在檔案中找不到輸出資料行名稱或輸入資料行名稱。|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|嘗試在 %2 上設定運算式 "%1" 的結果資料行失敗，錯誤碼為 0x%3!8.8X!。 無法決定接收運算式結果的輸入或輸出資料行，或運算式結果無法轉換成資料行類型。|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|%1 無法從封裝取得地區設定識別碼。|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|參數對應字串不是正確格式。|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|SQL 命令需要 %1!d! 個參數， 但參數對應只有 %2!d! 個參數 參數。|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|SQL 命令需要名稱為 "%1" 的參數，但在參數對應中找不到此參數。|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|一個以上的資料來源資料行具有名稱 "%1"。  資料來源資料行名稱必須是唯一的。|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|發現沒有名稱的資料來源資料行。  每個資料來源資料行都必須具有名稱。|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|元件與配置中斷連接。|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|配置元件的識別碼無效。|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|元件的輸入數目無效。|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|元件的輸出數目無效。|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|元件沒有任何輸入或輸出。|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|記憶體不足，無法配置這個元件操作的資料行清單。|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|輸出資料行 "%1" (%2!d!) 參考歷程識別碼為 %3!d! 的輸入資料行，但找不到具有此歷程識別碼的輸入。|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|至少一個輸入資料行必須標示為排序索引鍵，但找不到任何索引鍵。|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|資料行 "%1" (%2!d!) 和資料行 "%3" (%4!d!) 同時標示為排序索引鍵加權 %5!d!。|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|在修正驗證問題之前，元件無法執行要求的中繼資料變更。|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|輸入無法加入輸入集合中。|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|輸出無法加入輸出集合中。|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|無法從輸入集合刪除輸入。|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|無法從輸出集合移除輸出。|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|無法變更資料行的使用類型。|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|%1 必須可讀取/寫入，才能有自訂屬性 "%2"。 輸入或輸出資料行具有指定的自訂屬性，但無法讀取/寫入。 請移除屬性，或將資料行設定為可讀取/寫入。|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1 可讀取/寫入，且需要有自訂屬性 (Property) "%2"。 請加入此屬性 (Property)，或從資料行移除讀取/寫入屬性 (Attribute)。|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|無法刪除資料行。 元件不允許從這個輸入或輸出刪除資料行。|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|元件不允許將資料行加入這個輸入或輸出中。|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|找不到連接 "%1"。 請確認連接管理員包含此名稱的連接。|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|找不到識別碼為 "%1" 的執行階段連接管理員。 請確認連接管理員集合包含此識別碼的連接管理員。|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS 錯誤碼 DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER。  對 "%1" 連接管理員呼叫 AcquireConnection 方法失敗，錯誤碼為 0x%2!8.8X!。  在此之前可能已公佈過錯誤訊息，說明 AcquireConnection 方法呼叫為何失敗的詳細資訊。|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|從連接管理員 "%1" 取得的連接無效。|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|連接管理員 "%1" 不是正確類型。  必要的類型是 "%2"。 元件可用的類型是 "%3"。|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|無法從執行階段連接管理員取得 Managed 連接。|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|無法建立輸入來初始化輸入集合。|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|無法建立輸出來初始化輸出集合。|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|寫入檔案 "%1" 失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|連接管理員 "%1" 從 AcquireConnection 方法傳回類型不正確的物件。|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|輸入資料行 "%1" (%2!d!) 上需要 "%3" 屬性，但找不到此屬性。 應該加入遺漏的屬性。|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|"%1" 標示為唯讀，但未被其他任何資料行參考。 不允許未參考的資料行。|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|"%1" 參考資料行識別碼 %2!d!，但在輸入上找不到此資料行。 參考指向不存在的資料行。|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|"%1" 參考 "%2"，但此資料行不是 BLOB 類型。|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1" 參考輸出資料行識別碼 %2!d!，但在輸出上找不到該資料行。|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|讀取檔案 "%1" 失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|在緩時變維度轉換的輸入上，至少必須有一個固定、變更或歷程記錄類型的資料行。 請確認至少有一個資料行是 FixedAttribute、ChangingAttribute 或 HistoricalAttribute。|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|"%1" 的 ColumnType 屬性無效。 目前的值超出可接受的值範圍。|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|輸入資料行 "%1" 無法對應到外部資料行 "%2"，因為資料類型不同。 除了 DT_STR 和 DT_WSTR 之外，緩時變維度轉換不允許在不同類型的資料行之間對應。|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|"%1" 的資料類型是 DT_NTEXT，但 ANSI 檔案不支援。 請改用 DT_TEXT，並使用資料轉換元件將資料轉換成 DT_NTEXT。|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|"%1" 的資料類型是 DT_TEXT，但 Unicode 檔案不支援。 請改用 DT_NTEXT，並使用資料轉換元件將資料轉換成 DT_TEXT。|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|"%1" 的資料類型是 DT_IMAGE，但不受支援。 請改用 DT_TEXT 或 DT_NTEXT，並使用資料轉換元件在 DT_IMAGE 上轉換資料。|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|一般檔案連接管理員不支援格式 "%1"。 支援的格式為 Delimited、FixedWidth、RaggedRight 和 Mixed。|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|"%1" 應該包含檔案名稱，但不是 String 類型。|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|衝突的屬性設定造成錯誤。 "%1" 將 AllowAppend 屬性和 ForceTruncate 屬性同時設定為 TRUE， 這兩個屬性不能同時設定為 TRUE。 請將兩個屬性的其中一個設定為 FALSE。|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 參考資料行識別碼 %2!d!，但 %3 已經參考此資料行。 請從資料行的兩個參考移除其中一個。|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|連接管理員尚未指派給 %1。|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 參考識別碼為 %2!d! 的輸出資料行，但 %3 已經參考此資料行。|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|沒有任何輸入資料行參考 "%1"。 每一個輸出資料行必須只由一個輸入資料行參考。|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|"%1" 參考 "%2"，但此資料行不是正確類型。 必須是 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 參考指向的資料行必須是 BLOB 類型。|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|"%1" 應該包含檔案名稱，但不是 String 類型。|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|"%1" 將 %2 的 ExpectBOM 屬性設定為 TRUE，但是資料行並非 NT_NTEXT。 ExpectBOM 指定匯入資料行轉換必須有位元組順序標記 (BOM)。 請將 ExpectBOM 屬性設定為 False，或將輸出資料行資料類型變更為 DT_NTEXT。|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|資料輸出資料行必須是 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 資料輸出資料行只能設定為 BLOB 類型。|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|如果 FailOnFixedAttributeChange 屬性 (Property) 設定為 TRUE，當偵測到固定屬性 (Attribute) 變更時，轉換將失敗。 如果要將資料列傳送到固定屬性 (Attribute) 輸出，請將 FailOnFixedAttributeChange 屬性 (Property) 設定為 FALSE。|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|查閱轉換無法擷取任何資料列。 當 FailOnLookupFailure 設定為 TRUE 時，轉換會失敗，不會擷取任何資料列。|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|在緩時變維度轉換的輸入上，至少必須有一個 Key 類型的資料行。 請至少將一個資料行類型設定為 Key。|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|找不到名稱為 "%1" 的外部資料行。|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|推斷的指標資料行 "%1" 必須是 DT_BOOL 類型。|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|%1 必須將錯誤資料列配置值設定為 RD_NotUsed。|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|%1 必須將截斷資料列配置值設定為 RD_NotUsed。|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|找不到歷程識別碼為 %1!d! 的輸入資料行， 識別碼為 %2!d! 的輸出資料行需要此輸入資料行。|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|對輸出資料行識別碼 %1!d! 上指定的彙總類型而言，輸出資料類型無效。|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|對 %2 上指定彙總使用的 %1 而言，輸入資料類型無效。|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|輸入資料行歷程識別碼 %1!d! 和輸出資料行識別碼 %2!d! 的 資料類型不符 。|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|無法取得輸入識別碼 %1!d! 的輸入緩衝區控制代碼。|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|無法取得輸出識別碼 %1!d! 的輸出緩衝區控制代碼。|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|在輸入緩衝區中，找不到歷程識別碼為 %1!d! 的資料行 。|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|在輸入緩衝區中，找不到歷程識別碼為 %1!d! 的資料行 。|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|%1 的輸出資料行數目不可以是零。|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|一般檔案連接管理員中的資料行數目，必須與一般檔案配接器中的資料行數目相同。 一般檔案連接管理員的資料行數目是 %1!d!，一般檔案配接器的資料行數目是 %2!d!。|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|在一般檔案配接器的資料行集合中的索引 %3!d! 上， 找不到一般檔案連接管理員中索引 %2!d! 上的資料行 "%1" 。|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|識別碼為 %1!d! 的外部中繼資料行 已經對應到 %2。|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|轉換發現超過 %1!u! 個字元的索引鍵資料行 字元。|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|轉換發現超過 %1!u! 位元組的結果值 。|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|無法配置記憶體。|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|無法配置記憶體。|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|無法配置記憶體。|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|無法配置記憶體。|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|無法配置記憶體。|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|無法配置記憶體。|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|無法配置記憶體。|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|無法配置記憶體。|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|未參考輸入資料行 "%1"。|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|排序轉換無法建立包含 %1!d! 個執行緒的執行緒集區 。 記憶體不足。|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|排序轉換無法將工作項目排到其執行緒集區的佇列中。 記憶體不足。|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|在排序轉換中，工作者執行緒停止，錯誤碼為 0x%1!8.8X!。 排序緩衝區時遇到重大錯誤。|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads 是 %1!ld!，必須介於 1 到 %2!ld! (含) 之間，或 -1 表示預設為 CPU 數目。|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|無法從 XML 載入。|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|無法儲存到 XML。|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|無法將值 "%1" 轉換成整數。|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|無法將值 "%1" 轉換成布林值。|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|接近識別碼為 %1!d! 的物件發現載入錯誤。|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|值 "%1" 對屬性 "%2" 而言無效。|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|值 "%1" 對屬性 "%2" 而言無效。|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|值 "%1" 對屬性 "%2" 而言無效。|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|%1 未對應到輸出資料行。|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|%1 具有無效的對應。  識別碼為 %2!ld! 的輸出資料行不存在於 這個元件上。|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|%1 對應到輸出資料行，但此資料行已具有這個輸入的對應。|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|因為錯誤 0x%2!8.8X!，無法將歷程識別碼為 %1!ld! 的輸入資料行轉換成 DT_WSTR 。|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|在封裝中找不到識別碼為 %1!d! 的參考物件 。|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|無法讀取 pipelinexml 模組所需的持續性屬性。 管線未提供此屬性。|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|值 "%1" 對屬性 "%2" 而言無效。|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|無法擷取自訂屬性 "%1"。|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|在輸入資料行集合中，找不到歷程識別碼為 %1!d! 的輸入資料行，此歷程識別碼是在 ParameterMap 自訂屬性中參考，其參數位於位置號碼 %2!d!。|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|找不到參考資料行 "%1"。|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 和參考資料行 "%2" 具有不相容的資料類型。|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|參數化 SQL 陳述式產生的中繼資料不符合主要 SQL 陳述式。|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|參數化 SQL 陳述式包含不正確的參數數目。 必須是 %1!d! 個，但找到 %2!d! 個。|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 具有無法聯結的資料類型。|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 具有無法複製的資料類型。|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|%1 具有不支援的資料類型。 必須是 DT_STR 或 DT_WSTR。|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|%1 具有不支援的資料類型。 必須是 DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT 或 DT_IMAGE。|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|%1 具有不支援的資料類型。 必須是 DT_STR、DT_WSTR、DT_TEXT 或 DT_NTEXT。|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|排序轉換無法建立事件，以便和工作者執行緒通訊。 系統處理不足，無法執行排序轉換。|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|排序轉換無法建立工作者執行緒。 記憶體不足，無法執行排序轉換。|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|排序轉換無法比較緩衝區識別碼 %2!d! 中的資料列 %1!d!  和緩衝區識別碼 %4!d! 中的資料列  %3!d! 。|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|查閱轉換參考中繼資料包含太少資料行。 請檢查 SQLCommand 屬性。 SELECT 陳述式至少必須傳回一個資料行。|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|無法為 ColumnInfo 結構陣列配置記憶體。|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|無法為 ColumnPair 結構陣列配置記憶體。|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|無法配置 BUFFCOL 結構陣列的記憶體來建立主要工作空間。|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|無法建立主要工作空間緩衝區。|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|無法為雜湊表配置記憶體。|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|無法配置記憶體來建立雜湊節點的堆積。|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|無法為雜湊節點堆積配置記憶體。|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|無法建立 LRU 節點的堆積。 發生記憶體不足的狀況。|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|無法為 LRU 節點堆積配置記憶體。 發生記憶體不足的狀況。|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|載入資料行中繼資料時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|提取資料列集時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|擴展內部快取時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|繫結參數時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|建立繫結時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|在執行階段期間，Switch 陳述式遇到無效的大小寫。|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|無法為主要工作空間緩衝區的新資料列配置記憶體。 發生記憶體不足的狀況。|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|提取參數化資料列集時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|提取參數化資料列時發生 OLE DB 錯誤。 請檢查 SQLCommand 和 SqlCommandParam 屬性。|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|無法為主要工作空間緩衝區的新資料列配置記憶體。 發生記憶體不足的狀況。|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|無法建立主要工作空間緩衝區。|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|無法為雜湊表配置記憶體。|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|無法配置記憶體來建立雜湊節點的堆積。|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|無法為雜湊節點堆積配置記憶體。|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|無法配置記憶體來建立 CountDistinct 節點的堆積。|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|無法為 CountDistinct 節點堆積配置記憶體。|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|無法配置記憶體來建立 CountDistinct 鏈結的堆積。|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|無法為 CountDistinct 雜湊表配置記憶體。|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|無法為 CountDistinct 工作空間緩衝區的新資料列配置記憶體。|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|無法建立 CountDistinct 工作空間緩衝區。|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|無法為 CountDistinct 摺疊陣列配置記憶體。|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|無法為 CountDistinct 鏈結配置記憶體。|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|歷程識別碼為 %1!d!  與 %2!d! 的資料行 各有不相符的中繼資料。 輸入資料行 (對應到 Copymap 的輸出資料行) 沒有相同的中繼資料 (資料類型、有效位數、小數位數、長度或字碼頁)。|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|歷程識別碼為 "%1!d!" 的資料行 以不正確的形式對應到輸入資料行。 輸出資料行的 CopyColumnId 屬性不正確。|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|無法擷取資料行 "%1" 的 Long 資料。|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|從資料行擷取 Long 資料，但無法加入資料流程工作緩衝區中。|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|輸出 "%1" (%2!d!) 有輸出資料行，但多點傳送輸出未宣告資料行。 封裝已損毀。|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|無法載入當地語系化資源識別碼 %1!d!。 請確認 RLL 檔案存在。|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|無法取得 Events 介面。 無效 Events 介面已傳遞到資料流程模組來保存到 XML。|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|在 XML 載入期間設定路徑物件時發生錯誤。|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|在 XML 載入期間設定輸入物件時發生錯誤。|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|在 XML 載入期間設定輸出物件時發生錯誤。|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|在 XML 載入期間設定輸入資料行物件時發生錯誤。|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|在 XML 載入期間設定輸出資料行物件時發生錯誤。|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|在 XML 載入期間設定屬性物件時發生錯誤。|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|在 XML 載入期間設定連接物件時發生錯誤。|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|特殊轉換的特定資料行遺漏或類型不正確。|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|模糊群組轉換無法建立必要的資料表和存取子。|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|模糊群組轉換無法複製輸入。|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|模糊群組轉換無法產生群組。|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|套用屬性 '%1' 的設定時，模糊群組發生意外的錯誤。|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|在標準化資料時，模糊群組轉換無法挑選要使用的標準資料列。|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|模糊群組不支援類型 IMAGE、TEXT 或 NTEXT 的輸入資料行。|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|在資料類型不是 DT_STR 或 DT_WSTR 的資料行 "%1" (%2!d!) 上指定模糊相符。|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|模糊群組轉換管線發生錯誤，傳回錯誤碼 0x%1!8.8X!: "%2"。|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|輸出資料行 "%2" (%3!d!) 指定的字碼頁 %1!d! 無效 。  您必須先將此資料行轉換為 DT_WSTR，方法是在此資料行之前插入資料轉換。|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|設定緩衝區驅動輸出 "%1" (%2!d!) 的資料結尾旗標時失敗。|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|無法複製輸入緩衝區。 發生記憶體不足的狀況或內部錯誤。|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|資料行 "%1" 要求同時產生片假名和平假名字元。|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|資料行 "%1" 要求同時產生簡體中文和繁體中文字元。|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|資料行 "%1" 要求作業同時產生全形和半形字元。|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|資料行 "%1" 結合日文字元的作業和中文字元的作業。|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|資料行 "%1" 結合中文字元的作業和大小寫作業。|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|資料行 "%1" 結合日文字元的作業和大小寫作業。|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|資料行 "%1" 將資料行同時對應到大寫和小寫。|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|資料行 "%1" 結合大小寫以外的旗標和語言大小寫作業。|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|無法依指定來對應資料行 "%1" 的資料類型。|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|不支援已存在的比對索引 "%2" 的版本 (%1)。 需要的版本是 "%3"。 如果索引中繼資料保存的版本不符合用來建立目前程式碼的版本，就會發生這個錯誤。 請使用目前程式碼版本重建索引，修正錯誤。|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|資料表 "%1" 似乎不是有效的預先建立比對索引。 當無法從指定的預先建立索引載入中繼資料記錄時，就會發生這個錯誤。|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|無法讀取指定的預先建立比對索引 "%1"。  OLEDB 錯誤碼: 0x%2!8.8X!。|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|沒有具有參考資料表資料行之有效聯結的輸入資料行。  請確定至少有一個聯結是使用輸入資料行屬性 JoinToReferenceColumn 和 JoinType 所定義。|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|指定已存在的比對索引 "%1" 最初不是以資料行 "%2" 的模糊相符資訊建立。  必須重建來包含這項資訊。 當用來建立索引的資料行不是模糊聯結資料行時，就會發生這個錯誤。|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|提供給屬性 "%2" 的名稱 "%1" 不是有效的 SQL 識別碼名稱。 如果屬性的名稱不符合有效 SQL 識別碼名稱的規格時，就會發生這個錯誤。|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|模糊查閱轉換的 MinSimilarity 臨界值屬性必須是大於或等於 0.0 但小於 1.0 的值。|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|屬性 "%2" 的值 "%1" 無效。|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|在輸入資料行 "%1" 和參考資料行 "%2" 之間指定的模糊查閱無效，因為只有在類型 DT_STR 和 DT_WSTR 的字串資料行之間，才支援模糊聯結。|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|完全查閱資料行 "%1" 和 "%2" 沒有相等的資料類型，或兩者是無法比較的字串類型。 在具有相等資料類型或 DT_STR 和 DT_WSTR 組合的資料行之間，支援完全聯結。|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|複製資料行 "%1" 和 "%2" 沒有相等的資料類型，或兩者不是可完整轉換的字串類型。 如果在具有相等資料類型或 DT_STR 和 DT_WSTR 組合的資料行之間，支援從參考複製到輸出，但不支援其他類型，就會發生這個問題。|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|通過資料行 "%1" 和 "%2" 沒有相等的資料類型。 只有相等資料類型的資料行，才支援做為輸入到輸出之間的通過資料行。|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|找不到參考資料行 "%1"。|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|輸出資料行必須只指定一個 CopyColumn 或 PassThruColumn 屬性。 當 CopyColumn 和 PassThruColumn 屬性同時設定或同時不設定為非空白值時，就會發生這個錯誤。|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|在輸入資料行集合中， 找不到對輸出資料行 '%3' 的屬性 '%2' 所指定的來源歷程識別碼 '%1!d!'。 在輸入集內找不到輸出資料行上指定為通過資料行的輸入資料行識別碼時，就會發生這個問題。|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|在參考資料表/查詢中，找不到在預先建立之索引 "%2" 中的資料行 "%1"。 在預先存在的比對索引建立之後，如果參考資料表的結構描述/查詢已變更，就會發生這個問題。|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|元件遇到大於 2147483647 個字元的 Token。|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|無法附加輸出檔。 資料行 "%1" 的名稱相符，但是檔案中的資料行類型為 %2，而輸入資料行的類型為 %3。 資料行中繼資料的資料類型不符。|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|無法附加輸出檔。 資料行 "%1" 是依名稱比對，但檔案中的資料行最大長度是 %2!d!，而輸入資料行的最大長度則是 %3!d! 。 資料行的中繼資料長度不相符。|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|無法附加輸出檔。 資料行 "%1" 依名稱比對，但檔案中的資料行具有字碼頁 %2!d!， 輸入資料行具有字碼頁 %3!d!。 具名資料行中繼資料的字碼頁不符。|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|無法附加輸出檔。 資料行 "%1" 依名稱比對，但檔案中的資料行的有效位數是 %2!d!， 輸入資料行的有效位數是 %3!d!。 具名資料行中繼資料的有效位數不符。|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|無法附加輸出檔。 資料行 "%1" 依名稱比對，但檔案中的資料行的小數位數是 %2!d!， 輸入資料行的小數位數是 %3!d!。  具名資料行中繼資料的小數位數不符。|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|無法判斷 "%1" 上的 DBMS 名稱和版本。 如果在連接上的 IDBProperties 未傳回驗證 DBMS 名稱和版本所需的資訊，就會發生這個問題。|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|不支援 "%1" 的 DBMS 類型或版本。  需要與 Microsoft SQL Server 8.0 版或更新版本之間的連接。 如果在連接上的 IDBProperties 未傳回正確的版本，就會發生這個問題。|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1 是特殊錯誤輸出資料行，不能刪除。|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|對資料行 "%1" 指定的資料類型不是預期的類型 "%2"。|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|在輸入資料行集合中，找不到輸入資料行歷程識別碼 "%1"，此歷程識別碼是由輸出資料行 "%3" 上的屬性 "%2" 所參照。|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|由輸出資料行 "%3" 上的 "%2" 屬性所參考的輸入資料行 "%1" 必須有屬性 ToBeCleaned=True，而且有一個有效 ExactFuzzy 屬性值。|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|參考資料表 '%1' 在整數識別欄位上沒有叢集索引，但如果屬性 'CopyRefTable' 設定為 FALSE，則需要這個索引。 如果 CopyRefTable 是 false，則參考資料表在整數識別欄位上必須有叢集索引。|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|參考資料表 '%1' 包含非整數類型的識別欄位，但並不支援。 請使用資料表的檢視，且檢視不包含資料行 '%2'。  當建立參考資料表的副本時，因為會加入整數識別欄位，但每個資料表僅允許一個識別欄位，所以會發生這個錯誤。|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|不能同時指定 MatchContribution 和階層資訊。 這是不允許的，因為這兩個屬性都是計分加權因數。|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|階層的層級必須是唯一的數字。 階層值的有效層級是大於或等於 1 的整數。 數字愈小，資料行在階層中的位置愈低。 預設值是 0，表示資料行不是階層的一部分。 不允許重疊和間隔。|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|未定義要進行模糊群組的資料行。  至少必須要有一個輸入資料行的資料行屬性為 ToBeCleaned=true 和 ExactFuzzy=2。|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|識別碼為 '%1!d!' 的資料行 無效，原因不明。|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|不支援資料行 '%1' 的資料類型。|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|輸出資料行 '%1' 的長度小於來源資料行 '%2' 的長度。|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|只能有一個輸入資料行。|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|只能有兩個輸出資料行。|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|輸入資料行只能使用 DT_WSTR 或 DT_NTEXT 做為資料類型。|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|輸出資料行 [%1!d!] 只能使用 '%2' 做為資料類型。|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|參考資料行只能以 DT_STR 或 DT_WSTR 做為其資料類型。|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|尋找參考資料行 '%1' 時發生錯誤。|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|轉換的詞彙類型只能是 WordOnly、PhraseOnly 或 WordPhrase。|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|頻率臨界值不應該低於 '%1!d!'。|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|詞彙最大長度的值不應該低於 '%1!d!'。|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|詞彙擷取參考中繼資料包含太多資料行。|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|配置記憶體時發生錯誤。|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|建立工作空間緩衝區時發生錯誤。|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|建立繫結時發生 OLEDB 錯誤。|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|提取資料列集時發生 OLEDB 錯誤。|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|擴展內部快取時發生 OLEDB 錯誤。|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|在資料列 %1!ld! 資料行 %2!ld! 上擷取詞彙時發生錯誤。 傳回的錯誤碼是 0x%3!8.8X!。 解決方法是從輸入將它移除。|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|候選詞彙數目超出限制 4G。|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|用於排除詞彙的參考資料表、檢視表或資料行無效。|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|字串資料行 '%1' 的長度超過 4000 個字元。  必須從 DT_STR 轉換為 DT_WSTR，所以會發生截斷。  請減少資料行寬度，或僅使用 DT_WSTR 資料行類型。|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|尚未設定用於排除詞彙的參考資料表、檢視表或資料行。|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|詞彙查閱包含太少輸出資料行。|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|參考資料行只能以 DT_STR 或 DT_WSTR 做為其資料類型。|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|尋找參考資料行 '%1' 時發生錯誤。|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|詞彙查閱參考中繼資料包含太少資料行。|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|正規化文字時發生錯誤。|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|建立工作空間緩衝區時發生錯誤。|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|建立繫結時發生 OLEDB 錯誤。|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|提取資料列集時發生 OLEDB 錯誤。|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|擴展內部快取時發生 OLEDB 錯誤。|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|在資料列 %1!ld! 資料行 %2!ld! 上查閱詞彙時發生錯誤。 傳回的錯誤碼是 0x%3!8.8X!。 解決方法是從輸入將它移除。|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|至少一個通過資料行未對應到輸出資料行。|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|只能有一個輸入資料行對應到一個參考資料行。|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|對應到參考資料行的輸入資料行，只能使用 DT_NTXT 或 DT_WSTR 做為資料類型。|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|參考資料表名稱 "%1" 不是有效的 SQL 識別碼。 當無法從輸入字串中剖析資料表名稱時，就會發生這個錯誤。 名稱可能有不具引號的空格。 請確認名稱已正確加上引號。|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|詞彙篩選開始反覆運算時發生錯誤。|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|回收用於快取詞彙的緩衝區時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|STL 容器發生 std::length_error。|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|儲存含有標點符號的文字時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|處理第 %1!ld! 個參考詞彙時發生錯誤。 傳回的錯誤碼是 0x%2!8.8X!。 解決方法是從參考資料表移除參考詞彙。|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|排序參考詞彙時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|計算候選詞彙時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|模糊查閱無法依 Exhaustive 屬性啟用時的要求，將整個參考資料表載入主記憶體。  系統記憶體不足，或者為 MaxMemoryUsage 指定的上限不足以載入參考資料表。  請將 MaxMemoryUsage 設定為 0 或大幅增加它。  或者停用 Exhaustive。|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|初始化詞彙查閱的引擎時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|處理句子時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|將字串加入至內部緩衝區時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|從內部緩衝區儲存 part-of-speech 標記時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|計算候選詞彙時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|初始化 part-of-speech 處理器時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|載入有限狀態 Automation 時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|初始化詞彙擷取的引擎時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|在句子內處理時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|初始化 part-of-speech 處理器時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|將字串加入至內部緩衝區時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|將文字加入統計解碼器時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|句子解碼時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|設定排除詞彙時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|處理輸入的文件時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|測試點是否為縮寫字的一部分時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|設定參考詞彙時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|處理輸入的文件時發生錯誤。 傳回的錯誤碼是 0x%1!8.8X!。|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|屬性 %1 的值是 %2!d!，這是不允許的。  值必須大於或等於 %3!d!。|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|屬性 %1 的值是 %2!d!，必須小於或等於屬性 %4 的值 %3!d! 。|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|嘗試刪除現有的模糊相符索引 "%1" 時遇到錯誤。 可能是這個資料表並非以模糊查閱 (或這個模糊查閱版本) 建立、已損毀或有其他問題。 請嘗試手動刪除資料表 "%2" 或指定不同名稱給 MatchIndexName 屬性。|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|轉換的分數類型只能是頻率或 TFIDF。|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|指定的參考資料表有太多資料列。 模糊查閱僅適用於資料列數少於 10 億的參考資料表。 請考慮使用參考資料表較小的檢視表。|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|無法判斷參考資料表 '%1' 的大小。  可能是這個物件是檢視表而不是資料表。  當 CopyReferentaceTable=false 時，模糊查閱不支援檢視。  請確定資料表存在且 CopyReferenceTable=true。|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|%3 不支援在 %2 上的 SSIS 資料流程工作資料類型 "%1"。|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|在識別碼為 %2!d! 的輸出上，無法為識別碼為 %1!d! 的輸出資料行設定資料類型屬性 。 找不到輸出或資料行。|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|在 %2 上，無法變更自訂屬性 "%1" 的值。|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|非錯誤輸出上的 %1 在錯誤輸出上沒有對應的輸出資料行。|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|錯誤輸出上的 %1 在非錯誤輸出上沒有對應的輸出資料行。|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|錯誤輸出上的 %1 的屬性，與對應的資料來源資料行的屬性不符。|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|無法變更 %1 上輸出資料行的資料類型 (DT_WSTR 和 DT_NTEXT 資料行除外)。|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|"%1" 的資料類型與來源資料行 "%3" 的資料類型 "%2" 不符。|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|%1 在結構描述中沒有相符的來源資料行。|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|用於參考詞彙的參考資料表/檢視表或資料行無效。|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|尚未設定用於參考詞彙的參考資料表/檢視表或資料行。|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|%1 對應至識別碼為 %2!ld! 的外部中繼資料行，該資料行已經對應至其他資料行。|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|為屬性 '%2' 指定的 SQL 物件名稱 '%1' 包含的前置詞數目大於最大數。  最大值為 2。|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|值太大，無法納入資料行。|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|SSIS IDataReader 已經關閉。|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|SSIS IDataReader 超過結果集的結尾。|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|資料行的序數位置無效。|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|無法將 %1 從資料類型 "%2" 轉換為資料類型 "%3"。|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|%1 具有不支援的字碼頁 %2!d!。|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|%1 對於 XML 結構描述沒有對應。|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|歷程識別碼為 %1!d!  與 %2!d! 的資料行 各有不相符的中繼資料。 對應至輸出資料行的輸入資料行沒有相同的中繼資料 (資料類型、有效位數、小數位數、長度或字碼頁)。|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|SSIS IDataReader 已經關閉。 讀取逾時值已過期。|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|執行提供的 SQL 命令時發生錯誤: "%1"。 %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|為輸入資料行 '%1' 指定的 JoinType 屬性與起初建立相符索引時，為對應參考資料表資料行所指定的 JoinType 不同。  請使用給定的 JoinType 重建相符索引，或變更 JoinType 以符合建立相符索引時所使用的類型。|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|%3 不支援在資料行 "%2" 找到的 "%1" 資料類型。|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|%3 不支援在 %2 上找到的 "%1" 資料類型。|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|%2 不支援 %1 資料類型。|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|無法在移轉 %2 時加入專案參考 "%1"。 移轉可能必須以手動方式完成。|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|在 %2 移轉期間找到多個名為 "%1" 的進入點。 移轉可能必須以手動方式完成。|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|在 %1 移轉期間未找到任何進入點。 移轉可能必須以手動方式完成。|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|插入資料時發生例外狀況，從提供者傳回的訊息為: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|無法從 %1 擷取提供者的不變名稱，它目前並不受 ADO NET 目的地元件支援|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|資料提供者嘗試將資料插入至目的地時發生引數例外狀況。 傳回的訊息為: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|BatchSize 屬性必須為非負整數|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|將這個資料列傳送到目的地資料來源時發生錯誤。|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|執行 TSQL 命令發生例外狀況，訊息為: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|%3 不支援在資料行 "%2" 找到的 "%1" 資料類型。|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET 目的地無法取得 %1 連接。 這個連接可能已損毀。|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|指定的連接 %1 未受管理，請對 ADO NET 目的地使用 Managed 連接。|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|目的地元件沒有錯誤輸出。 它可能已損毀。|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|與外部資料行 %2 相關聯的 lineageID %1 不存在於執行階段。|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|資料庫中沒有 %1。 它可能已被移除或重新命名。|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|無法取得外部資料行的屬性。 您所輸入的資料表名稱可能不存在，或在資料表物件上沒有 SELECT 權限，因此透過連接取得資料行屬性的替代嘗試已失敗。 詳細的錯誤訊息為: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|ADO NET 目的地元件不支援輸入資料行錯誤配置。|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|ADO NET 目的地元件不支援輸入資料行截斷配置。|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|ADO NET 目的地元件不支援輸入截斷資料列配置。|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|不可有資料表或檢視表名稱。 \n\t 如果您是引用資料表名稱，請使用所選資料提供者的資料表前置詞 %1 與後置詞 %2 來進行引用。 \n\t 如果您是使用多部分名稱，請對資料表名稱最多使用三部分名稱。|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|在緩衝區中找不到歷程識別碼為 %2!d! 的資料行 "%1" 。 緩衝區管理員傳回錯誤碼 0x%3!8.8X!。|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|無法從緩衝區取得資料行 "%1" (%2!d!) 的資訊。 傳回的錯誤碼是 0x%3!8.8X!。|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|彙總 "%1" 時發現算術溢位。|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|無法從緩衝區取得資料列 "%1!ld!" 資料行 "%2!ld!" 的資訊 。 傳回的錯誤碼是 0x%3!8.8X!。|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|無法在緩衝區設定資料列 %1!ld! 資料行 %2!ld! 的資訊 。 傳回的錯誤碼是 0x%3!8.8X!。|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|無法使用必要的緩衝區。|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|嘗試取得緩衝區界限資訊失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|設定緩衝區的資料列集結尾失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|無法取得錯誤輸出緩衝區的資料。|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|從緩衝區移除資料列失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|嘗試設定緩衝區錯誤資訊失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|%2 上的 %1 發生錯誤。 傳回的資料行狀態是: "%3"。|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|無法快取參考中繼資料。|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|查閱期間產生的資料列不符。|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|%1 包含無效的錯誤或截斷資料列配置。|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|將資料列導向錯誤輸出失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|準備資料行狀態進行插入失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|在資料流程工作緩衝區中，嘗試尋找歷程識別碼為 %2!d! 的 %1 失敗， 錯誤碼為 0x%3!8.8X!。|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|在 %1 中找不到任何非特殊的錯誤資料行。|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS 錯誤碼 DTS_E_INDUCEDTRANSFORMFAILUREONERROR。  因為發生錯誤碼 0x%2!8.8X! 的錯誤， 且 %3" 的錯誤資料列配置指定在錯誤時失敗，所以 "%1" 失敗。 所指定元件上的指定物件發生錯誤。  在此之前可能已公佈過錯誤訊息，說明有關此失敗的詳細資訊。|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|因為發生截斷，且 "%2" 的截斷資料列配置指定在截斷時失敗，所以 "%1" 失敗。 指定之元件上的指定物件發生截斷錯誤。|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|"%2" 上的運算式 "%1" 已評估為 NULL，但 "%3" 需要布林值結果。 請修改輸出上的錯誤資料列配置，將這個結果視為 False (忽略失敗)，或將這個資料列重新導向錯誤輸出 (重新導向資料列)。  對條件式分割而言，運算式結果必須是布林值。  NULL 運算式結果是錯誤。|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|運算式已評估為 NULL，但需要布林結果。 請修改輸出上的錯誤資料列配置，將這個結果視為 False (忽略失敗)，或將這個資料列重新導向錯誤輸出 (重新導向資料列)。 對條件式分割而言，運算式結果必須是布林值。  NULL 運算式結果是錯誤。|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|不支援 UTF-16 Big Endian 的檔案格式。  僅支援 UTF-16 Little Endian 格式。|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|不支援 UTF-8 的檔案格式做為 Unicode。|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|無法讀取識別碼屬性。|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|快取索引資料行 %1 是由一個以上的查閱輸入資料行參考。|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|查閱並未參考所有快取連接管理員索引資料行。 查閱中的聯結的資料行數目: %1!d!。 索引資料行數目: %2!d!。|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|由於符號不符合或資料溢位以外的原因，而無法轉換資料值。|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|資料值違反了結構描述條件約束。|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|資料已遭截斷。|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|轉換失敗，因為資料值已簽署，而提供者所使用的類型未簽署。|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|轉換失敗，因為資料值造成提供者所使用的類型溢位。|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|沒有可用的狀態。|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|使用者沒有寫入資料行的正確權限。|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|資料值違反了資料行的完整性條件約束。|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|沒有可用的狀態。|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|由於符號不符合或資料溢位以外的原因，而無法轉換資料值。|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|資料已遭截斷。|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|轉換失敗，因為資料值已簽署，而提供者所使用的類型未簽署。|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|轉換失敗，因為資料值造成提供者所使用的類型溢位。|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|資料值違反了結構描述條件約束。|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|由於符號不符合或資料溢位以外的原因，而無法轉換資料值。|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|資料已遭截斷。|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|轉換失敗，因為資料值已簽署，而提供者所使用的類型未簽署。|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|轉換失敗，因為資料值造成提供者所使用的類型溢位。|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|沒有可用的狀態。|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|使用者沒有寫入資料行的正確權限。|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|資料值違反完整性條件約束。|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|由於符號不符合或資料溢位以外的原因，而無法轉換資料值。|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|資料已遭截斷。|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|轉換失敗，因為資料值已簽署，而提供者所使用的類型未簽署。|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|轉換失敗，因為資料值造成資料轉換使用的類型溢位。|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|沒有可用的狀態。|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|由於符號不符合或資料溢位以外的原因，而無法轉換資料值。|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|資料已遭截斷。|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|轉換失敗，因為資料值已簽署，但一般檔案來源配接器使用的類型未簽署。|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|轉換失敗，因為資料值造成一般檔案來源配接器使用的類型溢位。|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|沒有可用的狀態。|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|開啟檔案 "%1" 進行讀取失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|無法開啟檔案進行讀取。|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|開啟檔案 "%1" 進行寫入失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|無法開啟檔案進行寫入。|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|無法讀取檔案。|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|無法寫入檔案。|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|剖析類型陣列的屬性時，發現太多陣列元素。 elementCount 小於找到的陣列元素數目。|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|剖析類型陣列的屬性時，發現太少陣列元素。 elementCount 大於找到的陣列元素數目。|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|開啟檔案 "%1" 進行寫入失敗。 找不到檔案。|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|開啟檔案進行寫入失敗。 找不到檔案。|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|開啟檔案 "%1" 進行寫入失敗。 找不到路徑。|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|開啟檔案進行寫入失敗。 找不到路徑。|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|開啟檔案 "%1" 進行寫入失敗。 開啟太多檔案。|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|開啟檔案進行寫入失敗。 開啟太多檔案。|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|開啟檔案 "%1" 進行寫入失敗。 您沒有正確的權限。|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|開啟檔案進行寫入失敗。 您沒有正確的權限。|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|開啟檔案 "%1" 進行寫入失敗。 檔案已存在而無法覆寫。 如果 AllowAppend 屬性是 FALSE 且 ForceTruncate 屬性也設定為 FALSE，則檔案的存在就會造成這個失敗。|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|開啟檔案進行寫入時失敗。 檔案已存在而無法覆寫。 如果 AllowAppend 屬性和 ForceTruncate 屬性同時設定為 FALSE，則檔案的存在就會造成這個失敗。|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|%2 上的自訂屬性 "%1" 的值不正確。|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|資料行 "%1" 和 "%2" 具有不相容的中繼資料。|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|開啟檔案 "%1" 進行寫入失敗，因為磁碟已滿。 磁碟空間不足，無法儲存這個檔案。|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|嘗試開啟檔案進行寫入失敗，因為磁碟已滿。|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|產生排序索引鍵失敗，錯誤為 0x%1!8.8X!。 ComparisonFlags 已啟用，但使用 LCMapString 產生 sortkey 失敗。|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|轉換無法對應字串，傳回錯誤 0x%1!8.8X!。 LCMapString 失敗。|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|開啟檔案 "%1" 進行讀取失敗。 找不到檔案。|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|開啟檔案進行讀取失敗。 找不到檔案。|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|開啟檔案 "%1" 進行讀取失敗。 找不到路徑。|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|開啟檔案進行讀取失敗。 找不到路徑。|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|開啟檔案 "%1" 進行讀取失敗。 開啟太多檔案。|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|開啟檔案進行讀取失敗。 開啟太多檔案。|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|嘗試開啟檔案 "%1" 進行讀取失敗。 存取遭到拒絕。|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|開啟檔案進行讀取失敗。 您沒有正確的權限。|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|檔案 "%1" 的位元組順序標示 (BOM) 值是 0x%2!4.4X!，但預期的值是 0x%3!4.4X!。 已設定這個檔案的 ExpectBOM 屬性，但檔案中的 BOM 值遺漏或無效。|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|檔案的位元組順序標示 (BOM) 值無效。 已設定這個檔案的 ExpectBOM 屬性，但檔案中的 BOM 值遺漏或無效。|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1 未附加至元件。  必須附加至元件。|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|自訂屬性 %1 的值不正確。  必須是介於 %2!d! 至 %3!I64d! 之間的數字 。|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|對這個資料行選取的彙總類型而言，無法指定自訂屬性 "%1"。 只有對群組依據和相異計數的彙總類型，才能指定比較旗標自訂屬性。|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|只有對資料類型為 DT_STR 或 DT_WSTR 的資料行，才能指定比較旗標自訂屬性 "%1"。|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|%1 上的彙總失敗，錯誤碼為 0x%2!8.8X!。|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|設定對應時發生錯誤。 %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1 無法讀取 XML 資料。|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1 無法取得 "%2" 屬性指定的變數。|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1 包含值為 %2 的 RowsetID，但此值未參考結構描述中的資料表。|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|屬性 %1 必須是空的或介於 %2!u! 至 %3!u! 之間的數字 。 Keys 或 CountDistinctKeys 屬性包含無效的值。 屬性必須是介於 0 到 ULONG_MAX (含) 之間的數字，不然就不要設定。|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|彙總元件遇到太多相異索引鍵組合。 無法容納 %1!u! 個以上的 相異索引鍵值。 主要工作空間中有 ULONG_MAX 個以上的相異索引鍵值。|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|彙總元件在執行計算相異彙總時，發現太多相異值。 無法容納 %1!u! 個以上的 相異值。 執行計算相異彙總時，有 ULONG_MAX 個以上的相異值。|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|嘗試寫入檔名資料行失敗，錯誤碼為 0x%1!8.8X!。|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|發生錯誤，但無法決定造成錯誤的資料行。|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|無法將查閱中繼資料從版本 %1!d! 升級到 %2!d! 。 在呼叫 PerformUpgrade() 時，查閱轉換無法從現有版本號碼升級中繼資料。|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|找不到句子的結尾界限。|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|詞彙擷取轉換無法處理輸入文字，因為輸入文字的句子太長。 此句子已分割為數個句子。|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1 無法讀取 XML 資料。 %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|呼叫查閱轉換方法 ReinitializeMetadata 失敗。|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|查閱轉換至少必須包含一個已聯結參考資料行的輸入資料行，但未指定任何資料行。 您至少必須指定一個聯結資料行。|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|Managed 錯誤基礎結構公佈的訊息字串包含了格式不正確的規格。 此為內部錯誤。|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|使用 Managed 錯誤基礎結構來格式化訊息字串時，發現不支援格式化的變數類型。 此為內部錯誤。|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1 無法處理資料。 %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|%2 的屬性 "%1" 是空的。|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|嘗試針對路徑為 "%2" 的 XML 資料表，建立名稱為 "%1" 的輸出失敗，因為名稱無效。|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|值太大，無法納入 %1。|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1 無法處理資料。|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|"%1" 失敗，因為發生截斷，而且 "%2" 上的截斷資料列配置 (位於 "%3") 指定在截斷時失敗。 指定之元件上的指定物件發生截斷錯誤。|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|因為發生錯誤碼 0x%2!8.8X! 的錯誤， 且 %3" 的錯誤資料列配置 (位於 "%4") 指定在錯誤時失敗，所以 "%1" 失敗。 所指定元件上的指定物件發生錯誤。|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|SQLCE 目的地無法設定資料列的資料行值。|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|SQLCE 目的地無法插入資料列。|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|載入資料行中繼資料時遇到 OLEDB 錯誤。|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|查閱參考中繼資料包含的資料行太少。|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|載入資料行中繼資料時遇到 OLEDB 錯誤。|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|查閱參考中繼資料包含的資料行太少。|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|無法配置記憶體。|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|無法配置記憶體。|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|無法建立工作空間緩衝區。|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|無法具現化 XML DOM 文件，請確認 MSXML 二進位碼檔案已正確安裝及註冊。|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|無法將 XML 資料載入本機 DOM 中處理。|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|執行階段變數 "%1" 的類型不正確。 執行階段變數類型必須是 Object。|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|XML 來源配接器無法處理 XML 資料。 不支援多個內嵌結構描述。|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|XML 來源配接器無法處理 XML 資料。 元素的內容不能宣告為 anyType。|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|XML 來源配接器無法處理 XML 資料。 元素的內容不能包含對群組的參考 (ref)。|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|XML 來源配接器不支援複雜類型的混合內容模型。|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|XML 來源配接器無法處理 XML 資料。 內嵌結構描述必須是來源 XML 中的第一個子節點。|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|XML 來源配接器無法處理 XML 資料。 在來源 XML 中找不到內嵌結構描述，但是 "UseInlineSchema" 屬性設定為 True。|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|元件無法使用在 FastLoad 或大量插入的交易中會保留連接的連接管理員。|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|%1 無法設定為錯誤時使用交易中的連接來重新導向。|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|%1 沒有對應的輸入或輸出資料行。|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|未選取要寫入檔案的任何資料行。|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|%1 的資料類型無效。 資料類型為 DT_IMAGE、DT_TEXT 及 DT_NTEXT 的資料行不能寫入原始檔案。|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|這個元件使用外部中繼資料集合的方式不對。 元件應該在附加或截斷現有檔案時使用外部中繼資料。 否則，不需要外部中繼資料。|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|%1 對應至識別碼為 %2!d! 的外部中繼資料行。 選取的 [寫入選項] 值若是 [永遠建立]，輸入資料行就不應對應至外部中繼資料行。|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|無法開啟檔案讀取中繼資料。 如果檔案不存在，而且元件已經定義外部中繼資料，您可以將 "ValidateExternalMetadata" 屬性設定為 False，將會在執行階段建立檔案。|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|無法從資料流程緩衝區存取資料來源資料行 "%1" 的 LOB 資料，錯誤碼為 0x%2!8.8X!。|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1 無法處理 XML 資料。 %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|XML 來源配接器無法處理 XML 資料。|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|值 %1!d! 未辨識為有效的存取模式 。|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|無法取得資料來源資料行 "%1" 的完整中繼資料資訊。  請確定資料來源中已正確定義資料行。|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|只能變更 User Name 資料行、Package Name 資料行、Task Name 資料行和 Machine Name 資料行的長度。  所有其他稽核資料行資料類型的資訊都為唯讀。|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|OLE DB 提供者未傳回以 SQL 命令為基礎的資料列集。|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|認可失敗。|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|%2 上的自訂屬性 "%1" 只能與 ANSI 檔案一起使用。|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|%2 上的自訂屬性 "%1" 只能與 DT_BYTES 一起使用。|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS 錯誤碼 DTS_E_OLEDB_NOPROVIDER_ERROR。  要求的 OLE DB 提供者 %2 並未註冊。 錯誤碼：0x%1!8.8X!。|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS 錯誤碼 DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR。  要求的 OLE DB 提供者 %2 並未註冊 -- 可能是沒有 64 位元提供者可用。  錯誤碼：0x%1!8.8X!。|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|快取資料行 "%1" 對應到一個以上的資料行。 請移除重複的資料行對應。|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1 未對應到有效的快取資料行。|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|無法對應輸入資料行 "%1" 與快取資料行 "%2"，因為資料類型不符。|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|輸入資料行數目與快取資料行數目不符。|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|快取檔案名稱未提供或無效。 請提供有效的快取檔案名稱。|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|資料行 "%1" 的索引位置與快取連接管理員資料行 "%2" 的位置不同。|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|無法從檔案 "%1" 載入快取。|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|查閱輸入資料行 %1 會參考非索引快取資料行 %2。|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|無法取得連接字串。|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|無法對應輸入資料行 "%1" 與快取資料行 "%2"，因為一個或多個資料類型屬性不符。|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|在快取中找不到快取資料行 "%1"。|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|無法將 %1 對應至快取資料行。 hresult 為 0x%2!8.8X!。|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|%1 無法寫入快取，因為 %2 已經從檔案載入快取。|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|%1 無法從檔案 "%2" 載入快取，因為已經從檔案 "%3" 載入快取。|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|沒有任何元件使用彙總元件識別碼為 %1!d!  的輸出。 請將它移除，或將它與某個元件的輸入建立關聯。|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 無法將快取寫入檔案 "%2"。 hresult 為 0x%3!8.8X!。|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|元素 "%2" 上 "%1" 的 XML 結構描述資料類型資訊已變更。  請重新初始化這個元件的中繼資料，並檢閱資料行對應。|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 未用在聯結或複製中。 請從輸入資料行清單中移除未使用的資料行。|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|由於排序內送緩衝區時發生堆疊溢位，所以排序失敗。  請減少資料流程工作的 DefaultBufferMaxRows 屬性。|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|請考慮將連接字串中的 PROVIDER 變更為 %1，或造訪 http://www.microsoft.com/downloads 以便尋找並下載 %2 的支援。|  
|||DTS_E_INITTASKOBJECTFAILED|無法為工作 "%1!s!"、類型 "%2!s!" 初始化工作物件， 因為錯誤 0x%3!8.8X! "%4!s!"。|  
|||DTS_E_GETCATMANAGERFAILED|無法建立 COM 元件類別目錄管理員，因為錯誤 0x%1!8.8X! "%2!s!"。|  
|||DTS_E_COMPONENTINITFAILED|元件 %1!s! 無法初始化，因為錯誤 0x%2!8.8X! "%3!s!"。|  
  
##  <a name="msgWarning"></a> 警告訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 警告訊息的符號名稱以 **DTS_W_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|說明|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|評估期還剩 %1!lu!  天。 過期之後，就無法執行封裝。|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|引發警告。 在這個解釋警告特性的警告之前，應該還有其他特定的警告。|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|無法建立 XML 文件物件執行個體。 請確認已經正確安裝和註冊 MSXML。|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|無法載入 XML 組態檔。 XML 組態檔可能不正確或無效。|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|組態檔名稱 "%1" 無效。 請檢查組態檔名稱。|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|組態檔已經載入，但無效。 檔案格式不正確、可能遺漏元素或可能已經損壞。|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|找不到組態檔 "%1"。 請檢查目錄和檔案名稱。|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|找不到組態登錄機碼 "%1"。 組態項目指定的登錄機碼無法使用。 請檢查登錄，確定機碼存在。|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|在其中一個組態項目中的組態類型無效。 有效的類型列於 DTSConfigurationType 列舉中。|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|找不到封裝路徑參考的物件: "%1"。 嘗試在找不到的物件上解析封裝路徑時，就會發生這個問題。|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|組態項目 "%1" 的格式不正確，因為開頭不是封裝分隔符號。 請在封裝路徑前面加上 "\package"。|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|組態項目 "%1" 的格式不正確。 可能是因為遺漏分隔符號或格式化錯誤，例如無效的陣列分隔符號。|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|父變數 "%1" 的組態並未發生，因為沒有父變數集合。|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|無法匯入組態檔: "%1"。|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|父變數 "%1" 的組態並未發生，因為沒有父變數。 錯誤碼: 0x%2!8.8X!。|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|組態檔是空的，未包含組態項目。|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|組態 "%1" 的組態類型無效。 嘗試將組態物件的類型屬性設定為無效的組態類型時，就會發生這個問題。|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|在機碼 "%1" 中找不到登錄組態的組態類型。 請將名稱為 ConfigType 的值加入登錄機碼中，並給定字串值 "Variable"、"Property"、"ConnectionManager"、"LoggingProvider" 或 "ForEachEnumerator"。|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|在機碼 "%1" 中找不到登錄組態的組態值。 請將名稱為 Value 的值加入類型為 DWORD 或 String 的登錄機碼中。|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|處理組態無法在 "%1" 的封裝路徑上設定目的地。 嘗試設定目的地屬性或變數失敗時，就會發生這個問題。 請檢查目的地屬性或變數。|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|無法從 .ini 檔案擷取值。 ConfiguredValue 區段是空的或不存在: "%1"。|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|無法從 .ini 檔案擷取值。 ConfiguredType 區段是空的或不存在: "%1"。|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|無法從 .ini 檔案擷取值。 PackagePath 區段是空的或不存在: "%1"。|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|無法從 .ini 檔案擷取值。 ConfiguredValueType 區段是空的或不存在: "%1"。|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|無法成功匯入 SQL Server 的組態: "%1"。|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|.ini 組態檔無效，因為欄位是空的或遺漏了欄位。|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|資料表 "%1" 沒有任何組態記錄。 當從沒有組態記錄的 SQL Server 資料表設定時，就會發生這個問題。|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|不同的自訂事件使用相同名稱時發生錯誤。 自訂事件 "%1" 已經由這個容器的不同子系給予不同的定義。 當執行事件處理常式時，可能會發生錯誤。|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|組態嘗試變更唯讀變數。 變數位於封裝路徑 "%1"。|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|在封裝上呼叫 ProcessConfiguration 失敗。 組態嘗試在封裝路徑 "%1" 上變更屬性。|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|無法載入封裝的至少其中一個組態項目。 請檢查 "%1" 的組態項目和之前的警告，查看哪個組態失敗的描述。|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|組態檔中的組態項目 "%1" 無效，或無法設定變數。  此名稱指出哪個項目失敗。 在某些情況下，將無法取得名稱。|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|這個工作或容器失敗，因為 FailPackageOnFailure 屬性為 FALSE，封裝會繼續進行。 當封裝的 SaveCheckpoints 屬性設定為 TRUE 時，如果工作或容器失敗，就會公佈這個警告。|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|路徑是空的。|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS 警告碼 DTS_W_MAXIMUMERRORCOUNTREACHED。  Execution 方法成功，但引發的錯誤數目 (%1!d!) 到達最大容許值 (%2!d!); 導致失敗。 當錯誤數目到達 MaximumErrorCount 指定的數目時，就會發生這個問題。 請變更 MaximumErrorCount 或修正錯誤。|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|找不到組態環境變數。  環境變數是: "%1"。 當找不到封裝為組態設定所指定的環境變數時，就會發生這個問題。 請檢查封裝中的組態集合，確認指定的環境變數可用且有效。|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|連接管理員 "%1" 的提供者名稱已從 "%2" 變更為 "%3"。|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|讀取升級對應檔案時發生例外狀況。 例外狀況為 "%1"。|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|檔案 "%1" 中有重複的對應。 標記為 "%2"，機碼為 "%3"。|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|延伸模組 "%1" 已隱含升級至 "%2"。 請在 UpgradeMappings 目錄中加入這個延伸模組的對應。|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|檔案 "%1" 中的對應無效。 值不可以是 Null 或空白。 標記為 "%2"，機碼為 "%3"，值為 "%4"。|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|為了與舊版相容，ADO 類型連接管理員 "%1" 的 DataTypeCompatibility 屬性設定為 80。|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|For Each File 列舉值是空的。 For Each File 列舉值找不到符合檔案模式的任何檔案，或指定的目錄是空的。|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|無法將封裝路徑解析為封裝 "%1" 中的物件。 請確認封裝路徑有效。|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|反覆運算的運算式不是指派運算式: "%1"。 在 ForLoop 中，如果指派運算式中的運算式不是指派運算式，通常就會發生這種錯誤。|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|初始化運算式不是指派運算式: "%1"。 在 ForLoop 中，如果反覆運算式中的運算式不是指派運算式，通常就會發生這種錯誤。|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|可執行檔 "%1" 已成功貼上。 但是在集合 "LogProviders" 中找不到與此可執行檔相關聯的記錄提供者。  貼上的可執行檔未包含記錄提供者資訊。|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|已成功升級封裝。|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|"%1" ProgID 已被取代。 應該改用這個元件 "%2" 的新 ProgID。|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|作業 "%1" 失敗。|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|加密演算法 "%1" 使用較弱的加密法。|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|工作無法執行作業 "%1"。|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|檔案/處理序 "%1" 不在路徑中。|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|主旨是空的。|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|[收件者] 欄位的位址格式不正確。 可能遺漏 "@" 符號或無效。|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|[寄件者] 欄位的位址格式不正確。 可能遺漏 "@" 符號或無效。|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|兩個 XML 文件不相同。|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD 驗證將使用 XML 文件中 DOCTYPE 行所定義的 DTD 檔案， 不會使用指派給屬性 "%1" 的內容。|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|工作無法驗證 "%1"。|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|傳送動作值無效。  將設定為複製。|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|傳送方法值無效。  將設定為線上傳送。|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|下列訊息發生問題: "%1"。|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|目的地伺服器上已有錯誤訊息 "%1"。|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|目的地伺服器上已有作業 "%1"。|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|略過作業 "%1" 的傳送，因為它已存在於目的地端。|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|正在覆寫目的地伺服器端的作業 "%1"。|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|屬性 "FailIfExists" 的保存列舉值已變更且轉譯無效。 正在重設為預設值。|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|正在覆寫目的地端的登入 "%1"。|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|目的地端已有預存程序 "%1"。|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|目的地端已有規則 "%1"。|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|目的地端已有資料表 "%1"。|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|目的地端已有檢視表 "%1"。|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|目的地端已有使用者定義函數 "%1"。|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|目的地端已有預設值 "%1"。|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|目的地端已有使用者定義資料類型 "%1"。|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|目的地端已有分割區函數 "%1"。|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|目的地端已有分割區配置 "%1"。|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|目的地端已有結構描述 "%1"。|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|目的地端已有 SqlAssembly "%1"。|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|目的地端已有使用者定義彙總 "%1"。|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|目的地端已有使用者定義型別 "%1"。|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|目的地端已有 XmlSchemaCollection "%1"。|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|沒有指定的元素要傳送。|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|目的地端已有登入 "%1"。|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|目的地端已有使用者 "%1"。|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|無法驗證輸入資料行的歷程識別碼，因為執行樹狀目錄包含循環。|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|DataFlow 工作沒有元件。 請加入元件或移除工作。|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|%1 的 IsSorted 屬性設定為 TRUE，但所有輸出資料行的 SortKeyPositions 設定為零。|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|將不會讀取來源 "%1" (%2!d!)，因為在資料流程工作之外無法看到任何資料。|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|資料流程工作後續未使用輸出 "%3" (%4!d!) 和元件 "%5" (%6!d!) 的輸出資料行 "%1" (%2!d!)。 移除這個未使用的輸出資料行可以提升資料流程工作的效能。|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|已從資料流程工作移除元件 "%1" (%2!d!)，因為沒有用到輸出，而且輸入沒有副作用或未連接到其他元件的輸出。 如果需要此元件，則至少其中一個輸入的 HasSideEffects 屬性應該設定為 true，或輸出應該連接某些目標。|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|資料列已給予執行緒，但此執行緒不需進行任何處理。 配置具有離線輸出。 將 RunInOptimizedMode 屬性設定為 TRUE，可以更快速執行管線，並防止這個警告。|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|%1 的外部資料行與資料來源資料行不同步。 %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|資料行 "%1" 必須加入到外部資料行。|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|外部資料行 "%1" 必須更新。|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|必須從外部資料行移除 %1。|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|如果運算式 "%1" 的結果字串超過最大長度 %2!d! 個字元，則可能被截斷 字元。 運算式的結果值可能超過 DT_WSTR 的大小上限。|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|對 %2 上的輸入 %1!d! 呼叫 ProcessInput 方法，非預期地保留傳遞緩衝區的參考 。 在呼叫前，該緩衝區的 refcount 是 %3!d!， 呼叫傳回後變成 %4!d! 。|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|"%2" 上的 "%1" 的使用類型為 READONLY，但是並沒有運算式參考該類型。 請從可用的輸入資料行清單中移除該資料行，或者在運算式中參考它。|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|找不到元件 %2 的 "%1" 值。 找不到元件的 CurrentVersion 值。 如果元件未於 DTSInfo 區段中設定登錄資訊來包含 CurrentVersion 值，就會發生這個錯誤。 如果未適當地登錄元件，則在元件開發期間或在封裝中使用元件時，就會出現這個訊息。|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|緩衝區管理員無法取得暫存檔名稱。|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|緩衝區管理員無法在路徑 "%1" 上建立暫存檔。 不會再考慮使用此路徑做為暫存區。|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|警告: 無法開啟全域共用記憶體來與效能 DLL 通訊; 資料流程效能計數器無法使用。  若要解決問題，必須以管理員身分或在系統的主控台上執行此封裝。|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|檔案結尾有不完整的資料列。|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|在讀取標頭資料列時，已經到達資料檔案的結尾。 請確定標頭資料列分隔符號和要略過的標頭資料列數都正確。|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|無法從 OLE DB 提供者擷取資料行字碼頁資訊。  如果元件支援 "%1" 屬性，將使用該屬性的字碼頁。  如果目前的字串字碼頁值不正確，請變更屬性的值。  如果元件不支援屬性，將使用元件地區設定識別碼的字碼頁。|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|已經依指定方式排序資料，所以可以移除轉換。|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 參考的外部資料類型無法對應至資料流程工作資料類型。 將改用資料流程工作資料類型 DT_WSTR。|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|運算式 "%1" 永遠會導致資料截斷。 運算式包含靜態截斷 (固定值的截斷)。|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|在索引 %3!d!，識別碼為 %2!d! 的 輸入資料行 "%1"  未產生對應。 資料行的歷程識別碼為零。|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|指定的分隔符號與用來建立已存在之比對索引 "%1" 的分隔符號不相符。 當用來 Token 化欄位的分隔符號不符時，就會發生這個錯誤。 這對於比對行為或結果會產生未知的影響。|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|模糊查閱轉換的 MaxOutputMatchesPerInput 屬性為零。 將不會產生結果。|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|沒有具有 JoinType 資料行屬性設定為模糊的有效輸入資料行。  使用查詢轉換取代模糊查詢，可以改善完全聯結的效能。|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|參考資料行 "%1" 可能是 SQL 時間戳記資料行。 建立了模糊相符索引且製作參考資料表的複本時，所有參考資料表的時間戳記都將反映資料表在複製時的目前狀態。 如果 CopyReferenceTable 設定為 False，可能會發生非預期的行為。|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|給予 MatchIndexName 的資料表名稱 '%1' 已經存在，且 DropExistingMatchIndex 設定為 FALSE。  除非卸除這個資料表、指定不同名稱或將 DropExisitingMatchIndex 設定為 TRUE，否則轉換的執行會失敗。|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|輸入資料行 '%1' 的長度不等於要比對之參考資料行 '%2' 的長度。|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|DT_STR 來源資料行 "%1" 的字碼頁與 DT_STR 目的地資料行的字碼頁 "%2" 不符。  這可能會造成非預期的結果。|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|有 16 個以上的完全相符聯結，所以可能無法達到最佳效能。 請減少完全相符聯結的數目來提升效能。 SQL Server 限制每個索引最多 16 個資料行，所有查閱將使用反向索引。|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|Exhaustive 選項需要將整個參考載入主記憶體中。  由於已經為 MaxMemoryUsage 屬性指定了記憶體限制，因此整個參考資料表可能超出這個界限，而且比對作業可能會在執行階段失敗。|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|完全相符聯結中指定之資料行的累計長度超過索引鍵的 900 位元組限制。  模糊查閱會在完全相符資料行上建立索引，藉以提升查閱效能。建立這個索引時有可能失敗，迫使查閱尋求替代方法 (可能較慢) 來尋找相符項目。 如果效能是個問題，請嘗試移除一些完全相符聯結資料行，或縮短變動長度完全相符資料行的最大長度。|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|無法建立完全相符資料行的索引。 返回尋求替代的模糊查閱方法。|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|發生下列模糊群組內部管線警告，警告碼為 0x%1!8.8X!: "%2"。|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|具有外部資料類型 %2 的 %1 未指定最大長度。 將使用長度為 %4!d! 的 SSIS 資料流程工作資料類型 "%3" 。|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1 參考的外部資料類型 %2 無法對應至 SSIS 資料流程工作資料類型。  將改使用長度為 %3!d! 的 SSIS 資料流程工作資料類型 DT_WSTR 。|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|沒有任何資料列會傳送到錯誤輸出。 請設定錯誤或截斷配置，將資料列重新導向錯誤輸出，或者刪除資料流程轉換或附加至錯誤輸出的目的地。|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|傳送至錯誤輸出的資料列將會遺失。 請加入新的資料流程轉換或接收錯誤資料列的目的地，或重新設定元件，以停止將資料列重新導向錯誤輸出。|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|針對具有外部資料類型 %2 的 %1，XML 結構描述指定的 maxLength 限制為 %3!d!，此數值超過允許的最大資料行長度 %4!d!。 將使用長度為 %6!d! 的 SSIS 資料流程工作資料類型 "%5" 。|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|%1 在快取參考資料時，發現重複的參考索引鍵值。 這個錯誤只會發生在完整快取模式。 請移除重複的索引鍵值，或將快取模式變更為 PARTIAL 或 NO_CACHE。|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|從長度為 %2!d! 的資料流程資料行 "%1" 插入資料至長度為 %4!d! 的資料庫資料行 "%3"，因此可能會出現截斷 。|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|從長度為 %2!d! 的資料庫資料行 "%1" 擷取資料至長度為 %4!d! 的資料流程資料行 "%3"，因此可能會出現截斷 。|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|目前在使用錯誤資料列配置時不支援批次模式。 BatchSize 屬性將設定為 1。|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|未成功將任何資料列插入至目的地。 可能是因為資料行之間的資料類型不相符，或是因為使用 ADO.NET 不支援的資料類型。 由於此元件的錯誤配置不是 [失敗元件]，因此不會在此處顯示錯誤訊息; 將錯誤配置設為 [失敗元件] 便可在此處看到錯誤訊息。|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|由於將資料從輸入資料行 "%1" (資料類型為 "%2") 插入至外部資料行 "%3" (資料類型為 "%4")，可能會發生資料遺失。 如果這是預期中的行為，轉換的替代方法則是在 ADO NET 目的地元件之前使用資料轉換元件。|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1 已經沒有與資料庫資料行進行同步處理。  最新的資料行有 %2。 請視需要使用進階編輯器，重新整理可用的目的地資料行。|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|資料庫中沒有 %1。 它可能已被移除或重新命名。 請視需要使用進階編輯器，重新整理可用的目的地資料行。|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|名稱為 %1 的新資料行已加入至外部資料庫資料表。 請視需要使用進階編輯器，重新整理可用的目的地資料行。|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|沒有任何資料列會被傳送至無相符結果輸出。 請把轉換設為將無相符項目的資料列重新導向無相符結果輸出，或是刪除已附加至無相符結果輸出的資料流程轉換或目的地。|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|列舉 ADO.Net 提供者時收到例外狀況。 不變為 "%1"。 例外狀況訊息為: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|沒有任何輸入資料行對應到 %1。|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|資料表 "%1" 已變更。 此資料表可能已加入新的資料行。|  
  
##  <a name="msgInfo"></a> 參考用訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 參考用訊息的符號名稱以 **DTS_I_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|說明|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|正在啟動這個容器的分散式交易。|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|正在認可這個容器啟動的分散式交易。|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|正在中止目前的分散式交易。|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" 取得成功。|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" 釋放成功。|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" 建立成功。|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|將會為任何錯誤事件產生偵錯傾印檔案。|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|將會為下列事件代碼產生偵錯傾印檔案: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|事件代碼 0x%1!8.8X! 已導致在資料夾 "%2" 中產生偵錯傾印檔案。|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|正在建立 SSIS 資訊傾印檔案 "%1"。|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|已成功建立偵錯傾印檔案。|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|封裝格式已從版本 %1!d! 移轉到版本 %2!d! 。 必須儲存才能保留移轉變更。|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|此封裝中的指令碼已移轉。 此封裝必須儲存才能保留移轉變更。|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|正在接收檔案 "%1"。|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|正在傳送檔案 "%1"。|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|檔案 "%1" 已經存在。|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|因為內部錯誤，所以無法取得額外的錯誤資訊。|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|嘗試刪除檔案 "%1" 失敗。 當檔案不存在、檔案名稱拼字不正確或您沒有權限刪除檔案時，就可能發生這個問題。|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|封裝嘗試使用登錄機碼 "%1" 從登錄項目進行設定。|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|封裝嘗試從環境變數 "%1" 進行設定。|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|封裝嘗試從 .ini 檔 "%1" 設定。|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|封裝嘗試使用組態字串 "%1" 從 SQL Server 進行設定。|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|封裝嘗試從 XML 檔案 "%1" 設定。|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|封裝嘗試從父變數 "%1" 設定。|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|嘗試將 SSIS 從 "%1" 版升級到 "%2" 版。 封裝正在嘗試升級執行階段。|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|嘗試升級 "%1"。 封裝嘗試升級可延伸的物件。|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|封裝在執行期間會將檢查點儲存到檔案 "%1"。 封裝已設定為儲存檢查點。|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|封裝從檢查點檔案 "%1" 重新啟動。 封裝已設定為從檢查點重新啟動。|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|已更新檢查點檔案 "%1" 來記錄完成這個容器。|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|封裝順利完成之後已刪除檢查點檔案 "%1"。|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|檢查點檔案 "%1" 開始更新。|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|依據系統組態，最大並行可執行檔數目設定為 %1!d!。|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|最大並行可執行檔數目設定為 %1!d!。|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|開始執行封裝。|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|結束執行封裝。|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|已刪除目錄 "%1"。|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|已刪除檔案或目錄 "%1"。|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|覆寫目的地伺服器 "%2" 上的資料庫 "%1"。|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|略過錯誤訊息 "%1"，因為目的地伺服器上已有此訊息存在。|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|已傳送 "%1" 個錯誤訊息。|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|工作已傳送 "%1" 個預存程序。|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|已傳送 "%1" 個物件。|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|沒有要傳送的預存程序。|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|沒有要傳送的規則。|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|沒有要傳送的資料表。|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|沒有要傳送的檢視表。|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|沒有要傳送的使用者定義函數。|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|沒有要傳送的預設值。|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|沒有要傳送的使用者定義資料類型。|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|沒有要傳送的分割區函數。|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|沒有要傳送的分割區配置。|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|沒有要傳送的結構描述。|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|沒有要傳送的 SqlAssemblies。|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|沒有要傳送的使用者定義彙總。|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|沒有要傳送的使用者定義型別。|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|沒有要傳送的 XmlSchemaCollections。|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|沒有要傳送的登入。|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|沒有要傳送的使用者。|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|正在截斷資料表 "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|正在開始準備執行階段。|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|正在開始執行前階段。|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|正在開始執行後階段。|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|正在開始清除階段。|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|正在開始驗證階段。|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" 寫入 %2!ld! 個資料列 資料列。|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|正在開始執行階段。|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|緩衝區管理員偵測到系統虛擬記憶體偏低，但無法空出任何緩衝區。 已考量  %1!d! 個緩衝區，但 %2!d! 個已鎖定 。 可能是因為未安裝足夠記憶體，造成管線可用的記憶體不足、其他處理序正在使用記憶體或鎖定太多緩衝區。|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|緩衝區管理員執行 %3!d! 位元組的記憶體配置呼叫失敗， 無法空出任何緩衝區來緩和記憶體不足的壓力。 已考量  %1!d! 個緩衝區，但 %2!d! 個已鎖定 。 可能是因為未安裝足夠記憶體，造成管線可用的記憶體不足、其他處理序正在使用記憶體或鎖定太多緩衝區。|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|緩衝區管理員已配置 %1!d! 位元組， 但是仍偵測到記憶體不足的壓力，而且反覆嘗試交換緩衝區都告失敗。|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 已快取 %2!d! 個資料列 資料列。|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 已快取共 %2!d! 個 資料列。|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|原始來源配接器開啟檔案，但檔案未包含任何資料行。 配接器將不會產生資料。 這可能表示檔案損毀或沒有資料行，因此沒有資料。|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|有 OLE DB 參考訊息。|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|如果輸入資料行 "%1" 上的完全聯結 FuzzyComparisonFlags 設定為符合參考資料表資料行 "%2" 的預設 SQL 定序，則可以改善模糊相符的效能。  FuzzyComparisonFlagsEx 中也不可以設定摺疊 (Fold) 旗標。|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|在參考資料表中，如果在所有指定的完全相符資料行上建立索引，則可以提升模糊相符的效能。|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|並未檢閱錯誤與截斷配置。 如果您想繼續轉換這些資料列，請確定已設定讓這個元件將資料列重新導向錯誤輸出。|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|彙總轉換發現 %1!d! 個 索引鍵組合。 必須重新雜湊資料，因為索引鍵組合數目超出預期。 藉由調整 Keys、KeyScale 和 AutoExtendFactor 屬性，可以設定元件來避免資料重新雜湊。|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|彙總轉換發現 %1!d! 個 相異值。 轉換將重新雜湊資料，因為相異值數目超出預期。 藉由調整 CountDistinctKeys、CountDistinctKeyScale 和 AutoExtendFactor 屬性，可以設定元件來避免資料重新雜湊。|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|檔案 "%1" 的處理已開始。|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|檔案 "%1" 的處理已結束。|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|檔案 "%1" 已處理的資料列總數為 %2!I64d!。|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|"%1" 中資料插入作業的最終認可已啟動。|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|"%1" 中資料插入作業的最終認可已結束。|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|快取中已加入 %1!u! 個 資料列。 系統正在處理這些資料列。|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1 已處理快取中的 %2!u! 個 資料列。 處理時間為 %3 秒。 快取佔用 %4!I64u! 位元組的 記憶體。|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1 無法處理快取中的資料列。  處理時間為 %2 秒。|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1 已成功準備快取。 準備時間為 %2 秒。|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 已經執行下列作業：處理 %2!I64u! 個 資料列、發出 %3!I64u!  資料庫命令給參考資料庫並使用部分快取執行 %4!I64u! 個 查閱。|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 已經執行下列作業：處理 %2!I64u! 個 資料列、發出 %3!I64u!  個資料庫命令給參考資料庫、 使用部分快取執行 %4!I64u! 個查閱， 以及使用初始查閱中無相符項目的資料列快取執行 %5!I64u! 個查閱。|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 正在將快取寫入檔案 "%2"。|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 已將快取寫入檔案 "%2"。|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|OLE DB 目的地 "%1" 的插入認可大小上限屬性設定為 0。 這個屬性設定可能會導致執行中的封裝停止回應。 如需詳細資訊，請參閱 OLE DB 目的地編輯器 (連接管理員頁面) 的 F1 說明主題。|  
  
##  <a name="msgGeneral"></a> 一般和事件訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的符號名稱以 **DTS_MSG_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|說明|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|不正確的函數。|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|系統找不到指定的檔案。|  
|0x100|256|DTS_MSG_SERVER_STARTING|正在啟動 Microsoft SSIS 服務。<br /><br /> 伺服器版本 %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS 服務已啟動。<br /><br /> 伺服器版本 %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|等候作業逾時。|  
|0x103|259|DTS_MSG_SERVER_STOPPED|沒有其他可用的資料。|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS 服務無法啟動。<br /><br /> 錯誤: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|停止 Microsoft SSIS 服務時發生錯誤。<br /><br /> 錯誤: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS 服務組態檔不存在。<br /><br /> 載入預設值。|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS 服務組態檔不正確。<br /><br /> 讀取組態檔時發生錯誤: %1<br /><br /> 以預設值來載入伺服器。|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS 服務:<br /><br /> 指定組態檔的登錄設定不存在。<br /><br /> 嘗試載入預設組態檔。|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS 服務: 停止執行中的封裝。<br /><br /> 封裝執行個體識別碼: %1<br /><br /> 封裝識別碼: %2<br /><br /> 封裝名稱: %3<br /><br /> 封裝描述: %4<br /><br /> 封裝啟動者: %5。|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|封裝 "%1" 已啟動。|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|封裝 "%1" 已順利完成。|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|封裝 "%1" 已取消。|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|封裝 "%1" 失敗。|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|因為錯誤 %4，模組 %1 無法載入 DLL %2 來呼叫進入點 %3。 產品需要執行此 DLL，但在路徑上找不到此 DLL。|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|因為錯誤 %4，模組 %1 已載入 DLL %2，但找不到進入點 %3。 在路徑上找不到指定的 DLL，而產品需要執行此 DLL。|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|事件名稱: %1<br /><br /> 訊息: %9<br /><br /> 操作員: %2<br /><br /> 來源名稱: %3<br /><br /> 來源識別碼: %4<br /><br /> 執行識別碼: %5<br /><br /> 開始時間: %6<br /><br /> 結束時間: %7<br /><br /> 資料碼: %8|  
  
##  <a name="msgSuccess"></a> 成功訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 成功訊息的符號名稱以 **DTS_S_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|說明|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|值為 NULL。|  
|0x40005|262149|DTS_S_TRUNCATED|已截斷字串值。 緩衝區收到對資料行而言太長的字串，緩衝區已截斷字串。|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|在運算式評估期間發生截斷。 截斷是在評估期間發生，可能包含中間步驟的任何點。|  
  
##  <a name="msgPipeline"></a> 資料流程元件錯誤訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的符號名稱是以 **DTSBC_E_** 當作開頭，其中 "BC" 指的是大多數 Microsoft 資料流程元件衍生來源的原生基底類別。  
  
|十六進位碼|十進位碼|符號名稱|說明|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|輸出和錯誤輸出的總數 %1!lu! 不正確。 必須正好是 %2!lu!。|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|無法使用索引 %1!lu! 擷取輸出。|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|錯誤輸出數目 %1!lu! 不正確。 必須正好是 %2!lu!。|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|不正確的驗證狀態值 "%1!lu! "。  必須是 DTSValidationStatus 列舉的其中一個值。|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|輸入"%1!lu!" 沒有同步輸出。|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|輸入"%1!lu!" 沒有同步錯誤輸出。|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|HowToProcessInput 值 %1!lu! 無效。 必須是 HowToProcessInput 列舉的其中一個值。|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|無法從緩衝區取得資料列 "%1!ld!" 資料行 "%2!ld!" 的資訊 。  傳回的錯誤碼是 0x%3!8.8X!。|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|無法在緩衝區設定資料列 "%1!ld!" 資料行 "%2!ld!" 的資訊 。  傳回的錯誤碼是 0x%3!8.8X!。|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|屬性 "%1" 無效。|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|找不到屬性 "%1"。|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|指派值給唯讀屬性 "%1" 時發生錯誤。|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|%1 不允許插入輸出資料行。|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|輸出資料行的中繼資料與相關聯之輸入資料行的中繼資料不符。  將更新輸出資料行的中繼資料。|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|輸入資料行沒有相關聯的輸出資料行。 將加入輸出資料行。|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|輸出資料行沒有相關聯的輸入資料行。 將移除輸出資料行。|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|輸出資料行的中繼資料與相關聯之輸入資料行的中繼資料不符。  將取消對應輸入資料行。|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|輸入資料行沒有相關聯的輸出資料行。 將取消對應輸入資料行。|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|存在與輸出資料行相關聯的輸入資料行，但此輸出資料行已經與相同輸入的另一個輸入資料行相關聯。|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1 不允許插入外部中繼資料行。|  
  
  