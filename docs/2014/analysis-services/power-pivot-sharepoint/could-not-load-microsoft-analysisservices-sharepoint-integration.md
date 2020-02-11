---
title: 無法載入檔案或元件 &#39;的3.5.0.0、Culture = 中性、PublicKeyToken = b77a5c561934e089&#39; 或其相依性的其中之一。 系統找不到指定的檔案。 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b33e09d4dc7471f6447f1205f5c39746bc247ae7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071626"
---
# <a name="could-not-load-file-or-assembly-39microsoftdataservices-version3500-cultureneutral-publickeytokenb77a5c561934e08939-or-one-of-its-dependencies-the-system-cannot-find-the-file-specified"></a>無法載入檔案或元件 &#39;的3.5.0.0、Culture = 中性、PublicKeyToken = b77a5c561934e089&#39; 或其相依性的其中之一。 系統找不到指定的檔案。
  在擁有 PowerPivot for SharePoint 的 SharePoint 2010 環境中，如果您嘗試匯出資料摘要而且系統遺漏必要的 Microsoft ADO.NET Data Services 版本，將會發生這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用於|PowerPivot for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|找不到 ADO.NET Data Services 3.5 SP1。|  
|訊息文字|無法載入檔案或組件 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' 或是它的其中一個相依性。 系統找不到指定的檔案。|  
  
## <a name="explanation"></a>說明  
 SharePoint 2010 包含一個 [匯出為資料摘要] 按鈕，您可以用它來匯出 SharePoint 清單當做 XML 資料摘要。 此外，SharePoint 模式的 Reporting Services 和 PowerPivot for SharePoint 都支援需要 ADO.NET Data Services 的資料摘要功能。  
  
 如果尚未安裝 ADO.NET Data Services，則當您要求資料摘要時將會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
  
1.  請移至 SharePoint 2010 的硬體和軟體需求檔，[判斷硬體和軟體需求（sharepoint 2010）](https://go.microsoft.com/fwlink/?LinkId=169734) （https://go.microsoft.com/fwlink/?LinkId=169734)。  
  
2.  在 [Installing software prerequisites]**** 中，尋找對應到您所使用之作業系統的 ADO.NET Data Services 3.5 連結。  
  
3.  按一下該連結，並執行安裝程式來安裝服務。  
  
## <a name="see-also"></a>另請參閱  
 [將 PowerPivot 方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
