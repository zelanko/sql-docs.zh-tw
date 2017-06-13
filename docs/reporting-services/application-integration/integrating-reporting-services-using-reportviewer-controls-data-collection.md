---
title: "ReportViewer 控制項 2016年中的資料收集 |Microsoft 文件"
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4e8b0226c27380bd2089acf8d2d6c8d7b27c7c5b
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>使用資料收集 ReportViewer 控制項整合 Reporting Services
根據預設，ReportViewer 控制項會收集匿名使用資訊以深入了解客戶如何建立 Microsoft 的順序使用的控制項。 藉由建立進一步了解客戶如何部署和使用檢視器控制項，未來開發可以著重改良功能，提供大部分的價值給客戶。

如需 Microsoft SQL Server 2016 版本及任何其他產品和服務中使用者資料收集與使用方式的說明，請參閱這份 [Microsoft 提供的隱私權聲明](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx)。

## <a name="opting-out-of-telemetry"></a>選擇退出遙測

遙測可以停用程式設計方式透過 「 EnableTelemetry"。 作法是藉由編輯.aspx 網頁，裝載控制項

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

或者，pragmatically 在控制項呈現這類如同裝載的網頁 Page_Load 呼叫之前。
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另請參閱

[使用 WebForms ReportViewer 控制項](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[使用 ReportViewer 控制項整合 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 




