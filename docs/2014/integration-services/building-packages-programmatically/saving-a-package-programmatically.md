---
title: 以程式設計方式儲存套件 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0304d4ba3388874fbd2c19001b12094f1df4d351
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836694"
---
# <a name="saving-a-package-programmatically"></a>以程式設計方式儲存封裝
  在以程式設計方式建立新封裝或是修改現有封裝之後，通常會想要儲存變更。  
  
 本主題中用以儲存封裝的所有方法需要 `Microsoft.SqlServer.ManagedDTS` 組件的參考。 在新專案中加入參考之後，請使用 `using` 或 `Imports` 陳述式來匯入 <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間。  
  
## <a name="saving-a-package-programmatically"></a>以程式設計方式儲存封裝  
 若要以程式設計方式儲存套件，請呼叫 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別的下列其中一種方法：  
  
|儲存位置|要呼叫的方法|  
|----------------------|--------------------|  
|檔案|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 中的多個<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  用以搭配 SSIS 封裝存放區使用的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別之方法，僅支援 "." 或是本機伺服器的伺服器名稱。 您無法使用 "(本機)" 或者"localhost"。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [儲存套件](../save-packages.md)  
  
  
