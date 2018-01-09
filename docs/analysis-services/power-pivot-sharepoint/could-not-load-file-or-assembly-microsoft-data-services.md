---
title: "無法載入檔案或組件的 Microsoft Data Services |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0daa7111e93a81c367fda433cc7b530a4c90e8f4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>無法載入檔案或組件的 Microsoft Data Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在 SharePoint 2010 環境中具有[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]for SharePoint，如果您嘗試匯出資料摘要而且系統遺漏必要的 Microsoft ADO.NET Data Services 版本，會發生此錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|找不到 ADO.NET Data Services 3.5 SP1。|  
|訊息文字|無法載入檔案或組件 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' 或是它的其中一個相依性。 系統找不到指定的檔案。|  
  
## <a name="explanation"></a>說明  
 SharePoint 2010 包含一個 [匯出為資料摘要] 按鈕，您可以用它來匯出 SharePoint 清單當做 XML 資料摘要。 此外，SharePoint 模式的 Reporting Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 都支援需要 ADO.NET Data Services 的資料摘要功能。  
  
 如果尚未安裝 ADO.NET Data Services，則當您要求資料摘要時將會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
  
1.  移至 SharePoint 2010 的硬體和軟體需求文件集：[判斷硬體和軟體需求 (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734)。  
  
2.  在 [Installing software prerequisites] 中，尋找對應到您所使用之作業系統的 ADO.NET Data Services 3.5 連結。  
  
3.  按一下該連結，並執行安裝程式來安裝服務。  
  
## <a name="see-also"></a>請參閱  
 [將 Power Pivot 解決方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
