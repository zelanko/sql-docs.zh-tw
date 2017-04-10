---
title: "佈建 R Server Only SQL Server 2016 Enterprise VM on Azure | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# 佈建 R Server Only SQL Server 2016 Enterprise VM on Azure

R Server Only SQL Server 2016 Enterprise Virtual Machine on Azure 是一個新的選項，可以快速且輕鬆地設定伺服器環境以便支援 R 方案。 此 Azure 虛擬機器已預先設定 Microsoft R Server (Standalone)。 

這個新的虛擬機器會取代 Azure Marketplace 中先前提供的 RRE for Windows Virtual Machine。 

此虛擬機器也包含 DeployR Enterprise，可以在應用程式與後端系統內部署 R 分析。 如需詳細資訊，請參閱[關於 Deploy R](https://msdn.microsoft.com/microsoft-r/deployr-about)。


## 佈建 R Server 虛擬機器

如果您剛開始使用 Azure VM，我們建議您閱讀這篇文章，以取得使用入口網站並設定虛擬機器的詳細資訊。
[虛擬機器 - 快速入門](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

從 Microsoft Azure Marketplace 建立 R Server VM 
1. 按一下 [虛擬機器]，然後在 [搜尋] 方塊中，輸入 [R Server]。
2. 選取 **R Server Only SQL Server 2016 Enterprise**
3. 如這篇文章中所述，繼續佈建虛擬機器︰[https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 
7. VM 已建立並在執行之後，按一下 [連接] 按鈕以開啟連線並登入新電腦。
8. 當您連線時，依預設會開啟伺服器管理員，但不需要其他伺服器設定。 關閉伺服器管理員移至桌面，並繼續執行接下來的步驟︰
    + 安裝其他 R 工具或開發工具
    + 設定 DeployR  

在 Azure 傳統入口網站中找出 R Server VM
1. 按一下 [虛擬機器]，然後按一下 [新增]。
2. 在 [新增] 窗格中，應該已選取 [計算] 和 [虛擬機器]。 
3. 按一下 [從組件庫] 尋找 VM 映像。 您可以在搜尋方塊中輸入 [R Server] 或按一下 [Microsoft] 然後向下捲動，直到您看到 [R Server Only SQL Server 2016 Enterprise]。


## 安裝 R 工具
根據預設，Microsoft R Server 包含所有已安裝的 R 工具，以及 R 的基本安裝，包括 RTerm 和 RGui。 如果您想要立即開始使用 R，在桌面上已經新增 RGui 的捷徑。

不過，您可能想要安裝其他 R 工具，例如 RStudio、R Tools for Visual Studio 或 Microsoft R Client。 請參閱下列連結，以取得下載位置和指示︰
+ [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

您安裝這些工具之後，請務必將工具指向 R Server 程式庫。

## 在虛擬機器上使用 DeployR

需要一些額外的步驟才能使用此 VM 上安裝的 DeployR 執行個體。 

設定 DeployR 執行個體︰

1. 在 VM 上開啟 [DeployR 系統管理員公用程式]。
2. 如此處所述，設定 DeployR 系統管理員密碼︰[後續安裝步驟](https://msdn.microsoft.com/microsoft-r/deployr-install-on-windows)
3. 設定 DeployR Web 內容。 如需詳細資訊，請參閱 [DeployR Admin Installation in the Cloud](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud) (在雲端安裝 DeployR 系統管理員) 
4. 如此處所述，在 VM 上開啟適當連接埠︰[設定 Azure 端點](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#configuring-azure-endpoints) 
4. 如此處所述，更新 Windows 防火牆︰[更新防火牆](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#updating-the-firewall) 

## 存取 Azure 儲存體帳戶中的資料 

當您需要使用 Azure 儲存體帳戶中的資料時，有幾個選項可以存取或移動資料︰


+ 使用公用程式，例如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)，將資料從儲存體帳戶複製到本機檔案系統。 

+ 將檔案新增至儲存體帳戶上的檔案共用，然後將檔案共用掛接為 VM 上的網路磁碟機。  如需詳細資訊，請參閱[掛接 Azure 檔案](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

## 使用 Azure Data Lake Storage (ADLS) 帳戶中的資料

如果您參考儲存體帳戶的方式與 HDFS 檔案系統相同，但是使用 webHDFS，您可以使用 ScaleR 從 ADLS 儲存體讀取資料。  如需詳細資訊，請參閱此[安裝指南](http://go.microsoft.com/fwlink/?LinkId=723452)。

## 資源

Microsoft R 相關文件位於 MSDSN 程式庫︰[R Server 和 Scale R](https://msdn.microsoft.com/microsoft-r)  


請參閱這些額外的資源以了解 R 的一般資訊︰ 
+ [DataCamp](http://www.datacamp.com) 提供 R 的免費簡介和中繼課程，以及使用 Revolution R 處理巨量資料的課程。
+ [Stack Overflow](http://www.stackoverflow.com) R 程式設計和 ML 工具問題的絕佳資源。 
+ [Cross Validated](https://stats.stackexchange.com/) 關於機器學習中的統計問題的網站。
+ [R Help 郵寄清單封存](https://www.r-project.org/mail.html) 歷程記錄資訊的絕佳資源。 
+ [MRAN 網站](https://mran.microsoft.com/documents/getting-started/) 許多其他 R 資源。  

## 另請參閱
[SQL Server R 服務](https://msdn.microsoft.com/library/mt604845.aspx)
