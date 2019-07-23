---
title: 以程式設計方式儲存套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e2a39d00ca84d7bcc428957ef254cc03a81648bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070636"
---
# <a name="saving-a-package-programmatically"></a>以程式設計方式儲存封裝

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在以程式設計方式建立新封裝或是修改現有封裝之後，通常會想要儲存變更。  
  
 本主題中用來儲存套件的所有方法，都需要 **Microsoft.SqlServer.ManagedDTS** 組件的參考。 在新專案中新增參考之後，請使用 **using** 或 **Imports** 陳述式匯入 <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間。  
  
## <a name="saving-a-package-programmatically"></a>以程式設計方式儲存封裝  
 若要以程式設計方式儲存套件，請呼叫 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別的下列其中一種方法：  
  
|儲存位置|要呼叫的方法|  
|----------------------|--------------------|  
|檔案|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 中的多個<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  用以搭配 SSIS 封裝存放區使用的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別之方法，僅支援 "." 或是本機伺服器的伺服器名稱。 您無法使用 "(本機)" 或者"localhost"。  
  
## <a name="see-also"></a>另請參閱  
 [儲存套件](../../integration-services/save-packages.md)  
  
  
