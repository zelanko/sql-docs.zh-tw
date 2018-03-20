---
title: "自動的安裝的 Python 機器學習服務 （資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 07/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: r-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 810adfeca86bc12bf05561eb50d555261579a1a5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="unattended-installation-of-python-machine-learning-services-in-database"></a>自動的安裝的 Python 機器學習服務 （資料庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題描述如何使用 SQL Server 2017 安裝程式中的命令列引數，若要使用機器學習服務，並將 Python，使用無訊息模式安裝的 SQL Server database engine。

> [!NOTE]
> 別忘了要包含授權合約，一個用於 Python，另一個適用於 SQL Server 的命令列引數。

## <a name="prerequisites"></a>필수 구성 요소

開始安裝程序之前，請注意下列需求：

+ Python 服務無法安裝獨立的 SQL Server 2017 database engine。 您必須包含 SQL 資料庫引擎功能。
+ 如果您正在執行離線安裝，您必須事先下載必要的 Python 元件，並將它們複製到本機資料夾。 如需下載位置，請參閱[安裝機器學習 Components without Internet Access](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)。
+ 沒有新的參數， */IACCEPTPYTHONLICENSETERMS*，表示您接受授權條款的使用 Continuum Analytics 所提供的 Python 元件。 如果您沒有在命令列中包含此參數，安裝程式將會失敗。
+ 若要完成安裝程式，而不需要回應提示，請確定您已識別所有必要的引數，包括 Python 和 SQL Server 的授權，以及任何其他您可能想要安裝的功能。
+  在 SQL Server 2016 的某些發行前版本需要混合的模式驗證。 它不再需要，但它可能適用於資料科學家開發和測試解決方案從遠端使用 SQL 登入其中的情況。

## <a name="perform-an-unattended-installation-of-python-machine-learning-services-in-database"></a>執行自動的安裝的 Python 機器學習服務 （資料庫）

下列範例所示**最小**必要的執行無訊息自動安裝 Python 和 database engine 的預設執行個體上時，在命令列中指定的功能。

> [!NOTE]
> 此功能需要 SQL Server 2017。 在舊版的 SQL Server 不支援 Python。

1. 開啟提升權限的命令提示字元中，並執行下列命令：

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONLICENSETERMS
    ```

    > [!NOTE]
    > 
    > 有新的安裝旗標的 Python:`SQL_INST_MPY`和`IACCEPTPYTHONLICENSETERMS`

2. 依照指示，請重新啟動伺服器。
3. 執行後續安裝設定步驟中所述[本節](#bkmk_PostInstall)。 另一個 SQL Server 服務重新啟動將會需要。

## <a name = "bkmk_PostInstall"></a>安裝後步驟

1.  安裝完成後，開啟新**查詢**視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行下列命令以啟用功能。

    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  您必須明確啟用功能並重新設定。否則，它將無法叫用外部指令碼，即使已安裝的功能。
  
3.  重新啟動 SQL Server 服務重新設定的執行個體。 這樣會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]以及服務。

3. 如果您有自訂安全性設定，或您將使用 SQL Server 支援遠端計算內容，則可能需要額外的步驟。 如需詳細資訊，請參閱[疑難排解機器學習安裝](../machine-learning-troubleshooting-faq.md)。
