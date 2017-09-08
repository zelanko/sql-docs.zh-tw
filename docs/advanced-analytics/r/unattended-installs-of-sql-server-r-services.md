---
title: "自動的安裝的機器學習服務 |Microsoft 文件"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: babb74aa866404853cfef83e1d30159354f385e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>自動的安裝的機器學習服務 （資料庫）

本主題描述如何安裝資料庫引擎，以無訊息模式執行個體中的機器學習中使用 SQL Server 安裝程式命令列引數。 在自動安裝中，您可以不使用安裝精靈 」 的互動式功能，而且必須提供才能完成安裝，包括授權合約適用於 SQL Server 和機器學習元件所需的所有引數。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （資料庫）

> [!IMPORTANT]
> 
> 在 SQL Server 2016 和 SQL Server 2017，若要啟用此功能安裝完成之後，不需要額外的步驟。 這些包括重新設定，然後重新啟動執行個體。 請務必檢閱所有步驟。

## <a name="prerequisites"></a>必要條件

+ 您必須在您將在其中使用機器學習服務每個執行個體上安裝資料庫引擎。

+ 如果電腦沒有網際網路存取，請務必安裝機器事先學習元件的安裝程式。 如需下載位置，請參閱[安裝沒有網際網路存取的機器學習元件](../../advanced-analytics/r/installing-ml-components-without-internet-access.md)。

+ 有新授權相關聯的 R，並將 Python 開放原始碼元件的參數。 您必須接受授權條款，您所安裝的每種語言，個別引數。 如果您沒有在命令列中包含此參數，安裝程式將會失敗。

+ 若要完成安裝程式，而不需要回應提示，請確定您已識別所有必要的引數，包括授權，以及任何其他您可能想要安裝的功能。

> [!NOTE] 
> 最早的版本中需要支援 SQL 登入的混合的安全性模式。 不過，您可以考慮啟用混合模式驗證，以支援使用 SQL 登入的資料科學家所開發的解決方案。

## <a name="bkmk_NewInstall"></a>自動的安裝的機器學習服務，以 R

下列範例所示**最小**執行無訊息方式，自動安裝時，在命令列中指定必要的功能安裝的 SQL Server 2017 機器服務 （資料庫）。

1. 開啟提升權限的命令提示字元中，並執行下列命令：

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    
    請注意在 SQL Server 2017 R 所需的旗標： `ADVANCEDANALYTICS`， `SQL_INST_MR`，和`IACCEPTROPENLICENSETERMS`。
2. 重新啟動伺服器。
3. 執行後續安裝設定步驟中所述[本節](#bkmk_PostInstall)。 另一個 SQL Server 服務重新啟動將會需要。

## <a name="OldInstall"></a>自動的安裝的 R 服務 （資料庫）
 
 下列範例所示**最小**安裝的 SQL Server 2016 R Services 的執行無訊息方式，自動安裝時，在命令列中指定必要的功能。

1. 開啟提升權限的命令提示字元中，並執行下列命令：

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    請注意 2016 R 服務所需的旗標：`ADVANCEDANALYTICS`和`IACCEPTROPENLICENSETERMS`。
2. 重新啟動伺服器。
3. 執行後續安裝設定步驟中所述[本節](#bkmk_PostInstall)。 另一個 SQL Server 服務重新啟動將會需要。

## <a name = "bkmk_PostInstall"></a>在執行安裝程式的其他步驟

1.  安裝完成後，開啟新**查詢**視窗[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後執行下列命令以啟用功能。
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  您必須明確啟用功能並重新設定。否則，它將無法叫用外部指令碼，即使已安裝的功能。
  
2.  重新啟動 SQL Server 服務重新設定的執行個體。 這樣會自動重新啟動相關[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]以及服務。

3. 如果您有自訂安全性設定，或您將使用 SQL Server 支援遠端計算內容，則可能需要額外的步驟。 如需詳細資訊，請參閱[升級及安裝常見問題集](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)。

