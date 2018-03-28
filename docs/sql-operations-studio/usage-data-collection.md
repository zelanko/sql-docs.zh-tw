---
title: 啟用或停用使用量資料收集，並損毀報表的 SQL Operations Studio （預覽） |Microsoft 文件
description: 本文說明如何控制如果使用量及損毀報告資料收集並傳送給 Microsoft。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae620951028ba8e0e82f89c4251238c92bc614ca
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>啟用或停用的使用量資料收集[!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>如何停用遙測報告

[!INCLUDE[name-sos](../includes/name-sos-short.md)]收集使用量資料，並將它傳送給 Microsoft，以協助改善產品和服務。 若要深入了解，閱讀[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)。

如果您不想要使用狀況資料傳送給 Microsoft，您可以設定*telemetry.enableTelemetry*設*false*。

若要從所有遙測事件轉為無都回應[!INCLUDE[name-sos](../includes/name-sos-short.md)]，從**檔案** > **喜好設定** > **設定**，新增下列選項：

```json
    "telemetry.enableTelemetry": false
```

**重要通知**： 此選項需要重新啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]才會生效。 

## <a name="how-to-disable-crash-reporting"></a>如何停用當機報告

若要停用當機報告，從**檔案** > **喜好設定** > **設定**，新增下列選項：

```json
    "telemetry.enableCrashReporter": false
```

**重要通知**： 此選項需要重新啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]才會生效。

## <a name="additional-resources"></a>其他資源
- [工作區和使用者設定](settings.md)