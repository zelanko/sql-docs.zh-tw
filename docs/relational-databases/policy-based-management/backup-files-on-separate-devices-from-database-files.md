---
title: 備份檔案必須位於和資料庫檔案不同的裝置上
description: 了解如何啟用原則來檢查備份檔案位置，將該位置與資料庫檔案位置進行比較，以搭配 SQL Server 進行原則式管理。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 5b98f8163a3564ccc4aadac6c71c30eb5cf37697
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285067"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>備份檔案必須位於和資料庫檔案不同的裝置上
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此規則會檢查資料庫檔案是否位在與備份檔案不同的裝置上。 如果資料庫檔案和備份檔案位於相同的裝置上，而且該裝置發生錯誤，將無法使用資料庫和備份。 此外，將資料庫和備份檔案放在不同裝置上會將資料庫的生產使用和寫入備份的 I/O 效能最佳化。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 我們建議備份磁碟應該與資料庫資料和記錄磁碟使用不同的磁碟。 為了確保您可以在資料或記錄磁碟故障時存取備份，這樣做有其必要。

如果資料庫檔案和備份檔案位於相同的裝置上，而且該裝置發生錯誤，將無法使用資料庫和備份。 此外，將資料庫和備份檔案放在不同裝置上會將資料庫的生產使用和寫入備份的 I/O 效能最佳化。
  
## <a name="see-also"></a>另請參閱 
   
  
 [備份裝置](../backup-restore/backup-devices-sql-server.md)  
  
