---
title: "選取備份裝置 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd3728537a840869617ac7a2e28e774411014cab
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="select-backup-device"></a>選取備份裝置
  使用 **[選取備份裝置]** 對話方塊，可選取還原作業的邏輯備份裝置。  
  
 邏輯備份裝置是使用者自訂的邏輯裝置，會對應至作業系統所提供的實體裝置 (磁帶機或磁碟機)。  
  
> [!NOTE]  
>  如果備份使用到多個備份裝置，則所有的備份裝置都必須對應至單一類型的裝置。  
  
 **若要使用 SQL Server Management Studio 檢視備份裝置的內容**  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>選項  
 **備份裝置**  
 在清單方塊中，選取您要從中還原之邏輯備份裝置的名稱。  
  
 如需如何檢視備份裝置內容的相關資訊，請參閱 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)。  
  
## <a name="remarks"></a>備註  
 如果您在清單中沒有看到包含您要搜尋之備份的邏輯備份裝置，則可能是已將備份直接寫入至一個或多個檔案或磁帶機。 如果是這種情況，請取消 **[選取備份裝置]** 對話方塊，並且在 **[指定備份]** 對話方塊的 **[備份媒體]** 清單方塊中選取 **[檔案]** 或 **[磁帶]** 。  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
