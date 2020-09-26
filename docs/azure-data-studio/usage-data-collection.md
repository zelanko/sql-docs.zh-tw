---
title: 啟用或停用使用方式資料收集和當機報告
description: 本文說明如何控制使用方式和當機報告資料的收集，以及是否傳送給 Microsoft。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 5ef44a7e2981d98c749e25692e667ae71b42843d
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91363885"
---
# <a name="enable-or-disable-usage-data-collection-for-azure-data-studio"></a>啟用或停用 Azure Data Studio 的使用狀況資料收集

## <a name="how-to-disable-telemetry-reporting"></a>如何停用遙測報告

Azure Data Studio 會收集使用狀況資料並傳送給 Microsoft，以協助改善我們的產品與服務。 若要深入了解，請閱讀[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)。

如果您不想要將使用方式資料傳送給 Microsoft，您可以將 *telemetry.enableTelemetry* 設定設為 *false*。

若要將來自 Azure Data Studio 的所有遙測事件設為無回應，請從 [檔案] > [喜好設定] > [設定] 中，新增下列選項：

```json
    "telemetry.enableTelemetry": false
```

**重要須知**：此選項需要重新啟動 Azure Data Studio 才會生效。 

## <a name="how-to-disable-crash-reporting"></a>如何停用當機報告

若要停用當機報告，請從 [檔案] > [喜好設定] > [設定]，新增下列選項：

```json
    "telemetry.enableCrashReporter": false
```

**重要須知**：此選項需要重新啟動 Azure Data Studio 才會生效。

## <a name="additional-resources"></a>其他資源
- [工作區與使用者設定](settings.md)
