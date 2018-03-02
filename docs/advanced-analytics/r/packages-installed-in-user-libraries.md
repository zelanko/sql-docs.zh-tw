---
title: "避免安裝在使用者程式庫中的 R 封裝上的錯誤 |Microsoft 文件"
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b7f640cc33cb61ab8dffc57edb3b522808129880
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2018
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>避免安裝在使用者程式庫中的 R 封裝上的錯誤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有經驗的 R 使用者通常都會被封鎖或無法使用預設程式庫時，在使用者程式庫安裝 R 封裝。 不過，這個方法不支援在 SQL Server，而且使用者文件庫的安裝通常會結束 「 找不到封裝 」 錯誤。

本文將協助您避免此錯誤的因應措施。 它說明如何修改您的 R 程式碼，並建議的正確 R 封裝安裝程序使用 R 封裝，從 SQL Server 執行個體。

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>為什麼 R 使用者程式庫無法從 SQL Server 存取

R 開發人員需要安裝新的 R 封裝習慣安裝封裝，在每次您的預設程式庫就無法使用，或當開發人員不是在電腦上的系統管理員使用私用，使用者程式庫。

例如，在一般的 R 開發環境，使用者會將封裝的位置 R 環境變數`libPath`，或參考完整的封裝路徑，就像這樣：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

這不會運作，執行 SQL Server 中的 R 解決方案時因為安裝 R 封裝，至特定的預設文件庫的執行個體相關聯。 封裝無法使用時的預設程式庫中，您收到這個錯誤，當您嘗試呼叫封裝：

*Library(xxx) 時發生錯誤： 沒有名為 ' 封裝 name' 的封裝*

## <a name="how-to-avoid-package-not-found-errors"></a>如何避免發生 「 找不到封裝 」 錯誤

+ 排除使用者程式庫的相依性 

    若要安裝必要的 R 封裝至自訂使用者文件庫中，不正確的開發作法是因為若方案由另一個使用者沒有存取程式庫位置執行，它會導致錯誤。

    此外，如果封裝已安裝預設文件庫中，R 執行階段從載入封裝的預設程式庫中，即使您的 R 程式碼中指定不同的版本。

+ 修改您的程式碼在共用環境中執行。

+ 避免安裝封裝，做為方案的一部分。 如果您沒有權限才能安裝封裝，程式碼將會失敗。 即使您沒有權限才能安裝封裝，您應該做因此分別從您想要執行其他程式碼。

+ 檢查您的程式碼，以確保不會呼叫已解除安裝的封裝。

+ 更新您的程式碼，以便移除直接參考的 R 封裝或 R 程式庫路徑。 

+ 了解哪些封裝程式庫是與執行個體相關聯。 如需詳細資訊，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)
