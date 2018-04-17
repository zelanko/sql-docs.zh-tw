---
title: 設定及管理 SQL Server 機器學習服務執行個體 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0b524e7e9fb24ff0296fc0e70c8bb8a462f3d199
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="configure-and-manage-machine-learning-components-in-sql-server"></a>設定及管理 SQL Server 中的機器學習服務元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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

這些文章說明如何在 SQL Server 執行個體上安裝新的 R 封裝、 管理 R 封裝程式庫，以及資料庫還原後還原封裝程式庫。

+ [安裝和管理 R 封裝](installing-and-managing-r-packages.md)
+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [使用資料庫角色執行個體啟用封裝管理](r-package-how-to-enable-or-disable.md)
+ [建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [判斷 SQl Server 上已安裝的 R 封裝](determine-which-packages-are-installed-on-sql-server.md)
+ [SQL Server 和檔案系統之間同步處理的 R 封裝](package-install-uninstall-and-sync.md)
+ [使用者文件庫中安裝 R 封裝](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>服務組態

這些文章說明如何變更的基礎服務架構以及如何管理與擴充性服務相關聯的安全性主體。

+ [安全性考量](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [修改 SQL Server R 服務的使用者帳戶集區](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [設定及管理進階分析擴充功能](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [使用資料庫角色執行個體啟用封裝管理](r-package-how-to-enable-or-disable.md)
+ [R 服務的效能微調](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>資源管理

這些文章說明如何實作 R 或 Python 作業在 Enterprise Edition 中使用資源管理員功能可用的資源管理。

+ [的資源管理](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [How to Create a Resource Pool](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

另請參閱：

+ [使用自訂的 SSMS 報告監視 R](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>初始安裝

與初始安裝和設定相關的其他說明，請參閱下列文章：

+ [升級及安裝常見問題集](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [安全性考量](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [R Services 已知的問題](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

