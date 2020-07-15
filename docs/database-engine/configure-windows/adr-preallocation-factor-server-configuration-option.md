---
title: ADR Preallocation Factor 組態選項 | Microsoft Docs
description: 說明適用於 ADR Preallocation Factor 的 SQL Server 執行個體組態設定。
ms.custom: ''
ms.date: 06/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ADR Preallocation Factor
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4e53c7c9d0d128c1697a301fc013469f5ac34c00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85698179"
---
# <a name="adr-preallocation-factor-configuration-option"></a>ADR Preallocation Factor 組態選項

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在 SQL Server 2019 中引進。

這是[加速資料庫復原](../../relational-databases/accelerated-database-recovery-concepts.md)所需的組態設定。

加速資料庫復原 (ADR) 會維護資料的版本，以供復原之用。 這些版本是在各種資料操作語言 (DML) 的作業中產生。 版本會儲存在稱為持續版本存放區 (PVS) 的內部資料表中。 

## <a name="remarks"></a>備註  

如果將 PVS 資料表的分頁配置為前景使用者 DML 作業的一部分，則效能可能會降低。 為了解決這個問題，有一個背景執行緒會預先配置分頁，並讓這些分頁立即可供 DML 交易使用。 當背景執行緒預先配置足夠的分頁，且前景 PVS 配置的百分比接近 0 時，效能最佳。 如果百分比很高且會影響效能，則錯誤記錄檔就會包含標籤為 `PreallocatePVS` 的項目。

背景執行緒預先配置的分頁數目是以各種工作負載啟發式項目為基礎，但主要是以 512 個分頁的區塊來配置頁面。 ADR 預先配置因數是區塊的倍數。 根據預設，此因數為 4。 這表示此功能會在需要時一次預先配置 2048 個分頁。 

雖然背景執行緒會考慮工作負載模式，但如果有需要，也可以增加此因數來改善效能。

> [!CAUTION]
> 如果 PVS 預先配置增加太多，則會與系統中的其他配置競爭，因此實際上可能會降低整體效能
>
> 修改此設定之前，請先測試系統的整體效能。

## <a name="examples"></a>範例  

下列範例會將預先配置因數設定為 4。

```tsql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO 
sp_configure 'ADR Preallocation Factor', 4;
RECONFIGURE;
GO
```

## <a name="see-also"></a>另請參閱  

- [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [加速資料庫復原](../../relational-databases/accelerated-database-recovery-concepts.md)
- [管理加速資料庫復原](../../relational-databases/accelerated-database-recovery-management.md)