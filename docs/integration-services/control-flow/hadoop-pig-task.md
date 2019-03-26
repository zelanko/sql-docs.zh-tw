---
title: Hadoop Pig 工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 88b9871a3e89ab1f21c6c37344ed26e19fc5dca7
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271712"
---
# <a name="hadoop-pig-task"></a>Hadoop Pig 工作
  使用 Hadoop Pig 工作在 Hadoop 叢集上執行 Pig 指令碼。  
  
 若要加入 Hadoop Pig 工作，請將其拖放至設計工具。 然後按兩下工作，或按一下滑鼠右鍵並按一下 [編輯]，以查看 [Hadoop Pig 工作編輯器] 對話方塊。  
  
 ![Hadoop Pig 工作編輯器](../../integration-services/control-flow/media/hadoop-pig-task.png "Hadoop Pig 工作編輯器")  
  
## <a name="options"></a>選項。  
 在 [Hadoop Pig 工作編輯器] 對話方塊中設定下列選項。  
  
|欄位|Description|  
|-----------|-----------------|  
|**Hadoop 連接**|指定現有的 Hadoop 連接管理員或建立新的連接管理員。 此連接管理員會指出 WebHCat 服務的裝載位置。|  
|**SourceType**|指定查詢的來源類型。 可用的值為 **ScriptFile** 和 **DirectInput**。|  
|**InlineScript**|當 **SourceType** 的值為 **DirectInput**時，指定 Pig 指令碼。|  
|**HadoopScriptFilePath**|當 **SourceType** 的值為 **ScriptFile**時，在 Hadoop 上指定指令碼檔案路徑。|  
|**TimeoutInMinutes**|以分鐘為單位來指定逾時值。 如果在逾時之前尚未完成的話，則 Hadoop 工作將會停止。 指定 0 以為 Hadoop 工作進行排程，以便以非同步方式執行。|  
  
## <a name="see-also"></a>另請參閱  
 [Hadoop 連接管理員](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
