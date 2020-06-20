---
title: 設定公用程式控制點資料倉儲 (SQL Server 公用程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 60b9623b468f2763cf619c325412373e3603f3a3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023640"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>設定公用程式控制點資料倉儲 (SQL Server 公用程式)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體所收集的資料會儲存在公用程式管理資料倉儲 (UMDW) 中；UMDW 檔案名稱為 sysutility_mdw。  
  
 您可以設定 UMDW 資料保留週期。 如需詳細資訊，請參閱[公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)。  
  
 這一版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]無法設定下列組態設定：  
  
-   UMDW 名稱：Sysutility_mdw。  
  
-   收集組上傳頻率：每隔 15 分鐘。  
  
 UMDW 目錄是可設定的： \<System drive> ： \Program Files\Microsoft SQL Server \ MSSQL10_50。 <UCP_Name> \mssql\data \\ ，其中 \<System drive> 通常是 C：\硬碟磁碟機. 記錄檔（Sysutility_mdw_ \<GUID> _LOG）位於相同的目錄中。  
  
> [!NOTE]  
>  可以使用卸離/附加或 ALTER DATABASE 來變更 UMDW (sysutility_mdw) 檔案的位置。 我們建議使用 ALTER DATABASE。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)  
  
  
