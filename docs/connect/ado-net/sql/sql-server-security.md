---
title: SQL Server 安全性
description: 提供 SQL Server 安全性功能的概觀及應用程式案例，適用於建立以 SQL Server 為目標的安全 ADO.NET 應用程式。
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: bb9e02743122958cb567e01f5011fc9f8b3481e6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452002"
---
# <a name="sql-server-security"></a>SQL Server 安全性

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 具有許多功能，可支援安全資料庫應用程式的建立。  
  
資料竊取或破壞等一般的安全性考量，則適用於所使用的 SQL Server 版本。 資料完整性也應該視為安全性問題。 如果資料未受到保護，可能會因為特定的資料操作已被允許，且資料不小心或惡意地修改了不正確的值或整個刪除，而變成不萬能。 此外，通常必須遵守法律需求，例如機密資訊的正確儲存。 儲存某些類型的個人資料會完全禁止，這取決於特定管轄區中的法律。  
  
每個 SQL Server 版本和每個 Windows 版本一樣，都具有不同的安全性功能，而越新的版本功能越強。 請務必瞭解，安全性功能本身無法保證安全的資料庫應用程式。 每個資料庫應用程式在其需求、執行環境、部署模型、實體位置和使用者群體中都是唯一的。 部分在範圍中的應用程式可能只需要最少的安全性，而透過網際網路部署的其他本機應用程式或應用程式則可能需要嚴格的安全性措施，以及進行中的監視和評估。  
  
您應該在設計階段就考量 SQL Server 資料庫應用程式的安全性需求，而不是事後才加以考量。 及早在開發週期中評估威脅，可讓您在偵測到弱點的任何地方，減輕潛在損害的機會。  
  
即使應用程式的初始設計是音效，隨著系統的發展，新威脅可能會出現。 藉由建立多個資料庫的防線，您可以將安全性缺口所造成的損害降到最低。 您的第一道防線是要減少受攻擊面的範圍，不要授與絕對必要的許可權。  
  
本節中的主題簡要說明與開發人員相關的 SQL Server 安全性功能，並提供連結至《SQL Server 線上叢書》中相關主題的連結，以及提供更深入探討的其他資源。  
  
## <a name="in-this-section"></a>本節內容  
[在 SQL Server 中進行驗證](authentication-sql-server.md)  
描述 SQL Server 中的登入和驗證，並提供其他資源的連結。 
  
[SQL Server 中的應用程式安全性案例](application-security-scenarios-sql-server.md)  
包含討論 ADO.NET 和 SQL Server 應用程式之各種應用程式安全性案例的主題。  
  
[SQL Server Express 安全性](sql-server-express-security.md)  
說明 SQL Server Express 的安全性考量。  
  
## <a name="related-sections"></a>相關章節  
[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
說明 SQL Server 和 Azure SQL Database 的安全性考慮。

[SQL Server 安裝的安全性考量](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
說明安裝 SQL Server 之前要考慮的安全性考慮。

## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
