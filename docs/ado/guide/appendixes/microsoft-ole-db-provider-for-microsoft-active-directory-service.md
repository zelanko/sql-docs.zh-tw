---
title: Microsoft OLE DB Provider for Microsoft Active Directory 服務 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 837f5fbcbb6c7730cdfcbe08e532a73c5faad06f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758324"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft OLE DB Provider for Microsoft Active Directory 服務
Active Directory 服務介面（ADSI）提供者可讓 ADO 透過 ADSI 連接到異類目錄服務。 這可讓 ADO 應用程式除了任何與 LDAP 相容的目錄服務和 Novell 目錄服務之外，也能夠唯讀存取 Microsoft Windows NT 4.0 和 Microsoft Windows 2000 目錄服務。 ADSI 本身是以提供者模型為基礎，因此，如果有新的提供者可存取另一個目錄，則 ADO 應用程式將能夠順暢地存取它。 ADSI 提供者是無限制執行緒且已啟用 Unicode。  
  
## <a name="connection-string-parameters"></a>連接字串參數  
 若要連接到這個提供者，請將[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性的**provider**引數設定為下列內容：  
  
```vb
ADSDSOObject  
```  
  
 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性也會傳回這個字串。  
  
## <a name="typical-connection-string"></a>一般連接字串  
 此提供者的一般連接字串如下所示：  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 此字串包含下列關鍵字。  
  
|關鍵字|描述|  
|-------------|-----------------|  
|**提供者**|指定 Active Directory 服務的 OLE DB 提供者。|  
|**使用者識別碼**|指定使用者名稱。 如果省略此關鍵字，則會使用目前的登入。|  
|**密碼**|指定使用者密碼。 如果省略此關鍵字，則為。 然後會使用目前的登入。|  
  
> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定**Trusted_Connection = yes**或**整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。  
  
## <a name="command-text"></a>命令文字  
 提供者會使用下列語法來辨識四部分的命令文字字串：  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|值|說明|  
|-----------|-----------------|  
|*路徑*|表示要從中開始搜尋的**ADsPath**物件（也就是搜尋的根）。|  
|*Filter*|以 RFC 1960 格式表示搜尋篩選準則。|  
|*屬性*|表示要傳回的屬性清單（以逗號分隔）。|  
|*範圍*|選擇性。 指定搜尋範圍的**字串**。 可以是下列其中一項：<br /><br /> -Base-僅搜尋基底物件（搜尋的根目錄）。<br />-OneLevel-僅搜尋一個層級。<br />-子樹-搜尋整個子樹。|  
  
 例如：  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 提供者也支援命令文字的 SQL SELECT。 例如：  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>備註  
 提供者不接受預存程序呼叫或簡單的資料表名稱（例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性一律會是**adCmdText**）。 如需更完整的命令文字元素描述，請參閱 Active Directory 服務介面檔。  
  
## <a name="recordset-behavior"></a>記錄集行為  
 下表列出使用此提供者開啟之[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上可用的功能。 只有靜態資料指標類型（**adOpenStatic**）可供使用。  
  
 如需提供者設定之**記錄集**行為的詳細資訊，請執行[支援](../../../ado/reference/ado-api/supports-method.md)方法，並列舉**記錄集**的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以判斷提供者特定的動態屬性是否存在。  
  
 **標準 ADO 記錄集屬性的可用性：**  
  
|屬性|可用性|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|讀取/寫入|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|讀取/寫入|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|唯讀|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|  
|[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)|讀取/寫入|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|讀取/寫入|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|一律**adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|一律**adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|一律**adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|讀取/寫入|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|讀取/寫入|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|無法使用|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|唯讀|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|讀取/寫入|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|唯讀|  
|[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|唯讀|  
|[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)|唯讀|  
  
 **標準 ADO 記錄集方法的可用性：**  
  
|方法|是否可用？|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|否|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|  
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|是|  
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|是|  
|[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|  
|[移動](../../../ado/reference/ado-api/move-method-ado.md)|是|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|是|  
|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|  
|[再次](../../../ado/reference/ado-api/requery-method.md)|是|  
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|是|  
|[支援](../../../ado/reference/ado-api/supports-method.md)|是|  
|[更新](../../../ado/reference/ado-api/update-method.md)|否|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|  
  
 如需有關 ADSI 和提供者細節的詳細資訊，請參閱 Active Directory 服務介面檔或造訪 ADSI 網頁。  
  
## <a name="see-also"></a>另請參閱  
 [CommandType 屬性（ADO）](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString 屬性（ADO）](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Provider 屬性（ADO）](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
