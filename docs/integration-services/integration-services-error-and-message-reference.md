---
title: Integration Services 錯誤和訊息參考 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c4d989bf1049faa41838de1f86f93b9ef2db228e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057650"
---
# <a name="integration-services-error-and-message-reference"></a>Integration Services 錯誤和訊息參考

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  下表列出預先定義的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤、警告和參考用訊息 (依據每一個類別內的遞增號碼順序)，連同這些訊息的數字代碼和符號名稱。 每一個錯誤都會以欄位形式定義於 <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別內。  
  
 當您遇到錯誤碼而沒有描述時，這個清單可能會非常有用。 此清單這次沒有包含疑難排解資訊。  
  
> [!IMPORTANT]  
>  在使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 時所看到的許多錯誤訊息都是來自其他元件。 在本主題中，您會找到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 元件所引發的所有錯誤。 如果您在清單中看不到您的錯誤，表示該錯誤是由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]之外的元件所引發。 這可能包括 OLE DB 提供者、其他的資料庫元件 (例如 [!INCLUDE[ssDE](../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ) 或是其他的服務或元件，例如檔案系統、SMTP 伺服器或 Message Queuing (也稱為 MSMQ) 等等。 若要尋找有關這些外部錯誤訊息的資訊，請參閱該元件的特定文件集。  
  
 此清單包含下列的訊息群組：  
  
-   [錯誤訊息 (DTS_E_*)](#msgError)  
  
-   [警告訊息 (DTS_W_*)](#msgWarning)  
  
-   [參考用訊息 (DTS_I_*)](#msgInfo)  
  
-   [一般和事件訊息 (DTS_MSG_*)](#msgGeneral)  
  
-   [成功訊息 (DTS_S_*)](#msgSuccess)  
  
-   [資料流程元件錯誤訊息 (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> 錯誤訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的符號名稱以 **DTS_E_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|Description|  
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
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|SSIS 記錄提供者 "%1" 失敗，錯誤碼為 0x%2!8.8X! (%3)。  這表示可歸因於特定之記錄提供者的記錄錯誤。|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|SaveToSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。  發出的 SQL 陳述式失敗。|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|LoadFromSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。  發出的 SQL 陳述式失敗。|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|RemoveFromSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。發出的 SQL 陳述式失敗。|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|ExistsOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。 發出的 SQL 陳述式失敗。|  
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
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|SSIS 執行階段無法將 OLE DB 連接編列到分散式交易中，錯誤為 0x%1!8.8X! "%2"。|  
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
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|An error occurred when renaming folder " %1\\\\%2" to "%1\\\\%3" on SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|The RenameFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Error deleting SQL Server folder "%1".|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|The RemoveFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|The specified package path does not contain a package name. This occurs when the path does not contain at least one backslash or one forward slash.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Cannot find folder "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|While trying to find a folder on SQL an OLE DB error was encountered with error code 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|The SSIS logging provider has failed to open the log. Error code: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Failed to get ConnectionInfos collection with error 0x%1!8.8X! "%2". This error occurs when the call to IDTSApplication100::get_ConnectionInfos fails.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Deadlock detected while trying to lock variables. The locks cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|The Variables collection has not been returned from the VariableDispenser. An operation was attempted that is only allowed on dispensed collections.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|This Variables collection has already been unlocked. The Unlock method is called only once on a dispensed Variables collection.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|One or more variables failed to unlock.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|The Variables collection was returned the from VariableDispenser and cannot be modified. Items cannot be added to or removed from dispensed collections.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|The variable "%1" is already on the read list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|The variable "%1" is already on the write list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Failed to lock variable "%1" for read access with error 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Failed to lock variable "%1" for read/write access with error 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|The custom event "%1" is already declared with a different parameter list. A task is trying to declare a custom event, which another task has already declared with a different parameter list.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|The task providing the custom event "%1" does not allow this event to be handled in the package. The custom event was declared with AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|The VariableDispenser received an unsafe Variables collection. This operation cannot be repeated.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath was called on the ForEachEnumerator but there was no ForEachLoop package path specified.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|A deadlock was detected while trying to lock variable "%1" for read access. A lock could not be acquired after 16 attempts and timed out.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|A deadlock was detected while trying to lock variables "%1" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|A deadlock was detected while trying to lock variables "%1" for read access and variables "%2" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|The protection level of the package requires a password, but PackagePassword property is empty.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Failed to decrypt an encrypted XML node because the password was not specified or not correct. Package load will attempt to continue without the encrypted information.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Failed to decrypt a package that is encrypted with a user key. You may not be the user who encrypted this package, or you are not using the same machine that was used to save the package.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|The protection level, ServerStorage, cannot be used when saving to this destination. The system could not verify that the destination supports secure storage capability.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer method has failed.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|The package cannot be loaded because the state of the digital signature violates signature policy. Error 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|The package is not signed.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|The log provider for SQL Server Profiler was unable to load pfclnt.dll because it is only supported on 32-bit systems.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|The object cannot be added because another object with the same name already exists in the collection. Use a different name to resolve this error.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|The object name cannot be changed from "%1" to "%2" because another object in the collection already uses that name. Use a different name to resolve this error.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|There was an error enumerating the package dependencies. Check other messages for more information.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|The current package settings are not supported.  Please change the SaveCheckpoints property or the TransactionOption property.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|The connection manager failed to defect from the transaction.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|The specified breakpoint ID already exists. This error occurs when a task calls CreateBreakpoint with the same ID multiple times. It is possible to create a breakpoint with the same ID multiple times if the task calls RemoveBreakpoint on the first creation before creating the second one.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|The specified breakpoint ID does not exist. This error occurs when a task references a breakpoint that does not exist.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|The file, "%1", could not be opened for writing. The file could be read-only, or you do not have the correct permissions.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|No result rowset is associated with the execution of this query. The result is not correctly specified.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|Debug dump files were not generated correctly. The hresult is 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|The URL specified is not valid. This can happen when the server or proxy URL is null, or in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|The URL %1 is not valid. This can happen when a scheme other than http or https is specified, or the URL is in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Connection to server %1 cannot be established. This error can occur when the server does not exist, or the proxy settings are incorrect.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|The connection with the server has been reset or terminated. Try again later.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|The login attempt failed for "%1". This error occurs when the login credentials provided are incorrect. Verify the login credentials.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|The server name specified in the URL %1 cannot be resolved.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Proxy authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|SSL certificate response obtained from the server was not valid. Cannot process the request.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|The request has timed out. This error can occur when the timeout specified was too short, or a connection to the server or proxy cannot be established. Ensure that the server and proxy URL are correct.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Client certificate is missing. This error occurs when the server is expecting an SSL client certificate and the user has provided an invalid certificate, or has not provided a certificate. A client certificate must be configured for this connection.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|The specified server, URL %1, has a redirect and the redirect request failed.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Server authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|Request cannot be processed. Try again later.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|Server returned status code - %1!u! : %2. This error occurs when the server is experiencing problems.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|This platform is not supported by WinHttp services.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Timeout value is not valid. Timeout should be in the range of %1!d! to %2!d! (in seconds).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|The chunk size is not valid. The ChunkSize property should be in the range of %1!d! to %2!d! (in KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Error processing client certificate. This error can occur when the client certificate provided was not found in the Personal Certificate Store. Verify that the client certificate is valid.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|Server returned error code "403 - Forbidden". This error can occur when the specified resource needs "https" access, but the certificate validity period has expired, the certificate is not valid for the use requested, or the certificate has been revoked or revocation can not be checked.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Error initializing HTTP session with proxy "%1". This error can occur when an invalid proxy was specified. HTTP connection manager only supports CERN-type proxies.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Error opening certificate store.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Failed to decrypt protected XML node "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Failed to decrypt protected connection string for server "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|The version number cannot be negative. This error occurs when the VersionMajor, VersionMinor, or VersionBuild property of the package is set to a negative value.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|The package has been migrated to a later version during loading. It must be reloaded to complete the process. This is an internal error code.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Package migration from version %1!d! to version %2!d! failed with error 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Package migration module has failed to load.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Package migration module has failed.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Unable to persist object using default persistence. This error occurs when the default persistence is unable to determine which objects are on the hosted object.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|Cannot add or remove an element from a package in runtime mode. This error occurs when an attempt is made to add or remove an object from a collection while the package is executing.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|The "%1" node cannot be found in custom default persistence. This error occurs if the default saved XML of an extensible object was changed in a way that a saved object is no longer found, or if the extensible object itself changed.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|This collection cannot be modified during package validation or execution.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|The "%1" collection cannot be modified during package validation or execution. "%2" cannot be added to the collection.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|Connection with the FTP server has not been established.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|An error occurred in the requested FTP operation. Detailed error description: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|The number of retries is not valid. The number of retries should be between %1!d! and %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|The FTP connection manager needs the following DLL to function: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|The port specified in the connection string is not valid. The ConnectionString format is ServerName:Port. Port should be an integer value between %1!d! and %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Creating folder "%1" ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Deleting folder "%1" ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Changing current directory to "%1". %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|No files to transfer. This error can occur when performing a Send or Receive operation and no files are specified for the transfer.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|Specified local path is not valid. Specify a valid local path. This can occur when the specified local path is null.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|No files specified to delete.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Internal error occurred while loading the certificate. This error could occur when the certificate data is invalid.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Internal error occurred while saving the certificate data.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|Checkpoint file "%1" does not match this package. The ID of the package and the ID in the checkpoint file do not match.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|An existing checkpoint file is found with contents that do not appear to be for this package, so the file cannot be overwritten to start saving new checkpoints. Remove the existing checkpoint file and try again. This error occurs when a checkpoint file exists, the package is set to not use a checkpoint file, but to save checkpoints. The existing checkpoint file will not be overwritten.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|The checkpoint file "%1" is locked by another process. This may occur if another instance of this package is currently executing.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Checkpoint file "%1" failed to open due to error 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Checkpoint file "%1" failed during creation due to error 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|The FTP Port contains an invalid value. The FTP Port value should be an integer between %1!d! and %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Connect to SSIS Service on machine "%1" failed:<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|The Expression property is not supported on Variable objects. Use the EvaluateAsExpression property instead.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|The expression "%1" on property "%2" cannot be evaluated. Modify the expression to be valid.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|The result of the expression "%1" on property "%2" cannot be written to the property. The expression was evaluated, but cannot be set on the property.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|The evaluation expression for the loop is not valid. The expression needs to be modified. There should be additional error messages.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|The expression "%1" must evaluate to True or False. Change the expression to evaluate to a Boolean value.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|There is no expression for the loop to evaluate. This error occurs when the expression on the For Loop is empty. Add an expression.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|The assignment expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|The initialization expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|The version number in the package is not valid. The version number cannot be greater than current version number.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|The version number in the package is not valid. The version number is negative.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|The package has an older format version, but automatic package format upgrading is disabled.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|A truncation occurred during evaluation of the expression.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|The wrapper was unable to set the value of the variable specified in the ExecutionValueVariable property.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|The expression for variable "%1" failed evaluation. There was an error in the expression.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|The attempted operation is not supported with this database version.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Transaction cannot be specified when a retained connection is used. This error occurs when Retain is set to TRUE on the connection manager, but AcquireConnection was called with a non-null transaction parameter.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Incompatible transaction context was specified for a retained connection. This connection has been established under a different transaction context. Retained connections can be used under exactly one transaction context.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Resume call failed because the package is not suspended. This occurs when the client calls resume, but the package is not suspended.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Execute call failed because the executable is already executing. This error occurs when the client calls Execute on a container that is still executing from the last Execute call.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Suspend or Resume call failed because the executable is not executing, or is not the top-level executable. This occurs when the client calls Suspend or Resume on an executable that is not currently processing an Execute call.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|The file specified in the For Each File enumerator is not valid. Check that the file specified in the For Each File enumerator exists.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|The value index is not an integer . Mapping a For Each Variable number %1!d! to the variable "%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|The value index is negative. The ForEach Variable Mapping number %1!d! to variable "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|ForEach Variable Mapping number %1!d! to variable "%2" cannot be applied.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Failure when adding an object to a ForEachPropertyMapping that is not a direct child of the ForEachLoop container.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Failed to remove a system variable. This error occurs when removing a variable that is a required variable.  Required variables are variables that are created by the runtime for communicating between tasks and the runtime.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Changing the property of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Changing the name of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Changing the namespace of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Changing the event handler name failed. Event handler names are read-only.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Cannot retrieve path to object. This is a system error.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|The type of the value being assigned to variable "%1" differs from the current variable type. Variables may not change type during execution. Variable types are strict, except for variables of type Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Invalid characters in string: "%1". This occurs when a string supplied for a property value contains unprintable characters.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS object name is invalid. More specific errors would have been raised explaining the exact naming problem.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|The property "%1" is read only. This occurs when a change to a read-only property is attempted.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|The object does not support type information. This occurs when the runtime attempts to get the type information from an object to populate the Properties collection.  The object must support type information.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|The property "%1" is write-only. This error occurs when trying to retrieve the value of a property through a property object, but the property is write-only.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|The object does not implement IDispatch. This error occurs when a property object or properties collection attempts to access an IDispatch interface on an object.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Unable to retrieve the type library of the object. This error occurs when the Properties collection attempts to retrieve the type library for an object through its IDispatch interface.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Cannot create a task from XML for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Failed to create an XML document "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|An error occurred because there is a property mapping from a variable to a property with a different type. The property type must match the variable type.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Attempted to set property mapping to target unsupported object type. This error occurs when passing an unsupported object type to a property mapping.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1".  Verify that the package path is valid.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|The destination property for the property map is empty. Set the destination property name.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|The package failed to restore at least one property mapping.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|The variable name is ambiguous because multiple variables with this name exist in different namespaces. Specify namespace-qualified name to prevent ambiguity.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|The destination object in a property mapping has no parent. The destination object is not a child of any sequence container. It may have been removed from the package.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|The property mapping is not valid. The mapping is ignored.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Failure when alerting property mappings that a target is being removed.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|An invalid property mapping is found on the For Each Loop. This occurs when the ForEach property mapping fails to restore.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|A destination property was specified on a property mapping that is invalid. This occurs when a property is specified on a destination object that in not found on that object.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Cannot create a task from XML. This occurs when the runtime is unable to resolve the name to create a task. Verify that the name is correct.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|Cannot replace the existing checkpoint file with the updated checkpoint file. The checkpoint was successfully created in a temporary file, but overwriting the existing file with the new file failed.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|The package is configured to always restart from a checkpoint, but checkpoint file is not specified.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|The attempt to load the XML checkpoint file "%1" failed with error 0x%2!8.8X! "%3". Check that the file name specified is correct, and that the file exists.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|The package failed during execution because the checkpoint file cannot be loaded. Further execution of the package requires a checkpoint file. This error usually occurs when the CheckpointUsage property is set to ALWAYS, which specifies that the package always restarts.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|The evaluation condition expression on the For Loop "%1" is empty. There must be a Boolean evaluation expression in the For Loop.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|The result of the assignment expression "%1" cannot be converted to a type that is compatible with the variable that it was assigned to.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Error using a read-only variable "%1" in an assignment expression. The expression result cannot be assigned to the variable because the variable is read only. Choose a variable that can be written to, or remove the expression from this variable.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Cannot evaluate expression "%1" because the variable "%2" does not exist or cannot be accessed for writing. The expression result cannot be assigned to the variable because the variable was not found, or could not be locked for write access.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|The expression "%1" has a result type of "%2", which cannot be converted to a supported type.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|The conversion of the result of the expression"%1" from type "%2" to a supported type failed with error code 0x%3!8.8X!. An unexpected error occurred when trying to convert the expression result to a type supported by the runtime engine, even though the type conversion is supported.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|The object name is not valid. The name cannot be set to NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|The object name is not valid. The name cannot be empty.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|The object name "%1" is not valid. The name cannot contain any of the following characters: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|Object name "%1" is not valid. The name cannot contain control characters that render it unprintable.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|Object name "%1" is not valid. Name cannot begin with a whitespace.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|Object name "%1" is not valid. Name cannot end with a whitespace.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|Object name "%1" is not valid. Name must begin with an alphabetical character.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|Object name "%1" is not valid. Name must begin with an alphabetical character or underscore "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|Object name "%1" is not valid. Name must contain only alphanumeric characters or underscores "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|Object name "%1" is not valid. The name cannot contain any of the following characters: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Failed to load the value property "%1" using default persistence.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|Connection manager "%1" is not of type "%2"|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" is empty|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Invalid data node in the nodelist enumerator section|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|No enumerator can be created|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|The operation failed because the cache is in use.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|The property cannot be modified.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|The package upgrade has failed.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Error 0x%1!8.8X! while loading package file "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|The package is not specified.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|The connection is not specified.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" has an unsupported type "%2". Only "FILE" and "OLEDB" connection managers are supported.|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Error 0x%1!8.8X! while loading package file "%3" into an XML document. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Error 0x%1!8.8X! while preparing to load the package. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|The Validate method on the task failed, and returned error code 0x%1!8.8X! (%2). The Validate method must succeed and indicate the result using an "out" parameter.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|The Execute method on the task returned error code 0x%1!8.8X! (%2). The Execute method must succeed, and indicate the result using an "out" parameter.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|A failure occurred on task "%1": 0x%2!8.8X! while retrieving dependencies. The runtime was retrieving dependencies from the task's dependencies collection when the error occurred. The task may have incorrectly implemented one of the dependency interfaces.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|There were errors during task validation.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|The connection string format is not valid. It must consist of one or more components of the form X=Y, separated by semicolons. This error occurs when a connection string with zero components is set on database connection manager.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|The connection string components cannot contain unquoted semicolons. If the value must contain a semicolon, enclose the entire value in quotes. This error occurs when values in the connection string contain unquoted semicolons, such as the InitialCatalog property.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Validation of one or more log providers failed. The package cannot execute. The package does not execute when a log provider fails validation.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Invalid value in array.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|An element of the enumerator returned by the ForEach Enumerator does not implement IEnumerator, contradicting the CollectionEnumerator property of the ForEach Enumerator.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|The enumerator failed to retrieve element at index "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Function not found.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Function not found.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX Script Task was initiated with a wrong XML element.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|An error occurred while attempting to retrieve the scripting languages installed on the system.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|An error occurred while creating the ActiveX script host. Verify that you have the script host installed properly.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|An error occurred while trying to instantiate the script host for the chosen language. Verify that the script language you have chosen is installed on your system.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|An error occurred while adding the SSIS variables to the script host namespace. This might prevent the task from using SSIS variables in the script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|A fatal error occurred while trying to parse the script text. Verify that the script engine for the chosen language is installed properly.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|The function name entered is not valid. Verify that a valid function name has been specified.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|An error occurred while executing the script. Verify that the script engine for the selected language is installed properly.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|An error occurred while adding the managed type library to the script host. Verify that the DTS 2000 runtime is installed.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Bulk Insert Task was initiated with a wrong XML element.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Data file name not specified.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Failed to acquire the specified connection: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Attempt to obtain the Connection Manager failed.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|The connection is not valid.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|The connection is null.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Execution failed.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|An error occurred while retrieving the tables from the database.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|An error occurred while retrieving the columns of the table.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|An error occurred in the database operation.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|The specified connection "%1" is either not valid, or points to an invalid object. To continue, specify a valid connection.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|The destination connection specified is not valid. Supply a valid connection to continue.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|You must specify a table name to continue.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|The connection is not valid.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Execution failed.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Error occurred while retrieving the tables from the database.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Error occurred while retrieving the columns of the table.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Error occurred while trying to open the data file.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Cannot convert the input OEM file to the specified format.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Error in database operation.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|No connection manager specified.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|Connection "%1" is not an Analysis Services connection.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Unable to locate connection "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services Execute DDL task received an invalid task data node.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services Processing task received an invalid task data node.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|The DDL is not valid.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|The DDL found in ProcessingCommands is not valid.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|The Execution result cannot be saved in a read-only variable.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|Variable "%1" it's not defined.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|Connection Manager "%1" it's not defined.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|Connection Manager "%1" it's not a FILE Connection Manager.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|"%1" was not found during deserialization.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|The trace has been stopped due to an exception.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Execution of DDL failed.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|Variable "%1" is not defined.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|File connection "%1" is not defined.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Execute DTS 2000 Package task is initiated with a wrong XML element.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Package name is not specified.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|Package ID is not specified.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|Package version GUID is not specified.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server is not specified.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|SQL Server user name not specified.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Storage file name not specified.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|The DTS 2000 package property is empty.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|An error occurred while executing the DTS 2000 package.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Cannot load the available SQL Servers from the network. Check the network connection.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|The data type cannot be null. Please specify the correct data type to use for validating the value.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Cannot validate a null against any data type.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|A required argument is null.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|To execute the DTS 2000 Package task, start SQL Server Setup and use the Advanced button from the Components to Install page to select Legacy Components.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|The time-out value provided is not valid. Specify the number of seconds that the task allows the process to run. The minimum time-out is 0, which indicates that no time-out value is used and the process runs to completion or until an error occurs. The maximum time-out is 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Cannot redirect streams if the process can continue executing beyond the lifetime of the task.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|The process timed out.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|The executable is not specified.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|The standard out variable is read-only.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|The standard error variable is read-only.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|The Execute Process task received a task data node that is not valid.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|In Executing "%2" "%3" at "%1", The process exit code was "%4" while the expected was "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|The directory "%1" does not exist.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|File/Process "%1" does not exist in directory "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|Working Directory "%1" does not exist.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|The process exited with return code "%1". However, "%2" was expected.|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Synchronization object failed.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|The File System task received an invalid task data node.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|The Directory already exists.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" is not valid on operation type "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|Destination property of operation "%1" not set.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|Source property of operation "%1" not set.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is not a file.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|Variable "%1" does not exist.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|File or directory "%1" represented by connection "%2" does not exist.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|The destination file connection manager "%1" has an invalid usage type: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|The source file connection manager "%1" has an invalid usage type "%2".|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Provides information regarding File System operations.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|File System Task|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Perform file system operations, such as copying and deleting files.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Synchronization object failed.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Unable to obtain the file list.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|The local path is empty.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|The remote path is empty.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|The local variable is empty.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|The remote variable is empty.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|The FTP task received an invalid task data node.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid FTP connection is provided.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|The connection specified is not an FTP connection. Verify that a valid FTP connection is provided.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|There are no files at "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|The File "%1" doesn't contain file path(s).|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|The variable "%1" doesn't contain file path(s).|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|Variable "%1" does not exist.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Invalid path on operation "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" already exists.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is Not a file.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Directory is not specified in the variable "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|No files found in "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Directory is not specified in the file connection manager "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Unable to delete local file "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Unable to remove local directory "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Unable to create local directory "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Unable to receive files using "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Unable to send files using "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Unable to create remote directory using "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Unable to remove remote directory using "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Unable to delete remote files using "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Unable to connect to FTP server using "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|Variable "%1" doesn't start with "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|Remote path "%1" doesn't start with "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the FTP connection. Please check if you have specified a valid connection type "%1".|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Opening the certificate store failed.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|An error occurred while retrieving the display name of the certificate.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|An error occurred while retrieving the issuer name of the certificate.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|An error occurred while retrieving the friendly name of the certificate.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|The MSMQ connection name is not set.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Task was initialized with the wrong XML element.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|Data file name is empty.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|The name specified for the data file to save is empty.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|File size should be less than 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Saving the data file failed.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|String filter value is empty.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Queue path is not valid.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|The message queue task does not support enlisting in distributed transactions.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|The message type is not valid.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|The message queue timed out. No message has been received.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|The property specified is not valid. Verify that the argument type is correct.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Message is not authenticated.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|You are trying to set the value of Encryption Algorithm with an invalid object.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|The variable to receive string message is empty.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|Variable to receive variable message is empty.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|Connection "%1" is not of type MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|The data file "%1" already exists at the specified location. Cannot overwrite the file as the Overwrite option is set to false.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|The specified variable "%1" to receive string message is not found in the package variable collection.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|The connection manager "%1" is empty.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|The connection manager "%1" does not exist.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Error "%1": "%2"\r\nLine "%3"   Column "%4" through "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|There was an error compiling the script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Error "%1": "%2"\r\nLine "%3" Columns "%4"-"%5"\r\nLine Text: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|User script returned a failure result.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|User script files failed to load.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|User script threw an exception: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Could not create an instance of entrypoint class "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|There was an exception while loading Script Task from XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|Source item "%1" was not found in the package.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|Binary item "%1" was not found in the package.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" was not recognized as a valid script language.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|The script name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|The script language specified is not valid.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Cannot initialize to a null task.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|The Script Task user interface must initialize to an Script Task.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|The Script Task user interface is not initialized.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|Name cannot be empty.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|The project name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|The script language specified is not valid.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Entry point not found.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|The script language is not specified. Verify that a valid script language is specified.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|User interface initialization: The task is null.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|The Script Task user interface is initialized with an incorrect task.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|No recipient is specified.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|The Simple Mail Transfer Protocol (SMTP) server is not specified. Provide a valid name or IP address of the SMTP server.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Send Mail task is initiated with an incorrect XML element.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|Either the file "%1" does not exist or you do not have permissions to access the file.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Verify that the Simple Mail Transfer Protocol (SMTP) server specified is valid.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type File.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|On operation "%1", file "%2" does not exist.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|Connection "%1" is not of type SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|Connection "%1" is empty.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|The specified connection "%1" does not exist.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|No Transact-SQL statement specified.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|The connection does not support XML result sets.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Cannot locate a handler for the specified connection type.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|No connection manager is specified.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Cannot acquire a connection from the connection manager.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Cannot have a null parameter name.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|The parameter name is not valid.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Valid parameter names are of type Int or String.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|Variable "%1" cannot be used in a result binding because it is read-only.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|The index is not assigned in this collection.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|The variable "%1" cannot be used as an "out" parameter or return value in a parameter binding because it is read-only.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|The object does not exist in this collection.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Cannot acquire a managed connection.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Cannot populate the result columns for a single row result type. The query returned an empty result set.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|There is an invalid number of result bindings returned for the ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|The result binding name must be set to zero for full result set and XML results.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|The parameter directions flag is not valid.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|The XML fragment does not contain SQL Task data.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|A parameter with type return value is not the first parameter, or there are more than one parameter of type return value.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not a file connection manager.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|Type of variable "%1" is not string.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|Variable "%1" does not exist or could not be locked.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|Connection manager "%1" does not exist.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Failed to acquire connection "%1". Connection may not be configured correctly or you may not have the right permissions on this connection.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Result binding by name "%1" is not supported for this connection type.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|A result set type of single row is specified, but no rows were returned.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|No disconnected record set is available for the Transact-SQL statement.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Unsupported type.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Unknown type.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Unsupported data type on parameter binding \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|Parameter names cannot be an mix of ordinal and named types.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|The parameter direction on parameter binding \\"%s\\" is not valid.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|The data type on result set binding \\"%s\\" is not supported.|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|The result column index %d is not valid.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Cannot find column \\"%s\\" in the result set.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|No result rowset is associated with the execution of this query.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Disconnected recordsets are not available from ODBC connections.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|The data type in the result set, column %hd, is not supported.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|Cannot load XML with query result.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|A connection name or variable name for the package must be specified.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Failed to create the package.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|The TableMetaDataNode is not an XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Failed to create the pipeline.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|The variable is not the correct type.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|The connection manager specified is not a FILE connection manager.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Invalid file name specified on the connection manager "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid HTTP connection is specified.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|The connection does not exist. Verify that a valid, existing HTTP connection is specified.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|The Web Service name is empty. Verify that a valid web service name is specified.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|The web method name is empty. Verify that a valid web method is specified.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|The web method is empty or may not exist. Verify that there is an existing web method to specify.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|The output location is empty. Verify that an existing file connection or variable is specified.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|The variable cannot be found. Verify that the variable exists in the package.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Cannot save the result. Verify that the variable is not read-only.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|The Web Service Task is initiated with an incorrect XML element.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Unexpected XML element found.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the HTTP connection. Verify that a valid connection type is specified.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Cannot save the result. Verify that there is an existing file connection.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Cannot save the result. Verify that the file exists.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Cannot save the result. The file name is empty or the file is in use by another process.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|There was an error in acquiring the file connection. Verify that a valid file connection is specified.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Only Complex Types with Primitive values, Primitive Arrays, and Enumerations are supported.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Only Primitive, Enum, Complex, PrimitiveArray, and ComplexArray types are supported.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|This version of WSDL is not supported.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Initialized with an incorrect XML element.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|A mandatory attribute is not found.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|The enum "%1" does not have any values. The WSDL is corrupted.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|The connection cannot be found.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Connection by this name already exists.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|Connection cannot be null or empty.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|The specified Uniform Resource Identifier (URI) does not contain a valid WSDL.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Could not read the WSDL file. The input WSDL file is not valid. The reader threw the following error: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|Service Description cannot be null.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|Service name cannot be null.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL cannot be null.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|The service is not currently available.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|The service is not available on the SOAP port.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find the Binding that corresponds to the SOAP port.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find a PortType that corresponds to the SOAP port.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Cannot find the message that corresponds to the method specified.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Could not generate the proxy for the given web service. The following errors were encountered while generating the proxy "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Could not load the proxy for the given web service. The exact error is as follows: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Could not find the specified service. The exact error is as follows: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|The Web Service threw the following error during method execution: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Could not execute the web method. The exact error is as follows: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo cannot be null.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|The specified WebMethodInfo is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue is not of type PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|The WebMethodInfo you have specified is wrong. "%1" is not Primitive Type.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|The format of the ArrayValue is not valid. There should be at least one element in the array.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|The value of the enumeration cannot be null. Select a default value for the enumeration.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Cannot validate a null against any datatype.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|The enumeration Value is not correct.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|The class specified does not contain a public property by the name "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Cleanup failed. The proxy that was created for the web service may not have been deleted.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Could not create an object of type "%1". Please check whether the default constructor exists.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|The data type cannot be null. Specify the value of the data type to validate.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|The ParamValue cannot be inserted at this position. The index specified might be lesser than zero or greater than the length.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|The input WSDL file is not valid.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|The destination must be set.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|No WMI connection is set.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI Data Reader Task received an invalid task data node.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|The task failed validation.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|Variable "%1" is not of type string or object.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|Variable "%1" should be of type object to be assigned a data table.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Task failed due to invalid WMI query: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Unable to write to variable "%1" since it set to keep its original value.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|The WMI connection is missing.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|The task failed to execute the WMI query.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|The WMI Event Watcher Task received a task data node that is not valid.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Timeout of "%1" second(s) occurred before event represented by "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Watching for the Wql query caused the following system exception: "%1". Check the query for errors or WMI connection for access rights/permissions.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|The Operations specified is not defined.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|The connection type is not File.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Cannot get an XmlReader from the source XML document.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Cannot get an XmlReader from the changed XML document.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Cannot get the XDL diffgram reader from the XDL diffgram XML.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|The node list is empty.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|The element was not found.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|The Operations specified is not defined.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Unexpected content item in XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|No schema found to enforce validation.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|A validation error occurred when validating the instance document.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|The root nodes do not match.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|The Edit Script Operation type in the final Edit Script is not valid.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|CDATA nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Comment nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Text nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Significant white space nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Correct the OperationCost array so that it reflects the XmlDiffOperation enumeration.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|There are no operations in the task.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|The document already contains data and should not be used again.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|The node type is not valid.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|The XML Task received a task data node that is not valid.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|Variable data type is not a String.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Cannot get encoding from XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|Source is not specified.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|Second operand is not specified.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Invalid XDL diffgram. "%1" is an invalid path descriptor.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Invalid XDL diffgram. No node matches the path descriptor "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Invalid XDL diffgram. Expecting xd:xmldiff as a root element with namespace URI "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute on the xd:xmldiff element is missing.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute on the xd:xmldiff element is missing.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute has an invalid value.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute has an invalid value.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|The XDL diffgram is not applicable to this XML document. The rcDocHash value does not match.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Invalid XDL diffgram; more than one node matches the "%1" path descriptor on the xd:node or xd:change element.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|The XDL diffgram is not applicable to this XML document. A new XML declaration cannot be added.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Internal Error. XmlDiffPathSingleNodeList can contain only one node.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Internal Error. "%1" nodes left after patch, expecting 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|The File/Text Produced by the XSLT is not a valid XmlDocument, thus can not be set as result of operation: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|Property "%1" has no source Xml text; Xml Text is either invalid, null or empty string.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|A source connection must be specified.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|A destination connection must be specified.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|The connection "%1" could not be found in the package.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|The connection "%1" specifies a SQL Server instance with a version that is not supported for transfer.  Only versions 7, 2000, and 2005 are supported.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|The source connection "%1" must specify a SQL Server instance with a version earlier than or the same as the destination connection "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|A source database must be specified.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|The source database "%1" must exist on the source server.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|A destination database must be specified.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|The source database and the destination database can not be the same.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|The transfer file information %1 is missing the filename.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|The transfer file information %1 is missing the folder part.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|The transfer file information %1 is missing the network share part.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|The number of source transfer files and the number of destination transfer files must be the same.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|Enlisting in transactions is not supported.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|The following exception occurred during an offline database transfer: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|The network share "%1" could not be found.|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|The network share "%1 could not be accessed.  The error is: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|The user "%1" must be a DBO or a sysadmin for "%2" in order to perform an online database transfer.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|The user "%1" must be a sysadmin on "%2" to perform an offline database transfer.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Full text catalogs can only be included when performing an offline database transfer between 2 SQL Server 2005 servers.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|The database "%1" already exists on the destination server "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|At least one source file must be specified.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Could not find the file "%1" in the source database "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|The operation requested is not allowed in systems compliant with U.S. FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Executing the query "%1" failed with the following error: "%2". Possible failure reasons: Problems with the query, "ResultSet" property not set correctly, parameters not set correctly, or connection not established correctly.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Error reading stored procedure names from the xml file.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Invalid data node for the Transfer Stored Procedure task.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|Connection "%1" is not of type "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Execution failed with the following error "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|An error occurred with the following error message: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Bulk insert execution failed.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Invalid destination path.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Can not create directory. User chose to fail the task if directory exists.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|The task has a transaction option of "Required" and connection "%1" is of type "ODBC". ODBC connections don't support transactions.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|An error occurred while assigning a value to variable "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|The source is empty.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|The destination is empty.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|File or directory "%1" does not exist.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|Variable "%1" is used as a source or destination and is empty.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|The variable "%1" should be of type object to be assigned a data table.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|The variable "%1" does not have a string data type.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|There was an error acquiring the FTP connection. Verify that a valid connection type is specified in "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|The FTP connection manager "%1" can not be found.|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|File usage type of connection "%1" should be "%2" for operation "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|The source server can not be the same as the destination server.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|There are no Error Messages to transfer.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|The lists of error messages and their corresponding languages are of different sizes.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|The error message id "%1" is out of the allowed range of user defined error messages. User defined error message ids are between 50000 and 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|This task can not participate in a transaction.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Failed to transfer some or all of the Error Messages.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|The error message "%1" can not be found at source server.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Execution failed with the following error: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Failed to transfer the Job(s).|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|There are no Jobs to transfer.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|The job "%1" can not be found at source server.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|The list of "Logins" to transfer is empty.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Can not get the list of "Logins" from source server.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|Login "%1" already exists at destination server.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|Login "%1" does not exist at source.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Failed to transfer some or all of the logins.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Failed to transfer the stored procedure(s). More informative error should have been raised.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Stored Procedure "%1" is not found at the source.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|Stored procedure "%1" already exists at destination server.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|There are no stored procedures to transfer.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Failed to transfer the object(s).|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|The list of "Objects" to transfer is empty.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|Stored procedure "%1" does not exist at the source.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|An error occurred while trying to get set the Stored Procedures list to transfer: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|Rule "%1" does not exist at the source.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|An error occurred while trying to get set the Rules list to transfer: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|Table "%1" does not exist at the source.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|An error occurred while trying to get set the Tables list to transfer: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|View "%1" does not exist at the source.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|An error occurred while trying to get set the Views list to transfer: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|User Defined Function "%1" does not exist at the source.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|An error occurred while trying to get set the User Defined Functions list to transfer: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|Default "%1" does not exist at the source.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|An error occurred while trying to get set the Defaults list to transfer: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|User Defined Data Type "%1" does not exist at the source.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|An error occurred while trying to get set the User Defined Data Types list to transfer: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|Partition Function "%1" does not exist at the source.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|An error occurred while trying to get set the Partition Functions list to transfer: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|Partition Scheme "%1" does not exist at the source.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|An error occurred while trying to get set the Partition Schemes list to transfer: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|Schema "%1" does not exist at the source.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|An error occurred while trying to get set the Schemas list to transfer: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1" does not exist at the source.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|An error occurred while trying to get set the SqlAssemblies list to transfer: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|User Defined Aggregate "%1" does not exist at the source.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|An error occurred while trying to get set the User Defined Aggregates list to transfer: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|User Defined Type "%1" does not exist at the source.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|An error occurred while trying to get set the User Defined Types list to transfer: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1" does not exist at the source.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|An error occurred while trying to get set the XmlSchemaCollections list to transfer: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Objects of type "%1" are only supported between SQL Server 2005 or newer servers.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|The databases list is empty.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|Login "%1" does not exist at the source.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|An error occurred while trying to get set the Logins list to transfer: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|User "%1" does not exist at the source.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|An error occurred while trying to get set the Users list to transfer: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|The task can not have a retained connection manager in a transaction.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|Unable to obtain XML data from SQL Server as Unicode because the provider does not support the OUTPUTENCODING property.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|For the FTP operation "%1", the FILE connection manager "%2" can not be found.|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"Logins" are server level objects and can not be dropped first since the source and destination are the same server. Dropping objects first will remove the logins from the source as well.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|Parameter "%1" cannot be negative. (-1) is used for the default value.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Data Flow objects cannot be loaded. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Data Flow objects cannot be saved. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Failed to save Data Flow objects.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Failed to load Data Flow objects|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Failed to save Data Flow objects. The specified format is not supported.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Failed to load Data Flow objects. The specified format is not supported.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Failed to set the XML persistence events property for the Data Flow objects.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Failed to set the persistence XML DOM property for the Data Flow objects.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Failed to set the persistence XML ELEMENT property for the Data Flow objects.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Failed to set xml persistence properties for the Data Flow objects.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Failed to get custom property collection for Data Flow components.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|An execution tree contains a cycle.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|The %1 object "%2" (%3!d!) is disconnected from the layout.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|The ID for the layout object is not valid.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|A required input object is not connected to a path object.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 has an invalid synchronous input ID %2!d!.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 has lineage ID %2!d!, but should have had %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|The package contains two objects with the duplicate name of "%1" and "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|The "%1" and the "%2" are in the same exclusion group, but they do not have the same synchronous input.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Two objects in the same collection have a duplicate lineage ID of %1!d!. The objects are %2 and %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|The layout failed validation.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|One or more component failed validation.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|The layout and one or more components failed validation.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|The Data Flow task engine failed at startup because it cannot create one or more required threads.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|A thread failed to create a mutex at initialization.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|A thread failed to create a semaphore at initialization.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|The system reports %1!d! percent memory load. There are %2 bytes of physical memory with %3 bytes free. There are %4 bytes of virtual memory with %5 bytes free. The paging file has %6 bytes with %7 bytes free.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|A buffer failed while allocating %1!d! bytes.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|The Buffer Manager could not be created.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Buffer Type %1!d! had a size of %2!I64d! bytes.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 is marked as dangling, but has a path attached to it.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 failed validation and returned error code 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 failed the post-execute phase and returned error code 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 failed the prepare phase and returned error code 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 failed the pre-execute phase and returned error code 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 failed the cleanup phase and returned error code 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 has lineage ID %2!d! that was not previously used in the Data Flow task.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|Cannot connect %1 to %2 because a cycle would be created.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|The data type "%1" cannot be compared. Comparison of that data type is not supported, so it cannot be sorted or used as a key.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|This thread has shut down and is not accepting buffers for input.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS Error Code DTS_E_THREADFAILED.  Thread "%1" has exited with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the thread has exited.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS Error Code DTS_E_PROCESSINPUTFAILED.  The ProcessInput method on component "%1" (%2!d!) failed with error code 0x%3!8.8X! while processing input "%4" (%5!d!). The identified component returned an error from the ProcessInput method. The error is specific to the component, but the error is fatal and will cause the Data Flow task to stop running.  There may be error messages posted before this with more information about the failure.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|A set of virtual buffers cannot be realized.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|The number of threads required for this pipeline is %1!d!, which is more than the system limit of %2!d!. The pipeline requires too many threads as configured. There are either too many asynchronous outputs, or EngineThreads property is set too high. Split the pipeline into multiple packages, or reduce the value of the EngineThreads property.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|The Data Flow engine scheduler cannot obtain a count of the sources in the layout.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|The Data Flow engine scheduler cannot obtain a count of the destinations in the layout.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|The component view is unavailable. Make sure the component view has been created.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|The component view ID is incorrect. The component view may be out of synchronization. Try releasing the component view and recreating it.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|This buffer is not locked and cannot be manipulated.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|The Data Flow task cannot allocate memory to build a buffer definition. The buffer definition had %1!d! columns.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|The Data Flow task cannot register a buffer type. The type had %1!d! columns and was for execution tree %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|The UsesDispositions property cannot be changed from its initial value. This occurs when the XML is edited and the UsesDispositions value is modified. This value is set by the component when it is added to the package and is not allowed to change.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|The Data Flow task failed to initialize a required thread and cannot begin execution. The thread previously reported a specific error.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|The Data Flow task failed to create a required thread and cannot begin running. The usually occurs when there is an out-of-memory state.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|The synchronous input of "%1" cannot be set to "%2" because a cycle would be created.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|A custom property named "%1" is invalid because there is a stock property with that name. A custom property cannot have the same name as a stock property on the same object.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|The buffer was already unlocked.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 failed initialization and returned error code 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 failed during shut down and returned error code 0x%2!8.8X!. A component failed to release its interfaces.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS Error Code DTS_E_PRIMEOUTPUTFAILED.  The PrimeOutput method on %1 returned error code 0x%2!8.8X!.  The component returned a failure code when the pipeline engine called PrimeOutput(). The meaning of the failure code is defined by the component, but the error is fatal and the pipeline stopped executing.  There may be error messages posted before this with more information about the failure.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS Error Code DTS_E_THREADCANCELLED.  Thread "%1" received a shutdown signal and is terminating. The user requested a shutdown, or an error in another thread is causing the pipeline to shutdown.  There may be error messages posted before this with more information on why the thread was cancelled.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|Distributor for thread "%1" failed to initialize property "%2" on component "%3" because of error 0x%8.8X. The distributor could not initialize the component's property and cannot continue running.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|The Data Flow task cannot register a view buffer type. The type had %1!d! columns and was for input ID %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|There is not enough memory to create an execution tree.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|There is not enough memory to insert an object into the hash table.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|The object is not in the hash table.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Cannot create a component view because another one already exists. Only one component view can exist at a time.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|At input "%1" (%2!d!), the virtual input column collection does not contain a virtual input column with lineage ID %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|The requested object has the incorrect object type.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|The buffer manager cannot create a temporary storage file on any path in the BufferTempStoragePath property. There is an incorrect file name or no permission or the paths have been full.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|The buffer manager could not seek to offset %1!d! in file "%2". The file is damaged.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|The buffer manager cannot extend the file "%1" to length %2!lu! bytes.  There was insufficient disk space.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|The buffer manager cannot write %1!d! bytes to file "%2". There was insufficient disk space or quota.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|The buffer manager cannot read %1!d! bytes from file "%2". The file is damaged.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|Buffer ID %1!d! supports other virtual buffers and cannot be placed into sequential mode. IDTSBuffer100.SetSequentialMode was called on a buffer that supports virtual buffers.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|This operation could not be performed because buffer is in read-only mode. A read-only buffer cannot be modified.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|ID %1 cannot be set to %2!d! because a cycle would be created.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|The buffer manager ran out of memory while trying to extend the table of buffer types. This is caused by an out-of-memory condition.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|The buffer manager failed to create a new buffer type.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|The Data Flow engine scheduler failed to retrieve the execution tree with index %1!d! from the layout. The scheduler received a count containing more execution trees than actually exist.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|The Data Flow task failed to create a buffer to call PrimeOutput for output "%3" (%4!d!) on component "%1" (%2!d!). This error usually occurs due to an out-of-memory condition.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|The Data Flow engine scheduler failed to create a thread object because not enough memory is available. This is caused by an out-of-memory condition.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|The Data Flow engine scheduler cannot retrieve object with ID %1!d! from the layout. The Data Flow engine scheduler previously located an object that is now no longer available.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|The Data Flow task failed to prepare buffers for the execution tree node beginning at output "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|The Data Flow task cannot create a virtual buffer to prepare for execution.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|The maximum ID has been reached. There are no more IDs available to assign to objects.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|The %1 is already attached and cannot be attached again.  Detach it and try again.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|Column name "%1" on output "%2" cannot be used because it conflicts with a column of the same name on synchronous input "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|The Data Flow task cannot to create a buffer to mark the end of the rowset.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|A managed user component has thrown exception "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|The Data Flow engine scheduler cannot allocate enough memory for the execution structures. The system was low on memory before execution started.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|An out-of-memory condition prevented the creation of the buffer object.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|An out-of-memory condition prevents the mapping of a buffer's lineage IDs to DTP_HCOL indexes.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|The "%1!s!" cannot cache the Variables collection and returned error code 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|The "%1" failed to cache the component metadata object and returned error code 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" has a non-zero SortKeyPosition, but its value (%2!ld!) is too large. It must be less than or equal to the number of columns.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but the absolute values of the non-zero output column SortKeyPositions do not form a monotonically increasing sequence, starting at one.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" failed validation and returned validation status "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|Component "%1!s!" could not be created and returned error code 0x%2!8.8X! "%3!s!". Make sure that the component is registered correctly.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|The module containing "%1" is not registered or installed correctly.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|The module containing "%1" cannot be located, even though it is registered.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|The script component is configured to pre-compile the script, but binary code is not found. Please visit the IDE in Script Component Editor by clicking Design Script button to cause binary code to be generated.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|The buffer manager cannot create a file to spool a long object on the directories named in the BLOBTempStoragePath property.  Either an incorrect file name was provided, or there are no permissions, or the paths have been full.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|The SynchronousInputID property on "%1" was %2!d!, and %3!d! was expected.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|No object exists with the ID %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Unable to locate an object with ID %1!d! because of the error code 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|The code page %1!d! specified on output column "%2" (%3!d!) is not valid. Select a different code page for output column "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|The EventInfos collection could not be cached by "%1" and returned error code 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|The name for "%1" is a duplicate.  All names must be unique.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|There is no output column associated with input column "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" has a virtual buffer extending from a root source. There is an exclusion group that is not zero with a synchronous input that is zero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" cannot be an error output because error outputs cannot be placed on synchronous, non-exclusive outputs.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|A divide-by-zero error occurred. The right side operand evaluates to zero in the expression "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|The literal "%1" is too large to fit into type %2. The magnitude of the literal overflows the type.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|The result of the binary operation "%1" on data types %2 and %3 exceeds the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|The result of the binary operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|The result of the function call "%1" is too large to fit in type "%2". The magnitude of the result of the function call overflows the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|The data types "%1" and "%2" are incompatible for binary operator "%3". The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|The data type "%1" cannot be used with binary operator "%2". The type of one or both of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator "%1" in operation "%2". Both operands for this operator must be positive or negative.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|The binary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or an out-of-memory condition exists.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Attempt to set the result type of binary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Comparing "%1" to string "%2" failed.|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|The data type "%1" cannot be used with unary operator "%2". This operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|The unary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or there is an out-of-memory condition.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Attempt to set the result type of unary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|The function "%1" does not support the data type "%2" for parameter number %3!d!. The type of the parameter could not be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|The function "%1" was not recognized. Either the function name is incorrect or does not exist.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|The length %1!d! is not valid for function "%2". The length parameter cannot be negative. Change the length parameter to zero or a positive value.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|The start index %1!d! is not valid for function "%2". The start index value must be an integer greater than 0. Start index is one-based, not zero-based.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|The function "%1" cannot perform the character mapping on string "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" is not a valid date part for function "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Parameter number %1!d! of the function NULL with data type "%2" is not valid. The parameters of NULL() must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Parameter number %1!d! of the function NULL with data type "%2" is not an integer. A parameter of NULL() must be an integer or a type that can be converted to an integer.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Parameter number %1!d! of the function "%2" is not static. This parameter must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Parameter number %1!d! of the cast to data type "%2" is not valid. The parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Parameter number %1!d! of the cast to data type "%2" is not an integer. A parameter of a cast operator must be an integer or a type that can be converted to an integer.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Cannot cast expression "%1" from data type "%2" to data type "%3". The requested cast is not supported.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Attempt to parse the expression "%1" failed.  The token "%2" at line number "%3", character number "%4" was not recognized. The expression cannot be parsed because it contains invalid elements at the location specified.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|An error occurred when parsing the expression "%1". The expression failed to parse for an unknown reason.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Attempt to parse the expression "%1" failed and returned error code 0x%2!8.8X!. The expression cannot be parsed. It might contain invalid elements or it might not be well-formed. There may also be an out-of-memory error.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|The expression "%1" is not valid and cannot be parsed. The expression may contain invalid elements or it may not be well-formed.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|There was no expression to compute. An attempt was made to compute or get the string of an empty expression.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Attempt to compute the expression "%1" failed with error code 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed with error code 0x%1!8.8X!. Failed when attempting to generate a displayable string that represents the expression.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Cannot convert the expression result data type "%1" to the column data type "%2". The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression "%1" of the conditional operator has an invalid data type of "%2". The conditional expression of the conditional operator must return a Boolean, which is type DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|The data types "%1" and "%2" are incompatible for the conditional operator. The operand types cannot be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Attempt to set the result type of conditional operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|This buffer has been orphaned. The buffer manager has shut down, leaving an outstanding buffer and no cleanup will occur for the buffer. There is a potential for memory leaks and other problems.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Attempt to find the input column named "%1" failed with error code 0x%2!8.8X!. The input column specified was not found in the input column collection.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Attempt to find the input column with lineage ID %1!d! failed with error code 0x%2!8.8X!. The input column was not found in the input column collection.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|The expression contains unrecognized token "%1". If "%1" is a variable, it should be expressed as "\@%1". The specified token is not valid. If the token is intended to be a variable name, it should be prefixed with the \@ symbol.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|The expression contains unrecognized token "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|The variable "%1" was not found in the Variables collection. The variable might not exist in the correct scope.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Attempt to parse the expression "%1" failed. The expression might contain an invalid token, an incomplete token, or an invalid element. It might not be well-formed, or might be missing part of a required element such as a parenthesis.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|The name for "%1" is blank, and names cannot be blank.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|The "%1" has the HasSideEffects property set to TRUE, but "%1" is synchronous and cannot have side effects. Set the HasSideEffects property to FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|The value, %1!d!, specified for the code page parameter of the cast to data type "%2", is not valid. The code page is not installed on the machine.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|The value %1!d! specified for the precision parameter of the cast to data type "%2" is not valid. Precision must be in the range %3!d! to %4!d! and the precision value is out of range for the type cast.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|The value %1!d! specified for the scale parameter of the cast to data type "%2" is not valid. The scale must be in the range %3!d! to %4!d! and the scale value is out of range for the type cast. Scale must not exceed precision and must be positive.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|The IsSorted property for "%1" is false, but %2!lu! of its output columns' SortKeyPositions are non-zero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|The code pages must match for operands of conditional operation "%1" for type %2. The code page of the left operand does not match the code page of the right operand. For the conditional operator on the specified type, the code pages must be the same.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|Input "%1" (%2!d!) references input "%3" (%4!d!), but they do not have the same number of columns. Input %5!d! has %6!d! columns, while input %7!d! has %8!d! columns.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|No object exists with a lineage ID of %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|The output column for the file name cannot be found.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|The output column for the file name is not a null-terminated Unicode character string, which is data type DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|A distributor failed to give a buffer to thread "%1" because of error 0x%2!8.8X!. The target thread is probably shutting down.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|The LocaleID %1!ld! is not installed on this system.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal hexadecimal escape sequence of  "\x%2". The escape sequence is not supported in string literals in the expression evaluator. The hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal escape sequence of "\\%2!c!". The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, use a double backslash, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" contains no output columns. An asynchronous output must contain output columns.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|The "%1" has a long object data type of DT_TEXT, DT_NTEXT, or DT_IMAGE, which is not supported.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Output ID %1!d! was given multiple error output configurations. First %2!d! and %3!d!, then %4!d! and %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|The OLE DB provider failed during the data type conversion verification for "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|This buffer represents the end of the rowset and its row count cannot be altered.  An attempt was made to call AddRow or RemoveRow on a buffer that has the end of rowset flag.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|The data type "%1" is not supported in an expression. The specified type is not supported or is not valid.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|The PrimeOutput method on "%1" returned success, but did not report an end of the rowset. There is an error in the component. It should have reported an end-of-row. The pipeline will shut down execution to avoid unpredictable results.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|An overflow occurred while converting from data type "%1" to data type "%2". The source type is too large for the destination type.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|Conversion from data type "%1" to data type "%2" is unsupported. The source type cannot be converted to the destination type.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Error code 0x%1!8.8X! occurred attempting to convert from data type %2 to data type %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|The conditional operation "%1" failed with error code 0x%2!8.8X!. There was an internal error or an out-of-memory error.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Casting expression "%1" from data type "%2" to data type "%3" failed with error code 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Evaluating function "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Parameter number %1!d! of the function "%2" cannot be converted to a static value.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|The error row disposition on "%1" cannot be set to redirect the row when the fast load option is turned on, and the maximum insert commit size is set to zero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|The code pages for operands of binary operator "%1" for type "%2" must match. Currently, the code page of the left operand does not match the code page of the right operand. For the specified binary operator on the specified type, the code pages must be the same.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Retrieving the value of Variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|The data type of variable "%1" is not supported in an expression.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Unable to cast expression "%1" from data type "%2" to data type "%3" because the code page of the value being cast (%4!d!) does not match the requested result code page (%5!d!). The code page of the source must match the code page requested for the destination.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|The default buffer size must be between %1!d! and %2!d! bytes. An attempt was made to set the DefaultBufferSize property to a value that is too small or too large.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|The default buffer maximum rows must be larger than %1!d! rows. An attempt was made to set the DefaultBufferMaxRows property to a value that is too small.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|The code page on %1 is %2!d! and is required to be %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Failed to assign %3!d! to the EngineThreads property of the Data Flow task. The value must be between %1!d! and %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Parsing the expression "%1" failed. The single quotation mark at line number "%2", character number "%3", was not expected.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Parsing the expression "%1" failed. The equal sign (=) at line number "%2", character number "%3", was not expected. A double equals sign (==) may be required at the location specified.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|Component "%1" failed to cache the runtime object reference tracker collection and returned error code 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|There are multiple input columns with the name "%1". The desired input column must be specified uniquely as [Component Name].[%2] or referenced by lineage ID. Currently, the input column specified exists on more than one component.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Locating the input column named "[%1].[%2]" failed with error code 0x%3!8.8X!. The input column was not found in the input column collection.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|There are multiple variables with the name "%1". The desired variable must be specified uniquely as \@[Namespace::%2]. The variable exists in more than one namespace.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|The Data Flow engine scheduler failed to reduce the execution plan for the pipeline. Set the OptimizedMode property to false.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|The function SQRT cannot operate on negative values, and a negative value was passed to the SQRT function.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|The function LN cannot operate on zero or negative values, and a zero or negative value was passed to the LN function.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|The function LOG cannot operate on zero or negative values, and a zero or negative value was passed to the LOG function.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|The parameters passed to the function POWER cannot be evaluated and yield an indeterminate result.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|The runtime cannot provide a cancel event because of error 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|The pipeline received a request to cancel and is shutting down.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|The result of the unary minus (negation) operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|The placeholder "%1" was found in an expression. This must be replaced with an actual parameter or operand.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|The length %1!d! specified for function "%2" is negative, and is not valid. The length parameter must be positive.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|The repeat count %1!d! is negative and is not valid for function "%2". The repeat count parameter cannot be negative.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Reading the variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|For operands of a binary operation, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used in a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count %1!d! is not valid for function "%2". This parameter must be greater than zero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" failed to cache the LogEntryInfos collection and returned error code 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|The date part parameter specified for function "%1" is not valid. It must be a static string.  The date part parameter cannot contain dynamic elements, such as input columns, and must be of type DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|The value %1!d! specified for the length parameter of the cast to data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|The value %1!d! specified for the code page parameter of the NULL function with data type "%2" is not valid. The code page is not installed on the computer.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|The value %1!d! specified for the precision parameter of the NULL function with data type "%2" is out of range. Precision must be in the range %3!d! to %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|The value %1!d! specified for the scale parameter of the NULL function with data type %2 is out of range. Scale must be in the range %3!d! to %4!d!. Scale must not exceed precision and must not be negative.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|The value %1!d! specified for the length parameter of the "NULL" function with data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|The %1 can't be assigned a negative value.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|The "%1" custom property for "%2" cannot be set to true.  The column data type must be one of the following:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2, or DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|The "%1" cannot be reattached. Delete the path, add a new one, and attach it.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|The function "%1" requires %2!d! parameters, not %3!d! parameter. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|The function "%1" requires %2!d! parameter, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|The function "%1" requires %2!d! parameters, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Attempt to parse the expression "%1" failed because there was an out-of-memory error.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|The %1 failed to be able to perform its required product level check and returned error code 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS Error Code DTS_E_PRODUCTLEVELTOLOW.  The %1 cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|A string literal in the expression exceeds the maximum allowed length of %1!d! characters.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|The variable %1 contains a string that exceeds the maximum allowed length of %2!d! characters.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|The %1 was found, but it does not support a required Integration Services interface (IDTSRuntimeComponent100).  Obtain an updated version of this component from the component provider.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|The registry key "%1" cannot be opened.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Cannot get the file name for the component with a CLSID of "%1". Verify that the component is registered properly or that the CLSID provided is correct.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|The CLSID for one of the components is not valid. Verify that all the components in the pipeline have valid CLSIDs.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|The CLSID for one of the components with ID %1!d! is not valid.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|The index is not valid.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|The Application object cannot be accessed. Verify that SSIS is correctly installed.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Retrieving the file name for a component failed with error code 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Cannot retrieve property "%1" from component with ID %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Attempting to use ID %1!d! more than once in the Data Flow Task.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Cannot retrieve an item by lineage ID from a collection that does not contain columns.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Cannot find the connection manager with ID "%1" in the connection manager collection due to error code 0x%2!8.8X!. That connection manager is needed by "%3" in the connection manager collection of "%4". Verify that a connection manager in the connection manager collection, Connections, has been created with that ID.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|Thread "%1" received a buffer for input %2!d!, but this thread is not responsible for that input. An error occurred, causing the Data Flow engine scheduler to build a bad execution plan.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|The component "%1" (%2!d!) cannot provide an IDTSRuntimeComponent100 interface.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|The Data Flow task engine attempted to copy a buffer to assign another thread, but failed.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|The Data Flow task engine failed to create a view buffer of type %1!d! over type %2!d! for buffer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|The buffer manager attempted to push an error row to an output that was not registered as an error output. There was a call to DirectErrorRow on an output that does not have the IsErrorOut property set to TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|A call was made to a buffer method on a private buffer and private buffers do not support this operation.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Private mode buffers do not support this operation.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|This operation cannot be called on a buffer passed to PrimeOutput. A call was made to a buffer method during PrimeOutput, but that call is not allowed during PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|This operation cannot be called on a buffer passed to ProcessInput. A call was made to a buffer method during ProcessInput, but that call is not allowed during ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|The code encountered a column that was too wide.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Cannot get the ID of the runtime connection manager specified by "%1" in the connection manager collection, Connections, of "%2" due to error code 0x%3!8.8X!. Verify that the ConnectionManager.ID property of the runtime connection object has been set for the component.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|The "%1" in the connection manager collection, Connections, of "%2" does not have a value for the ID property. Verify that the ConnectionManagerID property of the runtime connection object has been set for the component.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Metadata cannot be changed during execution.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|The component metadata for "%1" could not be upgraded to the newer version of the component. The PerformUpgrade method failed.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|The version of %1 is not compatible with this version of the DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|The component is missing, not registered, not upgradeable, or missing required interfaces. The contact information for this component is "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|The method was called on the wrong buffer. Buffers that are not used for component output do not support this operation.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|An error occurred during computation of the expression.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Division by zero occurred in the expression.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|The magnitude of the literal value was too big to fit in the type requested.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|The result of a binary operation was too big for the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|The magnitude of the result of a binary operation overflows the maximum size for result data type.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|The magnitude of the result of a function call was too big to fit in the result type, and overflowed the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Incompatible data types were used with a binary operator. The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|An unsupported data type was used with a binary operator. The type of one, or both, of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator. The operands for this operator must be both positive or both negative.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|A binary operation failed. There was an out-of-memory condition, or an internal error occurred.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Setting the result type of a binary operation failed.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Cannot compare two strings.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|An unsupported data type is used with a unary operator. The operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|A unary operation failed. An out-of-memory condition occurred, or there was an internal error.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Setting the result type of a unary operation failed.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|A function has a parameter with an unsupported data type. The type of the parameter cannot be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|An invalid function name appeared in the expression. Verify that the function name is correct and does exist.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|The length parameter was not valid for function SUBSTRING. The length parameter cannot be negative.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|The start index was not valid for function SUBSTRING. The start index value must be an integer greater than zero. The start index is 1-based, not 0-based.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|An incorrect number of parameters was given to a function. The function name was recognized, but the number of parameters was not correct.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|A character mapping function failed.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|An unrecognized date part parameter was specified for a date function.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|An invalid parameter was given for function NULL. The parameters of NULL must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|An invalid parameter was given for function NULL. A parameter of NULL must be an integer, or a type that can be converted to an integer.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|An invalid parameter was given for a function. This parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|An invalid parameter was given for a cast operation. Parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|An invalid parameter was given for a cast operation. A parameter of a cast operator must be an integer, or a type that can be converted to an integer.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|The expression contained an unsupported type cast.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|The expression contained a token that was not recognized. The expression could not be parsed because it contains invalid elements.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|The expression is not valid and could not be parsed. It might contain invalid elements, or it might not be well-formed.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|The result of a unary minus (negation) operation overflowed the maximum size for result data type. The magnitude of the result of the operation overflows the type of the result.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Attempt to compute the expression failed.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Cannot convert the expression result data type to the column data type. The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression of the conditional operator has invalid data type. The conditional expression must be of type DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|The data types of the operands of the conditional operator were incompatible. The operand types could not be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Setting the result type of a conditional operation failed.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|The input column specified was not found in the input column collection.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Attempt to find an input column by lineage ID failed. The input column was not found in the input column collection.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|The expression contains an unrecognized token that appears to be an input column reference, but the input column collection is not available to process input columns. The input column collection has not been provided to the expression evaluator, but an input column was included in the expression.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|A variable specified was not found in the collection. It might not exist in the correct scope. Verify that the variable exists and that the scope is correct.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Attempt to parse the expression failed. The expression contains an invalid or incomplete token. It may contain invalid elements, be missing part of a required element such as closing parentheses, or may not be well formed.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|The value specified for the code page parameter of the cast to data type DT_STR or DT_TEXT is not valid. The specified code page is not installed on the computer.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|The value specified for the precision parameter of a cast operation is out of range for the type cast.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|The value specified for the scale parameter of a cast operation is out of range for the type cast. Scale must not exceed precision and must not be negative.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|The code pages do not match in a conditional operation. The code page of the left operand does not match the code page of the right operand. For the conditional operator of that type, the code pages must be the same.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|A string literal contains an illegal hexadecimal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. Hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|The string literal contains an illegal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, format it as a double backslash, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|An unsupported or unrecognized data type was used in the expression.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|An overflow occurred while converting between data types. The source type is too large to fit in the destination type.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|The expression contains an unsupported data type conversion. The source type cannot be converted to the destination type.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|An error occurred while attempting to perform data conversion. The source type could not be converted to the destination type.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|The conditional operation failed.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|An error occurred while attempting to perform a type cast.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting "%1" from type DT_STR to type DT_WSTR failed with error code 0x%2!8.8X!. An error occurred while performing the implicit conversion on the input column.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting an input column from type DT_STR to type DT_WSTR failed. An error occurred while performing the  implicit conversion on the input column.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|An error occurred while evaluating the function.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|A function parameter cannot be converted to a static value. The parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|The length parameter is not valid for function RIGHT. The length parameter cannot be negative.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|The repeat count parameter is not valid for function REPLICATE. This parameter cannot be negative.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|The code pages do not match in a binary operation. The code page of the left operand does not match the code page of the right operand. For this binary operation, the code pages must be the same.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Retrieving the value for a variable failed.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|The expression contains a variable with an unsupported data type.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Unable to cast the expression because the code page of the value being cast does not match the requested result code page. The code page of the source must match the code page requested for the destination.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|The expression contains an unexpected single quotation mark. A double quotation mark may be required.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|The expression contains an unexpected equal sign (=). This error usually occurs when a double equals sign (==) is needed.|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|An ambiguous input column name was specified.  The column must be qualified as [Component Name].[Column Name] or referenced by lineage ID. This error occurs when the input column exists on more than one component, and must be differentiated by the addition of component name or by using the lineage ID.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|A placeholder function parameter or operand was found in an expression. This should be replaced with an actual parameter or operand.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|An ambiguous variable name was specified. The desired variable must be qualifed as \@[Namespace::Variable]. This error occurs when the variable exists in more than one namespace.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|For operands of binary operation, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count parameter is not valid for function FINDSTRING. This parameter must be greater than zero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|The "date part" parameter specified for a date function is not valid. "Date part" parameters must be static strings, and cannot contain dynamic elements such as input columns. They must be of type DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|The value specified for the length parameter of a cast operation is not valid. The length must be positive. The length specified for the type cast is negative. Change to a positive value.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|The value specified for the length parameter of a NULL function is not valid. The length must be positive. The length specified for the NULL function is negative. Change to a positive value.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|The value specified for the code page parameter of the NULL function with data type DT_STR or DT_TEXT is not valid. The code page specified is not installed on the computer. Either change the code page that is specified, or install the code page on the computer.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|The value specified for the precision parameter of a NULL function is not valid. The precision that was specified is out of range for the NULL function.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|The value specified for the scale parameter of a NULL function is not valid. The scale that was specified is out of range for the NULL function. Scale must not exceed precision and must be positive.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|The %1 failed attempting to write data to %2 on %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|Lookup transform has received a cancel request from the user.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|Processing of character or binary large object (LOB) data has stopped because the 4-GB limit was reached.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|The managed pipeline component "%1" could not be loaded.  The exception was: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS Error Code DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: The Excel Connection Manager is not supported in the 64-bit version of SSIS, as no OLE DB provider is available.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|The cache file is damaged, or the file was not created by using the Cache connection manager.  Provide a valid cache file.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|The SQL command has not been set correctly. Check SQLCommand property.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|COM error object information is available.  Source: "%1"  error code: 0x%2!8.8X!  Description: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Unable to access the acquired connections.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|The number of columns is incorrect.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Column "%1" cannot be found at the datasource.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|An OLE DB record is available.  Source: "%1"  Hresult: 0x%2!8.8X!  Description: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS Error Code DTS_E_OLEDBERROR.  An OLE DB error has occurred. Error code: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|Component is already connected. The component needs to be disconnected before attempting to connect it.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|The value of the property "%1" is incorrect.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Cannot open the datafile "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|No destination flat file name was provided. Make sure the flat file connection manager is configured with a connection string. If the flat file connection manager is used by multiple components, ensure that the connection string contains enough file names.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|The text qualifier for column "%1" cannot be found.|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|Conversion from "%1" to "%2" is not supported.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|The error code 0x%1!8.8X! was returned when validating type conversion from %2 to %3.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Cannot find input column with lineage ID "%1!d!" which is needed by "%2". Check SourceInputColumnLineageID custom property of the output column.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be at least %1!d! outputs.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be exactly %1!d! output(s).|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|A string was too long to be converted.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|The number of inputs is incorrect. There must be exactly %1!d! inputs.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|The number of input columns for %1 cannot be zero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|This component has %1!d! inputs.  No input is allowed on this component.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput was called with an invalid input ID of %1!d!.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|The custom property "%1" needs to be of type %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|The buffer type is not valid. Make sure the Pipeline layout and all components pass validation.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|The value for custom property "%1" is incorrect.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|An error occurred due to no connection. A connection is required when requesting metadata. If you are working offline, uncheck Work Offline on the SSIS menu to enable the connection.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|The custom property "%1" cannot be created.|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|The custom property collection cannot be retrieved for initialization.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Cannot create an OLE DB accessor. Verify that the column metadata is valid.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput was called with an invalid output ID of %1!d!.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|The value for property "%1" on "%2" is not valid.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|A connection is required to read data.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|An error occurred while reading header rows.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Duplicate column name "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Cannot get the name of the column with ID %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Direct row to output "%1" (%2!d!) failed.|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Cannot create the bulk insert thread due to error "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|The thread for the SSIS Bulk Insert task failed initialization.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|The thread for the SSIS Bulk Insert task is already running.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|The thread for the SSIS Bulk Insert task terminated with errors or warnings.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Failed to open a fastload rowset for "%1". Check that the object exists in the database.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Error due to no connection. A connection is required before metadata validation can proceed.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|A destination table name has not been provided.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|The OLE DB provider used by the OLE DB adapter does not support IConvertType. Set the adapter's ValidateColumnMetaData property to FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|The OLE DB provider used by the OLE DB adapter cannot convert between types "%1" and "%2" for "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Column metadata validation failed.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" is a row ID column and cannot be included in a data insertion operation.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Attempting insertion into the row version column "%1". Cannot insert into a row version column.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Failure inserting into the read-only column "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Unable to retrieve column information from the data source. Make sure your target table in the database is available.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|A buffer could not be locked. The system is out of memory or the buffer manager has reached its quota.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|The %1 has a ComparisonFlags property that includes extra flags with the value %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|The column metadata was unavailable for validation.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|Cannot write to the data file.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|The column delimiter for column "%1" was not found.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Failed to parse the column "%1" in the data file.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|The file name is not properly specified.  Supply the path and name to the raw file either directly in the FileName property or by specifying a variable in the FileNameVariable property.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|File "%1" cannot be opened for writing. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|An I/O buffer cannot be created for the output file. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|Cannot write %1!d! bytes to file "%2". See previous error messages for details.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Encountered bad metadata in file header. The file is damaged or not a SSIS-produced raw data file.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Error occurred because the output file already exists and the WriteOption is set to Create Once. Set the WriteOption property to Create Always, or delete the file.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Error caused by conflicting property settings. Both the AllowAppend property and the ForceTruncate property are set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|The file had bad version and flags information. The file is damaged or not a SSIS-produced raw data file.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|The output file was written by an incompatible version and cannot be appended. The file may be an older file format that is no longer useable.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Cannot append output file because no column in the existing file matches column "%1" from the input. Old file does not match in metadata.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Cannot append output file because the number of columns in the output file does not match the number of columns in this destination. The old file does not match in metadata.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|There was an error retrieving column code page information.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Cannot read %1!d! bytes from file "%2". The cause of the failure should have been previously reported.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Unexpected end-of-file encountered while reading %1!d! bytes from file "%2". The file ended prematurely because of an invalid file format.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|The column %1 cannot be used. The raw adapters do not support image, text, or ntext data.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|The adapter encountered an unrecognized data type of %1!d!. This could be caused by a damaged input file (source) or by an invalid buffer type (destination).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|String too long. The adapter read a string that was %1!d! bytes long, and expected a string no longer than %2!d! bytes, at offset %3!d!. This could indicate a damaged input file. The file shows a string length that is too large for the buffer column.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|The raw adapter attempted to skip %1!d! bytes in the input file for unreferenced column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|The raw adapter attempted to read %1!d! bytes in the input file for column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|The file name property is not valid. The file name is a device or contains invalid characters.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Unable to prepare the SSIS bulk insert for data insertion.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|Database object name "%1" is not valid.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Order clause is not valid.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|File "%1" cannot be opened for reading. Error may occur when there are no privileges or the file is not found. Exact cause is reported in previous error message.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Unable to create the Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Unable to configure the Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Unsupported datatype for column %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|The attempt to read from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|The attempt to read column "%2!d!" data from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%2!8.8X!.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|The VariableName property is not set to the name of a valid variable. Need a runtime variable name to write to.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Unable to create or configure the ADODB.Recordset object.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Error writing to the ADODB.Recordset object.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|The file name is not valid. The file name is a device or contains invalid characters.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|The file name "%1" is not valid. The file name is a device or contains invalid characters.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Unable to retrieve destination column descriptions from the parameters of the SQL command.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Parameters are not bound. All parameters in the SQL command must be bound to input columns.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|The PivotUsage value for the input column "%1" (%2!d!) is not valid.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys found. Only one input column can be used as the Pivot Key.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|No Pivot Key found. One input column must be used as the Pivot Key.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|More than one output column (such as "%1" (%2!d!)) is mapped to input column "%3" (%4!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Output column "%1" (%2!d!) cannot be mapped to PivotKey input column.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|Output column "%1" (%2!d!) has a SourceColumn %3!d! that is not a valid input column lineage ID.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column, but its PivotKeyValue property value is missing.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column with a non-unique PivotKeyValue property value.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|Input column "%1" (%2!d!) is not mapped to any output column.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Failure occurred while comparing values for the set keys.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|The Input column "%1" (%2!d!) cannot be used as a Set Key, Pivot Key, or Pivot Value because it contains long data.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Incorrect output type. The output column "%1" (%2!d!) must have the same data type and metadata as the input column to which it is mapped.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Failure when trying to pivot the source records.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|The pivot key value "%1" is not valid.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|An error occurred while skipping data rows.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|An error occurred while processing file "%1" on data row %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|An error occurred while initializing the flat file parser.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Unable to retrieve column information from the flat file connection manager.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Failed to write out column name for column "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|The column type for column "%1" is incorrect. It is type "%2". It can only be either "%3" or "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|The attempt to write data of %1!d! bytes into the disk I/O failed. The disk I/O buffer has %2!d! free bytes.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|An error occurred while writing out the file header.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|An error occurred while getting the file size for file "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|An error occurred while setting the file pointer for file "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|An error occurred while setting up the disk I/O buffer.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|The column data for column "%1" overflowed the disk I/O buffer.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|An unexpected disk I/O error occurred while reading the file.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|An disk I/O time out occurred while reading the file.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|The Usage Type specified for the input columns to this transform cannot be read/write. Change the Usage Type to be read-only.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Cannot copy or convert flat file data for column "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Data conversion failed. The data conversion for column "%1" returned status value %2!d! and status text "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|The Variables collection is not available.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|Duplicate PivotKeyValue. Input column "%1" (%2!d!) is mapped to a Pivoted Value output column and has a non-unique PivotKeyValue.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|No unpivot destination found. At least one input column must be mapped with a PivotKeyValue to an DestinationColumn in the output.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue is not valid. In an UnPivot transform with more than one unpivoted DestinationColumn, the set of PivotKeyValues per destination must match exactly.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Incorrect UnPivot metadata. In an UnPivot transform, all input columns with a PivotKeyValue that is set, and are pointing to the same DestinationColumn, must have metadata that exactly matches the DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Cannot convert the pivot key value "%1" to the data type of the pivot key column.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys specified. Only one output column can be used as the Pivot Key.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|Output column "%1" (%2!d!) is not mapped by any input column's DestinationColumn property.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|No output column is marked as the PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|Input column "%1" (%2!d!) has a DestinationColumn property value that does not refer to a valid output column LineageID.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Duplicate destination error. More than one non-pivoted input column is mapped to the same destination output column.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|No input columns found. At least one input column must be mapped to an output column.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|The number of input and output columns are not equal. The total number of input columns on all inputs must be the same as the total number of output columns.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|The input is not sorted. The "%1" must be sorted.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|The JoinType custom property for the %1 contains a value of %2!ld!, which is not valid. Valid values are 0 (full), 1 (left), or 2 (inner).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|The NumKeyColumns value is not valid. In the %1, the value for the NumKeyColumns custom property must be between 1 and %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|No key columns are found. The %1 must have at least one column with a SortKeyPosition that is non-zero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Not enough key columns. The %1 must have at least %2!ld! columns with non-zero SortKeyPosition values.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Datatype mismatch occurred. The datatypes for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|The column with the SortKeyPosition value of %1!ld! is not valid. It should be %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Sort direction mismatch. The sort directions for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Missing column. The %1 must have an associated input column.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Input columns must have output columns. There are input columns with a usage type of read-only that do not have associated output columns.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags are not zero. The comparison flags for non-string columns must be zero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|The comparison flags for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Unrecognized pivot key value.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|Lineage item value %1!ld! is not valid. The valid range is between %2!ld! and %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Input columns not allowed. The number of input columns must be zero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|The datatype for "%1" is not valid for the specified lineage item.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|The length for "%1" is not valid for the specified lineage item.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|The metadata for "%1" does not match the metadata for the associated output column.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|There are output columns that have SortKeyPosition values that don't match the associated input columns' SortKeyPosition.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|The attempt to add a row to the Data Flow task buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Data conversion failed while converting column "%1" (%2!d!) to column "%3" (%4!d!).  The conversion returned status value %5!d! and status text "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|The attempt to allocate a row handle buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|The attempt to send a row to SQL Server failed with error code 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|The attempt to prepare the buffer status failed with error code 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|The attempt to retrieve the start of the buffer row failed with error code 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|The thread for the SSIS Bulk Insert is no longer running.  No more rows can be inserted. Try increasing the bulk insert thread timeout.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|The source file is not valid. The source file is returning a count of more than 131,072 columns. This usually occurs when the source file is not produced by the raw file destination.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|The %1 is an extra unattached input and will be removed.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|The %1 is not attached but is not marked as dangling.  It will be marked as dangling.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Duplicate pivot key value "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Duplicate pivot key value.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Failure retrieving component locale ID. Error code 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Mismatched locale IDs. The component locale ID (%1!d!) does not match the connection manager locale ID (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|The component locale ID has not been set. Flat file adapters need to have the locale ID on the flat file connection manager set.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|The binary field is too large. The adapter attempted to read a binary field that was %1!d! bytes long, but expected a field no longer than %2!d! bytes at offset %3!d!. This usually occurs when the input file is not valid. The file contains a string length that is too large for the buffer column.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|The percentage, %2!ld!, is not valid for the "%1" property. It must be between 0 and 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|The number of rows, %2!ld!, is not valid for the "%1" property. It must be greater than 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|The adapter was asked to write a string that was %1!I64d! bytes long, but all data must be less than 4294967295 bytes in length.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|No inputs were mapped to an output. The "%1" must have at least one input column mapped to an output column.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|Conversion from "%1" with code page %2!d! to "%3" with code page %4!d! is not supported.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|The external metadata column mapping for %1 is not valid.  The external metadata column ID cannot be zero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|The %1 is mapped to an external metadata column that does not exist.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Writing long object data of type DT_TEXT, DT_NTEXT, or DT_IMAGE to Data Flow task buffer failed for column "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Opening a rowset for "%1" failed. Check that the object exists in the database.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Accessing variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|The connection manager "%1" is not found. A component failed to find the connection manager in the Connections collection.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|The upgrade from version "%1" to version %2!d! failed.|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|A value in an input column is too large to be stored in the ADODB.Recordset object.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Columns "%1" and "%2" cannot convert between unicode and non-unicode string data types.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|The variable "%1" specified by VariableName property is not a valid variable. Need a valid variable name to write to.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|The variable "%1" specified by VariableName property is not an integer. Change the variable to be of type VT_I4, VT_UI4, VT_I8, or VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|No column was specified to allow the component to advance through the file.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|The "%1" has IsSorted set to TRUE, but the SortKeyPosition on all output columns are zero. Either change the IsSorted to FALSE, or select at least one output column to contain a non-zero SortKeyPosition.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|The "%1" metadata does not match the metadata of the input column.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|The value of the specified variable cannot be located, locked, or set.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|The column "%1" cannot be processed because more than one code page (%2!d! and %3!d!) are specified for it.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|The column "%1" can't be inserted because the conversion between types %2 and %3 is not supported.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Column "%1" cannot convert between unicode and non-unicode string data types.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|The %1 cannot find the column with LineageID %2!ld! in its input buffer.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|The %1 cannot get the column information for column %2!lu! from its input buffer.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|The %1 cannot get the column information for column "%2!lu!" from its copy buffer.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|The %1 cannot register a buffer type for its copy buffer.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|The %1 cannot create a buffer to copy its data into for sorting.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader client has failed to call Read or has closed the DataReader.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|No column information was returned by the SQL command.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|The %1 was unable to retrieve column information for the SQL command. The following error occurred: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|A source table name has not been provided.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|The cache index position, %1!d!, is not valid. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|The index position, %1!d!, is a duplicate. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|At least one index column should be specified for the Cache connection manager. To specify an index column, set the Index Position property of the cache column.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Cache index positions must be contiguous. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|The property "%1" cannot be set on "%2". The property being set is not supported on the specified object. Check the property name, case, and spelling.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|The property type cannot be changed from the type that was set by the component.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Output ID %1!d! failed during insert. The new output was not created.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Cannot delete output ID %1!d! from the output collection.  The ID may not be valid, or the ID may have been the default or error output.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Failed to set property "%1" on "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Failed to set the type of %1 to type: "%2", length: %3!d!, precision: %4!d!, scale: %5!d!, codepage: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|More than one error output was found on the component, and there can be only one.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|The property on an output column cannot be set.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|The data type for "%1" cannot be modified in the error "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|The "%1" cannot have its IsSorted property set to TRUE because it is not a source output. A source output has a SynchronousInputID value of zero.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|The "%1" cannot have a SortKeyPosition property set to non-zero because "%2" is not a source output. The output column "colname" (ID) cannot have its SortKeyPosition property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|The ComparisonFlags property cannot be set to a non-zero value for "%1" because the "%2" is not a source output. The output column "colname" (ID) cannot have a ComparisonFlags property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags for "%1" must be zero because its type is not a string type. ComparisonFlags can only be non-zero for string type columns.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|The "%1" cannot have a ComparisonFlags property set to non-zero because its SortKeyPosition is set to zero. An output column's ComparisonFlags can only be non-zero if its SortKeyPosition is also non-zero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|The property is read-only.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|The %1 had an invalid datatype value (%2!ld!) set.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|The "%1" requires a code page to be set but the value passed was zero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|The "%1" has a length that is not valid. The length must be between %2!ld! and %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|The "%1" has a scale that is not valid. The scale must be between %2!ld! and %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|The "%1" has a precision that is not valid. The precision must be between %2!ld! and %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|The "%1" has a value set for length, precision, scale, or code page that is a value other than zero, but the data type requires the value to be zero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|The %1 does not allow setting output column datatype properties.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|The "%1" contains an invalid data type. "%1 " is a special error column,  and the only valid data type is DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|The component does not supply error code descriptions.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|The specified error code is not associated with this component.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|A truncation caused a row to be redirected, based on the truncation disposition settings.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|The "%1" is unable to make the column with lineage ID %2!d! read/write because that usage type is not allowed on this column. An attempt was made to change the usage type of an input column to a type, UT_READWRITE, that is not supported on this component.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|The %1 has forbidden the requested use of the input column with lineage ID %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|The "%1" was unable to make the requested change to the input column with lineage ID %2!d!. The request failed with error code 0x%3!8.8X!. The specified error occurred while attempting to set the usage type of an input column.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Attempt to set the data type properties on "%1" failed with error code 0x%2!8.8X!. The error occurred while attempting to set one or more of the data type properties of the output column.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|The metadata for "%1" cannot be retrieved. Make sure the object name is correct and the object exists.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|The output column cannot be mapped to an external metadata column.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|The variable %1 is required to be of type "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|The %1 does not allow setting external metadata column datatype properties.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|The ID, %1!lu!, is neither an input ID nor an output ID. The specified ID must be the input ID or the output ID that the external metadata collection is associated with.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|The external metadata collection on "%1" is marked as not used, so no operations can be performed on it.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|The %1 is a synchronous output and the buffer type cannot be retrieved for a synchronous output.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|The input column "%1" must be read-only. The input column has a usage type other than read-only, which is not allowed.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|The "%1" is missing the required property "%2". The object is required to have the specified custom property.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|The output %1 cannot not have property "%2", but currently has that property assigned.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|The %1 must be in exclusion group %2!d!. All outputs must be in the specified exclusion group.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|The property "%1" is empty. The property cannot be empty.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|Memory cannot be allocated for the expression "%1". There was an out-of-memory error while creating an internal object to hold the expression.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Cannot parse the expression "%1". The expression was not valid, or there is an out-of-memory error.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Computing the expression "%1" failed with error code 0x%2!8.8X!. The expression may have errors, such as divide by zero, that cannot be detected at parse time, or there may be an out-of-memory error.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Memory cannot be allocated for the Expression objects. An out-of-memory error occurred while creating the array of Expression object pointers.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|The %1 failed with error code 0x%2!8.8X! while creating the Expression Manager.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|The expression "%1" is not Boolean. The result type of the expression must be Boolean.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|The expression "%1" on "%2" is not valid.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|The column "%1" (%2!d!) cannot be matched to any input file column. The output column name or input column name cannot be found in the file.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Attempting to set the result column for the expression "%1" on %2 failed with error code 0x%3!8.8X!. The input or output column that was to receive the result of the expression cannot be determined, or the expression result cannot be cast to the column type.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|The %1 failed to get the locale ID from the package.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|The parameter mapping string is not in the correct format.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|The SQL command requires %1!d! parameters, but the parameter mapping only has %2!d! parameters.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|The SQL command requires a parameter named "%1", which is not found in the parameter mapping.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|There is more than one data source column with the name "%1".  The data source column names must be unique.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|There is a data source column with no name.  Each data source column must have a name.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|A component is disconnected from the layout.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|The ID for a layout component is not valid.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|A component has an invalid number of inputs.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|A component has an invalid number of outputs.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|A component does not have any inputs or outputs.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|Not enough memory was available to allocate a list of the columns that are being manipulated by this component.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|Output column "%1" (%2!d!) references input column with lineage ID %3!d!, but no input could be found with that lineage ID.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|At least one input column must be marked as a sort key, but no keys were found.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Both column "%1" (%2!d!) and column "%3" (%4!d!) were marked with sort key weight %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|The component cannot perform the requested metadata change until the validation problem is fixed.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|An input cannot be added to the inputs collection.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|An output cannot be added to the outputs collection.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|An input cannot be deleted from the inputs collection.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|An output cannot be removed from the outputs collection.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|The usage type of the column cannot be changed.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|The %1 must be read/write to have custom property "%2". The input or output column has the specified custom property, but is not read/write. Remove the property, or make the column read/write.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|The %1 is read/write and is required to have custom property "%2". Add the property, or make remove the read/write attribute from the column.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|The column cannot be deleted. The component does not allow columns to be deleted from this input or output.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|The component does not allow adding columns to this input or output.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|The connection "%1" cannot be found. Verify that the connection manager has a connection with that name.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|The runtime connection manager with the ID "%1" cannot be found. Verify that the connection manager collection has a connection manager with that ID.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS Error Code DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  The AcquireConnection method call to the connection manager "%1" failed with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the AcquireConnection method call failed.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|The connection acquired from the connection manager "%1" is not valid.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" is an incorrect type.  The type required is "%2". The type available to the component is "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Cannot acquire a managed connection from the run-time connection manager.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|An input cannot be created to initialize the inputs collection.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|An output cannot be created to initialize the outputs collection.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Writing to the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|The connection manager "%1" returned an object of an  incorrect type from the AcquireConnection method.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|The "%3" property is required on input column "%1" (%2!d!), but is not found. The missing property should be added.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|The "%1" is marked read-only, but is not referenced by any other column. Unreferenced columns are not allowed.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|The "%1" references column ID %2!d!, and that column is not found on the input. A reference points to a nonexistent column.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not of a BLOB type.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|The "%1" references output column ID %2!d!, and that column is not found on the output.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Reading from the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|There must be at least one column of Fixed, Changing, or Historical type on the input of a Slowly Changing Dimension transform. Verify that at least one column is a FixedAttribute, ChangingAttribute, or HistoricalAttribute.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|The ColumnType property of "%1" is not valid. The current value is outside the range of acceptable values.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|The input column "%1" cannot be mapped to external column "%2" because they have different data types. The Slowly Changing Dimension transform does not allow mapping between column of different types except for DT_STR and DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|The data type for "%1" is DT_NTEXT, which is not supported with ANSI files. Use DT_TEXT instead and convert the data to DT_NTEXT using the data conversion component.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|The data type for "%1" is DT_TEXT, which is not supported with Unicode files. Use DT_NTEXT instead and convert the data to DT_TEXT using the data conversion component.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|The data type for "%1" is DT_IMAGE, which is not supported. Use DT_TEXT or DT_NTEXT instead and convert the data from, or to, DT_IMAGE using the data conversion component.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|Format "%1" is not supported by Flat File Connection Manager. Supported formats are Delimited, FixedWidth, RaggedRight, and Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not of a String type.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Error caused by conflicting property settings. The "%1" has both the AllowAppend property and the ForceTruncate property set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|The %1 references column ID %2!d!, but that column is already referenced by %3. Remove one of the two reference to the column.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|A connection manager has not been assigned to the %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|The %1 references the output column with ID %2!d!, but that column is already referenced by %3.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|The "%1" is not referenced by any input column. Each output column must be referenced by exactly one input column.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not the correct type. It must be DT_TEXT, DT_NTEXT, or DT_IMAGE. A reference points to a column that must be a BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not a String type.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|The "%1" has the ExpectBOM property set to TRUE for %2, but the column is not NT_NTEXT. The ExpectBOM specifies that the Import Column transformation expects a byte-order mark (BOM). Either set the ExpectBOM property to false or change the output column data type to DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Data output columns must be DT_TEXT, DT_NTEXT, or DT_IMAGE. The data output column may only be set to a BLOB type.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|If the FailOnFixedAttributeChange property is set to TRUE, the transformation will fail when a fixed attribute change is detected. To send rows to the Fixed Attribute output, set the FailOnFixedAttributeChange property to FALSE.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|The Lookup transformation failed to retrieve any rows. The transform fails when the FailOnLookupFailure is set to TRUE and no rows are retrieved.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|There must be at least one column type of Key on the input of a Slowly Changing Dimension transformation. Set at least one column type to Key.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Cannot find external column with name "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|Inferred indicator column "%1" must be of type DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|The %1 must have its error row disposition value set to RD_NotUsed.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|The %1 must have its truncation row disposition value set to RD_NotUsed.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Cannot find input column with lineage ID %1!d! needed by output column with ID %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Invalid output data type for aggregate type specified at output column ID %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Invalid input data type for %1 used for the specified aggregate at %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Data types of input column lineage ID %1!d! and output column ID %2!d! do not match.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Cannot get input buffer handle for input ID %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Cannot get output buffer handle for output ID %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Cannot find column with lineage ID %1!d! in output buffer.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Cannot find column with lineage ID %1!d! in input buffer.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|The number of output columns for %1 cannot be zero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|The number of columns in the flat file connection manager must be the same as the number of columns in the flat file adapter. The number of columns for the flat file connection manager is %1!d!, while the number of columns for the flat file adapter is %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|The column "%1" at index %2!d! in the flat file connection manager was not found at index %3!d! in the column collection of the flat file adapter.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|The external metadata column with ID %1!d! has already been mapped to %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|The transform encountered a key column that was larger than %1!u! characters.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|The transform encountered a result value that was longer than %1!u! bytes.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Unable to allocate memory.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Unable to allocate memory.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Unable to allocate memory.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Unable to allocate memory.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|The input column "%1" is not referenced.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|The Sort transformation could not create a thread pool with %1!d! threads. Not enough memory is available.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|The Sort transformation cannot queue a work item to its thread pool. There is not enough memory available.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|A worker thread in the Sort transformation stopped with error code 0x%1!8.8X!. A catastrophic error was encountered while sorting a buffer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads was %1!ld!, and should be between 1 and %2!ld!, inclusive or -1 to default to the number of CPUs.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Unable to load from XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|Unable to save to XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Unable to convert the value "%1" to an integer.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Unable to convert the value "%1" to a Boolean.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Load error encountered near object with ID %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|The %1 is not mapped to an output column.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|The %1 has a mapping that is not valid.  An output column with an ID of %2!ld! does not exist on this component.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|The %1 is mapped to an output column that already has a mapping on this input.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Could not convert input column with Lineage ID %1!ld! to DT_WSTR due to error 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Referenced object with ID %1!d! not found in package.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Cannot read a persistence property required for the pipelinexml module. The property was not provided by the pipeline.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Cannot retrieve custom property "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|An input column with the lineage ID %1!d!, referenced in the ParameterMap custom property with the parameter on position number %2!d!, cannot be found in the input columns collection.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Unable to locate reference column "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 and reference column named "%2" have incompatible data types.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|The parameterized SQL statement yields metadata which does not match the main SQL statement.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|The parameterized SQL statement contains an incorrect number of parameters. Expected %1!d!, but found %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 has a datatype which cannot be joined on.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 has a datatype which cannot be copied.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR or DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT, or DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, or DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|The Sort transformation cannot create an event to communicate with its worker threads. Not enough system handles are available to the Sort transformation.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|The Sort transformation cannot create a worker thread. Not enough memory is available to Sort transformation.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|The Sort transformation failed to compare row %1!d! in buffer ID %2!d! to row %3!d! in buffer ID %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|The Lookup transformation reference metadata contains too few columns. Check the SQLCommand property. The SELECT statement must return at least one column.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory for an array of ColumnInfo structures.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Could not allocate memory for an array of ColumnPair structures.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Unable to allocate memory for an array of BUFFCOL structures for the creation of a main workspace.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Unable to allocate memory for hash table.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for hash nodes.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for a hash node heap.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Unable to create a heap for LRU nodes. An out-of-memory condition occurred.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Unable to allocate memory for the LRU node heap. An out-of-memory condition occurred.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|OLE DB error occurred while loading column metadata. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|OLE DB error occurred while fetching rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|OLE DB error occurred while populating internal cache. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|OLE DB error occurred while binding parameters. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|OLE DB error occurred while creating bindings. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|An invalid case was encountered in a switch statement during runtime.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|OLE DB error occurred while fetching parameterized rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|OLE DB error occurred while fetching parameterized row. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Unable to allocate memory for the hash table.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for the hash nodes.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for the hash node heap.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct nodes.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Unable to allocate memory for CountDistinct node heap.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct chains.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Unable to allocate memory for CountDistinct hash table.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the CountDistinct workspace buffer.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Unable to create a CountDistinct workspace buffer.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Unable to allocate memory for CountDistinct Collapse array.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Unable to allocate memory for CountDistinct chains.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column for copymap does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|The output column with lineage ID "%1!d!" is incorrectly mapped to an input column. The CopyColumnId property of the output column is not correct.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Failed to retrieve long data for column "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Long data was retrieved for a column but cannot be added to the Data Flow task buffer.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|Output "%1" (%2!d!) has output columns, but multicast outputs do not declare columns. The package is damaged.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Unable to load a localized resource ID %1!d!. Verify that the RLL file is present.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Cannot acquire Events Interface. An invalid Events interface was passed to the data flow module for persisting to XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|An error occurred while setting a path object during XML load.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Error setting input object during XML load.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Error setting output object during XML load.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Error setting input column object during XML load.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Error setting output column object during XML load.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Error setting property object during XML load.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Error setting connection object during XML load.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Special transformation-specific columns are either missing or have incorrect types.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|Fuzzy Grouping transformation failed to create required tables and accessors.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|Fuzzy Grouping transformation failed to copy input.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|Fuzzy Grouping transformation failed to generate groups.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|An unexpected error occurred in Fuzzy Grouping when applying the settings of property '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|The Fuzzy Grouping transformation failed to pick a canonical row of data to use in standardizing the data.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|Fuzzy Grouping does not support input columns of type IMAGE, TEXT, or NTEXT.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|A fuzzy match is specified on column "%1" (%2!d!) that is not a data type of DT_STR or DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|A Fuzzy Grouping transformation pipeline error occurred and returned error code 0x%1!8.8X!: "%2".|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|The code page %1!d! specified on column "%2" (%3!d!) is not supported.  You must first convert this column to DT_WSTR which can be done by inserting a Data Conversion Transform before this one.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Failure encountered while setting end of data flag for the buffer driving output "%1" (%2!d!).|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|The input buffer could not be cloned. An out-of-memory condition occurred or there was an internal error.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|Column "%1" requests that Katakana and Hiragana characters be produced at the same time.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|Column "%1" requests that Simple Chinese and Traditional Chinese characters be produced at the same time.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|Column "%1" requests operations to generate both full width and half width characters.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|Column "%1" combines operations on Japanese characters with operations for Chinese characters.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|Column "%1" combines operations on Chinese characters with uppercase and lowercase operations.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|Column "%1" combines operations on Japanese characters with uppercase and lowercase operations.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|Column "%1" maps the column to both uppercase and lowercase.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|Column "%1" combines flags other than uppercase and lowercase with the linguistic casing operation.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|The data type of column "%1" cannot be mapped as specified.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|The version (%1) of the pre-existing match index "%2" is not supported. The version expected is "%3". This error occurs if the version persisted in the index metadata does not match the version which the current code was built for. Fix the error by rebuilding the index with the current version of the code.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|The table "%1" does not appear to be a valid pre-built match index. This error occurs if the metadata record cannot be loaded from the specified pre-built index.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Unable to read specified pre-built match index "%1".  OLEDB Error code: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|There were no input columns with a valid join to a reference table column.  Make sure that there is at least one join defined using the input column properties JoinToReferenceColumn and JoinType.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|The specified pre-existing match index "%1" was not originally built with fuzzy match information for column "%2".  It must be rebuilt to include this information. This error occurs when the index was built with the column not being a fuzzy join column.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|The name "%1" given for property "%2" is not a valid SQL identifier name. This error occurs if the name for the property does not conform to the specifications for a valid SQL identifier name.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|The MinSimilarity threshold property on the Fuzzy Lookup transformation must be a value greater than or equal to 0.0 but less than 1.0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|The value "%1" for property "%2" is not valid.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|The fuzzy lookup specified between input column "%1" and reference column "%2" is not valid because fuzzy joins are only supported between string columns, types DT_STR and DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|The exact lookup columns, "%1" and "%2", do not have equal data types or are not comparable string types. Exact joins are supported between columns with equal data types or a DT_STR and DT_WSTR combination.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|The copy columns, "%1" and "%2", do not have equal data types or are not trivially convertible string types. This occurs because copying from reference to output between columns with equal data types, or a DT_STR and DT_WSTR combination, is supported, but other types are not.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|The passthrough columns, "%1" and "%2", do not have equal data types. Only columns with equal data types are supported as passthrough columns from input to output.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Cannot locate reference column "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|An output column must have exactly one CopyColumn or PassThruColumn property specified. This error occurs when neither the CopyColumn or the PassThruColumn properties, or both the CopyColumn and PassThruColumn properties, are set to non-empty values.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|The source lineage id '%1!d!' specified for property '%2' on output column '%3' was not found in the input column collection. This occurs when the input column id specified on an output column as a passthrough column is not found in the set of inputs.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|The column "%1" in the pre-built index "%2" was not found in the reference table/query. This happens if the schema/query of the reference table has changed since the pre-existing match index was built.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|The component encountered a token that was larger than 2147483647 characters.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has type %2 and the input column has type %3. The metadata for the column does not match on data type.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has maximum length %2!d! and the input column has maximum length %3!d!. The metadata for the column does not match in length.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has code page %2!d! and the input column has code page %3!d!. The metadata for the named column does not match on code page.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|The output file cannot be appended. Column "%1" matches by name, but the column in the file has precision %2!d! and the input column has precision %3!d!. The metadata for the named column does not match on precision.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has scale %2!d! and the input column has scale %3!d!.  The metadata for the named column does not match on scale.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Unable to determine the DBMS name and version on "%1". This occurs if the IDBProperties on the connection did not return information needed to verify the DBMS name and version.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|The DBMS type or version of "%1" is not supported.  A connection to Microsoft SQL Server version 8.0 or later is required. This occurs if IDBProperties on the connection did not return a the correct version.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|The %1 is a special error output column and cannot be deleted.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|The data type specified for column "%1" is not the expected type "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|The input column lineage ID "%1" referenced by property "%2" on output column "%3" could not be located in the input column collection.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|The input column "%1" referenced by the "%2" property on output column "%3" must have property ToBeCleaned=True and have a valid ExactFuzzy property value.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|The reference table '%1' does not have a clustered index on an integer identity column, which is required if the property 'CopyRefTable' is set to FALSE. If CopyRefTable is false, the reference table must have a clustered index on an integer identity column.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|The reference table '%1' contains a non-integer type identity column which is not supported. Use a view of the table without the column '%2'.  This error occurs  because when a copy is made of the reference table, an integer identity column is added, and only one identity column is allowed per table.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|Both MatchContribution and hierarchy information cannot be specified at the same time. This is not allowed because these properties are both weighing factors for scoring.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Levels in hierarchy should be unique numbers . Valid  level in hierarchy values are integers greater than or equal to 1. The smaller the number is, the lower the column is in the hierarchy. The default value is 0, indicating that the column is not part of a hierarchy. Overlaps and gaps are not allowed.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|No columns to fuzzy group on were defined.  There must be at least one input column with column properties ToBeCleaned=true and ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|The column with ID '%1!d!' was not valid for an undetermined reason.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|The data type of column '%1' is not supported.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|The length of output column '%1' is less than that of its source column '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|There should be only one input column.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|There should be exactly two output columns.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|The input column can only have DT_WSTR or DT_NTEXT as its data type.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|The output column [%1!d!] can only have '%2' as its data type.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|The Term Type of the transformation can only be WordOnly, PhraseOnly or WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|The value of Frequency Threshold should not be lower than '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|The value of Max Length of Term should not be lower than '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Term Extraction reference metadata contains too few columns.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|An error occurred while allocating memory.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|An error occurred while extracting terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|The number of the term candidates exceeds its limit, 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|The reference table, view, or column that is used for Exclusion Terms is not valid.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|The length of string column '%1' exceeds 4000 characters.  A conversion from DT_STR to DT_WSTR is necessary, so a truncation would occur.  Either reduce the column width or use only DT_WSTR column types.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|The reference table, view, or column to be used for an Exclusion Terms has not been set.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|Term Lookup contains too few output columns.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Term Lookup reference metadata contains too few columns.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|An error occurred while normalizing words.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|An error occurred while looking up terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|At least one Passthrough column is not mapped to an output column.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|There should be exactly one input column mapped to one reference column.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|The input column mapped to a reference column can only have DT_NTXT or DT_WSTR as its data type.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|The reference table name "%1" is not a valid SQL identifier. This error occurs if the table name cannot be parsed from the input string. There may be unquoted spaces in the name. Verify that the name is correctly quoted.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|An error occurred while the Term Filter was starting its iteration.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|An error occurred while reclaiming the buffer used for caching terms. The error code returned was 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|An std::length_error occurred from the STL containers.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|An error occurred while saving words with punctuation characters. The error code returned was 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|An error occurred while processing the %1!ld!th reference term. The error code returned was 0x%2!8.8X!. Please remove the reference term from your reference table as a work-around.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|An error occurred while sorting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|Fuzzy Lookup was unable to load the entire reference table into main memory as is required when the Exhaustive property is enabled.  Either we ran out of system memory or a limit was specified for MaxMemoryUsage which was not sufficient to load the reference table.  Either set MaxMemoryUsage to 0 or increase it significantly.  Alternatively, disable Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|An error occurred while initializing the engine of Term Lookup. The error code returned was 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|An error occurred while processing sentences. The error code returned was 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|An error occurred while saving part-of-speech tags from an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|An error occurred while loading the finite state automata. The error code returned was 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|An error occurred while initializing the engine of Term Extraction. The error code returned was 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|An error occurred while processing within a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|An error occurred while adding words to a statistical decoder. The error code returned was 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|An error occurred while decoding for a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|An error occurred while setting exclusion terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|An error occurred while testing whether a dot is a part of an acronym. The error code returned was 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|An error occurred while setting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|The value for the property %1 is %2!d!, which is not allowed.  The value must be greater than or equal to %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|The value for the property %1 is %2!d!, which must be less than or equal to the value of %3!d! for property %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|An error was encountered when trying to delete the existing fuzzy match index named "%1". It is possible that this table was not created by Fuzzy Lookup (or this version of Fuzzy Lookup), it has been damaged, or there is another problem. Try manually deleting the table named "%2" or specify a different name for the MatchIndexName property.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|The Score Type of the transformation can only be Frequency or TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|The reference table specified has too many rows. Fuzzy Lookup only works with reference tables having less than 1 billion rows. Consider using a smaller view of your reference table.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Unable to determine the size of the reference table '%1'.  It is possible that this object is a view and not a table.  Fuzzy Lookup does not support views when CopyReferentaceTable=false.  Make sure that the table exists and that CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|The SSIS Data Flow Task data type "%1" on the %2 is not supported for the %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Unable to set data type properties for the output column with ID %1!d! on the output with ID %2!d!. The output or column could not be found.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|The value of custom property "%1" on the %2 cannot be changed.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|The %1 on the non-error output has no corresponding output column on the error output.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|The %1 on the error output has no corresponding output column on the non-error output.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|The %1 on the error output has properties that do not match the properties of its corresponding data source column.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|The data type of output columns on the %1 cannot be changed, except for DT_WSTR and DT_NTEXT columns.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|The data type of "%1" does not match the data type "%2" of the source column "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|The %1 does not have a matching source column in the schema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|The reference table/view or column used for the reference terms is invalid.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|The reference table/view or column used for the reference terms has not been set.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|The %1 is mapped to the external metadata column with ID %2!ld!, which is already mapped to another column.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|The SQL object name '%1' specified for property '%2' contains more than the maximum number of prefixes.  The maximum is 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|The value was too large to fit in the column.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|The SSIS IDataReader is closed.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|The SSIS IDataReader is past the end of the result set.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|The ordinal position of the column is not valid.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|Cannot convert the %1 from data type "%2" to data type "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|The %1 has unsupported code page %2!d!.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|The %1 has no mapping to the XML schema.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|The SSIS IDataReader is closed. The read timeout has expired.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|An error occurred executing the provided SQL command: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|The JoinType property specified for input column '%1' differs from the JoinType specified for the corresponding reference table column when the Match Index was initially created.  Either rebuild the Match Index with the given JoinType or change the JoinType to match the type used when the Match Index was created.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|The data type "%1" found on %2 is not supported for the %3.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|The data type of the %1 is not supported for the %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Failed to add project reference "%1" while migrating %2. Migration might need to be completed manually.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Multiple entry points with the name "%1" were found during the migration of %2. Migration might need to be completed manually.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|No entry point was found during the migration of %1. Migration might need to be completed manually.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|An exception has occurred during data insertion, the message returned from the provider is: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Failed to retrieve the provider invariant name from %1, it is currently not supported by ADO NET Destination component|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|An argument exception has occurred while data provider tried to insert data to destination. The returned message is : %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|The BatchSize property must be a non-negative integer|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|An error has occurred while sending this row to destination data source.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|Executing tSQL command throws an exception, the message is :  %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET Destination has failed to acquire the connection %1. The connection may have been corrupted.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|The specified connection %1 is not managed, please use managed connection for ADO NET destination.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|The destination component does not have an error output. It may have been corrupted.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|The lineageID %1 associated with external column %2 does not exist at run time.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Failed to get properties of external columns. The table name you entered may not exist, or you do not have SELECT permission on the table object and an alternative attempt to get column properties through connection has failed. Detailed error messages are: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|Input column error disposition is not supported by ADO NET Destination component.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|Input column truncation disposition is not supported by ADO NET Destination component.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|Input  truncation row disposition is not supported by ADO NET Destination component.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|The Table or View name is not expected. \n\t If you are quoting the table name, please use the prefix %1 and the suffix %2 of your selected data provider for quotation. \n\t If you are using multipart name, please use at most three parts for the table name.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Failed to find column "%1" with lineage ID %2!d! in the buffer. The buffer manager returned error code 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Failed to get information for column "%1" (%2!d!) from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Arithmetic overflow encountered while aggregating "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Failed to get information for row %1!ld!, column %2!ld! from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Failed to set information for row %1!ld!, column %2!ld! into the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|A required buffer is not available.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|The attempt to get buffer boundary information failed with error code 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Setting the end of rowset for the buffer failed with error code 0x%1!8.8X!.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Failed to get data for the error output buffer.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Removing a row from the buffer failed with error code 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|The attempt to set buffer error information failed with error code 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|There was an error with %1 on %2. The column status returned was: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Unable to cache reference metadata.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|Row yielded no match during lookup.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|The %1 has an invalid error or truncation row disposition.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Directing the row to the error output failed with error code 0x%1!8.8X!.|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Preparing column statuses for insert failed with error code 0x%1!8.8X!.|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|An attempt to find %1 with lineage ID %2!d! in the Data Flow Task buffer failed with error code 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Failed to find any non-special error column in %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS Error Code DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" specifies failure on error. An error occurred on the specified object of the specified component.  There may be error messages posted before this with more information about the failure.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|The expression "%1" on "%2" evaluated to NULL, but the "%3" requires a Boolean results. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row).  The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|The expression evaluated to NULL, but a Boolean result is required. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row). The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|The file format of UTF-16 big endian is not supported.  Only UTF-16 little endian format is supported.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|The file format of UTF-8 is not supported as Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Cannot read ID attribute.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|The cache index column %1 is referenced by more than one lookup input column.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|Lookup does not reference all cache connection manager index columns. Number of joined columns in lookup: %1!d!. Number of index columns: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violated the integrity constraints for the column.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violates integrity constraints.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the data conversion transform.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the flat file source adapter was unsigned.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the flat file source adapter.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Opening the file "%1" for reading failed with error code 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Failed to open file for reading.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Opening the file "%1" for writing failed with error code 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Failed to open file for writing.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Failed to read from file.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Failed to write to file.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Too many array elements were found when parsing a property of type array. The elementCount is less than the number of array elements found.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Too few array elements were found when parsing a property of type array. The elementCount is more than the number of array elements found.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file "%1" for writing failed. The file cannot be found.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file for writing failed. The file cannot be found.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file "%1" for writing failed. The path cannot be found.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file for writing failed. The path cannot be found.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file "%1" for writing failed. There are too many files open.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file for writing failed. There are too many files open.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file "%1" for writing failed. You do not have the correct permissions.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file for writing failed. You do not have the correct permissions.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Opening the file "%1" for writing failed. The file exists and cannot be overwritten. If the AllowAppend property is FALSE and the ForceTruncate property is set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Opening a file for writing failed. The file already exists and cannot be overwritten. If both the AllowAppend property and the ForceTruncate property are set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|The value for custom property "%1" on %2 is incorrect.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Columns "%1" and "%2" have incompatible metadata.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Opening the file "%1" for writing failed because the disk is full. There is not sufficient disk space to save this file.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Attempting to open the file for writing failed because the disk is full.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Generating a sort key failed with error 0x%1!8.8X!. The ComparisonFlags are enabled, and generating a sortkey with LCMapString failed.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|Transform failed to map string and returned error 0x%1!8.8X!. The LCMapString failed.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Opening the file "%1" for reading failed. The file was not found.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Opening a file for reading failed. The file was not found.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening the file "%1" for reading failed. The path cannot be found.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening a file for reading failed. The path was not found.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file "%1" for reading failed. There are too many files open.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file for reading failed. There are too many files open.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Attempting to open the file "%1" for reading failed. Access is denied.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Opening the file for reading failed. You do not have the correct permissions.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file "%1" is 0x%2!4.4X!, but the expected value is 0x%3!4.4X!. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file is not valid. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|The %1 is not attached to a component.  It is required that a component be attached.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|The value for custom property %1 is incorrect.  It should be a number between %2!d! and %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|The custom property "%1" cannot be specified for the aggregation type selected for this column. The comparison flags custom property can only be specified for group by and count distinct aggregation types.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|The comparison flags custom property "%1" can only be specified for columns of with datatype DT_STR or DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Aggregation on %1 failed with error code 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|There was an error setting up the mapping. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|The %1 was unable to read the XML data.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|The %1 was unable to get the variable specified by the "%2" property.|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|The %1 contains a RowsetID with a value of %2 that does not reference a data table in the schema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|The property %1 must either be empty, or a number between %2!u! and %3!u!. The Keys or CountDistinctKeys property has a invalid value. The property should be a number between 0 and ULONG_MAX, inclusive, or not be set.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|The aggregate component encountered too many distinct key combinations. It cannot accommodate more than %1!u! distinct key values. There are more than ULONG_MAX distinct key values in the main workspace.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|The aggregate component encountered too many distinct values while calculating the count distinct aggregate. It cannot accommodate more than %1!u! distinct values. There were more than ULONG_MAX distinct values while calculating the count distinct aggregation.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|The attempt to write to the filename column failed with error code 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|An error occurred, but the column that caused the error cannot be determined.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Unable to upgrade lookup metadata from version %1!d! to %2!d!. The Lookup transform was unable to upgrade metadata from the existing version number in a call to PerformUpgrade().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Failed to locate the ending boundary of a sentence.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|The Term Extraction transformation is unable to process the input text because a sentence from the input text is too long. The sentence is segmented into several sentences.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|The %1 was unable to read the XML data. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|The call to Lookup transform method, ReinitializeMetadata, failed.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|The lookup transform must contain at least one input column joined to a reference column, and none were specified. You must specify at least one join column.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|The message string being posted by the managed error infrastructure contains a bad format specification. This is an internal error.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|While formatting a message string using the managed error infrastructure, there was a variant type that does not have formatting support. This is an internal error.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|The %1 was unable to process the data. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|The property "%1" on the %2 was empty.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Attempting to create an output with the name "%1" for the XML table with the path "%2" failed because the name is invalid.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|The value was too large to fit in the %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|The %1 was unable to process the data.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2"  at "%3" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" at "%4" specifies failure on error. An error occurred on the specified object of the specified component.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|The SQLCE destination could not set the column values for the row.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|The SQLCE destination could not insert the row.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Unable to allocate memory.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Unable to create workspace buffer.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Unable to instantiate XML DOM document, please verify that MSXML binaries are properly installed and registered.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|Unable to load XML data into a local DOM for processing.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|The type of the runtime variable "%1" is incorrect. The runtime variable type must be Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. Multiple inline schemas are not supported.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not be declared as anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not contain a reference (ref) to a group.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|The XML Source Adapter does not support mixed content model on Complex Types.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|The XML Source Adapter was unable to process the XML data. An inline schema must be the first child node in the source Xml.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|The XML Source Adapter was unable to process the XML data. No inline schema was found in the source XML, but the "UseInlineSchema" property was set to true.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|The component cannot use a connection manager that retains its connection in a transaction with fastload or bulk insert.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|The %1 cannot be set to redirect on error using a connection in a transaction.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|The %1 does not have a corresponding input or output column.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|There is no selected column to be written to the file.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|The %1 has an invalid data type. Columns with data types DT_IMAGE, DT_TEXT and DT_NTEXT cannot be written to raw files.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|The external metadata collection is improperly used by this component. The component should use external metadata when appending or truncating an existing file. Otherwise, the external metadata is not needed.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|The %1 is mapped to an external metadata column with the id %2!d!. Input columns should not be mapped to external metadata columns when selected Write Option value is Create Always.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|The file  cannot be opened for reading the metadata. If the file does not exist, and the component has already defined external metadata, you can set the "ValidateExternalMetadata" property to "false" and the file will be created at the runtime.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Failed to access LOB data from the data flow buffer for data source column "%1" with error code 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|The %1 was unable to process the XML data. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|The XML Source Adapter was unable to process the XML data.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|The value %1!d! is not recognized as a valid access mode.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Complete metadata information for the data source column "%1" is not available.  Make sure the column is correctly defined in the data source.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Only lengths of User Name column, Package Name column, Task Name column and Machine Name column can be changed.  All other audit column datatype information is read only.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|A rowset based on the SQL command was not returned by the OLE DB provider.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|A commit failed.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|The custom property "%1" on %2 can only be used with ANSI files.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|The custom property "%1" on %2 can only be used with DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_ERROR.  The requested OLE DB provider %2 is not registered. Error code: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  The requested OLE DB provider %2 is not registered -- perhaps no 64-bit provider is available.  Error code: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|The cache column, "%1", is mapped to more than one column. Remove the duplicate column mappings.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|The %1 is not mapped to valid cache column.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because the data types do not match.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|The number of input columns does not match the number of cache columns.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|The cache file name is either not provided or is not valid. Provide a valid cache file name.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|The index position of column, "%1", is different from index position of Cache connection manager column, "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Failed to load the cache from file, "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|The lookup input column %1 references non-index cache column %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Failed to get the connection string.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because one or more data type properties do not match.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Cache column "%1" was not found in the cache.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Failed to map %1 to a cache column. The hresult is 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|The %1 cannot write to the cache because the cache has been loaded from a file by %2.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|The %1 cannot load the cache from file "%2" because the cache has already been loaded from file "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|The output with ID %1!d! of Aggregate component is not used by any component. Please either remove it or associate it with an input of some component.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|The %1 failed to write the cache to file "%2". The hresult is 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|The XML schema data type information for "%1" on  element "%2" has changed.  Please re-initialize the metadata for this component and review column mappings.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 not used in join or copy. Please remove the unused column from the input column list.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|The sort failed due to a stack overflow while sorting an incoming buffer.  Please reduce the DefaultBufferMaxRows property on the Data Flow Task.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Consider changing the PROVIDER in the connection string to %1 or visit https://www.microsoft.com/downloads to find and install support for %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Failed to initialize the task object for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Failed to create COM Component Categories Manager due to error 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|Component %1!s! failed to initialize due to error 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Warning Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] warning messages begin with **DTS_W_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|There are %1!lu! days left in the evaluation. When it expires, packages will not be able to be executed.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Warning(s) raised. There should be more specific warnings preceding this one that explain the specifics of the warning(s).|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Cannot create an XML document object instance. Verify that MSXML is installed and registered correctly.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Cannot load the XML configuration file. The XML configuration file may be malformed or not valid.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|The configuration file name "%1" is not valid. Check the configuration file name.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|The configuration file loaded, but is not valid. The file is not formatted correctly, may be missing an element, or may be damaged.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|The configuration file "%1" cannot be found. Check the directory and file name.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Configuration registry key "%1" was not found. A configuration entry specifies a registry key that is not available. Check the registry to ensure that the key is there.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|The configuration type in one of the configuration entries was not valid. Valid types are listed in the DTSConfigurationType enumeration.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|The package path referenced an object that cannot be found: "%1". This occurs when an attempt is made to resolve a package path to an object that cannot be found.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with the package delimiter. Prepend "\package" to the package path.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|Configuration from a parent variable "%1" did not occur because there was no parent variable collection.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Failure importing configuration file: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|Configuration from a parent variable "%1" did not occur because there was no parent variable. Error code: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|The configuration file was empty and contained no configuration entries.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|The configuration type for configuration "%1" is not valid. This may occur when an attempt is made to set the type property of a configuration object to an invalid configuration type.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|The configuration type for the registry configuration was not found in key "%1". Add a value called ConfigType to the registry key and give it a string value of "Variable", "Property", "ConnectionManager", "LoggingProvider", or "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|The configuration value for the registry configuration was not found in key "%1". Add a value called Value to the registry key of type DWORD or String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Process configuration failed to set the destination at the package path of "%1". This occurs when attempting to set the destination property or variable fails. Check the destination property or variable.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredValue section is either empty, or does not exist: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredType section is either empty, or does not exist: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Failed to retrieve value from the .ini file. The PackagePath section is either empty, or does not exist: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Failed to retrieve value from the .ini file. The ConfiguredValueType section is either empty, or does not exist: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|Configuration from SQL Server was not successfully imported: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|The .ini configuration file is not valid due to empty or missing fields.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|Table "%1" does not have any records for configuration. This occurs when configuring from a SQL Server table that has no records for the configuration.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Error using same name for different custom events. The custom event "%1" was defined differently by different children of this container. There may be an error when executing the event handler.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|The configuration attempted to change a read-only variable. The variable is at the package path "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Calling ProcessConfiguration on the package failed. The configuration attempted to change the property at the package path "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Failed to load at least one of the configuration entries for the package. Check configuration entries for "%1" and previous warnings to see descriptions of which configuration failed.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|The configuration entry "%1" in the configuration file was not valid, or failed to configure the variable.  The name indicates which entry failed. In some cases, the name will not be available.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|This task or container has failed, but because FailPackageOnFailure property is FALSE, the package will continue. This warning is posted when the SaveCheckpoints property of the package is set to TRUE and the task or container fails.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|The path is empty.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS Warning Code DTS_W_MAXIMUMERRORCOUNTREACHED.  The Execution method succeeded, but the number of errors raised (%1!d!) reached the maximum allowed (%2!d!); resulting in failure. This occurs when the number of errors reaches the number specified in MaximumErrorCount. Change the MaximumErrorCount or fix the errors.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|The configuration environment variable was not found.  The environment variable was: "%1". This occurs when a package specifies an environment variable for a configuration setting but it cannot be found. Check the configurations collection in the package and verify that the specified environment variable is available and valid.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|The provider name for the connection manager "%1" has been changed from "%2" to "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|An exception occurred while reading the upgrade mapping files. The exception is "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|There is a duplicate mapping in file, "%1". The tag is "%2", and the key is "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|The extension, "%1", was implicitly upgraded to "%2". Add a mapping for this extension to the UpgradeMappings directory.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|A mapping in the file, "%1", is not valid. Values cannot be null or empty. The tag is "%2", the key is "%3", and the value is "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|The DataTypeCompatibility property of ADO type connection manager "%1" was set to 80 for backward compatibility reasons.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|The For Each File enumerator is empty. The For Each File enumerator did not find any files that matched the file pattern, or the specified directory was empty.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1". Verify that the package path is valid.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|The iteration expression is not an assignment expression: "%1". This error usually occurs when the expression in the assignment expression on the ForLoop is not an assignment expression.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|The initialization expression is not an assignment expression: "%1". This error usually occurs when the expression in the iterate expressions on the ForLoop is not an assignment expression.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|The executable "%1" was pasted successfully. However a log provider that was associated with the executable was not found in the collection "LogProviders".  The executable was pasted without log provider information.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Succeeded in upgrading the package.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|The "%1" ProgID has been deprecated. The new ProgID for this component "%2" should be used instead.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Operation "%1" failed.|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|The encryption algorithm "%1" uses weak encryption.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Task failed to execute operation "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|The subject is empty.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|The address in the "To" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|The address in the "From" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|The two XML documents are different.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD Validation will use the DTD file defined in the DOCTYPE line in the XML document. It will not use what is assigned to the property "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Task failed to validate "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|The transfer action value was invalid.  It is being set to copy.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|The transfer method value was invalid.  It is being set to an online transfer.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|A problem occurred with the following messages: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Skipping the transfer of job "%1" since it already exists at destination.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Overwriting the job "%1" at destination server.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Persisted enumeration value of property "FailIfExists" was changed and rendered invalid. Resetting to default.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Overwriting Login "%1" at destination.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|There are no elements specified to transfer.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|The lineage IDs of the input columns cannot be validated because the execution trees contain cycles.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|The DataFlow task has no components. Add components or remove the task.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but all of its output columns' SortKeyPositions are set to zero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|Source "%1" (%2!d!) will not be read because none of its data ever becomes visible outside the Data Flow Task.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|The output column "%1" (%2!d!) on output "%3" (%4!d!) and component "%5" (%6!d!) is not subsequently used in the Data Flow task. Removing this unused output column can increase Data Flow task performance.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Component "%1" (%2!d!) has been removed from the Data Flow task because its output is not used and its inputs either have no side effects or are not connected to outputs of other components. If the component is required, then the HasSideEffects property on at least one of its inputs should be set to true, or its output should be connected to something.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Rows were given to a thread, but that thread has no work to do. The layout has a disconnected output. Running the pipeline with the RunInOptimizedMode property set to TRUE will be faster, and prevents this warning.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|The external columns for %1 are out of synchronization with the data source columns. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|The column "%1" needs to be added to the external columns.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|The external column "%1" needs to be updated.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|The %1 needs to be removed from the external columns.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|The result string for expression "%1" may be truncated if it exceeds the maximum length of %2!d! characters. The expression could have a result value that exceeds the maximum size of a DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|A call to the ProcessInput method for input %1!d! on %2 unexpectedly kept a reference to the buffer it was passed. The refcount on that buffer was %3!d! before the call, and %4!d! after the call returned.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|The "%1" on "%2" has usage type READONLY, but is not referenced by an expression. Remove the column from the list of available input columns, or reference it in an expression.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Cannot find the "%1" value for component %2. The CurrentVersion value for the component cannot be located. This error occurs if the component has not set its registry information to contain a CurrentVersion value in the DTSInfo section. This message occurs during component development, or when the component is used in a package, if the component is not registered properly.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Warning: Could not open global shared memory to communicate with performance DLL; data flow performance counters are not available.  To resolve, run this package as an administrator, or on the system's console.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|There is a partial row at the end of the file.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|The end of the data file was reached while reading header rows. Make sure the header row delimiter and the number of header rows to skip are correct.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Cannot retrieve the column code page info from the OLE DB provider.  If the component supports the "%1" property, the code page from that property will be used.  Change the value of the property if the current string code page values are incorrect.  If the component does not support the property, the code page from the component's locale ID will be used.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|The data is already sorted as specified so the transform can be removed.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|The %1 references an external data type that cannot be mapped to a Data Flow task data type. The Data Flow task data type DT_WSTR will be used instead.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|The expression "%1" will always result in a truncation of data. The expression contains a static truncation (the truncation of a fixed value).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|The input column "%1" with ID %2!d! at index %3!d! is unmapped. The lineage ID for the column is zero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|The specified delimiters do not match the delimiters used to build the pre-existing match index "%1". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|The MaxOutputMatchesPerInput property on the Fuzzy Lookup transformation is zero. No results will be produced.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|There were no valid input columns with JoinType column property set to Fuzzy.  Performance on Exact joins may be improved by using the Lookup transform instead of FuzzyLookup.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|The reference column "%1" may be a SQL timestamp column. When the fuzzy match index is built, and a copy of the reference table is made, all reference table timestamps will reflect the current state of the table at the time of the copy. Unexpected behavior may occur if the CopyReferenceTable is set to false.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|A table with the name '%1' given for MatchIndexName already exists and DropExistingMatchIndex is set to FALSE.  Transform execution will fail unless this table is dropped, a different name is specified, or DropExisitingMatchIndex is set to TRUE.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|The length of input column '%1' is not equal to the length of the reference column '%2' that it is being matched against.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|The code pages of the DT_STR source column "%1" and the DT_STR dest column "%2" do not match.  This may cause unexpected results.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|There are more than 16 exact match joins, so performance may not be optimal. Reduce the number of exact match joins to improve performance. SQL Server has a limit of 16 columns per index, the inverted index will be used for all lookups.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|The Exhaustive option requires that the entire reference be loaded into main memory.  Since a memory limit has been specified for the MaxMemoryUsage property, it is possible that the entire reference table will not fit within this bound and that the match operation will fail at runtime.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|The cumulative lengths of the columns specified in the exact match joins exceeds the 900 byte limit for index keys.  Fuzzy Lookup creates an index on the exact match columns to increase lookup performance and there is a possibility that creation of this index may fail and the lookup will fall back to an alternative, possibly slower, method of finding matches. If performance is a problem, try removing some exact match join columns or reduce the maximum lengths of variable length exact match columns.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Failed to create an index for exact match columns. Reverting to alternative fuzzy lookup method.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|The following Fuzzy Grouping internal pipeline warning occurred with warning code 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|No maximum length was specified for the %1 with external data type %2. The SSIS Data Flow Task data type "%3" with a length of %4!d! will be used.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|The %1 references external data type %2, which cannot be mapped to a SSIS Data Flow Task data type.  The SSIS Data Flow Task data type DT_WSTR with a length of %3!d! will be used instead.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|No rows will be sent to error output(s). Configure error or truncation dispositions to redirect rows to the error output(s), or delete data flow transformations or destinations that are attached to the error output(s).|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|Rows sent to the error output(s) will be lost. Add new data flow transformations or destinations to receive error rows, or reconfigure the component to stop redirecting rows to the error output(s).|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|For the %1 with external data type %2, the XML schema specified a maxLength constraint of %3!d!, which exceeds the maximum allowed column length of %4!d!. The SSIS Data Flow Task data type "%5" with a length of %6!d! will be used.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|The %1 encountered duplicate reference key values when caching reference data. This error occurs in Full Cache mode only. Either remove the duplicate key values, or change the cache mode to PARTIAL or NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Truncation may occur due to inserting data from data flow column "%1" with a length of %2!d! to database column "%3" with a length of %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Truncation may occur due to retrieving data from database column "%1" with a length of %2!d! to data flow column "%3" with a length of %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Batch mode is not currently supported when error row disposition is used. The BatchSize property will be set to 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|No rows were successfully inserted into the destination. This may be due to a data type mismatch between columns, or due to the use of a datatype that is unsupported by your ADO.NET provider. Since the error disposition for this component is not "Fail component", error messages are not shown here; set the error disposition to "Fail component" to see error messages here.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Potential data loss may occur due to inserting data from input column "%1" with data type "%2" to external column "%3" with data type "%4". If this is intended, an alternative way to do conversion is using a Data Conversion component before ADO NET destination component.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|The %1 has been out of synchronization with the database column.  The latest column has %2. Use advanced editor to refresh  available destination columns if needed.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed. Use Advanced Editor to refresh the available destination columns if needed.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|A new column with name %1 has been added to the external database table. Use advanced editor to refresh available destination columns if needed.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|No rows will be sent to the no match output. Configure the transformation to redirect rows with no matching entries to the no match output, or delete the data flow transformations or destinations that are attached to the no match output.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Exception received while enumerating ADO.Net providers. The invariant was "%1". The exception message is: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|The %1 has no input column mapped to it.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|The table "%1" has changed. New columns might have been added to the table.|  
  
##  <a name="msgInfo"></a> Informational Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] informational messages begin with **DTS_I_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Starting distributed transaction for this container.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Committing distributed transaction started by this container.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Aborting the current distributed transaction.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" was successfully acquired.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" was successfully released.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" was successfully created.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Debug dump files will be generated for any error event.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Debug dump files will be generated for the following event codes: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Event code, 0x%1!8.8X!, triggered generation of debug dump files in the folder "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Creating SSIS information dump file "%1".|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Debug dump files successfully created.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|The package format was migrated from version %1!d! to version %2!d!. It must be saved to retain migration changes.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|The scripts in the package were migrated. The package must be saved to retain migration changes.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Receiving file "%1".|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Sending file "%1".|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|File "%1" already exists.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Cannot get extra error information due to an internal error.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|The attempt to delete file "%1" failed. This may occur when the file does not exist, the file name was spelled incorrectly, or you do not have permissions to delete the file.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|The package is attempting to configure from a registry entry using the registry key "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|The package is attempting to configure from the environment variable "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|The package is attempting to configure from the .ini file "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|The package is attempting to configure from SQL Server using the configuration string "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|The package is attempting to configure from the XML file "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|The package is attempting to configure from the parent variable "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|Attempting an upgrade of SSIS from version "%1" to version "%2". The package is attempting to upgrade the runtime.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Attempting to upgrade "%1". The package is attempting to upgrade an extensible object.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|The package will be saving checkpoints to file "%1" during execution. The package is configured to save checkpoints.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|The package restarted from checkpoint file "%1". The package was configured to restart from checkpoint.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|Checkpoint file "%1" was updated to record completion of this container.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|Checkpoint file "%1" was deleted after successful completion of the package.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Checkpoint file "%1" update starting.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Based on the system configuration, the maximum concurrent executables are set to %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|Maximum concurrent executables are set to %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Beginning of package execution.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|End of package execution.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Overwriting the database "%1" on the destination server "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Skipping error message "%1" since it already exists on the destination server.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" Error Messages were transferred.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|The task transferred "%1" Stored Procedures.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|Transferred "%1" objects.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|There are no Stored Procedures to transfer.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|There are no Rules to transfer.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|There are no Tables to transfer.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|There are no Views to transfer.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|There are no User Defined Functions to transfer.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|There are no Defaults to transfer.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|There are no User Defined Data Types to transfer.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|There are no Partition Functions to transfer.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|There are no Partition Schemes to transfer.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|There are no Schemas to transfer.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|There are no SqlAssemblies to transfer.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|There are no User Defined Aggregates to transfer.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|There are no User Defined Types to transfer.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|There are no XmlSchemaCollections to transfer.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|There are no Logins to transfer.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|There are no Users to transfer.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Truncating table "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Prepare for Execute phase is beginning.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Pre-Execute phase is beginning.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Post Execute phase is beginning.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Cleanup phase is beginning.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Validation phase is beginning.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" wrote %2!ld! rows.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Execute phase is beginning.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|The buffer manager detected that the system was low on virtual memory, but was unable to swap out any buffers. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough is installed, other processes are using it, or too many buffers are locked.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|The buffer manager failed a memory allocation call for %3!d! bytes, but was unable to swap out any buffers to relieve memory pressure. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough are installed, other processes were using it, or too many buffers are locked.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|The buffer manager has allocated %1!d! bytes, even though the memory pressure has been detected and repeated attempts to swap buffers have failed.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 has cached %2!d! rows.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 has cached a total of %2!d! rows.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|The raw source adapter opened a file, but the file contains no columns. The adapter will not produce data. This could indicate a damaged file, or that there are zero columns and, therefore, no data.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|An OLE DB informational message is available.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Fuzzy match performance can be improved if the exact join FuzzyComparisonFlags on the input column "%1" are set to match with the default SQL collation for reference table column "%2".  It is also necessary that no fold flags are set in FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Fuzzy match performance can be improved if an index is created upon the reference table across all of the specified exact match columns.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|Error and truncation dispositions were not reviewed. Make sure this component is configured to redirect rows to error outputs, if you wish to further transform those rows.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|The Aggregate transformation has encountered %1!d! key combinations. It has to re-hash data because the number of key combinations is more than expected. The component can be configured to avoid data re-hash by adjusting the Keys, KeyScale, and AutoExtendFactor properties.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|The Aggregate transformation has encountered %1!d! distinct values while performing a "count distinct" aggregation on "%2". The transformation will re-hash data because the number of distinct values is more than expected. The component can be configured to avoid data re-hash by adjusting the CountDistinctKeys, CountDistinctKeyScale, and AutoExtendFactor properties.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|The processing of file "%1" has started.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|The processing of file "%1" has ended.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|The total number of data rows processed for file "%1" is %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|The final commit for the data insertion in "%1" has started.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|The final commit for the data insertion  in "%1" has ended.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! rows are added to the cache. The system is processing the rows.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|The %1 processed %2!u! rows in the cache. The processing time was %3 seconds. The cache used %4!I64u! bytes of memory.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|The %1 failed to process the rows in the cache.  The processing time was %2 second(s).|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|The %1 succeeded in preparing the cache. The preparation time was %2 seconds.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, and performed %4!I64u! lookups using partial cache.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, performed %4!I64u! lookups using partial cache and %5!I64u! lookups using the cache for rows with no matching entries in the initial lookup.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|The %1 is writing the cache to file "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|The %1 has written the cache to file "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|The Maximum insert commit size property of the OLE DB destination "%1" is set to 0. This property setting can cause the running package to stop responding. For more information, see the F1 Help topic for OLE DB Destination Editor (Connection Manager Page).|  
  
##  <a name="msgGeneral"></a> General and Event Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_MSG_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Incorrect function.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|The system cannot find the file specified.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Starting Microsoft SSIS Service.<br /><br /> Server version %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS Service started.<br /><br /> Server version %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|The wait operation timed out.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|No more data is available.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS Service failed to start.<br /><br /> Error: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Error stopping Microsoft SSIS Service.<br /><br /> Error: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS Service configuration file does not exist.<br /><br /> Loading with default settings.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS Service configuration file is incorrect.<br /><br /> Error reading config file: %1<br /><br /> Loading server with default settings.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS Service:<br /><br /> Registry setting specifying configuration file does not exist.<br /><br /> Attempting to load default config file.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS Service: stopping running package.<br /><br /> Package instance ID: %1<br /><br /> Package ID: %2<br /><br /> Package name: %3<br /><br /> Package description: %4<br /><br /> Package started by: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Package "%1" started.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Package "%1" finished successfully.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Package "%1" has been cancelled.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Package "%1" failed.|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|Module %1 cannot load DLL %2 to call entry point %3 because of error %4. The product requires that DLL to run, but the DLL could not be found on the path.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|Module %1 loaded DLL %2, but cannot find entry point %3 because of error %4. The named DLL could not be found on the path, and the product requires that DLL to run.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
  
##  <a name="msgSuccess"></a> Success Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] success messages begin with **DTS_S_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|The value is NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|The string value was truncated. The buffer received a string that was too long for the column, and the string was truncated by the buffer.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|A truncation occurred during evaluation of the expression. The truncation occurred during evaluation, which may include any point in an intermediate step.|  
  
##  <a name="msgPipeline"></a> Data Flow Component Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTSBC_E_**, where "BC" refers to the native base class from which most Microsoft data flow components are derived.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|The total number of outputs and error outputs, %1!lu!, is incorrect. There must be exactly %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Cannot retrieve output with index %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|The number of error outputs, %1!lu!,  is incorrect. There must be exactly %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Incorrect validation status value, "%1!lu! ".  It must be one of the values found in the DTSValidationStatus enumeration.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|The input "%1!lu!" has no synchronous output.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|The input "%1!lu!" has no synchronous error output.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|The HowToProcessInput value, %1!lu!, is not valid. It must be one of the values from the HowToProcessInput enumeration.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Failed to get information for row "%1!ld!", column "%2!ld!" from the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Failed to set information for row "%1!ld!", column "%2!ld!" into the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|The property "%1" is not valid.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|The property "%1" was not found.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Error assigning a value to the read-only property "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|The %1 does not allow the insertion of output columns.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|The output columns' metadata does not match the associated input columns' metadata.  The output columns' metadata will be updated.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|There are input columns that do not have associated output columns. The output columns will be added.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|There are output columns that do not have associated input columns. The output columns will be removed.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|The output columns' metadata does not match the associated input columns' metadata.  The input columns will be unmapped.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|There are input columns that do not have associated output columns. The input columns will be unmapped.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|There is an input column associated with an output column, and that output column is already associated with another input column on the same input.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|The %1 does not allow the insertion of external metadata columns.|  
  
  在 SQL Server 上，將資料夾 " %1\\\\ 重新命名為 `2" to "%1\\\\`3" 時發生錯誤。
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: sql
ms.prod_service: "integration-services"
ms.reviewer: ""
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords: 
  - "error numbers [Integration Services]"
  - "hresults [Integration Services]"
  - "errors [Integration Services], listed"
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
---
# Integration Services Error and Message Reference

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  The following tables list predefined [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] errors, warnings, and informational messages, in ascending numerical order within each category, along with their numeric codes and symbolic names. Each of these errors is defined as a field in the <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> class in the <xref:Microsoft.SqlServer.Dts.Runtime> namespace.  
  
 This list may be useful when you encounter an error code without its description. The list does not include troubleshooting information at this time.  
  
> [!IMPORTANT]  
>  Many of the error messages that you may see while working with [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] come from other components. In this topic, you will find all the errors raised by [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] components. If you do not see your error in the list, the error was raised by a component outside [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. These may include OLE DB providers, other database components such as the [!INCLUDE[ssDE](../includes/ssde-md.md)] and [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , or other services or components such as the file system, the SMTP server, Message Queuing (also known as MSMQ), and so forth. To find information about these external error messages, see the documentation specific to the component.  
  
 This list cadontains the following groups of messages:  
  
-   [Error Messages (DTS_E_*)](#msgError)  
  
-   [Warning Messages (DTS_W_*)](#msgWarning)  
  
-   [Informational Messages(DTS_I_*)](#msgInfo)  
  
-   [General and Event Messages(DTS_MSG_*)](#msgGeneral)  
  
-   [Success Messages(DTS_S_*)](#msgSuccess)  
  
-   [Data Flow Component Error Messages (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_E_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Overwriting Stored Procedure "%1" at destination.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|The data type "%1" found on column "%2" is not supported for the %3. This column will be converted to  DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|The column %1 in table %2 in the XML schema does not have a mapping in the external metadata columns.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|An internal object or variable was not initialized. This is an internal product error.  This error is returned when a variable should have a valid value but does not.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services evaluation period has expired.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|This property cannot be assigned a negative value. This error occurs when a negative value is assigned to a property that can only contain positive values, such as the COUNT property.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Indexes cannot be negative. This error occurs when a negative value is used as an index to a collection.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Invalid server name "%1". SSIS service does not support multi-instance, use just server name instead of "server name\instance".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Migration for VSA scripts can not be done on 64 bit platforms due to lack of Visual Tools for Applications designer support. Run the migration under WOW64 on 64 bit platforms.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|The command execution generated errors.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|To run a SSIS package outside of [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] you must install %1 of Integration Services or higher.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|The variable cannot be found. This occurs when an attempt is made to retrieve a variable from the Variables collection on a container during execution of the package, and the variable is not there. The variable name may have changed or the variable is not being created.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Error trying to write to a read-only variable, "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Unable to find the directories containing Tasks and Data Flow Task components. Check the integrity of your installation.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|Package name is too long. The limit is 128 characters. Shorten the package name.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|Package description is too long. The limit is 1024 characters. Shorten the package description.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments property is too long. The limit is 1024 characters. Try shortening the VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|The element cannot be found in a collection. This error happens when you try to retrieve an element from a collection on a container during execution of the package and the element is not there.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|The specified package could not be loaded from the SQL Server database.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|The variable value assignment is not valid. This error happens when the client or a task assigns a runtime object to a variable value.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Error assigning namespace to the variable. The namespace "System" is reserved for system use. This error happens when a component or task attempts to create a variable with a namespace of "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|The connection "%1" is not found. This error is thrown by Connections collection when the specific connection element is not found.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|The variable "%1" is a 64-bit integer variable, which is not supported on this operating system. The variable has been recast to 32-bit integer.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|An attempt change to a read-only attribute on variable "%1" occurred. This error happens when a read-only attribute for a variable is being changed at runtime. Read-only attributes can be changed only at design time.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Invalid attempt to set a variable to a container reference.  Variables are not allowed to reference containers.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Assigning invalid value or object to variable "%1". This error happens when a value is not appropriate for variables.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|One or more error occurred. There should be more specific errors preceding this one that explains the details of the errors. This message is used as a return value from functions that encounter errors.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Error getting or setting an array value. The type "%1" is not allowed. This occurs when loading an array into a variable.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Unsupported type in array. This happens when saving an array of unsupported types into a variable.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Error loading value "%1" from node "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|Node "%1" is not a valid node. This happens when saving fails.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Failed to load task "%1", type "%2". The contact information for this task is "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|Element "%1" does not exist in collection "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|The ObjectData element is missing in the XML block of a hosted object. This occurs when the XML parser attempts to locate the data element for an object and it cannot be found.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|The variable "%1" cannot be found. This error occurs when an attempt to retrieve a variable from a variables collection on a container during execution of the package occurs, and the variable is not there.  A variable name may have changed or the variable is not being created.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|The package cannot execute because it contains tasks that failed to load.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|The task has failed to load. The contact information for this task is "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Error loading task "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Error loading task. This happens when loading a task from XML fails.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|The %1 cannot write to the cache because %2 has already written to it.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Failed to prepare the cache for new data.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Failed to mark the cache as filled with data.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|The cache is not initialized and cannot be read by %1.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Failed to prepare the cache for providing data.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|The cache is being written to by %1, and cannot be read by %2.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|The cache is being read from %1 and cannot be written to by %2.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|The runtime object cannot be loaded from the specified XML node.  This happens when trying to load a package or other object from an XML node that is not of the correct type, such as a non-SSIS XML node.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Failed to open package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into the XML document. This can be the result of either providing an incorrect file name was specified when calling LoadPackage or the XML file was specified and has an incorrect format.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Failed to load XML due to error 0x%1!8.8X! "%2". This happens when loading a package and the file cannot be opened or loaded correctly into XML document.  This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Failed to load XML from package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Failed to open package file. This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Unable to decode a binary format in the package.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Unable to load the package as XML because of package does not have a valid XML format. A specific XML parser error will be posted.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Error loading from XML. No further detailed error information can be specified for this problem because no Events object was passed where detailed error information can be stored.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Cannot create an instance of the XML Document Object Model. MSXML may not be registered.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|The package cannot be loaded. This occurs when attempting to load an older version package, or the package file refers to an invalid structured object.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Failed to save package file.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Failed to save package file "%1" with error 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|The object must inherit from IDTSName100 and does not.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with package delimiter. There was no "\package" delimiter.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Failure exporting configuration file.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|Properties collection cannot be modified.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Unable to save configuration file. The file may be read only.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure property is not applicable to the package container.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|The task "%1" cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|Unable to save xml to "%1". The file may be read only.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Failed to convert a type in the configuration "%1" for the package path "%2".  This happens when a configuration value cannot be converted from a string to the appropriate destination type. Check the configuration value to ensure it can be converted to the type of the destination property or variable.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Configuration failure. This is a generic warning for all configuration types. Other warnings should precede this with more information.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Package failed validation from the ExecutePackage task. The package cannot run.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Failed to create mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" already exists and is owned by another user.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Failed to acquire mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Failed to release mutex "%1" with error 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|The wrappers task pointer is not valid. The wrapper has an invalid pointer to a task.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|The executable has been added to the Executables collection of another container. This occurs when a client tries to add an executable to more than one Executables collection. You need to remove the executable from the current Executables collection before attempting to add it.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|The connection type "%1" specified for connection manager "%2" is not recognized as a valid connection manager type. This error is returned when an attempt is made to create a connection manager for an unknown connection type. Check the spelling in the connection type name.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|An object was created but the attempt to add it to a collection failed. This can occur due to an out-of-memory condition.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|There was an error creating an Open Database Connectivity (ODBC) environment.|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|There was an error creating an Open Database Connectivity (ODBC) database connection.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|There was an error trying to establish an Open Database Connectivity (ODBC) connection with the database server.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|The qualifier is already set on this instance of the connection manager. The qualifier may be set once per instance.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|The qualifier has not been set on this instance of the connection manager. Setting the qualifier is required to complete initialization.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|This connection manager does not support specification of qualifiers.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Connection manager "0x%1" cannot be cloned for out-of-process execution.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|The log provider for SQL Server Profiler was unable to load pfclnt.dll. Please check that SQL Server Profiler is installed.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|The SSIS logging infrastructure failed with error code 0x%1!8.8X!. This error indicates that this logging error is not attributable to a specific log provider.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|The SSIS logging provider "%1" failed with error code 0x%2!8.8X! (%3).  This indicates a logging error attributable to the specified log provider.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|The SaveToSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|The LoadFromSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|The RemoveFromSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement that was issued has failed.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|The ExistsOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB has failed making a database connection when using the supplied connection string.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|When adding a precedence constraint, a From executable was specified that is not a child of this container.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|When adding a precedence constraint, the To executable specified is not a child of this container.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|There was an error trying enlist an ODBC connection in a transaction. The SQLSetConnectAttr failed to set the SQL_ATTR_ENLIST_IN_DTC attribute.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|The connection manager "%1" will not acquire a connection because the package OfflineMode property is TRUE. When the OfflineMode is TRUE, connections cannot be acquired.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|The SSIS Runtime has failed to start the distributed transaction due to error 0x%1!8.8X! "%2". The DTC transaction failed to start. This could occur because the MSDTC Service is not running.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|The SetQualifier method cannot be called on a connection manager during package execution. This method is used at design-time only.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Storing or modifying packages in SQL Server requires the SSIS runtime and database to be the same version. Storing packages in earlier versions is not supported.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Connection "%1" failed validation.|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|The file name "%1" specified in the connection was not valid.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Multiple file names cannot be specified on a connection when the Retain property is TRUE. Vertical bars were found on the connection string, meaning multiple file names are being specified and, in addition, the Retain property is TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|An ODBC error %1!d! has occurred.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|There was an error in the precedence constraint between "%1" and "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Failed to populate the ForEachEnumeratorInfos collection with native ForEachEnumerators with the following error code: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|The GetEnumerator method of the ForEach Enumerator has failed with error 0x%1!8.8X! "%2". This occurs when the ForEach Enumerator cannot enumerate.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|The raw certificate data cannot be obtained from the supplied certificate object (error: %1). This occurs when CPackage::put_CertificateObject cannot instantiate the ManagedHelper object, when the ManagedHelper object fails, or when the ManagedHelper object returns a malformed array.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Failed to create certificate context (error: %1). This occurs in CPackage::put_CertificateObject or CPackage::LoadFromXML when the corresponding CryptoAPI function fails.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Opening MY certificate store failed with error "%1".This occurs in CPackage::LoadUserCertificateByName and CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|The certificate specified by name in MY store cannot be found (error: %1). This occurs in CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Unable to find the specified certificate by hash in "MY" store (error: %1). Occurs in CPackage::LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|The hash value is not a one-dimensional array of bytes (error: %1). This occurs in CPackage::LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|The data in the array cannot be accessed (error: %1). This error can occur wherever GetDataFromSafeArray is called.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|The SSIS managed helper object failed during creation with error 0x%1!8.8X! "%2". This occurs whenever CoCreateInstance CLSID_DTSManagedHelper fails.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|The SSIS Runtime has failed to enlist the OLE DB connection in a distributed transaction with error 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Package signing failed with error 0x%1!8.8X! "%2". This occurs when the ManagedHelper.SignDocument method fails.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Failed to check for XML signature envelope in package XML with error 0x%1!8.8X! "%2". This occurs in CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Failed to obtain XML source from XML DOM object with error 0x%1!8.8X! "%2". This occurs when IXMLDOMDocument::get_xml fails.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|The cryptographic signature of the package failed verification due to error 0x%1!8.8X! "%2". This occurs when the signature verification operation fails.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Failed to obtain cryptographic key pair associated with the specified certificate with error 0x%1!8.8X! "%2". Verify that you have the key pair for which the certificate was issued. This error usually occurs when trying to sign a document using a certificate for which the person does not have the private key.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|The digital signature is not valid. The contents of the package have been modified.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|The digital signature is valid; however the signer is not trusted and, therefore, authenticity cannot be guaranteed.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|The connection does not support enlisting in distributed transaction.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Failed to apply package protection with error 0x%1!8.8X! "%2". This error occurs when saving to Xml.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Failed to remove package protection with error 0x%1!8.8X! "%2". This occurs in the CPackage::LoadFromXML method.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|The package is encrypted with a password. The password was not specified, or is not correct.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|A precedence constraint already exists between the specified executables. More than one precedence constraint is not allowed.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|The package failed to load due to error 0x%1!8.8X! "%2". This occurs when CPackage::LoadFromXML fails.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Failed to find package object in signed XML envelope with error 0x%1!8.8X! "%2". This occurs when signed XML does not contain a SSIS package, as expected.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|The lengths of parameter names, types, and descriptions arrays are not equal. The lengths must be equal. This occurs when the lengths of the arrays are mismatched. There should be one entry per parameter in each array.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|An OLE DB error 0x%1!8.8X! (%2) occurred while enumerating packages. A SQL statement was issued and failed.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|The log provider type "%1" specified for log provider "%2" is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|The log provider type is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|The connection type specified for connection manager is not a valid connection manager type. This error occurs when an attempt is made to create a connection manager for unknown connection type. Verify the spelling of the connection type name.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|An error was encountered when trying to remove the package "%1" from SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|An error was encountered when trying to create a folder on SQL Server named "%1" in folder "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|The CreateFolderOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement issued has failed.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|An error occurred when renaming folder " %1\\\\%2" to "%1\\\\%3" on SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|RenameFolderOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。 發出的 SQL 陳述式失敗。|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|刪除 SQL Server 資料夾 "%1" 時發生錯誤。|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|RemoveFolderOnSQLServer 方法發現 OLE DB 錯誤碼 0x%1!8.8X! (%2)。 發出的 SQL 陳述式失敗。|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|指定的封裝路徑未包含封裝名稱。 當路徑未至少包含一個反斜線或一個斜線時，就會發生這個問題。|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|找不到資料夾 "%1"。|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|嘗試在 SQL 上尋找資料夾時發現 OLE DB 錯誤，錯誤碼為 0x%1!8.8X! (%2)。|  
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
|0xC0016001|-1073651711|DTS_E_INVALIDURL|指定的 URL 無效。 當伺服器或 Proxy URL 為 Null 或格式不正確時，就會發生這個問題。 有效 URL 格式的形式是 https://ServerName:Port/ResourcePath 或 https://ServerName:Port/ResourcePath 。|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|URL %1 無效。 當指定 http 或 https 以外的配置或 URL 的格式不正確時，就會發生這個問題。 有效 URL 格式的形式是 https://ServerName:Port/ResourcePath 或 https://ServerName:Port/ResourcePath 。|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|無法建立與伺服器 %1 的連接。 當伺服器不存在或 Proxy 設定不正確時，就會發生這個錯誤。|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|已經重設或結束與伺服器的連接。 請稍後再試一次。|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|"%1" 的登入嘗試失敗。 當提供的登入憑證不正確時，就會發生這個錯誤。 請驗證登入認證。|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|無法解析 URL %1 中指定的伺服器名稱。|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Proxy 驗證失敗。 當未提供登入認證或認證不正確時，就會發生這個錯誤。|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|從伺服器取得的 SSL 憑證回應無效。 無法處理要求。|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|要求已逾時。當指定的逾時值太短時，或無法建立與伺服器或 Proxy 的連接時，就會發生這個錯誤。 請確定伺服器和 Proxy URL 都正確。|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|遺漏用戶端憑證。 當伺服器需要 SSL 用戶端憑證，但使用者提供無效的憑證或未提供憑證時，就會發生這個錯誤。 必須為這個連接設定用戶端憑證。|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|指定的伺服器 URL %1 有重新導向，但重新導向要求失敗。|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|伺服器驗證失敗。 當未提供登入認證或認證不正確時，就會發生這個錯誤。|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|無法處理要求。 請稍後再試一次。|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|伺服器傳回狀態碼 - %1!u! : %2。 當伺服器遇到問題時，就會發生這個錯誤。|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|WinHttp 服務不支援這個平台。|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|逾時值無效。 逾時值應該在 %1!d! 至 %2!d! 到 %2!d! (秒)。|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|區塊大小無效。 ChunkSize 屬性應該在 %1!d! 至 %2!d! 到 %2!d! (KB)。|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|處理用戶端憑證時發生錯誤。 在個人憑證存放區 (Personal Certificate Store) 找不到提供的用戶端憑證時，就會發生這個錯誤。 請確認用戶端憑證有效。|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|伺服器傳回錯誤碼「403 - 禁止」。 當指定的資源需要 "https" 存取時，但憑證有效期間已過期、憑證在要求的用途上無效、憑證已撤鎖或無法檢查撤銷時，就會發生這個錯誤。|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|使用 Proxy "%1" 初始化 HTTP 工作階段時發生錯誤。 當指定無效的 Proxy 時，就會發生這個錯誤。 HTTP 連接管理員僅支援 CERN 類型 Proxy。|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|開啟憑證存放區時發生錯誤。|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|無法將保護的 XML 節點 "%1" 解密，錯誤為 0x%2!8.8X! 失敗。 您可能沒有存取這項資訊的權限。 當發生密碼編譯錯誤時，就會發生這個錯誤。 請確認有正確的金鑰。|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|無法將伺服器 "%1" 的受保護連接字串解密，錯誤為 0x%2!8.8X! 失敗。 您可能沒有存取這項資訊的權限。 當發生密碼編譯錯誤時，就會發生這個錯誤。 請確認有正確的金鑰。|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|版本號碼不可以是負值。 當封裝的 VersionMajor、VersionMinor 或 VersionBuild 屬性設定為負值時，就會發生這個錯誤。|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|封裝在載入期間已移轉至較新版本。 必須重新載入，才能完成處理程序。 此為內部錯誤碼。|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|封裝從 %1!d! 版本移轉至 %2!d! 版本 失敗，錯誤為 0x%3!8.8X! "%4"。|  
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
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|檢查點檔案 "%1" 在建立時失敗，因為發生錯誤 0x%2!8.8X! 失敗。|  
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
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|值索引是負值。 ForEach Variable 對應數字 %1!d! 至變數 "%2"。|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|無法套用 ForEach Variable 對應數字 %1!d! 至變數 "%2"。|  
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
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|嘗試載入 XML 檢查點檔案 "%1" 失敗，錯誤為 0x%2!8.8X! 失敗。 請確認指定的檔案名稱正確，且檔案存在。|  
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
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|物件名稱 "%1" 無效。 名稱不能包含下列任何字元: / \ : ? " < > &#124;|  
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
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|在工作上的 Execute 方法傳回錯誤碼 0x%1!8.8X! (%2)。 Execute 方法必須成功，並使用 "out" 參數表示結果。|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|工作 "%1"失敗：0x%2!8.8X! 。 發生錯誤時，執行階段正從工作的相依性集合擷取相依性。 工作可能未正確實作其中一個相依性介面。|  
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
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|訊息佇列逾時。未收到任何訊息。|  
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
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|使用者介面初始化：工作為 Null。|  
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
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|符合 U.S. 規範的系統上不允許要求的作業。FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|執行查詢 "%1" 失敗，發生下列錯誤: "%2"。 可能的失敗原因：查詢發生問題、未正確設定 "ResultSet" 屬性、未正確設定參數，或未正確建立連接。|  
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
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|緩衝區類型 %1!d! 的大小為 %2!I64d! 位元組 。|  
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
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|資料流程工作無法註冊緩衝區類型。 類型具有 %1!d! 個資料行，且已用於 %2!d!. 執行樹狀目錄。|  
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
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|資料流程工作無法註冊檢視緩衝區類型。 類型具有 %1!d! 個資料行，且已用於輸入識別碼 %2!d!。|  
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
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|緩衝區識別碼 %1!d! 支援其他虛擬緩衝區，但無法設定為循序模式。 在支援虛擬緩衝區的緩衝區上呼叫 IDTSBuffer100.SetSequentialMode。|  
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
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!" 無法快取 Variables 集合，傳回錯誤碼 0x%2!8.8X。|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1" 無法快取元件中繼資料物件，傳回錯誤碼 0x%2!8.8X!。|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" 具有非零的 SortKeyPosition，但值 (%2!ld!) 太大。 必須小於或等於資料行數目。|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|%1 的 IsSorted 屬性設定為 TRUE，但非零輸出資料行 SortKeyPositions 的絕對值，未形成從 1 開始的單純遞增序列。|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" 驗證失敗，傳回驗證狀態 "%2"。|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|元件 "%1!s!" 無法建立，傳回錯誤碼 0x%2!8.8X! "%3!s!"。 請確定元件已正確註冊。|  
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
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|對函數 "%2" 而言，長度 %1!d! 無效。 長度參數不可以是負數。 請將長度參數變更為零或正值。|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|函數 "%2" 的起始索引 %1!d! 無效。 起始索引值必須是大於 0 的整數。 起始索引以一為基底，不是以零為基底。|  
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
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|運算式包含無法辨識的 Token "%1"。 如果 "%1" 是變數，則必須以 "\@%1" 表示。 指定的 Token 無效。 如果 Token 要作為變數名稱，則必須以 \@ 符號為前置詞。|  
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
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal escape sequence of "\\%2!c!". The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, use a double backslash, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" contains no output columns. An asynchronous output must contain output columns.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|The "%1" has a long object data type of DT_TEXT, DT_NTEXT, or DT_IMAGE, which is not supported.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Output ID %1!d! was given multiple error output configurations. First %2!d! and %3!d!, then %4!d! and %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|The OLE DB provider failed during the data type conversion verification for "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|This buffer represents the end of the rowset and its row count cannot be altered.  An attempt was made to call AddRow or RemoveRow on a buffer that has the end of rowset flag.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|The data type "%1" is not supported in an expression. The specified type is not supported or is not valid.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|The PrimeOutput method on "%1" returned success, but did not report an end of the rowset. There is an error in the component. It should have reported an end-of-row. The pipeline will shut down execution to avoid unpredictable results.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|An overflow occurred while converting from data type "%1" to data type "%2". The source type is too large for the destination type.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|Conversion from data type "%1" to data type "%2" is unsupported. The source type cannot be converted to the destination type.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Error code 0x%1!8.8X! occurred attempting to convert from data type %2 to data type %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|The conditional operation "%1" failed with error code 0x%2!8.8X!. There was an internal error or an out-of-memory error.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Casting expression "%1" from data type "%2" to data type "%3" failed with error code 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Evaluating function "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Parameter number %1!d! of the function "%2" cannot be converted to a static value.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|The error row disposition on "%1" cannot be set to redirect the row when the fast load option is turned on, and the maximum insert commit size is set to zero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|The code pages for operands of binary operator "%1" for type "%2" must match. Currently, the code page of the left operand does not match the code page of the right operand. For the specified binary operator on the specified type, the code pages must be the same.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Retrieving the value of Variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|The data type of variable "%1" is not supported in an expression.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Unable to cast expression "%1" from data type "%2" to data type "%3" because the code page of the value being cast (%4!d!) does not match the requested result code page (%5!d!). The code page of the source must match the code page requested for the destination.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|The default buffer size must be between %1!d! and %2!d! bytes. An attempt was made to set the DefaultBufferSize property to a value that is too small or too large.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|The default buffer maximum rows must be larger than %1!d! rows. An attempt was made to set the DefaultBufferMaxRows property to a value that is too small.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|The code page on %1 is %2!d! and is required to be %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Failed to assign %3!d! to the EngineThreads property of the Data Flow task. The value must be between %1!d! and %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Parsing the expression "%1" failed. The single quotation mark at line number "%2", character number "%3", was not expected.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Parsing the expression "%1" failed. The equal sign (=) at line number "%2", character number "%3", was not expected. A double equals sign (==) may be required at the location specified.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|Component "%1" failed to cache the runtime object reference tracker collection and returned error code 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|There are multiple input columns with the name "%1". The desired input column must be specified uniquely as [Component Name].[%2] or referenced by lineage ID. Currently, the input column specified exists on more than one component.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Locating the input column named "[%1].[%2]" failed with error code 0x%3!8.8X!. The input column was not found in the input column collection.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|There are multiple variables with the name "%1". The desired variable must be specified uniquely as \@[Namespace::%2]. The variable exists in more than one namespace.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|The Data Flow engine scheduler failed to reduce the execution plan for the pipeline. Set the OptimizedMode property to false.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|The function SQRT cannot operate on negative values, and a negative value was passed to the SQRT function.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|The function LN cannot operate on zero or negative values, and a zero or negative value was passed to the LN function.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|The function LOG cannot operate on zero or negative values, and a zero or negative value was passed to the LOG function.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|The parameters passed to the function POWER cannot be evaluated and yield an indeterminate result.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|The runtime cannot provide a cancel event because of error 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|The pipeline received a request to cancel and is shutting down.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|The result of the unary minus (negation) operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|The placeholder "%1" was found in an expression. This must be replaced with an actual parameter or operand.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|The length %1!d! specified for function "%2" is negative, and is not valid. The length parameter must be positive.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|The repeat count %1!d! is negative and is not valid for function "%2". The repeat count parameter cannot be negative.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Reading the variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|For operands of a binary operation, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used in a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count %1!d! is not valid for function "%2". This parameter must be greater than zero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" failed to cache the LogEntryInfos collection and returned error code 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|The date part parameter specified for function "%1" is not valid. It must be a static string.  The date part parameter cannot contain dynamic elements, such as input columns, and must be of type DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|The value %1!d! specified for the length parameter of the cast to data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|The value %1!d! specified for the code page parameter of the NULL function with data type "%2" is not valid. The code page is not installed on the computer.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|The value %1!d! specified for the precision parameter of the NULL function with data type "%2" is out of range. Precision must be in the range %3!d! to %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|The value %1!d! specified for the scale parameter of the NULL function with data type %2 is out of range. Scale must be in the range %3!d! to %4!d!. Scale must not exceed precision and must not be negative.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|The value %1!d! specified for the length parameter of the "NULL" function with data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|The %1 can't be assigned a negative value.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|The "%1" custom property for "%2" cannot be set to true.  The column data type must be one of the following:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2, or DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|The "%1" cannot be reattached. Delete the path, add a new one, and attach it.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|The function "%1" requires %2!d! parameters, not %3!d! parameter. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|The function "%1" requires %2!d! parameter, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|The function "%1" requires %2!d! parameters, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Attempt to parse the expression "%1" failed because there was an out-of-memory error.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|The %1 failed to be able to perform its required product level check and returned error code 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS Error Code DTS_E_PRODUCTLEVELTOLOW.  The %1 cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|A string literal in the expression exceeds the maximum allowed length of %1!d! characters.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|The variable %1 contains a string that exceeds the maximum allowed length of %2!d! characters.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|The %1 was found, but it does not support a required Integration Services interface (IDTSRuntimeComponent100).  Obtain an updated version of this component from the component provider.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|The registry key "%1" cannot be opened.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Cannot get the file name for the component with a CLSID of "%1". Verify that the component is registered properly or that the CLSID provided is correct.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|The CLSID for one of the components is not valid. Verify that all the components in the pipeline have valid CLSIDs.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|The CLSID for one of the components with ID %1!d! is not valid.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|The index is not valid.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|The Application object cannot be accessed. Verify that SSIS is correctly installed.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Retrieving the file name for a component failed with error code 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Cannot retrieve property "%1" from component with ID %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Attempting to use ID %1!d! more than once in the Data Flow Task.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Cannot retrieve an item by lineage ID from a collection that does not contain columns.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Cannot find the connection manager with ID "%1" in the connection manager collection due to error code 0x%2!8.8X!. That connection manager is needed by "%3" in the connection manager collection of "%4". Verify that a connection manager in the connection manager collection, Connections, has been created with that ID.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|Thread "%1" received a buffer for input %2!d!, but this thread is not responsible for that input. An error occurred, causing the Data Flow engine scheduler to build a bad execution plan.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|The component "%1" (%2!d!) cannot provide an IDTSRuntimeComponent100 interface.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|The Data Flow task engine attempted to copy a buffer to assign another thread, but failed.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|The Data Flow task engine failed to create a view buffer of type %1!d! over type %2!d! for buffer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|The buffer manager attempted to push an error row to an output that was not registered as an error output. There was a call to DirectErrorRow on an output that does not have the IsErrorOut property set to TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|A call was made to a buffer method on a private buffer and private buffers do not support this operation.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Private mode buffers do not support this operation.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|This operation cannot be called on a buffer passed to PrimeOutput. A call was made to a buffer method during PrimeOutput, but that call is not allowed during PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|This operation cannot be called on a buffer passed to ProcessInput. A call was made to a buffer method during ProcessInput, but that call is not allowed during ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|The code encountered a column that was too wide.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Cannot get the ID of the runtime connection manager specified by "%1" in the connection manager collection, Connections, of "%2" due to error code 0x%3!8.8X!. Verify that the ConnectionManager.ID property of the runtime connection object has been set for the component.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|The "%1" in the connection manager collection, Connections, of "%2" does not have a value for the ID property. Verify that the ConnectionManagerID property of the runtime connection object has been set for the component.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Metadata cannot be changed during execution.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|The component metadata for "%1" could not be upgraded to the newer version of the component. The PerformUpgrade method failed.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|The version of %1 is not compatible with this version of the DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|The component is missing, not registered, not upgradeable, or missing required interfaces. The contact information for this component is "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|The method was called on the wrong buffer. Buffers that are not used for component output do not support this operation.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|An error occurred during computation of the expression.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Division by zero occurred in the expression.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|The magnitude of the literal value was too big to fit in the type requested.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|The result of a binary operation was too big for the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|The magnitude of the result of a binary operation overflows the maximum size for result data type.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|The magnitude of the result of a function call was too big to fit in the result type, and overflowed the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Incompatible data types were used with a binary operator. The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|An unsupported data type was used with a binary operator. The type of one, or both, of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator. The operands for this operator must be both positive or both negative.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|A binary operation failed. There was an out-of-memory condition, or an internal error occurred.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Setting the result type of a binary operation failed.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Cannot compare two strings.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|An unsupported data type is used with a unary operator. The operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|A unary operation failed. An out-of-memory condition occurred, or there was an internal error.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Setting the result type of a unary operation failed.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|A function has a parameter with an unsupported data type. The type of the parameter cannot be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|An invalid function name appeared in the expression. Verify that the function name is correct and does exist.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|The length parameter was not valid for function SUBSTRING. The length parameter cannot be negative.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|The start index was not valid for function SUBSTRING. The start index value must be an integer greater than zero. The start index is 1-based, not 0-based.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|An incorrect number of parameters was given to a function. The function name was recognized, but the number of parameters was not correct.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|A character mapping function failed.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|An unrecognized date part parameter was specified for a date function.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|An invalid parameter was given for function NULL. The parameters of NULL must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|An invalid parameter was given for function NULL. A parameter of NULL must be an integer, or a type that can be converted to an integer.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|An invalid parameter was given for a function. This parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|An invalid parameter was given for a cast operation. Parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|An invalid parameter was given for a cast operation. A parameter of a cast operator must be an integer, or a type that can be converted to an integer.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|The expression contained an unsupported type cast.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|The expression contained a token that was not recognized. The expression could not be parsed because it contains invalid elements.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|The expression is not valid and could not be parsed. It might contain invalid elements, or it might not be well-formed.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|The result of a unary minus (negation) operation overflowed the maximum size for result data type. The magnitude of the result of the operation overflows the type of the result.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Attempt to compute the expression failed.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Cannot convert the expression result data type to the column data type. The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression of the conditional operator has invalid data type. The conditional expression must be of type DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|The data types of the operands of the conditional operator were incompatible. The operand types could not be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Setting the result type of a conditional operation failed.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|The input column specified was not found in the input column collection.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Attempt to find an input column by lineage ID failed. The input column was not found in the input column collection.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|The expression contains an unrecognized token that appears to be an input column reference, but the input column collection is not available to process input columns. The input column collection has not been provided to the expression evaluator, but an input column was included in the expression.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|A variable specified was not found in the collection. It might not exist in the correct scope. Verify that the variable exists and that the scope is correct.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Attempt to parse the expression failed. The expression contains an invalid or incomplete token. It may contain invalid elements, be missing part of a required element such as closing parentheses, or may not be well formed.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|The value specified for the code page parameter of the cast to data type DT_STR or DT_TEXT is not valid. The specified code page is not installed on the computer.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|The value specified for the precision parameter of a cast operation is out of range for the type cast.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|The value specified for the scale parameter of a cast operation is out of range for the type cast. Scale must not exceed precision and must not be negative.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|The code pages do not match in a conditional operation. The code page of the left operand does not match the code page of the right operand. For the conditional operator of that type, the code pages must be the same.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|A string literal contains an illegal hexadecimal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. Hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|The string literal contains an illegal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, format it as a double backslash, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|An unsupported or unrecognized data type was used in the expression.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|An overflow occurred while converting between data types. The source type is too large to fit in the destination type.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|The expression contains an unsupported data type conversion. The source type cannot be converted to the destination type.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|An error occurred while attempting to perform data conversion. The source type could not be converted to the destination type.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|The conditional operation failed.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|An error occurred while attempting to perform a type cast.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting "%1" from type DT_STR to type DT_WSTR failed with error code 0x%2!8.8X!. An error occurred while performing the implicit conversion on the input column.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting an input column from type DT_STR to type DT_WSTR failed. An error occurred while performing the  implicit conversion on the input column.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|An error occurred while evaluating the function.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|A function parameter cannot be converted to a static value. The parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|The length parameter is not valid for function RIGHT. The length parameter cannot be negative.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|The repeat count parameter is not valid for function REPLICATE. This parameter cannot be negative.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|The code pages do not match in a binary operation. The code page of the left operand does not match the code page of the right operand. For this binary operation, the code pages must be the same.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Retrieving the value for a variable failed.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|The expression contains a variable with an unsupported data type.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Unable to cast the expression because the code page of the value being cast does not match the requested result code page. The code page of the source must match the code page requested for the destination.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|The expression contains an unexpected single quotation mark. A double quotation mark may be required.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|The expression contains an unexpected equal sign (=). This error usually occurs when a double equals sign (==) is needed.|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|An ambiguous input column name was specified.  The column must be qualified as [Component Name].[Column Name] or referenced by lineage ID. This error occurs when the input column exists on more than one component, and must be differentiated by the addition of component name or by using the lineage ID.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|A placeholder function parameter or operand was found in an expression. This should be replaced with an actual parameter or operand.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|An ambiguous variable name was specified. The desired variable must be qualifed as \@[Namespace::Variable]. This error occurs when the variable exists in more than one namespace.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|For operands of binary operation, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count parameter is not valid for function FINDSTRING. This parameter must be greater than zero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|The "date part" parameter specified for a date function is not valid. "Date part" parameters must be static strings, and cannot contain dynamic elements such as input columns. They must be of type DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|The value specified for the length parameter of a cast operation is not valid. The length must be positive. The length specified for the type cast is negative. Change to a positive value.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|The value specified for the length parameter of a NULL function is not valid. The length must be positive. The length specified for the NULL function is negative. Change to a positive value.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|The value specified for the code page parameter of the NULL function with data type DT_STR or DT_TEXT is not valid. The code page specified is not installed on the computer. Either change the code page that is specified, or install the code page on the computer.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|The value specified for the precision parameter of a NULL function is not valid. The precision that was specified is out of range for the NULL function.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|The value specified for the scale parameter of a NULL function is not valid. The scale that was specified is out of range for the NULL function. Scale must not exceed precision and must be positive.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|The %1 failed attempting to write data to %2 on %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|Lookup transform has received a cancel request from the user.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|Processing of character or binary large object (LOB) data has stopped because the 4-GB limit was reached.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|The managed pipeline component "%1" could not be loaded.  The exception was: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS Error Code DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: The Excel Connection Manager is not supported in the 64-bit version of SSIS, as no OLE DB provider is available.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|The cache file is damaged, or the file was not created by using the Cache connection manager.  Provide a valid cache file.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|The SQL command has not been set correctly. Check SQLCommand property.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|COM error object information is available.  Source: "%1"  error code: 0x%2!8.8X!  Description: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Unable to access the acquired connections.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|The number of columns is incorrect.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Column "%1" cannot be found at the datasource.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|An OLE DB record is available.  Source: "%1"  Hresult: 0x%2!8.8X!  Description: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS Error Code DTS_E_OLEDBERROR.  An OLE DB error has occurred. Error code: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|Component is already connected. The component needs to be disconnected before attempting to connect it.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|The value of the property "%1" is incorrect.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Cannot open the datafile "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|No destination flat file name was provided. Make sure the flat file connection manager is configured with a connection string. If the flat file connection manager is used by multiple components, ensure that the connection string contains enough file names.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|The text qualifier for column "%1" cannot be found.|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|Conversion from "%1" to "%2" is not supported.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|The error code 0x%1!8.8X! was returned when validating type conversion from %2 to %3.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Cannot find input column with lineage ID "%1!d!" which is needed by "%2". Check SourceInputColumnLineageID custom property of the output column.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be at least %1!d! outputs.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be exactly %1!d! output(s).|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|A string was too long to be converted.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|The number of inputs is incorrect. There must be exactly %1!d! inputs.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|The number of input columns for %1 cannot be zero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|This component has %1!d! inputs.  No input is allowed on this component.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput was called with an invalid input ID of %1!d!.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|The custom property "%1" needs to be of type %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|The buffer type is not valid. Make sure the Pipeline layout and all components pass validation.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|The value for custom property "%1" is incorrect.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|An error occurred due to no connection. A connection is required when requesting metadata. If you are working offline, uncheck Work Offline on the SSIS menu to enable the connection.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|The custom property "%1" cannot be created.|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|The custom property collection cannot be retrieved for initialization.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Cannot create an OLE DB accessor. Verify that the column metadata is valid.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput was called with an invalid output ID of %1!d!.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|The value for property "%1" on "%2" is not valid.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|A connection is required to read data.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|An error occurred while reading header rows.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Duplicate column name "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Cannot get the name of the column with ID %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Direct row to output "%1" (%2!d!) failed.|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Cannot create the bulk insert thread due to error "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|The thread for the SSIS Bulk Insert task failed initialization.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|The thread for the SSIS Bulk Insert task is already running.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|The thread for the SSIS Bulk Insert task terminated with errors or warnings.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Failed to open a fastload rowset for "%1". Check that the object exists in the database.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Error due to no connection. A connection is required before metadata validation can proceed.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|A destination table name has not been provided.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|The OLE DB provider used by the OLE DB adapter does not support IConvertType. Set the adapter's ValidateColumnMetaData property to FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|The OLE DB provider used by the OLE DB adapter cannot convert between types "%1" and "%2" for "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Column metadata validation failed.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" is a row ID column and cannot be included in a data insertion operation.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Attempting insertion into the row version column "%1". Cannot insert into a row version column.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Failure inserting into the read-only column "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Unable to retrieve column information from the data source. Make sure your target table in the database is available.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|A buffer could not be locked. The system is out of memory or the buffer manager has reached its quota.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|The %1 has a ComparisonFlags property that includes extra flags with the value %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|The column metadata was unavailable for validation.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|Cannot write to the data file.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|The column delimiter for column "%1" was not found.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Failed to parse the column "%1" in the data file.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|The file name is not properly specified.  Supply the path and name to the raw file either directly in the FileName property or by specifying a variable in the FileNameVariable property.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|File "%1" cannot be opened for writing. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|An I/O buffer cannot be created for the output file. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|Cannot write %1!d! bytes to file "%2". See previous error messages for details.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Encountered bad metadata in file header. The file is damaged or not a SSIS-produced raw data file.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Error occurred because the output file already exists and the WriteOption is set to Create Once. Set the WriteOption property to Create Always, or delete the file.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Error caused by conflicting property settings. Both the AllowAppend property and the ForceTruncate property are set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|The file had bad version and flags information. The file is damaged or not a SSIS-produced raw data file.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|The output file was written by an incompatible version and cannot be appended. The file may be an older file format that is no longer useable.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Cannot append output file because no column in the existing file matches column "%1" from the input. Old file does not match in metadata.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Cannot append output file because the number of columns in the output file does not match the number of columns in this destination. The old file does not match in metadata.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|There was an error retrieving column code page information.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Cannot read %1!d! bytes from file "%2". The cause of the failure should have been previously reported.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Unexpected end-of-file encountered while reading %1!d! bytes from file "%2". The file ended prematurely because of an invalid file format.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|The column %1 cannot be used. The raw adapters do not support image, text, or ntext data.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|The adapter encountered an unrecognized data type of %1!d!. This could be caused by a damaged input file (source) or by an invalid buffer type (destination).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|String too long. The adapter read a string that was %1!d! bytes long, and expected a string no longer than %2!d! bytes, at offset %3!d!. This could indicate a damaged input file. The file shows a string length that is too large for the buffer column.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|The raw adapter attempted to skip %1!d! bytes in the input file for unreferenced column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|The raw adapter attempted to read %1!d! bytes in the input file for column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|The file name property is not valid. The file name is a device or contains invalid characters.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Unable to prepare the SSIS bulk insert for data insertion.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|Database object name "%1" is not valid.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Order clause is not valid.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|File "%1" cannot be opened for reading. Error may occur when there are no privileges or the file is not found. Exact cause is reported in previous error message.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Unable to create the Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Unable to configure the Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Unsupported datatype for column %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|The attempt to read from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|The attempt to read column "%2!d!" data from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%2!8.8X!.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|The VariableName property is not set to the name of a valid variable. Need a runtime variable name to write to.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Unable to create or configure the ADODB.Recordset object.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Error writing to the ADODB.Recordset object.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|The file name is not valid. The file name is a device or contains invalid characters.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|The file name "%1" is not valid. The file name is a device or contains invalid characters.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Unable to retrieve destination column descriptions from the parameters of the SQL command.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Parameters are not bound. All parameters in the SQL command must be bound to input columns.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|The PivotUsage value for the input column "%1" (%2!d!) is not valid.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys found. Only one input column can be used as the Pivot Key.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|No Pivot Key found. One input column must be used as the Pivot Key.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|More than one output column (such as "%1" (%2!d!)) is mapped to input column "%3" (%4!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Output column "%1" (%2!d!) cannot be mapped to PivotKey input column.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|Output column "%1" (%2!d!) has a SourceColumn %3!d! that is not a valid input column lineage ID.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column, but its PivotKeyValue property value is missing.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column with a non-unique PivotKeyValue property value.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|Input column "%1" (%2!d!) is not mapped to any output column.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Failure occurred while comparing values for the set keys.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|The Input column "%1" (%2!d!) cannot be used as a Set Key, Pivot Key, or Pivot Value because it contains long data.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Incorrect output type. The output column "%1" (%2!d!) must have the same data type and metadata as the input column to which it is mapped.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Failure when trying to pivot the source records.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|The pivot key value "%1" is not valid.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|An error occurred while skipping data rows.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|An error occurred while processing file "%1" on data row %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|An error occurred while initializing the flat file parser.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Unable to retrieve column information from the flat file connection manager.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Failed to write out column name for column "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|The column type for column "%1" is incorrect. It is type "%2". It can only be either "%3" or "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|The attempt to write data of %1!d! bytes into the disk I/O failed. The disk I/O buffer has %2!d! free bytes.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|An error occurred while writing out the file header.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|An error occurred while getting the file size for file "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|An error occurred while setting the file pointer for file "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|An error occurred while setting up the disk I/O buffer.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|The column data for column "%1" overflowed the disk I/O buffer.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|An unexpected disk I/O error occurred while reading the file.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|An disk I/O time out occurred while reading the file.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|The Usage Type specified for the input columns to this transform cannot be read/write. Change the Usage Type to be read-only.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Cannot copy or convert flat file data for column "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Data conversion failed. The data conversion for column "%1" returned status value %2!d! and status text "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|The Variables collection is not available.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|Duplicate PivotKeyValue. Input column "%1" (%2!d!) is mapped to a Pivoted Value output column and has a non-unique PivotKeyValue.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|No unpivot destination found. At least one input column must be mapped with a PivotKeyValue to an DestinationColumn in the output.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue is not valid. In an UnPivot transform with more than one unpivoted DestinationColumn, the set of PivotKeyValues per destination must match exactly.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Incorrect UnPivot metadata. In an UnPivot transform, all input columns with a PivotKeyValue that is set, and are pointing to the same DestinationColumn, must have metadata that exactly matches the DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Cannot convert the pivot key value "%1" to the data type of the pivot key column.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys specified. Only one output column can be used as the Pivot Key.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|Output column "%1" (%2!d!) is not mapped by any input column's DestinationColumn property.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|No output column is marked as the PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|Input column "%1" (%2!d!) has a DestinationColumn property value that does not refer to a valid output column LineageID.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Duplicate destination error. More than one non-pivoted input column is mapped to the same destination output column.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|No input columns found. At least one input column must be mapped to an output column.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|The number of input and output columns are not equal. The total number of input columns on all inputs must be the same as the total number of output columns.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|The input is not sorted. The "%1" must be sorted.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|The JoinType custom property for the %1 contains a value of %2!ld!, which is not valid. Valid values are 0 (full), 1 (left), or 2 (inner).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|The NumKeyColumns value is not valid. In the %1, the value for the NumKeyColumns custom property must be between 1 and %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|No key columns are found. The %1 must have at least one column with a SortKeyPosition that is non-zero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Not enough key columns. The %1 must have at least %2!ld! columns with non-zero SortKeyPosition values.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Datatype mismatch occurred. The datatypes for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|The column with the SortKeyPosition value of %1!ld! is not valid. It should be %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Sort direction mismatch. The sort directions for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Missing column. The %1 must have an associated input column.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Input columns must have output columns. There are input columns with a usage type of read-only that do not have associated output columns.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags are not zero. The comparison flags for non-string columns must be zero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|The comparison flags for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Unrecognized pivot key value.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|Lineage item value %1!ld! is not valid. The valid range is between %2!ld! and %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Input columns not allowed. The number of input columns must be zero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|The datatype for "%1" is not valid for the specified lineage item.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|The length for "%1" is not valid for the specified lineage item.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|The metadata for "%1" does not match the metadata for the associated output column.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|There are output columns that have SortKeyPosition values that don't match the associated input columns' SortKeyPosition.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|The attempt to add a row to the Data Flow task buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Data conversion failed while converting column "%1" (%2!d!) to column "%3" (%4!d!).  The conversion returned status value %5!d! and status text "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|The attempt to allocate a row handle buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|The attempt to send a row to SQL Server failed with error code 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|The attempt to prepare the buffer status failed with error code 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|The attempt to retrieve the start of the buffer row failed with error code 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|The thread for the SSIS Bulk Insert is no longer running.  No more rows can be inserted. Try increasing the bulk insert thread timeout.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|The source file is not valid. The source file is returning a count of more than 131,072 columns. This usually occurs when the source file is not produced by the raw file destination.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|The %1 is an extra unattached input and will be removed.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|The %1 is not attached but is not marked as dangling.  It will be marked as dangling.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Duplicate pivot key value "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Duplicate pivot key value.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Failure retrieving component locale ID. Error code 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Mismatched locale IDs. The component locale ID (%1!d!) does not match the connection manager locale ID (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|The component locale ID has not been set. Flat file adapters need to have the locale ID on the flat file connection manager set.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|The binary field is too large. The adapter attempted to read a binary field that was %1!d! bytes long, but expected a field no longer than %2!d! bytes at offset %3!d!. This usually occurs when the input file is not valid. The file contains a string length that is too large for the buffer column.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|The percentage, %2!ld!, is not valid for the "%1" property. It must be between 0 and 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|The number of rows, %2!ld!, is not valid for the "%1" property. It must be greater than 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|The adapter was asked to write a string that was %1!I64d! bytes long, but all data must be less than 4294967295 bytes in length.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|No inputs were mapped to an output. The "%1" must have at least one input column mapped to an output column.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|Conversion from "%1" with code page %2!d! to "%3" with code page %4!d! is not supported.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|The external metadata column mapping for %1 is not valid.  The external metadata column ID cannot be zero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|The %1 is mapped to an external metadata column that does not exist.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Writing long object data of type DT_TEXT, DT_NTEXT, or DT_IMAGE to Data Flow task buffer failed for column "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Opening a rowset for "%1" failed. Check that the object exists in the database.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Accessing variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|The connection manager "%1" is not found. A component failed to find the connection manager in the Connections collection.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|The upgrade from version "%1" to version %2!d! failed.|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|A value in an input column is too large to be stored in the ADODB.Recordset object.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Columns "%1" and "%2" cannot convert between unicode and non-unicode string data types.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|The variable "%1" specified by VariableName property is not a valid variable. Need a valid variable name to write to.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|The variable "%1" specified by VariableName property is not an integer. Change the variable to be of type VT_I4, VT_UI4, VT_I8, or VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|No column was specified to allow the component to advance through the file.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|The "%1" has IsSorted set to TRUE, but the SortKeyPosition on all output columns are zero. Either change the IsSorted to FALSE, or select at least one output column to contain a non-zero SortKeyPosition.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|The "%1" metadata does not match the metadata of the input column.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|The value of the specified variable cannot be located, locked, or set.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|The column "%1" cannot be processed because more than one code page (%2!d! and %3!d!) are specified for it.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|The column "%1" can't be inserted because the conversion between types %2 and %3 is not supported.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Column "%1" cannot convert between unicode and non-unicode string data types.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|The %1 cannot find the column with LineageID %2!ld! in its input buffer.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|The %1 cannot get the column information for column %2!lu! from its input buffer.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|The %1 cannot get the column information for column "%2!lu!" from its copy buffer.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|The %1 cannot register a buffer type for its copy buffer.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|The %1 cannot create a buffer to copy its data into for sorting.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader client has failed to call Read or has closed the DataReader.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|No column information was returned by the SQL command.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|The %1 was unable to retrieve column information for the SQL command. The following error occurred: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|A source table name has not been provided.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|The cache index position, %1!d!, is not valid. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|The index position, %1!d!, is a duplicate. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|At least one index column should be specified for the Cache connection manager. To specify an index column, set the Index Position property of the cache column.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Cache index positions must be contiguous. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|The property "%1" cannot be set on "%2". The property being set is not supported on the specified object. Check the property name, case, and spelling.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|The property type cannot be changed from the type that was set by the component.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Output ID %1!d! failed during insert. The new output was not created.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Cannot delete output ID %1!d! from the output collection.  The ID may not be valid, or the ID may have been the default or error output.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Failed to set property "%1" on "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Failed to set the type of %1 to type: "%2", length: %3!d!, precision: %4!d!, scale: %5!d!, codepage: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|More than one error output was found on the component, and there can be only one.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|The property on an output column cannot be set.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|The data type for "%1" cannot be modified in the error "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|The "%1" cannot have its IsSorted property set to TRUE because it is not a source output. A source output has a SynchronousInputID value of zero.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|The "%1" cannot have a SortKeyPosition property set to non-zero because "%2" is not a source output. The output column "colname" (ID) cannot have its SortKeyPosition property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|The ComparisonFlags property cannot be set to a non-zero value for "%1" because the "%2" is not a source output. The output column "colname" (ID) cannot have a ComparisonFlags property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags for "%1" must be zero because its type is not a string type. ComparisonFlags can only be non-zero for string type columns.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|The "%1" cannot have a ComparisonFlags property set to non-zero because its SortKeyPosition is set to zero. An output column's ComparisonFlags can only be non-zero if its SortKeyPosition is also non-zero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|The property is read-only.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|The %1 had an invalid datatype value (%2!ld!) set.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|The "%1" requires a code page to be set but the value passed was zero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|The "%1" has a length that is not valid. The length must be between %2!ld! and %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|The "%1" has a scale that is not valid. The scale must be between %2!ld! and %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|The "%1" has a precision that is not valid. The precision must be between %2!ld! and %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|The "%1" has a value set for length, precision, scale, or code page that is a value other than zero, but the data type requires the value to be zero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|The %1 does not allow setting output column datatype properties.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|The "%1" contains an invalid data type. "%1 " is a special error column,  and the only valid data type is DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|The component does not supply error code descriptions.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|The specified error code is not associated with this component.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|A truncation caused a row to be redirected, based on the truncation disposition settings.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|The "%1" is unable to make the column with lineage ID %2!d! read/write because that usage type is not allowed on this column. An attempt was made to change the usage type of an input column to a type, UT_READWRITE, that is not supported on this component.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|The %1 has forbidden the requested use of the input column with lineage ID %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|The "%1" was unable to make the requested change to the input column with lineage ID %2!d!. The request failed with error code 0x%3!8.8X!. The specified error occurred while attempting to set the usage type of an input column.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Attempt to set the data type properties on "%1" failed with error code 0x%2!8.8X!. The error occurred while attempting to set one or more of the data type properties of the output column.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|The metadata for "%1" cannot be retrieved. Make sure the object name is correct and the object exists.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|The output column cannot be mapped to an external metadata column.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|The variable %1 is required to be of type "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|The %1 does not allow setting external metadata column datatype properties.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|The ID, %1!lu!, is neither an input ID nor an output ID. The specified ID must be the input ID or the output ID that the external metadata collection is associated with.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|The external metadata collection on "%1" is marked as not used, so no operations can be performed on it.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|The %1 is a synchronous output and the buffer type cannot be retrieved for a synchronous output.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|The input column "%1" must be read-only. The input column has a usage type other than read-only, which is not allowed.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|The "%1" is missing the required property "%2". The object is required to have the specified custom property.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|The output %1 cannot not have property "%2", but currently has that property assigned.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|The %1 must be in exclusion group %2!d!. All outputs must be in the specified exclusion group.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|The property "%1" is empty. The property cannot be empty.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|Memory cannot be allocated for the expression "%1". There was an out-of-memory error while creating an internal object to hold the expression.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Cannot parse the expression "%1". The expression was not valid, or there is an out-of-memory error.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Computing the expression "%1" failed with error code 0x%2!8.8X!. The expression may have errors, such as divide by zero, that cannot be detected at parse time, or there may be an out-of-memory error.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Memory cannot be allocated for the Expression objects. An out-of-memory error occurred while creating the array of Expression object pointers.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|The %1 failed with error code 0x%2!8.8X! while creating the Expression Manager.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|The expression "%1" is not Boolean. The result type of the expression must be Boolean.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|The expression "%1" on "%2" is not valid.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|The column "%1" (%2!d!) cannot be matched to any input file column. The output column name or input column name cannot be found in the file.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Attempting to set the result column for the expression "%1" on %2 failed with error code 0x%3!8.8X!. The input or output column that was to receive the result of the expression cannot be determined, or the expression result cannot be cast to the column type.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|The %1 failed to get the locale ID from the package.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|The parameter mapping string is not in the correct format.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|The SQL command requires %1!d! parameters, but the parameter mapping only has %2!d! parameters.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|The SQL command requires a parameter named "%1", which is not found in the parameter mapping.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|There is more than one data source column with the name "%1".  The data source column names must be unique.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|There is a data source column with no name.  Each data source column must have a name.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|A component is disconnected from the layout.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|The ID for a layout component is not valid.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|A component has an invalid number of inputs.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|A component has an invalid number of outputs.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|A component does not have any inputs or outputs.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|Not enough memory was available to allocate a list of the columns that are being manipulated by this component.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|Output column "%1" (%2!d!) references input column with lineage ID %3!d!, but no input could be found with that lineage ID.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|At least one input column must be marked as a sort key, but no keys were found.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Both column "%1" (%2!d!) and column "%3" (%4!d!) were marked with sort key weight %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|The component cannot perform the requested metadata change until the validation problem is fixed.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|An input cannot be added to the inputs collection.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|An output cannot be added to the outputs collection.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|An input cannot be deleted from the inputs collection.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|An output cannot be removed from the outputs collection.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|The usage type of the column cannot be changed.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|The %1 must be read/write to have custom property "%2". The input or output column has the specified custom property, but is not read/write. Remove the property, or make the column read/write.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|The %1 is read/write and is required to have custom property "%2". Add the property, or make remove the read/write attribute from the column.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|The column cannot be deleted. The component does not allow columns to be deleted from this input or output.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|The component does not allow adding columns to this input or output.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|The connection "%1" cannot be found. Verify that the connection manager has a connection with that name.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|The runtime connection manager with the ID "%1" cannot be found. Verify that the connection manager collection has a connection manager with that ID.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS Error Code DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  The AcquireConnection method call to the connection manager "%1" failed with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the AcquireConnection method call failed.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|The connection acquired from the connection manager "%1" is not valid.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" is an incorrect type.  The type required is "%2". The type available to the component is "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Cannot acquire a managed connection from the run-time connection manager.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|An input cannot be created to initialize the inputs collection.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|An output cannot be created to initialize the outputs collection.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Writing to the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|The connection manager "%1" returned an object of an  incorrect type from the AcquireConnection method.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|The "%3" property is required on input column "%1" (%2!d!), but is not found. The missing property should be added.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|The "%1" is marked read-only, but is not referenced by any other column. Unreferenced columns are not allowed.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|The "%1" references column ID %2!d!, and that column is not found on the input. A reference points to a nonexistent column.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not of a BLOB type.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|The "%1" references output column ID %2!d!, and that column is not found on the output.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Reading from the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|There must be at least one column of Fixed, Changing, or Historical type on the input of a Slowly Changing Dimension transform. Verify that at least one column is a FixedAttribute, ChangingAttribute, or HistoricalAttribute.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|The ColumnType property of "%1" is not valid. The current value is outside the range of acceptable values.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|The input column "%1" cannot be mapped to external column "%2" because they have different data types. The Slowly Changing Dimension transform does not allow mapping between column of different types except for DT_STR and DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|The data type for "%1" is DT_NTEXT, which is not supported with ANSI files. Use DT_TEXT instead and convert the data to DT_NTEXT using the data conversion component.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|The data type for "%1" is DT_TEXT, which is not supported with Unicode files. Use DT_NTEXT instead and convert the data to DT_TEXT using the data conversion component.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|The data type for "%1" is DT_IMAGE, which is not supported. Use DT_TEXT or DT_NTEXT instead and convert the data from, or to, DT_IMAGE using the data conversion component.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|Format "%1" is not supported by Flat File Connection Manager. Supported formats are Delimited, FixedWidth, RaggedRight, and Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not of a String type.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Error caused by conflicting property settings. The "%1" has both the AllowAppend property and the ForceTruncate property set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|The %1 references column ID %2!d!, but that column is already referenced by %3. Remove one of the two reference to the column.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|A connection manager has not been assigned to the %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|The %1 references the output column with ID %2!d!, but that column is already referenced by %3.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|The "%1" is not referenced by any input column. Each output column must be referenced by exactly one input column.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not the correct type. It must be DT_TEXT, DT_NTEXT, or DT_IMAGE. A reference points to a column that must be a BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not a String type.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|The "%1" has the ExpectBOM property set to TRUE for %2, but the column is not NT_NTEXT. The ExpectBOM specifies that the Import Column transformation expects a byte-order mark (BOM). Either set the ExpectBOM property to false or change the output column data type to DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Data output columns must be DT_TEXT, DT_NTEXT, or DT_IMAGE. The data output column may only be set to a BLOB type.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|If the FailOnFixedAttributeChange property is set to TRUE, the transformation will fail when a fixed attribute change is detected. To send rows to the Fixed Attribute output, set the FailOnFixedAttributeChange property to FALSE.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|The Lookup transformation failed to retrieve any rows. The transform fails when the FailOnLookupFailure is set to TRUE and no rows are retrieved.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|There must be at least one column type of Key on the input of a Slowly Changing Dimension transformation. Set at least one column type to Key.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Cannot find external column with name "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|Inferred indicator column "%1" must be of type DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|The %1 must have its error row disposition value set to RD_NotUsed.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|The %1 must have its truncation row disposition value set to RD_NotUsed.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Cannot find input column with lineage ID %1!d! needed by output column with ID %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Invalid output data type for aggregate type specified at output column ID %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Invalid input data type for %1 used for the specified aggregate at %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Data types of input column lineage ID %1!d! and output column ID %2!d! do not match.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Cannot get input buffer handle for input ID %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Cannot get output buffer handle for output ID %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Cannot find column with lineage ID %1!d! in output buffer.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Cannot find column with lineage ID %1!d! in input buffer.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|The number of output columns for %1 cannot be zero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|The number of columns in the flat file connection manager must be the same as the number of columns in the flat file adapter. The number of columns for the flat file connection manager is %1!d!, while the number of columns for the flat file adapter is %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|The column "%1" at index %2!d! in the flat file connection manager was not found at index %3!d! in the column collection of the flat file adapter.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|The external metadata column with ID %1!d! has already been mapped to %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|The transform encountered a key column that was larger than %1!u! characters.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|The transform encountered a result value that was longer than %1!u! bytes.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Unable to allocate memory.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Unable to allocate memory.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Unable to allocate memory.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Unable to allocate memory.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|The input column "%1" is not referenced.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|The Sort transformation could not create a thread pool with %1!d! threads. Not enough memory is available.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|The Sort transformation cannot queue a work item to its thread pool. There is not enough memory available.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|A worker thread in the Sort transformation stopped with error code 0x%1!8.8X!. A catastrophic error was encountered while sorting a buffer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads was %1!ld!, and should be between 1 and %2!ld!, inclusive or -1 to default to the number of CPUs.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Unable to load from XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|Unable to save to XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Unable to convert the value "%1" to an integer.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Unable to convert the value "%1" to a Boolean.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Load error encountered near object with ID %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|The %1 is not mapped to an output column.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|The %1 has a mapping that is not valid.  An output column with an ID of %2!ld! does not exist on this component.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|The %1 is mapped to an output column that already has a mapping on this input.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Could not convert input column with Lineage ID %1!ld! to DT_WSTR due to error 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Referenced object with ID %1!d! not found in package.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Cannot read a persistence property required for the pipelinexml module. The property was not provided by the pipeline.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Cannot retrieve custom property "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|An input column with the lineage ID %1!d!, referenced in the ParameterMap custom property with the parameter on position number %2!d!, cannot be found in the input columns collection.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Unable to locate reference column "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 and reference column named "%2" have incompatible data types.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|The parameterized SQL statement yields metadata which does not match the main SQL statement.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|The parameterized SQL statement contains an incorrect number of parameters. Expected %1!d!, but found %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 has a datatype which cannot be joined on.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 has a datatype which cannot be copied.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR or DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT, or DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, or DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|The Sort transformation cannot create an event to communicate with its worker threads. Not enough system handles are available to the Sort transformation.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|The Sort transformation cannot create a worker thread. Not enough memory is available to Sort transformation.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|The Sort transformation failed to compare row %1!d! in buffer ID %2!d! to row %3!d! in buffer ID %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|The Lookup transformation reference metadata contains too few columns. Check the SQLCommand property. The SELECT statement must return at least one column.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory for an array of ColumnInfo structures.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Could not allocate memory for an array of ColumnPair structures.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Unable to allocate memory for an array of BUFFCOL structures for the creation of a main workspace.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Unable to allocate memory for hash table.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for hash nodes.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for a hash node heap.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Unable to create a heap for LRU nodes. An out-of-memory condition occurred.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Unable to allocate memory for the LRU node heap. An out-of-memory condition occurred.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|OLE DB error occurred while loading column metadata. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|OLE DB error occurred while fetching rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|OLE DB error occurred while populating internal cache. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|OLE DB error occurred while binding parameters. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|OLE DB error occurred while creating bindings. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|An invalid case was encountered in a switch statement during runtime.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|OLE DB error occurred while fetching parameterized rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|OLE DB error occurred while fetching parameterized row. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Unable to allocate memory for the hash table.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for the hash nodes.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for the hash node heap.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct nodes.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Unable to allocate memory for CountDistinct node heap.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct chains.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Unable to allocate memory for CountDistinct hash table.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the CountDistinct workspace buffer.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Unable to create a CountDistinct workspace buffer.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Unable to allocate memory for CountDistinct Collapse array.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Unable to allocate memory for CountDistinct chains.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column for copymap does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|The output column with lineage ID "%1!d!" is incorrectly mapped to an input column. The CopyColumnId property of the output column is not correct.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Failed to retrieve long data for column "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Long data was retrieved for a column but cannot be added to the Data Flow task buffer.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|Output "%1" (%2!d!) has output columns, but multicast outputs do not declare columns. The package is damaged.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Unable to load a localized resource ID %1!d!. Verify that the RLL file is present.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Cannot acquire Events Interface. An invalid Events interface was passed to the data flow module for persisting to XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|An error occurred while setting a path object during XML load.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Error setting input object during XML load.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Error setting output object during XML load.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Error setting input column object during XML load.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Error setting output column object during XML load.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Error setting property object during XML load.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Error setting connection object during XML load.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Special transformation-specific columns are either missing or have incorrect types.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|Fuzzy Grouping transformation failed to create required tables and accessors.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|Fuzzy Grouping transformation failed to copy input.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|Fuzzy Grouping transformation failed to generate groups.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|An unexpected error occurred in Fuzzy Grouping when applying the settings of property '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|The Fuzzy Grouping transformation failed to pick a canonical row of data to use in standardizing the data.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|Fuzzy Grouping does not support input columns of type IMAGE, TEXT, or NTEXT.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|A fuzzy match is specified on column "%1" (%2!d!) that is not a data type of DT_STR or DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|A Fuzzy Grouping transformation pipeline error occurred and returned error code 0x%1!8.8X!: "%2".|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|The code page %1!d! specified on column "%2" (%3!d!) is not supported.  You must first convert this column to DT_WSTR which can be done by inserting a Data Conversion Transform before this one.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Failure encountered while setting end of data flag for the buffer driving output "%1" (%2!d!).|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|The input buffer could not be cloned. An out-of-memory condition occurred or there was an internal error.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|Column "%1" requests that Katakana and Hiragana characters be produced at the same time.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|Column "%1" requests that Simple Chinese and Traditional Chinese characters be produced at the same time.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|Column "%1" requests operations to generate both full width and half width characters.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|Column "%1" combines operations on Japanese characters with operations for Chinese characters.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|Column "%1" combines operations on Chinese characters with uppercase and lowercase operations.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|Column "%1" combines operations on Japanese characters with uppercase and lowercase operations.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|Column "%1" maps the column to both uppercase and lowercase.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|Column "%1" combines flags other than uppercase and lowercase with the linguistic casing operation.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|The data type of column "%1" cannot be mapped as specified.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|The version (%1) of the pre-existing match index "%2" is not supported. The version expected is "%3". This error occurs if the version persisted in the index metadata does not match the version which the current code was built for. Fix the error by rebuilding the index with the current version of the code.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|The table "%1" does not appear to be a valid pre-built match index. This error occurs if the metadata record cannot be loaded from the specified pre-built index.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Unable to read specified pre-built match index "%1".  OLEDB Error code: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|There were no input columns with a valid join to a reference table column.  Make sure that there is at least one join defined using the input column properties JoinToReferenceColumn and JoinType.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|The specified pre-existing match index "%1" was not originally built with fuzzy match information for column "%2".  It must be rebuilt to include this information. This error occurs when the index was built with the column not being a fuzzy join column.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|The name "%1" given for property "%2" is not a valid SQL identifier name. This error occurs if the name for the property does not conform to the specifications for a valid SQL identifier name.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|The MinSimilarity threshold property on the Fuzzy Lookup transformation must be a value greater than or equal to 0.0 but less than 1.0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|The value "%1" for property "%2" is not valid.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|The fuzzy lookup specified between input column "%1" and reference column "%2" is not valid because fuzzy joins are only supported between string columns, types DT_STR and DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|The exact lookup columns, "%1" and "%2", do not have equal data types or are not comparable string types. Exact joins are supported between columns with equal data types or a DT_STR and DT_WSTR combination.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|The copy columns, "%1" and "%2", do not have equal data types or are not trivially convertible string types. This occurs because copying from reference to output between columns with equal data types, or a DT_STR and DT_WSTR combination, is supported, but other types are not.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|The passthrough columns, "%1" and "%2", do not have equal data types. Only columns with equal data types are supported as passthrough columns from input to output.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Cannot locate reference column "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|An output column must have exactly one CopyColumn or PassThruColumn property specified. This error occurs when neither the CopyColumn or the PassThruColumn properties, or both the CopyColumn and PassThruColumn properties, are set to non-empty values.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|The source lineage id '%1!d!' specified for property '%2' on output column '%3' was not found in the input column collection. This occurs when the input column id specified on an output column as a passthrough column is not found in the set of inputs.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|The column "%1" in the pre-built index "%2" was not found in the reference table/query. This happens if the schema/query of the reference table has changed since the pre-existing match index was built.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|The component encountered a token that was larger than 2147483647 characters.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has type %2 and the input column has type %3. The metadata for the column does not match on data type.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has maximum length %2!d! and the input column has maximum length %3!d!. The metadata for the column does not match in length.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has code page %2!d! and the input column has code page %3!d!. The metadata for the named column does not match on code page.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|The output file cannot be appended. Column "%1" matches by name, but the column in the file has precision %2!d! and the input column has precision %3!d!. The metadata for the named column does not match on precision.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has scale %2!d! and the input column has scale %3!d!.  The metadata for the named column does not match on scale.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Unable to determine the DBMS name and version on "%1". This occurs if the IDBProperties on the connection did not return information needed to verify the DBMS name and version.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|The DBMS type or version of "%1" is not supported.  A connection to Microsoft SQL Server version 8.0 or later is required. This occurs if IDBProperties on the connection did not return a the correct version.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|The %1 is a special error output column and cannot be deleted.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|The data type specified for column "%1" is not the expected type "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|The input column lineage ID "%1" referenced by property "%2" on output column "%3" could not be located in the input column collection.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|The input column "%1" referenced by the "%2" property on output column "%3" must have property ToBeCleaned=True and have a valid ExactFuzzy property value.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|The reference table '%1' does not have a clustered index on an integer identity column, which is required if the property 'CopyRefTable' is set to FALSE. If CopyRefTable is false, the reference table must have a clustered index on an integer identity column.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|The reference table '%1' contains a non-integer type identity column which is not supported. Use a view of the table without the column '%2'.  This error occurs  because when a copy is made of the reference table, an integer identity column is added, and only one identity column is allowed per table.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|Both MatchContribution and hierarchy information cannot be specified at the same time. This is not allowed because these properties are both weighing factors for scoring.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Levels in hierarchy should be unique numbers . Valid  level in hierarchy values are integers greater than or equal to 1. The smaller the number is, the lower the column is in the hierarchy. The default value is 0, indicating that the column is not part of a hierarchy. Overlaps and gaps are not allowed.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|No columns to fuzzy group on were defined.  There must be at least one input column with column properties ToBeCleaned=true and ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|The column with ID '%1!d!' was not valid for an undetermined reason.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|The data type of column '%1' is not supported.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|The length of output column '%1' is less than that of its source column '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|There should be only one input column.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|There should be exactly two output columns.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|The input column can only have DT_WSTR or DT_NTEXT as its data type.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|The output column [%1!d!] can only have '%2' as its data type.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|The Term Type of the transformation can only be WordOnly, PhraseOnly or WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|The value of Frequency Threshold should not be lower than '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|The value of Max Length of Term should not be lower than '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Term Extraction reference metadata contains too few columns.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|An error occurred while allocating memory.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|An error occurred while extracting terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|The number of the term candidates exceeds its limit, 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|The reference table, view, or column that is used for Exclusion Terms is not valid.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|The length of string column '%1' exceeds 4000 characters.  A conversion from DT_STR to DT_WSTR is necessary, so a truncation would occur.  Either reduce the column width or use only DT_WSTR column types.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|The reference table, view, or column to be used for an Exclusion Terms has not been set.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|Term Lookup contains too few output columns.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Term Lookup reference metadata contains too few columns.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|An error occurred while normalizing words.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|An error occurred while looking up terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|At least one Passthrough column is not mapped to an output column.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|There should be exactly one input column mapped to one reference column.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|The input column mapped to a reference column can only have DT_NTXT or DT_WSTR as its data type.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|The reference table name "%1" is not a valid SQL identifier. This error occurs if the table name cannot be parsed from the input string. There may be unquoted spaces in the name. Verify that the name is correctly quoted.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|An error occurred while the Term Filter was starting its iteration.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|An error occurred while reclaiming the buffer used for caching terms. The error code returned was 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|An std::length_error occurred from the STL containers.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|An error occurred while saving words with punctuation characters. The error code returned was 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|An error occurred while processing the %1!ld!th reference term. The error code returned was 0x%2!8.8X!. Please remove the reference term from your reference table as a work-around.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|An error occurred while sorting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|Fuzzy Lookup was unable to load the entire reference table into main memory as is required when the Exhaustive property is enabled.  Either we ran out of system memory or a limit was specified for MaxMemoryUsage which was not sufficient to load the reference table.  Either set MaxMemoryUsage to 0 or increase it significantly.  Alternatively, disable Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|An error occurred while initializing the engine of Term Lookup. The error code returned was 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|An error occurred while processing sentences. The error code returned was 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|An error occurred while saving part-of-speech tags from an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|An error occurred while loading the finite state automata. The error code returned was 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|An error occurred while initializing the engine of Term Extraction. The error code returned was 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|An error occurred while processing within a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|An error occurred while adding words to a statistical decoder. The error code returned was 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|An error occurred while decoding for a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|An error occurred while setting exclusion terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|An error occurred while testing whether a dot is a part of an acronym. The error code returned was 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|An error occurred while setting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|The value for the property %1 is %2!d!, which is not allowed.  The value must be greater than or equal to %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|The value for the property %1 is %2!d!, which must be less than or equal to the value of %3!d! for property %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|An error was encountered when trying to delete the existing fuzzy match index named "%1". It is possible that this table was not created by Fuzzy Lookup (or this version of Fuzzy Lookup), it has been damaged, or there is another problem. Try manually deleting the table named "%2" or specify a different name for the MatchIndexName property.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|The Score Type of the transformation can only be Frequency or TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|The reference table specified has too many rows. Fuzzy Lookup only works with reference tables having less than 1 billion rows. Consider using a smaller view of your reference table.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Unable to determine the size of the reference table '%1'.  It is possible that this object is a view and not a table.  Fuzzy Lookup does not support views when CopyReferentaceTable=false.  Make sure that the table exists and that CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|The SSIS Data Flow Task data type "%1" on the %2 is not supported for the %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Unable to set data type properties for the output column with ID %1!d! on the output with ID %2!d!. The output or column could not be found.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|The value of custom property "%1" on the %2 cannot be changed.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|The %1 on the non-error output has no corresponding output column on the error output.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|The %1 on the error output has no corresponding output column on the non-error output.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|The %1 on the error output has properties that do not match the properties of its corresponding data source column.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|The data type of output columns on the %1 cannot be changed, except for DT_WSTR and DT_NTEXT columns.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|The data type of "%1" does not match the data type "%2" of the source column "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|The %1 does not have a matching source column in the schema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|The reference table/view or column used for the reference terms is invalid.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|The reference table/view or column used for the reference terms has not been set.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|The %1 is mapped to the external metadata column with ID %2!ld!, which is already mapped to another column.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|The SQL object name '%1' specified for property '%2' contains more than the maximum number of prefixes.  The maximum is 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|The value was too large to fit in the column.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|The SSIS IDataReader is closed.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|The SSIS IDataReader is past the end of the result set.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|The ordinal position of the column is not valid.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|Cannot convert the %1 from data type "%2" to data type "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|The %1 has unsupported code page %2!d!.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|The %1 has no mapping to the XML schema.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|The SSIS IDataReader is closed. The read timeout has expired.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|An error occurred executing the provided SQL command: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|The JoinType property specified for input column '%1' differs from the JoinType specified for the corresponding reference table column when the Match Index was initially created.  Either rebuild the Match Index with the given JoinType or change the JoinType to match the type used when the Match Index was created.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|The data type "%1" found on %2 is not supported for the %3.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|The data type of the %1 is not supported for the %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Failed to add project reference "%1" while migrating %2. Migration might need to be completed manually.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Multiple entry points with the name "%1" were found during the migration of %2. Migration might need to be completed manually.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|No entry point was found during the migration of %1. Migration might need to be completed manually.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|An exception has occurred during data insertion, the message returned from the provider is: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Failed to retrieve the provider invariant name from %1, it is currently not supported by ADO NET Destination component|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|An argument exception has occurred while data provider tried to insert data to destination. The returned message is : %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|The BatchSize property must be a non-negative integer|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|An error has occurred while sending this row to destination data source.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|Executing tSQL command throws an exception, the message is :  %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET Destination has failed to acquire the connection %1. The connection may have been corrupted.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|The specified connection %1 is not managed, please use managed connection for ADO NET destination.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|The destination component does not have an error output. It may have been corrupted.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|The lineageID %1 associated with external column %2 does not exist at run time.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Failed to get properties of external columns. The table name you entered may not exist, or you do not have SELECT permission on the table object and an alternative attempt to get column properties through connection has failed. Detailed error messages are: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|Input column error disposition is not supported by ADO NET Destination component.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|Input column truncation disposition is not supported by ADO NET Destination component.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|Input  truncation row disposition is not supported by ADO NET Destination component.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|The Table or View name is not expected. \n\t If you are quoting the table name, please use the prefix %1 and the suffix %2 of your selected data provider for quotation. \n\t If you are using multipart name, please use at most three parts for the table name.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Failed to find column "%1" with lineage ID %2!d! in the buffer. The buffer manager returned error code 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Failed to get information for column "%1" (%2!d!) from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Arithmetic overflow encountered while aggregating "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Failed to get information for row %1!ld!, column %2!ld! from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Failed to set information for row %1!ld!, column %2!ld! into the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|A required buffer is not available.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|The attempt to get buffer boundary information failed with error code 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Setting the end of rowset for the buffer failed with error code 0x%1!8.8X!.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Failed to get data for the error output buffer.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Removing a row from the buffer failed with error code 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|The attempt to set buffer error information failed with error code 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|There was an error with %1 on %2. The column status returned was: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Unable to cache reference metadata.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|Row yielded no match during lookup.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|The %1 has an invalid error or truncation row disposition.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Directing the row to the error output failed with error code 0x%1!8.8X!.|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Preparing column statuses for insert failed with error code 0x%1!8.8X!.|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|An attempt to find %1 with lineage ID %2!d! in the Data Flow Task buffer failed with error code 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Failed to find any non-special error column in %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS Error Code DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" specifies failure on error. An error occurred on the specified object of the specified component.  There may be error messages posted before this with more information about the failure.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|The expression "%1" on "%2" evaluated to NULL, but the "%3" requires a Boolean results. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row).  The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|The expression evaluated to NULL, but a Boolean result is required. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row). The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|The file format of UTF-16 big endian is not supported.  Only UTF-16 little endian format is supported.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|The file format of UTF-8 is not supported as Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Cannot read ID attribute.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|The cache index column %1 is referenced by more than one lookup input column.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|Lookup does not reference all cache connection manager index columns. Number of joined columns in lookup: %1!d!. Number of index columns: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violated the integrity constraints for the column.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violates integrity constraints.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the data conversion transform.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the flat file source adapter was unsigned.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the flat file source adapter.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Opening the file "%1" for reading failed with error code 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Failed to open file for reading.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Opening the file "%1" for writing failed with error code 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Failed to open file for writing.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Failed to read from file.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Failed to write to file.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Too many array elements were found when parsing a property of type array. The elementCount is less than the number of array elements found.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Too few array elements were found when parsing a property of type array. The elementCount is more than the number of array elements found.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file "%1" for writing failed. The file cannot be found.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file for writing failed. The file cannot be found.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file "%1" for writing failed. The path cannot be found.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file for writing failed. The path cannot be found.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file "%1" for writing failed. There are too many files open.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file for writing failed. There are too many files open.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file "%1" for writing failed. You do not have the correct permissions.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file for writing failed. You do not have the correct permissions.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Opening the file "%1" for writing failed. The file exists and cannot be overwritten. If the AllowAppend property is FALSE and the ForceTruncate property is set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Opening a file for writing failed. The file already exists and cannot be overwritten. If both the AllowAppend property and the ForceTruncate property are set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|The value for custom property "%1" on %2 is incorrect.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Columns "%1" and "%2" have incompatible metadata.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Opening the file "%1" for writing failed because the disk is full. There is not sufficient disk space to save this file.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Attempting to open the file for writing failed because the disk is full.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Generating a sort key failed with error 0x%1!8.8X!. The ComparisonFlags are enabled, and generating a sortkey with LCMapString failed.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|Transform failed to map string and returned error 0x%1!8.8X!. The LCMapString failed.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Opening the file "%1" for reading failed. The file was not found.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Opening a file for reading failed. The file was not found.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening the file "%1" for reading failed. The path cannot be found.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening a file for reading failed. The path was not found.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file "%1" for reading failed. There are too many files open.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file for reading failed. There are too many files open.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Attempting to open the file "%1" for reading failed. Access is denied.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Opening the file for reading failed. You do not have the correct permissions.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file "%1" is 0x%2!4.4X!, but the expected value is 0x%3!4.4X!. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file is not valid. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|The %1 is not attached to a component.  It is required that a component be attached.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|The value for custom property %1 is incorrect.  It should be a number between %2!d! and %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|The custom property "%1" cannot be specified for the aggregation type selected for this column. The comparison flags custom property can only be specified for group by and count distinct aggregation types.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|The comparison flags custom property "%1" can only be specified for columns of with datatype DT_STR or DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Aggregation on %1 failed with error code 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|There was an error setting up the mapping. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|The %1 was unable to read the XML data.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|The %1 was unable to get the variable specified by the "%2" property.|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|The %1 contains a RowsetID with a value of %2 that does not reference a data table in the schema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|The property %1 must either be empty, or a number between %2!u! and %3!u!. The Keys or CountDistinctKeys property has a invalid value. The property should be a number between 0 and ULONG_MAX, inclusive, or not be set.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|The aggregate component encountered too many distinct key combinations. It cannot accommodate more than %1!u! distinct key values. There are more than ULONG_MAX distinct key values in the main workspace.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|The aggregate component encountered too many distinct values while calculating the count distinct aggregate. It cannot accommodate more than %1!u! distinct values. There were more than ULONG_MAX distinct values while calculating the count distinct aggregation.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|The attempt to write to the filename column failed with error code 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|An error occurred, but the column that caused the error cannot be determined.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Unable to upgrade lookup metadata from version %1!d! to %2!d!. The Lookup transform was unable to upgrade metadata from the existing version number in a call to PerformUpgrade().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Failed to locate the ending boundary of a sentence.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|The Term Extraction transformation is unable to process the input text because a sentence from the input text is too long. The sentence is segmented into several sentences.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|The %1 was unable to read the XML data. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|The call to Lookup transform method, ReinitializeMetadata, failed.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|The lookup transform must contain at least one input column joined to a reference column, and none were specified. You must specify at least one join column.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|The message string being posted by the managed error infrastructure contains a bad format specification. This is an internal error.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|While formatting a message string using the managed error infrastructure, there was a variant type that does not have formatting support. This is an internal error.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|The %1 was unable to process the data. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|The property "%1" on the %2 was empty.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Attempting to create an output with the name "%1" for the XML table with the path "%2" failed because the name is invalid.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|The value was too large to fit in the %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|The %1 was unable to process the data.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2"  at "%3" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" at "%4" specifies failure on error. An error occurred on the specified object of the specified component.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|The SQLCE destination could not set the column values for the row.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|The SQLCE destination could not insert the row.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Unable to allocate memory.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Unable to create workspace buffer.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Unable to instantiate XML DOM document, please verify that MSXML binaries are properly installed and registered.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|Unable to load XML data into a local DOM for processing.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|The type of the runtime variable "%1" is incorrect. The runtime variable type must be Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. Multiple inline schemas are not supported.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not be declared as anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not contain a reference (ref) to a group.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|The XML Source Adapter does not support mixed content model on Complex Types.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|The XML Source Adapter was unable to process the XML data. An inline schema must be the first child node in the source Xml.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|The XML Source Adapter was unable to process the XML data. No inline schema was found in the source XML, but the "UseInlineSchema" property was set to true.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|The component cannot use a connection manager that retains its connection in a transaction with fastload or bulk insert.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|The %1 cannot be set to redirect on error using a connection in a transaction.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|The %1 does not have a corresponding input or output column.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|There is no selected column to be written to the file.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|The %1 has an invalid data type. Columns with data types DT_IMAGE, DT_TEXT and DT_NTEXT cannot be written to raw files.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|The external metadata collection is improperly used by this component. The component should use external metadata when appending or truncating an existing file. Otherwise, the external metadata is not needed.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|The %1 is mapped to an external metadata column with the id %2!d!. Input columns should not be mapped to external metadata columns when selected Write Option value is Create Always.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|The file  cannot be opened for reading the metadata. If the file does not exist, and the component has already defined external metadata, you can set the "ValidateExternalMetadata" property to "false" and the file will be created at the runtime.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Failed to access LOB data from the data flow buffer for data source column "%1" with error code 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|The %1 was unable to process the XML data. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|The XML Source Adapter was unable to process the XML data.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|The value %1!d! is not recognized as a valid access mode.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Complete metadata information for the data source column "%1" is not available.  Make sure the column is correctly defined in the data source.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Only lengths of User Name column, Package Name column, Task Name column and Machine Name column can be changed.  All other audit column datatype information is read only.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|A rowset based on the SQL command was not returned by the OLE DB provider.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|A commit failed.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|The custom property "%1" on %2 can only be used with ANSI files.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|The custom property "%1" on %2 can only be used with DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_ERROR.  The requested OLE DB provider %2 is not registered. Error code: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  The requested OLE DB provider %2 is not registered -- perhaps no 64-bit provider is available.  Error code: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|The cache column, "%1", is mapped to more than one column. Remove the duplicate column mappings.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|The %1 is not mapped to valid cache column.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because the data types do not match.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|The number of input columns does not match the number of cache columns.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|The cache file name is either not provided or is not valid. Provide a valid cache file name.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|The index position of column, "%1", is different from index position of Cache connection manager column, "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Failed to load the cache from file, "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|The lookup input column %1 references non-index cache column %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Failed to get the connection string.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because one or more data type properties do not match.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Cache column "%1" was not found in the cache.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Failed to map %1 to a cache column. The hresult is 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|The %1 cannot write to the cache because the cache has been loaded from a file by %2.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|The %1 cannot load the cache from file "%2" because the cache has already been loaded from file "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|The output with ID %1!d! of Aggregate component is not used by any component. Please either remove it or associate it with an input of some component.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|The %1 failed to write the cache to file "%2". The hresult is 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|The XML schema data type information for "%1" on  element "%2" has changed.  Please re-initialize the metadata for this component and review column mappings.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 not used in join or copy. Please remove the unused column from the input column list.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|The sort failed due to a stack overflow while sorting an incoming buffer.  Please reduce the DefaultBufferMaxRows property on the Data Flow Task.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Consider changing the PROVIDER in the connection string to %1 or visit https://www.microsoft.com/downloads to find and install support for %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Failed to initialize the task object for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Failed to create COM Component Categories Manager due to error 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|Component %1!s! failed to initialize due to error 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Warning Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] warning messages begin with **DTS_W_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|There are %1!lu! days left in the evaluation. When it expires, packages will not be able to be executed.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Warning(s) raised. There should be more specific warnings preceding this one that explain the specifics of the warning(s).|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Cannot create an XML document object instance. Verify that MSXML is installed and registered correctly.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Cannot load the XML configuration file. The XML configuration file may be malformed or not valid.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|The configuration file name "%1" is not valid. Check the configuration file name.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|The configuration file loaded, but is not valid. The file is not formatted correctly, may be missing an element, or may be damaged.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|The configuration file "%1" cannot be found. Check the directory and file name.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Configuration registry key "%1" was not found. A configuration entry specifies a registry key that is not available. Check the registry to ensure that the key is there.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|The configuration type in one of the configuration entries was not valid. Valid types are listed in the DTSConfigurationType enumeration.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|The package path referenced an object that cannot be found: "%1". This occurs when an attempt is made to resolve a package path to an object that cannot be found.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with the package delimiter. Prepend "\package" to the package path.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|Configuration from a parent variable "%1" did not occur because there was no parent variable collection.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Failure importing configuration file: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|Configuration from a parent variable "%1" did not occur because there was no parent variable. Error code: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|The configuration file was empty and contained no configuration entries.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|The configuration type for configuration "%1" is not valid. This may occur when an attempt is made to set the type property of a configuration object to an invalid configuration type.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|The configuration type for the registry configuration was not found in key "%1". Add a value called ConfigType to the registry key and give it a string value of "Variable", "Property", "ConnectionManager", "LoggingProvider", or "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|The configuration value for the registry configuration was not found in key "%1". Add a value called Value to the registry key of type DWORD or String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Process configuration failed to set the destination at the package path of "%1". This occurs when attempting to set the destination property or variable fails. Check the destination property or variable.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredValue section is either empty, or does not exist: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredType section is either empty, or does not exist: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Failed to retrieve value from the .ini file. The PackagePath section is either empty, or does not exist: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Failed to retrieve value from the .ini file. The ConfiguredValueType section is either empty, or does not exist: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|Configuration from SQL Server was not successfully imported: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|The .ini configuration file is not valid due to empty or missing fields.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|Table "%1" does not have any records for configuration. This occurs when configuring from a SQL Server table that has no records for the configuration.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Error using same name for different custom events. The custom event "%1" was defined differently by different children of this container. There may be an error when executing the event handler.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|The configuration attempted to change a read-only variable. The variable is at the package path "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Calling ProcessConfiguration on the package failed. The configuration attempted to change the property at the package path "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Failed to load at least one of the configuration entries for the package. Check configuration entries for "%1" and previous warnings to see descriptions of which configuration failed.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|The configuration entry "%1" in the configuration file was not valid, or failed to configure the variable.  The name indicates which entry failed. In some cases, the name will not be available.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|This task or container has failed, but because FailPackageOnFailure property is FALSE, the package will continue. This warning is posted when the SaveCheckpoints property of the package is set to TRUE and the task or container fails.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|The path is empty.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS Warning Code DTS_W_MAXIMUMERRORCOUNTREACHED.  The Execution method succeeded, but the number of errors raised (%1!d!) reached the maximum allowed (%2!d!); resulting in failure. This occurs when the number of errors reaches the number specified in MaximumErrorCount. Change the MaximumErrorCount or fix the errors.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|The configuration environment variable was not found.  The environment variable was: "%1". This occurs when a package specifies an environment variable for a configuration setting but it cannot be found. Check the configurations collection in the package and verify that the specified environment variable is available and valid.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|The provider name for the connection manager "%1" has been changed from "%2" to "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|An exception occurred while reading the upgrade mapping files. The exception is "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|There is a duplicate mapping in file, "%1". The tag is "%2", and the key is "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|The extension, "%1", was implicitly upgraded to "%2". Add a mapping for this extension to the UpgradeMappings directory.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|A mapping in the file, "%1", is not valid. Values cannot be null or empty. The tag is "%2", the key is "%3", and the value is "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|The DataTypeCompatibility property of ADO type connection manager "%1" was set to 80 for backward compatibility reasons.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|The For Each File enumerator is empty. The For Each File enumerator did not find any files that matched the file pattern, or the specified directory was empty.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1". Verify that the package path is valid.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|The iteration expression is not an assignment expression: "%1". This error usually occurs when the expression in the assignment expression on the ForLoop is not an assignment expression.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|The initialization expression is not an assignment expression: "%1". This error usually occurs when the expression in the iterate expressions on the ForLoop is not an assignment expression.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|The executable "%1" was pasted successfully. However a log provider that was associated with the executable was not found in the collection "LogProviders".  The executable was pasted without log provider information.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Succeeded in upgrading the package.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|The "%1" ProgID has been deprecated. The new ProgID for this component "%2" should be used instead.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Operation "%1" failed.|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|The encryption algorithm "%1" uses weak encryption.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Task failed to execute operation "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|The subject is empty.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|The address in the "To" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|The address in the "From" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|The two XML documents are different.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD Validation will use the DTD file defined in the DOCTYPE line in the XML document. It will not use what is assigned to the property "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Task failed to validate "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|The transfer action value was invalid.  It is being set to copy.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|The transfer method value was invalid.  It is being set to an online transfer.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|A problem occurred with the following messages: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Skipping the transfer of job "%1" since it already exists at destination.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Overwriting the job "%1" at destination server.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Persisted enumeration value of property "FailIfExists" was changed and rendered invalid. Resetting to default.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Overwriting Login "%1" at destination.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|There are no elements specified to transfer.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|The lineage IDs of the input columns cannot be validated because the execution trees contain cycles.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|The DataFlow task has no components. Add components or remove the task.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but all of its output columns' SortKeyPositions are set to zero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|Source "%1" (%2!d!) will not be read because none of its data ever becomes visible outside the Data Flow Task.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|The output column "%1" (%2!d!) on output "%3" (%4!d!) and component "%5" (%6!d!) is not subsequently used in the Data Flow task. Removing this unused output column can increase Data Flow task performance.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Component "%1" (%2!d!) has been removed from the Data Flow task because its output is not used and its inputs either have no side effects or are not connected to outputs of other components. If the component is required, then the HasSideEffects property on at least one of its inputs should be set to true, or its output should be connected to something.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Rows were given to a thread, but that thread has no work to do. The layout has a disconnected output. Running the pipeline with the RunInOptimizedMode property set to TRUE will be faster, and prevents this warning.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|The external columns for %1 are out of synchronization with the data source columns. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|The column "%1" needs to be added to the external columns.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|The external column "%1" needs to be updated.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|The %1 needs to be removed from the external columns.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|The result string for expression "%1" may be truncated if it exceeds the maximum length of %2!d! characters. The expression could have a result value that exceeds the maximum size of a DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|A call to the ProcessInput method for input %1!d! on %2 unexpectedly kept a reference to the buffer it was passed. The refcount on that buffer was %3!d! before the call, and %4!d! after the call returned.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|The "%1" on "%2" has usage type READONLY, but is not referenced by an expression. Remove the column from the list of available input columns, or reference it in an expression.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Cannot find the "%1" value for component %2. The CurrentVersion value for the component cannot be located. This error occurs if the component has not set its registry information to contain a CurrentVersion value in the DTSInfo section. This message occurs during component development, or when the component is used in a package, if the component is not registered properly.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Warning: Could not open global shared memory to communicate with performance DLL; data flow performance counters are not available.  To resolve, run this package as an administrator, or on the system's console.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|There is a partial row at the end of the file.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|The end of the data file was reached while reading header rows. Make sure the header row delimiter and the number of header rows to skip are correct.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Cannot retrieve the column code page info from the OLE DB provider.  If the component supports the "%1" property, the code page from that property will be used.  Change the value of the property if the current string code page values are incorrect.  If the component does not support the property, the code page from the component's locale ID will be used.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|The data is already sorted as specified so the transform can be removed.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|The %1 references an external data type that cannot be mapped to a Data Flow task data type. The Data Flow task data type DT_WSTR will be used instead.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|The expression "%1" will always result in a truncation of data. The expression contains a static truncation (the truncation of a fixed value).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|The input column "%1" with ID %2!d! at index %3!d! is unmapped. The lineage ID for the column is zero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|The specified delimiters do not match the delimiters used to build the pre-existing match index "%1". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|The MaxOutputMatchesPerInput property on the Fuzzy Lookup transformation is zero. No results will be produced.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|There were no valid input columns with JoinType column property set to Fuzzy.  Performance on Exact joins may be improved by using the Lookup transform instead of FuzzyLookup.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|The reference column "%1" may be a SQL timestamp column. When the fuzzy match index is built, and a copy of the reference table is made, all reference table timestamps will reflect the current state of the table at the time of the copy. Unexpected behavior may occur if the CopyReferenceTable is set to false.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|A table with the name '%1' given for MatchIndexName already exists and DropExistingMatchIndex is set to FALSE.  Transform execution will fail unless this table is dropped, a different name is specified, or DropExisitingMatchIndex is set to TRUE.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|The length of input column '%1' is not equal to the length of the reference column '%2' that it is being matched against.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|The code pages of the DT_STR source column "%1" and the DT_STR dest column "%2" do not match.  This may cause unexpected results.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|There are more than 16 exact match joins, so performance may not be optimal. Reduce the number of exact match joins to improve performance. SQL Server has a limit of 16 columns per index, the inverted index will be used for all lookups.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|The Exhaustive option requires that the entire reference be loaded into main memory.  Since a memory limit has been specified for the MaxMemoryUsage property, it is possible that the entire reference table will not fit within this bound and that the match operation will fail at runtime.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|The cumulative lengths of the columns specified in the exact match joins exceeds the 900 byte limit for index keys.  Fuzzy Lookup creates an index on the exact match columns to increase lookup performance and there is a possibility that creation of this index may fail and the lookup will fall back to an alternative, possibly slower, method of finding matches. If performance is a problem, try removing some exact match join columns or reduce the maximum lengths of variable length exact match columns.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Failed to create an index for exact match columns. Reverting to alternative fuzzy lookup method.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|The following Fuzzy Grouping internal pipeline warning occurred with warning code 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|No maximum length was specified for the %1 with external data type %2. The SSIS Data Flow Task data type "%3" with a length of %4!d! will be used.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|The %1 references external data type %2, which cannot be mapped to a SSIS Data Flow Task data type.  The SSIS Data Flow Task data type DT_WSTR with a length of %3!d! will be used instead.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|No rows will be sent to error output(s). Configure error or truncation dispositions to redirect rows to the error output(s), or delete data flow transformations or destinations that are attached to the error output(s).|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|Rows sent to the error output(s) will be lost. Add new data flow transformations or destinations to receive error rows, or reconfigure the component to stop redirecting rows to the error output(s).|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|For the %1 with external data type %2, the XML schema specified a maxLength constraint of %3!d!, which exceeds the maximum allowed column length of %4!d!. The SSIS Data Flow Task data type "%5" with a length of %6!d! will be used.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|The %1 encountered duplicate reference key values when caching reference data. This error occurs in Full Cache mode only. Either remove the duplicate key values, or change the cache mode to PARTIAL or NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Truncation may occur due to inserting data from data flow column "%1" with a length of %2!d! to database column "%3" with a length of %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Truncation may occur due to retrieving data from database column "%1" with a length of %2!d! to data flow column "%3" with a length of %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Batch mode is not currently supported when error row disposition is used. The BatchSize property will be set to 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|No rows were successfully inserted into the destination. This may be due to a data type mismatch between columns, or due to the use of a datatype that is unsupported by your ADO.NET provider. Since the error disposition for this component is not "Fail component", error messages are not shown here; set the error disposition to "Fail component" to see error messages here.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Potential data loss may occur due to inserting data from input column "%1" with data type "%2" to external column "%3" with data type "%4". If this is intended, an alternative way to do conversion is using a Data Conversion component before ADO NET destination component.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|The %1 has been out of synchronization with the database column.  The latest column has %2. Use advanced editor to refresh  available destination columns if needed.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed. Use Advanced Editor to refresh the available destination columns if needed.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|A new column with name %1 has been added to the external database table. Use advanced editor to refresh available destination columns if needed.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|No rows will be sent to the no match output. Configure the transformation to redirect rows with no matching entries to the no match output, or delete the data flow transformations or destinations that are attached to the no match output.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Exception received while enumerating ADO.Net providers. The invariant was "%1". The exception message is: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|The %1 has no input column mapped to it.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|The table "%1" has changed. New columns might have been added to the table.|  
  
##  <a name="msgInfo"></a> Informational Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] informational messages begin with **DTS_I_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Starting distributed transaction for this container.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Committing distributed transaction started by this container.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Aborting the current distributed transaction.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" was successfully acquired.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" was successfully released.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" was successfully created.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Debug dump files will be generated for any error event.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Debug dump files will be generated for the following event codes: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Event code, 0x%1!8.8X!, triggered generation of debug dump files in the folder "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Creating SSIS information dump file "%1".|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Debug dump files successfully created.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|The package format was migrated from version %1!d! to version %2!d!. It must be saved to retain migration changes.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|The scripts in the package were migrated. The package must be saved to retain migration changes.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Receiving file "%1".|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Sending file "%1".|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|File "%1" already exists.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Cannot get extra error information due to an internal error.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|The attempt to delete file "%1" failed. This may occur when the file does not exist, the file name was spelled incorrectly, or you do not have permissions to delete the file.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|The package is attempting to configure from a registry entry using the registry key "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|The package is attempting to configure from the environment variable "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|The package is attempting to configure from the .ini file "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|The package is attempting to configure from SQL Server using the configuration string "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|The package is attempting to configure from the XML file "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|The package is attempting to configure from the parent variable "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|Attempting an upgrade of SSIS from version "%1" to version "%2". The package is attempting to upgrade the runtime.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Attempting to upgrade "%1". The package is attempting to upgrade an extensible object.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|The package will be saving checkpoints to file "%1" during execution. The package is configured to save checkpoints.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|The package restarted from checkpoint file "%1". The package was configured to restart from checkpoint.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|Checkpoint file "%1" was updated to record completion of this container.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|Checkpoint file "%1" was deleted after successful completion of the package.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Checkpoint file "%1" update starting.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Based on the system configuration, the maximum concurrent executables are set to %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|Maximum concurrent executables are set to %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Beginning of package execution.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|End of package execution.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Overwriting the database "%1" on the destination server "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Skipping error message "%1" since it already exists on the destination server.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" Error Messages were transferred.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|The task transferred "%1" Stored Procedures.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|Transferred "%1" objects.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|There are no Stored Procedures to transfer.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|There are no Rules to transfer.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|There are no Tables to transfer.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|There are no Views to transfer.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|There are no User Defined Functions to transfer.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|There are no Defaults to transfer.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|There are no User Defined Data Types to transfer.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|There are no Partition Functions to transfer.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|There are no Partition Schemes to transfer.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|There are no Schemas to transfer.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|There are no SqlAssemblies to transfer.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|There are no User Defined Aggregates to transfer.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|There are no User Defined Types to transfer.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|There are no XmlSchemaCollections to transfer.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|There are no Logins to transfer.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|There are no Users to transfer.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Truncating table "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Prepare for Execute phase is beginning.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Pre-Execute phase is beginning.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Post Execute phase is beginning.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Cleanup phase is beginning.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Validation phase is beginning.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" wrote %2!ld! rows.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Execute phase is beginning.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|The buffer manager detected that the system was low on virtual memory, but was unable to swap out any buffers. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough is installed, other processes are using it, or too many buffers are locked.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|The buffer manager failed a memory allocation call for %3!d! bytes, but was unable to swap out any buffers to relieve memory pressure. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough are installed, other processes were using it, or too many buffers are locked.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|The buffer manager has allocated %1!d! bytes, even though the memory pressure has been detected and repeated attempts to swap buffers have failed.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 has cached %2!d! rows.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 has cached a total of %2!d! rows.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|The raw source adapter opened a file, but the file contains no columns. The adapter will not produce data. This could indicate a damaged file, or that there are zero columns and, therefore, no data.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|An OLE DB informational message is available.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Fuzzy match performance can be improved if the exact join FuzzyComparisonFlags on the input column "%1" are set to match with the default SQL collation for reference table column "%2".  It is also necessary that no fold flags are set in FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Fuzzy match performance can be improved if an index is created upon the reference table across all of the specified exact match columns.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|Error and truncation dispositions were not reviewed. Make sure this component is configured to redirect rows to error outputs, if you wish to further transform those rows.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|The Aggregate transformation has encountered %1!d! key combinations. It has to re-hash data because the number of key combinations is more than expected. The component can be configured to avoid data re-hash by adjusting the Keys, KeyScale, and AutoExtendFactor properties.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|The Aggregate transformation has encountered %1!d! distinct values while performing a "count distinct" aggregation on "%2". The transformation will re-hash data because the number of distinct values is more than expected. The component can be configured to avoid data re-hash by adjusting the CountDistinctKeys, CountDistinctKeyScale, and AutoExtendFactor properties.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|The processing of file "%1" has started.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|The processing of file "%1" has ended.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|The total number of data rows processed for file "%1" is %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|The final commit for the data insertion in "%1" has started.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|The final commit for the data insertion  in "%1" has ended.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! rows are added to the cache. The system is processing the rows.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|The %1 processed %2!u! rows in the cache. The processing time was %3 seconds. The cache used %4!I64u! bytes of memory.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|The %1 failed to process the rows in the cache.  The processing time was %2 second(s).|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|The %1 succeeded in preparing the cache. The preparation time was %2 seconds.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, and performed %4!I64u! lookups using partial cache.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, performed %4!I64u! lookups using partial cache and %5!I64u! lookups using the cache for rows with no matching entries in the initial lookup.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|The %1 is writing the cache to file "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|The %1 has written the cache to file "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|The Maximum insert commit size property of the OLE DB destination "%1" is set to 0. This property setting can cause the running package to stop responding. For more information, see the F1 Help topic for OLE DB Destination Editor (Connection Manager Page).|  
  
##  <a name="msgGeneral"></a> General and Event Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_MSG_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Incorrect function.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|The system cannot find the file specified.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Starting Microsoft SSIS Service.<br /><br /> Server version %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS Service started.<br /><br /> Server version %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|The wait operation timed out.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|No more data is available.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS Service failed to start.<br /><br /> Error: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Error stopping Microsoft SSIS Service.<br /><br /> Error: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS Service configuration file does not exist.<br /><br /> Loading with default settings.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS Service configuration file is incorrect.<br /><br /> Error reading config file: %1<br /><br /> Loading server with default settings.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS Service:<br /><br /> Registry setting specifying configuration file does not exist.<br /><br /> Attempting to load default config file.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS Service: stopping running package.<br /><br /> Package instance ID: %1<br /><br /> Package ID: %2<br /><br /> Package name: %3<br /><br /> Package description: %4<br /><br /> Package started by: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Package "%1" started.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Package "%1" finished successfully.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Package "%1" has been cancelled.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Package "%1" failed.|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|Module %1 cannot load DLL %2 to call entry point %3 because of error %4. The product requires that DLL to run, but the DLL could not be found on the path.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|Module %1 loaded DLL %2, but cannot find entry point %3 because of error %4. The named DLL could not be found on the path, and the product requires that DLL to run.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
  
##  <a name="msgSuccess"></a> Success Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] success messages begin with **DTS_S_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|The value is NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|The string value was truncated. The buffer received a string that was too long for the column, and the string was truncated by the buffer.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|A truncation occurred during evaluation of the expression. The truncation occurred during evaluation, which may include any point in an intermediate step.|  
  
##  <a name="msgPipeline"></a> Data Flow Component Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTSBC_E_**, where "BC" refers to the native base class from which most Microsoft data flow components are derived.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|The total number of outputs and error outputs, %1!lu!, is incorrect. There must be exactly %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Cannot retrieve output with index %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|The number of error outputs, %1!lu!,  is incorrect. There must be exactly %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Incorrect validation status value, "%1!lu! ".  It must be one of the values found in the DTSValidationStatus enumeration.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|The input "%1!lu!" has no synchronous output.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|The input "%1!lu!" has no synchronous error output.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|The HowToProcessInput value, %1!lu!, is not valid. It must be one of the values from the HowToProcessInput enumeration.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Failed to get information for row "%1!ld!", column "%2!ld!" from the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Failed to set information for row "%1!ld!", column "%2!ld!" into the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|The property "%1" is not valid.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|The property "%1" was not found.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Error assigning a value to the read-only property "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|The %1 does not allow the insertion of output columns.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|The output columns' metadata does not match the associated input columns' metadata.  The output columns' metadata will be updated.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|There are input columns that do not have associated output columns. The output columns will be added.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|There are output columns that do not have associated input columns. The output columns will be removed.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|The output columns' metadata does not match the associated input columns' metadata.  The input columns will be unmapped.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|There are input columns that do not have associated output columns. The input columns will be unmapped.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|There is an input column associated with an output column, and that output column is already associated with another input column on the same input.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|The %1 does not allow the insertion of external metadata columns.|  
  
  字串常值 "%1" 包含不合法的逸出序列 "\\`2!c!"。 在運算式評估工具中，字串常值不支援逸出序列。-如果字串中需要反斜線，請使用雙反斜線 "\\\\"。 conceptual
helpviewer_keywords: 
  - "error numbers [Integration Services]"
  - "hresults [Integration Services]"
  - "errors [Integration Services], listed"
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
---
# Integration Services Error and Message Reference

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  The following tables list predefined [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] errors, warnings, and informational messages, in ascending numerical order within each category, along with their numeric codes and symbolic names. Each of these errors is defined as a field in the <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> class in the <xref:Microsoft.SqlServer.Dts.Runtime> namespace.  
  
 This list may be useful when you encounter an error code without its description. The list does not include troubleshooting information at this time.  
  
> [!IMPORTANT]  
>  Many of the error messages that you may see while working with [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] come from other components. In this topic, you will find all the errors raised by [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] components. If you do not see your error in the list, the error was raised by a component outside [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. These may include OLE DB providers, other database components such as the [!INCLUDE[ssDE](../includes/ssde-md.md)] and [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , or other services or components such as the file system, the SMTP server, Message Queuing (also known as MSMQ), and so forth. To find information about these external error messages, see the documentation specific to the component.  
  
 This list cadontains the following groups of messages:  
  
-   [Error Messages (DTS_E_*)](#msgError)  
  
-   [Warning Messages (DTS_W_*)](#msgWarning)  
  
-   [Informational Messages(DTS_I_*)](#msgInfo)  
  
-   [General and Event Messages(DTS_MSG_*)](#msgGeneral)  
  
-   [Success Messages(DTS_S_*)](#msgSuccess)  
  
-   [Data Flow Component Error Messages (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_E_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Overwriting Stored Procedure "%1" at destination.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|The data type "%1" found on column "%2" is not supported for the %3. This column will be converted to  DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|The column %1 in table %2 in the XML schema does not have a mapping in the external metadata columns.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|An internal object or variable was not initialized. This is an internal product error.  This error is returned when a variable should have a valid value but does not.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services evaluation period has expired.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|This property cannot be assigned a negative value. This error occurs when a negative value is assigned to a property that can only contain positive values, such as the COUNT property.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Indexes cannot be negative. This error occurs when a negative value is used as an index to a collection.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Invalid server name "%1". SSIS service does not support multi-instance, use just server name instead of "server name\instance".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Migration for VSA scripts can not be done on 64 bit platforms due to lack of Visual Tools for Applications designer support. Run the migration under WOW64 on 64 bit platforms.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|The command execution generated errors.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|To run a SSIS package outside of [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] you must install %1 of Integration Services or higher.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|The variable cannot be found. This occurs when an attempt is made to retrieve a variable from the Variables collection on a container during execution of the package, and the variable is not there. The variable name may have changed or the variable is not being created.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Error trying to write to a read-only variable, "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Unable to find the directories containing Tasks and Data Flow Task components. Check the integrity of your installation.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|Package name is too long. The limit is 128 characters. Shorten the package name.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|Package description is too long. The limit is 1024 characters. Shorten the package description.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments property is too long. The limit is 1024 characters. Try shortening the VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|The element cannot be found in a collection. This error happens when you try to retrieve an element from a collection on a container during execution of the package and the element is not there.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|The specified package could not be loaded from the SQL Server database.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|The variable value assignment is not valid. This error happens when the client or a task assigns a runtime object to a variable value.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Error assigning namespace to the variable. The namespace "System" is reserved for system use. This error happens when a component or task attempts to create a variable with a namespace of "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|The connection "%1" is not found. This error is thrown by Connections collection when the specific connection element is not found.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|The variable "%1" is a 64-bit integer variable, which is not supported on this operating system. The variable has been recast to 32-bit integer.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|An attempt change to a read-only attribute on variable "%1" occurred. This error happens when a read-only attribute for a variable is being changed at runtime. Read-only attributes can be changed only at design time.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Invalid attempt to set a variable to a container reference.  Variables are not allowed to reference containers.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Assigning invalid value or object to variable "%1". This error happens when a value is not appropriate for variables.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|One or more error occurred. There should be more specific errors preceding this one that explains the details of the errors. This message is used as a return value from functions that encounter errors.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Error getting or setting an array value. The type "%1" is not allowed. This occurs when loading an array into a variable.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Unsupported type in array. This happens when saving an array of unsupported types into a variable.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Error loading value "%1" from node "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|Node "%1" is not a valid node. This happens when saving fails.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Failed to load task "%1", type "%2". The contact information for this task is "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|Element "%1" does not exist in collection "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|The ObjectData element is missing in the XML block of a hosted object. This occurs when the XML parser attempts to locate the data element for an object and it cannot be found.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|The variable "%1" cannot be found. This error occurs when an attempt to retrieve a variable from a variables collection on a container during execution of the package occurs, and the variable is not there.  A variable name may have changed or the variable is not being created.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|The package cannot execute because it contains tasks that failed to load.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|The task has failed to load. The contact information for this task is "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Error loading task "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Error loading task. This happens when loading a task from XML fails.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|The %1 cannot write to the cache because %2 has already written to it.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Failed to prepare the cache for new data.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Failed to mark the cache as filled with data.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|The cache is not initialized and cannot be read by %1.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Failed to prepare the cache for providing data.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|The cache is being written to by %1, and cannot be read by %2.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|The cache is being read from %1 and cannot be written to by %2.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|The runtime object cannot be loaded from the specified XML node.  This happens when trying to load a package or other object from an XML node that is not of the correct type, such as a non-SSIS XML node.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Failed to open package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into the XML document. This can be the result of either providing an incorrect file name was specified when calling LoadPackage or the XML file was specified and has an incorrect format.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Failed to load XML due to error 0x%1!8.8X! "%2". This happens when loading a package and the file cannot be opened or loaded correctly into XML document.  This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Failed to load XML from package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Failed to open package file. This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Unable to decode a binary format in the package.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Unable to load the package as XML because of package does not have a valid XML format. A specific XML parser error will be posted.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Error loading from XML. No further detailed error information can be specified for this problem because no Events object was passed where detailed error information can be stored.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Cannot create an instance of the XML Document Object Model. MSXML may not be registered.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|The package cannot be loaded. This occurs when attempting to load an older version package, or the package file refers to an invalid structured object.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Failed to save package file.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Failed to save package file "%1" with error 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|The object must inherit from IDTSName100 and does not.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with package delimiter. There was no "\package" delimiter.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Failure exporting configuration file.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|Properties collection cannot be modified.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Unable to save configuration file. The file may be read only.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure property is not applicable to the package container.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|The task "%1" cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|Unable to save xml to "%1". The file may be read only.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Failed to convert a type in the configuration "%1" for the package path "%2".  This happens when a configuration value cannot be converted from a string to the appropriate destination type. Check the configuration value to ensure it can be converted to the type of the destination property or variable.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Configuration failure. This is a generic warning for all configuration types. Other warnings should precede this with more information.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Package failed validation from the ExecutePackage task. The package cannot run.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Failed to create mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" already exists and is owned by another user.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Failed to acquire mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Failed to release mutex "%1" with error 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|The wrappers task pointer is not valid. The wrapper has an invalid pointer to a task.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|The executable has been added to the Executables collection of another container. This occurs when a client tries to add an executable to more than one Executables collection. You need to remove the executable from the current Executables collection before attempting to add it.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|The connection type "%1" specified for connection manager "%2" is not recognized as a valid connection manager type. This error is returned when an attempt is made to create a connection manager for an unknown connection type. Check the spelling in the connection type name.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|An object was created but the attempt to add it to a collection failed. This can occur due to an out-of-memory condition.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|There was an error creating an Open Database Connectivity (ODBC) environment.|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|There was an error creating an Open Database Connectivity (ODBC) database connection.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|There was an error trying to establish an Open Database Connectivity (ODBC) connection with the database server.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|The qualifier is already set on this instance of the connection manager. The qualifier may be set once per instance.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|The qualifier has not been set on this instance of the connection manager. Setting the qualifier is required to complete initialization.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|This connection manager does not support specification of qualifiers.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Connection manager "0x%1" cannot be cloned for out-of-process execution.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|The log provider for SQL Server Profiler was unable to load pfclnt.dll. Please check that SQL Server Profiler is installed.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|The SSIS logging infrastructure failed with error code 0x%1!8.8X!. This error indicates that this logging error is not attributable to a specific log provider.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|The SSIS logging provider "%1" failed with error code 0x%2!8.8X! (%3).  This indicates a logging error attributable to the specified log provider.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|The SaveToSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|The LoadFromSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|The RemoveFromSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement that was issued has failed.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|The ExistsOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB has failed making a database connection when using the supplied connection string.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|When adding a precedence constraint, a From executable was specified that is not a child of this container.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|When adding a precedence constraint, the To executable specified is not a child of this container.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|There was an error trying enlist an ODBC connection in a transaction. The SQLSetConnectAttr failed to set the SQL_ATTR_ENLIST_IN_DTC attribute.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|The connection manager "%1" will not acquire a connection because the package OfflineMode property is TRUE. When the OfflineMode is TRUE, connections cannot be acquired.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|The SSIS Runtime has failed to start the distributed transaction due to error 0x%1!8.8X! "%2". The DTC transaction failed to start. This could occur because the MSDTC Service is not running.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|The SetQualifier method cannot be called on a connection manager during package execution. This method is used at design-time only.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Storing or modifying packages in SQL Server requires the SSIS runtime and database to be the same version. Storing packages in earlier versions is not supported.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Connection "%1" failed validation.|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|The file name "%1" specified in the connection was not valid.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Multiple file names cannot be specified on a connection when the Retain property is TRUE. Vertical bars were found on the connection string, meaning multiple file names are being specified and, in addition, the Retain property is TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|An ODBC error %1!d! has occurred.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|There was an error in the precedence constraint between "%1" and "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Failed to populate the ForEachEnumeratorInfos collection with native ForEachEnumerators with the following error code: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|The GetEnumerator method of the ForEach Enumerator has failed with error 0x%1!8.8X! "%2". This occurs when the ForEach Enumerator cannot enumerate.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|The raw certificate data cannot be obtained from the supplied certificate object (error: %1). This occurs when CPackage::put_CertificateObject cannot instantiate the ManagedHelper object, when the ManagedHelper object fails, or when the ManagedHelper object returns a malformed array.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Failed to create certificate context (error: %1). This occurs in CPackage::put_CertificateObject or CPackage::LoadFromXML when the corresponding CryptoAPI function fails.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Opening MY certificate store failed with error "%1".This occurs in CPackage::LoadUserCertificateByName and CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|The certificate specified by name in MY store cannot be found (error: %1). This occurs in CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Unable to find the specified certificate by hash in "MY" store (error: %1). Occurs in CPackage::LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|The hash value is not a one-dimensional array of bytes (error: %1). This occurs in CPackage::LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|The data in the array cannot be accessed (error: %1). This error can occur wherever GetDataFromSafeArray is called.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|The SSIS managed helper object failed during creation with error 0x%1!8.8X! "%2". This occurs whenever CoCreateInstance CLSID_DTSManagedHelper fails.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|The SSIS Runtime has failed to enlist the OLE DB connection in a distributed transaction with error 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Package signing failed with error 0x%1!8.8X! "%2". This occurs when the ManagedHelper.SignDocument method fails.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Failed to check for XML signature envelope in package XML with error 0x%1!8.8X! "%2". This occurs in CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Failed to obtain XML source from XML DOM object with error 0x%1!8.8X! "%2". This occurs when IXMLDOMDocument::get_xml fails.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|The cryptographic signature of the package failed verification due to error 0x%1!8.8X! "%2". This occurs when the signature verification operation fails.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Failed to obtain cryptographic key pair associated with the specified certificate with error 0x%1!8.8X! "%2". Verify that you have the key pair for which the certificate was issued. This error usually occurs when trying to sign a document using a certificate for which the person does not have the private key.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|The digital signature is not valid. The contents of the package have been modified.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|The digital signature is valid; however the signer is not trusted and, therefore, authenticity cannot be guaranteed.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|The connection does not support enlisting in distributed transaction.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Failed to apply package protection with error 0x%1!8.8X! "%2". This error occurs when saving to Xml.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Failed to remove package protection with error 0x%1!8.8X! "%2". This occurs in the CPackage::LoadFromXML method.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|The package is encrypted with a password. The password was not specified, or is not correct.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|A precedence constraint already exists between the specified executables. More than one precedence constraint is not allowed.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|The package failed to load due to error 0x%1!8.8X! "%2". This occurs when CPackage::LoadFromXML fails.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Failed to find package object in signed XML envelope with error 0x%1!8.8X! "%2". This occurs when signed XML does not contain a SSIS package, as expected.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|The lengths of parameter names, types, and descriptions arrays are not equal. The lengths must be equal. This occurs when the lengths of the arrays are mismatched. There should be one entry per parameter in each array.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|An OLE DB error 0x%1!8.8X! (%2) occurred while enumerating packages. A SQL statement was issued and failed.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|The log provider type "%1" specified for log provider "%2" is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|The log provider type is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|The connection type specified for connection manager is not a valid connection manager type. This error occurs when an attempt is made to create a connection manager for unknown connection type. Verify the spelling of the connection type name.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|An error was encountered when trying to remove the package "%1" from SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|An error was encountered when trying to create a folder on SQL Server named "%1" in folder "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|The CreateFolderOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement issued has failed.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|An error occurred when renaming folder " %1\\\\%2" to "%1\\\\%3" on SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|The RenameFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Error deleting SQL Server folder "%1".|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|The RemoveFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|The specified package path does not contain a package name. This occurs when the path does not contain at least one backslash or one forward slash.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Cannot find folder "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|While trying to find a folder on SQL an OLE DB error was encountered with error code 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|The SSIS logging provider has failed to open the log. Error code: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Failed to get ConnectionInfos collection with error 0x%1!8.8X! "%2". This error occurs when the call to IDTSApplication100::get_ConnectionInfos fails.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Deadlock detected while trying to lock variables. The locks cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|The Variables collection has not been returned from the VariableDispenser. An operation was attempted that is only allowed on dispensed collections.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|This Variables collection has already been unlocked. The Unlock method is called only once on a dispensed Variables collection.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|One or more variables failed to unlock.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|The Variables collection was returned the from VariableDispenser and cannot be modified. Items cannot be added to or removed from dispensed collections.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|The variable "%1" is already on the read list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|The variable "%1" is already on the write list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Failed to lock variable "%1" for read access with error 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Failed to lock variable "%1" for read/write access with error 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|The custom event "%1" is already declared with a different parameter list. A task is trying to declare a custom event, which another task has already declared with a different parameter list.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|The task providing the custom event "%1" does not allow this event to be handled in the package. The custom event was declared with AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|The VariableDispenser received an unsafe Variables collection. This operation cannot be repeated.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath was called on the ForEachEnumerator but there was no ForEachLoop package path specified.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|A deadlock was detected while trying to lock variable "%1" for read access. A lock could not be acquired after 16 attempts and timed out.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|A deadlock was detected while trying to lock variables "%1" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|A deadlock was detected while trying to lock variables "%1" for read access and variables "%2" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|The protection level of the package requires a password, but PackagePassword property is empty.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Failed to decrypt an encrypted XML node because the password was not specified or not correct. Package load will attempt to continue without the encrypted information.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Failed to decrypt a package that is encrypted with a user key. You may not be the user who encrypted this package, or you are not using the same machine that was used to save the package.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|The protection level, ServerStorage, cannot be used when saving to this destination. The system could not verify that the destination supports secure storage capability.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer method has failed.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|The package cannot be loaded because the state of the digital signature violates signature policy. Error 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|The package is not signed.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|The log provider for SQL Server Profiler was unable to load pfclnt.dll because it is only supported on 32-bit systems.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|The object cannot be added because another object with the same name already exists in the collection. Use a different name to resolve this error.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|The object name cannot be changed from "%1" to "%2" because another object in the collection already uses that name. Use a different name to resolve this error.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|There was an error enumerating the package dependencies. Check other messages for more information.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|The current package settings are not supported.  Please change the SaveCheckpoints property or the TransactionOption property.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|The connection manager failed to defect from the transaction.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|The specified breakpoint ID already exists. This error occurs when a task calls CreateBreakpoint with the same ID multiple times. It is possible to create a breakpoint with the same ID multiple times if the task calls RemoveBreakpoint on the first creation before creating the second one.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|The specified breakpoint ID does not exist. This error occurs when a task references a breakpoint that does not exist.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|The file, "%1", could not be opened for writing. The file could be read-only, or you do not have the correct permissions.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|No result rowset is associated with the execution of this query. The result is not correctly specified.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|Debug dump files were not generated correctly. The hresult is 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|The URL specified is not valid. This can happen when the server or proxy URL is null, or in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|The URL %1 is not valid. This can happen when a scheme other than http or https is specified, or the URL is in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Connection to server %1 cannot be established. This error can occur when the server does not exist, or the proxy settings are incorrect.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|The connection with the server has been reset or terminated. Try again later.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|The login attempt failed for "%1". This error occurs when the login credentials provided are incorrect. Verify the login credentials.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|The server name specified in the URL %1 cannot be resolved.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Proxy authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|SSL certificate response obtained from the server was not valid. Cannot process the request.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|The request has timed out. This error can occur when the timeout specified was too short, or a connection to the server or proxy cannot be established. Ensure that the server and proxy URL are correct.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Client certificate is missing. This error occurs when the server is expecting an SSL client certificate and the user has provided an invalid certificate, or has not provided a certificate. A client certificate must be configured for this connection.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|The specified server, URL %1, has a redirect and the redirect request failed.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Server authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|Request cannot be processed. Try again later.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|Server returned status code - %1!u! : %2. This error occurs when the server is experiencing problems.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|This platform is not supported by WinHttp services.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Timeout value is not valid. Timeout should be in the range of %1!d! to %2!d! (in seconds).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|The chunk size is not valid. The ChunkSize property should be in the range of %1!d! to %2!d! (in KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Error processing client certificate. This error can occur when the client certificate provided was not found in the Personal Certificate Store. Verify that the client certificate is valid.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|Server returned error code "403 - Forbidden". This error can occur when the specified resource needs "https" access, but the certificate validity period has expired, the certificate is not valid for the use requested, or the certificate has been revoked or revocation can not be checked.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Error initializing HTTP session with proxy "%1". This error can occur when an invalid proxy was specified. HTTP connection manager only supports CERN-type proxies.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Error opening certificate store.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Failed to decrypt protected XML node "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Failed to decrypt protected connection string for server "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|The version number cannot be negative. This error occurs when the VersionMajor, VersionMinor, or VersionBuild property of the package is set to a negative value.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|The package has been migrated to a later version during loading. It must be reloaded to complete the process. This is an internal error code.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Package migration from version %1!d! to version %2!d! failed with error 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Package migration module has failed to load.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Package migration module has failed.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Unable to persist object using default persistence. This error occurs when the default persistence is unable to determine which objects are on the hosted object.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|Cannot add or remove an element from a package in runtime mode. This error occurs when an attempt is made to add or remove an object from a collection while the package is executing.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|The "%1" node cannot be found in custom default persistence. This error occurs if the default saved XML of an extensible object was changed in a way that a saved object is no longer found, or if the extensible object itself changed.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|This collection cannot be modified during package validation or execution.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|The "%1" collection cannot be modified during package validation or execution. "%2" cannot be added to the collection.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|Connection with the FTP server has not been established.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|An error occurred in the requested FTP operation. Detailed error description: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|The number of retries is not valid. The number of retries should be between %1!d! and %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|The FTP connection manager needs the following DLL to function: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|The port specified in the connection string is not valid. The ConnectionString format is ServerName:Port. Port should be an integer value between %1!d! and %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Creating folder "%1" ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Deleting folder "%1" ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Changing current directory to "%1". %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|No files to transfer. This error can occur when performing a Send or Receive operation and no files are specified for the transfer.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|Specified local path is not valid. Specify a valid local path. This can occur when the specified local path is null.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|No files specified to delete.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Internal error occurred while loading the certificate. This error could occur when the certificate data is invalid.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Internal error occurred while saving the certificate data.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|Checkpoint file "%1" does not match this package. The ID of the package and the ID in the checkpoint file do not match.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|An existing checkpoint file is found with contents that do not appear to be for this package, so the file cannot be overwritten to start saving new checkpoints. Remove the existing checkpoint file and try again. This error occurs when a checkpoint file exists, the package is set to not use a checkpoint file, but to save checkpoints. The existing checkpoint file will not be overwritten.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|The checkpoint file "%1" is locked by another process. This may occur if another instance of this package is currently executing.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Checkpoint file "%1" failed to open due to error 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Checkpoint file "%1" failed during creation due to error 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|The FTP Port contains an invalid value. The FTP Port value should be an integer between %1!d! and %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Connect to SSIS Service on machine "%1" failed:<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|The Expression property is not supported on Variable objects. Use the EvaluateAsExpression property instead.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|The expression "%1" on property "%2" cannot be evaluated. Modify the expression to be valid.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|The result of the expression "%1" on property "%2" cannot be written to the property. The expression was evaluated, but cannot be set on the property.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|The evaluation expression for the loop is not valid. The expression needs to be modified. There should be additional error messages.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|The expression "%1" must evaluate to True or False. Change the expression to evaluate to a Boolean value.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|There is no expression for the loop to evaluate. This error occurs when the expression on the For Loop is empty. Add an expression.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|The assignment expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|The initialization expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|The version number in the package is not valid. The version number cannot be greater than current version number.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|The version number in the package is not valid. The version number is negative.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|The package has an older format version, but automatic package format upgrading is disabled.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|A truncation occurred during evaluation of the expression.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|The wrapper was unable to set the value of the variable specified in the ExecutionValueVariable property.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|The expression for variable "%1" failed evaluation. There was an error in the expression.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|The attempted operation is not supported with this database version.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Transaction cannot be specified when a retained connection is used. This error occurs when Retain is set to TRUE on the connection manager, but AcquireConnection was called with a non-null transaction parameter.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Incompatible transaction context was specified for a retained connection. This connection has been established under a different transaction context. Retained connections can be used under exactly one transaction context.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Resume call failed because the package is not suspended. This occurs when the client calls resume, but the package is not suspended.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Execute call failed because the executable is already executing. This error occurs when the client calls Execute on a container that is still executing from the last Execute call.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Suspend or Resume call failed because the executable is not executing, or is not the top-level executable. This occurs when the client calls Suspend or Resume on an executable that is not currently processing an Execute call.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|The file specified in the For Each File enumerator is not valid. Check that the file specified in the For Each File enumerator exists.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|The value index is not an integer . Mapping a For Each Variable number %1!d! to the variable "%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|The value index is negative. The ForEach Variable Mapping number %1!d! to variable "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|ForEach Variable Mapping number %1!d! to variable "%2" cannot be applied.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Failure when adding an object to a ForEachPropertyMapping that is not a direct child of the ForEachLoop container.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Failed to remove a system variable. This error occurs when removing a variable that is a required variable.  Required variables are variables that are created by the runtime for communicating between tasks and the runtime.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Changing the property of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Changing the name of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Changing the namespace of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Changing the event handler name failed. Event handler names are read-only.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Cannot retrieve path to object. This is a system error.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|The type of the value being assigned to variable "%1" differs from the current variable type. Variables may not change type during execution. Variable types are strict, except for variables of type Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Invalid characters in string: "%1". This occurs when a string supplied for a property value contains unprintable characters.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS object name is invalid. More specific errors would have been raised explaining the exact naming problem.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|The property "%1" is read only. This occurs when a change to a read-only property is attempted.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|The object does not support type information. This occurs when the runtime attempts to get the type information from an object to populate the Properties collection.  The object must support type information.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|The property "%1" is write-only. This error occurs when trying to retrieve the value of a property through a property object, but the property is write-only.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|The object does not implement IDispatch. This error occurs when a property object or properties collection attempts to access an IDispatch interface on an object.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Unable to retrieve the type library of the object. This error occurs when the Properties collection attempts to retrieve the type library for an object through its IDispatch interface.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Cannot create a task from XML for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Failed to create an XML document "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|An error occurred because there is a property mapping from a variable to a property with a different type. The property type must match the variable type.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Attempted to set property mapping to target unsupported object type. This error occurs when passing an unsupported object type to a property mapping.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1".  Verify that the package path is valid.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|The destination property for the property map is empty. Set the destination property name.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|The package failed to restore at least one property mapping.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|The variable name is ambiguous because multiple variables with this name exist in different namespaces. Specify namespace-qualified name to prevent ambiguity.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|The destination object in a property mapping has no parent. The destination object is not a child of any sequence container. It may have been removed from the package.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|The property mapping is not valid. The mapping is ignored.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Failure when alerting property mappings that a target is being removed.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|An invalid property mapping is found on the For Each Loop. This occurs when the ForEach property mapping fails to restore.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|A destination property was specified on a property mapping that is invalid. This occurs when a property is specified on a destination object that in not found on that object.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Cannot create a task from XML. This occurs when the runtime is unable to resolve the name to create a task. Verify that the name is correct.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|Cannot replace the existing checkpoint file with the updated checkpoint file. The checkpoint was successfully created in a temporary file, but overwriting the existing file with the new file failed.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|The package is configured to always restart from a checkpoint, but checkpoint file is not specified.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|The attempt to load the XML checkpoint file "%1" failed with error 0x%2!8.8X! "%3". Check that the file name specified is correct, and that the file exists.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|The package failed during execution because the checkpoint file cannot be loaded. Further execution of the package requires a checkpoint file. This error usually occurs when the CheckpointUsage property is set to ALWAYS, which specifies that the package always restarts.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|The evaluation condition expression on the For Loop "%1" is empty. There must be a Boolean evaluation expression in the For Loop.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|The result of the assignment expression "%1" cannot be converted to a type that is compatible with the variable that it was assigned to.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Error using a read-only variable "%1" in an assignment expression. The expression result cannot be assigned to the variable because the variable is read only. Choose a variable that can be written to, or remove the expression from this variable.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Cannot evaluate expression "%1" because the variable "%2" does not exist or cannot be accessed for writing. The expression result cannot be assigned to the variable because the variable was not found, or could not be locked for write access.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|The expression "%1" has a result type of "%2", which cannot be converted to a supported type.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|The conversion of the result of the expression"%1" from type "%2" to a supported type failed with error code 0x%3!8.8X!. An unexpected error occurred when trying to convert the expression result to a type supported by the runtime engine, even though the type conversion is supported.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|The object name is not valid. The name cannot be set to NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|The object name is not valid. The name cannot be empty.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|The object name "%1" is not valid. The name cannot contain any of the following characters: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|Object name "%1" is not valid. The name cannot contain control characters that render it unprintable.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|Object name "%1" is not valid. Name cannot begin with a whitespace.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|Object name "%1" is not valid. Name cannot end with a whitespace.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|Object name "%1" is not valid. Name must begin with an alphabetical character.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|Object name "%1" is not valid. Name must begin with an alphabetical character or underscore "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|Object name "%1" is not valid. Name must contain only alphanumeric characters or underscores "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|Object name "%1" is not valid. The name cannot contain any of the following characters: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Failed to load the value property "%1" using default persistence.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|Connection manager "%1" is not of type "%2"|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" is empty|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Invalid data node in the nodelist enumerator section|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|No enumerator can be created|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|The operation failed because the cache is in use.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|The property cannot be modified.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|The package upgrade has failed.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Error 0x%1!8.8X! while loading package file "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|The package is not specified.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|The connection is not specified.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" has an unsupported type "%2". Only "FILE" and "OLEDB" connection managers are supported.|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Error 0x%1!8.8X! while loading package file "%3" into an XML document. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Error 0x%1!8.8X! while preparing to load the package. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|The Validate method on the task failed, and returned error code 0x%1!8.8X! (%2). The Validate method must succeed and indicate the result using an "out" parameter.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|The Execute method on the task returned error code 0x%1!8.8X! (%2). The Execute method must succeed, and indicate the result using an "out" parameter.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|A failure occurred on task "%1": 0x%2!8.8X! while retrieving dependencies. The runtime was retrieving dependencies from the task's dependencies collection when the error occurred. The task may have incorrectly implemented one of the dependency interfaces.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|There were errors during task validation.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|The connection string format is not valid. It must consist of one or more components of the form X=Y, separated by semicolons. This error occurs when a connection string with zero components is set on database connection manager.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|The connection string components cannot contain unquoted semicolons. If the value must contain a semicolon, enclose the entire value in quotes. This error occurs when values in the connection string contain unquoted semicolons, such as the InitialCatalog property.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Validation of one or more log providers failed. The package cannot execute. The package does not execute when a log provider fails validation.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Invalid value in array.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|An element of the enumerator returned by the ForEach Enumerator does not implement IEnumerator, contradicting the CollectionEnumerator property of the ForEach Enumerator.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|The enumerator failed to retrieve element at index "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Function not found.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Function not found.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX Script Task was initiated with a wrong XML element.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|An error occurred while attempting to retrieve the scripting languages installed on the system.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|An error occurred while creating the ActiveX script host. Verify that you have the script host installed properly.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|An error occurred while trying to instantiate the script host for the chosen language. Verify that the script language you have chosen is installed on your system.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|An error occurred while adding the SSIS variables to the script host namespace. This might prevent the task from using SSIS variables in the script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|A fatal error occurred while trying to parse the script text. Verify that the script engine for the chosen language is installed properly.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|The function name entered is not valid. Verify that a valid function name has been specified.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|An error occurred while executing the script. Verify that the script engine for the selected language is installed properly.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|An error occurred while adding the managed type library to the script host. Verify that the DTS 2000 runtime is installed.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Bulk Insert Task was initiated with a wrong XML element.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Data file name not specified.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Failed to acquire the specified connection: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Attempt to obtain the Connection Manager failed.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|The connection is not valid.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|The connection is null.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Execution failed.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|An error occurred while retrieving the tables from the database.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|An error occurred while retrieving the columns of the table.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|An error occurred in the database operation.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|The specified connection "%1" is either not valid, or points to an invalid object. To continue, specify a valid connection.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|The destination connection specified is not valid. Supply a valid connection to continue.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|You must specify a table name to continue.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|The connection is not valid.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Execution failed.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Error occurred while retrieving the tables from the database.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Error occurred while retrieving the columns of the table.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Error occurred while trying to open the data file.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Cannot convert the input OEM file to the specified format.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Error in database operation.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|No connection manager specified.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|Connection "%1" is not an Analysis Services connection.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Unable to locate connection "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services Execute DDL task received an invalid task data node.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services Processing task received an invalid task data node.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|The DDL is not valid.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|The DDL found in ProcessingCommands is not valid.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|The Execution result cannot be saved in a read-only variable.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|Variable "%1" it's not defined.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|Connection Manager "%1" it's not defined.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|Connection Manager "%1" it's not a FILE Connection Manager.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|"%1" was not found during deserialization.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|The trace has been stopped due to an exception.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Execution of DDL failed.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|Variable "%1" is not defined.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|File connection "%1" is not defined.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Execute DTS 2000 Package task is initiated with a wrong XML element.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Package name is not specified.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|Package ID is not specified.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|Package version GUID is not specified.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server is not specified.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|SQL Server user name not specified.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Storage file name not specified.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|The DTS 2000 package property is empty.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|An error occurred while executing the DTS 2000 package.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Cannot load the available SQL Servers from the network. Check the network connection.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|The data type cannot be null. Please specify the correct data type to use for validating the value.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Cannot validate a null against any data type.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|A required argument is null.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|To execute the DTS 2000 Package task, start SQL Server Setup and use the Advanced button from the Components to Install page to select Legacy Components.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|The time-out value provided is not valid. Specify the number of seconds that the task allows the process to run. The minimum time-out is 0, which indicates that no time-out value is used and the process runs to completion or until an error occurs. The maximum time-out is 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Cannot redirect streams if the process can continue executing beyond the lifetime of the task.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|The process timed out.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|The executable is not specified.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|The standard out variable is read-only.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|The standard error variable is read-only.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|The Execute Process task received a task data node that is not valid.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|In Executing "%2" "%3" at "%1", The process exit code was "%4" while the expected was "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|The directory "%1" does not exist.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|File/Process "%1" does not exist in directory "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|Working Directory "%1" does not exist.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|The process exited with return code "%1". However, "%2" was expected.|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Synchronization object failed.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|The File System task received an invalid task data node.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|The Directory already exists.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" is not valid on operation type "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|Destination property of operation "%1" not set.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|Source property of operation "%1" not set.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is not a file.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|Variable "%1" does not exist.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|File or directory "%1" represented by connection "%2" does not exist.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|The destination file connection manager "%1" has an invalid usage type: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|The source file connection manager "%1" has an invalid usage type "%2".|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Provides information regarding File System operations.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|File System Task|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Perform file system operations, such as copying and deleting files.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Synchronization object failed.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Unable to obtain the file list.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|The local path is empty.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|The remote path is empty.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|The local variable is empty.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|The remote variable is empty.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|The FTP task received an invalid task data node.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid FTP connection is provided.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|The connection specified is not an FTP connection. Verify that a valid FTP connection is provided.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|There are no files at "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|The File "%1" doesn't contain file path(s).|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|The variable "%1" doesn't contain file path(s).|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|Variable "%1" does not exist.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Invalid path on operation "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" already exists.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is Not a file.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Directory is not specified in the variable "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|No files found in "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Directory is not specified in the file connection manager "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Unable to delete local file "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Unable to remove local directory "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Unable to create local directory "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Unable to receive files using "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Unable to send files using "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Unable to create remote directory using "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Unable to remove remote directory using "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Unable to delete remote files using "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Unable to connect to FTP server using "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|Variable "%1" doesn't start with "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|Remote path "%1" doesn't start with "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the FTP connection. Please check if you have specified a valid connection type "%1".|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Opening the certificate store failed.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|An error occurred while retrieving the display name of the certificate.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|An error occurred while retrieving the issuer name of the certificate.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|An error occurred while retrieving the friendly name of the certificate.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|The MSMQ connection name is not set.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Task was initialized with the wrong XML element.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|Data file name is empty.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|The name specified for the data file to save is empty.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|File size should be less than 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Saving the data file failed.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|String filter value is empty.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Queue path is not valid.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|The message queue task does not support enlisting in distributed transactions.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|The message type is not valid.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|The message queue timed out. No message has been received.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|The property specified is not valid. Verify that the argument type is correct.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Message is not authenticated.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|You are trying to set the value of Encryption Algorithm with an invalid object.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|The variable to receive string message is empty.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|Variable to receive variable message is empty.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|Connection "%1" is not of type MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|The data file "%1" already exists at the specified location. Cannot overwrite the file as the Overwrite option is set to false.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|The specified variable "%1" to receive string message is not found in the package variable collection.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|The connection manager "%1" is empty.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|The connection manager "%1" does not exist.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Error "%1": "%2"\r\nLine "%3"   Column "%4" through "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|There was an error compiling the script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Error "%1": "%2"\r\nLine "%3" Columns "%4"-"%5"\r\nLine Text: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|User script returned a failure result.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|User script files failed to load.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|User script threw an exception: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Could not create an instance of entrypoint class "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|There was an exception while loading Script Task from XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|Source item "%1" was not found in the package.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|Binary item "%1" was not found in the package.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" was not recognized as a valid script language.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|The script name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|The script language specified is not valid.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Cannot initialize to a null task.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|The Script Task user interface must initialize to an Script Task.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|The Script Task user interface is not initialized.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|Name cannot be empty.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|The project name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|The script language specified is not valid.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Entry point not found.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|The script language is not specified. Verify that a valid script language is specified.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|User interface initialization: The task is null.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|The Script Task user interface is initialized with an incorrect task.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|No recipient is specified.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|The Simple Mail Transfer Protocol (SMTP) server is not specified. Provide a valid name or IP address of the SMTP server.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Send Mail task is initiated with an incorrect XML element.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|Either the file "%1" does not exist or you do not have permissions to access the file.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Verify that the Simple Mail Transfer Protocol (SMTP) server specified is valid.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type File.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|On operation "%1", file "%2" does not exist.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|Connection "%1" is not of type SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|Connection "%1" is empty.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|The specified connection "%1" does not exist.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|No Transact-SQL statement specified.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|The connection does not support XML result sets.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Cannot locate a handler for the specified connection type.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|No connection manager is specified.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Cannot acquire a connection from the connection manager.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Cannot have a null parameter name.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|The parameter name is not valid.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Valid parameter names are of type Int or String.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|Variable "%1" cannot be used in a result binding because it is read-only.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|The index is not assigned in this collection.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|The variable "%1" cannot be used as an "out" parameter or return value in a parameter binding because it is read-only.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|The object does not exist in this collection.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Cannot acquire a managed connection.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Cannot populate the result columns for a single row result type. The query returned an empty result set.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|There is an invalid number of result bindings returned for the ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|The result binding name must be set to zero for full result set and XML results.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|The parameter directions flag is not valid.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|The XML fragment does not contain SQL Task data.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|A parameter with type return value is not the first parameter, or there are more than one parameter of type return value.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not a file connection manager.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|Type of variable "%1" is not string.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|Variable "%1" does not exist or could not be locked.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|Connection manager "%1" does not exist.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Failed to acquire connection "%1". Connection may not be configured correctly or you may not have the right permissions on this connection.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Result binding by name "%1" is not supported for this connection type.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|A result set type of single row is specified, but no rows were returned.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|No disconnected record set is available for the Transact-SQL statement.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Unsupported type.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Unknown type.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Unsupported data type on parameter binding \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|Parameter names cannot be an mix of ordinal and named types.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|The parameter direction on parameter binding \\"%s\\" is not valid.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|The data type on result set binding \\"%s\\" is not supported.|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|The result column index %d is not valid.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Cannot find column \\"%s\\" in the result set.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|No result rowset is associated with the execution of this query.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Disconnected recordsets are not available from ODBC connections.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|The data type in the result set, column %hd, is not supported.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|Cannot load XML with query result.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|A connection name or variable name for the package must be specified.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Failed to create the package.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|The TableMetaDataNode is not an XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Failed to create the pipeline.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|The variable is not the correct type.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|The connection manager specified is not a FILE connection manager.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Invalid file name specified on the connection manager "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid HTTP connection is specified.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|The connection does not exist. Verify that a valid, existing HTTP connection is specified.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|The Web Service name is empty. Verify that a valid web service name is specified.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|The web method name is empty. Verify that a valid web method is specified.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|The web method is empty or may not exist. Verify that there is an existing web method to specify.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|The output location is empty. Verify that an existing file connection or variable is specified.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|The variable cannot be found. Verify that the variable exists in the package.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Cannot save the result. Verify that the variable is not read-only.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|The Web Service Task is initiated with an incorrect XML element.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Unexpected XML element found.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the HTTP connection. Verify that a valid connection type is specified.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Cannot save the result. Verify that there is an existing file connection.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Cannot save the result. Verify that the file exists.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Cannot save the result. The file name is empty or the file is in use by another process.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|There was an error in acquiring the file connection. Verify that a valid file connection is specified.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Only Complex Types with Primitive values, Primitive Arrays, and Enumerations are supported.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Only Primitive, Enum, Complex, PrimitiveArray, and ComplexArray types are supported.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|This version of WSDL is not supported.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Initialized with an incorrect XML element.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|A mandatory attribute is not found.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|The enum "%1" does not have any values. The WSDL is corrupted.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|The connection cannot be found.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Connection by this name already exists.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|Connection cannot be null or empty.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|The specified Uniform Resource Identifier (URI) does not contain a valid WSDL.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Could not read the WSDL file. The input WSDL file is not valid. The reader threw the following error: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|Service Description cannot be null.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|Service name cannot be null.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL cannot be null.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|The service is not currently available.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|The service is not available on the SOAP port.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find the Binding that corresponds to the SOAP port.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find a PortType that corresponds to the SOAP port.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Cannot find the message that corresponds to the method specified.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Could not generate the proxy for the given web service. The following errors were encountered while generating the proxy "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Could not load the proxy for the given web service. The exact error is as follows: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Could not find the specified service. The exact error is as follows: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|The Web Service threw the following error during method execution: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Could not execute the web method. The exact error is as follows: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo cannot be null.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|The specified WebMethodInfo is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue is not of type PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|The WebMethodInfo you have specified is wrong. "%1" is not Primitive Type.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|The format of the ArrayValue is not valid. There should be at least one element in the array.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|The value of the enumeration cannot be null. Select a default value for the enumeration.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Cannot validate a null against any datatype.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|The enumeration Value is not correct.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|The class specified does not contain a public property by the name "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Cleanup failed. The proxy that was created for the web service may not have been deleted.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Could not create an object of type "%1". Please check whether the default constructor exists.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|The data type cannot be null. Specify the value of the data type to validate.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|The ParamValue cannot be inserted at this position. The index specified might be lesser than zero or greater than the length.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|The input WSDL file is not valid.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|The destination must be set.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|No WMI connection is set.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI Data Reader Task received an invalid task data node.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|The task failed validation.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|Variable "%1" is not of type string or object.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|Variable "%1" should be of type object to be assigned a data table.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Task failed due to invalid WMI query: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Unable to write to variable "%1" since it set to keep its original value.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|The WMI connection is missing.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|The task failed to execute the WMI query.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|The WMI Event Watcher Task received a task data node that is not valid.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Timeout of "%1" second(s) occurred before event represented by "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Watching for the Wql query caused the following system exception: "%1". Check the query for errors or WMI connection for access rights/permissions.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|The Operations specified is not defined.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|The connection type is not File.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Cannot get an XmlReader from the source XML document.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Cannot get an XmlReader from the changed XML document.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Cannot get the XDL diffgram reader from the XDL diffgram XML.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|The node list is empty.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|The element was not found.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|The Operations specified is not defined.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Unexpected content item in XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|No schema found to enforce validation.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|A validation error occurred when validating the instance document.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|The root nodes do not match.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|The Edit Script Operation type in the final Edit Script is not valid.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|CDATA nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Comment nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Text nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Significant white space nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Correct the OperationCost array so that it reflects the XmlDiffOperation enumeration.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|There are no operations in the task.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|The document already contains data and should not be used again.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|The node type is not valid.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|The XML Task received a task data node that is not valid.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|Variable data type is not a String.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Cannot get encoding from XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|Source is not specified.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|Second operand is not specified.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Invalid XDL diffgram. "%1" is an invalid path descriptor.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Invalid XDL diffgram. No node matches the path descriptor "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Invalid XDL diffgram. Expecting xd:xmldiff as a root element with namespace URI "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute on the xd:xmldiff element is missing.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute on the xd:xmldiff element is missing.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute has an invalid value.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute has an invalid value.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|The XDL diffgram is not applicable to this XML document. The rcDocHash value does not match.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Invalid XDL diffgram; more than one node matches the "%1" path descriptor on the xd:node or xd:change element.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|The XDL diffgram is not applicable to this XML document. A new XML declaration cannot be added.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Internal Error. XmlDiffPathSingleNodeList can contain only one node.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Internal Error. "%1" nodes left after patch, expecting 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|The File/Text Produced by the XSLT is not a valid XmlDocument, thus can not be set as result of operation: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|Property "%1" has no source Xml text; Xml Text is either invalid, null or empty string.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|A source connection must be specified.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|A destination connection must be specified.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|The connection "%1" could not be found in the package.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|The connection "%1" specifies a SQL Server instance with a version that is not supported for transfer.  Only versions 7, 2000, and 2005 are supported.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|The source connection "%1" must specify a SQL Server instance with a version earlier than or the same as the destination connection "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|A source database must be specified.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|The source database "%1" must exist on the source server.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|A destination database must be specified.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|The source database and the destination database can not be the same.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|The transfer file information %1 is missing the filename.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|The transfer file information %1 is missing the folder part.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|The transfer file information %1 is missing the network share part.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|The number of source transfer files and the number of destination transfer files must be the same.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|Enlisting in transactions is not supported.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|The following exception occurred during an offline database transfer: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|The network share "%1" could not be found.|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|The network share "%1 could not be accessed.  The error is: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|The user "%1" must be a DBO or a sysadmin for "%2" in order to perform an online database transfer.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|The user "%1" must be a sysadmin on "%2" to perform an offline database transfer.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Full text catalogs can only be included when performing an offline database transfer between 2 SQL Server 2005 servers.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|The database "%1" already exists on the destination server "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|At least one source file must be specified.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Could not find the file "%1" in the source database "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|The operation requested is not allowed in systems compliant with U.S. FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Executing the query "%1" failed with the following error: "%2". Possible failure reasons: Problems with the query, "ResultSet" property not set correctly, parameters not set correctly, or connection not established correctly.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Error reading stored procedure names from the xml file.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Invalid data node for the Transfer Stored Procedure task.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|Connection "%1" is not of type "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Execution failed with the following error "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|An error occurred with the following error message: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Bulk insert execution failed.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Invalid destination path.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Can not create directory. User chose to fail the task if directory exists.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|The task has a transaction option of "Required" and connection "%1" is of type "ODBC". ODBC connections don't support transactions.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|An error occurred while assigning a value to variable "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|The source is empty.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|The destination is empty.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|File or directory "%1" does not exist.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|Variable "%1" is used as a source or destination and is empty.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|The variable "%1" should be of type object to be assigned a data table.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|The variable "%1" does not have a string data type.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|There was an error acquiring the FTP connection. Verify that a valid connection type is specified in "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|The FTP connection manager "%1" can not be found.|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|File usage type of connection "%1" should be "%2" for operation "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|The source server can not be the same as the destination server.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|There are no Error Messages to transfer.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|The lists of error messages and their corresponding languages are of different sizes.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|The error message id "%1" is out of the allowed range of user defined error messages. User defined error message ids are between 50000 and 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|This task can not participate in a transaction.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Failed to transfer some or all of the Error Messages.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|The error message "%1" can not be found at source server.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Execution failed with the following error: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Failed to transfer the Job(s).|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|There are no Jobs to transfer.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|The job "%1" can not be found at source server.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|The list of "Logins" to transfer is empty.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Can not get the list of "Logins" from source server.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|Login "%1" already exists at destination server.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|Login "%1" does not exist at source.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Failed to transfer some or all of the logins.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Failed to transfer the stored procedure(s). More informative error should have been raised.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Stored Procedure "%1" is not found at the source.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|Stored procedure "%1" already exists at destination server.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|There are no stored procedures to transfer.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Failed to transfer the object(s).|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|The list of "Objects" to transfer is empty.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|Stored procedure "%1" does not exist at the source.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|An error occurred while trying to get set the Stored Procedures list to transfer: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|Rule "%1" does not exist at the source.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|An error occurred while trying to get set the Rules list to transfer: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|Table "%1" does not exist at the source.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|An error occurred while trying to get set the Tables list to transfer: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|View "%1" does not exist at the source.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|An error occurred while trying to get set the Views list to transfer: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|User Defined Function "%1" does not exist at the source.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|An error occurred while trying to get set the User Defined Functions list to transfer: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|Default "%1" does not exist at the source.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|An error occurred while trying to get set the Defaults list to transfer: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|User Defined Data Type "%1" does not exist at the source.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|An error occurred while trying to get set the User Defined Data Types list to transfer: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|Partition Function "%1" does not exist at the source.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|An error occurred while trying to get set the Partition Functions list to transfer: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|Partition Scheme "%1" does not exist at the source.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|An error occurred while trying to get set the Partition Schemes list to transfer: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|Schema "%1" does not exist at the source.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|An error occurred while trying to get set the Schemas list to transfer: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1" does not exist at the source.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|An error occurred while trying to get set the SqlAssemblies list to transfer: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|User Defined Aggregate "%1" does not exist at the source.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|An error occurred while trying to get set the User Defined Aggregates list to transfer: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|User Defined Type "%1" does not exist at the source.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|An error occurred while trying to get set the User Defined Types list to transfer: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1" does not exist at the source.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|An error occurred while trying to get set the XmlSchemaCollections list to transfer: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Objects of type "%1" are only supported between SQL Server 2005 or newer servers.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|The databases list is empty.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|Login "%1" does not exist at the source.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|An error occurred while trying to get set the Logins list to transfer: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|User "%1" does not exist at the source.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|An error occurred while trying to get set the Users list to transfer: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|The task can not have a retained connection manager in a transaction.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|Unable to obtain XML data from SQL Server as Unicode because the provider does not support the OUTPUTENCODING property.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|For the FTP operation "%1", the FILE connection manager "%2" can not be found.|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"Logins" are server level objects and can not be dropped first since the source and destination are the same server. Dropping objects first will remove the logins from the source as well.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|Parameter "%1" cannot be negative. (-1) is used for the default value.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Data Flow objects cannot be loaded. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Data Flow objects cannot be saved. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Failed to save Data Flow objects.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Failed to load Data Flow objects|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Failed to save Data Flow objects. The specified format is not supported.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Failed to load Data Flow objects. The specified format is not supported.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Failed to set the XML persistence events property for the Data Flow objects.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Failed to set the persistence XML DOM property for the Data Flow objects.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Failed to set the persistence XML ELEMENT property for the Data Flow objects.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Failed to set xml persistence properties for the Data Flow objects.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Failed to get custom property collection for Data Flow components.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|An execution tree contains a cycle.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|The %1 object "%2" (%3!d!) is disconnected from the layout.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|The ID for the layout object is not valid.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|A required input object is not connected to a path object.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 has an invalid synchronous input ID %2!d!.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 has lineage ID %2!d!, but should have had %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|The package contains two objects with the duplicate name of "%1" and "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|The "%1" and the "%2" are in the same exclusion group, but they do not have the same synchronous input.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Two objects in the same collection have a duplicate lineage ID of %1!d!. The objects are %2 and %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|The layout failed validation.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|One or more component failed validation.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|The layout and one or more components failed validation.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|The Data Flow task engine failed at startup because it cannot create one or more required threads.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|A thread failed to create a mutex at initialization.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|A thread failed to create a semaphore at initialization.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|The system reports %1!d! percent memory load. There are %2 bytes of physical memory with %3 bytes free. There are %4 bytes of virtual memory with %5 bytes free. The paging file has %6 bytes with %7 bytes free.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|A buffer failed while allocating %1!d! bytes.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|The Buffer Manager could not be created.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Buffer Type %1!d! had a size of %2!I64d! bytes.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 is marked as dangling, but has a path attached to it.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 failed validation and returned error code 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 failed the post-execute phase and returned error code 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 failed the prepare phase and returned error code 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 failed the pre-execute phase and returned error code 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 failed the cleanup phase and returned error code 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 has lineage ID %2!d! that was not previously used in the Data Flow task.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|Cannot connect %1 to %2 because a cycle would be created.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|The data type "%1" cannot be compared. Comparison of that data type is not supported, so it cannot be sorted or used as a key.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|This thread has shut down and is not accepting buffers for input.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS Error Code DTS_E_THREADFAILED.  Thread "%1" has exited with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the thread has exited.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS Error Code DTS_E_PROCESSINPUTFAILED.  The ProcessInput method on component "%1" (%2!d!) failed with error code 0x%3!8.8X! while processing input "%4" (%5!d!). The identified component returned an error from the ProcessInput method. The error is specific to the component, but the error is fatal and will cause the Data Flow task to stop running.  There may be error messages posted before this with more information about the failure.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|A set of virtual buffers cannot be realized.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|The number of threads required for this pipeline is %1!d!, which is more than the system limit of %2!d!. The pipeline requires too many threads as configured. There are either too many asynchronous outputs, or EngineThreads property is set too high. Split the pipeline into multiple packages, or reduce the value of the EngineThreads property.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|The Data Flow engine scheduler cannot obtain a count of the sources in the layout.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|The Data Flow engine scheduler cannot obtain a count of the destinations in the layout.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|The component view is unavailable. Make sure the component view has been created.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|The component view ID is incorrect. The component view may be out of synchronization. Try releasing the component view and recreating it.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|This buffer is not locked and cannot be manipulated.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|The Data Flow task cannot allocate memory to build a buffer definition. The buffer definition had %1!d! columns.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|The Data Flow task cannot register a buffer type. The type had %1!d! columns and was for execution tree %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|The UsesDispositions property cannot be changed from its initial value. This occurs when the XML is edited and the UsesDispositions value is modified. This value is set by the component when it is added to the package and is not allowed to change.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|The Data Flow task failed to initialize a required thread and cannot begin execution. The thread previously reported a specific error.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|The Data Flow task failed to create a required thread and cannot begin running. The usually occurs when there is an out-of-memory state.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|The synchronous input of "%1" cannot be set to "%2" because a cycle would be created.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|A custom property named "%1" is invalid because there is a stock property with that name. A custom property cannot have the same name as a stock property on the same object.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|The buffer was already unlocked.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 failed initialization and returned error code 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 failed during shut down and returned error code 0x%2!8.8X!. A component failed to release its interfaces.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS Error Code DTS_E_PRIMEOUTPUTFAILED.  The PrimeOutput method on %1 returned error code 0x%2!8.8X!.  The component returned a failure code when the pipeline engine called PrimeOutput(). The meaning of the failure code is defined by the component, but the error is fatal and the pipeline stopped executing.  There may be error messages posted before this with more information about the failure.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS Error Code DTS_E_THREADCANCELLED.  Thread "%1" received a shutdown signal and is terminating. The user requested a shutdown, or an error in another thread is causing the pipeline to shutdown.  There may be error messages posted before this with more information on why the thread was cancelled.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|Distributor for thread "%1" failed to initialize property "%2" on component "%3" because of error 0x%8.8X. The distributor could not initialize the component's property and cannot continue running.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|The Data Flow task cannot register a view buffer type. The type had %1!d! columns and was for input ID %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|There is not enough memory to create an execution tree.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|There is not enough memory to insert an object into the hash table.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|The object is not in the hash table.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Cannot create a component view because another one already exists. Only one component view can exist at a time.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|At input "%1" (%2!d!), the virtual input column collection does not contain a virtual input column with lineage ID %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|The requested object has the incorrect object type.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|The buffer manager cannot create a temporary storage file on any path in the BufferTempStoragePath property. There is an incorrect file name or no permission or the paths have been full.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|The buffer manager could not seek to offset %1!d! in file "%2". The file is damaged.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|The buffer manager cannot extend the file "%1" to length %2!lu! bytes.  There was insufficient disk space.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|The buffer manager cannot write %1!d! bytes to file "%2". There was insufficient disk space or quota.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|The buffer manager cannot read %1!d! bytes from file "%2". The file is damaged.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|Buffer ID %1!d! supports other virtual buffers and cannot be placed into sequential mode. IDTSBuffer100.SetSequentialMode was called on a buffer that supports virtual buffers.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|This operation could not be performed because buffer is in read-only mode. A read-only buffer cannot be modified.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|ID %1 cannot be set to %2!d! because a cycle would be created.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|The buffer manager ran out of memory while trying to extend the table of buffer types. This is caused by an out-of-memory condition.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|The buffer manager failed to create a new buffer type.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|The Data Flow engine scheduler failed to retrieve the execution tree with index %1!d! from the layout. The scheduler received a count containing more execution trees than actually exist.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|The Data Flow task failed to create a buffer to call PrimeOutput for output "%3" (%4!d!) on component "%1" (%2!d!). This error usually occurs due to an out-of-memory condition.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|The Data Flow engine scheduler failed to create a thread object because not enough memory is available. This is caused by an out-of-memory condition.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|The Data Flow engine scheduler cannot retrieve object with ID %1!d! from the layout. The Data Flow engine scheduler previously located an object that is now no longer available.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|The Data Flow task failed to prepare buffers for the execution tree node beginning at output "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|The Data Flow task cannot create a virtual buffer to prepare for execution.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|The maximum ID has been reached. There are no more IDs available to assign to objects.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|The %1 is already attached and cannot be attached again.  Detach it and try again.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|Column name "%1" on output "%2" cannot be used because it conflicts with a column of the same name on synchronous input "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|The Data Flow task cannot to create a buffer to mark the end of the rowset.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|A managed user component has thrown exception "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|The Data Flow engine scheduler cannot allocate enough memory for the execution structures. The system was low on memory before execution started.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|An out-of-memory condition prevented the creation of the buffer object.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|An out-of-memory condition prevents the mapping of a buffer's lineage IDs to DTP_HCOL indexes.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|The "%1!s!" cannot cache the Variables collection and returned error code 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|The "%1" failed to cache the component metadata object and returned error code 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" has a non-zero SortKeyPosition, but its value (%2!ld!) is too large. It must be less than or equal to the number of columns.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but the absolute values of the non-zero output column SortKeyPositions do not form a monotonically increasing sequence, starting at one.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" failed validation and returned validation status "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|Component "%1!s!" could not be created and returned error code 0x%2!8.8X! "%3!s!". Make sure that the component is registered correctly.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|The module containing "%1" is not registered or installed correctly.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|The module containing "%1" cannot be located, even though it is registered.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|The script component is configured to pre-compile the script, but binary code is not found. Please visit the IDE in Script Component Editor by clicking Design Script button to cause binary code to be generated.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|The buffer manager cannot create a file to spool a long object on the directories named in the BLOBTempStoragePath property.  Either an incorrect file name was provided, or there are no permissions, or the paths have been full.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|The SynchronousInputID property on "%1" was %2!d!, and %3!d! was expected.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|No object exists with the ID %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Unable to locate an object with ID %1!d! because of the error code 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|The code page %1!d! specified on output column "%2" (%3!d!) is not valid. Select a different code page for output column "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|The EventInfos collection could not be cached by "%1" and returned error code 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|The name for "%1" is a duplicate.  All names must be unique.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|There is no output column associated with input column "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" has a virtual buffer extending from a root source. There is an exclusion group that is not zero with a synchronous input that is zero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" cannot be an error output because error outputs cannot be placed on synchronous, non-exclusive outputs.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|A divide-by-zero error occurred. The right side operand evaluates to zero in the expression "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|The literal "%1" is too large to fit into type %2. The magnitude of the literal overflows the type.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|The result of the binary operation "%1" on data types %2 and %3 exceeds the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|The result of the binary operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|The result of the function call "%1" is too large to fit in type "%2". The magnitude of the result of the function call overflows the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|The data types "%1" and "%2" are incompatible for binary operator "%3". The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|The data type "%1" cannot be used with binary operator "%2". The type of one or both of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator "%1" in operation "%2". Both operands for this operator must be positive or negative.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|The binary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or an out-of-memory condition exists.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Attempt to set the result type of binary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Comparing "%1" to string "%2" failed.|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|The data type "%1" cannot be used with unary operator "%2". This operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|The unary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or there is an out-of-memory condition.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Attempt to set the result type of unary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|The function "%1" does not support the data type "%2" for parameter number %3!d!. The type of the parameter could not be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|The function "%1" was not recognized. Either the function name is incorrect or does not exist.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|The length %1!d! is not valid for function "%2". The length parameter cannot be negative. Change the length parameter to zero or a positive value.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|The start index %1!d! is not valid for function "%2". The start index value must be an integer greater than 0. Start index is one-based, not zero-based.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|The function "%1" cannot perform the character mapping on string "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" is not a valid date part for function "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Parameter number %1!d! of the function NULL with data type "%2" is not valid. The parameters of NULL() must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Parameter number %1!d! of the function NULL with data type "%2" is not an integer. A parameter of NULL() must be an integer or a type that can be converted to an integer.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Parameter number %1!d! of the function "%2" is not static. This parameter must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Parameter number %1!d! of the cast to data type "%2" is not valid. The parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Parameter number %1!d! of the cast to data type "%2" is not an integer. A parameter of a cast operator must be an integer or a type that can be converted to an integer.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Cannot cast expression "%1" from data type "%2" to data type "%3". The requested cast is not supported.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Attempt to parse the expression "%1" failed.  The token "%2" at line number "%3", character number "%4" was not recognized. The expression cannot be parsed because it contains invalid elements at the location specified.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|An error occurred when parsing the expression "%1". The expression failed to parse for an unknown reason.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Attempt to parse the expression "%1" failed and returned error code 0x%2!8.8X!. The expression cannot be parsed. It might contain invalid elements or it might not be well-formed. There may also be an out-of-memory error.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|The expression "%1" is not valid and cannot be parsed. The expression may contain invalid elements or it may not be well-formed.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|There was no expression to compute. An attempt was made to compute or get the string of an empty expression.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Attempt to compute the expression "%1" failed with error code 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed with error code 0x%1!8.8X!. Failed when attempting to generate a displayable string that represents the expression.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Cannot convert the expression result data type "%1" to the column data type "%2". The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression "%1" of the conditional operator has an invalid data type of "%2". The conditional expression of the conditional operator must return a Boolean, which is type DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|The data types "%1" and "%2" are incompatible for the conditional operator. The operand types cannot be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Attempt to set the result type of conditional operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|This buffer has been orphaned. The buffer manager has shut down, leaving an outstanding buffer and no cleanup will occur for the buffer. There is a potential for memory leaks and other problems.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Attempt to find the input column named "%1" failed with error code 0x%2!8.8X!. The input column specified was not found in the input column collection.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Attempt to find the input column with lineage ID %1!d! failed with error code 0x%2!8.8X!. The input column was not found in the input column collection.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|The expression contains unrecognized token "%1". If "%1" is a variable, it should be expressed as "\@%1". The specified token is not valid. If the token is intended to be a variable name, it should be prefixed with the \@ symbol.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|The expression contains unrecognized token "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|The variable "%1" was not found in the Variables collection. The variable might not exist in the correct scope.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Attempt to parse the expression "%1" failed. The expression might contain an invalid token, an incomplete token, or an invalid element. It might not be well-formed, or might be missing part of a required element such as a parenthesis.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|The name for "%1" is blank, and names cannot be blank.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|The "%1" has the HasSideEffects property set to TRUE, but "%1" is synchronous and cannot have side effects. Set the HasSideEffects property to FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|The value, %1!d!, specified for the code page parameter of the cast to data type "%2", is not valid. The code page is not installed on the machine.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|The value %1!d! specified for the precision parameter of the cast to data type "%2" is not valid. Precision must be in the range %3!d! to %4!d! and the precision value is out of range for the type cast.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|The value %1!d! specified for the scale parameter of the cast to data type "%2" is not valid. The scale must be in the range %3!d! to %4!d! and the scale value is out of range for the type cast. Scale must not exceed precision and must be positive.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|The IsSorted property for "%1" is false, but %2!lu! of its output columns' SortKeyPositions are non-zero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|The code pages must match for operands of conditional operation "%1" for type %2. The code page of the left operand does not match the code page of the right operand. For the conditional operator on the specified type, the code pages must be the same.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|Input "%1" (%2!d!) references input "%3" (%4!d!), but they do not have the same number of columns. Input %5!d! has %6!d! columns, while input %7!d! has %8!d! columns.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|No object exists with a lineage ID of %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|The output column for the file name cannot be found.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|The output column for the file name is not a null-terminated Unicode character string, which is data type DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|A distributor failed to give a buffer to thread "%1" because of error 0x%2!8.8X!. The target thread is probably shutting down.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|The LocaleID %1!ld! is not installed on this system.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal hexadecimal escape sequence of  "\x%2". The escape sequence is not supported in string literals in the expression evaluator. The hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal escape sequence of "\\%2!c!". The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, use a double backslash, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" 未包含輸出資料行。 非同步輸出必須包含輸出資料行。|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|"%1" 具有 Long 物件資料類型 DT_TEXT、DT_NTEXT 或 DT_IMAGE，但不受支援。|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|輸出識別碼 %1!d! 有多個錯誤輸出組態。 第一個為 %2!d! 和 %3!d!，接著為 %4!d! 和 %5!d!。|  
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
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|預設緩衝區大小必須介於 %1!d! 與 %2!d! 的資料行 。 嘗試將 DefaultBufferSize 屬性設定為太小或太大的值。|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|預設緩衝區最大資料列數必須大於 %1!d! 個資料列 資料列。 嘗試將 DefaultBufferMaxRows 屬性設定為太小的值。|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|%1 的字碼頁為 %2!d!， 但必須是 %3!d!。|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|無法將 %3!d! 指派給資料流程工作的 EngineThreads 屬性 。 值必須介於 %1!d! 至 %2!d! 之間 。|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|剖析運算式 "%1" 失敗。 行號 "%2"、字元編號 "%3" 的單引號為非預期的。|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|剖析運算式 "%1" 失敗。 不需要行號 "%2"、字元編號 "%3" 上的等號 (=)。 在指定的位置上可能需要雙等號 (==)。|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|元件 "%1" 無法快取執行階段物件參考追蹤程式集合，傳回錯誤碼 0x%2!8.8X!。|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|多個輸入資料行的名稱為 "%1"。 所要的輸入資料行必須唯一指定為 [Component Name].[%2]，或以歷程識別碼來參考。 目前，指定的輸入資料行存在於一個以上的元件中。|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|尋找名稱為 "[%1].[%2]" 的輸入資料行失敗，錯誤碼為 0x%3!8.8X!。 在輸入資料行集合中找不到此輸入資料行。|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|多個變數的名稱為 "%1"。 所要的變數必須唯一指定為 \@[Namespace::%2]。 此變數存在於一個以上的命名空間中。|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|資料流程引擎排程器無法縮減管線的執行計畫。 請將 OptimizedMode 屬性設定為 false。|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|函數 SQRT 無法用於負值，而且負值已傳遞至 SQRT 函數。|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|函數 LN 無法用於零或負值，而且零或負值已傳遞至 LN 函數。|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|函數 LOG 無法用於零或負值，而且零或負值已傳遞至 LOG 函數。|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|無法評估傳遞至函數 POWER 的參數，而且產生未定的結果。|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|因為錯誤 0x%1!8.8X!，所以執行階段無法提供取消事件。|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|管線收到取消的要求，正在關閉中。|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|一元減號 (負) 運算的結果 "%1" 超出結果資料類型 "%2" 的大小上限。 運算結果的大小造成結果類型溢位。|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|運算式中發現預留位置 "%1"。 必須使用實際參數或運算元取代。|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|對函數 "%2" 而言，長度 %1!d! 。 長度參數必須為正數。|  
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
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|"%2" 的 "%1" 自訂屬性不能設定為 true。  資料行資料類型必須是下列其中一項：DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4、DT_UI8、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAMPOFFSET、DT_DATE、DT_DBDATE、DT_DBTIME、DT_DBTIME2 或 DT_FILETIME。|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|無法重新附加 "%1"。 請刪除路徑、加入新路徑，然後再附加。|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|函數 "%1" 需要 %2!d! 參數， 而非 %3!d! 參數。 已辨識函數名稱，但參數數目無效。|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|函數 "%1" 需要 %2!d! 參數， 而非 %3!d! 參數。 已辨識函數名稱，但參數數目無效。|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|函數 "%1" 需要 %2!d! 參數， 而非 %3!d! 參數。 已辨識函數名稱，但參數數目無效。|  
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
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|指定了模稜兩可的變數名稱。 所要的變數必須指定為 \@[Namespace::Variable]。 當變數存在於一個以上的命名空間中時，就會發生這個錯誤。|  
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
|0xC0202002|-1071636478|DTS_E_COMERROR|有 COM 錯誤物件資訊可用。  來源: "%1"  錯誤碼:0x%2!8.8X!  描述: "%3"。|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|無法存取已取得的連接。|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|資料行數目不正確。|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|在資料來源中找不到資料行 "%1"。|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|有 OLE DB 記錄可用。  來源: "%1"  Hresult:0x%2!8.8X!  描述: "%3"。|  
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
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|無法從檔案 "%2" 讀取 %1!d! 。 先前應該已經報告失敗的原因。|  
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
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|輸出資料行 "%1" (%2!d!) 的 SourceColumn %3!d! 不是有效的輸入資料行歷程識別碼。|  
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
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|不支援從字碼頁為 %2!d! 的 "%1" 轉換成字碼頁為 %4!d! 的 "%3" 。|  
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
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|輸出識別碼 %1!d! 失敗。 未建立新的輸出。|  
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
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|排序轉換無法比較緩衝區識別碼 %2!d! 中的資料列 %1!d! 和緩衝區識別碼 %4!d! 中的資料列 %3!d! 。|  
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
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|歷程識別碼為 %1!d! 與 %2!d! 的資料行 各有不相符的中繼資料。 輸入資料行 (對應到 Copymap 的輸出資料行) 沒有相同的中繼資料 (資料類型、有效位數、小數位數、長度或字碼頁)。|  
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
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|無法讀取指定的預先建立比對索引 "%1"。  OLEDB 錯誤碼：0x%2!8.8X!。|  
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
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|歷程識別碼為 %1!d! 與 %2!d! 的資料行 各有不相符的中繼資料。 對應至輸出資料行的輸入資料行沒有相同的中繼資料 (資料類型、有效位數、小數位數、長度或字碼頁)。|  
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
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|沒有任何元件使用彙總元件識別碼為 %1!d! 的輸出。 請將它移除，或將它與某個元件的輸入建立關聯。|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 無法將快取寫入檔案 "%2"。 hresult 為 0x%3!8.8X!。|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|元素 "%2" 上 "%1" 的 XML 結構描述資料類型資訊已變更。  請重新初始化這個元件的中繼資料，並檢閱資料行對應。|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 未用在聯結或複製中。 請從輸入資料行清單中移除未使用的資料行。|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|由於排序內送緩衝區時發生堆疊溢位，所以排序失敗。  請減少資料流程工作的 DefaultBufferMaxRows 屬性。|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|請考慮將連接字串中的 PROVIDER 變更為 %1，或前往 https://www.microsoft.com/downloads 以尋找並安裝 %2 的支援。|  
|||DTS_E_INITTASKOBJECTFAILED|無法為工作 "%1!s!"、類型 "%2!s!" 初始化工作物件， 因為錯誤 0x%3!8.8X! "%4!s!"。|  
|||DTS_E_GETCATMANAGERFAILED|無法建立 COM 元件類別目錄管理員，因為錯誤 0x%1!8.8X! "%2!s!"。|  
|||DTS_E_COMPONENTINITFAILED|元件 %1!s! 無法初始化，因為錯誤 0x%2!8.8X! "%3!s!"。|  
  
##  <a name="msgWarning"></a> 警告訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 警告訊息的符號名稱以 **DTS_W_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|評估期還剩 %1!lu! 天。 過期之後，就無法執行封裝。|  
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
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|父變數 "%1" 的組態並未發生，因為沒有父變數。 錯誤碼：0x%2!8.8X!。|  
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
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|[收件者] 欄位的位址格式不正確。 可能遺漏 "\@" 符號或無效。|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|[寄件者] 欄位的位址格式不正確。 可能遺漏 "\@" 符號或無效。|  
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
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|警告：無法開啟全域共用記憶體來與效能 DLL 通訊；資料流程效能計數器無法使用。  若要解決問題，必須以管理員身分或在系統的主控台上執行此封裝。|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|檔案結尾有不完整的資料列。|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|在讀取標頭資料列時，已經到達資料檔案的結尾。 請確定標頭資料列分隔符號和要略過的標頭資料列數都正確。|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|無法從 OLE DB 提供者擷取資料行字碼頁資訊。  如果元件支援 "%1" 屬性，將使用該屬性的字碼頁。  如果目前的字串字碼頁值不正確，請變更屬性的值。  如果元件不支援屬性，將使用元件地區設定識別碼的字碼頁。|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|已經依指定方式排序資料，所以可以移除轉換。|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 參考的外部資料類型無法對應至資料流程工作資料類型。 將改用資料流程工作資料類型 DT_WSTR。|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|運算式 "%1" 永遠會導致資料截斷。 運算式包含靜態截斷 (固定值的截斷)。|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|在索引 %3!d!，識別碼為 %2!d! 的 輸入資料行 "%1" 未產生對應。 資料行的歷程識別碼為零。|  
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
  
|十六進位碼|十進位碼|符號名稱|Description|  
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
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|緩衝區管理員偵測到系統虛擬記憶體偏低，但無法空出任何緩衝區。 已考量 %1!d! 個緩衝區，但 %2!d! 個已鎖定 。 可能是因為未安裝足夠記憶體，造成管線可用的記憶體不足、其他處理序正在使用記憶體或鎖定太多緩衝區。|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|緩衝區管理員執行 %3!d! 位元組的記憶體配置呼叫失敗， 無法空出任何緩衝區來緩和記憶體不足的壓力。 已考量 %1!d! 個緩衝區，但 %2!d! 個已鎖定 。 可能是因為未安裝足夠記憶體，造成管線可用的記憶體不足、其他處理序正在使用記憶體或鎖定太多緩衝區。|  
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
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 已經執行下列作業：處理 %2!I64u! 個 資料列、發出 %3!I64u! 資料庫命令給參考資料庫並使用部分快取執行 %4!I64u! 個 查閱。|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 已經執行下列作業：處理 %2!I64u! 個 資料列、發出 %3!I64u! 個資料庫命令給參考資料庫、 使用部分快取執行 %4!I64u! 個查閱， 以及使用初始查閱中無相符項目的資料列快取執行 %5!I64u! 個查閱。|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 正在將快取寫入檔案 "%2"。|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 已將快取寫入檔案 "%2"。|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|OLE DB 目的地 "%1" 的插入認可大小上限屬性設定為 0。 這個屬性設定可能會導致執行中的封裝停止回應。 如需詳細資訊，請參閱 OLE DB 目的地編輯器 (連接管理員頁面) 的 F1 說明主題。|  
  
##  <a name="msgGeneral"></a> 一般和事件訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的符號名稱以 **DTS_MSG_** 當作開頭。  
  
|十六進位碼|十進位碼|符號名稱|Description|  
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
  
|十六進位碼|十進位碼|符號名稱|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|值為 NULL。|  
|0x40005|262149|DTS_S_TRUNCATED|已截斷字串值。 緩衝區收到對資料行而言太長的字串，緩衝區已截斷字串。|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|在運算式評估期間發生截斷。 截斷是在評估期間發生，可能包含中間步驟的任何點。|  
  
##  <a name="msgPipeline"></a> 資料流程元件錯誤訊息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的符號名稱是以 **DTSBC_E_** 當作開頭，其中 "BC" 指的是大多數 Microsoft 資料流程元件衍生來源的原生基底類別。  
  
|十六進位碼|十進位碼|符號名稱|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|輸出和錯誤輸出的總數 %1!lu! 不正確。 必須正好是 %2!lu!。|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|無法使用索引 %1!lu! 擷取輸出。|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|錯誤輸出數目 %1!lu! 不正確。 必須正好是 %2!lu!。|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|不正確的驗證狀態值 "%1!lu! " 包含不支援的資料類型。  必須是 DTSValidationStatus 列舉的其中一個值。|  
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
  
  
