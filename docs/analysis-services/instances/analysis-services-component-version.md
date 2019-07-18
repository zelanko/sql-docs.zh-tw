---
title: 確認 SQL Server Analysis Services 累積更新組建版本 |Microsoft Docs
ms.date: 07/11/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1da8384bb51360178e1735d13f6c6b706e8b7ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659055"
---
# <a name="verify-analysis-services-cumulative-update-build-version"></a>驗證 Analysis Services 累積更新組建版本

從 SQL Server 2017 開始，SQL Server Database Engine 組建版本號碼與 Analysis Services 組建版本號碼不相符。 雖然 Analysis Services 和 Database Engine 使用相同的安裝程式，建置系統每次使用是分開的。

 在某些情況下，可能必須驗證已套用累計更新 (CU) 建置套件，並已更新 Analysis Services 元件。 您可以藉由比較您電腦上安裝的組建版本號碼與特定的 cu Analysis Services 元件檔的組建版本號碼進行驗證。

## <a name="verify-component-file-version"></a>驗證元件檔案版本

若要確認元件檔案版本， 

1. 移至[SQL Server 2017 組建版本](https://support.microsoft.com/help/4047329)。 
2. 在  **SQL Server 2017 累積更新 (CU) 建置**，按一下**知識庫編號**您想要確認組建。
3. 在 **累積更新 （#） SQL Server 2017**文章，在**累計更新封裝資訊**區段中，展開**累計更新套件檔案資訊**.
4. 在  **SQL Server 2017 Analysis Services**資料表中，檢查檔案的版本，如**msmdsrv.exe**元件檔案。 如果已套用的 CU，檔案版本號碼應符合 msmdsrv.exe 檔案安裝在您的電腦上。

## <a name="see-also"></a>另請參閱  

[安裝 SQL Server 服務更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)  

[Microsoft SQL server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx)
  
  
