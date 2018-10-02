---
title: 工作主機容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7f421e1d4a127b5f359313c7fb31e66327dd347b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694106"
---
# <a name="task-host-container"></a>工作主機容器
  工作主機容器會封裝單一工作。 在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，工作主機不會另外設定，而是在您設定其封裝之工作的屬性時設定。 如需工作主機容器所封裝工作的詳細資訊，請參閱 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)。  
  
 此容器會將變數與事件處理常式的使用延伸至工作層級。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 事件處理常式](../../integration-services/integration-services-ssis-event-handlers.md)和 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  
  
## <a name="configuration-of-the-task-host"></a>設定工作主機  
 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [屬性] 視窗中，或以程式設計方式設定屬性。  
  
 如需在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中設定這些屬性的相關資訊，請參閱 [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
 如需以程式設計方式設定這些屬性的相關資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>另請參閱  
 [整合服務容器](../../integration-services/control-flow/integration-services-containers.md)  
  
  
