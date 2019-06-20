---
title: 在安裝 SQL Server 更新之後升級 DQS 資料庫結構描述 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: 1ab01928d2e5f4364afe74d9c5e2b6a0a1079e1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66776329"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>在安裝 SQL Server 更新之後升級 DQS 資料庫結構描述

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在之前設定的 DQS 執行個體上安裝 SQL Server 更新 (修補、Hotfix 或累計更新) 之後，您可能必須使用 **upgrade** 命令列參數執行 DQSInstaller.exe 檔案來升級 DQS 資料庫結構描述。 否則，當您嘗試使用 Data Quality Client 連接至資料品質伺服器時，您可能會收到以下錯誤：  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 升級 DQS 資料庫結構描述並不會影響 DQS 資料庫中的現有資料 (知識庫、資料品質專案及 DQS_STAGING_DATA 資料庫中的匯出結果)。 但是，在您升級 DQS 資料庫結構描述之前必須先備份 DQS 資料庫，以免在結構描述升級期間有任何意外的資料遺失狀況。 如需有關備份 DQS 資料庫的詳細資訊，請參閱 [備份及還原 DQS 資料庫](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)。  
  
> [!NOTE]  
>  大部分的 SQL Server 更新都需要升級至 DQS 資料庫結構描述。 如需將需要升級至 DQS 資料庫結構描述之 SQL Server 更新資訊，請參閱圖表中步驟 1.A[升級 DQS:Data Quality Services 上安裝累計更新或 Hotfix 修補](https://go.microsoft.com/fwlink/?LinkID=251565)。  
  
## <a name="prerequisites"></a>先決條件  
  
-   您必須以 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 電腦上 Administrator 群組成員的身分登入。  
  
-   您的 Windows 使用者帳戶必須是安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 之 SQL Server 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
### <a name="to-upgrade-dqs-databases-schema"></a>若要升級 DQS 資料庫結構描述  
  
1.  (建議) 在您繼續升級結構描述之前，請先備份 DQS 資料庫。 如需有關備份 DQS 資料庫的詳細資訊，請參閱 [備份及還原 DQS 資料庫](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)。  
  
2.  啟動 [命令提示字元]。  
  
3.  在命令提示字元中，將目錄變更為 DQSInstaller.exe 所在的位置。 如果已經安裝了 SQL Server 的預設執行個體，DQSInstaller.exe 檔會位於 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn。  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  在命令提示字元中輸入下列命令，然後按 ENTER：  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  安裝程式會提示您先備份 DQS 資料庫後再繼續。 如果您已經備份 DQS 資料庫，請輸入 **Y** 或 **Yes** 然後按 ENTER 繼續升級。  
  
6.  在成功升級 DQS 資料庫結構描述之後，將會顯示完成訊息。  
  
## <a name="next-steps"></a>後續步驟  
 從 Data Quality Client 應用程式登入已升級的資料品質伺服器。  
  
 如需有關升級 DQS 資料庫結構描述，SQL Server 安裝完成後的更新及相關疑難排解步驟，請參閱[升級 DQS:Data Quality Services 上安裝累計更新或 Hotfix 修補](https://go.microsoft.com/fwlink/?LinkID=251565)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [在 .NET Framework 更新之後升級 SQLCLR 組件](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
