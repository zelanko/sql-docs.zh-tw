---
title: 選取備份裝置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 76cf12be8e5ae29d5f6dfe22d4ef5e7233b8677a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141548"
---
# <a name="select-backup-device"></a>選取備份裝置
  使用 **[選取備份裝置]** 對話方塊，可選取還原作業的邏輯備份裝置。  
  
 邏輯備份裝置是使用者自訂的邏輯裝置，會對應至作業系統所提供的實體裝置 (磁帶機或磁碟機)。  
  
> [!NOTE]  
>  如果備份使用到多個備份裝置，則所有的備份裝置都必須對應至單一類型的裝置。  
  
 **若要使用 SQL Server Management Studio 檢視備份裝置的內容**  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>選項。  
 **備份裝置**  
 在清單方塊中，選取您要從中還原之邏輯備份裝置的名稱。  
  
 如需如何檢視備份裝置內容的相關資訊，請參閱 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)。  
  
## <a name="remarks"></a>備註  
 如果您在清單中沒有看到包含您要搜尋之備份的邏輯備份裝置，則可能是已將備份直接寫入至一個或多個檔案或磁帶機。 如果是這種情況，請取消 **[選取備份裝置]** 對話方塊，並且在 **[指定備份]** 對話方塊的 **[備份媒體]** 清單方塊中選取 **[檔案]** 或 **[磁帶]** 。  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
