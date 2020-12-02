---
title: 選取備份裝置 | Microsoft Docs
description: 針對 SQL Server 還原，請使用 [選取備份裝置] 對話方塊，以選取還原作業的邏輯備份裝置。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3eb2dc44dde731d77ecea441532d45f8b7fa8b39
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125501"
---
# <a name="select-backup-device"></a>選取備份裝置
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  使用 **[選取備份裝置]** 對話方塊，可選取還原作業的邏輯備份裝置。  
  
 邏輯備份裝置是使用者自訂的邏輯裝置，會對應至作業系統所提供的實體裝置 (磁帶機或磁碟機)。  
  
> [!NOTE]  
>  如果備份使用到多個備份裝置，則所有的備份裝置都必須對應至單一類型的裝置。  
  
 **若要使用 SQL Server Management Studio 檢視備份裝置的內容**  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>選項。  
 **備份裝置**  
 在清單方塊中，選取您要從中還原之邏輯備份裝置的名稱。  
  
 如需如何檢視備份裝置內容的相關資訊，請參閱 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)。  
  
## <a name="remarks"></a>備註  
 如果您在清單中沒有看到包含您要搜尋之備份的邏輯備份裝置，則可能是已將備份直接寫入至一個或多個檔案或磁帶機。 如果是這種情況，請取消 **[選取備份裝置]** 對話方塊，並且在 **[指定備份]** 對話方塊的 **[備份媒體]** 清單方塊中選取 **[檔案]** 或 **[磁帶]** 。  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
