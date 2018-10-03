---
title: 移轉 SQL Server 登入，使用 Data Migration Assistant |Microsoft Docs
description: 了解如何移轉 SQL Server 登入，使用 Data Migration Assistant
ms.custom: ''
ms.date: 08/29/2018
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
ms.author: rajpo
manager: craigg
ms.openlocfilehash: e52fdcd55cddea31e317afe04833f5413c006325
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836936"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>移轉 SQL Server 登入，使用 Data Migration Assistant

本文提供使用 Data Migration Assistant 移轉 SQL Server 登入的概觀。 

## <a name="which-logins-are-migrated"></a>移轉的登入

- 您可以移轉 （例如網域使用者或 Windows 網域群組） 的 Windows 主體為基礎的登入。 您也可以移轉建立根據 SQL 驗證，也稱為 SQL Server 登入的登入。

- Data Migration Assistant 目前不支援與獨立安全性憑證 （登入對應到憑證）、 獨立的非對稱金鑰 （對應至非對稱金鑰的登入） 和對應至認證的登入相關聯的登入。

- 不會移動 data Migration Assistant **sa**登入和伺服器名稱加上雙引號的雜湊與原則 (\#\#)，這是僅供內部使用。

- 根據預設，資料移轉小幫手，請選取要移轉所有合格的登入。 或者，您可以選取要移轉的特定登入。 Data Migration Assistant 移轉時所有合格的登入，登入使用者的對應中保持不變的已移轉的資料庫。 

  如果您打算移轉特定登入，請務必選取對應至在選取要移轉的資料庫中的一或多個使用者的登入。

- 登入移轉的一部分，Data Migration Assistant 也將使用者定義伺服器角色並將伺服器層級權限加入的使用者定義伺服器角色。 角色的擁有者將會設定為**sa**主體。

## <a name="during-and-after-migration"></a>在移轉前後和期間

- 登入移轉的一部分，Data Migration Assistant 將指派權限給目標 SQL Server 上的安全性實體存在於來源 SQL Server 上。 

  如果登入已在目標 SQL Server 中，Data Migration Assistant 移轉只指派給安全性實體的權限，不會重新產生整個登入。

- 資料移轉小幫手會盡力將登入對應至資料庫使用者，如果目標伺服器上已經有登入。

- 建議您檢閱移轉的結果，以了解登入移轉及任何建議的移轉後動作的整體狀態。

## <a name="resources"></a>資源

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)
