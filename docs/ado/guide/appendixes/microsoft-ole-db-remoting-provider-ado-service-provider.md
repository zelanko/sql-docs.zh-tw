---
description: 'Microsoft OLE DB (ADO 服務提供者的遠端處理提供者) '
title: Microsoft OLE DB 遠端處理提供者 (ADO 服務提供者) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e8520dc35b7a6d913736637cabaf34a2bd60651
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806533"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB 遠端處理提供者總覽
Microsoft OLE DB 遠端處理提供者可讓用戶端電腦上的本機使用者叫用遠端電腦上的資料提供者。 如您是遠端電腦上的本機使用者，指定遠端電腦的資料提供者參數。 然後指定遠端處理提供者用來存取遠端電腦的參數。 然後您就可以像本機使用者一樣存取遠端電腦。

> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至  [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。

## <a name="provider-keyword"></a>Provider 關鍵字
 若要叫用 OLE DB 遠端處理提供者，請在連接字串中指定下列關鍵字和值。  (記下提供者名稱中的空白空間。 ) 

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>其他關鍵字
 叫用此服務提供者時，會有下列其他關鍵字相關。

|關鍵字|描述|
|-------------|-----------------|
|**資料來源**|指定遠端資料源的名稱。 它會傳遞至 OLE DB 的遠端處理提供者進行處理。<br /><br /> 這個關鍵字相當於 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件的 [Connect](../../reference/rds-api/connect-property-rds.md) 屬性。|

## <a name="dynamic-properties"></a>動態屬性
 叫用此服務提供者時，會將下列動態屬性加入至 [連接](../../reference/ado-api/connection-object-ado.md)物件的 [屬性](../../reference/ado-api/properties-collection-ado.md) 集合。

|動態屬性名稱|描述|
|---------------------------|-----------------|
|**DFMode**|表示 DataFactory 模式。 字串，指定伺服器上所需的 [DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 物件版本。 請先設定這個屬性，然後再開啟連接來要求特定版本的 **DataFactory**。 如果要求的版本無法使用，則會嘗試使用先前的版本。 如果沒有之前的版本，將會發生錯誤。 如果 **DFMode** 小於可用的版本，就會發生錯誤。 連接完成後，這個屬性是唯讀的。<br /><br /> 可以是下列其中一個有效的字串值：<br /><br /> -"25"-版本 2.5 (預設) <br />-"21"-版本2。1<br />-"20"-版本2。0<br />-"15"-版本1。5|
|**命令屬性**|指出將新增至命令 (資料列集之字串的值，) 由 MS 遠端提供者傳送到伺服器的屬性。 這個字串的預設值是 vt_empty。|
|**目前的 DFMode**|表示伺服器上 **DataFactory** 的實際版本號碼。 檢查這個屬性，以查看是否接受 **DFMode** 屬性所要求的版本。<br /><br /> 可以是下列其中一個有效的長整數值：<br /><br /> -25-2.5 版 (預設) <br />-21-版本2。1<br />-20-版本2。0<br />-15-版本1。5<br /><br /> 使用 **MSRemote** 提供者時，將 "DFMode = 20;" 新增至連接字串，可以在更新資料時提升伺服器的效能。 使用此設定時，伺服器上的 **RDSServer DataFactory** 物件會使用較不需要大量資源的模式。 不過，此設定無法使用下列功能：<br /><br /> -使用參數化查詢。<br />-在呼叫 **Execute** 方法之前取得參數或資料行資訊。<br />-將 **交易更新** 設定為 **True**。<br />-正在取得資料列狀態。<br />-呼叫 **Resync** 方法。<br />-透過 **Update Resync** 屬性明確或自動重新整理 () 。<br />-設定 **命令** 或 **記錄集** 屬性。<br />-使用 **adCmdTableDirect**。|
|**處理常式**|指出伺服器端自訂程式的名稱 (或處理常式) 擴充 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)的功能，以及處理常式所使用的任何參數，全部以逗號分隔 ( "，" ) 。 **字串**值。|
|**網際網路超時**|指出等候傳送至伺服器之要求的最大毫秒數。  (預設值為5分鐘。 ) |
|**遠端提供者**|指出要在遠端伺服器上使用的資料提供者名稱。|
|**遠端伺服器**|指出此連接所要使用的伺服器名稱和通訊協定。 這個屬性就相當於 [RDS。DataContro](../../reference/rds-api/datacontrol-object-rds.md) 物件 [伺服器](../../reference/rds-api/server-property-rds.md) 屬性。|
|**交易更新**|當設定為 **True**時，這個值會指出當在伺服器上執行 [UpdateBatch](../../reference/ado-api/updatebatch-method.md) 時，它會在交易內完成。 此布林值動態屬性的預設值為 **False**。|

 您也可以藉由在連接字串中將其名稱指定為關鍵字，來設定可寫入動態屬性。 例如，藉由指定下列各項，將 [ **網際網路超時** 動態] 屬性設定為五秒：

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 您也可以藉由將動態屬性的名稱指定為 **Properties** 屬性的索引，來設定或抓取動態屬性。 下列範例顯示如何取得和列印 **Internet Timeout** 動態屬性的目前值，然後設定新的值：

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>備註
 在 ADO 2.0 中，OLE DB 的遠端處理提供者只能在[Recordset](../../reference/ado-api/recordset-object-ado.md)物件**Open**方法的*ActiveConnection*參數中指定。 從 ADO 2.1 開始，也可以在[Connection](../../reference/ado-api/connection-object-ado.md) object **Open**方法的*ConnectionString*參數中指定提供者。

 RDS 的對等專案 **。** 無法使用 DataControl 物件 [SQL](../../reference/rds-api/sql-property.md) 屬性。 改為使用 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件 **Open** method *Source* 引數。

 **注意** 指定 "...;Remote Provider = MS Remote; ... "會建立四層案例。 非三個階層的案例尚未經過測試，因此不需要。

## <a name="example"></a>範例
 這個範例會在名為 *>yourserver.database.windows.net*的伺服器上，對**Pubs**資料庫的**作者**資料表執行查詢。 遠端資料源和遠端伺服器的名稱是在[Connection](../../reference/ado-api/connection-object-ado.md)物件的[open](../../reference/ado-api/open-method-ado-connection.md)方法中提供，而 SQL 查詢則是在[記錄集](../../reference/ado-api/recordset-object-ado.md)物件的[open](../../reference/ado-api/open-method-ado-recordset.md)方法中指定。 會傳回、編輯 **記錄集** 物件，並使用它來更新資料來源。

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>另請參閱
 [OLE DB 遠端處理提供者總覽](/previous-versions/windows/desktop/ms713673(v=vs.85))