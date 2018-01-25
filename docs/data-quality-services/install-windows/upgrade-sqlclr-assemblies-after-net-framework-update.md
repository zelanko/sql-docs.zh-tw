---
title: "在 .NET Framework 更新之後升級 SQLCLR 組件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b1a008cc-7e6b-4655-a869-bd429f986400
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f234417f1e1148a0edce88df46835f63ef22625
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="upgrade-sqlclr-assemblies-after-net-framework-update"></a>在 .NET Framework 更新之後升級 SQLCLR 組件
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 是參考 Microsoft .NET Framework 4 組件的 SQL Common Language Runtime (SQLCR) 常式集合。 如果您在電腦上安裝任何會影響這類參考 .NET Framework 組件的 .NET Framework 更新，則會導致全域組件快取 (GAC) 中組件的模組版本 ID (MVID) 發生變更。 這樣會造成 GAC 中所參考組件的 MVID 與 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中組件的 MVID 不相符。  
  
 如果 .NET Framework 更新需要您重新啟動 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 電腦，會自動升級受影響的 SQLCLR 組件，以修正重新啟動 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 電腦時的 MVID 不相符問題。 不過，若是不需要您重新啟動 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 電腦的 .NET Framework 更新，則會發生錯誤，因為當您嘗試使用 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 連接至 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]時，會造成組件的 MVID 不相符：  
  
```  
A new version of .NET was installed on this machine. In order to continue to work with DQS please run dqsinstaller.exe –upgradedlls.  
```  
  
 若要修正此問題，則必須升級 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中受影響的 SQLCLR 組件。 您可以透過使用 **upgradedlls** 命令列參數執行 DQSInstaller.exe 檔的方式略過重新建立 DQS 資料庫，而只升級受影響的組件。 這樣可確保您的知識庫、資料品質專案以及 DQS 中的任何其他資料都會保留下來。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   您必須以 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 電腦上 Administrator 群組成員的身分登入。  
  
-   您的 Windows 使用者帳戶必須是安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 之 SQL Server 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
### <a name="to-upgrade-sqlclr-assemblies"></a>升級 SQLCLR 組件  
  
1.  啟動 [命令提示字元]。  
  
2.  在命令提示字元中，將目錄變更為 DQSInstaller.exe 所在的位置。 如果已經安裝了 SQL Server 的預設執行個體，DQSInstaller.exe 檔會位於 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn。  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  在命令提示字元中輸入下列命令，然後按 ENTER：  
  
    ```  
    dqsinstaller.exe -upgradedlls  
    ```  
  
4.  其餘步驟與 [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer) 的 [從開始畫面、開始功能表或 Windows 檔案總管執行 DQSInstaller.exe](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)一節中的步驟 2-6 相同。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [在安裝 SQL Server 更新之後升級 DQS 資料庫結構描述](../../data-quality-services/install-windows/upgrade-dqs-databases-schema-after-installing-sql-server-update.md)  
  
  
