---
title: "Microsoft OLE DB 的遠端服務提供者 （ADO 服務提供者） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cbc0d0060a58d1e73fe2df94c598a1fa054abd15
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB 的遠端服務提供者概觀
Microsoft OLE DB 遠端服務提供者可讓用戶端電腦上的本機使用者叫用遠端電腦上的資料提供者。 如果您在遠端電腦上的本機使用者一樣，請指定遠端電腦的資料提供者參數。 然後指定遠端服務提供者用來存取遠端電腦的參數。 然後，您可以如同是本機使用者存取遠端電腦。

> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。

## <a name="provider-keyword"></a>提供者關鍵字
 要叫用 OLE DB 遠端服務提供者，指定連接字串中的下列關鍵字和值。 （請注意 提供者名稱的空白空間）。

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>其他關鍵字
 叫用此服務提供者時，下列的其他關鍵字都有關。

|關鍵字|描述|
|-------------|-----------------|
|**資料來源**|指定遠端資料來源的名稱。 它會進行處理傳遞給 OLE DB 遠端服務提供者。<br /><br /> 此關鍵字相當於[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的[連接](../../../ado/reference/rds-api/connect-property-rds.md)屬性。|

## <a name="dynamic-properties"></a>動態屬性
 叫用此服務提供者時，已加入下列的動態屬性[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。

|動態屬性名稱|描述|
|---------------------------|-----------------|
|**DFMode**|指出 DataFactory 模式。 字串，指定所需的版本[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)伺服器上的物件。 設定此屬性之前開啟連接要求的特定版本**DataFactory**。 如果無法使用要求的版本，將會嘗試使用前一個版本。 如果沒有先前的版本，則會發生錯誤。 如果**DFMode**小於可用的版本中，會發生錯誤。 這個屬性是唯讀之後進行連線。<br /><br /> 可以是下列有效的字串值的其中一個：<br /><br /> -「 25"，版本 2.5 （預設值）<br />-"21"— 2.1 版<br />-"20"-2.0 版<br />-"15"-1.5 版|
|**命令屬性**|表示將會加入至 MS 遠端提供者傳送到伺服器的命令 （資料列集） 屬性的字串值。 這個字串的預設值為 vt_empty。|
|**目前 DFMode**|指出實際的版本號碼的**DataFactory**在伺服器上。 檢查這個屬性，請參閱版本是否要求中**DFMode**屬性已被接受。<br /><br /> 可以是下列有效的長整數值的其中一個：<br /><br /> -25-版本 2.5 （預設值）<br />-21-版本 2.1<br />-20-2.0 版<br />-15-1.5 版<br /><br /> 新增 「 DFMode = 20; 」 到您的連接字串時使用**MSRemote**更新資料時，提供者可以改善您的伺服器效能。 使用此設定， **RDSServer.DataFactory**伺服器上的物件會使用大量的資源模式。 不過，下列功能不適用於這項設定：<br /><br /> -使用參數化的查詢。<br />-取得參數或資料行的資訊，然後再呼叫**Execute**方法。<br />-設定**Transact 更新**至**True**。<br />-取得資料列狀態。<br />-呼叫**重新同步處理**方法。<br />重新整理 （明確或自動） 透過**重新同步處理更新**屬性。<br />-設定**命令**或**資料錄集**屬性。<br />-使用**adCmdTableDirect**。|
|**處理常式**|表示延伸功能的伺服器端自訂程式 （或處理常式） 的名稱[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，以及任何處理常式所使用的參數*，*以逗號分隔 （分隔","). A**字串**值。|
|**網際網路逾時**|表示最大傳入及傳出伺服器要求等待的毫秒數。 （預設值為 5 分鐘）。|
|**遠端提供者**|表示要在遠端伺服器上使用的資料提供者的名稱。|
|**遠端伺服器**|指出此連接所使用的伺服器名稱和通訊通訊協定。 這個屬性就相當於[.RDSDataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件[伺服器](../../../ado/reference/rds-api/server-property-rds.md)屬性。|
|**Transact 更新**|當設定為**True**，這個值表示當[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)執行的伺服器上，它將會完成在交易內。 此布林值的動態屬性的預設值是**False**。|

 您也可以藉由指定其名稱為連接字串中的關鍵字設定可寫入的動態屬性。 例如，設定**Internet 逾時**為五秒，藉由指定的動態屬性：

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 您也可能會設定或擷取動態屬性，藉由指定其名稱為的索引**屬性**屬性。 下列範例示範如何取得和目前的值列印**Internet 逾時**動態屬性，並將其設定新的值：

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>備註
 在 ADO 2.0 中，OLE DB 遠端服務提供者只可指定之*ActiveConnection*參數[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件**開啟**方法。 從 ADO 2.1 開始，提供者也可以指定在*ConnectionString*參數[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件**開啟**方法。

 相當於**.RDSDataControl**物件[SQL](../../../ado/reference/rds-api/sql-property.md)便無法使用屬性。 [資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件**開啟**方法*來源*改為使用引數。

 **請注意**"...; 指定遠端提供者 = MS 遠端;...」 會建立四個層案例。 案例三個層級尚未經過測試，並不需要。

## <a name="example"></a>範例
 這個範例會在執行查詢**作者**資料表**Pubs**名為伺服器上的資料庫*您的伺服器*。 中所提供的遠端資料來源和遠端伺服器名稱[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件和 SQL 查詢中指定[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 A**資料錄集**傳回、 編輯及用來更新資料來源物件。

```
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=http://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>請參閱
 [OLE DB 的遠端服務提供者的概觀](http://msdn.microsoft.com/en-us/4083b72f-68c4-4252-b366-abb70db5ca2b)
