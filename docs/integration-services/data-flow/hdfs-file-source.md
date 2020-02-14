---
title: HDFS 檔案來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a06374e2803a5e482e6d5a7a665756e38cb7f2f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71292440"
---
# <a name="hdfs-file-source"></a>HDFS 檔案來源

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  HDFS 檔案來源元件可讓 SSIS 封裝從 HDFS 檔案讀取資料。 支援的檔案格式為文字和 Avro。 (不支援 ORC 來源。)  
  
 若要設定 HDFS 檔案來源，請將 HDFS 檔案來源拖放到資料流程設計師，然後按兩下元件以開啟編輯器。  
  
 ![HDFS 檔案來源編輯器](../../integration-services/data-flow/media/hdfs-file-source.png "HDFS 檔案來源編輯器")  
  
## <a name="options"></a>選項。  
 在 [Hadoop File Source Editor (Hadoop 檔案來源編輯器)]  對話方塊的 [一般]  索引標籤上，設定下列選項。  
  
|欄位|描述|  
|-----------|-----------------|  
|**Hadoop 連接**|指定現有的 Hadoop 連接管理員或建立新的連接管理員。 此連接管理員會指出 HDFS 檔案的裝載位置。|  
|**檔案路徑**|指定 HDFS 檔案的名稱。|  
|**檔案格式**|指定 HDFS 檔案的格式。 可用的選項為文字和 Avro。 (不支援 ORC 來源。)|  
|**資料行分隔符號字元**|如果您選取文字格式，請指定資料行分隔符號字元。|  
|**第一個資料列的資料行名稱**|如果您選取文字格式，請指定檔案中的第一個資料列是否包含資料行名稱。|  
  
 設定這些選項之後，請選取 [資料行]  索引標籤，將資料流程中的來源資料行對應至目的地資料行。  
  
## <a name="see-also"></a>另請參閱  
 [Hadoop 連接管理員](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 檔案目的地](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
