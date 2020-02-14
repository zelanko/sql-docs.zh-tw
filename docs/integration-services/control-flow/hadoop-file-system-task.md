---
title: Hadoop 檔案系統工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e97ae33bcccee338be576138ca335bd6298e0128
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294074"
---
# <a name="hadoop-file-system-task"></a>Hadoop 檔案系統工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Hadoop 檔案系統工作可讓 SSIS 封裝在 Hadoop 叢集內進行檔案複製。  
  
 若要加入 Hadoop 檔案系統工作，請將其拖放至設計工具。 然後在工作上按兩下，或按一下滑鼠右鍵，再按 編輯  ，以開啟 Hadoop 檔案系統工作編輯器)  對話方塊。  
  
 ![Hadoop 檔案系統工作編輯器](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Hadoop 檔案系統工作編輯器")  
  
## <a name="options"></a>選項。  
 在 Hadoop 檔案系統工作編輯器)  對話方塊中設定下列選項。  
  
|欄位|描述|  
|-----------|-----------------|  
|**Hadoop 連接**|指定現有的 Hadoop 連接管理員或建立新的連接管理員。 此連線管理員會指出目的地檔案的裝載位置。|  
|**Hadoop 檔案路徑**|指定 HDFS 上的檔案或目錄路徑。|  
|**Hadoop 檔案類型**|指定 HDFS 檔案系統物件是檔案還是目錄。|  
|**覆寫目的地**|指定是否要覆寫目標檔案 (如果它已經存在的話)。|  
|**運算**|指定作業。 可用的作業包括 **CopyToHDFS**、 **CopyFromHDFS**和 **CopyWithinHDFS**。|  
|**本機檔案連線**|指定現有的檔案連線管理員或建立新的連線管理員。 此連線管理員會指出來源檔案的裝載位置。|  
|**是否遞迴**|指定是否要以遞迴方式複製所有的子資料夾。|  
  
## <a name="see-also"></a>另請參閱  
 [Hadoop 連接管理員](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
