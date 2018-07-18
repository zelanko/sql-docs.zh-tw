---
title: 重新部署的封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 35
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 02206eef9b83af13999e9a510253fc9264a5bda1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300528"
---
# <a name="redeployment-of-packages"></a>封裝的重新部署
  在部署專案後，您可能需要更新或擴充封裝功能，然後部署包含已更新封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。 做為重新部署封裝處理的一部分，您應該檢視包含在部署公用程式中的組態屬性。 例如，您可能不允許組態在重新部署封裝之後變更。  
  
## <a name="process-for-redeployment"></a>重新部署程序  
 在封裝更新完成後，您會重新建置專案、將部署資料夾複製到目標電腦，然後傳回 [封裝安裝精靈]。  
  
 如果您只更新專案中的幾個封裝，則可能不想重新部署整個專案。 若要只部署幾個封裝，您可以建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案、將已更新的封裝加入新的專案，然後建立和部署該專案。 當您將封裝加入其他專案時，封裝組態會自動隨封裝一同複製。  
  
## <a name="related-tasks"></a>相關工作  
 [使用部署公用程式來部署套件](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  
