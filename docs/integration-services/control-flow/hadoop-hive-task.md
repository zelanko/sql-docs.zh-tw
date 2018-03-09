---
title: "Hadoop Hive 工作 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66e0ac41dbc9015be94ec18180a5c8fa3932efe9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="hadoop-hive-task"></a>Hadoop Hive 工作
  使用 Hadoop Hive 工作在 Hadoop 叢集上執行 Hive 指令碼。  
  
 若要加入 Hadoop Hive 工作，請將其拖放至設計工具。 然後在工作上按兩下，或按一下滑鼠右鍵並按一下 [編輯]，以開啟 [Hadoop Hive 工作編輯器] 對話方塊。  
  
 ![Hadoop Hive 工作編輯器](../../integration-services/control-flow/media/hadoop-hive-task.png "Hadoop Hive 工作編輯器")  
  
## <a name="options"></a>選項。  
 在 [Hadoop Hive 工作編輯器] 對話方塊中設定下列選項。  
  
|欄位|描述|  
|-----------|-----------------|  
|**Hadoop 連接**|指定現有的 Hadoop 連接管理員或建立新的連接管理員。 此連接管理員會指出 WebHCat 服務的裝載位置。|  
|**SourceType**|指定查詢的來源類型。 可用的值為 **ScriptFile** 和 **DirectInput**。|  
|**InlineScript**|當 **SourceType** 的值為 **DirectInput**時，指定 Hive 指令碼。|  
|**HadoopScriptFilePath**|當 **SourceType** 的值為 **ScriptFile**時，在 Hadoop 上指定指令碼檔案路徑。|  
|**TimeoutInMinutes**|以分鐘為單位來指定逾時值。 如果在逾時之前尚未完成的話，則 Hadoop 工作將會停止。 指定 0 以為 Hadoop 工作進行排程，以便以非同步方式執行。|  
  
## <a name="see-also"></a>另請參閱  
 [Hadoop 連接管理員](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
