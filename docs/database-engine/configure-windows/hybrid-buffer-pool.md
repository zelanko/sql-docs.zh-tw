---
title: 混合式緩衝集區 | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.openlocfilehash: a8098c38b72ba44ab973fe5564b93740252bafc6
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560305"
---
# <a name="hybrid-buffer-pool"></a>混合式緩衝集區
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在 SQL Server 2019 CTP 2.1 中，SQL Server 資料庫引擎引進了一項新功能，可讓它直接存取持續性記憶體 (PMEM) 裝置中所儲存資料庫檔案的資料頁。 

在沒有持續性記憶體的傳統系統中，SQL Server 會在緩衝集區中快取資料頁。 透過混合式緩衝集區，SQL Server 會略過將分頁複製到緩衝集區中以 DRAM 為基礎部分的作業，而改為直接參考位於 PMEM 裝置上的資料庫檔案分頁。 存取混合式緩衝集區中位於 PMEM 的資料檔案是使用記憶體對應 I/O 執行，也稱為啟用檔案 (enlightenment)。

只有完整分頁才能直接在 PMEM 裝置上參考。 當分頁變成中途分頁時，它會保留在 DRAM 中，並在最終寫回 PMEM 裝置。

Windows 和 Linux 都提供這個功能。

## <a name="enable-hybrid-buffer-pool"></a>啟用混合式緩衝集區

在 CTP 2.1 上，您必須啟用啟動追蹤旗標 809，才能使用混合式緩衝集區。

## <a name="best-practices-for-hybrid-buffer-pool"></a>混合式緩衝集區的最佳做法

* 在 Windows 上格式化 PMEM 裝置時，請使用可用於 NTFS 的最大配置單位大小 (在 Windows Server 2019 為 2 MB) ，並確定裝置已啟用 DAX (DirectAccess)
  