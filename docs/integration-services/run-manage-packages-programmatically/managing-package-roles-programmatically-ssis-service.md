---
title: 以程式設計方式管理套件角色 (SSIS 服務) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cfc826b47bdd58e11a912a320eb3e71ff389c413
ms.sourcegitcommit: a251adad8474b477363df6a121431b837f22bf77
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47864166"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>以程式設計方式管理封裝角色 (SSIS 服務)
  當您以程式設計方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，可能會想要判斷有哪些角色可供套用至封裝，或是判斷或設定套用至個別封裝的角色。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空間的 <xref:Microsoft.SqlServer.Dts.Runtime> 類別，提供各種方法以滿足這些需求。  
  
 角色只能套用到儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 資料庫的套件中。 如需套件角色的詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)。  
  
 本主題中討論的所有方法都需要 **Microsoft.SqlServer.ManagedDTS** 組件的參考。 在新專案中新增參考之後，請使用 **using** 或 **Imports** 陳述式匯入 <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間。  
  
> [!IMPORTANT]  
>  用以搭配 SSIS 封裝存放區使用的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別之方法，僅支援 "."、localhost 或是本機伺服器的伺服器名稱。 您無法使用 "(local)"。  
  
## <a name="determining-which-roles-are-available"></a>判斷可以使用哪些角色  
 若要判斷有哪些角色可供儲存在特定伺服器上的封裝使用，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 方法。  
  
## <a name="determining-which-roles-are-assigned"></a>判斷已指派哪些角色  
 若要判斷已將哪些角色指派到特定封裝，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 方法。 若要將角色指派到套件，請呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 方法。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 角色 &#40;SSIS 服務&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
