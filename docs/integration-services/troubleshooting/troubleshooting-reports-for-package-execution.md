---
description: 疑難排解封裝執行的報表
title: 針對套件執行的報告進行疑難排解 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fc476ac-bd69-434e-9636-70776e0b3b6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c91d575842410d79411bb5cdd77d5ecff27f13c7
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88495160"
---
# <a name="troubleshooting-reports-for-package-execution"></a>疑難排解封裝執行的報表

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的目前版本中， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供一些標準報表，可協助您監視和疑難排解已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 其中兩份封裝報表特別有助於您檢視封裝執行狀態以及識別執行失敗的原因。  
  
-   **Integration Services 儀表板** - 這份報表會提供過去 24 小時內 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上所有封裝執行的概觀。 此報表顯示每個封裝諸如狀態、作業類型、封裝名稱等資訊。  
  
     您可以依照下列方式解譯開始時間、結束時間和持續時間：  
  
    -   如果封裝仍在執行中，則持續時間 = 目前時間 - 開始時間  
  
    -   如果封裝已完成，則持續時間 = 結束時間 - 開始時間  
  
     對於伺服器上已執行的每個封裝，儀表板可讓您放大報表，尋找可能發生之封裝執行錯誤的特定詳細資料。 例如，您可以按一下 [概觀] 顯示執行中工作狀態的高階概觀，或是按一下 [所有訊息] 顯示封裝執行過程中已擷取的詳細訊息。  
  
     您可以按一下 [篩選]  ，然後選取 [篩選設定]  對話方塊中的準則，篩選任何頁面上顯示的資料表。 可用的篩選準則取決於顯示的資料。 您可以在 [篩選設定]  對話方塊中按一下排序圖示，以變更報表的排序次序。  
  
-   **活動 - 所有執行報表** - 這份報表會顯示伺服器上已執行之所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行的摘要。 此摘要會顯示每個執行的資訊，例如狀態、開始時間和結束時間。 每個摘要項目都包含執行詳細資訊的連結，包括執行期間產生的訊息以及效能資料。 就如同 Integration Services 儀表板一樣，您可以將篩選套用至資料表，以縮小顯示的資訊範圍。  
  
## <a name="related-content"></a>相關內容  
 [Integration Services 伺服器的報表](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)  
  
 [套件執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
