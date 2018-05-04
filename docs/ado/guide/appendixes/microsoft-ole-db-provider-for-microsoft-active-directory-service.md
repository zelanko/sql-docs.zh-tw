---
title: Microsoft OLE DB Provider for Microsoft Active Directory 服務 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88e853530b2904a22fa233597bec9d0ac2c9152a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft OLE DB Provider for Microsoft Active Directory 服務
Active Directory 服務介面 (ADSI) 提供者可讓 ADO 連接到透過 ADSI 異質目錄服務。 這可讓 ADO 應用程式對唯讀存取 Microsoft Windows NT 4.0 和 Microsoft Windows 2000 目錄服務，除了任何 LDAP 相容目錄服務和 Novell 目錄服務。 ADSI 本身為基礎的提供者模型，使新的提供者提供存取至另一個目錄時，ADO 應用程式將能夠順暢地存取它。 ADSI 提供者是無限制執行緒，啟用 Unicode。  
  
## <a name="connection-string-parameters"></a>連接字串參數  
 若要連接到此提供者，設定**提供者**引數的[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性如下：  
  
```  
ADSDSOObject  
```  
  
 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性會傳回這個字串以及。  
  
## <a name="typical-connection-string"></a>一般連接字串  
 此提供者的一般連接字串如下所示：  
  
```  
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 下列關鍵字所組成的字串。  
  
|關鍵字|Description|  
|-------------|-----------------|  
|**提供者**|指定 Active Directory 服務的 OLE DB 提供者。|  
|**使用者識別碼**|指定使用者名稱。 如果省略此關鍵字，則會使用目前登入。|  
|**密碼**|指定的使用者密碼。 如果省略此關鍵字。 則會使用目前登入。|  
  
> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。  
  
## <a name="command-text"></a>命令文字  
 下列語法中的提供者所能辨識的四部分的命令文字字串：  
  
```  
"Root; Filter; Attributes[; Scope]"  
```  
  
|Value|Description|  
|-----------|-----------------|  
|*Root*|指出**ADsPath**要開始搜尋 （也就是說，搜尋的根） 的物件。|  
|*篩選*|表示搜尋篩選器以 RFC 1960 格式。|  
|*屬性*|表示要傳回之屬性的逗號分隔清單。|  
|*範圍*|選擇性。 A**字串**，指定搜尋範圍。 可以是下列其中一項：<br /><br /> 基底 — 搜尋才基底物件 （搜尋的根）。<br />-OneLevel — 搜尋只有一個層級。<br />-樹狀子目錄，搜尋整個樹狀子目錄。|  
  
 例如：  
  
```  
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 提供者也支援 SQL SELECT 命令文字。 例如：  
  
```  
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>備註  
 提供者不接受預存程序呼叫或簡單的資料表名稱 (例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性一定會是**adCmdText**)。 請參閱 Active Directory 服務介面文件如需更完整的命令文字項目說明。  
  
## <a name="recordset-behavior"></a>資料錄集行為  
 下表列出可以使用的功能[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)開啟使用此提供者的物件。 靜態資料指標類型 (**adOpenStatic**) 使用。  
  
 如需有關**資料錄集**您的提供者組態，執行行為[支援](../../../ado/reference/ado-api/supports-method.md)方法，並列舉[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**資料錄集**來判斷是否存在特定提供者的動態屬性。  
  
 **標準的 ADO 資料錄集屬性的可用性：**  
  
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
|[篩選](../../../ado/reference/ado-api/filter-property.md)|讀取/寫入|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|讀取/寫入|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|無法使用|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|唯讀|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|讀取/寫入|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|唯讀|  
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|唯讀|  
|[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)|唯讀|  
  
 **標準的 ADO 資料錄集方法的可用性：**  
  
|方法|可用？|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|  
|[[取消]](../../../ado/reference/ado-api/cancel-method-ado.md)|否|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|  
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|是|  
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|是|  
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|  
|[[移動]](../../../ado/reference/ado-api/move-method-ado.md)|是|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|是|  
|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|  
|[重新查詢](../../../ado/reference/ado-api/requery-method.md)|是|  
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|是|  
|[支援](../../../ado/reference/ado-api/supports-method.md)|是|  
|[Update](../../../ado/reference/ado-api/update-method.md)|否|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|  
  
 如需 ADSI 與提供者的細節的詳細資訊，請參閱 Active Directory 服務介面文件或瀏覽 ADSI 網頁。  
  
## <a name="see-also"></a>另請參閱  
 [CommandType 屬性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
