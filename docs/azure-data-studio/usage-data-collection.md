---
title: 啟用或停用使用方式資料收集和當機報告
titleSuffix: Azure Data Studio
description: 本文說明如何控制使用方式和當機報告資料的收集，以及是否傳送給 Microsoft。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 416c22aa04e289e7959e41924344666e4329ecf1
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957002"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>啟用或停用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的使用方式資料收集

## <a name="how-to-disable-telemetry-reporting"></a>如何停用遙測報告

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會收集使用方式資料並傳送給 Microsoft，協助改善我們的產品和服務。 若要深入了解，請閱讀[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)。

如果您不想要將使用方式資料傳送給 Microsoft，您可以將 *telemetry.enableTelemetry* 設定設為 *false*。

若要將來自 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的所有遙測事件設為無回應，請從 [檔案]   > [喜好設定]   > [設定]  ，新增下列選項：

```json
    "telemetry.enableTelemetry": false
```

**重要須知**：此選項需要重新啟動 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 才會生效。 

## <a name="how-to-disable-crash-reporting"></a>如何停用當機報告

若要停用當機報告，請從 [檔案]   > [喜好設定]   > [設定]  ，新增下列選項：

```json
    "telemetry.enableCrashReporter": false
```

**重要須知**：此選項需要重新啟動 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 才會生效。

## <a name="additional-resources"></a>其他資源
- [工作區與使用者設定](settings.md)
