---
title: ReportViewer 控制項 2016 中的資料收集 | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 69cc665274d7463982cdfddd32d2b979e25a156e
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50028147"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>使用 ReportViewer 控制項整合 Reporting Services - 資料收集

控制項會收集匿名使用方式資料，以深入了解客戶如何利用產品。 使用方式資料可讓您專注於與客戶最相關之增強功能的未來開發。

[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)提供 Microsoft SQL Server 和報表檢視器的資料收集和使用方式作法說明。

## <a name="opting-out-of-data-collection"></a>退出資料收集

透過 ```EnableTelemetry``` 屬性，可以停用收集使用方式資料。

```
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

或者，在呈現控制項之前實際停用。
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另請參閱

[使用 WebForms 報表檢視器控制項](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[使用報表檢視器控制項整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



