---
title: 遠端 Blob 存放區 (RBS) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4379e0ff3ca534acd6ae130cbdf0f8acd2b6a81f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66009853"
---
# <a name="remote-blob-store-rbs-sql-server"></a>遠端 Blob 存放區 (RBS) (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遠端 BLOB 存放區 (RBS) 是選用的附加元件，可讓資料庫管理員在商品儲存方案中儲存二進位大型物件，而不是直接儲存在主要資料庫伺服器上。  
  
 RBS 包含在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝媒體中，但不會由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝。  
  
 如需 RBS 的詳細資訊，請參閱本主題中的 [RBS 資源](#rbsresources)。  
  
## <a name="benefits-of-rbs"></a>RBS 的優點  
 RBS 提供下列優點：  
  
### <a name="optimized-database-storage-and-performance"></a>最佳化的資料庫儲存和效能  
 將 BLOB 儲存在資料庫中可能會耗用大量的檔案空間以及昂貴的伺服器資源。 RBS 會將 BLOB 有效率地傳輸到您所選擇的專用儲存方案，並將其參考儲存在資料庫中。 這樣會為結構化的資料釋放伺服器儲存空間，並為資料庫作業釋放伺服器資源。  
  
### <a name="efficient-management-of-blobs"></a>有效率的 BLOB 管理  
 數個 RBS 功能都支援方便管理已儲存的 BLOB：  
  
-   BLOB 使用 ACID (不可部分完成、一致、隔離、持久) 交易進行管理。  
  
-   BLOB 會組織成集合。  
  
-   記憶體回收、一致性檢查，以及其他維護功能都包含在內。  
  
### <a name="standardized-api"></a>標準化的 API  
 RBS 會定義一組 API 來為應用程式提供標準化程式撰寫模型，以存取及修改任何 BLOB 存放區。 每一個 BLOB 存放區都可以指定它自己的提供者程式庫 (該程式庫會外掛到 RBS 用戶端程式庫)，並指定要如何儲存及存取 BLOB。  
  
 有好幾個協力廠商儲存方案廠商已經開發了符合這些標準 API，並在多種儲存平台上支援 BLOB 儲存的 RBS 提供者。  
  
## <a name="rbs-requirements"></a>RBS 需求  
 RBS 在儲存 BLOB 中繼資料所在的主要資料庫伺服器中，需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise。 不過，如果您使用提供的 FILESTREAM 提供者，可以將 BLOB 本身儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard 上。  
  
 RBS 包含一個 FILESTREAM 提供者，可讓您使用 RBS，將 BLOB 儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體上。 如果您要使用 RBS 將 BLOB 儲存在不同的儲存方案中，您必須使用針對該儲存方案開發的 RBS 提供者，或使用 RBS API 開發一個自訂的 RBS 提供者。 將 BLOB 儲存在 NTFS 檔案系統中的範例提供者，在 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190)上作為學習資源提供。  
  
## <a name="rbs-security"></a>RBS 安全性  
 當您使用自訂提供者將 BLOB 儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部時，可以提供給略過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性系統的其他處理序使用。 請確認您會使用適合自訂提供者使用之儲存媒體的權限和加密選項，保護已儲存的 BLOB。  
  
##  <a name="rbsresources"></a> RBS 資源  
 **RBS 文件集**  
 RBS 文件集包含在 Windows Installer 套件中。 如果您要在不安裝 RBS 的情況下檢閱 RBS 文件集，則可以在 [MSDN Library 中線上](https://go.microsoft.com/fwlink/?LinkId=210192)檢視該文件集的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本。  
  
 **RBS 技術白皮書**  
 [遠端 BLOB 儲存](https://go.microsoft.com/fwlink/?LinkId=210422)技術白皮書是可下載的 Microsoft Word 文件，這個技術白皮書提供有關安裝與設定 RBS 的詳細資訊。  
  
 **RBS 範例**  
 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) 上提供的 RBS 範例會示範如何開發 RBS 應用程式，以及如何開發與安裝自訂的 RBS 提供者。  
  
 **RBS 部落格**  
 [RBS 部落格](https://go.microsoft.com/fwlink/?LinkId=210315) 會提供其他資訊來協助您了解、部署，以及維護 RBS。  
  
  
