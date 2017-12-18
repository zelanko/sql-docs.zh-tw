---
title: "Hadoop 連線管理員 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c4bf82dad09b90f672e52947267ddf92fbdb984
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="hadoop-connection-manager"></a>Hadoop 連接管理員
  Hadoop 連接管理員可讓 SSIS 封裝使用您指定的屬性值連接到 Hadoop 叢集。  
  
## <a name="configure-the-hadoop-connection-manager"></a>設定 Hadoop 連接管理員  
  
1.  在 [加入 SSIS 連線管理員] 對話方塊中，選取 [Hadoop]，然後按一下 [加入]。 [Hadoop 連線管理員編輯器] 對話方塊隨即開啟。  
  
2.  選擇左窗格中的 [WebHCat] 或 [WebHDFS] 索引標籤，設定相關的 Hadoop 叢集資訊。  
  
3.  如果您啟用 [WebHCat] 選項，以在 Hadoop 上叫用 Hive 或 Pig 工作，請執行下列動作。  
  
    1.  對於 [WebHCat 主機]，輸入裝載 WebHCat 服務的伺服器。  
  
    2.  對於 [WebHCat 連接埠]，輸入 WebHCat 服務的連接埠 (預設為 50111)。  
  
    3.  選取用於存取 WebHCat 服務的 [驗證] 方法。 可用的值為：[基本] 和 [Kerberos]。  
  
         ![使用基本驗證的 Hadoop 連線管理員編輯器](../../integration-services/connection-manager/media/hadoop-cm-basic.png "使用基本驗證的 Hadoop 連線管理員編輯器")  
  
         ![使用 Kerberos 驗證的 Hadoop 連線管理員編輯器](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "使用 Kerberos 驗證的 Hadoop 連線管理員編輯器")  
  
    4.  對於 [WebHCat 使用者]，輸入已授權可存取 WebHCat 的 [使用者]。  
  
    5.  如果您選取 [Kerberos] 驗證，請輸入使用者的 [密碼] 和 [網域]。  
  
4.  如果您啟用 [WebHDFS] 選項以從 HDFS 中複製資料或將資料複製至其中，請執行下列動作。  
  
    1.  對於 [WebHDFS 主機]，輸入裝載 WebHDFS 服務的伺服器。  
  
    2.  對於 [WebHDFS 連接埠]，輸入 WebHDFS 服務的連接埠 (預設為 50070)。  
  
    3.  選取用於存取 WebHDFS 服務的 [驗證] 方法。 可用的值為：[基本] 和 [Kerberos]。  
  
    4.  對於 [WebHDFS 使用者]，輸入已授權可存取 HDFS 的使用者。  
  
    5.  如果您選取 [Kerberos] 驗證，請輸入使用者的 [密碼] 和 [網域]。  
  
5.  按一下 [測試連接] 來測試連接。 (只會測試您已啟用的連接)。  
  
6.  按一下 **[確定]** ，關閉對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [Hadoop Hive 工作](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig 工作](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop 檔案系統工作](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
