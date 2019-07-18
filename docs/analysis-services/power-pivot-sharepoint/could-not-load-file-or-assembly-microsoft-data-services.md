---
title: 無法載入檔案或組件的 Microsoft Data Services |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9472fffb790d8d18ced8d2a528011927717aabc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164165"
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>無法載入檔案或組件的 Microsoft Data Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在擁有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 2010 環境中，若您嘗試匯出資料摘要且系統遺漏必要的 Microsoft ADO.NET Data Services 版本，將會發生此錯誤。  
  
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
  
1.  移至適用於 SharePoint 2010 的硬體和軟體需求文件[判斷硬體和軟體需求 (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734) 。  
  
2.  在 [Installing software prerequisites]  中，尋找對應到您所使用之作業系統的 ADO.NET Data Services 3.5 連結。  
  
3.  按一下該連結，並執行安裝程式來安裝服務。  
  
## <a name="see-also"></a>另請參閱  
 [將 Power Pivot 解決方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
