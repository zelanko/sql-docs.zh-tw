---
title: "自動的安裝的機器學習服務 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f1c7aaf35c0c58e9a7aab3c5b31725f586ffd2ac
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2018
---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>自動的安裝的機器學習服務 （資料庫）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何使用 SQL Server 安裝程式中的命令列引數，若要安裝的機器學習服務元件。

自動安裝，是指，不使用互動式功能，安裝精靈中，並改為提供完整的安裝，包括授權合約適用於 SQL Server 和機器學習元件上所需的所有引數命令列或指令碼中，通常會以無訊息模式的一部分。

+ [SQL Server 2016 R Services](#bkmk_OldInstall)
+ [SQL Server 2017 機器學習服務](#bkmk_NewInstall)與 R 或 Python
+ [Microsoft R 伺服器或機器學習伺服器](../r/install-microsoft-r-server-from-the-command-line.md)

**適用於： SQL Server 2017 機器學習服務 （資料庫），SQL Server 2016 R Services**

## <a name="prerequisites"></a>필수 구성 요소

+ 您必須在您將在其中使用機器學習服務每個執行個體上安裝資料庫引擎。

+ 如果電腦沒有網際網路存取，請務必下載機器事先學習元件的安裝程式。 請參閱[安裝沒有網際網路存取的機器學習元件](../r/installing-ml-components-without-internet-access.md)。

+ 有個別的 R，並將 Python 授權每一個開放原始碼元件的參數。 SQL Server 2016 支援只 R;SQL Server 2017 支援 R 和 Python。 您必須接受授權條款的每個安裝的語言。 如果您未在命令列中包含這個參數，安裝程式將會失敗。

+ 若要完成安裝程式，而不需要回應提示，請確定您已識別所有必要的引數，包括授權，以及任何其他您可能想要安裝的功能。

+ **混合**支援 SQL 登入的安全性模式下不需要像最早的版本。 雖然已不再需要，您可以考慮啟用混合模式驗證，以支援使用 SQL 登入的資料科學家所開發的解決方案。

> [!IMPORTANT]
> 
> 若要啟用此功能安裝完成之後，不需要額外的步驟。 這些包括重新設定，然後重新啟動執行個體。 請務必檢閱上一節中的所有項目[後續安裝步驟](#bkmk_PostInstall)以判斷安裝完成之後，需要的動作。

## <a name="bkmk_NewInstall"></a>  命令列安裝的 SQL Server 2017

下列範例中包含**最小**必要的功能。

> [!IMPORTANT]
> 請務必從提升權限的命令提示字元執行所有的命令。
> 
> 安裝完成後，一些額外的步驟所需。 請參閱[本節](#bkmk_PostInstall)。 
> 設定完成之後，將會需要另一個 SQL Server 服務重新啟動。

### <a name="install-r-only"></a>只安裝 R

下列範例會示範執行無訊息方式，自動安裝所需的引數加入之 R 語言安裝的 SQL Server 2017 機器服務 （資料庫）。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

請注意在 SQL Server 2017 R 所需的旗標：

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MR`
+ `IACCEPTROPENLICENSETERMS`。

### <a name="install-python-only"></a>只安裝 Python

下列範例會示範使用加入 Python 語言安裝的 SQL Server 2017 機器服務 （資料庫） 的執行無訊息方式，自動安裝所需的引數。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

請注意在 SQL Server 2017 Python 所需的旗標：

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

### <a name="install-both-r-and-python-on-a-named-instance"></a>具名執行個體上安裝 R 和 Python

下列範例會示範執行無訊息方式，自動安裝所需的引數安裝 SQL Server 2017 機器 Services （資料庫） 的具名執行個體上。 會加入 R 和 Python 語言。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

## <a name="OldInstall"></a> SQL Server 2016 命令列安裝
 
下列範例示範加入之 R 語言安裝的 SQL Server 2016 的執行無訊息方式，自動安裝所需的引數。

```
Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

請注意 2016 R 服務所需的旗標：

+ `ADVANCEDANALYTICS`
+ `IACCEPTROPENLICENSETERMS`

## <a name = "bkmk_PostInstall"></a>在執行安裝程式的其他步驟

SQL Server 安裝程式完成，不論您所安裝的版本之後，您必須執行下列步驟。 機器學習功能預設未啟用，且必須明確啟用。

1.  安裝完成後，開啟新**查詢**視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行下列命令以啟用功能。
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  您必須明確啟用功能並重新設定。否則，它將無法叫用外部指令碼，即使已安裝的功能。
  
2.  重新啟動 SQL Server 服務重新設定的執行個體。 這樣會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]以及服務。

> [!IMPORTANT]
> 
> 如果您有自訂的安全性設定，或如果您將使用 SQL Server 做為運算環境從遠端用戶端執行 R 或 Python 程式碼時，可能需要一些額外的步驟。 
> 
> 如需詳細資訊，請參閱[升級及安裝常見問題集](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)。
