---
title: "避免安裝在使用者程式庫中的 R 封裝上的錯誤 |Microsoft 文件"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0de06ebee16d903b4b00c9d8e4673bf450c485d1
ms.contentlocale: zh-tw
ms.lasthandoff: 10/10/2017

---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>避免安裝在使用者程式庫中的 R 封裝上的錯誤

有經驗的 R 使用者通常都會被封鎖或無法使用預設程式庫時，在使用者程式庫安裝 R 封裝。 不過，這個方法不支援在 SQL Server，而且使用者文件庫的安裝通常會結束 「 找不到封裝 」 錯誤。

本主題提供協助您避免此錯誤的因應措施。 它說明如何修改您的 R 程式碼，並建議的正確 R 封裝安裝程序使用 R 封裝，從 SQL Server 執行個體。

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>為什麼 R 使用者程式庫無法從 SQL Server 存取

R 開發人員需要安裝新的 R 封裝習慣安裝套件在和使用私用的使用者程式庫時的預設程式庫就無法使用，或當開發人員不是在電腦上的系統管理員。

例如，在一般的 R 開發環境，使用者會將封裝的位置 R 環境變數`libPath`，或參考完整的封裝路徑，就像這樣：

```R
library("c:/Users/<username>/R/win-library/packagename")  
```

不過，這可以永遠不會運作，SQL Server 中執行 R 解決方案時因為安裝 R 封裝，至特定的預設文件庫的執行個體相關聯。

如果封裝並未安裝於預設程式庫中，您可能會在嘗試呼叫封裝時發生這個錯誤：

*Library(xxx) 時發生錯誤： 沒有名為 ' 封裝 name' 的封裝*

也不正確的開發做法是必要的 R 封裝安裝至自訂使用者文件庫，因為如果沒有存取程式庫位置的另一個使用者所執行的方案，它會導致錯誤。

## <a name="how-to-install-r-packages-to-an-accessible-library"></a>如何安裝 R 封裝至可存取的文件庫

**適用於 SQL Server 2016**

使用執行個體相關聯的套件程式庫。 如需詳細資訊，請參閱[與 SQL Server 一起安裝的 R 封裝](installing-and-managing-r-packages.md)

**適用於 SQL Server 2017**

SQL Server 提供功能，可協助您管理多個封裝版本，並提供使用者的權限給個別的封裝，而不需要使用者具有檔案系統存取權。

如需如何設定共用的封裝程式庫，並將使用者指派給角色的詳細資訊，請參閱[for SQL Server 的 R 封裝管理](r-package-management-for-sql-server-r-services.md)。

如果您採用資料庫角色為基礎的封裝管理方法時，它不需要在不同的使用者目錄中安裝多份相同的封裝。 安裝的封裝，您需要然後與已驗證的使用者共用單一的複本。 因為封裝在資料庫層級進行管理，您也可以複製的封裝和資料庫之間的相關權限的群組。

## <a name="tips-for-avoiding-package-not-found-errors"></a>避免 「 找不到封裝 」 錯誤的秘訣

+ 修改程式碼以消除對使用者程式庫相依性。 當您移轉至執行的 R 解決方案[!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)]，很重要，您執行下列動作：

    + 執行個體相關聯的預設程式庫安裝您所需要的任何套件。

    + 編輯程式碼，以確保封裝會從預設程式庫，不是從特定的目錄或使用者程式庫載入。

+ 避免臨機操作的套件安裝做為方案的一部分。 請檢查您的程式碼，以確保沒有解除安裝的封裝，或使用動態地將封裝安裝的程式碼呼叫。 如果您沒有權限，程式碼會失敗，且如果您沒有權限，您應該安裝封裝分開從其他您想要執行的程式碼。

+ 修改 R 封裝程式庫的任何直接路徑。 如果已將封裝安裝於預設程式庫中，R 執行階段將從預設程式庫載入封裝，即使已在 R 程式碼中指定不同的程式庫也一樣。

