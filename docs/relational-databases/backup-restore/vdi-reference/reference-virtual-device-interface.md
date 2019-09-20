---
title: 虛擬裝置介面參考
titlesuffix: SQL Server VDI reference
description: 本文提供 SQL Server 備份的虛擬裝置介面參考概觀。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2b4556734044ad5bd688f8d5b286885450897b42
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847149"
---
# <a name="virtual-device-interface-vdi-reference"></a>虛擬裝置介面 (VDI) 參考

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本節包含適用於協力廠商備份軟體廠商所使用的 SQL Server 應用程式設計介面規格。

## <a name="overview"></a>概觀

虛擬裝置介面 (VDI) 提供最高的線上備份輸送量、最低限度的交易工作負載效能降級，以及盡可能最快速的還原時間。 它可讓協力廠商廠商實現 SQL Server 原生備份/還原的相同效能特性，並提供完整範圍的備份/還原功能。 SQL Server 7.0 已引進 VDI，而更新版本則持續支援和增強 VDI。

VDI 支援兩種主要類型的備份技術：

- 傳統的線上備份，其會讀取備份組的整個內容，並將其傳輸至備份媒體。

- 快照集備份，其使用基礎分割鏡像或寫入時複製技術。

透過 VDI 所完成傳統線上備份可以利用 SQL Server 中的完整備份和還原功能。 快照集備份僅限於完整資料庫和檔案/檔案群組備份。 不過，快照集備份可以透過傳統資料庫差異備份、檔案差異備份和交易記錄備份向前復原。

## <a name="next-steps"></a>後續步驟

檢閱本節中的 VDI 參考文件。

下載完整規格和支援的來源檔案：

[SQL Server 2005 虛擬備份裝置介面 (VDI) 規格](https://www.microsoft.com/download/details.aspx?id=17282)