---
title: 啟用或停用使用量資料收集，以及當機報告適用於 Azure 資料 Studio |Microsoft Docs
description: 本文說明如何控制是否收集使用量與損毀報告資料並傳送給 Microsoft。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b0a5adf802ab07e05f1041b1385044e2d580db32
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356479"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>啟用或停用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的使用量資料收集

## <a name="how-to-disable-telemetry-reporting"></a>如何停用遙測報告

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 收集使用量資料，並將它傳送給 Microsoft，以協助改善我們產品和服務。 若要進一步了解，請閱讀[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)。

如果您不想要使用狀況資料傳送給 Microsoft，您可以設定*telemetry.enableTelemetry*設定值為*false*。

若要從 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 將所有遙測事件設為無回應，請從**檔案**  >  **喜好設定**  >  **設定**，新增下列選項：

```json
    "telemetry.enableTelemetry": false
```

**重要須知**： 此選項需要重新啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]才會生效。 

## <a name="how-to-disable-crash-reporting"></a>如何停用當機報告

若要停用當機報告，從**檔案** > **喜好設定** > **設定**，新增下列選項：

```json
    "telemetry.enableCrashReporter": false
```

**重要須知**： 此選項需要重新啟動[!INCLUDE[name-sos](../includes/name-sos-short.md)]才會生效。

## <a name="additional-resources"></a>其他資源
- [工作區] 和 [使用者設定](settings.md)
