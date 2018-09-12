---
title: 備份檔案必須位在不同的資料庫檔案的裝置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18b1f6d38f67dacc2a8da06a061d6bd76e055196
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818104"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>備份檔案必須位在與資料庫檔案不同的裝置上
  此規則會檢查資料庫檔案是否位在與備份檔案不同的裝置上。 如果資料庫檔案和備份檔案位於相同的裝置上，而且該裝置發生錯誤，將無法使用資料庫和備份。 此外，將資料庫和備份檔案放在不同裝置上會將資料庫的生產使用和寫入備份的 I/O 效能最佳化。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 我們強烈建議您將資料庫和備份放在不同的備份裝置上。  
  
> [!NOTE]  
>  這個原則無法透過掛接點偵測個別的實體裝置。  
  
## <a name="for-more-information"></a>詳細資訊  
 [備份裝置 &#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [SQL Server 資料庫的備份與還原](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
