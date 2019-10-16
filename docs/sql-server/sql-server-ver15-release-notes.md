---
title: SQL Server 2019 版本資訊 | Microsoft Docs
ms.date: 10/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 9b6895abfa0b09459911eba03b52837379f2d162
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041195"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 預覽版版本資訊
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此文章說明 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的限制與已知問題。 如需相關資訊，請參閱：

>[SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)

>[!NOTE]
>該內容是針對 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候選版所發行。 候選版是預先發行的軟體。 此資訊可能會有所變更。 如需支援情節的詳細資訊，請參閱[支援](#support)。

## <a name="includesql-server-2019includessssqlv15-mdmd-release-candidate-rc"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候選版 (RC)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 最新的公開版本。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 只提供評估版。 沒有其他可用版本。

如需適用於候選版的支援與授權的完整詳細資料，請參閱您安裝媒體隨附的 `license_Eval.rtf`。

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>文件集

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 的文件有所限制，且內容會隨附於 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文件集。 文中專門針對 SQL Server 2019 (15.x) 的內容會以**適用於**來標示。

- **問題和對客戶的影響**：可以依版本篩選 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件。 使用每個文件頁面左上方控制項來篩選您的需求。

- **問題和對客戶的影響**︰SQL Server 2019 (15.x) 未提供任何離線內容。

## <a name="build-number"></a>組建編號

Windows、Linux 和容器上的 SQL Server 2019 RC 組建編號為 `15.0.1900.25`。  巨量資料叢集中使用的 SQL Server 2019 RC 組建編號為 `15.0.1900.47`。

## <a name="hardware-and-software-requirements"></a>硬體和軟體需求

- **問題和對客戶的影響**︰仍然會檢閱硬體和軟體需求，而且不是產品版本的最終需求。

  - **硬體**
    - [Windows - 處理器、記憶體和作業系統需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系統需求](../linux/sql-server-linux-setup.md#system)
  - **軟體**
    - Windows Server 2016 或更新版本。 如需其他需求，請參閱[安裝 SQL Server 的需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2。 可從[下載中心](https://www.microsoft.com/download/details.aspx?id=53344)取得。
    - 針對 Linux，請參閱 [Linux - 支援的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name="sql-server-installation-may-fail-if-ssms-18x-is-installed"></a>如果已安裝 SSMS 18.x，SQL Server 安裝可能會失敗

- **問題與對客戶的影響**：當依序進行下列安裝時，[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 安裝失敗：
  1. 在伺服器上安裝 SQL Server Management Studio (SSMS) 18.0、18.1、18.2 或 18.3 版。
  1. 嘗試從抽取式媒體進行 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 安裝。 例如，安裝媒體是 DVD。

- **因應措施**：
  1. 解除安裝比 SSMS 18.3.1 舊的任何版本。
  1. 安裝比 SSMS (18.3.1 或更新版本) 新的任何版本。 如需最新版本，請參閱[下載 SSMS](../ssms/download-sql-server-management-studio-ssms.md)。
  1. 以正常方式安裝 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]。

  >[!NOTE]
  >需要解除安裝。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 候選版。

## <a name="updated-compiler"></a>更新的編譯器

- **問題和對客戶的影響**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 是以更新的編譯器所建置。 CTP 2.1 有個已知的問題，由於更新編譯器的緣故，浮點數和其他轉換案例可能傳回與舊版不同的值。 CTP 2.2 內含可確保受影響案例傳回與舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 相同結果的運作。 截至候選版為止已無任何已知問題。 如果發現與 [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] 相較之下有任何結果異常，請立即回報 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 小組](https://aka.ms/sqlfeedback)。

- **因應措施**：不適用

- **適用於**：候選版

## <a name="installation-wizard-may-wait-between-eula-pages"></a>安裝精靈可能會在使用者授權合約頁面之間等待

- **問題和對客戶的影響**︰在安裝精靈安裝期間，處理序可能會在 R 服務的使用者授權合約 (EULA) 與 Python 的 EULA 之間等待很長時間。

- **因應措施**：等候安裝精靈繼續。 等待的時間可能會超過 30 分鐘。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0

## <a name="utf-8-collations"></a>UTF-8 定序

- **問題和對客戶的影響**︰啟用 UTF-8 的定序不能與某些其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能搭配使用。 使用下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能時不支援 UTF-8：

  - 記憶體內部 OLTP
  - PolyBase 的外部資料表 ([!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - Always Encrypted (最高至 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - 連結的伺服器 (最高至 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2)

  > [!Note]
  > 在 Azure Data Studio 或 SQL Server Data Tools (SSDT) 中，目前沒有可選擇啟用 UTF-8 之定序的 UI 支援。 最新 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) 18 版支援在 UI 中選擇啟用 UTF-8 的定序。
 
- **因應措施**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 沒有任何因應措施。


- **適用於**：所有 CTP 版本。

## <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

- **問題和對客戶的影響**︰豐富計算功能會造成效能最佳化及錯誤處理增強功能的表現下降。目前的預設值為停用。

- **因應措施**：若要啟用豐富計算，請執行 `DBCC traceon(127,-1)`。 如需詳細資料，請參閱[啟用豐富計算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2、CTP 3.1

## <a name="sql-server-configuration-manager-may-not-start"></a>SQL Server 組態管理員可能不會啟動

- **問題和對客戶的影響**︰若沒有 VCRuntime 140 (VCRUNTIME140.dll) 檔案，則不會啟動電腦上的 SQL Server 組態管理員 (SSCM)。 使用者可能會在啟動 SSCM 時見到下列對話方塊： 


  `MMC could not create the snap-in. The snap-in might not have been installed correctly.`

- **因應措施**：安裝最新的 VC 執行階段 2013 (x86)：

  - [Verbose](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
  - [直接](https://support.microsoft.com/help/4032938/update-for-visual-c-2013-redistributable-package)

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.1、CTP 3.0、CTP 2.5。

## <a name="always-on-availability-group-kubernetes-operator-not-supported"></a>不支援 Always On 可用性群組的 Kubernetes 運算子

- **問題和對客戶的影響**︰此候選版中不支援 Always On 可用性群組的 Kubernetes 運算子，而且在 RTM 中也不會提供。 

- **因應措施**：None

- **適用於**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 候選版

## <a name="master-data-service-notification-email-contains-broken-link"></a>Master Data Service 通知電子郵件包含中斷的連結

- **問題和對客戶的影響**︰來自 Master Data Services (MDS) 的通知電子郵件包含中斷的連結。 此連結會巡覽至傳回錯誤的頁面，如下列訊息所示：

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **因應措施**：開啟 MDS 入口網站，並手動移至資源。

- **適用於**：SQL Server 2019 候選版。

## <a name="machine-learning-services"></a>機器學習服務

如需 SQL Server Microsoft 機器學習服務中的問題，請參閱 [SQL Server Microsoft 機器學習服務機器學習服務中的已知問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
