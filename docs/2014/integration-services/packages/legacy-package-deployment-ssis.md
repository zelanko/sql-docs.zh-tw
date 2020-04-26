---
title: 封裝部署（SSIS） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c912d4417842bc332262549cc604b97eaa50a44d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767087"
---
# <a name="package-deployment-ssis"></a>封裝部署 (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含工具和精靈可以簡化將套件從開發電腦部署到實際伺服器或部署到其他電腦的流程。  
  
 封裝部署處理有四個步驟：  
  
1.  第一個選擇性的步驟是選擇性的，包含建立可在執行階段更新封裝元素屬性的封裝組態。 部署封裝時，會自動包含這些組態。  
  
2.  第二步是建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，以建立封裝部署公用程式。 專案的部署公用程式包含您要部署的封裝  
  
3.  第三步是將建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案時所建立的部署資料夾複製到目標電腦。  
  
4.  第四步是在目標電腦上執行 [封裝安裝精靈]，將封裝安裝到檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何建立部署公用程式的資訊，請參閱 [Create a Deployment Utility](../create-a-deployment-utility.md)(建立部署公用程式)。  
  
 如需如何使用部署公用程式來部署封裝的資訊，請參閱 [Deploy Packages by Using the Deployment Utility](../deploy-packages-by-using-the-deployment-utility.md)(使用部署公用程式來部署封裝)。  
  
 如需如何建立封裝組態的資訊，請參閱 [Create Package Configurations](../create-package-configurations.md)(建立封裝組態)。  
  
  
