---
title: 使用 Data Migration Assistant 遷移 SQL Server 登入
description: 瞭解如何使用 Data Migration Assistant 遷移 SQL Server 登入
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.custom: seo-lt-2019
ms.openlocfilehash: 368372ab7324b11e9f7fdaa6af94d5ba2c0534ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056486"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>使用 Data Migration Assistant 遷移 SQL Server 登入

本文概述如何使用 Data Migration Assistant 遷移 SQL Server 登入。

> [!IMPORTANT]
> 本主題適用于涉及 SQL Server 升級至較新版本內部部署產品或在 Azure 虛擬機器上 SQL Server 的案例。

## <a name="which-logins-are-migrated"></a>哪些登入已遷移

- 您可以根據 Windows 主體（例如網域使用者或 Windows 網域群組）來遷移登入。 您也可以遷移根據 SQL 驗證所建立的登入，也稱為 SQL Server 登入。

- Data Migration Assistant 目前不支援與獨立安全性憑證（對應至憑證的登入）相關聯的登入、獨立非對稱金鑰（對應至非對稱金鑰的登入），以及對應至認證的登入。

- Data Migration Assistant 不會使用**** 以雙重雜湊標記（\#\#）括住的名稱來移動 sa 登入和伺服器原則，這僅供內部使用。

- 根據預設，Data Migration Assistant 會選取要遷移的所有合格登入。 （選擇性）您可以選取要遷移的特定登入。 當 Data Migration Assistant 遷移所有合格的登入時，使用者對應在遷移的資料庫中會保持不變。

  如果您打算遷移特定登入，請務必選取對應到所選資料庫中一或多個使用者的登入，以進行遷移。

- 在登入遷移過程中，Data Migration Assistant 也會移動使用者定義的伺服器角色，並將伺服器層級許可權加入至使用者定義的伺服器角色。 角色的擁有者將會設定為**sa**主體。

## <a name="during-and-after-migration"></a>在遷移期間和之後

- 在進行登入遷移的過程中，Data Migration Assistant 會將目標 SQL Server 上的許可權指派給安全性實體，因為它們存在於來源 SQL Server 上。

  如果登入已經存在於目標 SQL Server 上，Data Migration Assistant 只會遷移指派給安全性實體的許可權，而不會重新建立整個登入。

- 如果目標伺服器上已有登入，Data Migration Assistant 可讓您將登入對應至資料庫使用者的最佳做法。

- 建議您檢查遷移結果，以瞭解登入遷移的整體狀態，以及任何建議的後續遷移動作。

## <a name="resources"></a>資源

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Data Migration Assistant：設定](../dma/dma-configurationsettings.md)
