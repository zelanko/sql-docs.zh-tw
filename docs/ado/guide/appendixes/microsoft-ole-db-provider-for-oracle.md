---
title: "Microsoft OLE DB Provider for Oracle |Microsoft 文件"
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
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: eb8cf771b758dc81bb80e38bc709c611d8125921
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 概觀
> [!IMPORTANT]
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用 Oracle 的 OLE DB 提供者。

 Microsoft OLE DB Provider for Oracle 可讓 ADO 存取 Oracle 資料庫。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，設定*提供者*引數的[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
MSDAORA
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性會傳回這個字串以及。

 如果 Oracle 資料庫中執行的聯結查詢 keyset 或 dynamic 資料指標，則會發生錯誤。 Oracle 僅支援靜態的唯讀資料指標。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 字串，包含這些關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 OLE DB Provider for Oracle。|
|**資料來源**|指定伺服器的名稱。|
|**使用者識別碼**|指定使用者名稱。|
|**密碼**|指定的使用者密碼。|

> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特有的連接參數
 提供者支援數個提供者特有的連接參數，除了由 ADO 所定義。 可以透過設定 ADO 連接屬性中，使用這些提供者特定屬性為[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)或做為一部分**ConnectionString**.

 這些參數是以完整描述[OLE DB 程式設計人員參考](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)。 [ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)提供這些參數名稱和對應的 OLE DB 屬性之間的交互參考。

|參數|描述|
|---------------|-----------------|
|**視窗控制代碼**|表示要用於提示您輸入其他資訊的視窗控制代碼。|
|**地區設定識別碼**|表示唯一 32 位元數字 （例如，1033年），指定與使用者的語言喜好設定。 這些喜好設定指出如何格式化日期和時間，依字母順序排序項目，字串比較時，依此類推。|
|**OLE DB 服務**|表示位元遮罩，指定啟用或停用 OLE DB 服務。|
|**提示**|指出是否要建立連接時提示使用者。|
|**擴充的屬性**|字串，包含提供者特定、 擴充連接資訊。 這個屬性只用於無法透過屬性機制中所述的提供者特定連接資訊。|

## <a name="see-also"></a>請參閱
 [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
