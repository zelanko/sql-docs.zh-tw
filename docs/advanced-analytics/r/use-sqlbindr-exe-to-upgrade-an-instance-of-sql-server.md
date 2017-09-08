---
title: "升級 SQL Server 執行個體中的機器學習元件 |Microsoft 文件"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9d7ddd95bdbcf6efca98ed94bc305924902b98
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>升級 SQL Server 執行個體中的機器學習元件

Microsoft 機器學習 Server for Windows 包含一個工具，您可以使用升級的 SQL Server 執行個體相關聯的 R 元件。 有兩個版本的工具： 精靈和命令列公用程式。

本文說明如何使用這些工具來升級的 SQL Server 相容的執行個體以及如何還原先前已升級執行個體。

您不需要使用此升級程序，如果您想要取得升級為 SQL Server 更新的一部分。 每當您安裝新的 service pack 或版本更新服務時，機器學習元件會一律會自動升級為最新版本。 如果您想要升級的速度更快比 affored 了 SQL Server 服務版本的元件，只能使用這個 proess。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

> [!NOTE]
> 在撰寫本文時，升級只適用於相容的 SQL Server 2016 執行個體。  雖然升級都支援 SQL Server 2017，但是不已釋放 Microsoft Machine Learning 伺服器要用來升級的新版本。

## <a name="upgrade-an-instance"></a>升級執行個體

升級程序指**繫結**，因為它會變更為使用新的現代化生命週期原則的 SQL Server 機器學習元件支援模型。 不過，升級不會變更的 SQL Server 資料庫的支援模型。

一般情況下，此授權系統可確保您的資料科學家總是會使用最新版本的 R。如需有關新式生命週期原則條款的詳細資訊，請參閱 [Microsoft R Server 的支援時間表 (英文)](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support)。

當您繫結執行個體時，會發生幾件事：

+ 支援模型會變更。 而不要依賴 SQL Server 服務版本，支援根據新的現代化生命週期原則。
+ 機器學習服務執行個體相關聯的元件會使用鎖定-步驟是在新的現代化生命週期原則的最新的版本中的每個版本中，會自動升級。 
+ 可能會加入新的 R 或 Python 封裝。 例如，從 Microsoft R Server 先前的更新加入新的 R 封裝，例如[MicrosoftML](../using-the-microsoftml-package.md)， [olapR](../r/how-to-create-mdx-queries-using-olapr.md)，和[sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)。
+ 執行個體不再以手動方式更新，除非是加入新套件。
+ 您可以選擇加入預先定型的模型。

如果您稍後決定您想要停止升級每個發行版本執行個體，您必須**解除繫結**中所述的執行個體[本節](#bkmk_Unbind)，然後再解除安裝機器學習所述的升級本文章中：[執行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。 處理程序完成時，未來的機器學習機器學習 Server 為基礎的升級將不再套用至執行個體。

### <a name="bkmk_prereqs"></a>升級的必要條件

1. 識別適合升級的執行個體。
    + 已安裝 R 服務的 SQL Server 2016
    + 至少要有 Service Pack 1 加上 CU3

2. 取得**Microsoft R Server**，下載個別的 Windows 安裝程式。

    [如何使用獨立 Windows Installer 在 Windows 上安裝 R Server 9.0.1 (英文)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)

> [!TIP]
> 
> 找不到 SqlBindR.exe？ 您可能有 R 伺服器尚未下載。 此公用程式是僅適用於 Microsoft R Server 的 Windows 安裝程式。

### <a name="bkmk_BindWizard"></a>使用新的安裝精靈升級

1. R 伺服器的新安裝程式在電腦上啟動具有您想要升級的執行個體。
  ![Microsoft R Server 安裝精靈](media/r-server-installer-01.PNG)
2. 接受授權合約的 Microsoft R Server 9.1.0，然後按一下 **下一步**。
3. 接受的授權條件開放原始碼 R 的元件，然後按一下 **下一步**。
4. 在**選取安裝資料夾**，接受預設值，或指定不同的位置將會安裝 R 程式庫。 
5. 安裝程式會識別任何屬於對象的繫結的本機執行個體。 如果沒有任何執行個體都會顯示，表示找到有效的執行個體。 您可能需要以修補伺服器，或檢查是否已安裝 R Services。
6. 選取您要升級，請按一下任何執行個體旁邊的核取方塊**下一步**。
7. 處理程序可能需要一段。
    
    在安裝期間，SQL Server R 服務所使用的 R 程式庫會取代文件庫的 Microsoft R Server 9.1.0。
    
    啟動控制板不會受到此程序，但是 R_SERVICES 資料夾中的程式庫將會移除，而且服務的屬性會變更，為使用中的程式庫`C:\Program Files\Microsoft\R Server\R_SERVER`。

### <a name="bkmk_BindCmd"></a>使用命令列升級

已安裝 Microsoft R 伺服器之後，您可以從命令列執行 SqlBindR.exe 工具。

1. 以系統管理員身分開啟命令提示字元，並瀏覽至包含 sqlbindr.exe 的資料夾。 預設位置是`C:\Program Files\Microsoft\R Server\Setup`
2. 輸入下列命令以檢視可用的執行個體清單︰ `SqlBindR.exe /list`
  
   請記下列出的完整執行個體名稱。 可能的執行個體名稱，例如`MSSQL13.MSSQLSERVER`預設執行個體，或類似`SERVERNAME.MYNAMEDINSTANCE`。
3. 使用 */bind* 引數執行 **SqlBindR.exe** 命令，並指定要升級的執行個體名稱，如上一個步驟中所傳回。

   例如，若要升級的預設執行個體，請輸入：`SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
4. 升級完成後，請重新啟動與任何已修改的執行個體相關的 Launchpad 服務。


## <a name="bkmk_Unbind"></a>還原或解除繫結執行個體

若要還原的 SQL Server 使用 SQL Server 所安裝的原始程式庫執行個體，您必須執行**解除繫結**作業。 您可以重新執行安裝程式精靈，Microsoft R server，或從命令列執行 SqlBindR 公用程式。

解除繫結時完成，請移除 Microsoft R Server 9.1.0 的程式庫，並會還原原始 SQL Server R 服務所使用的 R 程式庫。

SQL Server Launchpad 的內容會編輯要在預設資料夾中的 R 程式庫用於在 R_SERVICES， `C:\Program Files\Microsoft\R Server\R_SERVER`。

### <a name="unbind-using-the-wizard"></a>解除繫結使用精靈

1. 下載 Microsoft R Server 9.1.0 的新安裝程式。
2. 在具有您想要解除繫結的執行個體的電腦上執行安裝程式。
2. 安裝程式會識別會被解除繫結的本機執行個體。
3. 取消選取您想要還原為原始的 SQL Server R Services 設定的執行個體旁邊的核取方塊。
4. 接受 Microsoft R Server 9.1.0 的授權合約。 即使您要移除 R 伺服器，您必須接受授權合約。
5. 按一下 **[完成]**。 處理程序需要一些時間。

### <a name="unbind-using-the-command-line"></a>使用命令列解除繫結

1. 開啟命令提示字元並瀏覽至包含 **sqlbindr.exe** 的資料夾，如上一節所述。

2. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。

   例如，下列命令會還原預設執行個體：
   
    `SqlBindR.exe /unbind MSSQL13.MSSQLSERVER`

## <a name="known-issues"></a>已知問題

此區段會列出特有 SqlBindR.exe 公用程式，或使用 Microsoft R Server 安裝程式公用程式的升級會影響 SQL Server 執行個體所使用的已知的問題。

### <a name="restoring-packages-that-were-previously-installed"></a>還原先前安裝的封裝

在隨附於 Microsoft R Server 9.0.1 升級公用程式，此公用程式不能還原原始的封裝或 R 元件完整地要求使用者執行修復，在執行個體，套用所有的服務版本，然後再重新啟動執行個體。

不過，最新版本的升級的公用程式，Microsoft R server 9.1.0，將會自動還原原始 R 功能。 因此，您應該不需要重新安裝的 R 元件，或重新修補程式的伺服器。 不過，您仍然需要安裝任何可能在初始安裝後加入的 R 封裝。

如果您已經使用封裝管理角色來安裝及共用封裝，這項工作就能輕鬆： 您可以使用 R 命令來同步處理已安裝的封裝，在資料庫中，使用記錄在檔案系統，反之亦然。 如需詳細資訊，請參閱[安裝和管理的 R 封裝](installing-and-managing-r-packages.md)

### <a name="cannot-perform-upgrade-from-901"></a>無法從 9.0.1 執行升級

如果 SQL Server 2016 R Services 的執行個體先前已升級 9.0.1，當您執行 Microsoft R Server 9.1.0 的新安裝程式時，它會顯示所有有效的執行個體的清單，然後選取 預設的 先前繫結的執行個體。 如果您繼續時，先前繫結的執行個體將會解除繫結。 如此一來，較早 9.0.1 會移除安裝，包括任何相關的封裝，但不是安裝 Microsoft R Server (9.1.0) 的新版本。

因應措施，您可以修改現有的 R 伺服器安裝，如下所示：
1. 在控制台中開啟**新增或移除程式**。
2. 找出 Microsoft R Server，然後按一下**變更/修改**。
3. 安裝程式啟動時，選取您想要繫結至 9.1.0 的執行個體。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>繫結或解除繫結會保留多個暫存資料夾

有時繫結和解除繫結作業無法清除暫存資料夾。
如果您發現具有類似名稱的資料夾，您可以移除它，安裝完成之後：`R_SERVICES_<guid>`

> [!NOTE]
> 請務必等候安裝完成。 可能需要很長的時間，若要移除與版本相關聯的 R 程式庫，然後再加入新的 R 程式庫。 當作業完成時，將會移除暫存資料夾。

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe 命令語法

### <a name="usage"></a>使用方式

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|名稱|Description|
|------|------|
|*list*| 顯示目前電腦上所有 SQL 資料庫執行個體識別碼的清單|
|*bind*| 將指定的 SQL 資料庫執行個體升級到最新版 R Server，並確保執行個體自動取得 R Server 的未來升級|
|*unbind*|從指定的 SQL 資料庫執行個體解除安裝最新版的 R Server，並防止未來的 R Server 升級影響執行個體|

### <a name="errors"></a>錯誤

工具會傳回下列錯誤訊息：

|錯誤|解決方案|
|------|------|
|繫結執行個體時發生錯誤| 找不到執行個體。 請連絡支援部門以尋求協助。|
|執行個體已經繫結| 您執行了 *bind* 命令，但指定的執行個體已經繫結。 請選擇不同的執行個體。|
|執行個體尚未繫結| 您執行了 *unbind* 命令，但您指定的執行個體並未繫結。 請選擇另一個相容的執行個體。|
|不是有效的 SQL 執行個體識別碼| 您可能輸入了錯誤的執行個體名稱。 請使用 *list* 引數再次執行命令，查看可用的執行個體識別碼。|
|找不到任何執行個體| 這部電腦沒有 SQL Server R Services 的執行個體。|
|執行個體必須安裝相容版本的 SQL R Services (資料庫內)。| 請參閱本主題中的相容性需求以取得詳細資料。|
|解除繫結執行個體時發生錯誤| 無法解除繫結執行個體。 請連絡支援部門以尋求協助。|
|發生意外的錯誤| 其他錯誤。 請連絡支援部門以尋求協助。  |
|找不到任何 SQL 執行個體| 這部電腦沒有 SQL Server 的執行個體。 |

如需詳細資訊，請參閱 Microsoft R server 的版本資訊：

+ [什麼是 R Server 的新功能](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [R 伺服器的已知問題](https://docs.microsoft.com/r-server/resources-known-issues)

