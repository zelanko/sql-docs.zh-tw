---
title: Microsoft OLE DB Provider for Oracle |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60510302525562d9c3007a6ef57213fc261b4c60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926626"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 概觀
> [!IMPORTANT]
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用 Oracle OLE DB 提供者。

 Microsoft OLE DB Provider for Oracle 可讓 ADO 可以存取 Oracle 資料庫。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，將*提供者*引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```vb
MSDAORA
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性會傳回此字串以及。

 如果 Oracle 資料庫中執行聯結查詢與 keyset 或 dynamic 資料指標，便會發生錯誤。 Oracle 僅支援靜態唯讀資料指標。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 字串是由這些關鍵字所組成：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 OLE DB Provider for Oracle。|
|**資料來源**|指定伺服器的名稱。|
|**使用者識別碼**|指定使用者名稱。|
|**密碼**|指定使用者密碼。|

> [!NOTE]
>  如果您要連接到資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或是**Integrated Security = SSPI**而非使用者 ID 和密碼連接字串中的資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特有的連接參數
 提供者支援除了 ADO 所定義的數個提供者特有的連接參數。 因為 ADO 連接屬性，這些提供者特有的屬性可設透過[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合[連線](../../../ado/reference/ado-api/connection-object-ado.md)或是一部分**ConnectionString**.

 這些參數中的完整說明[OLE DB 程式設計人員參考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)。 [ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)提供這些參數名稱和對應的 OLE DB 屬性之間的交互參考。

|參數|描述|
|---------------|-----------------|
|**視窗控制代碼**|表示將提示您輸入其他資訊的視窗控制代碼。|
|**地區設定識別碼**|表示唯一 32 位元指定的數字 （例如，1033年） 的相關使用者的語言喜好設定。 這些喜好設定會指出如何格式化日期和時間，依字母順序排序項目，字串比較時，依此類推。|
|**OLE DB 服務**|表示位元遮罩，指定啟用或停用的 OLE DB 服務。|
|**提示**|指出是否要建立連接時提示使用者。|
|**擴充的屬性**|字串，包含提供者特定、 擴充連接資訊。 這個屬性僅適用於無法透過屬性機制中所述的提供者特有的連接資訊。|

## <a name="see-also"></a>另請參閱
 [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
