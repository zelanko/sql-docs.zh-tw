---
title: "以程式設計方式管理封裝角色 （SSIS 服務） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7a7fb000389756caf0c2f2ea00cd0b80e75557d8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="managing-package-roles-programmatically-ssis-service"></a>以程式設計方式管理封裝角色 (SSIS 服務)
  當您以程式設計方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，可能會想要判斷有哪些角色可供套用至封裝，或是判斷或設定套用至個別封裝的角色。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別，提供各種方法以滿足這些需求。  
  
 角色只能套用至儲存在封裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**資料庫。 如需封裝角色的詳細資訊，請參閱[Integration Services 角色 &#40;SSIS 服務 &#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 本主題所討論的所有方法都必須參考**Microsoft.SqlServer.ManagedDTS**組件。 在新的專案中加入參考之後，匯入<xref:Microsoft.SqlServer.Dts.Runtime>命名空間使用**使用**或**匯入**陳述式。  
  
> [!IMPORTANT]  
>  用以搭配 SSIS 封裝存放區使用的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別之方法，僅支援 "."、localhost 或是本機伺服器的伺服器名稱。 您無法使用 "(local)"。  
  
## <a name="determining-which-roles-are-available"></a>判斷可以使用哪些角色  
 若要判斷有哪些角色可供儲存在特定伺服器上的封裝使用，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 方法。  
  
## <a name="determining-which-roles-are-assigned"></a>判斷已指派哪些角色  
 若要判斷已將哪些角色指派到特定封裝，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 方法。 若要將角色指派到套件，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 方法。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 角色 &#40;SSIS 服務 &#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  

