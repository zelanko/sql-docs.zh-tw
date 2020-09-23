---
title: SQL Server 主要執行個體設定屬性
titleSuffix: SQL Server big data clusters
description: SQL Server 主要執行個體之設定屬性的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60888246623796d9b4d17c498da47ab4b6557cf2
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790421"
---
# <a name="sql-server-master-instance-configuration-properties"></a>SQL Server 主要執行個體設定屬性

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

## <a name="properties"></a>屬性

您可以在部署階段，設定主要執行個體的下列 SQL Server 選項。

|屬性|選項|
| --- | --- |
|`[sqlagent]`|`enabled = { true | false }` |
|`[telemetry]`|`customerfeedback = { true | false }` |
|`[telemetry]`|`userRequestedLocalAuditDirectory = </path/file>`|
|`[licensing]`| `pid = { Enterprise | Developer }`|
|`[traceflag]`|` traceflag<#> = <####>`|

### <a name="examples"></a>範例

下列範例會啟用 SQL 代理程式、遙測、設定 Enterprise Edition 的 PID，並啟用追蹤旗標 1204：

```
[sqlagent]
enabled=true

[telemetry]
customerfeedback=true
userRequestedLocalAuditDirectory = /tmp/audit

[licensing]
pid = Enterprise

[traceflag]
traceflag0 = 1204
```

如需相關指示，請參閱[設定 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的主要執行個體](configure-sql-server-master-instance.md)。

## <a name="next-steps"></a>後續步驟

[設定 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的主要執行個體](configure-sql-server-master-instance.md)
