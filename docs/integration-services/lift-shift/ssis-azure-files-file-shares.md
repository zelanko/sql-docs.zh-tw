---
title: 將檔案儲存至內部部署和 Azure 檔案共用並從中擷取 | Microsoft Docs
description: 本文描述如何透過 SSIS 在內部部署和 Azure 中使用檔案系統和檔案共用
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7fcc0c0f61ce62a2e891d269eea16902ff691080
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="store-and-retrieve-files-on-file-shares-on-premises-and-in-azure-with-ssis"></a>透過 SSIS 將檔案儲存至內部部署和 Azure 檔案共用並從中擷取
本文描述當您將使用本機檔案系統的套件隨即轉移至 Azure 中的 SQL Server Integration Services (SSIS) 時，如何更新 SSIS 套件。

> [!IMPORTANT]
> 目前，SSIS 目錄資料庫 (SSISDB) 僅支援一組存取認證。 因此，Azure-SSIS Integration Runtime (IR) 無法使用不同的認證，來連線到多個內部部署檔案共用和 Azure 檔案服務共用。

## <a name="store-temporary-files"></a>儲存暫存檔案
如果您需要在單一套件執行期間儲存及處理暫存檔案，套件可以使用目前的工作目錄 (`.`) 或 Azure-SSIS Integration Runtime 節點的暫存資料夾 (`%TEMP%`)。

## <a name="store-files-across-multiple-package-executions"></a>在多個套件執行之間儲存檔案
如果您需要儲存及處理永久性檔案，並在多個套件執行之間保存這些檔案，您可以使用內部部署檔案共用或 Azure 檔案服務

### <a name="use-on-premises-file-shares"></a>使用內部部署檔案共用
當您將使用本機檔案系統的套件隨即轉移至 Azure 中的 SSIS 時，若要繼續使用**內部部署檔案共用**，請執行下列動作：
1.  將檔案從本機檔案系統轉送至內部部署檔案共用。
2.  將內部部署檔案共用加入 Azure 虛擬網路 (VNet)。
3.  將您的 Azure-SSIS IR 加入相同的 VNet。 如需詳細資訊，請參閱[將 Azure-SSIS Integration Runtime 加入虛擬網路](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)。
4.  透過設定使用 Windows 驗證的存取認證，將您的 Azure-SSIS IR 連線到相同 VNet 中的內部部署檔案共用。 如需詳細資訊，請參閱[使用 Windows 驗證連線到內部部署資料來源和 Azure 檔案共用](ssis-azure-connect-with-windows-auth.md)。
5.  將您套件中的本機檔案路徑更新為指向內部部署檔案共用的 UNC 路徑。 例如，將 `C:\abc.txt` 更新為 `\\<on-prem-server-name>\<share-name>\abc.txt`。

### <a name="use-azure-file-shares"></a>使用 Azure 檔案共用
當您將使用本機檔案系統的套件隨即轉移至 Azure 中的 SSIS 時，若要使用 **Azure 檔案服務**，請執行下列動作：
1.  將檔案從本機檔案系統轉送至 Azure 檔案服務。 如需詳細資訊，請參閱 [Azure 檔案服務](https://azure.microsoft.com/services/storage/files/)。
2.  透過設定使用 Windows 驗證的存取認證，將您的 Azure-SSIS IR 連線到 Azure 檔案服務。 如需詳細資訊，請參閱[使用 Windows 驗證連線到內部部署資料來源和 Azure 檔案共用](ssis-azure-connect-with-windows-auth.md)。
3.  將您套件中的本機檔案路徑更新為指向 Azure 檔案服務的 UNC 路徑。 例如，將 `C:\abc.txt` 更新為 `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`。
