---
description: Microsoft OLE DB Provider for Microsoft Active Directory Service
title: Microsoft OLE DB Provider for Microsoft Active Directory Service |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: rothja
ms.author: jroth
ms.openlocfilehash: 08d945b101ac91300793920e3e01ea0a9619b372
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991049"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft OLE DB Provider for Microsoft Active Directory Service
Active Directory 服務介面 (ADSI) 提供者，可讓 ADO 透過 ADSI 連接到異類目錄服務。 除了任何符合 LDAP 規範的目錄服務和 Novell 目錄服務之外，這也可讓 ADO 應用程式唯讀存取 Microsoft Windows NT 4.0 和 Microsoft Windows 2000 目錄服務。 ADSI 本身是以提供者模型為基礎，因此，如果有新的提供者提供另一個目錄的存取權，則 ADO 應用程式將能夠順暢地進行存取。 ADSI 提供者已啟用無限制執行緒和 Unicode。  
  
## <a name="connection-string-parameters"></a>連接字串參數  
 若要連接到這個提供者，請將[ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)屬性的**提供者**引數設定如下：  
  
```vb
ADSDSOObject  
```  
  
 讀取 [Provider](../../reference/ado-api/provider-property-ado.md) 屬性也會傳回這個字串。  
  
## <a name="typical-connection-string"></a>一般連接字串  
 此提供者的一般連接字串如下所示：  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 字串包含下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|**提供者**|指定 Active Directory 服務的 OLE DB 提供者。|  
|**使用者識別碼**|指定使用者名稱。 如果省略此關鍵字，則會使用目前的登入。|  
|**密碼**|指定使用者密碼。 如果省略此關鍵字，則為。 然後會使用目前的登入。|  
  
> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定 **Trusted_Connection = yes** 或 **整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。  
  
## <a name="command-text"></a>命令文字  
 提供者可以使用下列語法辨識四部分的命令文字字串：  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|值|描述|  
|-----------|-----------------|  
|*根*|指出要從中開始搜尋的 **ADsPath** 物件 (也就是搜尋) 的根目錄。|  
|*Filter*|表示 RFC 1960 格式的搜尋篩選準則。|  
|*屬性*|表示要傳回的屬性清單（以逗號分隔）。|  
|*範圍*|選擇性。 指定搜尋範圍的 **字串** 。 可以是下列其中一項：<br /><br /> -Base-只搜尋基底物件 (搜尋) 的根目錄。<br />-OneLevel-只搜尋一個層級。<br />-子樹-搜尋整個子樹。|  
  
 例如：  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 提供者也支援適用于命令文字的 SQL SELECT。 例如：  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>備註  
 提供者不接受預存程序呼叫或簡單的資料表名稱 (例如， [CommandType](../../reference/ado-api/commandtype-property-ado.md) 屬性一律會 **adCmdText**) 。 如需更詳盡的命令文字元素說明，請參閱 Active Directory 服務介面檔。  
  
## <a name="recordset-behavior"></a>記錄集行為  
 下表列出使用此提供者開啟之 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件上的可用功能。 只有靜態資料指標類型 (**adOpenStatic**) 可用。  
  
 如需提供者設定的**記錄集**行為詳細資訊，請執行[支援](../../reference/ado-api/supports-method.md)的方法，並列舉**記錄集**的[屬性](../../reference/ado-api/properties-collection-ado.md)集合，以判斷是否存在提供者特定的動態屬性。  
  
 **標準 ADO 記錄集屬性的可用性：**  
  
|屬性|可用性|  
|--------------|------------------|  
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|讀取/寫入|  
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|讀取/寫入|  
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|唯讀|  
|[轉爐](../../reference/ado-api/bof-eof-properties-ado.md)|唯讀|  
|[書籤](../../reference/ado-api/bookmark-property-ado.md)|讀取/寫入|  
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|讀取/寫入|  
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|一律 **adUseServer**|  
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|一律 **adOpenStatic**|  
|[EditMode](../../reference/ado-api/editmode-property.md)|一律 **adEditNone**|  
|[Eof](../../reference/ado-api/bof-eof-properties-ado.md)|唯讀|  
|[Filter](../../reference/ado-api/filter-property.md)|讀取/寫入|  
|[LockType](../../reference/ado-api/locktype-property-ado.md)|讀取/寫入|  
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|無法使用|  
|[MaxRecords](../../reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|  
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|唯讀|  
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|讀取/寫入|  
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|唯讀|  
|[Source](../../reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|  
|[State](../../reference/ado-api/state-property-ado.md)|唯讀|  
|[狀態](../../reference/ado-api/status-property-ado-recordset.md)|唯讀|  
  
 **標準 ADO 記錄集方法的可用性：**  
  
|方法|是否可用？|  
|------------|----------------|  
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|否|  
|[取消](../../reference/ado-api/cancel-method-ado.md)|否|  
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|否|  
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|否|  
|[複製](../../reference/ado-api/clone-method-ado.md)|是|  
|[關閉](../../reference/ado-api/close-method-ado.md)|是|  
|[刪除](../../reference/ado-api/delete-method-ado-recordset.md)|否|  
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|是|  
|[移動](../../reference/ado-api/move-method-ado.md)|是|  
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MoveLast](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|是|  
|[開啟](../../reference/ado-api/open-method-ado-recordset.md)|是|  
|[重新](../../reference/ado-api/requery-method.md)|是|  
|[重新同步處理](../../reference/ado-api/resync-method.md)|是|  
|[支援](../../reference/ado-api/supports-method.md)|是|  
|[更新](../../reference/ado-api/update-method.md)|否|  
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|否|  
  
 如需 ADSI 和提供者細節的詳細資訊，請參閱 Active Directory 服務介面檔或流覽 ADSI 網頁。  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 CommandType 屬性 ](../../reference/ado-api/commandtype-property-ado.md)   
 [ (ADO) 的 ConnectionString 屬性 ](../../reference/ado-api/connectionstring-property-ado.md)   
 [ (ADO) 的屬性集合 ](../../reference/ado-api/properties-collection-ado.md)   
 [ (ADO) 的提供者屬性 ](../../reference/ado-api/provider-property-ado.md)   
 [ (ADO) 的記錄集物件 ](../../reference/ado-api/recordset-object-ado.md)   
 [Supports 方法](../../reference/ado-api/supports-method.md)