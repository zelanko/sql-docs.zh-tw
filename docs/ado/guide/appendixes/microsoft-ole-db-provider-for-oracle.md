---
description: Microsoft OLE DB Provider for Oracle 總覽
title: Microsoft OLE DB Provider for Oracle |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: rothja
ms.author: jroth
ms.openlocfilehash: d8da5e3d5de1ac0ee3f3dfa1b0f989679af3cd1d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991009"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 總覽
> [!IMPORTANT]
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 的 OLE DB 提供者。

 Microsoft OLE DB Provider for Oracle 允許 ADO 存取 Oracle 資料庫。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)屬性的*提供者*引數設定為：

```vb
MSDAORA
```

 讀取 [Provider](../../reference/ado-api/provider-property-ado.md) 屬性也會傳回這個字串。

 如果在 Oracle 資料庫中執行含有索引鍵集或動態資料指標的聯結查詢，就會發生錯誤。 Oracle 僅支援靜態的唯讀資料指標。

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
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定 **Trusted_Connection = yes** 或 **整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

## <a name="provider-specific-connection-parameters"></a>提供者特定的連接參數
 除了 ADO 定義的連接參數之外，提供者還支援數個提供者特定的連接參數。 如同 ADO 連接屬性，可以透過[連接](../../reference/ado-api/connection-object-ado.md)的[Properties](../../reference/ado-api/properties-collection-ado.md)集合或**ConnectionString**的一部分設定這些提供者特有的屬性。

 這些參數會在 OLE DB 程式設計 [人員參考](/previous-versions/windows/desktop/ms713643(v=vs.85))中完整說明。 [ADO 動態屬性索引](../../reference/ado-api/ado-dynamic-property-index.md)提供這些參數名稱和對應 OLE DB 屬性之間的交互參考。

|參數|描述|
|---------------|-----------------|
|**視窗控制代碼**|指出用來提示其他資訊的視窗控制碼。|
|**地區設定識別碼**|表示唯一的32位數位 (例如 1033) ，可指定與使用者語言相關的喜好設定。 這些喜好設定會指出日期和時間的格式化方式、依字母順序排序專案、比較字串等等。|
|**OLE DB 服務**|表示指定要啟用或停用 OLE DB 服務的位元遮罩。|
|**提示**|指出是否要在建立連接時提示使用者。|
|**擴充屬性**|字串，包含提供者特定的擴充連接資訊。 這個屬性只能用於無法透過屬性機制描述的提供者特定連接資訊。|

## <a name="see-also"></a>另請參閱
 [ConnectionString 屬性 (ado) ](../../reference/ado-api/connectionstring-property-ado.md) [Provider 屬性 (ado) ](../../reference/ado-api/provider-property-ado.md) [記錄集物件 (ado) ](../../reference/ado-api/recordset-object-ado.md)