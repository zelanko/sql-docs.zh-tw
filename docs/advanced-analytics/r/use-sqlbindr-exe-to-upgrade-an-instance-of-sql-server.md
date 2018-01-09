---
title: "升級 SQL Server 執行個體中的機器學習元件 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 424e7d86a00901c22220d19e86b1bbced698d850
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>升級 SQL Server 執行個體中的機器學習元件

本文說明的程序_繫結_，可用來升級機器學習 SQL Server 中所使用的元件。 更新頻率，根據機器學習伺服器版本的繫結程序鎖定伺服器，而不是使用 SQL Server 版本和更新排程。

> [!IMPORTANT]
> 您不需要使用此升級程序，如果您想要取得升級為 SQL Server 更新的一部分。 每當您安裝新的 service pack 或版本更新服務時，機器學習元件會一律會自動升級為最新版本。 只使用_繫結_如果您想要更快的速度比 SQL Server 服務版本會提供在元件的升級程序。

如果您必須在您想要停止的機器學習伺服器排程上的 升級任何時間，_解除繫結_中所述的執行個體[本節](#bkmk_Unbind)，解除安裝機器學習服務伺服器。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="binding-vs-upgrading"></a>繫結與升級

升級的機器學習服務元件的程序指**繫結**，因為它會變更為使用新的現代化軟體生命週期原則的 SQL Server 機器學習元件支援模型。 

一般情況下，切換到新的授權模式可確保資料科學家可以一律使用最新版本的 R 或 Python。 如需現代的生命週期原則的術語的詳細資訊，請參閱[Microsoft R Server 的支援時間表](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)。

> [!NOTE]
> 升級不會變更的 SQL Server 資料庫的支援模型並不會變更的 SQL Server 版本。

當您繫結執行個體時，會發生幾件事：

+ 支援模型會變更。 而不要依賴 SQL Server 服務版本，支援根據新的現代化生命週期原則。
+ 每個版本中，在鎖定步驟是在新的現代化生命週期原則的最新的版本中，會自動升級執行個體相關聯的機器學習服務元件。 
+ 可能會加入新的 R 或 Python 封裝。 例如，根據 Microsoft R Server 9.1 先前的更新加入新的 R 封裝，例如[MicrosoftML](../using-the-microsoftml-package.md)， [olapR](../r/how-to-create-mdx-queries-using-olapr.md)，和[sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)。
+ 執行個體不再以手動方式更新，除非是加入新套件。
+ 您會安裝由 Microsoft 提供的預先定型的模型的選項。

## <a name="bkmk_prereqs"></a>Prerequisites

由識別候選項目以進行升級的執行個體開始。 如果您執行安裝程式，並選取的繫結選項，它會傳回一份相容進行升級的執行個體。

請參閱下表針對支援的升級和需求的清單。

| SQL Server 版本| 支援的升級| 注意|
|-----|-----|------|
| SQL Server 2016| 機器學習伺服器 9.2.1| 至少需要 Service Pack 1 加上 CU3。 必須安裝並啟用 R 服務。|
| SQL Server 2017| 機器學習伺服器 9.2.1| 必須安裝並啟用機器學習服務 （資料庫）。 |

## <a name="bind-or-upgrade-an-instance"></a>繫結，或升級執行個體

機器學習 Server for Windows 包含一個工具，您可以使用升級機器學習語言和工具的 SQL Server 執行個體相關聯。 有兩個版本的工具： 精靈和命令列公用程式。

您可以執行精靈或命令列工具之前，您必須下載最新版的機器學習服務元件的獨立安裝程式。

+ [安裝機器學習適用於 Windows Server 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ [下載所需的離線安裝元件](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="bkmk_BindWizard"></a>使用新的安裝精靈升級

1. 啟動新的安裝程式的機器學習服務伺服器。 請務必在具有您想要升級的執行個體的電腦上執行安裝程式。

    ![Microsoft Machine Learning 伺服器安裝精靈](media/mls-921-installer-start.PNG)

2. 在頁面上，**設定安裝**，確認要升級，元件，然後檢閱相容的執行個體的清單。 如果會不顯示任何執行個體，請檢查[必要條件](#bkmk_prereqs)。

    若要升級的執行個體，選取執行個體名稱旁的核取方塊。 如果您未選取執行個體，建立機器學習 Server 的個別安裝時，與 SQL Server 程式庫並不會變更。

    ![Microsoft Machine Learning 伺服器安裝精靈](media/configure-the-installation.PNG)

3. 在**授權合約**頁面上，選取**我接受這些條款**機器學習伺服器接受授權條款。 

4. 在後續頁面中，提供額外的授權條款，選取，例如 Microsoft R Open 或 Python Anaconda 發佈任何開放原始碼元件的同意。

5. 在**幾乎那里**頁面上，記下的安裝資料夾。 預設資料夾是`~\Program Files\Microsoft\ML Server`。

    如果您想要變更安裝資料夾，按一下**進階**返回精靈的第一頁。 不過，您必須重複先前的所有選項。

6. 如果您要安裝的元件離線，您可能會提示需要的機器學習元件，例如 Microsoft R Open、 Python 伺服器和 Python 開啟的位置。

在安裝過程中，會取代任何 SQL Server 所使用的 R 或 Python 程式庫，並啟動控制板會更新以使用較新的元件。 如此一來，執行個體之前會使用預設 R_SERVICES 資料夾中的程式庫，升級之後移除這些程式庫，並變更為 Launchpad 服務的屬性，以使用新的位置中的程式庫。

### <a name="bkmk_BindCmd"></a>使用命令列升級

如果您不想要使用此精靈，您可以安裝機器學習伺服器，然後再 SqlBindR.exe 工具從命令列升級執行個體。

> [!TIP]
> 
> 找不到 SqlBindR.exe？ 您可能已不下載上面所列的元件。 此公用程式是只能用於機器學習服務伺服器的 Windows 安裝程式。

1. 以系統管理員身分開啟命令提示字元，並瀏覽至包含 sqlbindr.exe 的資料夾。 預設位置是`C:\Program Files\Microsoft\MLServer\Setup`

2. 輸入下列命令以檢視可用的執行個體清單︰ `SqlBindR.exe /list`
  
   請記下列出的完整執行個體名稱。 可能的執行個體名稱，例如`MSSQL14.MSSQLSERVER`是預設執行個體，或類似`SERVERNAME.MYNAMEDINSTANCE`。

3. 執行**SqlBindR.exe**命令搭配*/繫結*引數，並指定要升級之執行個體名稱使用上一個步驟中傳回的執行個體名稱。

   例如，若要升級的預設執行個體，請輸入：`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 在升級完成後，請重新啟動任何已修改的執行個體相關聯的啟動控制板服務。

## <a name="bkmk_Unbind"></a>還原或解除繫結執行個體

如果您決定您不再想升級機器學習使用機器學習的伺服器元件，您必須先_解除繫結_執行個體，然後解除安裝機器學習的伺服器。

+ 解除繫結執行個體

    您可以解除繫結執行個體，並還原到原始 SQL Server 安裝的這兩種方法使用的媒體櫃：

    + [使用安裝精靈](#bkmk_wizunbind)機器學習伺服器，並取消選取的執行個體上的所有功能
    + [使用 SqlBindR 公用程式](#bkmk_cmdunbind)與`/unbind`引數，後面接著執行個體名稱。

    正在解除繫結程序完成時，未來的機器學習機器學習 Server 為基礎的升級將不再套用至執行個體。

+ 解除安裝機器學習服務伺服器

    如需指示，請參閱[解除安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-uninstall)。 

### <a name="bkmk_wizunbind"></a>解除繫結使用精靈

1. 找出機器學習服務伺服器的安裝程式。 如果您已經移除安裝程式，您可能需要下載一次，或將它複製從另一部電腦。
2. 請務必在具有您想要解除繫結的執行個體的電腦上執行安裝程式。
2. 安裝程式會識別會被解除繫結的本機執行個體。
3. 取消選取您想要還原為原始設定的執行個體旁邊的核取方塊。
4. 接受授權合約。 您必須在安裝時，指出您接受授權條款偶數。
5. 按一下 **[完成]**。 處理程序需要一些時間。

### <a name="bkmk_cmdunbind"></a>使用命令列解除繫結

1. 開啟命令提示字元並瀏覽至包含 **sqlbindr.exe** 的資料夾，如上一節所述。

2. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。

   例如，下列命令會還原預設執行個體：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

## <a name="known-issues"></a>已知問題

此區段會列出特有使用 SqlBindR.exe 公用程式，或升級的機器學習伺服器可能會影響 SQL Server 執行個體的已知的問題。

### <a name="restoring-packages-that-were-previously-installed"></a>還原先前安裝的封裝

在隨附於 Microsoft R Server 9.0.1 升級公用程式，此公用程式不能還原原始的封裝或 R 元件完整地要求使用者執行修復，在執行個體，套用所有的服務版本，然後再重新啟動執行個體。

不過，最新版的 「 升級 」 公用程式會自動還原原始的 R 功能。 因此，您應該不需要重新安裝的 R 元件，或重新修補程式的伺服器。 不過，您必須安裝任何可能在初始安裝後加入的 R 封裝。

如果您已經使用封裝管理角色來安裝及共用封裝，這項工作就能輕鬆： 您可以使用 R 命令來同步處理已安裝的封裝，在資料庫中，使用記錄在檔案系統，反之亦然。 如需詳細資訊，請參閱[for SQL Server 的 R 封裝管理](r-package-management-for-sql-server-r-services.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>從 SQL Server 的多個升級的問題

如果 SQL Server 2016 R Services 的執行個體先前已升級 9.0.1，當您執行 Microsoft R Server 9.1.0 的新安裝程式時，它會顯示一份所有有效的執行個體，並接著依預設會選取先前繫結的執行個體。 如果您繼續時，先前繫結的執行個體將會解除繫結。 如此一來，較早 9.0.1 會移除安裝，包括任何相關的封裝，但不是安裝 Microsoft R Server (9.1.0) 的新版本。

因應措施，您可以修改現有的 R 伺服器安裝，如下所示：
1. 在控制台中開啟**新增或移除程式**。
2. 找出 Microsoft R Server，然後按一下**變更/修改**。
3. 安裝程式啟動時，選取您想要繫結至 9.1.0 的執行個體。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>繫結或解除繫結會保留多個暫存資料夾

有時繫結和解除繫結作業無法清除暫存資料夾。
如果您發現具有類似名稱的資料夾，您可以移除它，安裝完成之後：`R_SERVICES_<guid>`

> [!NOTE]
> 請務必等候安裝完成。 可能需要很長的時間，若要移除與版本相關聯的 R 程式庫，然後再加入新的 R 程式庫。 當作業完成時，會移除暫存資料夾。

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe 命令語法

### <a name="usage"></a>使用方式

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|[屬性]|描述|
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

+ [機器學習伺服器中的已知的問題](https://docs.microsoft.com/machine-learning-server/resources-known-issues)

+ [從舊版的 R 伺服器的功能通知](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [已過時、 已停止或已變更的功能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
