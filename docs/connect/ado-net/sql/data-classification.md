---
title: SqlClient 中的資料探索與分類
description: 描述如何檢查 SQL Server 資料庫是否支援資料分類，以及如何透過 SqlDataReader 物件存取資料分類資訊。
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 32c4968c4e734abf7bcb4addfde69bbdc5294d1c
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123864"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient 中的資料探索與分類

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[資料探索與分類](../../../relational-databases/security/sql-data-discovery-and-classification.md)是一組進階服務，用於探索、分類、標記和報告資料庫中的敏感性資料。 SqlClient 提供 API，可在基礎來源支援時公開唯讀資料探索和分類資訊。 這項資訊可透過 SqlDataReader 存取。

Microsoft.Data.SqlClient v2.1.0 引進了對資料分類 `Sensitivity Rank` 資訊的支援。 `Sensitivity Rank` 為識別碼，其以定義敏感度順位的一組預先定義值為基礎。 其他服務 (例如進階威脅防護) 可以使用此識別碼，根據其順位來偵測異常。 目前已在 Microsoft.Data.SqlClient.DataClassification 命名空間中提供下列資料分類 API：

```csharp
// New in Microsoft.Data.SqlClient v2.1.0
public enum SensitivityRank
{
    NOT_DEFINED = -1,
    NONE = 0,
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30,
    CRITICAL = 40
}

public sealed class SensitivityClassification
{
  // Returns the sensitivity rank for the query associated with the active 'SqlDataReader'.
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the labels collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<Label> Labels;

  // Returns the information types collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<InformationType> InformationTypes;

  // Returns the column sensitivity for this 'SensitivityClassification' Object
  public ReadOnlyCollection<ColumnSensitivity> ColumnSensitivities;
}

public sealed class SensitivityProperty
{
  // Returns the sensitivity rank for this 'SensitivityProperty' Object
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the label for this 'SensitivityProperty' Object
  public Label Label;

  // Returns the information type for this 'SensitivityProperty' Object
  public InformationType InformationType;
}

public sealed class Label
{
  // Gets the name for this 'Label' object
  public string Name;

  // Gets the ID for this 'Label' object
  public string Id;
}

public sealed class InformationType
{
  // Gets the name for this 'InformationType' object
  public string Name;

  // Gets the ID for this 'InformationType' object
  public string Id;
}

public sealed class ColumnSensitivity
{
  // Returns the list of sensitivity properties as received from Server for this 'ColumnSensitivity' information      
  public ReadOnlyCollection<SensitivityProperty> SensitivityProperties;
}
```

> [!NOTE]
> 只有在 SQL Server 支援具有順位的資料分類時，Microsoft.Data.SqlClient 才會讀取 `Sensitivity Rank` 資訊。 如果伺服器使用不具順位的舊版資料分類，則查詢的順位值為「未定義」。

此範例應用程式會示範如何存取 SqlDataReader 的資料分類屬性。

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]


**另請參閱**  

 - [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)
 - [sys.sensitivity_classifications (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)
 - [ADD SENSITIVITY CLASSIFICATION](../../../t-sql/statements/add-sensitivity-classification-transact-sql.md)