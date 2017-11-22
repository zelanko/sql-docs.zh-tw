---
title: "設定和管理 |Microsoft 文件"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0fd4554-60c6-4181-ac4c-2e366fb434f6
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f90cb9c8792086352403a6bb937391daf3f338f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configuration-and-management"></a>設定和管理

本文提供有關如何設定伺服器以支援這些產品機器學習服務與 SQL Server 的詳細資訊的連結：

+ SQL Server 2016 R 服務 （資料庫）
+ SQL Server 2017 機器學習服務 （資料庫）

> [!NOTE]
> 
> SQL Server 2016 版本支援 R 語言的原始寫入此內容。
> 
> 在 SQL Server 2017，支援已加入 Python，但是基礎架構和服務架構是相同的。 因此，您可以設定安全性、 記憶體、 資源控管和其他選項，以支援執行 Python 指令碼，您會為 R 指令碼的方式相同。
> 
> 不過，因為 Python 是新的功能、 潛在的最佳化的詳細的資訊的 Python 工作負載尚無可用的支援。 請請稍後再回來查看。

## <a name="r-package-management"></a>R 封裝管理

這些主題說明如何在 SQL Server 執行個體上安裝新的 R 封裝、 管理 R 封裝程式庫，以及資料庫還原後還原封裝程式庫。

+ [安裝和管理 R 封裝](installing-and-managing-r-packages.md)
+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [使用資料庫角色執行個體啟用封裝管理](r-package-how-to-enable-or-disable.md)
+ [建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [判斷 SQl Server 上已安裝的 R 封裝](determine-which-packages-are-installed-on-sql-server.md)
+ [SQL Server 和檔案系統之間同步處理的 R 封裝](package-install-uninstall-and-sync.md)
+ [使用者文件庫中安裝 R 封裝](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>服務組態

這些主題說明如何變更的基礎服務架構以及如何管理與擴充性服務相關聯的安全性主體。

+ [安全性考量](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [修改 SQL Server R 服務的使用者帳戶集區](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [設定及管理進階分析擴充功能](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [使用資料庫角色執行個體啟用封裝管理](r-package-how-to-enable-or-disable.md)
+ [R 服務的效能微調](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>資源管理

這些主題說明如何實作 R 或 Python 作業在 Enterprise Edition 中使用資源管理員功能可用的資源管理。

+ [的資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [How to Create a Resource Pool](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

另請參閱：

+ [使用自訂的 SSMS 報告監視 R](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>初始安裝

這些主題中可以找到與初始安裝和設定相關的其他說明：

+ [升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [安全性考量](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [R Services 已知的問題](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

