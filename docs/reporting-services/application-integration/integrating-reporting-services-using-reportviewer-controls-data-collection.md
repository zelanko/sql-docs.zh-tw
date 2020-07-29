---
title: ReportViewer 控制項 2016 中的資料收集
description: ReportViewer 會收集匿名使用方式資料以了解客戶如何使用產品，並專注於開發與客戶最相關的改善。
author: maggiesMSFT
ms.author: maggies
ms.custom: seo-lt-2019
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 06/03/2020
ms.openlocfilehash: 22f693824c244e02f313e488a067a0b732b2fa10
ms.sourcegitcommit: dc6ea6665cd2fb58a940c722e86299396b329fec
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84423396"
---
# <a name="integrate-reporting-services-using-reportviewer-controls---data-collection"></a>使用 ReportViewer 控制項整合 Reporting Services - 資料收集

控制項會收集匿名使用方式資料，以深入了解客戶如何利用產品。 使用方式資料可讓您專注於與客戶最相關之增強功能的未來開發。

[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)提供 Microsoft SQL Server 和報表檢視器的資料收集和使用方式作法說明。

## <a name="opting-out-of-data-collection"></a>退出資料收集

透過 ```EnableTelemetry``` 屬性，可以停用收集使用方式資料。

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

或者，在呈現控制項之前實際停用。
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另請參閱

[使用 WebForms 報表檢視器控制項](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[使用報表檢視器控制項整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



