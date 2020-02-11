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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926626"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 總覽
> [!IMPORTANT]
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 的 OLE DB 提供者。

 Microsoft OLE DB Provider for Oracle 可讓 ADO 存取 Oracle 資料庫。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性的*provider*引數設定為：

```vb
MSDAORA
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性也會傳回這個字串。

 如果在 Oracle 資料庫中執行具有索引鍵集或動態資料指標的聯結查詢，就會發生錯誤。 Oracle 只支援靜態唯讀資料指標。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 Oracle 的 OLE DB 提供者。|
|**資料來源**|指定伺服器的名稱。|
|**使用者識別碼**|指定使用者名稱。|
|**密碼**|指定使用者密碼。|

> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定**Trusted_Connection = yes**或**整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特定的連接參數
 除了 ADO 所定義的連接參數之外，提供者也支援數個提供者特定的連線參數。 如同 ADO 連接屬性，這些提供者特有的屬性可以透過[連接](../../../ado/reference/ado-api/connection-object-ado.md)的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合或**ConnectionString**的一部分來設定。

 這些參數會在 OLE DB 程式設計[人員參考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)中完整描述。 [ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)會提供這些參數名稱與對應 OLE DB 屬性之間的交互參考。

|參數|描述|
|---------------|-----------------|
|**視窗控制碼**|表示用來提示提供其他資訊的視窗控制碼。|
|**地區設定識別碼**|表示唯一32位數位（例如1033），指定與使用者語言相關的喜好設定。 這些喜好設定會指出日期和時間的格式化方式、專案會依字母順序排序、比較字串等等。|
|**OLE DB 服務**|表示指定要啟用或停用 OLE DB 服務的位元遮罩。|
|**及時**|指出是否要在建立連接時提示使用者。|
|**擴充屬性**|字串，包含提供者特定的延伸連接資訊。 此屬性僅適用于無法透過屬性機制描述的提供者特定連接資訊。|

## <a name="see-also"></a>另請參閱
 [ConnectionString 屬性（ado）](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供者屬性（Ado）](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset 物件（ado）](../../../ado/reference/ado-api/recordset-object-ado.md)
