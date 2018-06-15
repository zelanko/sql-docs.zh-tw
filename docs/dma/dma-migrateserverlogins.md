---
title: 移轉 SQL Server 登入 （資料移轉小幫手） |Microsoft 文件
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 23da8fe364ffad914013719f54871e85213befc5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32865453"
---
# <a name="migrating-sql-server-logins-using-data-migration-assistant"></a>使用資料移轉小幫手移轉 SQL Server 登入

本文章提供使用資料移轉小幫手移轉 SQL Server 登入的概觀。 

## <a name="key-concepts"></a>重要概念
以下是重要的概念。

- 您可以移轉 （例如網域使用者或 Windows 網域群組） 的 Windows 主體為基礎的登入。 您也可以移轉 SQL 驗證，也稱為 SQL Server 登入為基礎建立的登入。

- 資料移轉小幫手目前並不支援與獨立安全性憑證 （登入對應到憑證）、 獨立的非對稱金鑰 （登入對應到非對稱金鑰） 和對應到認證的登入相關聯的登入。

- 不會移動資料移轉小幫手**sa**登入與伺服器的原則，以雜湊用雙引號括住的名稱 (\#\#)，這是僅供內部使用。

- 根據預設，資料移轉 Assistatn 選取要移轉所有合格的登入。 或者，您可以選取要移轉的特定登入。 資料移轉小幫手移轉時所有合格的登入，登入使用者對應中保持不變的已移轉的資料庫。 

  如果您打算移轉特定登入，請務必選取對應至一或多個使用者在移轉所選的資料庫中的登入。

- 登入移轉時，資料移轉小幫手也將使用者定義伺服器角色並將伺服器層級權限加入的使用者定義伺服器角色。 角色的擁有者將會設定為**sa**主體。

- 登入移轉的一部分，資料移轉小幫手會指派權限給目標 SQL Server 上的安全性實體存在於來源 SQL Server 上。 

  如果登入已存在於目標 SQL Server 中，資料移轉小幫手移轉指派給安全性實體的權限，並將不會重新建立整個登入。

- 資料移轉小幫手會盡力在登入對應到資料庫使用者，如果目標伺服器上已有登入。

- 建議您檢閱移轉結果，以了解整體的狀態，登入移轉以及移轉後任何建議的動作。

## <a name="resources"></a>資源

[資料移轉小幫手 (DMA)](../dma/dma-overview.md)

[資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)
